<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/metadefender-icap-server-is-unable-to-connect-to-the-database -->

# Why is MetaDefender ICAP Server unable to connect to the database?

### [Issue](/docs/mdicap/knowledge-base/metadefender-icap-server-is-unable-to-connect-to-the-database#issue)

MetaDefender ICAP Server fails to connect to the database. The following is displayed when connecting to the MetaDefender ICAP Server web console:

The following error is displayed in the mdicapsrv.log:

Error

“[ERROR] <timestamp>:(icap.postgres) Postgres issue, error=’Could not load postgres’s information from file', param-'config file is invalid, ....”

### [Cause](/docs/mdicap/knowledge-base/metadefender-icap-server-is-unable-to-connect-to-the-database#cause)

The mdicapsrv_postgres.dat and mdicapsrv_postgres.cat files have become corrupted.

### [Remediation Steps](/docs/mdicap/knowledge-base/metadefender-icap-server-is-unable-to-connect-to-the-database#remediation-steps)

1. Stop the MetaDefender ICAP Server Service
2. Backup the corrupted Files

Backup the corrupted mdicapsrv_postgres.dat and mdicapsrv_postgres.cat files to a different location for future reference.

- Windows: The files are located in the ICAP Server’s installation folder.
- Linux: The files are located at:
- /usr/lib/mdicapsrv/mdicapsrv_postgres.cat /usr/lib/mdicapsrv/mdicapsrv_postgres.dat

3. Remove the corrupted files "mdicapsrv_postgres.dat" and "mdicapsrv_postgres.cat" files

- Windows: Navigate to the ICAP Server’s installation folder and delete the files.
- Linux: Run the following commands:

BashCopysudo rm /usr/lib/mdicapsrv/mdicapsrv_postgres.cat
sudo rm /usr/lib/mdicapsrv/mdicapsrv_postgres.dat

4. Create the Ignition File

Create an ignition file with the specified content.

- Windows: Create C:\opswat\mdicapsrv.conf
- Linux: Create /etc/opswat/mdicapsrv.conf

NOTE

If you are restoring an existing database, you will need to provide the username and password credentials used previously. Please consult your internal change management documentation to get these credentials.

Add the following to the file:

Ignition FileCopy[dbserver]
type=your db type, 'local' for bundle postgres, 'remote' for remote postgres.
host=ip address of remote postgres. For bundle postgres, it has to be localhost.
port=port of postgres.
user=postgres's user.
password=postgres's password.

**Example of an ignition file using bundled postgres:**

Ignition FileCopy[dbserver]
type=local
host=localhost
port=5432
user=mypostgresuser
password=mypostgrespassword

Customers who specified an instance name during ICAP Server installation need to enter the correct value instance_name in the ignition file. If not, ICAP Server will initiate a new database with the default instance name.

**Example:**

Ignition FileCopy[dbserver]
type=local
host=localhost
port=5432
user=mypostgresuser
password=mypostgrespassword
instance_name=myinstancename

If customers have configured a private user for their database and want to reuse this private user, they need to ensure that correct private_username and private_password are set in the ignition file.

**Example**

Ignition FileCopy[dbserver]
type=local
host=localhost
port=5432
user=mypostgresuser
password=mypostgrespassword
private_username=myprivateusername
private_password=myprivatepassword

5. Re-generate mdicapsrv_postgres.cat and mdicapsrv_postgres.dat

**Windows**

1. Open Command Prompt as Administrator
2. Navigate to the MetaDefender ICAP Server’s installation folder.
3. Run the following command:

CMDCopymdicapsrv-upgrade-db.exe

**Linux**

Export:

BashCopyLD_LIBRARY_PATH=/usr/lib/mdicapsrv:$LD_LIBRARY_PATH

Run the upgrade database tool using:

BashCopysudo /usr/sbin/mdicapsrv-upgrade-db

Change the owner and set permissions for the newly generated mdicapsrv_postgres.cat and mdicapsrv_postgres.dat files:

BashCopysudo chown metascan:metascan /usr/lib/mdicapsrv/mdicapsrv_postgres.cat
sudo chown metascan:metascan /usr/lib/mdicapsrv/mdicapsrv_postgres.dat
sudo chmod 777 /usr/lib/mdicapsrv/mdicapsrv_postgres.cat
sudo chmod 777 /usr/lib/mdicapsrv/mdicapsrv_postgres.dat

6. Start MetaDefender ICAP Server Service

### [Conclusion](/docs/mdicap/knowledge-base/metadefender-icap-server-is-unable-to-connect-to-the-database#conclusion)

Following these steps should resolve the issue of MetaDefender ICAP Server failing to connect to the database due to configuration files corruption. If the problems persist, please contact OPSWAT support for further assistance.
