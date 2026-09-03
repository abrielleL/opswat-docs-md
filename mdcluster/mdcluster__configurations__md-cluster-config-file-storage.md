<!-- source: https://www.opswat.com/docs/mdcluster/configurations/md-cluster-config-file-storage -->

# File Storage

MetaDefender Cluster (MD Cluster) introduces a built-in file storage server known as MD Cluster **File Storage**. The server stores and manages the live time of files and their duplications.

The administrator can set up MD Cluster to work with a single instance of MD Cluster **File Storage** or build a group of MD Cluster **File Storage** instances.

From `Inventory` > `Services` of the MD Cluster **Control Center** web console, the administrator can click on the gear icon in the top left corner of the `File Storage` group to access MD Cluster **File Storage** settings.

## [Multiple instances](/docs/mdcluster/configurations/md-cluster-config-file-storage#multiple-instances)

When several instances of MD Cluster **File Storage** are added to the File Storage group, `Min Replica` and `Max Replica` enable the administrator to configure the operation of the storage group, as shown in the table below.

| Setting | Behavior |
| --- | --- |
| `Min replica` = 1  `Max replica` = 1 | Every file is stored without a backup across all File Storage servers. File Storage servers in the group implement a **Sharding** solution for file storage. Since there is no backup for any file, if one server in the group goes down, files managed by that server will be lost to the clients. This setup provides the best performance but also poses a high risk of data loss. |
| `Min replica` > 1  `Max replica` > `Min replica` | Every file is stored on at least `Min replica` number of File Storage servers and at most `Max-replica` number of servers. The setting provides **High Availability** support for File Storage. In most cases, `Min replica` and `Max replica` are configured to 2 and 3, creating a balance between performance and efficiency in High Availability. |
| `Min replica` > 1  `Max replica` = `Min replica` | Every file is fully stored on `Max replica` number of file storage servers and will not succeed if it can not be. This setting is the strictest among three options and should be considered carefully due to its impact on system performance. |

Warning

Replication of a file across several MD Cluster File Storage servers significantly impacts the overall system performance. Hence, the number of replications must be evaluated thoughtfully.

## [Data retention](/docs/mdcluster/configurations/md-cluster-config-file-storage#data-retention)

The administrator can configure data retention for files stored in the File Storage group with the `Clean up range` option. By default, this option is disabled. The administrator has the option to retain files for 12 hours, 1 day, 1 week, etc., starting from the present time.

Info

Files eligible for retention include those produced by CDR, DLP, SBOM, Quarantine engines.

Package (.msi, .deb or .rpm) and module files are marked for cleanup manually and will never be affected by data retention.

## [Data protection](/docs/mdcluster/configurations/md-cluster-config-file-storage#data-protection)

By default, all files stored on the MD Cluster File Storage server are XOR bitwise with a randomly generated binary string. This option is enabled by default to prevent the file from being executed successfully due to unexpected factors. The administrator can disable the option to optimize MD Cluster File Storage performance, though it may expose the system to security risks.
