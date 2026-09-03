<!-- source: https://www.opswat.com/docs/mdmft/high-availability/sql-server-ha-verification-queries -->

# Verification Queries

Summarize Page    Connect to Cursor Connect to VS Code

Use these to check the state of the Availability Group and cluster. Run the SQL queries against the listener unless noted; the listener routes to the current primary.

## [Which node is primary](/docs/mdmft/high-availability/sql-server-ha-verification-queries#which-node-is-primary)

SELECT @@SERVERNAME AS PrimaryNode;
## [Replica roles and health](/docs/mdmft/high-availability/sql-server-ha-verification-queries#replica-roles-and-health)

Connect to the primary for complete results; a secondary returns only partial rows.

SELECT ag.name, ar.replica_server_name, ars.role_desc,
ars.operational_state_desc, ars.synchronization_health_desc
FROM sys.dm_hadr_availability_replica_states ars
JOIN sys.availability_replicas ar ON ars.replica_id = ar.replica_id
JOIN sys.availability_groups ag ON ag.group_id = ar.group_id;
## [Per-database synchronization state](/docs/mdmft/high-availability/sql-server-ha-verification-queries#per-database-synchronization-state)

This is the gate for automatic failover — both databases must be `SYNCHRONIZED` on the secondary.

SELECT ar.replica_server_name AS Node, drs.is_primary_replica AS IsPrimary,
drs.synchronization_state_desc AS SyncState, drs.synchronization_health_desc AS Health
FROM sys.dm_hadr_database_replica_states drs
JOIN sys.availability_replicas ar ON drs.replica_id = ar.replica_id
ORDER BY ar.replica_server_name;
## [Availability mode and failover mode](/docs/mdmft/high-availability/sql-server-ha-verification-queries#availability-mode-and-failover-mode)

SELECT ar.replica_server_name, ar.availability_mode_desc, ar.failover_mode_desc
FROM sys.availability_replicas ar;
## [Cluster and witness health](/docs/mdmft/high-availability/sql-server-ha-verification-queries#cluster-and-witness-health)

Get-ClusterNode -Cluster sqlclus | Format-Table Name,State,DynamicWeight
Get-ClusterResource -Cluster sqlclus | Where-Object ResourceType -like "*File Share*" | Format-Table Name,State
Get-ClusterGroup -Cluster sqlclus | Format-Table Name,OwnerNode,State
