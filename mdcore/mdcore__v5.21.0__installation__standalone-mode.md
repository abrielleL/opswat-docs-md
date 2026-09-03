<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/installation/standalone-mode -->

# Standalone mode

## [Windows](/docs/mdcore/v5.21.0/installation/standalone-mode#windows)

### [Wizard Installation](/docs/mdcore/v5.21.0/installation/standalone-mode#wizard-installation)

**The Install Wizard is only for the Windows installer (.msi file).**

Since MetaDefender Core 4.19.0, we have switched to using PostgreSQL DBMS which needs a dedicated database server. MetaDefender Core supports two modes to setup PostgreSQL server:

#### [Local PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#local-postgresql-server)

This is a bundled PostgreSQL. MetaDefender Core will itself install and setup a new PostgreSQL server locally in the same box with the product.

PostgreSQL user credentials

Unicode characters are NOT supported for "Username" and "Password"

"Password" does not accept # (hash) as starting character (e.g. #ABC)

The ignition file

If the ignition file exist in the designated location, then MetaDefender Core will use the details defined in the ignition file, rather than what is passed via the installation wizard.

More info about the ignition file based installation: [Command Line Installation](/docs/mdcore/v5.21.0/installation/standalone-mode#command-line-installation)

#### [Remote PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#remote-postgresql-server)

Info

**PostgreSQL** **version 14/15/16** **is required.**

MetaDefender Core will connect to a pre-installed PostgreSQL running remotely.

"Test Connection" button is required, to make sure the PostgreSQL is connected and authenticated successfully. Make sure to check and perform steps at [Open Connection On PostgreSQL Server](/docs/mdcore/v5.21.0/troubleshooting/open-connection-on-postgresql-server) if you are unable to test the connection with remote PostgreSQL server.

PostgreSQL user privilege requirements

MetaDefender Core will need to create and use dedicated PostgreSQL users for database setup, upgrade and its own operations. Those users requires certain privileges configured on PostgreSQL server, otherwise expecting failures to occur while installing and operating MetaDefender Core.

Details: [PostgreSQL User Privilege Requirements](/docs/mdcore/v5.21.0/troubleshooting/postgresql-user-privilege-requirement)

### [Command Line Installation](/docs/mdcore/v5.21.0/installation/standalone-mode#command-line-installation)

#### [Ignition File](/docs/mdcore/v5.21.0/installation/standalone-mode#ignition-file)

Note

For command line installation, it is **mandatory** to use [MetaDefender Core ignition file](/docs/mdcore/v5.21.0/installation/deployment-automation-support) to add PostgreSQL server information **BEFORE** installing MetaDefender Core 4.19.0 or newer.

Location: **C:\OPSWAT\ometascan.conf**

MetaDefender Core supports two modes to setup PostgreSQL server:

#### [Local PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#local-postgresql-server)

MetaDefender Core will install a new PostgreSQL server locally, next to the product.

A sample iginition file for PostgreSQL server information. **Only non-Unicode characters are supported for "user" and "password"**):

ometascan.confCopy[dbserver]
type=local
host=localhost
port=5432
user=postgres
password=non_Unicode_password
#### [Remote PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#remote-postgresql-server)

Info

**PostgreSQL** **version 14/15/16** **is required.**

MetaDefender Core will connect to a pre-installed PostgreSQL server running remotely and will setup its database.

A sample ignition file for PostgreSQL server information:

ometascan.confCopy[dbserver]
type=remote
host=192.168.86.32
port=5432
user=existingserver_admin_user
password=existing_server_pass
### [How to setup a remote PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#how-to-setup-a-remote-postgresql-server)

1. Download and install PostgreSQL server version 14.x for Windows x64 at <https://www.enterprisedb.com/downloads/postgres-postgresql-downloads>
2. Configure PostgreSQL for remote access so that your remote existing PostgreSQL server to accept upcoming connection from MetaDefender Core:

2.1) Modify the **pg_hba.conf** file**:** file resides in the PostgreSQL data directory. Common locations include: **C:\Program Files\PostgreSQL\14\data**(adjust the version number if needed).

