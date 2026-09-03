<!-- source: https://www.opswat.com/docs/cm/deployment/deploy-infra-for-private-cloud-aws -->

# Deploy Infrastructure (AWS)

## Overview and Scope

> **Info**
>
> This guide explains how to deploy the My OPSWAT Central Management stack on AWS using OpenTofu for infrastructure, Amazon EKS for Kubernetes, Helm/Helmfile for application release, and Ansible executed over AWS Systems Manager for MongoDB on EC2. It is a copy/paste, step-by-step deployment runbook from initial provisioning through application verification.

- What you deploy: VPC, subnets, NAT gateways, EKS cluster, core addons (ALB controller, Ingress NGINX, Cluster Autoscaler), MongoDB replica set on EC2 (via Ansible + SSM), Amazon MQ (RabbitMQ), Valkey (ElastiCache), S3 buckets, ACM certificate, and the MOCM application via Helm/Helmfile.
- Out of scope: detailed monitoring/alerting design, long-term backup/DR runbooks. See the Backup & Restore runbook for MongoDB snapshot strategy and options beyond EBS/DLM.

## Architecture Summary

- Networking: 1 VPC, 3 public subnets, 3 private subnets, Internet Gateway, NAT (single or per-AZ), VPC Endpoints (ECR dkr/api, STS, SSM, SSMMessages, EC2Messages, S3 Gateway).
- EKS: 1 cluster, 1 managed node group, addons (CoreDNS, kube-proxy, EBS CSI, Pod Identity), plus Helm-installed addons (ALB Controller, Ingress NGINX, Cluster Autoscaler).
- Data services: MongoDB Replica Set on EC2 (3 nodes, TLS), Amazon MQ for RabbitMQ, ElastiCache for Valkey, S3 buckets for product artifacts and data.
- Ingress: AWS ALB with TLS certificate from ACM.

