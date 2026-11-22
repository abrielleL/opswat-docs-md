<!-- source: https://www.opswat.com/docs/mdss/4.6.1/knowledge-base/liveness-api--get--api-health -->

# Liveness API: GET /api/health

`GET /api/health` tells you whether the MDSS API gateway process is up and answering HTTP requests. It checks nothing else.

**Available in all versions. No API key is needed from MDSS 4.6.0.** On 4.5.x and earlier, send the `ApiKey` header of any user; a Read Only Administrator key is enough.

## Request

| Parameter | Required | Effect |
| ---- | ---- | ---- |
| `verbose=true` | no | Adds the body `{"apiStatus":"Ok"}`. Without it the `200` answer has an empty body. |

The endpoint runs no query against the database, the cache or the message broker, and it does not ask the other MDSS services. It is safe to poll at any interval.

## Response

| HTTP | Body | Meaning |
| ---- | ---- | ---- |
| `200` | empty, or `{"apiStatus":"Ok"}` with `verbose=true` | The gateway process is up. |
| `502` | web server error page | The gateway is down or restarting. The web server in front of it could not reach it. |
| `401` |  | Only on 4.5.x and earlier, when no `ApiKey` header was sent. |

## What it does not tell you

`/api/health` keeps answering `200` while the database, the cache or the message broker is unreachable, and while Discovery, Scanning or Remediations are stopped. Users cannot log in or scan in those states, yet the process is alive.

- On MDSS 4.7.0 and later, use `GET /api/readyz` for that question. It needs no credentials either and answers `503` when MDSS cannot serve.
- On MDSS 4.6.x and earlier, `GET /api/healthz` with an administrator API key shows the state of each service.

## Examples

### Call it

```bash
curl -i https://<mdss-host>/api/health
curl -i "https://<mdss-host>/api/health?verbose=true"
```

```plaintext
HTTP/1.1 200 OK
Content-Type: application/json

{"apiStatus":"Ok"}
```

On 4.5.x and earlier:

```bash
curl -i -H "ApiKey: <read-only-administrator-api-key>" https://<mdss-host>/api/health
```

### Wait for the gateway to come up

```bash
until [ "$(curl -s -o /dev/null -w '%{http_code}' https://<mdss-host>/api/health)" = "200" ]; do
  sleep 5
done
echo "API gateway is up"
```

### Kubernetes liveness probe

```yaml
livenessProbe:
  httpGet:
    path: /api/health
    port: https
  periodSeconds: 10
  timeoutSeconds: 5
  failureThreshold: 3
```

### Why not `/`?

A web server that has lost its connection to the gateway still serves the login page at `/` with `200`. The same web server answers `502` on `/api/health`. Point health checks at `/api/health` or `/api/readyz`, never at `/`.

## Notes

- Each API gateway answers for itself. Behind a load balancer, probe every instance.
- MDSS Cloud and other multi-tenant deployments: from 4.7.0 the endpoint answers without a tenant cookie.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/4.6.1/llms.txt)
