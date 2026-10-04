<!-- source: https://www.opswat.com/docs/cm/deployment/upgrade-ha -->

# Upgrade

> **Upgrading from a Previous Release (10.6.2605 to 10.6.26062)**
>
> This document explains how to move an existing deployment from the previous release (app build `10.6.2605`) to **this release** (app build `10.6.26062`) **without destroying any live infrastructure**.

## Conventions used in this document

The actual on-disk folder names in your environment may vary (e.g. `mocm-10.5.2603/`, `mocm-2026.01/`, `releases/2026-05/`, or anything you choose). To stay release-name-agnostic, this document uses two placeholders:

| Placeholder | Meaning |
| ---- | ---- |
| `<previous-release>/` | The release directory currently running in production (app build `10.5.2603`, holds your live OpenTofu state). |
| <current-release>/ | The release directory of **this** package (app build `10.6.2605`) — the new version you are upgrading **to**. |

Replace both placeholders with the real paths on your machine before running any command.

## **Upgrading **`10.6.2605`** → **`10.6.26062`** (application / chart only)**

This is a **chart-only** upgrade — there are **no Terraform or infrastructure changes**. Skip the Terraform sections (Pre-upgrade checklist, Option A/B, Stage 4) below; those apply only when coming from `10.5.2603`. All changes ship in the `mocm/` Helm chart.

### **What's new (**`10.6.2605`** → **`10.6.26062`**)**

| Layer | Change |
| ---- | ---- |
| Helm | **New required value **`global.masterKekV1` (+ `global.currentKekVersion`), consumed by the product updater (`fusion-updater`, `fusion-updater-scheduler`). Must be generated and set before upgrade. |
| Images | Bumped from `10.6.2605` to `10.6.26062` (see `images/images.txt`). |

### **Steps**

1. **Merge **`values.yaml` — do **not** overwrite (same rule as the *Helm / Helmfile upgrade (application layer)* section below). Carry over your credentials / host / `productKey` / storage / `componentReplicas` into the new file.
2. **Bump the image tag** to `10.6.26062` in `global.image.tag`, and push the new images to ECR **before** syncing (`cd <current-release>/images && ./loadimage.sh`), otherwise pods will `ImagePullBackOff`.
3. **Diff, then sync** (the 3-release ordering `mocm-bootstrap-1` → `mocm-bootstrap-2` → `mocm-service` is enforced by Helmfile):

   `cd <current-release>/mocm`
   `helmfile -f helmfile.yaml -n fusion diff`
   `helmfile -f helmfile.yaml -n fusion sync 2>&1 | tee helmfile-upgrade.log`
4. **Verify** all pods are Running:

   `kubectl get pods -n fusion`

No Terraform apply is required for this upgrade. See the *Helm / Helmfile upgrade (application layer)* section below for the standard merge / diff / rollback rules.

## What's new in this release (`10.5.2603` → `10.6.2605`)

| Layer | Change |  |
| ---- | ---- | ---- |
| Application images | Bumped from `10.5.2603` to `10.6.2605` (see `images/images.txt`) |  |
| Terraform | New example `terraform/aws/terraform.tfvars.cost-optimized.example` |  |
| Terraform | New operational guides under `terraform/aws/docs/` (deployment, cost, DR, EKS upgrade, observability, WAF, …). |  |
| Helm | `mocm/values.yaml` reset to template form — placeholders must be filled in again. |  |

Review the full diff before you start:

```bash
diff -r <previous-release>/terraform/aws <current-release>/terraform/aws
diff    <previous-release>/mocm/values.yaml <current-release>/mocm/values.yaml
```

## Pre-upgrade checklist

1. **Snapshot everything.**
   - MongoDB EBS snapshots (DLM should already be running — verify).
   - `aws s3 cp` The contents of all 7 buckets to a safe location, or rely on versioning if enabled.
   - Take an RDS/ElastiCache final snapshot if applicable.
2. **Back up the local OpenTofu state.**

```bash
cp <previous-release>/terraform/aws/terraform.tfstate \
   <previous-release>/terraform/aws/terraform.tfstate.pre-upgrade
```

3. **Check tool versions** match the table in `README.md` — in particular `tofu >= 1.10.4`.
4. **Read** `tofu plan` output carefully before any `apply`. If you ever see `destroy` or `replace` on resources you intend to keep, **STOP** and investigate.

## Option A — Keep using the local backend (simplest, POC/single-operator)

Use this if you originally ran `tofu apply` inside `<previous-release>/terraform/aws/` without configuring a remote backend.

```bash
# 1. Copy customer-specific files into the new release
SRC=<previous-release>/terraform/aws
DST=<current-release>/terraform/aws

cp "$SRC"/terraform.tfstate            "$DST"/
cp "$SRC"/terraform.tfstate.backup     "$DST"/ 2>/dev/null || true
cp "$SRC"/terraform.tfvars             "$DST"/
cp "$SRC"/backend.tf                   "$DST"/ 2>/dev/null || true
cp -r "$SRC"/.terraform.lock.hcl       "$DST"/ 2>/dev/null || true
```

