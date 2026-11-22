<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/system-health-api---get--api-readyz -->

# Readiness API: GET /api/readyz

**Applies to:** MetaDefender Storage Security (MDSS) **4.7.0 and later**. Earlier versions do not have this endpoint and answer `401` or `404` on this path.

**Credentials:** none. The endpoint needs no API key, `Authorization` header or cookie. Credentials sent anyway are ignored.

`GET /api/readyz` reports whether this MDSS instance can serve requests. It is meant for load balancers, uptime monitors and Kubernetes readiness probes.

- Takes no parameters.
- The HTTP status code carries the verdict: `200` ready, `503` not ready. The body has the same shape in both cases.
- Every answer is current (`Cache-Control: no-store`) and is read from state the gateway already holds. A probe never queries the database, the cache or the broker itself, so any polling interval is safe.
- The body holds only statuses and short reason codes: no URLs, versions, sizes or keys.

```json
{
  "status": "Healthy",
  "components": {
    "cache":         { "status": "Healthy" },
    "database":      { "status": "Healthy" },
    "messageBroker": { "status": "Healthy" },
    "discovery":     { "status": "Healthy" },
    "scanning":      { "status": "Healthy" },
    "remediation":   { "status": "Healthy" }
  }
}
```

### Statuses

| Status | HTTP | Meaning |
| ---- | ---- | ---- |
| `Healthy` | 200 | Everything reports fine. |
| `Degraded` | 200 | MDSS serves requests, but something needs attention: processing paused by the storage guardrail, throttling, a replica missing, or no scan instance reachable. |
| `Unhealthy` | 503 | MDSS cannot serve: the cache, database or message broker is unreachable, or a core service is not reporting. |

The overall `status` is the worst component status. A component carries a `reason` only when it is not `Healthy`.

### Reasons

| Reason | Status | On | Meaning |
| ---- | ---- | ---- | ---- |
| `Unreachable` | Unhealthy | cache, database, messageBroker | The gateway's connection is down, or its check failed or timed out. |
| `Blocked` | Unhealthy | messageBroker | RabbitMQ has blocked the connection because of a memory or disk alarm on the broker. Nothing can be published. |
| `NotChecked` | Unhealthy | any | No check has completed yet (start-up), or the last result is older than 15 s. |
| `NotReporting` | Unhealthy | discovery, scanning, remediation | No replica of the service has sent a health report within its freshness window: the service is stopped, crashed or hung. |
| `Paused` | Degraded | discovery, scanning | Processing is paused by the storage guardrail: machine disk, database size or database disk at a critical level. |
| `NoInstanceReachable` | Degraded | scanning | Every MetaDefender Core instance returned errors on recent scan requests. |
| `Throttling` | Degraded | discovery, scanning, remediation | The service is throttling its intake because of resource or queue pressure. |
| `ReplicaMissing` | Degraded | discovery, scanning, remediation | One replica stopped reporting while another replica of the same service still reports. |

When several reasons apply to one component, the first in this order is reported: `NotReporting`, `Paused`, `NoInstanceReachable`, `Throttling`, `ReplicaMissing`.

## How the status is tracked

| Component | What is watched | Refreshed | Goes down after | Comes back after |
| ---- | ---- | ---- | ---- | ---- |
| `cache` | The state of the gateway's own Redis connection | every 5 s | up to 5 s | up to 10 s: reconnect plus one cycle |
| `database` | The gateway's own queries. One `SELECT 1` with a 3 s timeout runs only when no query answered in the last 5 s or a connection failure was seen. | every 5 s | up to 10 s | up to 10 s |
| `messageBroker` | The state of the gateway's own RabbitMQ connection | every 5 s | up to 5 s | up to 5 s |
| `discovery`, `scanning`, `remediation` | Health reports every service broadcasts over RabbitMQ, every 10 s by default | on each report | `NotReporting` after 3 missed reports: about 30 s after a crash or hang, immediately after a clean stop | up to 10 s: the first report of the restarted service |
| `Paused` | The storage guardrail in the Job Dispatcher: checked every 30 s, sent in its health report every 60 s | on each report | up to 90 s after a capacity signal turns critical | up to 90 s after every signal is back to normal. Resume is automatic only while all signals can be measured. |
| `Throttling` | The autoscaler state of the service, plus the discovery queue thresholds | on each report | up to 10 s | when pressure is relieved or the service is idle. The autoscaler holds Throttle for at least 30 s. |

