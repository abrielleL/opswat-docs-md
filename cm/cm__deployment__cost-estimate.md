<!-- source: https://www.opswat.com/docs/cm/deployment/cost-estimate -->

# Cost Estimate

---

This document provides a monthly AWS cost estimate for deploying the MOCM platform using the OpenTofu configurations in terraform/aws/. All figures are based on ap-northeast-1 (Tokyo) On-Demand rates as of early 2026, assuming 730 hours/month. Prices can change—always verify with the AWS Pricing Calculator when modifying region or resource types. These estimates exclude outbound data transfer beyond ~50GB, AWS Support, Shield Advanced, and any service/component not provisioned by the stack (e.g. CloudFront). WAF costs are in Section 6.

## 1. Deployment Scenarios - Quick Comparison

This stack supports two production-level deployment scenarios. Choosing between them depends on cost sensitivity and uptime requirements.

| Scenario | Configuration File | Estimated Monthly Cost (USD) |
| ---- | ---- | ---- |
| Cost-Optimized | terraform.tfvars.cost-optimized.example | ~$1,110 – $1,280 |
| High Availability | terraform.tfvars.high-availability-multi-az.example | ~$2,340 – $2,500 |

**Notes:**

> - Estimates include compute, managed services, networking, storage.
> - Excludes outbound data over ~50 GB, premium support, and services not managed by this stack.
> - WAF is included by default (see Section 6).

**How to select:** Copy the relevant `.tfvars` file to `terraform.tfvars` before running OpenTofu.

```markdown
# Minimum (cost-optimized)
cp terraform.tfvars.cost-optimized.example terraform.tfvars

# Production (high availability)
cp terraform.tfvars.high-availability-multi-az.example terraform.tfvars
```

|  | Cost-Optimized | High Availability |
| ---- | ---- | ---- |
| **When to Choose** | You care most about cost and can tolerate rare/short disruptions | You need maximum resilience and multi-AZ redundancy |
| **NAT Gateway** | Single (shared, lower cost, less fault-tolerant) | One per AZ (3x, higher cost, highly resilient) |
| **EKS nodes** | SPOT, pool of `t3.large`/`t3.xlarge`/`t3.2xlarge`, min/desired 10SPOT, pool of `t3.large`/`t3.xlarge`/`t3.2xlarge`, min/desired 10 | 8 On-Demand `m5.xlarge`, min/desired 8 |
| **RabbitMQ** | Single-instance, no failover | 3-node multi-AZ cluster, auto failover |
| **Bastion** | Disabled by default | Enabled |

---

## 2. Scenario A — Cost-Optimized (Minimum)

> > **Config file:** `terraform.tfvars.cost-optimized.example`
>
> This profile is for users minimizing AWS spend for production loads. It uses a single NAT, SPOT nodes for EKS, and a single RabbitMQ broker. If an AZ fails, network egress is lost until recovery. SPOT nodes may be interrupted.
>
> > **SPOT node note:** For EKS, only `t3.large`, `t3.xlarge`, and `t3.2xlarge` are allowed. Costs vary with which size and discount rates the autoscaler obtains.

**Key Terraform settings:**

```bash
single_nat_gateway             = true
eks_node_group_capacity_type   = "SPOT"
eks_node_group_instance_types  = ["t3.large", "t3.xlarge", "t3.2xlarge"]
eks_node_group_desired_size    = 10
eks_node_group_min_size        = 10
rabbitmq_deployment_mode       = "SINGLE_INSTANCE"
elasticache_node_type          = "cache.t3.medium"
mongodb_instance_type          = "t3.large"
enable_bastion                 = false
```

**Monthly Service Cost Breakdown:**

