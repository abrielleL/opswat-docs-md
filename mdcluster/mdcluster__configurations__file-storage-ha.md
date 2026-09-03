<!-- source: https://www.opswat.com/docs/mdcluster/configurations/file-storage-ha -->

# High Availability support for File Storage

### [Key concept](/docs/mdcluster/configurations/file-storage-ha#key-concept)

The High Availability solution for MetaDefender Cluster (MD Cluster) **File Storage** is implemented in this manner:

- A file is stored across multiple MD Cluster **File Storages** by MD Cluster **API Gateway** or **MetaDefender Core**.
- MD Cluster **API Gateway** or **MetaDefender Core** must request all MD Cluster **File Storage** instances for a file existence or a file download.

Info

A minimum of **three** MD Cluster File Storage instances must be installed on separate hosts for High Availability solution to function properly.

All MD Cluster File Storage instances must be of an identical version.

### [Setup Instructions](/docs/mdcluster/configurations/file-storage-ha#setup-instructions)

1. Setup MD Cluster **File Storage** instances on individual servers.
2. Sign to MD Cluster **Control Center** console with your Administrator account.
3. Navigate to `Inventory` > `Services`.
4. Expand the `File Storage Service` group.
5. Click `Add service`.
6. Enter the values for `Name`, `Host`, `Port` and `Connection Key` fields of individual MD Cluster File Storage instances set up in Step 1.
7. Click the `Check` icon in the bottom right to complete.

8. Ensure all MD Cluster `File Storage` instances are healthy and reachable by MD Cluster `Control Center`.

9. Click on the gear icon in the top left of `File Storage Service` group to configure the minimum and maximum replicas.

- Minimum replica: The minimum number of data copies that must be written for the operation to succeed.
- Maximum replica: The maximum of data copies stored across the system.

Info

To balance performance and high availability efficiency, the minimum and maximum replicas should be set to the following values:

- `Min replica` = 2
- `Max replica` = 3

10. Click `Save` to complete.
