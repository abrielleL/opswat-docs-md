<!-- source: https://www.opswat.com/docs/mdmft/high-availability/sql-server-ha-troubleshooting -->

# Troubleshooting

Summarize Page    Connect to Cursor Connect to VS Code

Common failures encountered when setting up or operating MetaDefender Managed File Transfer™ on a SQL Server Availability Group, and how to resolve them.

## [Replica stuck in RESOLVING and MetaDefender Managed File Transfer™ cannot reach the database](/docs/mdmft/high-availability/sql-server-ha-troubleshooting#replica-stuck-in-resolving-and-product_name-cannot-reach-the-database)

The cluster lost quorum, almost always because the file-share witness was offline, leaving a two-node cluster with an even vote count that cannot elect a new primary.

Make the witness healthy: confirm the cluster computer account (`DOMAIN\sqlclus$`) has Full permission on both the share and NTFS, re-run `Set-ClusterQuorum -NodeAndFileShareMajority`, and verify the File Share Witness resource is Online with both nodes at `DynamicWeight 1`.

## [Availability Group role shows Failed and will not fail over](/docs/mdmft/high-availability/sql-server-ha-troubleshooting#availability-group-role-shows-failed-and-will-not-fail-over)

The cluster role exhausted its failover threshold (the maximum number of failovers allowed within the failover period), which is common after repeated failover testing, so the cluster stops retrying and parks the role in a failed state.

Raise the threshold and bring the role back online:

(Get-ClusterGroup -Cluster sqlclus -Name ag-mft).FailoverThreshold = 20
Start-ClusterGroup -Name ag-mft -Cluster sqlclus
## [Cluster validation fails "Validate Active Directory Configuration"](/docs/mdmft/high-availability/sql-server-ha-troubleshooting#cluster-validation-fails-validate-active-directory-configuration)

Usually caused by running the validation while signed in as a **local** account rather than a domain account, or by a broken secure channel or stale DNS after renaming a node.

Sign in as a domain administrator; if needed, run `Test-ComputerSecureChannel -Repair` and `ipconfig /registerdns`. The other validation warnings (drivers, updates, IP configuration, network) are expected in an isolated environment and do not block cluster creation.

## [Secondary databases stuck in NOT SYNCHRONIZING](/docs/mdmft/high-availability/sql-server-ha-troubleshooting#secondary-databases-stuck-in-not-synchronizing)

Data movement is suspended. Resume it on the secondary:

ALTER DATABASE [sft_data] SET HADR RESUME;
ALTER DATABASE [sft_conn] SET HADR RESUME;
## [MetaDefender Managed File Transfer™ cannot connect to the database](/docs/mdmft/high-availability/sql-server-ha-troubleshooting#product_name-cannot-connect-to-the-database)

Work through the likely causes in order: the SQL Server service is not running after a reboot (set it to Automatic); TCP/IP is not enabled, or was enabled without restarting the service; a named instance is using a dynamic port; the firewall is blocking `1433`; or Force Encryption is on with an untrusted self-signed certificate.

Test reachability first with `Test-NetConnection <host> -Port 1433`, then address each layer. Using the default instance on a static port `1433` avoids the SQL Browser dependency.

## [Uninstalling reports that the database cannot be dropped](/docs/mdmft/high-availability/sql-server-ha-troubleshooting#uninstalling-reports-that-the-database-cannot-be-dropped)

A database that is part of an Availability Group cannot be dropped — this is expected SQL Server behavior. Remove the databases from the Availability Group first if they must be deleted. The MetaDefender Managed File Transfer™ uninstaller reports this as a warning and still completes successfully.
