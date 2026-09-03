<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-postgresql-windows -->

# Windows

PostgreSQL version 16.9 or higher is required.

### [Prerequisites](/docs/mdcluster/installation/md-cluster-postgresql-windows#prerequisites)

Before installing the PostgreSQL service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Windows 11 23H2+, or Windows Server 2019+. |
| Privileges | Administrator privileges. |
| Installation package | `postgresql-<version>-windwos-x64.exe` |
| Hardware | Minimum 8 vCPU and 16 GB RAM. |
| Disk space | At least 1 TB of available storage on **SSD** or **NVMe** for optimal performance.  Approximately 4 GB of storage is required per 1 million scanned objects for a deployment with 5 MD Core instances running 8 AV engines each. |
| Network access | Required port is open (default port: **5432**).  A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |

### [Install PostgreSQL](/docs/mdcluster/installation/md-cluster-postgresql-windows#install-postgresql)

1. Go to [Download PostgreSQL](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads) page.
2. Choose and download the Windows x86-64 version.
3. Once the download is complete, run the installer.
4. When prompted, keep the **default installation directory**.
5. Choose the **default components** to install.
6. Set a password for the `postgres` user. Make sure to **save this password** for later use.

7. Select the port. Default is **5432**.

8. Choose the **default locale** for the new database cluster.
9. Complete the installation process.

### [Open connection](/docs/mdcluster/installation/md-cluster-postgresql-windows#open-connection)

1. Locate the PostgreSQL data directory on your server.

BashCopyC:\Program Files\PostgreSQL\<version>\data\

2. To allow remote connections, open the **postgresql.conf** file and configure the following setting:

postgresql.confCopylisten_addresses = '*'

3. To allow MetaDefender Cluster services to access the database, open the **pg_hba.conf** file and add the following rule.

pg_hba.confCopyhost all all 0.0.0.0/0 scram-sha-256

4. Restart the PostgreSQL service to apply the changes.
