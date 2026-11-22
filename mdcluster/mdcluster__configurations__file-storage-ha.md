<!-- source: https://www.opswat.com/docs/mdcluster/configurations/file-storage-ha -->

# High Availability support for File Storage

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### Key concept

The High Availability solution for MetaDefender Cluster (MD Cluster) **File Storage** is implemented in this manner:

- A file is stored across multiple MD Cluster **File Storages** by MD Cluster **API Gateway** or **MetaDefender Core**.
- MD Cluster **API Gateway** or **MetaDefender Core** must request all MD Cluster **File Storage** instances for a file existence or a file download.

Info

A minimum of **three** MD Cluster File Storage instances must be installed on separate hosts for High Availability solution to function properly.

All MD Cluster File Storage instances must be of an identical version.

### Setup Instructions

1. Setup MD Cluster **File Storage** instances on individual servers.
2. Sign in to MD Cluster **Control Center** console with your Administrator account.
3. Navigate to `Library` > `Services`.
4. Locate the `File Storage` group.
5. Click the `+` (Add a File Storage service) button on the right side of the group.
6. Enter the values for `Name`, `Host`, `Port` and `Connection Key` fields of individual MD Cluster File Storage instances set up in Step 1.
7. Click `Add` to complete.

8. Expand the `File Storage` group and ensure all MD Cluster `File Storage` instances are healthy and reachable by MD Cluster `Control Center`.

9. Click the gear icon (`Settings`) on the right side of the `File Storage` group to configure the minimum and maximum replicas.

- `Min Replica`: The minimum number of data copies that must be written for the operation to succeed.
- `Max Replica`: The maximum of data copies stored across the system.

Info

To balance performance and high availability efficiency, the minimum and maximum replicas should be set to the following values:

- `Min Replica` = 2
- `Max Replica` = 3

10. Click `Save` to complete.
