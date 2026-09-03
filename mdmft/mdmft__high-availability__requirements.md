<!-- source: https://www.opswat.com/docs/mdmft/high-availability/requirements -->

# Requirements

Summarize Page    Connect to Cursor Connect to VS Code

| Component | Requirement |
| --- | --- |
| Operating system | Windows Server 2019 / 2022 / 2025 (64-bit). All SQL nodes joined to the same Active Directory domain |
| SQL Server edition | **Enterprise** (full Availability Group). Developer edition is Enterprise-equivalent and free for non-production, so it is suitable for lab and test environments |
| SQL Server version | 2016 or later (Database Level Health Detection requires 2016 or newer) |
| SQL service account | A single **domain** account (for example `DOMAIN\svc-sql`), identical on both nodes, so the replicas can authenticate to each other |
| Cluster | Windows Server Failover Cluster (WSFC) across both SQL nodes, plus a **file-share witness** for quorum |
| Ports | `1433` (SQL client and listener), `5022` (Availability Group data-mirroring endpoint), `1434/UDP` (SQL Browser, only for named instances) |

For the general MetaDefender® MFT prerequisites and the High Availability file storage requirements, see [Requirements](/docs/mdmft/high-availability/requirements).

> **Info**
>
> Only a full **Availability Group** is supported, not a Basic Availability Group. This is why Enterprise (or the Enterprise-equivalent Developer) edition is required — Standard edition offers only Basic Availability Groups.

> **Warning**
>
> MetaDefender® MFT expects **Force Encryption** to be enabled on SQL Server, but the MetaDefender® MFT services cannot persist the `TrustServerCertificate` setting. Through a listener, each replica presents its own certificate whose name does not match the listener name, so validated TLS requires a certificate whose **Subject Alternative Name covers the listener name and both node names**, installed in the MetaDefender® MFT host's LocalMachine Trusted Root store. Alternatively, disable Force Encryption (or set `--encrypt false` when repointing) for environments where transport encryption is not required.

Continue to [Setup](/docs/mdmft/high-availability/sql-server-ha-setup).