Open `<current-release>/terraform/aws/terraform.tfvars` and append the Valkey block below (new in `10.6.2605`). Skip if your file already contains `valkey_*`.

```bash
#############################
# Valkey Configuration (single node, no replica)
#############################
valkey_username                   = "fusion"
valkey_engine_version             = "8.0"
valkey_node_type                  = "cache.t3.micro"
valkey_port                       = 6379
valkey_family                     = "valkey8"
valkey_num_cache_clusters         = 1
valkey_automatic_failover_enabled = false
# Password is auto-generated by Terraform and stored in AWS Secrets Manager.
# Retrieve: aws secretsmanager get-secret-value \
#   --secret-id <name_prefix>/valkey/fusion \
#   --region <aws_region>
```

**Activate the ElastiCache (Redis) file for parallel run.** The previous release's ElastiCache resource is shipped as `09-elasticache.tf.2603` so OpenTofu ignores it by default. Rename it so the old Redis cluster keeps running alongside the new Valkey replication group during data migration:

```bash
cd <current-release>/terraform/aws
mv 09-elasticache.tf.2603 09-elasticache.tf
```

After this rename both `aws_elasticache_cluster.elasticache` (old Redis) and `aws_elasticache_replication_group.valkey` (new) will appear in the plan as `+ create` / no-op. Leave this file active until applications are fully cut over to Valkey — see Stage 4

```bash
# 4. Re-initialise providers (versions may have changed)
cd <current-release>/terraform/aws
tofu init -upgrade

# 5. Review the plan
tofu plan -out tfplan
#    Any destroy/replace on resources you intend to keep → STOP, investigate.

# 6. Apply
tofu apply tfplan
```

````bash
After the apply succeeds, **archive the old release directory** (don't delete
it) so you can roll back state if needed:

```bash
tar czf previous-release.tar.gz <previous-release>/
````

## Option B — Migrate to a remote backend (recommended for production)

Do this **once**, then every future release just points at the same bucket.

### B.1 First-time migration (still inside `<previous-release>`)

```bash
cd <previous-release>/terraform/aws

# Create the S3 bucket + DynamoDB lock table out-of-band, then:
cp backend.tf.example backend.tf
# Edit backend.tf — set bucket, key, region, dynamodb_table

tofu init -migrate-state    # pushes local state to S3, answer "yes"
```

After this step, `terraform.tfstate` in the local directory becomes irrelevant (OpenTofu reads/writes S3). You may delete it, but archiving is safer:

```bash
mv terraform.tfstate terraform.tfstate.migrated-to-s3
```

### B.2 Apply this release

```bash
# 1. Copy customer-specific files into the new release
SRC=<previous-release>/terraform/aws
DST=<current-release>/terraform/aws
cp "$SRC"/backend.tf       "$DST"/
cp "$SRC"/terraform.tfvars "$DST"/

# 2. Activate ElastiCache (Redis) so it keeps running in parallel with the new
#    Valkey replication group. Rename back to .2603 once apps are cut over —
#    see "Stage 4 — Decommission ElastiCache" at the bottom of this document.
mv "$DST"/09-elasticache.tf.2603 "$DST"/09-elasticache.tf

# 3. Append the Valkey block to terraform.tfvars. New in 10.6.2605;
# skip if your file already contains valkey_*. The block is identical to
# Option A step 2:
#############################
# Valkey Configuration (single node, no replica)
#############################
valkey_username                   = "fusion"
valkey_engine_version             = "8.0"
valkey_node_type                  = "cache.t3.micro"
valkey_port                       = 6379
valkey_family                     = "valkey8"
valkey_num_cache_clusters         = 1
valkey_automatic_failover_enabled = false
# Password is auto-generated by Terraform and stored in AWS Secrets Manager.
# Retrieve: aws secretsmanager get-secret-value \
#   --secret-id <name_prefix>/valkey/fusion \
#   --region <aws_region>

# 4. Init, plan, apply
cd "$DST"
tofu init                  # connects to the same S3 backend
tofu plan -out tfplan
tofu apply tfplan
```

No state file copying is required — both release directories point to the same remote state.

## Rollback

### From Option A (local backend)

```bash
cd <current-release>/terraform/aws
cp terraform.tfstate terraform.tfstate.failed
cp <previous-release>/terraform/aws/terraform.tfstate.pre-upgrade \
   <previous-release>/terraform/aws/terraform.tfstate
cd <previous-release>/terraform/aws
tofu init -upgrade
tofu apply       # re-converges to the previous baseline
```

### From Option B (remote backend)

S3 bucket versioning (enabled in `backend.tf.example`) lets you restore the previous state object:

```bash
aws s3api list-object-versions --bucket <state-bucket> --prefix <state-key>
aws s3api get-object --bucket <state-bucket> --key <state-key> \
  --version-id <pre-upgrade-version-id> terraform.tfstate.rollback
