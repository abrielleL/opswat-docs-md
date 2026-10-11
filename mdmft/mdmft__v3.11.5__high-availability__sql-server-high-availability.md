<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/high-availability/sql-server-high-availability -->

# SQL Server High Availability

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This section describes how to make the MetaDefender Managed File Transfer™ database tier highly available by hosting its databases in a **SQL Server Always On Availability Group**. MetaDefender Managed File Transfer™ connects to the Availability Group **listener**, which always routes to the current primary replica, so when a database node fails the connection follows the new primary automatically.

This is **database-level** high availability. It is independent of the MetaDefender Managed File Transfer™ application-level [High Availability](/docs/mdmft/v3.11.5/high-availability/high-availability) cluster and can be used on its own or combined with it.

Only a full **Availability Group** is supported, not a Basic Availability Group.

Recent versions of the **Database Configuration Tool** can change the database server **address** (`--server`), not only credentials. This means MetaDefender Managed File Transfer™ can be repointed at an Availability Group listener directly, with no IP-swap or DNS workaround: install MetaDefender Managed File Transfer™ normally, build the Availability Group, then repoint it at the listener.

## [In this section](/docs/mdmft/v3.11.5/high-availability/sql-server-high-availability#in-this-section)

- [Architecture](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-architecture) — the machines and how traffic flows through the listener.
- [Requirements](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-requirements) — editions, accounts, and ports.
- [Setup](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-setup) — the full build, cluster to failover test.
- [Synchronization Modes](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-synchronization-modes) — synchronous, asynchronous, readable secondary, multi-subnet.
- [Troubleshooting](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-troubleshooting) — common failures and fixes.
- [Verification Queries](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-verification-queries) — check roles, sync state, and cluster health.
