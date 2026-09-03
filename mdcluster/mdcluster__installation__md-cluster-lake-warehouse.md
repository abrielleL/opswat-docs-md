<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-lake-warehouse -->

# Lake and Warehouse setup

### [Overview](/docs/mdcluster/installation/md-cluster-lake-warehouse#overview)

This section describes how to set up the Data Lake and Data Warehouse in PostgreSQL. Once configured, execution services (such as MD Core, MD Cluster API Gateway and MD Cluster Callback Service) can store and retrieve scan results from them, and MD Cluster Control Center can access them to generate executive reports.

---

### [Prerequisites](/docs/mdcluster/installation/md-cluster-lake-warehouse#prerequisites)

1. **PostgreSQL Service**: Must be installed and running.
2. **MD Cluster Control Center**: Must be installed.
3. **Superuser Rights**: PostgreSQL user must have superuser privileges.

---

### [Assumption](/docs/mdcluster/installation/md-cluster-lake-warehouse#assumption)

It is assumed that PostgreSQL Server A is designated to host the Data Lake, while PostgreSQL Server B hosts the Data Warehouse. The Data Lake must be configured first, as the Data Warehouse will connect to it as its primary data source.

---

### [Windows](/docs/mdcluster/installation/md-cluster-lake-warehouse#windows)

1. On the machine hosting MD Cluster **Control Center**, navigate to the folder:

PowershellCopyC:\Program Files\OPSWAT\MetaDefender Cluster Control Center

2. Run the following command to set up **Data Lake** on PostgreSQL Server A:

PowershellCopymd-cluster-dbready.exe --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --target=lake

3. Run the following command to set up **Data Warehouse** on PostgreSQL Server B:

PowershellCopymd-cluster-dbready.exe --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --lake-host=<lake-postgres-host> --lake-port=<lake-postgres-port> --lake-user=<lake-postgres-user> --lake-password=<lake-postgres-password> --target=warehouse

---

### [Linux](/docs/mdcluster/installation/md-cluster-lake-warehouse#linux)

1. On the machine hosting MD Cluster Control Center, navigate to the folder:

BashCopy/usr/sbin

2. Run the following command to set up **Data Lake** on PostgreSQL Server A:

BashCopymd-cluster-dbready --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --target=lake

3. Run the following command to set up **Data Warehouse** on PostgreSQL Server B:

BashCopymd-cluster-dbready --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --lake-host=<lake-postgres-host> --lake-port=<lake-postgres-port> --lake-user=<lake-postgres-user> --lake-password=<lake-postgres-password> --target=warehouse

---

### [Combined Lake and Warehouse](/docs/mdcluster/installation/md-cluster-lake-warehouse#combined-lake-and-warehouse)

If the Data Lake and Data Warehouse are hosted on the same PostgreSQL instance, a combined setup command can be used:

BashCopymd-cluster-dbready --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --target=lake,warehouseWarning

While this approach is simpler and faster to deploy, it is not recommended for large-scale or long-running systems due to potential performance and scalability limitations.
