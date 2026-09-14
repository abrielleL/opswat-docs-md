<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/service-instance-scaling-on-linux -->

# Service Instance Scaling on Linux

This article is applicable only to MetaDefender Storage Security deployments that are running on **Linux**.

Available in **MetaDefender Storage Security 4.4.0** and later.

This guide explains how to run **extra instances** of MetaDefender Storage Security (MDSS) services so your deployment can handle more work in parallel. It's an optional setting for larger or busier environments.

If you've read the [Scan Priorities & Throughput Tuning](/docs/mdss/knowledge-base/scan-priorities) guide, here's the key difference:

- That guide tunes how hard a **single** service container works (more workers, bigger batches).
- This guide adds **more containers** of the same service, so the work is shared across them.

Info

Analogy: if a single service container is a moving team clearing boxes, then instance scaling adds more teams — each with their own truck — all working the same job at the same time.

---

## [How it works](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#how-it-works)

By default, each scalable service runs as **one** container. You can add up to **two extra** containers per service using the `*_ADDITIONAL_INSTANCES` settings.

The value is simply **how many extra containers to add on top of the default one**:

| Value | Total containers that run |
| --- | --- |
| `0` | 1 (default — just the original) |
| `1` | 2 |
| `2` | 3 (the maximum) |

The maximum is **2 additional** (3 total). Any higher value is automatically reduced to 2.

When MDSS starts, it reads these values and launches the extra containers automatically. They join the same workload and start sharing it immediately — no other configuration is needed.

---

## [What you can scale](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#what-you-can-scale)

There are two groups of services you can scale.

### [1. Central services](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#1-central-services)

These are the core engines of the scanning pipeline:

| Setting | Service | What it does |
| --- | --- | --- |
| `DISCOVERY_SERVICE_ADDITIONAL_INSTANCES` | Discovery | Walks through your storage and finds files to scan |
| `SCANNING_SERVICE_ADDITIONAL_INSTANCES` | Scanning | Scans each file for threats |
| `REMEDIATIONS_SERVICE_ADDITIONAL_INSTANCES` | Remediation | Acts on flagged files (move, delete, quarantine, etc.) |

### [2. Storage connectors (per integration)](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#2-storage-connectors-per-integration)

Each storage type you connect to has its own connector container. You can scale each one independently, so you can add capacity only where you need it:

| Setting | Storage type |
| --- | --- |
| `AMAZONSDK_ADDITIONAL_INSTANCES` | Amazon S3 |
| `AZUREBLOB_ADDITIONAL_INSTANCES` | Azure Blob Storage |
| `AZUREFILES_ADDITIONAL_INSTANCES` | Azure Files |
| `NFS_ADDITIONAL_INSTANCES` | NFS |
| `SMB_ADDITIONAL_INSTANCES` | SMB / CIFS |
| `SFTP_ADDITIONAL_INSTANCES` | SFTP |
| `FTP_ADDITIONAL_INSTANCES` | FTP |
| `MFT_ADDITIONAL_INSTANCES` | Managed File Transfer (MFT) |
| `BOX_ADDITIONAL_INSTANCES` | Box |
| `GRAPH_ADDITIONAL_INSTANCES` | Microsoft 365 (OneDrive / SharePoint Online) |
| `GOOGLECLOUD_ADDITIONAL_INSTANCES` | Google Cloud Storage |
| `ALIBABACLOUD_ADDITIONAL_INSTANCES` | Alibaba Cloud OSS |
| `ORACLESDK_ADDITIONAL_INSTANCES` | Oracle Cloud Storage |

Info

A connector is only scaled if that storage type is enabled in your deployment. Setting a value for a connector you don't use has no effect.

---

## [Examples](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#examples)

**Example 1 — Default (no scaling)**

SCANNING_SERVICE_ADDITIONAL_INSTANCES=0

One scanning container runs. This is the default and is right for most deployments.

**Example 2 — Add one extra scanning container**

SCANNING_SERVICE_ADDITIONAL_INSTANCES=1

Two scanning containers run and share the scanning workload — roughly doubling scanning capacity.

**Example 3 — Scale the whole central pipeline**

DISCOVERY_SERVICE_ADDITIONAL_INSTANCES=1
SCANNING_SERVICE_ADDITIONAL_INSTANCES=2
REMEDIATIONS_SERVICE_ADDITIONAL_INSTANCES=1

Discovery runs 2 containers, Scanning runs 3, and Remediation runs 2 — useful for a large, busy environment where every stage needs more throughput.

---

## [When should you scale instances?](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#when-should-you-scale-instances)

Add instances when **a single container is already working at full capacity** and your server still has spare CPU and memory to run more containers.

A good order to follow:

1. **First, tune the single container** using the prefetch and consumer-multiplier settings (see *Scan Priorities & Throughput Tuning*). This is the simplest change and often enough.
2. **Then, add instances** if one container — even fully tuned — still can't keep up, and you have the hardware to run more.

If your server's CPU is already near 100%, adding more containers will **not** help — they'll compete for the same resources. In that case, the answer is more hardware (a bigger server, or additional servers), not more instances.

---

## [How to apply changes](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#how-to-apply-changes)

1. Set the desired *ADDITIONAL* *INSTANCES values in your environment configuration (__customer.env**]
2. Restart MDSS so the extra containers are created

Info

Changes only take effect after a restart, because the extra containers are created at startup.

---

## [Things to keep in mind](/docs/mdss/knowledge-base/service-instance-scaling-on-linux#things-to-keep-in-mind)

- **The default (0) is right for most deployments.** Only scale when you have a clear throughput need and spare hardware.
- **The maximum is 2 additional instances (3 total) per service.** Higher values are automatically capped.
- **Only the services listed in this guide can be scaled.** Other MDSS services are designed to run as a single instance and should not be duplicated.
- **More instances need more resources.** Each extra container uses additional CPU and memory. Make sure your server has the capacity before scaling.
- **Instance scaling and worker tuning work together.** You can both add instances *and* tune each container's workers/prefetch for maximum throughput. </content>
