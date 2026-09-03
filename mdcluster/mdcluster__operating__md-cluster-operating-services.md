<!-- source: https://www.opswat.com/docs/mdcluster/operating/md-cluster-operating-services -->

# Services

This section will allow the user to add all necessary services for MetaDefender Cluster to fully function.

### [Data Lake and Data Warehouse](/docs/mdcluster/operating/md-cluster-operating-services#data-lake-and-data-warehouse)

Add the Data Lake and Data Warehouse in this section. Fill out all required fields. If High Availability was configured for [PostgreSQL](/docs/mdcluster/configurations/data-lake-ha), add them to this section as well.

Info

High Availability support for Postgres is only available for Data Lake

### [Redis](/docs/mdcluster/operating/md-cluster-operating-services#redis)

Add the Redis server in this section. Fill out all required fields.

To use an encrypted connection, enable **TLS Configuration** and set the port to the broker's TLS listener.

1. **Verify Certificate**: validates the broker's certificate. Turn it off to encrypt the traffic without verifying the peer.
2. **CA Certificate Path**: path to the CA certificate file. The file is read on the Control Center host, not on the Redis host. Leave it empty to use the operating system's trust store.

If High Availability was configured for [Redis](/docs/mdcluster/configurations/redis-ha), add them to this section as well. TLS settings are per connection, so configure them on each node.

### [RabbitMQ](/docs/mdcluster/operating/md-cluster-operating-services#rabbitmq)

Add the RabbitMQ server in this section. Fill out all required fields.

To use an encrypted connection, enable **TLS Configuration** and set the port to the broker's TLS listener.

1. **Verify Certificate**: validates the broker's certificate. Turn it off to encrypt the traffic without verifying the peer.
2. **CA Certificate Path**: path to the CA certificate file. The file is read on the Control Center host, not on the RabbitMQ host. Leave it empty to use the operating system's trust store.

If High Availability was configured for [RabbitMQ](/docs/mdcluster/configurations/rabbitmq-ha), add every node in this section as well. TLS settings are per connection, so configure them on each node.

### [File Storage](/docs/mdcluster/operating/md-cluster-operating-services#file-storage)

Add the File Storage server in this section. Fill out all required fields. If High Availability was configured for [File Storage](/docs/mdcluster/configurations/file-storage-ha), add them to this section as well.

### [File Storage Settings](/docs/mdcluster/operating/md-cluster-operating-services#file-storage-settings)

Values found in the File Storage Settings can be left in its default settings. However, when configuring High Availability for File Storage. Ensure that the Minimum replica and Maximum replica has been configured correctly. For more information on High Availability for File Storage, click [here](/docs/mdcluster/configurations/file-storage-ha).

- Min replica: The minimum number of data copies that must be written for the operation to succeed.
- Max replica: The maximum of data copies stored across the system.
- Clean up range: The number of days, weeks or months until clean up of files that are sanitized, watermarked files and files processed by Proactive DLP.
- Data protection at rest: The protection mechanism is applied to the files stored in File Storage. By default, all files are salted before being they are saved to disk.

### [Import Services](/docs/mdcluster/operating/md-cluster-operating-services#import-services)

The **Import Services** feature allows you to import connections for multiple service types—including **Data Lake**, **Data Warehouse**, **Redis**, **RabbitMQ**, and **File Storage**—from a single YAML file. This provides a faster alternative to creating each connection manually.

Info
> Importing services replaces all existing connections for each service type included in the YAML file. Connections for service types that are not included in the file remain unchanged

To import services:

1. On the **Services** page, click **Import Services** in the upper-right corner.

2. In the **Import Services** dialog, click **Download YAML Template** to download a sample file. Update the file with the connection details for the service types you want to import, and remove any service type sections that you do not want to import.

3. Drag the completed YAML file into the upload area, or click **Browse** to select the file from your computer.

4. Click **Import** to apply the new service connections.
