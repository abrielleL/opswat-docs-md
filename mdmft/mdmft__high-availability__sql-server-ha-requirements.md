<!-- source: https://www.opswat.com/docs/mdmft/high-availability/sql-server-ha-requirements -->

# Requirements

Summarize Page    Connect to Cursor Connect to VS Code

| Component | Requirement |
| --- | --- |
| Operating system | Windows Server 2019 / 2022 / 2025 (64-bit). All SQL nodes joined to the same Active Directory domain |
| SQL Server edition | **Enterprise** (full Availability Group) |
| SQL Server version | 2016 or later (Database Level Health Detection requires 2016 or newer) |
| SQL service account | A single **domain** account (for example `DOMAIN\svc-sql`), identical on both nodes, so the replicas can authenticate to each other |
| Cluster | Windows Server Failover Cluster (WSFC) across both SQL nodes, plus a **file-share witness** for quorum |
| Ports | `1433` (SQL client and listener), `5022` (Availability Group data-mirroring endpoint), `1434/UDP` (SQL Browser, only for named instances) |

For the general MetaDefender Managed File Transfer™ prerequisites and the High Availability file storage requirements, see [Requirements](/docs/mdmft/high-availability/requirements).

For more info about **SQL Server Always On availability group** prerequisites: [Availability Group: Prerequisites, Restrictions, and Recommendations - SQL Server Always On | Microsoft Learn](https://learn.microsoft.com/en-us/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability?view=sql-server-ver16)

Only a full **Availability Group** is supported, not a Basic Availability Group. This is why Enterprise (or the Enterprise-equivalent Developer) edition is required — Standard edition offers only Basic Availability Groups.

If MetaDefender Managed File Transfer™ connects to the database over an **encrypted** connection, the SQL Server certificate must be trusted by the MetaDefender Managed File Transfer™ host and valid for the Availability Group **listener name**. Use a certificate that meets both conditions, or connect without encryption.

Continue to [Setup](/docs/mdmft/high-availability/sql-server-ha-setup).