pg_hba.confCopyhost all all 0.0.0.0/0 scram-sha-256

2.2) Modify the **postgresql.conf** file. This file is in the same data directory as **pg_hba.conf**

postgresql.confCopylisten_addresses = '*'

3. Restart **postgres** service.

### [Install MetaDefender Core](/docs/mdcore/v5.21.0/installation/standalone-mode#install-metadefender-core)

On Windows systems, it is possible to install the product by executing the corresponding .msi file.

From the command line interface, it is also possible to put the following parameters

BashCopymsiexec /qn /i <msi file name> <option key>=<option value>

where the possible keys and their default values are the following:

| Key | Default Value | Description |
| --- | --- | --- |
| INSTALLFOLDER | \Program Files\OPSWAT\MetaDefender Core | Customize installation folder for product  Example: `INSTALLFOLDER="D:\Products"` |
| RESTADDRESS |  | REST interface binding IPv4 or IPv6 address ( '*' means that service listens on all IPv4 and IPv6 interfaces) |
| RESTPORT | 8008 | REST interface binding port |
| REPORT_ENGINE_ISSUE | true | Enable reporting of engine issue count. (possible values: "true" or "false"). |

Note

Reporting of engine issue count

If reporting of engine issue count is enabled, MetaDefender Core server will send only the **number** of initialization errors and **number** of unexpected stops for the specific db/engine version. This information is sent over a HTTPS channel when the product downloads the latest package descriptors. This information is used for early detection of any specific 3rd party engine quality issues.

For details on using msiexec, please consult [Windows installer documentation](https://technet.microsoft.com/en-us/library/cc782896%28v=ws.10%29.aspx).

## [Linux](/docs/mdcore/v5.21.0/installation/standalone-mode#linux)

**Only supports command-line installation.**

### [Ignition File](/docs/mdcore/v5.21.0/installation/standalone-mode#ignition-file)

Note

For command line installation, it is **mandatory** to use [MetaDefender Core ignition file](/docs/mdcore/v5.21.0/installation/deployment-automation-support) to add PostgreSQL server information **BEFORE** installing MetaDefender Core 4.19.0 or newer.

Location: **/etc/opswat/ometascan.conf**

MetaDefender Core supports two modes to setup a PostgreSQL server:

#### [Local PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#local-postgresql-server)

MetaDefender Core will install a new PostgreSQL server locally, next to the product.

A sample ignition file for PostgreSQL server information. **Only non-Unicode characters are supported for "user" and "password"**):

ometascan.confCopy[dbserver]
type=local
host=localhost
port=5432
user=postgres
password=non_Unicode_password
#### [Remote PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#remote-postgresql-server)

Info

**PostgreSQL** **version 14/15/16** **is required.**

MetaDefender Core will connect to a pre-installed PostgreSQL server running remotely and will setup its database.

A sample ignition file for PostgreSQL server information:

ometascan.confCopy[dbserver]
type=remote
host=192.168.86.32
port=5432
user=existingserver_admin_user
password=existing_server_pass
### [How to setup a remote PostgreSQL server](/docs/mdcore/v5.21.0/installation/standalone-mode#how-to-setup-a-remote-postgresql-server)

#### [Debian / Ubuntu](/docs/mdcore/v5.21.0/installation/standalone-mode#debian--ubuntu)

1. Update System Packages

BashCopysudo apt update
sudo apt upgrade -y

2. Add PostgreSQL APT Repository

BashCopysudo apt install -y wget ca-certificates
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo tee /etc/apt/trusted.gpg.d/pgdg.asc
echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -c | awk '{print $2}')-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list

3. Install PostgreSQL

BashCopysudo apt update
sudo apt install postgresql-14

4. Once installed, the PostgreSQL service should start automatically. You can verify that it is running:

BashCopysudo systemctl status postgresql

To start or restart the PostgreSQL service manually, you can run:

