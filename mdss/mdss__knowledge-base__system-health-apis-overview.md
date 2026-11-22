<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/system-health-apis-overview -->

# System Health APIs: which one to use

MDSS exposes three health endpoints on the API gateway. They answer different questions, so pick the one that matches what you want to know.

| Endpoint | Question it answers | Credentials | Available |
| ---- | ---- | ---- | ---- |
| `GET /api/health` | Is the API gateway process up? | None from 4.6.0. Before 4.6.0, the `ApiKey` header of any user. | All versions |
| `GET /api/readyz` | Can MDSS serve requests right now? | None | From 4.7.0 |
| `GET /api/healthz` | How is MDSS performing, and why? | `ApiKey` header of an administrator | All versions |

## Which one should I use?

- **A load balancer or monitor that needs up or down.** `GET /api/readyz` on MDSS 4.7.0 or later. On 4.6.x use `GET /api/health`; it stays `200` during a database, cache or broker outage, so it detects only a dead gateway. On 4.5.x and earlier `/api/health` needs an API key; a Read Only Administrator key is enough.
- **Kubernetes.** Liveness probe on `/api/health`, readiness probe on `/api/readyz`.
- **A script that waits for MDSS to start.** Poll `/api/health` until the process answers, then `/api/readyz` until MDSS is ready to log in and scan.
- **Slow scans, a pause or throttling.** `GET /api/healthz` with an administrator key, or the System tab in the UI. It explains the state and recommends an action.

## What each endpoint sees

|  | `/api/health` | `/api/readyz` | `/api/healthz` |
| ---- | ---- | ---- | ---- |
| API gateway process | yes | yes | yes |
| Cache, database and message broker connections | no | yes | no (database capacity only) |
| Discovery, Scanning and Remediations reporting | no | yes | yes |
| Storage guardrail pause and throttling | no | yes, as `Degraded` | yes, with reasons and limits |
| MetaDefender Core instances | no | yes, `Degraded` when none is reachable | yes, per instance |
| Host resources, throughput, recommendations | no | no | yes |

Never point a health check at `/`. It is a static page served by the web server and answers `200` even while the API is down.

## Examples

```bash
# Is the gateway process up?
curl -i https://<mdss-host>/api/health

# Can MDSS serve? 200 or 503, no credentials (4.7.0 and later)
curl -i https://<mdss-host>/api/readyz

# Full operational status, administrator API key
curl -s -H "ApiKey: <administrator-api-key>" https://<mdss-host>/api/healthz
```

## Detailed pages

- [Liveness API: GET /api/health](https://www.opswat.com/docs/mdss/knowledge-base/liveness-api--get--api-health)
- [Readiness API: GET /api/readyz](https://www.opswat.com/docs/mdss/knowledge-base/system-health-api---get--api-readyz)
- [System Health API: GET /api/healthz](https://www.opswat.com/docs/mdss/knowledge-base/system-health-api)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
