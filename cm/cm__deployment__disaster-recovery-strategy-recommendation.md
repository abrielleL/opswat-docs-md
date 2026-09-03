<!-- source: https://www.opswat.com/docs/cm/deployment/disaster-recovery-strategy-recommendation -->

# Disaster Recovery Strategy Recommendation

## Introduction

This document gives customers and operations teams a high-level view of the Disaster Recovery (DR) approach for the MOCM on‑premises deployment artifacts delivered with this project.

Scope: Infrastructure rebuild and MongoDB data recovery using AWS EBS snapshots (via OpenTofu/Terraform-compatible IaC) and operational procedures.

Out of scope: Application-level point-in-time recovery (PITR), logical backups (e.g., mongodump), and any customer-specific customizations unless explicitly documented.

This document does not replace detailed operational runbooks; use the links in References for step-by-step procedures.

## Assumptions

- AWS account with required permissions to create/attach EBS volumes, manage security groups, and launch EC2 instances.
- EBS snapshot IDs for MongoDB data and journal volumes are available and documented.
- Network connectivity and DNS are configurable to restore service endpoints after a rebuild.

## DR Objectives: RPO, RTO, and Limitations

| **Objective** | **Typical Expectation (Order of Magnitude)** | **Notes** |
| ---- | ---- | ---- |
| Recovery Point Objective (RPO) | Aligned to latest successful EBS snapshot | - Depends on snapshot frequency and success - No PITR; data between last snapshot and incident is unrecoverable |
| Recovery Time Objective (RTO) | Hours (influenced by snapshot restore and instance provisioning time) | - Varies by region capacity, EBS size, throughput limits - Operational steps include IaC plan/apply and service validation |

Actual RPO/RTO depends on your AWS environment (region, quotas), data size, and operational processes, and must be validated via recovery drills before committing to any SLA.

## High-level DR Flow

1. Prepare AWS account and networking for rebuild (VPC/subnets, security groups, IAM roles, KMS keys if applicable).
2. Ensure EBS snapshot IDs for MongoDB data and journal volumes are documented and accessible in the target region.
3. Select DR path in IaC: switch MongoDB volumes from greenfield creation to restore from snapshots.
4. Plan and apply infrastructure with OpenTofu (Terraform-compatible).
5. Run operational verification: MongoDB integrity checks, application services health, endpoint validation.

## DR Paths

### Path A: Greenfield Rebuild (no data restore)

Provision infrastructure and bootstrap services without restoring MongoDB data. Intended for testing or environments where data can be reseeded.

- Use default volume creation for MongoDB data and journal in the IaC modules.
- Skip snapshot variables and restore logic.

### Path B: Snapshot-based Restore (recommended)

This DR path switches MongoDB from creating empty (greenfield) data volumes to restoring volumes from your provided EBS snapshot IDs.

Enable the snapshot-restore code path in the IaC and provide the snapshot IDs for the MongoDB data and journal volumes. Ensure instance types, storage types, and security groups match production requirements.

## IaC Controls and Variables

The deployment uses OpenTofu (Terraform-compatible) modules. Variables control whether MongoDB volumes are created fresh or restored from specific EBS snapshots.

- Set snapshot restore flags and provide snapshot IDs for data and journal volumes.
- Keep variable files for DR separate from production defaults to avoid accidental overwrites.

## Command Examples

Run the following from the root of the IaC project when using the DR variable file:

```bash
tofu init
tofu plan -var-file=dr-mongodb.tfvars
tofu apply -var-file=dr-mongodb.tfvars -auto-approve
```

Use a separate workspace or state backend key for DR if you also manage non-DR environments with the same repository.

## Operational Validation After Restore

- Verify EC2 instances, security groups, and EBS volume attachments are as expected.
- Start MongoDB and confirm it recognizes the restored data and journal volumes.
- Run MongoDB integrity checks and basic CRUD tests.
- Validate application services and endpoints dependent on MongoDB.

## Risks and Mitigations

- Mismatched snapshot and AMI/kernel versions can cause boot or mount failures. Mitigation: align AMI and drivers with the environment where snapshots were taken.
- Insufficient regional capacity or throttling may slow restores. Mitigation: pre-validate quotas and consider warm standby options for critical workloads.
- Incorrect device mapping breaks MongoDB data paths. Mitigation: verify device names and fstab/systemd mounts in IaC and OS configs.
