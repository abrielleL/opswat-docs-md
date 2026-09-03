<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/high-availability -->

# High availability

The bundled `postgres`, `redis` and `rabbitmq` are **single-pod** deployments. They exist so that a fresh install works out of the box and matches the Docker Compose stack — not for production. Each is a single point of failure whose loss stops the cluster.

MetaDefender Cluster Workers already running continue to serve traffic through a MetaDefender Cluster Control Center outage.

## [Choosing an approach](/docs/mdcluster/container-deployment/high-availability#choosing-an-approach)

In production, prefer a **managed service** from your cloud provider. Azure, AWS and Google Cloud all offer PostgreSQL-compatible databases with built-in high availability, backups and dynamic scaling — considerably less to operate than a database cluster you run yourself.

If the dependency must live inside the Kubernetes cluster, the options below are tested:

| Dependency | On-cluster solution |
| --- | --- |
| PostgreSQL | [CloudNativePG](https://cloudnative-pg.io/) operator, 3 instances |
| Redis | [dandydeveloper/redis-ha](https://github.com/DandyDeveloper/charts) (Redis + Sentinel), 3 nodes, HAProxy enabled |
| RabbitMQ | [RabbitMQ Cluster Operator](https://www.rabbitmq.com/kubernetes/operator/operator-overview), 3 nodes |

Namespace and DNS. The Service names below assume the HA components run in the same namespace as the mdcluster release. If they live elsewhere, use the fully qualified form `<service>.<namespace>.svc.cluster.local`.

## [RabbitMQ](/docs/mdcluster/container-deployment/high-availability#rabbitmq)

For production, use the official [RabbitMQ Cluster Operator](https://www.rabbitmq.com/kubernetes/operator/operator-overview).

The Bitnami community chart also works and is quicker to stand up, but note that it now ships images from the `bitnamilegacy` repository and is best-effort and unsupported.

Create `bitnami_rabbitmq.yaml`:

replicaCount: 3
persistence:
enabled: true
size: 50Gi
auth:
username: '<rabbitmq-user>'
password: '<rabbitmq-password>'
erlangCookie: '<erlang-cookie>'
image:
registry: docker.io
repository: bitnamilegacy/rabbitmq
global:
security:
allowInsecureImages: true
# resources:
# requests: { cpu: "4", memory: "8Gi" }
# limits: { cpu: "4", memory: "8Gi" }helm repo add bitnami https://charts.bitnami.com/bitnami
helm upgrade --install md-rabbitmq-ha bitnami/rabbitmq \
--version 16.0.14 -f ./bitnami_rabbitmq.yaml

This creates pods `md-rabbitmq-ha-0`, `-1` and `-2`, reachable through the headless Service `md-rabbitmq-ha-headless`.

## [Redis](/docs/mdcluster/container-deployment/high-availability#redis)

Create `dandy_redis.yaml`:

persistentVolume:
enabled: false
redis:
disableCommands: null # keep FLUSHDB/FLUSHALL enabled — the scan engines use them
haproxy:
enabled: true # required: gives one writable endpoint at md-redis-ha-haproxy:6379
# resources:
# requests: { cpu: "2", memory: "8Gi" }
# limits: { cpu: "2", memory: "8Gi" }
# sentinel:
# resources:
# requests: { cpu: "100m", memory: "256Mi" }
# limits: { cpu: "200m", memory: "512Mi" }helm repo add dandydev https://dandydeveloper.github.io/charts
helm upgrade --install md-redis-ha dandydev/redis-ha -f ./dandy_redis.yaml

This creates pods `md-redis-ha-server-0`, `-1` and `-2`, reachable through the `md-redis-ha` Service.

**Front the cluster with a single writable endpoint instead**. Either enable the chart's HAProxy (haproxy.enabled=true, giving one endpoint at md-redis-ha-haproxy:6379), or use a managed Redis that presents a single writable address.

## [PostgreSQL](/docs/mdcluster/container-deployment/high-availability#postgresql)

CloudNativePG runs PostgreSQL as an operator-managed cluster with automatic failover.

### [Create the credentials Secret](/docs/mdcluster/container-deployment/high-availability#create-the-credentials-secret)

`cloudpg_secret.yaml`:

apiVersion: v1
kind: Secret
metadata:
name: md-postgres-ha-secret
type: kubernetes.io/basic-auth
stringData:
username: '<db-user>' # must match the role name below
password: '<db-password>' # must match every *_DB_PASSWORD / *_PASSWORD value
### [Define the cluster](/docs/mdcluster/container-deployment/high-availability#define-the-cluster)

`cloudpg_cluster.yaml`:

apiVersion: postgresql.cnpg.io/v1
kind: Cluster
metadata:
name: md-postgres-ha
spec:
instances: 3
storage:
size: 100Gi
# storageClass: ""
# resources:
# requests: { cpu: "4", memory: "8Gi" }
# limits: { cpu: "4", memory: "8Gi" }
managed:
roles:
- name: '<db-user>'
passwordSecret:
name: md-postgres-ha-secret
login: true
createdb: true # required: the Control Center creates the four cluster databases
superuser: true
postgresql:
parameters:
log_min_duration_statement: "300" # log queries slower than 300ms
log_line_prefix: "%t [%p]: [%l-1] user=%u,db=%d,app=%a,client=%h "
log_checkpoints: "off"
log_connections: "off"
log_disconnections: "off"
log_lock_waits: "on"

The role needs `createdb` and `superuser` because the MetaDefender Cluster Control Center's database initialisation step creates the MetaDefender Cluster databases.

### [Deploy](/docs/mdcluster/container-deployment/high-availability#deploy)

Install the operator with cluster-admin privileges — the manifest creates cluster-scoped resources:

kubectl apply --server-side -f \
https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/release-1.30/releases/cnpg-1.30.0.yaml

Then apply the Secret and the cluster:

kubectl apply -f cloudpg_secret.yaml
kubectl apply -f cloudpg_cluster.yaml

CloudNativePG exposes three Services: `md-postgres-ha-rw` (the current primary, read-write), `md-postgres-ha-ro` (replicas) and `md-postgres-ha-r` (any instance). **MetaDefender Cluster must use -rw.** The endpoint follows the primary automatically on failover.

## [MetaDefender Cluster File Storage](/docs/mdcluster/container-deployment/high-availability#metadefender-cluster-file-storage)

File Storage is part of the `mdcluster` chart rather than an external dependency, but it holds submitted files and their metadata, so it needs its own treatment.

### [Configuration](/docs/mdcluster/container-deployment/high-availability#configuration)

env:
FILE_STORAGE_MIN_REPLICA: 2
FILE_STORAGE_MAX_REPLICA: 2
file-storage:
replicas: 3
persistence:
enabled: true # one PVC per replica; false means ephemeral emptyDir
size: 100Gi # per replica

`FILE_STORAGE_MIN_REPLICA` and `FILE_STORAGE_MAX_REPLICA` control how many copies of each file are stored. They are a redundancy factor, not a limit on how many instances the MetaDefender Cluster Control Center connects to.

| Setting | Meaning |
| --- | --- |
| `env.FILE_STORAGE_MIN_REPLICA` | Minimum copies of each file required for a write to succeed — **and** minimum healthy instances. |
| `env.FILE_STORAGE_MAX_REPLICA` | How many copies of each file to write |

This must hold:

`FILE_STORAGE_MIN_REPLICA` <= `FILE_STORAGE_MAX_REPLICA` <= `file-storage.replicas`

### [Requirements](/docs/mdcluster/container-deployment/high-availability#requirements)

**Persistence must be enabled.** With `persistence.enabled: false` each replica uses an ephemeral `emptyDir` and loses its files on restart, which defeats the point of running several.

**Each replica needs its own ReadWriteOnce volume.** Do not point the replicas at a single shared `ReadWriteMany` volume — each instance owns its own metadata database and expects exclusive access.

**Spread the replicas across nodes.** By default nothing prevents all MetaDefender Cluster File Storage pods from landing on the same node, which would make node loss a total outage. Add anti-affinity:

file-storage:
affinity:
podAntiAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
- topologyKey: kubernetes.io/hostname
labelSelector:
matchLabels:
app: file-storage

Use `requiredDuringScheduling` only if you have at least as many eligible nodes as replicas; otherwise the surplus pods stay `Pending`. Use `preferredDuringScheduling` for a best-effort spread. For zone-level fault tolerance, combine this with a zone-aware `StorageClass` — a pod cannot move to another zone if its volume is pinned to the first one.

## [Point MetaDefender Cluster at the external infrastructure](/docs/mdcluster/container-deployment/high-availability#point-metadefender-cluster-at-the-external-infrastructure)

Add the following to your values file. Passwords **must match** the RabbitMQ chart auth and the CloudNativePG role Secret exactly — a mismatch produces authentication failures at startup rather than a clear configuration error.

# Disable the bundled single-pod infrastructure
postgres: { enabled: false }
redis: { enabled: false }
rabbitmq: { enabled: false }
secrets:
CONTROL_CENTER_ENCRYPTION_KEY: '<32-character-key>'
ADMIN_APIKEY: '<control-center-api-key>'
# LICENSE_KEY: '<license-key>'
# PostgreSQL — all four pairs must match the CloudNativePG role
CONTROL_CENTER_DB_USER: '<db-user>'
CONTROL_CENTER_DB_PASSWORD: '<db-password>'
IDENTITY_DB_USER: '<db-user>'
IDENTITY_DB_PASSWORD: '<db-password>'
DATALAKE_USER: '<db-user>'
DATALAKE_PASSWORD: '<db-password>'
WAREHOUSE_USER: '<db-user>'
WAREHOUSE_PASSWORD: '<db-password>'
# RabbitMQ — must match bitnami_rabbitmq.yaml auth
RABBITMQ_USER: '<rabbitmq-user>'
RABBITMQ_PASSWORD: '<rabbitmq-password>'
# REDIS_USER / REDIS_PASSWORD — only if your Redis requires auth
env:
# PostgreSQL: always the read-write endpoint
CONTROL_CENTER_DB_HOST: 'md-postgres-ha-rw'
CONTROL_CENTER_DB_PORT: 5432
IDENTITY_DB_HOST: 'md-postgres-ha-rw'
IDENTITY_DB_PORT: 5432
DATALAKE_SERVICES: 'md-postgres-ha-rw:5432'
WAREHOUSE_SERVICES: 'md-postgres-ha-rw:5432'
# RabbitMQ: all three brokers
RABBITMQ_SERVICES: 'md-rabbitmq-ha-0.md-rabbitmq-ha-headless:5672,md-rabbitmq-ha-1.md-rabbitmq-ha-headless:5672,md-rabbitmq-ha-2.md-rabbitmq-ha-headless:5672'
# Redis: the single writable HAProxy endpoint, never the individual nodes
REDIS_SERVICES: 'md-redis-ha-haproxy:6379'
# File Storage: must be <= file-storage.replicas
FILE_STORAGE_MIN_REPLICA: 2
FILE_STORAGE_MAX_REPLICA: 2
# Multiple replicas of the stateful cluster services
file-storage:
replicas: 3
persistence: { enabled: true, size: 100Gi }
workers:
ometascan: { replicas: 3 }
api-gateway: { replicas: 2 }
callback-service: { replicas: 2 }

Install as usual:

helm install mdcluster ./mdcluster -f ./override-values.yaml
