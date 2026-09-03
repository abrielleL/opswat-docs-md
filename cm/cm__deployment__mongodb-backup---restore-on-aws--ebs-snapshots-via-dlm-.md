<!-- source: https://www.opswat.com/docs/cm/deployment/mongodb-backup---restore-on-aws--ebs-snapshots-via-dlm- -->

# MongoDB Backup & Restore on AWS (EBS Snapshots via DLM)

### **1) Overview**

This document explains the backup approach for a MongoDB deployment running as a **replica set on Amazon EC2** with **separate EBS data volumes**. Backups are implemented using **AWS Data Lifecycle Manager (DLM)** to create **scheduled EBS snapshots** of MongoDB volumes, with an option to **copy snapshots to a second AWS region** for disaster recovery.

This approach provides **volume-level (block) backups** at specific snapshot times. It is **not** a MongoDB application-aware backup and does **not** provide continuous point-in-time recovery (PITR) by itself.

---

### **2) What is included (automated by the OpenTofu module)**

The infrastructure automation provisions and manages:

- **AWS DLM policy** to take **scheduled EBS snapshots** of MongoDB volumes selected by tag.
- **Optional cross-region snapshot copy**, if configured.
- Required **IAM execution role** for DLM.
- Consistent **volume tagging** so the correct volumes are included in the snapshot lifecycle.

**Result:** You receive periodic EBS snapshots for tagged MongoDB volumes, plus optional copies stored in another region.

---

### **3) What is NOT included (out of scope for this module)**

The following are **not** provisioned or operated by this automation and require a separate design/installation if needed:

- **Point-in-time recovery (PITR)** via continuous oplog archival (e.g., to S3).
- **Percona Backup for MongoDB (PBM)**, MongoDB Ops Manager/Cloud Manager agents, or similar MongoDB-aware backup tools.
- **Logical backups** such as `mongodump`, and any Cron/EventBridge/SSM scheduling for those workflows.

If you require PITR or logical backups, those must be implemented as **separate components with separate operational runbooks**.

---

### **4) Backup behavior (DLM snapshots)**

**Snapshot selection**

- DLM targets EBS volumes with a specific tag key/value (module-configured).
- MongoDB **data volumes are always tagged** for snapshot inclusion.
- **Root volume snapshots** are optional and depend on configuration.

**Schedule**

- Snapshots run on a DLM schedule (cron in **UTC**).
- The minimum practical interval for DLM is typically **1 hour**.

**Retention**

- Snapshots are retained per configured count **per volume** in the primary region.

**Cross-region copy (optional)**

- When enabled, every snapshot is **copied** to a destination region and retained there for a configured number of days.
- This increases **storage** and **data transfer** costs.

**Consistency model**

- DLM snapshots are **crash-consistent at the block level** (EBS snapshot semantics).
- They are **not** a quiesced MongoDB backup and do not guarantee a single “cluster-wide consistent instant” across all replica set members.

**Important clarification**

- With cross-region copy enabled, there are **two storage locations** (primary snapshots + copied snapshots), but it is the **same snapshot point-in-time**, stored in two regions—**not two independent backup methods**.

---

### **5) RPO / RTO expectations (high level)**

These are **order-of-magnitude** expectations and must be validated in your environment before committing to SLAs.

- **DLM snapshots only:**
  - **RPO:** Up to **one backup interval** (e.g., daily snapshots → up to ~24 hours of potential data loss).
  - **RTO:** Often **moderate to fast**, depending on restore mechanics (create volume from snapshot, attach, start `mongod`, validate).
- **Replica set failover (no restore):**
  - Very fast recovery for **node/AZ failure** with near-zero RPO for that failure class.
  - **Does not protect** against **logical mistakes** (bad writes, `dropDatabase`, etc.), because those replicate to all members.

To “undo” to an exact point in time (beyond snapshot times), you typically need **PITR** (oplog-based) or additional patterns (e.g., delayed secondary)—which are **outside** this DLM-only scope.

---

### **6) Customer responsibilities/assumptions**

- You are responsible for selecting the **schedule, retention, and (optional) cross-region copy** settings that meet your recovery objectives.
- If you require **PITR** or **logical backups**, you must implement and operate them separately (e.g., PBM + S3, or `mongodump` workflows).
- Regular **restore testing** in a non-production environment is strongly recommended to confirm real RPO/RTO and operational readiness.

---

### **7) How to verify backups (customer checklist)**

**AWS Console**

1. Go to **EC2 → Lifecycle Manager** and confirm the DLM policy is **Enabled**.
2. Go to **EC2 → Snapshots** (primary region) and confirm snapshots exist for the expected cadence.
3. If cross-region copy is enabled, switch to the **destination region** and confirm copied snapshots exist.
4. Confirm timestamps align with the configured schedule (**UTC**).

**AWS CLI (examples)** Replace `REGION` with your AWS region.

List DLM policies:

```bash
aws dlm get-lifecycle-policies --region REGION --output table
```

Describe a lifecycle policy:

```bash
aws dlm get-lifecycle-policy --policy-id policy-XXXXXXXX --region REGION
```

List snapshots by tag:

```bash
aws ec2 describe-snapshots --region REGION \ --owner-ids self \ --filters "Name=tag:BackupSource,Values=dlm-mongodb" \ --query 'Snapshots[*].[SnapshotId,StartTime,VolumeId,State]' \ --output table
```
