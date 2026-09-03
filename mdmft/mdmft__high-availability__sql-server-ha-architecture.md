<!-- source: https://www.opswat.com/docs/mdmft/high-availability/sql-server-ha-architecture -->

# Architecture

Summarize Page    Connect to Cursor Connect to VS Code

A minimum setup uses four machines: a domain controller, a MetaDefender Managed File Transfer™ instance, and two SQL Server replicas. MetaDefender Managed File Transfer™ connects to the first replica to create its databases; the second replica receives copies of those databases through the Availability Group.

| Machine | Role |
| --- | --- |
| Domain controller | Active Directory, DNS, and the cluster's file-share witness |
| MetaDefender Managed File Transfer™ host | Runs MetaDefender Managed File Transfer™; connects to the database through the Availability Group listener |
| SQL node 1 | SQL Server replica (primary), Windows Failover Cluster node. Holds the MetaDefender Managed File Transfer™ databases, created here during installation |
| SQL node 2 | SQL Server replica (secondary), Windows Failover Cluster node |
| Availability Group listener | The virtual name and IP that MetaDefender Managed File Transfer™ uses to reach the database (a logical endpoint, not a machine) |

The MetaDefender Managed File Transfer™ databases `sft_data` and `sft_conn` are placed into the Availability Group with **synchronous commit** and **automatic failover**. Clients connect only through the listener; the listener directs every connection to the current primary replica.

When the primary replica becomes unavailable, the Windows Server Failover Cluster promotes the secondary to primary and the listener begins directing connections to it. MetaDefender Managed File Transfer™ reconnects through the same listener name with no configuration change.

This covers **database** high availability only. MetaDefender Managed File Transfer™'s own **application** high availability — active/passive MetaDefender® MFT nodes behind the MetaDefender MFT High Availability Controller™ — is a separate layer, described under [High Availability](/docs/mdmft/high-availability/high-availability). In production the two can be combined, with the MetaDefender Managed File Transfer™ nodes pointing at the Availability Group listener.

Continue to [Requirements](/docs/mdmft/high-availability/sql-server-ha-requirements).
