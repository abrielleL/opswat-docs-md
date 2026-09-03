<!-- source: https://www.opswat.com/docs/mdicap/installation/untitled -->

# Automate Deployment

Both Linux and Windows can use ignition file to add PostgreSQL server information since MD ICAP Server 5.2.0 , refer to [Deployment automation support](/docs/mdicap/installation/deployment-automation-supporthhj) page

Make sure to create the ignition file before you start the installation, if it doesn't exists before, the server will go ahead and install MetaDefender ICAP Server with default values. (more details about [Ignition file](/docs/mdicap/installation/deployment-automation-supporthhj#ignition-file) at [Deployment automation support](/docs/mdicap/installation/deployment-automation-supporthhj))

- **Windows:**`C:\OPSWAT\mdicapsrv.conf`
- **Linux:**`/etc/opswat/mdicapsrv.conf`

#### [2.2.1.Setup Local (Bundle) PostgreSQL server](/docs/mdicap/installation/untitled#221setup-local-bundle-postgresql-server)

- MetaDefender ICAP Server will install a new PostgreSQL server locally, next to the product.

  - A sample iginition file for PostgreSQL server information (***Only non-Unicode characters supported for "user" and "password"***** _ _**** _**** __ _**** _**** __ _**** ***** *** _ __ )_:

**+ Standalone mode**

mdicapsrv.confCopy[global]
dbmode=1
[dbserver]
type=local
host=localhost
port=5433
user=postgres
password=non_Unicode_password

**+ Shared mode**

Info

Specific the instance_name in ignition file (the instance_name must be **unique)**

if instance_name does not exist in mdicapsrv.conf then default instance name with 6 characters extracted from that MetaDefender ICAP deployment ID.

mdicapsrv.confCopy[global]
dbmode=4
instance_name=mdicapsrv_test_1
[dbserver]
type=local
host=localhost
port=5433
user=postgres
password=non_Unicode_password
#### [2.2.2.Remote (Existing) PostgreSQL server](/docs/mdicap/installation/untitled#222remote-existing-postgresql-server)

Warning

**PostgreSQL version 12.14** **is required.**

MetaDefender ICAP Server will connect to a pre-installed PostgreSQL server running remotely and will setup its database.

Make sure to follow steps at Open Connection On PostgreSQL Server first, so that your remote existing PostgreSQL server to accept upcoming connection from MetaDefender ICAP Server .

A sample ignition file for PostgreSQL server information:

**+ Standalone mode**

mdicapsrv.confCopy[global]
dbmode=1
[dbserver]
type=remote
host=192.168.86.32
port=5433
user=existingserver_admin_user
password=existing_server_pass

**+ Shared mode**

Info

Specific the instance_name in ignition file (the instance_name must be **unique)**

if instance_name does not exist in mdicapsrv.conf then default instance name with 6 characters extracted from that MetaDefender ICAP deployment ID.

mdicapsrv.confCopy[global]
dbmode=4
instance_name=mdicapsrv_test_1
[dbserver]
type=remote
host=192.168.86.32
port=5433
user=existingserver_admin_user
password=existing_server_pass

After installing MetaDefender ICAP Server successfully, you may want to remove all credentials info created for [dbserver] section in ignition file for security reason.
