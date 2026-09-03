<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-postgresql-linux -->

# Linux

Requires PostgreSQL version 16.9 or later.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-postgresql-linux#prerequisites)

Before installing the PostgreSQL service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Debian 12+, Ubuntu 22.04+, Ubuntu 24.04+, Rocky Linux 9+, or RHEL 9+ |
| Privileges | `root` or `sudo` privileges. |
| Hardware | Minimum 8 vCPU and 16 GB RAM. |
| Disk space | At least 1 TB of available storage on **SSD** or **NVMe** for optimal performance.  Approximately 4 GB of storage is required per 1 million scanned objects for a deployment with 5 MD Core instances running 8 AV engines each. |
| Network access | Required port is open (default port: **5432**).  A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |

## [Debian, Ubuntu](/docs/mdcluster/installation/md-cluster-postgresql-linux#debian-ubuntu)

### [Install PostgreSQL](/docs/mdcluster/installation/md-cluster-postgresql-linux#install-postgresql)

1. Add the official PostgreSQL repository.

BashCopysudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
# Automated get VERSION_CODENAME
source /etc/os-release
echo "Using VERSION_CODENAME: $VERSION_CODENAME"
# Add PostgreSQL software repository
sudo tee /etc/apt/sources.list.d/pgdg.sources <<EOF
Types: deb deb-src
URIs: https://apt.postgresql.org/pub/repos/apt
Suites: $(echo $VERSION_CODENAME)-pgdg
Architectures: amd64
Components: main
Signed-By: /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc
EOF
sudo apt update

2. Install PostgreSQL 16.

BashCopysudo apt install -y postgresql-16.10

3. Install additional supplied modules and extensions.

BashCopysudo apt install -y postgresql-contrib

4. Configures PostgreSQL to start automatically whenever the system boots.

BashCopysudo systemctl enable --now postgresql

5. Setup login password. Make sure to save this password for later use.

BashCopysudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD '<your_password>';"
### [Open connection](/docs/mdcluster/installation/md-cluster-postgresql-linux#open-connection)

1. Locate the PostgreSQL data directory on your server.

BashCopy/etc/postgresql/<version>/main/

2. To allow remote connections, open the **postgresql.conf** file and configure the following setting:

postgresql.confCopylisten_addresses = '*'

3. To allow MetaDefender Cluster services to access the database, open the `**pg_hba.conf**` file and add the following rule.

pg_hba.confCopyhost all all 0.0.0.0/0 scram-sha-256

4. Restart the PostgreSQL service to apply the changes.

BashCopysudo systemctl restart postgresql
## [Rocky, RHEL](/docs/mdcluster/installation/md-cluster-postgresql-linux#rocky-rhel)

### [Install PostgreSQL](/docs/mdcluster/installation/md-cluster-postgresql-linux#install-postgresql)

1. Copy, paste, and run the relevant parts of the setup script:

BashCopysudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo dnf install -y postgresql16-server
sudo /usr/pgsql-16/bin/postgresql-16-setup initdb
sudo systemctl enable postgresql-16
sudo systemctl start postgresql-16

2. Install additional supplied modules and extensions.

BashCopysudo dnf install -y postgresql16-contrib

3. Setup login password. Make sure to save this password for later use.

BashCopysudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD '<your_password>';"
### [Open connection](/docs/mdcluster/installation/md-cluster-postgresql-linux#open-connection)

1. Locate the PostgreSQL data directory on your server.

BashCopy/var/lib/pgsql/16/data

2. To allow remote connections, open the **postgresql.conf** file and configure the following setting:

postgresql.confCopylisten_addresses = '*'

3. To allow MetaDefender Cluster services to access the database, open the `**pg_hba.conf**` file and add the following rule.

pg_hba.confCopyhost all all 0.0.0.0/0 scram-sha-256

4. Restart the PostgreSQL service to apply the changes.

BashCopysudo systemctl restart postgresql-16
