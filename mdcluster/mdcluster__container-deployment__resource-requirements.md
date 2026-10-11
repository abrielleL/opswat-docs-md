<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/resource-requirements -->

# Resource requirements

View as Markdown Ask ChatGPT about this page Ask Claude about this page

By default, the charts set no resource requests or limits. For any environment carrying real traffic, set requests and limits explicitly.

## [**The published baseline**](/docs/mdcluster/container-deployment/resource-requirements#the-published-baseline)

Per-component minimums are maintained in [System requirements](/docs/mdcluster/installation/md-cluster-system-requirements):

| Component | CPU | Memory | Storage |
| --- | --- | --- | --- |
| `postgres` | 8 | 16Gi | 1Ti SSD/NVMe |
| `redis` | 2 | 32Gi | 20Gi |
| `rabbitmq` | 4 | 8Gi | 100Gi |
| `file-storage` | 8 | 8Gi | 1Ti SSD/NVMe |
| `control-center` | 4 | 4Gi | 100Gi |
| `identity-service` | 4 | 4Gi | 50Gi |
| `api-gateway` | 4 | 8Gi | 50Gi |
| `callback-service` | 4 | 4Gi | 50Gi |
| `download-service` | 4 | 4Gi | 50Gi |
| `ometascan` | See the [MetaDefender Core requirements](https://www.opswat.com/docs/mdcore) |  |  |

## [**Assigning CPU and memory**](/docs/mdcluster/container-deployment/resource-requirements#assigning-cpu-and-memory)

1. Requests and limits use the standard Kubernetes `resources` block. Every component in both charts accepts it. Update `override-values.yaml` in [Quick start](/docs/mdcluster/container-deployment/quick-start)

# --- Instance ---
workers:
ometascan:
resources:
requests: { cpu: "4", memory: 4Gi, ephemeral-storage: 200Gi }
limits: { cpu: "8", memory: 16Gi, ephemeral-storage: 200Gi }
# The API Gateway and Callback Service have the same allowance.
api-gateway:
resources:
requests: { cpu: "4", memory: 4Gi, ephemeral-storage: 50Gi }
limits: { cpu: "4", memory: 4Gi, ephemeral-storage: 50Gi }
callback-service:
resources:
requests: { cpu: "4", memory: 8Gi, ephemeral-storage: 50Gi }
limits: { cpu: "4", memory: 8Gi, ephemeral-storage: 50Gi }
download-service:
resources:
requests: { cpu: "4", memory: 4Gi, ephemeral-storage: 50Gi }
limits: { cpu: "4", memory: 4Gi, ephemeral-storage: 50Gi }
# --- Services ---
control-center:
resources:
requests: { cpu: "2", memory: 4Gi, ephemeral-storage: 100Gi }
limits: { cpu: "4", memory: 4Gi, ephemeral-storage: 100Gi }
identity-service:
resources:
requests: { cpu: "1", memory: 1Gi, ephemeral-storage: 50Gi }
limits: { cpu: "2", memory: 2Gi, ephemeral-storage: 50Gi }
file-storage:
resources:
requests: { cpu: "2", memory: 4Gi }
limits: { cpu: "8", memory: 8Gi }
persistence:
enabled: true
size: 100Gi
postgres:
resources:
requests: { cpu: "4", memory: 8Gi }
limits: { cpu: "8", memory: 8Gi }
persistence:
enabled: true
size: 100Gi

2. Apply config

helm upgrade mdcluster ./mdcluster --install -f ./override-values.yaml
