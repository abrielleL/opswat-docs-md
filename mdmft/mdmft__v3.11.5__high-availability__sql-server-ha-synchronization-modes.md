<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/high-availability/sql-server-ha-synchronization-modes -->

# Synchronization Modes

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

The supported configuration for MetaDefender Managed File Transfer™ database high availability is **synchronous commit** with **automatic failover**. Configure both replicas this way when you create the Availability Group.

- **Synchronous commit** — a transaction is not acknowledged until it has been hardened on both the primary and the secondary replica, so no committed data is lost when the primary fails.
- **Automatic failover** — if the primary becomes unavailable, the cluster promotes the secondary to primary automatically, with no manual intervention. Automatic failover requires synchronous commit, because the cluster only promotes a secondary that is guaranteed to hold every committed transaction.

Set both replicas to **Availability Mode = Synchronous commit** and **Failover Mode = Automatic** in the New Availability Group Wizard — see [Setup](/docs/mdmft/v3.11.5/high-availability/sql-server-ha-setup).

Synchronous commit waits for the secondary on every commit, so the latency between replicas directly affects write performance.
