<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-is-unable-to-connect-to-the-database -->

# Why is MetaDefender Core unable to connect to the database?

### [Issue](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-is-unable-to-connect-to-the-database#issue)

MetaDefender Core fails to connect to the database. The following is displayed when connecting to the MetaDefender Core web console:

The following error is displayed in the core.log:

Error

“[ERROR] <timestamp>:(core.postgres) Postgres issue, error=’Could not load postgres’s information from file', param-'config file is invalid, ....”

### [Cause](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-is-unable-to-connect-to-the-database#cause)

The `ometascan_postegres.cat` and `ometascan_postgres.dat` files have become corrupted.

### [Remediation Steps](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-is-unable-to-connect-to-the-database#remediation-steps)

1. Stop the MetaDefender Core Service
2. Backup the corrupted Files

Backup the corrupted *ometascan_postgres.dat* and *ometascan_postgres.cat* files to a different location for future reference.

- Windows: The files are located in the Core’s installation folder.
- Linux: The files are located at:

FIle ListCopy/usr/lib/ometascan/ometascan_postgres.cat
/usr/lib/ometascan/ometascan_postgres.dat

3. Remove the Corrupted Files *ometascan_postgres.dat* and *ometascan_postgres.cat* files.

Delete the corrupted *ometascan_postgres.dat* and *ometascan_postgres.cat* files.

- Windows: Navigate to the Core’s installation folder and delete the files.
- Linux: Run the following commands:

shellCopysudo rm /usr/lib/ometascan/ometascan_postgres.cat
sudo rm /usr/lib/ometascan/ometascan_postgres.dat

4. Create the Ignition File

Create an ignition file with the specified content.

- Windows: Create `C:\opswat\ometascan.conf`
- Linux: Create `/etc/opswat/ometascan.conf`

Note:

If you are restoring an existing database, you will need to provide the username and password credentials used previously. Please consult your internal change management documentation to get these credentials.

Add the following content to the file:

[dbserver]
type=your db type, 'local' for bundle postgres, 'remote' for remote postgres.
host=ip address of remote postgres. For bundle postgres, it has to be localhost.
port=port of postgres.
user=postgres's user.
password=postgres's password.

**Example of an ignition file using bundled postgres:**

[dbserver]
type=local
host=localhost
port=5432
user=mypostgresuser
password=mypostgrespassword

Customers who specified an instance name during initial Core installation will need to enter the correct value for instance_name in the ignition file. If not, Core will initiate a new database with the default instance name.

**Example:**

Ignition FileCopy[dbserver]
type=local
host=localhost
port=5432
user=mypostgresuser
password=mypostgrespassword
instance_name=myinstancename

If customers have configured a private user for their database and want to reuse this private user, they need to ensure that correct private_username and private_password are set in the ignition file.

**Example:**

Ignition FileCopy[dbserver]
type=local
host=localhost
port=5432
user=mypostgresuser
password=mypostgrespassword
private_username=myprivateusername
private_password=myprivatepassword

5. Re-generate `ometascan_postgres.cat` and `ometascan_postgres.dat`

**Windows**

1. Open Command Prompt as Administrator
2. Navigate to the MetaDefender Core’s installation folder.
3. Run the following command:

CMDCopyometascan-upgrade-db.exe

**Linux**

Export:

BashCopyLD_LIBRARY_PATH=/usr/lib/ometascan:$LD_LIBRARY_PATH

Run the upgrade database tool using:

BashCopysudo /usr/sbin/ometascan-upgrade-db

Change the owner and set permissions for the newly generated ometascan_postgres.cat and ometascan_postgres.dat files:

BashCopysudo chown metascan:metascan /usr/lib/ometascan/ometascan_postgres.cat
sudo chown metascan:metascan /usr/lib/ometascan/ometascan_postgres.dat
sudo chmod 777 /usr/lib/ometascan/ometascan_postgres.cat
sudo chmod 777 /usr/lib/ometascan/ometascan_postgres.dat

6. Start MetaDefender Core Service

### [Conclusion](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-is-unable-to-connect-to-the-database#conclusion)

Following these steps should resolve the issue of MetaDefender Core failing to connect to the database due to configuration files corruption. If the problems persist, please contact OPSWAT support for further assistance.