| Service | Configuration | USD/month |
| ---- | ---- | ---- |
| EKS Control Plane | 1 cluster | ~$73 |
| EKS Node Group | 10 x `t3.large/xlarge/2xlarge` (SPOT) | ~$225 – $350 |
| MongoDB EC2 | 3 x `t3.large` (On-Demand) | ~$180 |
| Amazon MQ (RabbitMQ) | mq.m5.large SINGLE_INSTANCE + 200GB EBS | ~$250 |
| ElastiCache (Redis) | 1 x `cache.t3.medium` | ~$48 |
| NAT Gateway | 1 gateway + ~50GB data transfer | ~$35 – $40 |
| VPC Endpoints | 6 interface + 1 S3 Gateway | ~$153 |
| EBS (MongoDB) | 3 x 79GB root + 3 x 201GB data (gp3) | ~$81 |
| EBS (EKS nodes) | 10 x 49GB (gp3)10 x 49GB (gp3) | ~$48 |
| S3 | 7 buckets, ~50GB | ~$5 |
| CloudWatch Logs | VPC Flow Logs (7d) + MQ logs (3d) | ~$5 – $15 |
| KMS | 1 CMK (EKS secrets) | ~$1 |
| ECR | 8 repos, ~20GB images | ~$2 |
| Secrets Manager | 3 secrets | ~$1 |
| Route 53 |  |  |
| ACM | 1 certificate | $0 |
| Bastion EC2 | optional (if enabled) | ~$15 – $30 |
| **Total** |  | **~$1,110 – $1,280** |

---

## 3. Scenario B — High Availability (Production)

> > **Config file:** `terraform.tfvars.high-availability-multi-az.example`
>
> For environments demanding maximum up-time, this mode provisions multi-AZ networking, On-Demand EKS nodes, and RabbitMQ in a 3-node cluster to eliminate single points of failure.
>
> **Key Terraform settings (diffs from Cost-Optimized):**

```bash
single_nat_gateway             = false
eks_node_group_capacity_type   = "ON_DEMAND"
eks_node_group_instance_types  = ["m5.xlarge"]
eks_node_group_desired_size    = 8
eks_node_group_min_size        = 8
rabbitmq_deployment_mode       = "CLUSTER_MULTI_AZ"
elasticache_node_type          = "cache.t3.medium"
mongodb_instance_type          = "t3.xlarge"
enable_bastion                 = true
bastion_instance_type          = "t3.medium"
```

---

**Monthly Service Cost Breakdown:**

| Service | Configuration | USD/month |
| ---- | ---- | ---- |
| EKS Control Plane | 1 cluster | ~$73 |
| EKS Node Group | 8 x `m5.xlarge` (On-Demand) | ~$1,050 – $1,200 |
| MongoDB EC2 | 3 x `t3.large` (On-Demand) | ~$360 |
| Amazon MQ (RabbitMQ) | mq.m5.large CLUSTER_MULTI_AZ + EBS | ~$480 |
| ElastiCache (Redis) | 1 x `cache.t3.medium` | ~$48 |
| NAT Gateway | 3 gateways (one per AZ) + ~100GB data | ~$35 – $40 |
| VPC Endpoints | 6 interface + 1 S3 Gateway | ~$153 |
| EBS (MongoDB) | 3 x 79GB root + 3 x 201GB data (gp3) | ~$81 |
| EBS (EKS nodes) | 10 x 49GB (gp3)10 x 49GB (gp3) | ~$48 |
| S3 | 7 buckets, ~50GB | ~$5 |
| CloudWatch Logs | VPC Flow Logs (7d) + MQ logs (3d) | ~$5 – $15 |
| KMS | 1 CMK (EKS secrets) | ~$1 |
| ECR | 8 repos, ~20GB images | ~$2 |
| Secrets Manager | 3 secrets | ~$1 |
| Route 53 |  |  |
| ACM | 1 certificate | $0 |
| Bastion EC2 | optional (if enabled) | ~$15 – $30 |
| **Total** |  | **~$2,340 – $2,500** |

## 4. Key Cost Drivers — How Variables Affect Your Bill

The variables/choices below most significantly affect monthly AWS charges. Adjust these in `.tfvars` to scale usage versus cost.

**TDB**

## 5. AWS WAF

WAF is included in the base stack, with 3 managed rules active by default.

**Baseline cost (default rules):**

|  | **Unit Price** | Qty | USD/month |
| ---- | ---- | ---- | ---- |
| Web ACL | $5.00/ACL | 1 | $5.00 |
| Rules | $1.00/rule | 3 | $3.00 |
| Inspection | $0.60/million req | varies | usage-based |
| **Total (1M req)** |  |  | ~$8.60 |
| **Total (10M req)** |  |  | ~$14.00 |

**Advanced managed rules** (disabled by default):

| Rule Group | Extra Fee/million req | Description |
| ---- | ---- | ---- |
| `AWSManagedRulesBotControlRuleSet` (common/targeted) | $1.00 / $10.00 | Varying bot detection (targeted = ML, SDK required) |
| ACFP, ATP | $10.00 | Account fraud/takeover prevention |

