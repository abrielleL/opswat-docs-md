<!-- source: https://www.opswat.com/docs/mdemail/installation/migration -->

# Migration

## [From MetaDefender Email Gateway Security v5](/docs/mdemail/installation/migration#from-metadefender-email-gateway-security-v5)

Moving to PostgreSQL database

Email Gateway Security v6 is moving to use PostgreSQL database, allowing support for a high-availability setup. Its database can be separated from the product and stored on any PostgreSQL server, even in a cluster.

Migrating the databases from version 5 to version 6 is supported with an external migration tool provided during installation. It should be executed in a controlled fashion by the *system administrators*, therefore data migration is not part of the product installation process.

### [Preparation for the migration](/docs/mdemail/installation/migration#preparation-for-the-migration)

1. Upgrade Email Gateway Security to version 5.7.7. Release 5.7.7 is the only officially supported version 5 release at the moment from where a system can be migrated and upgraded to version 6.
2. Take a backup (optional but recommended). Stop the product and make a backup of the `data` folder (default `C:\Program Files\OPSWAT\MetaDefender Email Security\data`) by copying it to ensure the recoverability and integrity of the data. This backup could be used as a source of migration to separate it even more from a running product.
3. Upgrade Email Gateway Security to version 6.1.0 (or newer) by running the installer. During the installation you will setup the PostgreSQL database. It can be either installed and hosted by the product or hosted externally. When the application is started it will create the database schema we need to migrate data into. For details see [Installation](/docs/mdemail/installation/installation).

   1. After that, the Email Gateway Security service can be stopped (recommended) or running, but the database service must be running. (Windows service name: `OPSWAT MetaDefender Email Gateway Security Database Server`).
4. Stop processing emails (optional but recommended). Stop traffic towards Email Gateway Security or wait for low traffic hours so migration does not impact real-time email traffic.

   1. Disable any admin or user reports because they can cause inaccurate reports and multiple emails reported during migration. Check the report functionality configurations under **Settings > Quarantine reports** menu, **Settings > Alerts & Reports > Quarantine Reports** section and main **Reporting** menu.

### [Starting the migration process](/docs/mdemail/installation/migration#starting-the-migration-process)

The installation folder (default `C:\Program Files\OPSWAT\MetaDefender Email Security`) contains the migration tool (`EmailGatewaySecurity.Migration.exe`).

Open a new terminal in the installation folder as an administrator. The migration tool needs administrator privileges to read the email related files within the installation folder. Only administrators can access them, if it's installed in under "Program Files".

Help function

The application has a help function with:

**.\EmailGatewaySecurity.Migration.exe -?**

which prints out the available arguments.

By default no arguments are needed to be specified, the tool will read the configuration from the product settings. If the data was in a backup folder, you could specify a different data folder by ***--dataPath*** argument:

`.\EmailGatewaySecurity.Migration.exe --dataPath "<Path to backup>"`

The backup has three required components which have to be accessed: the ***email database*** (`mdemailsecurity.db.sqlite`), the ***config database*** (`config.db.sqlite`) and the ***queue storage*** (`/data/queuestore` folder).

When the application is started, it will request for the database password. It will be cleared off from the terminal, only use it for database connection and will not be stored anywhere.

The migration is split into separate distinct sections such as Emails, Report history, and statistics. These sections are executed sequentially in a batch of 50 items at a time. In one batch all items and every dependent item will be transferred to the database.

Debug info

Migration tool has an argument `--debug` which will enable more detailed logging. It can be enabled, if a support personnel asks for it:

`.\EmailGatewaySecurity.Migration.exe --dataPath "<Path to backup>" --debug True`

### [Cancel and resume a migration](/docs/mdemail/installation/migration#cancel-and-resume-a-migration)

Once the migration is running you should be able to see an update about its progress every second, and you should be able to cancel it by pressing `CTRL + C`. Once the migration is cancelled, it will finish the current transaction and stop at a safe commit point. Next time, when the migration is executed it can continue from where it left off.

### [Resuming normal operations](/docs/mdemail/installation/migration#resuming-normal-operations)

If any changes were made like disabling traffic or reports, those can be reset after the migration is completed.

Migration logs

The migration tool will create a log file per run next to the executable in a folder named `Logs`. By default, an `info` level log will be written there containing details of errors if something can not be migrated.

The log level can be set to `debug` with the `--debug` command line switch of the tool. Debug logging allows a bit more trace-like log to observe the behaviour of the migration process.

## [From MetaDefender Email Gateway Security v4](/docs/mdemail/installation/migration#from-metadefender-email-gateway-security-v4)

Invalid licenses

The Email Gateway Security v5 can be activated using a v4 license.

For details about editions see [Installation/Licensing](/docs/mdemail/installation/licensing).

Activation required

The v5 license must always be activated on the instance before Email Gateway Security v5 can start processing emails. For details see [Installation/Licensing](/docs/mdemail/installation/licensing).

To migrate from Email Gateway Security v4 to v5, simply run the installer of Email Gateway Security v5 and perform an upgrade.

Automatic upgrade

All configuration and databases will be migrated automatically to Email Gateway Security v5.

## [Moving from one server to an other server](/docs/mdemail/installation/migration#moving-from-one-server-to-an-other-server)

Prerequisites

1. The [Web Management Console and Public Rescan Page](/docs/mdemail/configuration/transport-layer-security#web-management-console-and-public-rescan-page) service connections must be downgraded to plain text from TLS for the migration on the source system.
2. The destination server must be a clean installation, installed with the same Email Gateway Security product version as the source server. The [Wizard](/docs/mdemail/installation/wizard) does not need to be completed on the destination server.
3. MetaDefender Core, MetaDefender MFT, SMTP and Active Directory [services](/docs/mdemail/configuration/server-profiles) must be accessible through the same network path (IP, FQDN, port, etc.) and protocol (HTTP, SMTP, LDAP, etc.) on the destination server as on the source.
4. Certificate and private key files must be accessible on the same file system path on the destination server as on the source.
5. Certificates must be installed in the Trusted Store in the destination operating system the same way as on the source operating system.
6. Log files files must be accessible on the same file system path on the destination server as on the source.

To move the Email Gateway Security deployment from one server to an other server, follow these steps:

1. On the source Email Gateway Security server

   1. Remove the server from production to not receive any further emails.
   2. Wait until all emails in *Pending*, *Processing* or *Reprocessing* status complete processing and end up in either *Sent*, *Blocked* or *Failed* status.
   3. Export the configuration:

      1. Export the current configuration with **Settings > General** */ Configuration / Export configuration;*
      2. Also export the *Computer\HKEY_LOCAL___MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security* Registry key;
      3. Back up the *<installation directory>\data* folder (default *C:\Program Files\OPSWAT\MetaDefender Email Security\data*) .
2. On the destination Email Gateway Security server

   1. Stop the Email Gateway Security service.

      1. Overwrite the *<installation directory>\data* folder (default *C:\Program Files\OPSWAT\MetaDefender Email Security\data*) with the one backed up on the source server in step *1.c.iii*.
      2. Import the Registry backup taken on the source server in the step *1.c.ii*.
   2. Start the Email Gateway Security service.

      1. Activate the Email Gateway Security deployment.
      2. Import the configuration backup taken on the source server in the step *1.c.i*.
   3. Check Email Gateway Security and verify if Server Profiles, Security Rules, Email History and Quarantine look good.
3. Upgrade the [Web Management Console and Public Rescan Page](/docs/mdemail/configuration/transport-layer-security#web-management-console-and-public-rescan-page) service connections to use TLS.