Over time:

- **Start-up.** The gateway answers `503` until its first checks run and the first report of every service arrives, about 10 to 20 s after it starts. The components show `NotChecked` or `NotReporting`.
- **One instance at a time.** Each API gateway answers for itself. Behind a load balancer, probe every instance.
- **Forgotten replicas.** A replica silent for 180 s is removed. Until then it shows as `ReplicaMissing` if another replica of the same service still reports, or `NotReporting` if none does.
- **Logging.** The gateway logs a state change once: `Readiness check: the Database is Unhealthy (Unreachable)` and later `Readiness check: the Database is reachable again`. A `503` answered to a probe is logged at Information, not Error.

## Examples

### Call it

```bash
curl -i https://<mdss-host>/api/readyz
```

Only the HTTP code:

```bash
curl -s -o /dev/null -w "%{http_code}\n" https://<mdss-host>/api/readyz
```

Only the components that are not healthy:

```bash
curl -s https://<mdss-host>/api/readyz | jq '.components | to_entries[] | select(.value.status != "Healthy")'
```

### Database unreachable: `503 Service Unavailable`

```json
{
  "status": "Unhealthy",
  "components": {
    "cache":         { "status": "Healthy" },
    "database":      { "status": "Unhealthy", "reason": "Unreachable" },
    "messageBroker": { "status": "Healthy" },
    "discovery":     { "status": "Healthy" },
    "scanning":      { "status": "Healthy" },
    "remediation":   { "status": "Healthy" }
  }
}
```

`/api/health` still answers `200` in this state: the process is alive, but it cannot serve.

### Paused by the storage guardrail: `200 OK`

```json
{
  "status": "Degraded",
  "components": {
    "cache":         { "status": "Healthy" },
    "database":      { "status": "Healthy" },
    "messageBroker": { "status": "Healthy" },
    "discovery":     { "status": "Degraded", "reason": "Paused" },
    "scanning":      { "status": "Degraded", "reason": "Paused" },
    "remediation":   { "status": "Healthy" }
  }
}
```

The instance stays in the load balancer rotation. Free disk or database space, and the status returns to `Healthy` by itself.

### Load balancer health check

| Setting | Value |
| ---- | ---- |
| Path | `/api/readyz` |
| Success codes | `200` |
| Interval | 10 to 30 s |
| Timeout | 5 s |
| Unhealthy threshold | 2 |
| Healthy threshold | 2 |

Do not point the health check at `/`: it is a static page served by the web server and answers `200` even while the API is down.

### Kubernetes readiness probe

```yaml
readinessProbe:
  httpGet:
    path: /api/readyz
    port: https
  periodSeconds: 10
  timeoutSeconds: 5
  failureThreshold: 3
```

### What you see during an Amazon MQ (RabbitMQ) maintenance

1. A broker node restarts. Within 5 s `/api/readyz` answers `503`, `messageBroker: Unreachable`.
2. Every MDSS service restarts after losing the broker. While the API gateway restarts, the web server answers `502` on every endpoint, `/api/health` included, for a few seconds up to about half a minute.
3. The gateway is back: `503` with `NotChecked` or `NotReporting` for about 20 s while its checks and the service reports arrive.
4. Every service reports: `200`, `Healthy`.

If `503` with `NotReporting` persists for more than 2 to 3 minutes after the maintenance has ended, a service did not come back. Run `sudo mdss -c restart` on Linux, or restart the MDSS services on Windows.

## Limitations

- A Redis that is frozen but keeps its connection open still shows `cache: Healthy`. A stopped or killed Redis is detected. Tracked in MDSS-15082.
- `NoInstanceReachable` reflects the errors the scanning service saw on recent scan requests. It is not a direct check of MetaDefender Core, and with no recent scans `scanning` stays `Healthy`.
- On MDSS Cloud and other multi-tenant deployments `/api/health` and `/api/readyz` answer without a tenant cookie and report deployment-level state only.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