**Shield Advanced** ($3,000/mo, not included) is opt-in outside the stack.

**WAF Logging:** If enabled, logs go to S3 at ~$0.023/GB/month stored.

## 6. Get a Precise Quote — Calculator & Planning Steps

To precisely estimate AWS billing:

1. Run `tofu plan` to get actual resource sizes/counts.
2. Use the [AWS Pricing Calculator](https://calculator.aws/):
   - Region: ap-northeast-1
   - EC2 details (EKS + MongoDB + Bastion)
   - Amazon MQ/RabbitMQ config
   - ElastiCache sizing
   - Count of NAT Gateways & egress
   - Count of VPC endpoints × AZs
   - EBS volumes
   - WAF config (ACL, rules, expected traffic)
3. Add a 10–15% buffer for data transfer, logging, and S3 request cost.
4. New accounts: review [AWS Free Tier](https://aws.amazon.com/free/).

---

## 7. Observability Stack (Optional Add-On)

(Only applies if the monitoring node group is enabled. See [OBSERVABILITY_GUIDE.md](OBSERVABILITY_GUIDE.md) for setup details. Pricing uses us-east-1 as reference; adjust for your region.)

### Compute: EKS Monitoring Node Group

Dedicated Spot node group. ResourceSpecPrice/hrCountMonthlyt3.xlarge4 vCPU / 16 GiB$0.0502–3$73–$110t3.2xlarge8 vCPU / 32 GiB$0.1002–3$146–$219

> Default config: t3.xlarge, min 2, desired 3, max 5.

### Storage: EBS (gp3)

ComponentSize/ReplicaReplicasTotal$/movmstorage50 GiB3150$12vlstorage100 GiB3300$24Root EBS50 GiB3150$12**Total**$48

### Network: Internal NLB and Cross-AZ Data

#### Deep Dive: NLB Cost Model

- **NLB hourly charge:** $0.0225 per AZ × 3 AZ × 730h = **$49.28/mo**
- **NLCU usage (for this workload):** Negligible (<$1/mo)
- **Cross-AZ transfer (MongoDB log flows, etc):** ~$0.80/mo

See “Cost Optimization” below for details and ways to reduce/remove NLB cost.

**Total:** CategoryLowHighCompute (Spot)$73$110Storage (gp3)$48$48Network (NLB 3-AZ + cross-AZ)$51$51**Overall Total $172 $209**

#### Managed Alternatives Comparison

SolutionEst. CostNotesSelf-hosted (3-AZ NLB)$172–$209Full control; no per-metric/log feesSelf-hosted (1-AZ NLB)$139–$176One AZ; lower availability for logsNo NLB (K8s logs only)$122–$159No MongoDB EC2 log shippingAmazon CloudWatch$300–$800+Cost scales by metric/logAmazon Managed Prometheus + Grafana$200–$500+Per-series/metric queries chargeDatadog$500–$2,000+Per-host pricing + log indexing fees

## 8. Cost Optimization Tips

Apply these tips to minimize your AWS cost for both cluster and observability stack:

### Core Stack

1. **Keep ****single_nat_gateway = true** unless you require multi-AZ NAT. Saves ~$70/mo.
2. **Use SPOT nodes** (`eks_node_group_capacity_type = "SPOT"`) for the highest savings.
3. **Start RabbitMQ with ****SINGLE_INSTANCE** and increase HA only when needed.
4. **Keep log retention periods minimal** (e.g., 3 days for MQ/EKS) unless compliance requires more.
5. **Minimize VPC Flow Logs retention** (defaults: 7 days).
6. **Use ECR lifecycle policies** to limit docker image sprawl/storage.
7. **Default S3 encryption** (AES256) avoids extra KMS expense.

### Observability / Monitoring

1. **Right-size storage:** Start with smaller PVCs and expand as you grow.
2. **Reduce replicas** in non-prod (use single-node clusters).
3. **Shorten log/metric retention** to minimize storage growth.
4. **Handle Spot interruptions:** If Spot instance churn is too frequent, fallback to On-Demand (will 3× compute cost).
5. **Remove unused Grafana dashboards** to avoid unnecessary fetches.
6. **Skip NLB if MongoDB log shipping is not required**—use ClusterIP for VLInsert service to save ~$51/mo.
7. **Limit NLB to 1 AZ** for log shipping to save ~$33/mo, if you accept the single-AZ failure risk.

/table