# Then push it back with `tofu state push terraform.tfstate.rollback`
```

## Helm / Helmfile upgrade (application layer)

The chart upgrade procedure itself (lint → `helmfile diff` → `helmfile sync`, release ordering, rollback) is already documented in `mocm/README.md` → Upgrade. Follow that document for the actual commands.

What is **specific to a cross-release upgrade** and easy to get wrong:

1. **Do NOT copy** `<previous-release>/mocm/values.yaml` over `<current-release>/mocm/values.yaml`. The new `values.yaml` ships with placeholders (`< REPLACE_VALUE_* >`) and may contain **new keys** that did not exist in the previous release. A blind copy will silently drop those new keys. Correct workflow — **merge**, don't overwrite:

```bash
# Keep the new file as the base, copy your real values into it
cp <current-release>/mocm/values.yaml <current-release>/mocm/values.yaml.new
# Open both side-by-side and port your credentials / host / productKey /
# storage / componentReplicas from the previous release into the new file.
diff -u <current-release>/mocm/values.yaml.new \
        <previous-release>/mocm/values.yaml | less
```

2. **Bump the image tag** in `global.image.tag`:

```bash
global:
  image:
    registry: "<id>.dkr.ecr.<region>.amazonaws.com"
    tag: "10.6.2605"          # was the previous build, e.g. "10.5.2603"
    pullPolicy: IfNotPresent
```

Make sure the new images are already pushed to ECR (`cd <current-release>/images && ./loadimage.sh`) **before** running `helmfile sync`, otherwise pods will go into `ImagePullBackOff`.

3. ** Run a diff first— the 3-release ordering

(`mocm-bootstrap-1` → `mocm-bootstrap-2` → `mocm-service`) is enforced by Helmfile, but you should still preview the diff:

```bash
cd <current-release>/mocm
helmfile -f helmfile.yaml -n fusion diff
```

Then apply with the standard command from `mocm/README.md`:

```bash
helmfile -f helmfile.yaml -n fusion sync 2>&1 | tee helmfile-upgrade.log
```

4. ** Helm rollback is per-release, not per-package. If `mocm-service` fails to upgrade, roll back only that release:

```bash
helm rollback mocm-service -n fusion
```

You do **not** need to roll back the Terraform layer just because the Helm layer failed.

5. **Chart-level changes** are tracked in `mocm/CHANGELOG.md`. Read the entry for the version shipped with this release before upgrading — any `### Changed` or `### Removed` item there may require values-file edits beyond the steps above.

## Stage 4 — Decommission ElastiCache (Redis) after Valkey cutover

After Path A/B + the Helm upgrade above, **both** caches are running so applications can be migrated without downtime:

| Resource | State after the upgrade apply |
| ---- | ---- |
| `aws_elasticache_cluster.elasticache` (Redis) | Still serving live traffic |
| `aws_elasticache_replication_group.valkey` | Created, idle, ready to use |

Run Stage 4 **only after** every workload that used the old Redis is pointing at the Valkey endpoint (stored in Secrets Manager as `<name_prefix>/valkey/<valkey_username>`) and you have observed Valkey serving traffic for at least one full business cycle.

### 4.1 Verify nothing still depends on ElastiCache (Redis)

```bash
# Connections to the old cache cluster should be 0 over the observation window.
aws cloudwatch get-metric-statistics \
  --namespace AWS/ElastiCache \
  --metric-name CurrConnections \
  --dimensions Name=CacheClusterId,Value=<name_prefix>-cache \
  --statistics Maximum --period 300 \
  --start-time "$(date -u -d '24 hours ago' +%FT%TZ)" \
  --end-time   "$(date -u +%FT%TZ)"
```

Also grep the live Helm values for any hostnames still pointing at the old endpoint:

```bash
grep -RnE 'elasticache|redis\.amazonaws\.com' <current-release>/mocm/
```

If anything matches, finish the application-layer cutover before continuing.

### 4.2 (Optional) Take a final snapshot

If you want a last-chance restore point before destroying the cluster:

```bash
aws elasticache create-snapshot \
  --cache-cluster-id <name_prefix>-cache \
  --snapshot-name    <name_prefix>-cache-final
```

### 4.3 Rename the file back so OpenTofu plans a destroy

```bash
cd <current-release>/terraform/aws
mv 09-elasticache.tf 09-elasticache.tf.2603
```

Renaming back to `.2603` deactivates the resource block **and** its co-located `elasticache_*` variables in one step (they live in the same file — see the header comment in `09-elasticache.tf.2603`).

### 4.4 Plan and apply the teardown

```bash
tofu plan -out tfplan
#    Expect destroys for:
#      aws_elasticache_cluster.elasticache
#      aws_elasticache_parameter_group.elasticache
#      aws_elasticache_subnet_group.elasticache
#    No destroy or replace on any *valkey* resource — if you see one, STOP.

tofu apply tfplan
```

The matching security group `aws_security_group.elasticache` is defined in `02-sg.tf` and is **not** touched by renaming `09-elasticache.tf`. If nothing else references it after teardown, remove it in a follow-up commit.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