BashCopysudo systemctl start postgresql
sudo systemctl enable postgresql
sudo systemctl status postgresql

5. By default, the Postgres user is configured without a password. Run the following command to set a password for the Postgres user:

BashCopysudo -u postgres psql
postgres=# alter user postgres with password 'password';

6. Install needed extensions:

BashCopysudo -u postgres psql
postgres=# CREATE EXTENSION IF NOT EXISTS pg_trgm;
postgres=# CREATE EXTENSION IF NOT EXISTS btree_gin;

7. Configure PostgreSQL for remote access

BashCopysudo nano /etc/postgresql/14/main/postgresql.conf
# Change the following line with your server IP address:
listen_addresses = 'your-server-ip'
sudo nano /etc/postgresql/14/main/pg_hba.conf
# Change the following line
# Accept from anywhere
host all all 0.0.0.0/0 scram-sha-256
# Restart PostgreSQL service
sudo systemctl restart postgresql
#### [Red Hat Enterprise Linux 8, 9 / Rocky Linux 9](/docs/mdcore/v5.21.0/installation/standalone-mode#red-hat-enterprise-linux-8-9--rocky-linux-9)

Note

Due to the shorter support cycle on Red Hat Enterprise Linux, all supported versions of PostgreSQL are not available on this platform. The PostgreSQL Yum Repository will integrate with the normal systems and patch management, and provide automatic updates for all supported versions of PostgreSQL throughout the supported lifetime of PostgreSQL. Reference: <https://www.postgresql.org/download/linux/redhat/>

1. Install the PostgreSQL repository RPM:

BashCopysudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo dnf -qy module disable postgresql
sudo dnf install -y postgresql14-14.15 postgresql14-server-14.15

2. Run these CMDs to initialize the PostgreSQL:

BashCopysudo /usr/pgsql-14/bin/postgresql-14-setup initdb
sudo systemctl start postgresql-14
sudo systemctl enable postgresql-14
sudo systemctl status postgresql-14

3. By default, the Postgres user is configured without a password. Run the following command to set a password for the Postgres user:

BashCopysudo -u postgres psql
postgres=# alter user postgres with password 'password';

4. Install needed extensions:

BashCopysudo dnf install -y postgresql14-contrib
sudo -u postgres psql
postgres=# CREATE EXTENSION IF NOT EXISTS pg_trgm;
postgres=# CREATE EXTENSION IF NOT EXISTS btree_gin;

5. Configure PostgreSQL for remote access

BashCopysudo nano /var/lib/pgsql/14/data/postgresql.conf
# Change the following line with your server IP address:
listen_addresses = 'your-server-ip'
sudo nano /var/lib/pgsql/14/data/pg_hba.conf
# Change the following line
# Accept from anywhere
host all all 0.0.0.0/0 scram-sha-256
# Restart PostgreSQL service
sudo systemctl restart postgresql-14

**A sample ignition file for PostgreSQL server information:**

ometascan.confCopy[dbserver]
type=remote
host=192.168.86.32
port=5432
user=existingserver_admin_user
password=existing_server_pass

After installing MetaDefender Core successfully, you may want to remove all credentials info created for the [dbserver] section in the ignition file for security reasons.

Warning

If the MetaDefender Core package dependencies are not installed on your system, you may need to have a working Internet connection, or you may have to provide the Installation media during the installation. Consult your Operating System documentation on how to use Installation media as a package repository.

### [Install MetaDefender Core](/docs/mdcore/v5.21.0/installation/standalone-mode#install-metadefender-core)

#### [Debian / Ubuntu package (.deb)](/docs/mdcore/v5.21.0/installation/standalone-mode#debian--ubuntu-package-deb)

BashCopysudo dpkg -i <filename> || sudo apt-get install -f
#### [Red Hat Enterprise Linux 8, 9 package / Rocky Linux 9 package (.rpm)](/docs/mdcore/v5.21.0/installation/standalone-mode#red-hat-enterprise-linux-8-9-package--rocky-linux-9-package-rpm)

BashCopysudo dnf install -y <filename>