![](https://uploads.developerhub.io/prod/97qW/stuui6ajg6tk0th8a24d4f33aootxpif64lwx3aa84wng67ug0sftdonqhbgtopy.png)

| Category | Resource | Count | Notes |
| ---- | ---- | ---- | ---- |
| **Networking** | VPC | 1 | CIDR defined by `vpc_cidr` |
|  | Public subnets | 3 |  |
|  | Private subnets | 3 | One per AZ |
|  | Internet Gateway | 1 |  |
|  | VPC Endpoints (Interface) | 6 | ECR dkr, ECR api, STS, SSM, SSMMessages, EC2MessagesVPC Endpoints (Interface) |
|  | VPC Endpoints (Gateway) | 1 | S3 Gateway (free)VPC Endpoints (Gateway) |
|  | Security Groups | 7 typical | EKS Node, ALB, VPC Endpoint, ElastiCache, Bastion, MongoDB, RabbitMQ — if `enable_bastion = false`, Bastion-related rules may be absent; exact set follows the moduleSecurity Groups |
| **EKS** | EKS cluster | 1 | Includes EKS-managed cluster security group |
|  | Managed Node Group | 1 | Capacity type and instance types **differ by profile** (see table below) Managed Node Group |
|  | Node count | 8 | desired 8, min 8, max 20 (same in both `.example` files)Node count |
|  | OpenTofu-managed addons | 4 | kube-proxy, CoreDNS, EBS CSI Driver, Pod Identity Agent (kube-state-metrics optional, default off)OpenTofu-managed addons |
| **Compute / Data** | MongoDB EC2 instances | 3 | 1 primary + 2 secondary, each with root + data EBS volume; **instance type** varies by profile (see below) |
|  | MongoDB EBS data volumes | 3 | 1 per node, mounted at `/mnt/data`MongoDB EBS data volumes |
| **IAM / Secrets / KMS** | IAM roles + policies | multiple | EKS cluster, node group, Bastion (if enabled), MongoDB EC2, Pod Identity |
|  | Secrets Manager secrets | 2 | MongoDB admin, RabbitMQ admin (auto-generated passwords)Secrets Manager secrets |
|  | KMS key + alias | 1 + 1 | EKS secrets encryptionKMS key + alias |
| **DNS / Certs** | Route53 Private Hosted Zone | 1 | If `enable_mongodb_private_dns = true` (default in both examples) |
|  | Route53 A records | 3 | mongo-01, mongo-02, mongo-03 -> private IPsRoute53 A records |
|  | ACM certificate | 1 | If `domain_name` is set; DNS validation optionalACM certificate |
| **Storage** | S3 buckets | 7 | gears-fusion-files, gears-cloud, gears-custom-scripts, mdcore, fusion-updater, mdfusion-vpack, ansible-ssm-logs |
| **Logs** | CloudWatch Log Groups | 4 | Amazon MQ general + connection, EKS cluster, RabbitMQ |

#### Differs by profile (reference `.example` files)

| Category | Resource | Cost-optimized (`terraform.tfvars.cost-optimized.example`) | HA multi-AZ (`terraform.tfvars.high-availability-multi-az.example`) |
| ---- | ---- | ---- | ---- |
| **Networking** | NAT Gateway + Elastic IP | 1 + 1 (`single_nat_gateway = true`) | 3 + 3 (`single_nat_gateway = false`, one NAT per AZ) |
|  | Route tables | Typically **1 public + 1 private** shared across private subnets (single NAT) | **1 public + 3 private** (one private route table per AZ is common with multi-NAT) — exact layout **varies by** `single_nat_gateway` and module wiring |
| **EKS** | Capacity + instance types | **SPOT**; `eks_node_group_instance_types = ["t3.large", "t3.xlarge", "t3.2xlarge"]` | **ON_DEMAND**; `["t3.large"]` |
| **Datastores** | Amazon MQ (RabbitMQ) | **1 broker**, `SINGLE_INSTANCE` | **Cluster**, `CLUSTER_MULTI_AZ` (multi-AZ failover; not a single-node broker) |
|  | ElastiCache (Valkey) | 1 node, `cache.t3.medium` | 1 node, `cache.t3.medium` |
| **Compute / Data** | MongoDB EC2 instance type | `t3.large` | `t3.xlarge` |
| **Compute** | Bastion EC2 | **0** (`enable_bastion = false`) | **1** (`enable_bastion = true`), `t3.medium`; SSM Session Manager, no public IP |

## Prerequisites

**AWS Account & Permissions**

- **AWS Account** (new or existing)
- **IAM User** with Administrator permissions or specific permissions for:
  - `AdministratorAccess`

**Local Environment**

| **Tool** | **Version** | **Install** |
| ---- | ---- | ---- |
| **OpenTofu** | >= v1.11.* | `brew install opentofu` or [download](https://opentofu.org/docs/intro/install/) |
| **AWS CLI** | >= 2.0 | `brew install awscli` or [download](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |
| **kubectl** | >= 1.34 | `brew install kubectl` or [download](https://kubernetes.io/docs/tasks/tools/) |
| **Helm** | >= 3.x.x , *(Helm v4 is not supported)* | `brew install helm` or [download](https://helm.sh/docs/intro/install/) |
| **Helmfile** | >= 1.0.x | `brew install helmfile` or [download](https://helmfile.readthedocs.io/en/latest/#installation) |
| **helm-diff** | latest | `helm plugin install or`[download](https://github.com/databus23/helm-diff) |

## Inputs and Variables to Customize

### terraform.tfvars (OpenTofu)

- Domain and certificate: domain_name, enable_certificate_validation, route53_zone_id (if validating via Route 53).
- EKS and networking: region, vpc_cidr, public/private subnets (or count), eks_service_ipv4_cidr, node group instance types and sizes, NAT settings (single vs multi).
- Security and access: bootstrap_cluster_creator_admin_permissions = true; KMS usage for secrets encryption.

### mocm/values.yaml (Helm)

- Image registry and tag: set your container registry (ECR, Harbor, or any OCI registry) and image tag. The tag should match the images provided in the release package.
- Ingress: host (your external DNS name), ingressClassName (e.g., nginx).
- Global secrets: MongoDB, RabbitMQ, Valkey, and admin-user. If Terraform created MongoDB and RabbitMQ, retrieve their credentials from AWS Secrets Manager (instructions below) and fill them here.

## Step-by-Step Deployment Infrastructure

### Phase 1: OpenTofu Infrastructure

Working directory: terraform/aws

1. #### Configure AWS CLI credentials

```bash
# Configure AWS CLI with your credentials
aws configure
# Enter your AWS Access Key ID, Secret Access Key, and preferred region when prompted
# Example:
# AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
# AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
# Default region name [None]: us-east-1
# Default output format [None]: json
# Verify configuration
aws sts get-caller-identity
```

2. **Extract Package**

![]()

Download MOCM Kubernetes from My OPSWAT Portal and extract the MOCM on-premise package and verify the directory structure:

```bash
# Extract the package
tar -xzf MyOPSWATCentralManagement_10.5.2603.9060.tar.gz
# Expected directory structure:
├── terraform/
│   ├── aws/       # AWS Infrastructure (OpenTofu + Ansible) — current release
│   ├── azure/     # Azure Infrastructure — TBD
│   ├── gcp/       # GCP Infrastructure — TBD
│   └── README.md
├── mocm/          # Helm charts for application deployment
├── images/        # Container images and loading script
```

3. **Navigate to the AWS IaC Directory**

All infrastructure commands in this guide run from the `terraform/` directory.

```bash
cd terraform/aws
```

**Working Directory**: `terraform/aws` -- you will stay here until explicitly told to navigate elsewhere.

4. **Configure Remote Backend (Optional but Recommended)**

If you want to store OpenTofu state remotely on S3 (recommended for team collaboration):

```bash
# Create S3 bucket for Terraform state (replace with your unique bucket name)
aws s3 mb s3://your-company-terraform-state --region [YOUR_REGION]
# Enable versioning
aws s3api put-bucket-versioning \
  --bucket your-company-terraform-state \
  --versioning-configuration Status=Enabled
```

Note: Replace your-company-terraform-state with a unique bucket name. S3 bucket names must be globally unique across all AWS accounts.

Then configure OpenTofu to use it:

```bash
# Copy backend example
cp backend.tf.example backend.tf
# Edit backend.tf and replace YOUR_BUCKET_NAME
nano backend.tf
```

Replace `YOUR_BUCKET_NAME` with the S3 bucket name you created above.

> **Note:**
>
> - S3 backend uses `use_lockfile` to prevent conflicts when multiple people run tofu simultaneously
> - State file is NOT encrypted by default (`encrypt = false`) - change to `true` for production if needed
> - If you skip this step, OpenTofu will store state file locally (terraform.tfstate)

5. **Create terraform.tfvars Configuration File**

**Step 5a — Pick a Profile and Copy the Example**

Choose the scenario that fits your requirements, then copy the corresponding example:

```bash
# Option A — Cost-Optimized (single NAT, SPOT nodes, single-instance broker)
cp terraform.tfvars.cost-optimized.example terraform.tfvars
# Option B — High Availability / Multi-AZ (multi-AZ NAT, On-Demand nodes, HA broker)
cp terraform.tfvars.high-availability-multi-az.example terraform.tfvars

# Edit your configuration
nano terraform.tfvars
```

Update the configuration values according to your environment.

**Step 5b — Pin EKS Cluster + Managed Add-on Versions**

EKS requires five managed add-ons whose versions must match your chosen `eks_version` . Run the command below in your target Region to retrieve the latest compatible versions:

```bash
export AWS_DEFAULT_REGION=<your-region>   # must match aws_region in tfvars
export K8S_VER=1.34                       # must match eks_version in tfvars

for ADDON in kube-proxy coredns aws-ebs-csi-driver eks-pod-identity-agent; do
  VER=$(aws eks describe-addon-versions \
    --addon-name "$ADDON" \
    --kubernetes-version "$K8S_VER" \
    --query 'addons[0].addonVersions[0].addonVersion' \
    --output text)
  printf "%-28s %s\n" "$ADDON" "$VER"
done
```

Copy the output versions into your `terraform.tfvars`  using the mapping below:

**Example (EKS 1.34):**

```bash
# EKS managed add-ons — versions must match eks_version
eks_addon_version_kube_proxy             = "v1.34.3-eksbuild.2"
eks_addon_version_coredns                = "v1.13.2-eksbuild.1"
eks_addon_version_aws_ebs_csi_driver     = "v1.56.0-eksbuild.1"
eks_addon_version_eks_pod_identity_agent = "v1.3.10-eksbuild.2"
```

**Step 5c — Configure S3 CORS for Browser Downloads**

You must provide your portal’s domain to explicitly allow **CORS** access on S3 for browser-based downloads from either `gears-fusion-files` or `gears-cloud` . Each bucket has its own variable in `terraform.tfvars`  ; both require the same CORS rule format (allowing only GET/HEAD, with `ExposeHeaders`   including `ETag`   and `Content-Disposition`.

```bash
gears_fusion_files_cors_allowed_origins = [
  "https://your-portal.customer-domain.com"
]
gears_cloud_cors_allowed_origins = [
  "https://your-portal.customer-domain.com"
```

- Each variable controls CORS only for its respective bucket `gears-fusion-files`  or  gears-cloud
- You must provide a domain value here if the user needs to download files via browser.
- Do not leave this as [ ] if browser download is required, otherwise downloads will fail or filenames will be incomplete.

**Step 5d — Configure AWS WAF (Web Application Firewall)**

WAF is always created with 3 baseline managed rules by default `AWSManagedRulesAmazonIpReputationList` , `AWSManagedRulesCommonRuleSet` , `AWSManagedRulesKnownBadInputsRuleSet`

**Configure managed rules.**

They are pre-configured in `terraform.tfvars`  . To add more rules, append to `waf_managed_rules` :

```bash
waf_config = {
  enable_logging = false
  waf_managed_rules = [
    { name = "AWSManagedRulesAmazonIpReputationList", priority = 10, override_action = "none" },
    { name = "AWSManagedRulesCommonRuleSet",          priority = 20, override_action = "none",
      rule_action_overrides = [
        { name = "SizeRestrictions_BODY",        action = "count" },
        { name = "SizeRestrictions_QUERYSTRING",  action = "count" },
        { name = "CrossSiteScripting_BODY",       action = "count" },
        { name = "GenericRFI_BODY",               action = "count" },
        { name = "GenericLFI_BODY",               action = "count" },
        { name = "NoUserAgent_HEADER",            action = "count" },
        { name = "EC2MetaDataSSRF_BODY",          action = "count" },
      ]
    },
    { name = "AWSManagedRulesKnownBadInputsRuleSet",  priority = 30, override_action = "none" },
    # { name = "AWSManagedRulesSQLiRuleSet",           priority = 40, override_action = "none" },
    # { name = "AWSManagedRulesLinuxRuleSet",          priority = 50, override_action = "none" },
    # { name = "AWSManagedRulesBotControlRuleSet",     priority = 60, override_action = "count" },
  ]
}
```

**Step 5e — Configure SSL Certificate**

Choose the appropriate configuration based on where your domain is managed:

**Option 1: Domain managed in Route 53 (AWS)**

```bash
domain_name                   = "*.yourdomain.com"
enable_certificate_validation = true
route53_zone_id              = "Z1234567890ABC"  # Get from: aws route53 list-hosted-zones
```

Certificate will be `automatically validated`  in 2-5 minutes

**Option 2: Domain managed externally (GoDaddy, Cloudflare, Namecheap, etc.)**

```bash
domain_name                   = "*.yourdomain.com"
enable_certificate_validation = false
route53_zone_id              = ""
```

Certificate will be created but  **Pending Validation** — you must manually add DNS validation records in your DNS provider.

> **Warning**: If `enable_certificate_validation = true`  , you **must** provide `route53_zone_id`   (the Hosted Zone ID, not the domain name).

> **Note**: Use a wildcard cert `*.yourdomain.com`   or a single-domain cert for `mocm.yourdomain.com` . A single ALB handles both REST and gRPC traffic on the same domain.

### **Phase 2 - Deploy Infrastructure (OpenTofu)**

1. Initialize OpenTofu

```bash
tofu init
```

2. Plan Deployment

```bash
tofu plan -var-file=terraform.tfvars
```

**Debug Tip:** If you encounter issues, enable debug logging:

```bash
TF_LOG=DEBUG TF_LOG_PATH="tofu-debug.log" tofu plan -var-file=terraform.tfvars
```

3. Apply Infrastructure

```bash
tofu apply -var-file=terraform.tfvars
# Enter "yes" to continue
# Deployment process will take 15-30 minutes
```

### Phase 3 - Configure EKS and Ingress

Install essential EKS addons:

- Cluster Autoscaler
- AWS Load Balancer Controller
- Ingress NGINX Controller
- Application Load Balancer (ALB) with HTTPS

#### Step 1: Configure kubectl and Export Environment Variables

**Working Directory**: `terraform/aws` (where you ran `tofu apply`)

Configure kubectl and export all environment variables needed for helmfile before navigating away.

```bash
# Configure kubectl to connect to your EKS cluster
aws eks update-kubeconfig \
  --region $(tofu output -raw aws_region) \
  --name $(tofu output -raw eks_cluster_name)

# Required env vars for helmfile (all addons + ALB Ingress)
export CLUSTER_NAME=$(tofu output -raw eks_cluster_name)
export AWS_REGION=$(tofu output -raw aws_region)
export CERTIFICATE_ARN=$(tofu output -raw acm_certificate_arn)
export PUBLIC_SUBNET_IDS=$(tofu output -raw public_subnet_ids_csv)
export ALB_SECURITY_GROUP_ID=$(tofu output -raw alb_security_group_id)
export WAF_WEB_ACL_ARN=$(tofu output -raw waf_web_acl_arn)
```

#### Step 2: Install EKS Addons + MOCM Ingress

**Working Directory**: `terraform/aws/eks-addons/`

```bash
# Navigate to eks-addons directory
cd eks-addons

# Validate: render helmfile.yaml.gotmpl and check env vars resolved correctly
helmfile build

# Validate: render full K8s manifests without deploying (dry-run)
helmfile template --enable-live-output

# Deploy all EKS addons + ALB Ingress (with live output + log capture)
helmfile sync --enable-live-output 2>&1 | tee helmfile-sync.log
```

**Troubleshooting:** If deployment fails, capture debug logs and send to support:

```bash
helmfile sync --enable-live-output --debug 2>&1 | tee helmfile-debug.log
```

**Optional (from 2nd run):** `helmfile diff`   shows only changes before syncing. On the first run it prints the full manifest.

```bash
helmfile diff --enable-live-output
```

**Key flags:**

- `--enable-live-output` — show real-time Helm stdout/stderr (essential for seeing progress)
- `--debug` — verbose output for troubleshooting
- `2>&1 | tee file.log` — capture all output to a file for support

**Customization (optional):** Edit these files before running `helmfile sync` if you need custom configurations:

- `helm/cluster-autoscaler/values.yaml`
- `helm/aws-load-balancer-controller/values.yaml`
- `helm/ingress-nginx/values.yaml`

#### Step 3: Verify Addons

```bash
kubectl get pods -A | grep -E "(cluster-autoscaler|aws-load-balancer|traefik)"
```

**Expected output:**

```bash
traefik         traefik-6f8b9c7d4f-abc12                                     1/1     Running   0   16m
traefik         traefik-6f8b9c7d4f-def34                                     1/1     Running   0   16m
kube-system     aws-load-balancer-controller-59c9d5fb65-kj2dp                1/1     Running   0   16m
kube-system     aws-load-balancer-controller-59c9d5fb65-r5hzm                1/1     Running   0   17m
kube-system     cluster-autoscaler-aws-cluster-autoscaler-78c97ddddf-l9mfv   1/1     Running   0   11m
```

#### Step 4: Verify ALB Ingress

If you exported the ALB env vars (`CERTIFICATE_ARN`, `PUBLIC_SUBNET_IDS`, `ALB_SECURITY_GROUP_ID`) in Step 1, the ALB Ingress was deployed automatically by `helmfile sync` in Step 2.

```bash
# Check ALB Ingress resource
kubectl get ingress mocm-ingress -n traefik

# Check gRPC path-based Ingress (same ALB, GRPC Target Group)
kubectl get ingress -n traefik
```

**After 2-3 minutes, you should see:**

```bash
NAME                   CLASS   HOSTS   ADDRESS                                                                PORTS   AGE
mocm-ingress           alb     *       mocm-ingress-1234567890-123456789.ap-northeast-1.elb.amazonaws.com     80      3m
mocm-ingress-grpc      alb     *       mocm-ingress-1234567890-123456789.ap-northeast-1.elb.amazonaws.com     80      3m
```

### Phase 4 - Deploy MongoDB (Ansible)

Deploy MongoDB 8.0 replica set (3 nodes) using Ansible via AWS SSM.

#### Prerequisites

Ensure you have the following tools installed before proceeding:

| Tool | Version | Installation |
| ---- | ---- | ---- |
| **uv** | Latest | [Installation guide](https://docs.astral.sh/uv/getting-started/installation/) |
| **AWS Session Manager Plugin** | Latest | [Installation guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-install-plugin.html) |
| **jq** | Latest | JSON processor for parsing OpenTofu outputs |

```bash
# Verify all tools are installed
uv --version
session-manager-plugin --version
jq --version
```

#### Step 1: Export OpenTofu Outputs

**Working Directory**: `terraform/aws` (where you ran `tofu apply`)

Export all values needed for Ansible. These environment variables are used in all subsequent steps.

```bash
# MongoDB instance IDs (from mongodb_instances output map)
export MONGO_PRIMARY_ID=$(tofu output -json mongodb_instances | jq -r '.primary_instance_id')
export MONGO_SECONDARY_1_ID=$(tofu output -json mongodb_instances | jq -r '.secondary_instance_ids[0]')
export MONGO_SECONDARY_2_ID=$(tofu output -json mongodb_instances | jq -r '.secondary_instance_ids[1]')
export AWS_REGION=$(tofu output -raw aws_region)
export SSM_BUCKET=$(tofu output -raw ansible_ssm_bucket_name)
export MONGODB_PASSWORD=$(tofu output -raw mongodb_admin_password)
export MONGODB_MONITOR_PASSWORD=$(tofu output -raw mongodb_monitor_password)

# MongoDB Private DNS (if enable_mongodb_private_dns = true)
export MONGODB_ZONE_NAME=$(tofu output -raw mongodb_private_zone_name)
```

**Important:** Keep this terminal open -- all subsequent Ansible commands reference these environment variables.

#### Step 2: Install Dependencies and Prepare Inventory

**Working Directory**: `terraform/aws/ansible/` (you will stay here for all remaining Ansible steps)

```bash
# Navigate to ansible directory
cd ansible

# Install Python dependencies (Ansible, plugins, etc.)
uv sync

# Install Ansible Galaxy roles and collections
uv run ansible-galaxy install -r requirements.yml

# Copy example inventory file (no need to edit - values are passed via command line)
cp inventory.ini.example inventory.ini
```

**Ansible Deployment Options**

There are 3 roles: **common** (EBS mount), **mongodb**, and **node_exporter**. The **common** role must run first because MongoDB uses `/mnt/data`.

| Option | When to use |
| ---- | ---- |
| **Option 1 -- Run all at once** | First deployment or full deployment |
| **Option 2 -- Run role by role** | Debug, retry a single role, or update one role only |

**Option 1 -- Run all at once:**

1. Run `playbook.yml` (common + mongodb)
2. Run `playbook-node-exporter.yml` (node_exporter)

**Option 2 -- Run role by role:**

1. `playbook.yml --tags common` (required first)
2. `playbook.yml --tags mongodb`
3. `playbook-node-exporter.yml`

**Idempotent:** Both playbooks are safe to re-run multiple times -- they do not overwrite data or cause errors.

**Required variables by playbook:**

| Playbook | Required variables |
| ---- | ---- |
| `playbook.yml` | `mongo_primary_instance_id`, `mongo_secondary_1_instance_id`, `mongo_secondary_2_instance_id`, `aws_region`, `ssm_bucket_name`, `mongodb_admin_password` |
| `playbook-node-exporter.yml` | `mongo_primary_instance_id`, `mongo_secondary_1_instance_id`, `mongo_secondary_2_instance_id`, `aws_region`, `ssm_bucket_name` |

Cluster 3 nodes use the same `mongodb_instance_type` (OpenTofu). Set `mongo_numa` based on instance type:

| mongodb_instance_type | mongo_numa | Playbook |
| ---- | ---- | ---- |
| t3.large, t3.xlarge | false (default) | No change needed |
| r5.4xlarge+, r7i, r7iz | true | Add `-e "mongo_numa=true"` |

**Note:** Enabling NUMA on a running cluster triggers a sequential restart of all 3 nodes.

**Verify NUMA on EC2 (SSM):** `lscpu | grep -i numa`, `grep ExecStart /usr/lib/systemd/system/mongod.service`, `cat /proc/$(pgrep mongod)/numa_maps | head -5`

#### Step 3: Test Connection (Optional)

```bash
# Test SSM connection to all MongoDB instances
uv run ansible -i inventory.ini production_mongodb -m ping \
  -e "mongo_primary_instance_id=$MONGO_PRIMARY_ID" \
  -e "mongo_secondary_1_instance_id=$MONGO_SECONDARY_1_ID" \
  -e "mongo_secondary_2_instance_id=$MONGO_SECONDARY_2_ID" \
  -e "aws_region=$AWS_REGION" \
  -e "ssm_bucket_name=$SSM_BUCKET"
```

Expected output: `SUCCESS` for all 3 nodes.

#### Step 4: Deploy MongoDB Cluster

```bash
# Deploy MongoDB cluster (actual deployment)
uv run ansible-playbook -i inventory.ini playbook.yml \
  -e "mongo_primary_instance_id=$MONGO_PRIMARY_ID" \
  -e "mongo_secondary_1_instance_id=$MONGO_SECONDARY_1_ID" \
  -e "mongo_secondary_2_instance_id=$MONGO_SECONDARY_2_ID" \
  -e "aws_region=$AWS_REGION" \
  -e "ssm_bucket_name=$SSM_BUCKET" \
  -e "mongodb_admin_password=$MONGODB_PASSWORD" \
  -e "mongodb_private_zone_name=$MONGODB_ZONE_NAME"
```

**Tip:**

- All values come from the `export` commands in Step 1 -- no manual copy-paste needed.
- `mongodb_private_zone_name` ensures TLS certificates include SANs for your private DNS hostnames.
- Playbooks are idempotent -- safe to re-run.

#### Step 4b: Deploy Node Exporter (Optional but Recommended)

Node Exporter exposes metrics on port 9100 for Prometheus. Run this playbook if you need MongoDB instance metrics (e.g., for EKS monitoring).

```bash
# Deploy Node Exporter on MongoDB instances
uv run ansible-playbook -i inventory.ini playbook-node-exporter.yml \
  -e "mongo_primary_instance_id=$MONGO_PRIMARY_ID" \
  -e "mongo_secondary_1_instance_id=$MONGO_SECONDARY_1_ID" \
  -e "mongo_secondary_2_instance_id=$MONGO_SECONDARY_2_ID" \
  -e "aws_region=$AWS_REGION" \
  -e "ssm_bucket_name=$SSM_BUCKET"
```

**Note:** Requires internet access (downloads Node Exporter from GitHub).

#### Step 5: Verify Cluster

**Note:** These commands use AWS CLI and can be run from any directory.

```bash
# Connect to primary MongoDB instance via SSM
aws ssm start-session --target $MONGO_PRIMARY_ID --region $AWS_REGION
# Inside SSM session, connect to MongoDB with TLS
sudo mongosh --tls \
  --tlsCertificateKeyFile /etc/mongodb/serverCert.pem \
  --tlsCAFile /etc/mongodb/rootCAcombined.pem \
  --tlsAllowInvalidCertificates --tlsAllowInvalidHostnames \
  -u admin -p "<your-mongodb-password>" \
  --authenticationDatabase admin
# Check replica set status
rs.status()
```

**Retrieve password later:**

```bash
# Get MongoDB admin password from Secrets Manager
aws secretsmanager get-secret-value \
  --secret-id "{name_prefix}/mongodb/admin" \
  --query SecretString --output text | jq '.'
```

#### Step 6: Verify MongoDB Private DNS (Route53)

If `enable_mongodb_private_dns = true` (default), OpenTofu created a **Route53 Private Hosted Zone** inside your VPC with A records for each MongoDB instance.

**Zone name format:** `internal.mongodb.<name_prefix>.<environment>`

The `mongodb_hostnames` output from Step 1 contains the values you need for Helm. Copy the `mongodb_hosts` value and use it for `MONGODB_HOSTS` in `mocm/values.yaml`:

**Tip:** If you closed the terminal or lost the output from Step 1, you can retrieve it again:

```bash
# From the repo root:
cd terraform/aws
tofu output mongodb_hostnames

# Or get just the mongodb_hosts connection string:
tofu output -json mongodb_hostnames | jq -r '.mongodb_hosts'
```

**Example** `mocm/values.yaml` configuration:

```yaml
global:
  secrets:
    - name: mongodb
      data:
        MONGODB_HOSTS: mongo-01.internal.mongodb.<name_prefix>.<environment>:27017,mongo-02.internal.mongodb.<name_prefix>.<environment>:27017,mongo-03.internal.mongodb.<name_prefix>.<environment>:27017
```

**Verify DNS resolution from an EKS pod:**

```yaml
kubectl run dns-test --rm -it --image=busybox --restart=Never -- nslookup mongo-01.internal.mongodb.<name_prefix>.<environment>
```

**Note:** The Private Hosted Zone is only resolvable from within the VPC (EKS pods, EC2 instances). It is not accessible from the public internet.

### Phase 5 - Infrastructure Summary

Your infrastructure is now ready:

- **AWS Resources**: VPC, EKS 1.34, MongoDB (3 nodes), RabbitMQ, Valkey, S3 buckets, ACM certificate
- **EKS Addons**: Cluster Autoscaler, ALB Controller, Ingress NGINX
- **MongoDB**: 3-node replica set with TLS/SSL authentication
- **VPC Endpoints**: ECR (x2), STS, S3 (Interface + Gateway), SSM (x3)

**Next step**: [Deploy Application with Helm Charts](https://www.opswat.com/docs/cm/deployment/deploy-application-with-helm-charts)
