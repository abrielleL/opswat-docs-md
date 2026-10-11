<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/quick-start -->

# Quick start

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [**Prerequisites**](/docs/mdcluster/container-deployment/quick-start#prerequisites)

- **Kubernetes 1.31.x** with a `kubectl` context pointing at the cluster
- **Helm 3.x.**
- Access to a **container registry** holding the [MetaDefender Cluster images](https://hub.docker.com/r/opswat/metadefendercluster-debian).
- A valid MetaDefender **license key**.
- Requires LoadBalancer service support
- A default `StorageClass`, if you enable persistence for PostgreSQL or MetaDefender (MD) Cluster File Storage

**Do not use Network File System (NFS) for persistent volumes.** NFS can corrupt the MD Cluster File Storage metadata database and the PostgreSQL data directory. [Longhorn](https://longhorn.io/) is a tested alternative for on-cluster storage.

## [**Step 1 — Add the chart repository**](/docs/mdcluster/container-deployment/quick-start#step-1--add-the-chart-repository)

The charts are published in the OPSWAT Kubernetes chart repository:

The repository can be cloned locally:

git clone https://github.com/OPSWAT/metadefender-k8s.git metadefender
cd metadefender/helm_charts
## [**Step 2 — Prepare a values file**](/docs/mdcluster/container-deployment/quick-start#step-2--prepare-a-values-file)

Create your own values file — this guide calls it `override-values.yaml`

# override-values.yaml
# --- Images -----------------------------------------------------------------
DOCKER_REPO: 'opswat/metadefendercluster-debian'
# imagePullSecrets:
# - name: regcred
# --- Workers: replica count per instance type -------------------------------
workers:
ometascan:
replicas: 1
api-gateway:
replicas: 1
# --- Expose API Gateway service by load balancer ---
service:
type: LoadBalancer
callback-service:
replicas: 1
download-service:
replicas: 1
secrets:
# --- Bootstrap administrator account ---
ADMIN_USER: '<admin-account>'
ADMIN_PASSWORD: '<admin-password>'
ADMIN_EMAIL: '<admin-email>'
CONTROL_CENTER_ENCRYPTION_KEY: '<encryption-key>' # 32 alphanumeric characters
LICENSE_KEY: '<license-key>'
# --- Expose Control Center service by load balancer ---
# control-center:
# service:
# type: LoadBalancer
# --- Persistence ---------------------------------
postgres:
enabled: true
persistence:
enabled: true
size: 100Gi
maxConnections: 400 # Max number of connections from the clients
file-storage:
replicas: 1
persistence:
enabled: true
size: 100Gi
# Container-level.
securityContext:
readOnlyRootFilesystem: true # Change to false if not using a read-only file system.
## [**Step 3 — Install**](/docs/mdcluster/container-deployment/quick-start#step-3--install)

helm install mdcluster ./mdcl uster -f ./override-values.yaml --wait --timeout 5m
## [**Step 4 — Verify**](/docs/mdcluster/container-deployment/quick-start#step-4--verify)

kubectl get pods -w
kubectl get svc -w

- Access MD Cluster Control Center UI using external IP with port `8892`.
- Post file to MD Cluster using external IP of MD Cluster API Gateway with port `8899`.
