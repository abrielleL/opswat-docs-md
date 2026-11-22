<!-- source: https://www.opswat.com/docs/mdss/4.6.1/knowledge-base/system-health-api -->

# System Health API: GET /api/healthz

**Applies to:** MetaDefender Storage Security (MDSS) 4.6.x and earlier, `GET /api/healthz`.

The request needs an API key of an administrator, sent in the `ApiKey` header. A health check that needs no API key will be available starting with MDSS 4.7.0.

## 1. Two status fields per service

Each entry in `perServiceStats` has two independent fields:

| Field | Question it answers | Values |
| ---- | ---- | ---- |
| `status` | Is the service processing normally? | `Healthy`, `Unhealthy` |
| `autoscalerStatus` | What is MDSS doing with the service's intake? | `Idle`, `Hold`, `Scaling Up`, `Scaling Down`, `Throttling`, `Paused` |

`Healthy` with `Hold` is the normal state of a busy system: the service works at the level its host, its queues and the scan instances allow, and MDSS keeps its intake there. A service is `Unhealthy` only while it is `Throttling` or `Paused`.

## 2. Autoscaler states

Every 10 seconds each service checks its host CPU and memory, its queues and, for Scanning, every scan instance. Each check is **Relieved**, **Warning** or **Critical**. From these the Scanning service raises or lowers its intake, the number of files it takes from its queue at a time. Discovery and Remediations only monitor: they report `Idle` or `Hold` and never scale.

| Value | Meaning | Enters when | Leaves when |
| ---- | ---- | ---- | ---- |
| `Idle` | Nothing to process. | The input queue is empty and nothing is in progress. | Work arrives. |
| `Scaling Up` | The intake is being increased. | Every check is Relieved with headroom to spare, confirmed 5 times in a row. `Hold` is shown while the confirmations are collected. | Right after the step. The next increase needs 5 new confirmations. |
| `Hold` | The intake stays where it is. The service runs at the level the system allows. | A check is in Warning but not yet for 2 consecutive runs, or every check is Relieved but close to its threshold, or confirmations for a scale-up are being collected, or throttling has just ended. Discovery and Remediations report `Hold` whenever they have work. | A check turns Critical (`Throttling`), a Warning persists (`Scaling Down`), headroom is confirmed (`Scaling Up`), or the work runs out (`Idle`). |
| `Scaling Down` | The intake is being reduced. | A check stayed in Warning for 2 consecutive runs: CPU above 90 %, memory above 80 %, the output queue above 70 % of its capacity, or a scan instance above its desired load. | Right after the step. |
| `Throttling` | The intake was halved at once to protect the system. The service is `Unhealthy`. | Any check is Critical: CPU at 95 % or more, memory at 90 % or more, the output queue at its critical size, or a scan instance returning too many errors. Discovery also throttles when one of its pending-file queues exceeds its limit. | After 30 seconds, if nothing is Critical any more; extended by 30 seconds while something still is. The service returns to `Hold`, never straight to `Scaling Up`. |
| `Paused` | File processing is stopped by the storage guardrail. All services are `Unhealthy`. | The MDSS disk, the database volume or the database size reaches 90 % of its capacity. | Every guardrail signal is back at 80 % or less. Checked every 30 seconds. |

## 3. Overall status

The top-level `status` uses the same six values, chosen in this order:

1. `Paused`, if the guardrail has paused processing. `statusReason` is then `Disk` or `Database`.
2. `Throttling`, if Discovery is throttling.
3. Otherwise the most severe state of the Scanning replicas: `Throttling`, then `Scaling Up`, `Scaling Down`, `Hold`, `Idle`.
4. `Idle`, if no Scanning replica has reported in the last 3 minutes.

## 4. Scan instances

`scanningInstancesStats` reports each MetaDefender Core, Cloud or Cluster instance as the Scanning service sees it.

| `status` | `reason` | Meaning |
| ---- | ---- | ---- |
| `Healthy` | `null` | The instance keeps up. |
| `Unhealthy` | `Overloaded` | The instance's queue is above the load MDSS wants to keep on it. MDSS sends it less. |
| `Unhealthy` | `429Responses` | More than 10 % of the last 100 responses were "429 Too Many Requests". MDSS scales down. |
| `Critical` | `BadResponses` | More than 10 % of the last 100 responses were errors. MDSS throttles scanning. |

## 5. Limits

`activeLimit`, `perServiceStats[].currentLimit` and `perServiceStats[].reason` name the resource that stops a service from taking more work. `activeLimit` is `null` when nothing limits the system; otherwise it is the first of these reported by any service:

| Value | Meaning |
| ---- | ---- |
| `Disk` | The MDSS disk is full enough to pause processing. |
| `Database` | The database volume or the database size is full enough to pause processing. |
| `Memory` | Host memory is the limit. |
| `Cpu` | Host CPU is the limit. |
| `Scanning Instances` | The scan instances are the limit. |
| `OutputThroughput` | Only in `reason`: the service throttles because its output queue cannot drain fast enough. |

## 6. Recommendations

`currentRecommendation` is `null` when there is nothing to recommend. Otherwise `severity` is `Critical` while processing is paused, `Warning` while a limit is active and `Info` otherwise, and `key` is one of:

| `key` | Shown when |
| ---- | ---- |
| `REST_API_MSG_RECOMMENDATION_INCREASE_SPECS` | The host is below the minimum specification: 16 vCPU and 32 GB, or 32 vCPU and 64 GB when MetaDefender Core runs on the same host. |
| `REST_API_MSG_RECOMMENDATION_INCREASE_STORAGE` | Processing is paused by the guardrail and the database is external. |
| `REST_API_MSG_RECOMMENDATION_USE_EXTERNAL_DB` | Processing is paused by the guardrail with a local database, or the local database is larger than 100 GB. |
| `REST_API_MSG_RECOMMENDATION_INCREASE_CPU` | Host CPU is the limit. |
| `REST_API_MSG_RECOMMENDATION_INCREASE_MEMORY` | Host memory is the limit. |
| `REST_API_MSG_RECOMMENDATION_USE_EXTERNAL_MDCORE` | The scan instances are the limit and MetaDefender Core runs on the MDSS host. |
| `REST_API_MSG_RECOMMENDATION_INCREASE_MDCORE_PERFORMANCE` | The scan instances are the limit and MetaDefender Core is external. |
| `REST_API_MSG_RECOMMENDATION_USE_EXTERNAL_CACHE` | Memory was the last limit and Redis runs on the MDSS host. |

A recommendation stays visible after its limit clears, until another limit replaces it.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/4.6.1/llms.txt)
