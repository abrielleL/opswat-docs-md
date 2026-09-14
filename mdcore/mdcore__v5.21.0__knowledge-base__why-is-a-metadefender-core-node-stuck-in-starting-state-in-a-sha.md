<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha -->

# Why Is a MetaDefender Core Node Stuck in Starting State in a Shared-Database Cluster?

**Info:**

- This article applies to MetaDefender Core in **shared-database (multi-node)** deployments running versions **prior to 5.21.0**.
## [**Issue**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#issue)

In a multi-node MetaDefender Core cluster sharing a single PostgreSQL database, a node may remain stuck in **Starting** state for an extended period, potentially hours, after being restarted. The issue is caused by a database deadlock between the restarting node's one-time startup privilege-grant operation and the background statistics refresh job (`warehouse.refresh`) running on other active nodes.

## [**Symptoms**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#symptoms)

- **Node stuck at "Starting":** The restarted Core node does not transition to a healthy or running state. The web UI and REST API remain unavailable on that node.
- **Extended startup duration:** The node may remain in Starting state for minutes to hours, depending on the load on the other nodes.
- **No scanning impact on other nodes:** File scanning on the remaining active nodes continues normally. The issue is isolated to the restarting node.
- **Deadlock errors in PostgreSQL logs:** Repeated `ERROR: deadlock detected` entries show contention between the startup `GRANT` statement and `warehouse.refresh()`.

## [**Evidence**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#evidence)

### [**PostgreSQL log pattern**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#postgresql-log-pattern)

ERROR: deadlock detected
DETAIL: Process <PID_A> waits for ShareLock on transaction <TXN_1>; blocked by process <PID_B>.
Process <PID_B> waits for ShareLock on transaction <TXN_2>; blocked by process <PID_A>.
Process <PID_A>: GRANT ALL PRIVILEGES ON SCHEMA pg_catalog TO <user>; COMMIT; ...
Process <PID_B>: SELECT * FROM warehouse.refresh(<instance_id>::SMALLINT);
### [**Core application log pattern**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#core-application-log-pattern)

CEF:0|OPSWAT|MSCW|<version>|common.base|==== START ====|2|OMSversion=<version> OMSmsgid=356
CEF:0|OPSWAT|MSCW|<version>|core.postgres|Postgres info|2|OMSinfo=Checking for database upgrade OMSmsgid=4085

The node logs `==== START ====` but never progresses to a ready state. The deadlock repeats on each retry cycle until the database happens to cancel the `warehouse.refresh` process instead of the startup process.

## [**Root Cause**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#root-cause)

When a MetaDefender Core node starts up, it performs a one-time database initialization as part of its startup sequence. At the same time, other active nodes in the cluster continuously run background maintenance jobs to keep internal statistics and dashboards up to date.

In versions prior to 5.21.0, these two operations can conflict when they run at the same time, causing the database to cancel the startup transaction. The node then retries, but under sustained cluster activity, the conflict can repeat — keeping the node stuck in Starting state.

This is a known limitation of the shared-database architecture in affected versions and is resolved by upgrading to 5.21.0 or later

## [**Resolution**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#resolution)

Upgrade to **MetaDefender Core 5.21.0** or later, which resolves the startup-versus-refresh deadlock at the application level. No manual workaround is needed after upgrading.

Core 5.21.0 introduces significant UI/UX changes. Plan accordingly.

## [**Prevention**](/docs/mdcore/v5.21.0/knowledge-base/why-is-a-metadefender-core-node-stuck-in-starting-state-in-a-sha#prevention)

- Schedule node restarts during low-load windows to minimize the chance of the background refresh job running concurrently with the startup grant.
- Monitor scan queue depth on remaining nodes before restarting a node. Sustained high queue depth increases the deadlock probability.

**Support:**

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-) before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
