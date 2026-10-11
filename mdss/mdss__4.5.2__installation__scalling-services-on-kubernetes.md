<!-- source: https://www.opswat.com/docs/mdss/4.5.2/installation/scalling-services-on-kubernetes -->

# Scalling services on Kubernetes

**Applies to:** MetaDefender Storage Security Helm chart **4.5.x.**

This article lists which MDSS pods to run with more than one replica for a given workload and how to set the replica count.

For the baseline high-availability setup (two replicas of the web client and API gateway, external PostgreSQL, RabbitMQ and Redis), see [Replication & High Availability on K8S](https://www.opswat.com/docs/mdss/installation/replicas-on-k8s). This article is about throughput, not availability.

## Which pods to scale

Each storage type enabled in `ENABLED_MODULES` has its own deployment named `<module>-services`, for example `amazonsdk-services` for Amazon S3 or `azureblob-services` for Azure Blob. It performs all listing, download and remediation operations against that storage type.

### Real-time protection, event-based (example: Amazon S3)

Storage events reach MDSS as soon as objects are written, so every stage sees the load at the same time. The events enter through the web client, which forwards them to the API gateway. Scale these together:

| Deployment | Recommended replicas | Why |
| ---- | ---- | ---- |
| `webclient` | 2 | Receives every storage event and forwards it to the API gateway. |
| `apigateway` | 2 | Processes one HTTP call per storage event. |
| `discoveryservice` | 2 | Coordinates the processing of each event. |
| `amazonsdk-services` | 2 | Reads the objects from S3. Use the `<module>-services` pod of your storage type. |
| `scanningservice` | 2 | Feeds MetaDefender Core. Scale only if scanning is the bottleneck and Core has spare capacity. |

### Real-time protection, polling

Polling lists the storage on a fixed interval, so the load is a periodic listing job. Focus on discovery:

| Deployment | Recommended replicas | Why |
| ---- | ---- | ---- |
| `discoveryservice` | 3 | Runs the listing cycle. |
| `<module>-services` of the polled storage type | 3 | Executes the listing calls against the storage. |
| `scanningservice` | 2, only if scanning is the bottleneck | Feeds MetaDefender Core. |

`webclient` and `apigateway` are not part of the polling path.

### On-demand and scheduled scans of large storages

Discovery is fast compared to scanning, so `discoveryservice` does not need extra replicas here.

| Deployment | Recommended replicas | Why |
| ---- | ---- | ---- |
| `scanningservice` | 2 | Feeds MetaDefender Core. Make sure Core has spare capacity. |
| `<module>-services` of the scanned storage type | 2 | Lists and downloads the files. |

### Remediation configured (move, copy, delete, replace, quarantine)

| Deployment | Recommended replicas | Why |
| ---- | ---- | ---- |
| `remediationsservice` | 2 | Decides and dispatches the remediation actions. |
| `<module>-services` of the storage where the action runs | 2 | For move and copy actions this is the **destination** storage type. For delete, replace and tag actions it is the scanned storage type. |

Example: files scanned in S3 and moved to an Azure Blob quarantine container need 2 replicas of `remediationsservice`, `amazonsdk-services` and `azureblob-services`.

### Do not scale these pods

Keep these at 1 replica:

- `jobdispatcher`, `workflowmanagerservice`, `licensingservice`, `notificationservice`, `loggingservice`, `storagesservice`, `identityservice`
- `pgmigrations`, `postgres-mdss`, `rabbitmq`, `redis` (use external managed services for HA instead)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
