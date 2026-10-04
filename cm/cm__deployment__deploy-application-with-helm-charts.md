<!-- source: https://www.opswat.com/docs/cm/deployment/deploy-application-with-helm-charts -->

# Deploy Application with Helm Charts

## Prerequisites

Before installing MOCM, ensure the following infrastructure components are already provisioned and accessible:

- **Helm** >= 3.0.0 installed
- **kubectl** configured and connected to EKS cluster
- **MongoDB cluster** deployed and accessible
- **ALB** configured and ready

### MOCM Helm Chart

A comprehensive Helm chart for deploying MOCM (My OPSWAT Central Management) services in on-premise Kubernetes environments.

### Required Infrastructure

| Component | Version | Description |
| ---- | ---- | ---- |
| **Kubernetes** | v1.34+ | Cluster with sufficient resources |
| **MongoDB** | 8.0+ | Database (standalone or replica set) |
| **RabbitMQ** | Latest | Message broker (AmazonMQ or compatible) |
| **Redis** | Latest | Cache service (Amazon ElastiCache) |
| **S3 Storage** | -  | Object storage (AWS S3 or compatible) |
| **Container Registry** | -  | Repositories (AWS ECR or other registry) |

### CLI Tools

| Tools | Version | Description | Install |
| ---- | ---- | ---- | ---- |
| **Helm** | v3.x+ | Package manager for Kubernetes | [Installing Helm &#124; Helm](https://helm.sh/docs/intro/install/) |
| **Kubectl** | v1.34+ | The Kubernetes command-line tool | [Install Tools &#124; Kubernetes](https://kubernetes.io/docs/tasks/tools/) |
| **Helmfile** | v1.4.x | Helmfile is a declarative spec for deploying helm charts. | [Releases · helmfile/helmfile](https://github.com/helmfile/helmfile/releases/) |
| **AWS CLI** | v2.x+ | Required for ECR authentication | [https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |
| **OpenSSL** | 3.6.1+ | Required for generating the product agent RSA key pair | [Downloads &#124; OpenSSL Library](https://openssl-library.org/source/) |
| **Docker** | v20.x+ | Required for loading and pushing images to ECR | [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) |

### S3 Bucket Requirements

The following S3 buckets must be created (replace `{name_prefix}` with your environment prefix):

```yaml
# Required S3 buckets
{name_prefix}-fusion-updater
{name_prefix}-gears-cloud
{name_prefix}-gears-custom-scripts
{name_prefix}-gears-fusion-files
{name_prefix}-mdcore
{name_prefix}-mdfusion-vpack
```

**Example with name_prefix** `mocm`:

```yaml
mocm-fusion-updater
mocm-gears-cloud
mocm-gears-custom-scripts
mocm-gears-fusion-files
mocm-mdcore
mocm-mdfusion-vpack
```

### Repository Requirements

> **Important**
>
> The ECR must be created before running this step (replace <id> with your id account aws and <region> for your region)

```yaml
<id>.dkr.ecr.<region>.amazonaws.com/ma-tomcat
<id>.dkr.ecr.<region>.amazonaws.com/ma-base
<id>.dkr.ecr.<region>.amazonaws.com/fusion-be-go
<id>.dkr.ecr.<region>.amazonaws.com/fusion-be-cm-go
<id>.dkr.ecr.<region>.amazonaws.com/fusion-be-pmp-go
<id>.dkr.ecr.<region>.amazonaws.com/fusion-cm
<id>.dkr.ecr.<region>.amazonaws.com/fusion-lic
<id>.dkr.ecr.<region>.amazonaws.com/fusion-fe
<id>.dkr.ecr.<region>.amazonaws.com/fusion-setup
```

If using another registry, repository must create

```yaml
fusion-be-go
fusion-be-cm-go
fusion-be-pmp-go
fusion-cm
fusion-fe
fusion-lic
fusion-setup
ma-base
ma-tomcat
```

### ALB Requirements

Note — ALB required: Single ALB with path-based routing: REST via Traefik, gRPC direct to connector service:

- ALB 1: Domain = "host", Protocol = HTTPS (443), Purpose = Main web traffic — UI, REST APIs, all HTTP-based services.

## Prepare

Download MOCM Kubernetes from My OPSWAT Portal and extract the MOCM on-premise package and verify the directory structure:

```yaml
# Extract the package
tar -xzf MyOPSWATCentralManagement_10.7.26062.9100.tar.gz
# Expected directory structure:
├── terraform/
│   ├── aws/       # AWS Infrastructure (OpenTofu + Ansible) — current release
│   ├── azure/     # Azure Infrastructure — TBD
│   ├── gcp/       # GCP Infrastructure — TBD
│   └── README.md
├── mocm/          # Helm charts for application deployment
├── scripts/			 # Script Generate RSA Key Pair for Product Agent
├── images/        # Container images and loading script
```

#### Tag and Push Images to Registry

```yaml
cd images
```

Inside folder images:

```yaml
├── fusion-be-go:<tag>
├── fusion-be-cm-go:<tag>
├── fusion-be-pmp-go:<tag>
├── fusion-cm:<tag>
├── fusion-fe:<tag>
├── fusion-lic:<tag>
├── fusion-setup:<tag>
├── images.txt
├── loadimage.sh
├── ma-base:<tag>
└── ma-tomcat:<tag>
```

---

#### **Prerequisites**: AWS CLI installed and configured with valid credentials. Docker must also be running.

Run the script:

```yaml
chmod +x loadimage.sh
./loadimage.sh
# When prompted:
AWS Account ID: <your-aws-account-id>
AWS Region:     <your-aws-region>   (e.g. us-west-2)
```

The script will:

1. Authenticate Docker to ECR automatically (`aws ecr get-login-password`)
2. Load every image tar file in the `images/` directory into Docker
3. For each image listed in `images.txt`, create the ECR repository if it does not exist, then tag and push the image

### Generate RSA Key Pair for Product Agent

`fusion-auth` and `fusion-connector` require an RSA key pair exposed as `PRODUCT_AGENT_RSA_PRIVATE_KEY`  / `PRODUCT_AGENT_RSA_PUBLIC_KEY`.

```bash
cd ../scripts
```

Contents of `scripts/`:

```plaintext
├── gen-cert.sh
└── gen-kek.sh
```

**Prerequisites**: OpenSSL installed.

Run the script:

```bash
chmod +x gen-cert.sh gen-kek.sh

./gen-cert.sh

# When prompted:

# Enter domain (e.g. mocm.example.com): your-domain;
```

The script will:

1. Create `./certs/` if it does not exist
2. Generate an OpenSSL config (`ssl.cnf`) and a self-signed certificate + RSA private key (`tls.crt`, `tls.key`, default 10 years)
3. Extract the public key into `public.key`

Output files in `./certs/`:

| File | Purpose |
| ---- | ---- |
| tls.key | RSA private key → `global.productKey.rsaPrivateKey` |
| public.key | RSA public key → `global.productKey.rsaPublicKey` |

Keep these files safe — they are used to populate `global.productKey` in `values.yaml`

```bash
./gen-kek.sh
```

e script prints a base64 key plus the exact `values.yaml` lines to paste.

> **Warning**: Set it **once**. It **cannot be changed** afterward — data encrypted
> with the old key would become undecryptable.

## Quick Start

Back to MOCM package folder

### Configure Values

Edit `values.yaml` with your environment details.

#### 1. Configuration

Update image, host, ingressclass and replicas in values.yaml

```yaml
image:
    registry: "<id>.dkr.ecr.<region>.amazonaws.com"
    tag: "<image_tag>" #Example: 10.4.2511
    pullPolicy: "IfNotPresent"
  host: "<domain_name>"
  ingressClassName: "<ingressclass_name>" #Example: traefik
  replicaCount: 2
```

`Host`: domain name for MOCM

If you need update replicas of one service, you can get svc and update replicas:

Example:

```yaml
componentReplicas:
    mk4InventoryApi: 3
    mdcoreLoad: 3
    maTomcat: 3
```

**NOTE** If you use Terraform (in the `terraform` folder) to install infrastructure, you can access AWS Secrets Manager in the AWS Console to retrieve the username and password for RabbitMQ and MongoDB.

For Redis OSS cache configuration:

- `REDIS_PRIMARY_HOST` is the primary endpoint.
- `REDIS_REPLICA_HOSTS` is the reader endpoint.

For the `admin-user` secret, these values are used to initialize the admin account login to the web console for managing MOCM.

#### 2. Configure credentials via values.yaml

Edit the `values.yaml` file to provide connection details and credentials. The file contains placeholders that need to be replaced with your actual values:

```yaml
global:
  secrets:
    - name: mongodb
      data:
        MONGODB_HOSTS: "< REPLACE_VALUE_MONGODB_HOSTS >"
        MONGODB_AUTH_USER: "< REPLACE_VALUE_MONGODB_AUTH_USER >"
        MONGODB_AUTH_PASSWORD: "< REPLACE_VALUE_MONGODB_AUTH_PASSWORD >"
        MONGODB_AUTH_DATABASE: "< REPLACE_VALUE_MONGODB_AUTH_DATABASE >"

    - name: rabbitmq
      data:
        RABBITMQ_HOST: "< REPLACE_VALUE_RABBITMQ_HOST_WITH_PORT >"
        RABBITMQ_USER: "< REPLACE_VALUE_RABBITMQ_USER >"
        RABBITMQ_PASSWORD: "< REPLACE_VALUE_RABBITMQ_PASSWORD >"

    - name: redis
      data:
        REDIS_PRIMARY_HOST: "< REPLACE_VALUE_REDIS_PRIMARY_ENDPOINT >"
        REDIS_REPLICA_HOSTS: "< REPLACE_VALUE_REDIS_READER_ENDPOINT >"

    - name: admin-user
      data:
        ADMIN_FIRST_NAME: "< REPLACE_VALUE_ADMIN_FIRST_NAME >"
        ADMIN_LAST_NAME: "< REPLACE_VALUE_ADMIN_LAST_NAME >"
        ADMIN_EMAIL: "< REPLACE_VALUE_ADMIN_EMAIL >"
        ADMIN_PASSWORD: "< REPLACE_VALUE_ADMIN_PASSWORD >"
```

**Note**: Replace all placeholder values with your actual configuration values before deployment.

Example:

```yaml
global:
  secrets:
    - name: mongodb
      data:
        MONGODB_HOSTS: your-mongodb-hosts:27017,your-mongodb-hosts:27017,your-mongodb-hosts:27017
        MONGODB_AUTH_USER: admin
        MONGODB_AUTH_PASSWORD: "your-mongodb-password"
        MONGODB_AUTH_DATABASE: admin

    - name: rabbitmq
      data:
        RABBITMQ_HOST: your-rabbitmq-host:5671
        RABBITMQ_USER: your-rabbitmq-user
        RABBITMQ_PASSWORD: "your-rabbitmq-password"

    - name: redis
      data:
        REDIS_PRIMARY_HOST: your-redis-host:6379
        REDIS_REPLICA_HOSTS: your-redis-host-ro:6379
        REDIS_USERNAME: "your-redis-username"
        REDIS_PASSWORD: "your-redis-password"

    - name: admin-user
      data:
        ADMIN_FIRST_NAME: your-first-name
        ADMIN_LAST_NAME: your-last-name
        ADMIN_EMAIL: "your-email@domain.com"
        ADMIN_PASSWORD: "your-secure-password"
```

We are generating passwords for **MongoDB** and **RabbitMQ** using AWS Secrets Manager.

For Redis:

- `REDIS_PRIMARY_HOST` = the **primary** endpoint
- `REDIS_REPLICA_HOSTS` = the **reader** endpoint
- `REDIS_USERNAME = Valkey/Redis RBAC username (required from v10.6.2605+)`
- `REDIS_PASSWORD = Valkey/Redis RBAC password (required from v10.6.2605+)`

For `admin-user` : these values initialize the admin account for managing MOCM.

#### Option: Create secrets manually with kubectl (Optional)

Instead of putting credentials in `values.yaml`, you can create secrets directly with `kubectl` before deploying.

**Important**: If you create secrets manually, you **must remove** `global.secrets` from `values.yaml`. If `global.secrets`  is present, the Helm pre-install/pre-upgrade hook will overwrite your manually created secrets on every deploy.

```yaml
kubectl create secret generic mongodb-secrets -n fusion \

--from-literal=MONGODB_HOSTS="host1:27017,host2:27017,host3:27017" \

--from-literal=MONGODB_AUTH_USER="admin" \

--from-literal=MONGODB_AUTH_PASSWORD="your-mongodb-password" \

--from-literal=MONGODB_AUTH_DATABASE="admin"
```

```yaml
kubectl create secret generic rabbitmq-secrets -n fusion \

--from-literal=RABBITMQ_HOST="your-rabbitmq-host:5671" \

--from-literal=RABBITMQ_USER="your-rabbitmq-user" \

--from-literal=RABBITMQ_PASSWORD="your-rabbitmq-password"
```

```yaml
kubectl create secret generic redis-secrets -n fusion \

--from-literal=REDIS_PRIMARY_HOST="your-redis-primary:6379" \

--from-literal=REDIS_REPLICA_HOSTS="your-redis-reader:6379"\

--from-literal=REDIS_USERNAME="your-redis-username" \

--from-literal=REDIS_PASSWORD="your-redis-password"
```

```yaml
kubectl create secret generic admin-user-secrets -n fusion \

--from-literal=ADMIN_FIRST_NAME="Admin" \

--from-literal=ADMIN_LAST_NAME="User" \

--from-literal=ADMIN_EMAIL="admin@example.com" \

--from-literal=ADMIN_PASSWORD="your-secure-password"
```

#### 3. Product RSA Key Pair

Paste the contents of `tls.key` and `public.key` into `global.productKey`. Use a `|` block scalar to preserve line breaks.

> **Note**: Do **not** include the `-----BEGIN ...-----` and `-----END ...-----` markers — paste only the body of the key

```yaml
global:
  productKey:
    rsaPrivateKey: |-
      MIIJQwIBADANBgkqhkiG9w0BAQEFAASCCS0wggkpAgEAAoICAQDCYXPFgve1AQTF
      rXNWOW2CpFyfUUATwysMJezvgp0MZVuBW3sHWGdy7xLGHEdR0LCs2DkLez3TpT4M
      ....
    rsaPublicKey: |-
      MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwmFzxYL3tQEExa1zVjlt
      gqRcn1FAE8MrDCXs74KdDGVbgVt7B1hncu8SxhxHUdCwrNg5C3s906U+DEtbODAY
      ....
```

#### 4.Master KEK

Paste the contents of gen-kek.sh

```yaml
global:
  masterKekV1: "<your-base64-32-byte-key>"
  currentKekVersion: "V1"
```

#### 5. S3 Storage

```yaml
global:
  storage:
    prefix: "mocm"
    region: "us-west-2"
```

#### 6. Component Replicas (Optional)

Override the default `replicaCount`  for specific services:

```yaml
global:
  componentReplicas:
    mk4InventoryApi: 3
    fusionMdcoreConsumer: 4
```

## Install

### 1. Deploy

From the `mocm/` directory. Choose **one** of the two options below.

#### Option A — Helmfile (recommended)

Helmfile reads `helmfile.yaml` and deploys all 3 releases in the correct order automatically, with `wait`, `waitForJobs`, and `needs` handling the sequencing.

```yaml
helmfile -f helmfile.yaml -n fusion sync 2>&1 | tee helmfile-sync.log
```

#### Option B — Helm (manual, release by release)

If you do not have Helmfile installed, deploy each release manually **in this exact order**:

```yaml
# Release 1: secrets + install-job + ma-tomcat (must complete before Release 2)
helm upgrade --install mocm-bootstrap-1 ./charts/mocm-bootstrap-1 \
  -f ./values.yaml \
  -n fusion \
  --wait --wait-for-jobs --timeout 15m

# Release 2: pmp-inventory-api (must complete before Release 3)
helm upgrade --install mocm-bootstrap-2 ./charts/mocm-bootstrap-2 \
  -f ./values.yaml \
  -n fusion \
  --wait --timeout 10m

# Release 3: all remaining services + Ingress
helm upgrade --install mocm-service ./charts/mocm-service \
  -f ./values.yaml \
  -n fusion \
  --wait --timeout 10m
```

> **Important**: The order **bootstrap-1 → bootstrap-2 → mocm-service** is mandatory. Do not run Release 2 until Release 1 is fully ready, and do not run Release 3 until Release 2 is fully ready.

The process takes **15–30 minutes** depending on your environment.

### 2. Verify Deployment

```yaml
# Check all 3 releases are deployed
helmfile -f helmfile.yaml -n fusion list

# Or with helm directly
helm list -n fusion
```

All releases should show status `deployed`.

```yaml
# Check all pods are Running
kubectl get pods -n fusion
```

All pods should reach `Running` state. If a pod is stuck in `Pending`:

```yaml
kubectl describe pod <pod-name> -n fusion
```

## Upgrade & Uninstall

> **Important**
>
> Before upgrading, always **back up your current** `values.yaml` file. The new chart version may ship with an updated `values.yaml` containing new keys or changed defaults. You should compare the new `values.yaml` with your existing one and **merge your custom values** (credentials, host, image registry, replicas, etc.) into the new file. Losing your previous `values.yaml` may result in missing configurations or service disruption after upgrade

### Upgrade

Check changes before upgrading (optional):

```bash
helmfile -f helmfile.yaml -n fusion diff
```

**Option A — Helmfile:**

```yaml
helmfile -f helmfile.yaml -n fusion sync 2>&1 | tee helmfile-upgrade.log
```

Helmfile `sync` is idempotent — it applies only the diff.

**Option B — Helm (same order as install):**

```yaml
helm upgrade mocm-bootstrap-1 ./charts/mocm-bootstrap-1 -f ./values.yaml -n fusion --wait --wait-for-jobs --timeout 15m
helm upgrade mocm-bootstrap-2 ./charts/mocm-bootstrap-2 -f ./values.yaml -n fusion --wait --timeout 10m
helm upgrade mocm-service ./charts/mocm-service -f ./values.yaml -n fusion --wait --timeout 10m
```

### Uninstall

```yaml
helmfile -f helmfile.yaml -n fusion destroy
```

Or uninstall individual releases with Helm (in reverse order):

```yaml
helm uninstall mocm-service -n fusion
helm uninstall mocm-bootstrap-2 -n fusion
helm uninstall mocm-bootstrap-1 -n fusion
```

## Testing (Static / Pre-deploy)

Validate charts before deploying to a cluster.

### Phase 1: Lint

```yaml
helm lint charts/mocm-bootstrap-1 -f values.yaml
helm lint charts/mocm-bootstrap-2 -f values.yaml
helm lint charts/mocm-service -f values.yaml
```

### Phase 2: Template Render

```yaml
helm template mocm-bootstrap-1 charts/mocm-bootstrap-1 -f values.yaml > /dev/null
helm template mocm-bootstrap-2 charts/mocm-bootstrap-2 -f values.yaml > /dev/null
helm template mocm-service charts/mocm-service -f values.yaml > /dev/null
```

To inspect rendered output:

```yaml
helm template mocm-bootstrap-1 charts/mocm-bootstrap-1 -f values.yaml > rendered-bootstrap-1.yaml
```

### Phase 3: Helmfile Validation

```yaml
# List releases and their ordering
helmfile -f helmfile.yaml list

# Render all releases (dry-run without cluster)
helmfile -f helmfile.yaml -n fusion template
```

## Troubleshooting

### Pod stuck in Pending

```yaml
kubectl describe pod <pod-name> -n fusion
```

Common causes: insufficient CPU/memory, missing PVC, node not ready.

### Secrets not created

Secrets are managed as Helm hooks (`pre-install`, `pre-upgrade`) in `mocm-bootstrap-1`. If secrets are missing, check:

```yaml
helm get hooks mocm-bootstrap-1 -n fusion
kubectl get secrets -n fusion
```

### Release failed

```yaml
# Check Helmfile status
helmfile -f helmfile.yaml -n fusion status

# Check specific release
helm status mocm-bootstrap-1 -n fusion
helm get notes mocm-bootstrap-1 -n fusion
```

### View logs

```yaml
kubectl logs deployment/<service-name> -n fusion --tail=100
```

### Point Domain to Ingress

After deploying MOCM and obtaining the external address of your Kubernetes ingress controller, you need to configure your DNS so that your chosen domain name points to the ingress.

- `host`(e.g. mocm.example.com) → ALB  address — Main web traffic (HTTPS)

## Access MOCM Console

After completing the deployment and DNS configuration, you can access the My OPSWAT Central Management console:

1. Open your browser and navigate to https://<your-domain> (the host value configured in values.yaml)
2. Enter the administrator credentials configured in values.yaml (admin-user secret):

- Email: the value of `ADMIN_EMAIL`
- Password: the value of `ADMIN_PASSWORD`

You should now have access to the My OPSWAT Central Management console.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
