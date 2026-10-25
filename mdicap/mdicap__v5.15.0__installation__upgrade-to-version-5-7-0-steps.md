<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps -->

# Upgrade to MetaDefender ICAP Server v5.7.0 or newer

View as Markdown Ask ChatGPT about this page Ask Claude about this page Warning

Please read this document carefully before upgrade. Metadefender ICAP Server v5.7.0 is supporting bundle PostgreSQL version v16.0x then:

- The ICAP Server instance which is using **local PostgreSQL database**:

  - ***With ICAP version older than v5.2.0, the SQLite database will be migrated to PostgreSQL database (the migration will take time)***
  - ***With ICAP version from v5.2.0 to v5.6.0: the local database will be migrated from PostgreSQL v12.x to v16.x (this will take time also)***
- The ICAP Server instance which is used remote database will not be impacted
## [Upgrade to v5.7.0 or newer from Metadefender ICAP server older than v5.2.0 (Sqlite database)](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#upgrade-to-v570-or-newer-from-metadefender-icap-server-older-than-v520-sqlite-database)

Metadefender ICAP Server which older than v5.2.0 is using SQLite database, then please follow the guide line [Upgrade to MetaDefender ICAP Server older than v5.2.0 (Sqlite) to version 5.2.0 -> v5.6.0 (PostgreSQL)](/docs/mdicap/v5.15.0/installation/upgrade-from-version-older-5-2-0)

Once upgraded to v5.6.0 get back to this page to do the upgrade to the latest MetaDefender ICAP Server version.

## [Upgrade to v5.7.0 or newer from Metadefender ICAP server version from v5.2.0 to v5.6.0 (PostgreSQL database)](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#upgrade-to-v570--or-newer-from-metadefender-icap-server-version-from-v520-to-v560-postgresql-database)

Please follow below steps to upgrade the Metadefender ICAP Server (including disaster recovery strategy)

### [Step 1: Check availability of free hard disk space](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-1-check-availability-of-free-hard-disk-space)

Warning

make sure the free space hard disk > 1.2 * size of pg_data folder

- Linux: /var/lib/mdicapsrv/pg_data
- Windows: C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data
### [Step 2: Stop mdicapsrv service](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-2-stop-mdicapsrv-service)

### [Step 3: Backup data](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-3-backup-data)

Backup **pg_data** folder

- Linux: backup folder /var/lib/mdicapsrv/pg_data
- Window: backup folder: <Installer-folder>\data\pg_data (default: `C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data)`

### [Step 4: Backup custom config for local PostgreSQL database](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-4-backup-custom-config-for-local-postgresql-database)

This step is required incase:

- Case 1: enable TLS for local PostgreSQL or
- Case 2: any tuning the Local PostgreSQL (such as: turning the max connection, work queue size, listening address, ....)

Linux: Back up all file in /usr/lib/mdicapsrv/postgres

Windows: back up all file in: <Installer-folder>/postgres (default: C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres)

### [Step 5: Upgrade to Metadefender ICAP server v5.7.0](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-5-upgrade-to-metadefender-icap-server-v570)

- CentOS:

BashCopysudo yum install <filename>

- Debian:

BashCopysudo dpkg -i <filename> || sudo apt-get install -f

- Windows: double click the msi to install

### [Step 6: Restore custom config](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-6-restore-custom-config)

This step is required if there is custom config of Step 4: Backup custom config for local PostgreSQL database

- Copy **pg_hba.conf** from backup **pg_data** folder at Step 3: Backup data to :

  - Linux: /var/lib/mdicapsrv/pg_data
  - Windows: C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data
- Copy all **config files** in postgres backup folder at Step 4: Backup custom config for local PostgreSQL database to:

  - Linux: /usr/lib/mdicapsrv/postgres
  - Windows: C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres
- Restart mdicapsrv service

### [Step 7: Recovery step if step 5 failed:](/docs/mdicap/v5.15.0/installation/upgrade-to-version-5-7-0-steps#step-7-recovery-step-if-step-5-failed)

This step will help recover to older MD ICAP server version incase upgrade to v5.7.0 failed (Step 5: Start install Metadefender ICAP server v5.7.0)

- Collect support package and send to OPSWAT to help us analyze (refer to: <https://www.opswat.com/docs/mdicap/troubleshooting/how-to-create-support-package>)
- Uninstall MD ICAP Server v5.7.0:

  - CentOS

BashCopysudo yum remove mdicapsrv

- Debian

BashCopysudo apt remove mdicapsrv

- Windows: uninstall the MD ICAP Server

- Delete below folders if exist

  - Linux:

    - /var/lib/mdicapsrv/pg_data
    - /usr/lib/mdicapsrv/postgres
    - /usr/lib/mdicapsrv/postgres-old
  - Windows:

    - C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data
    - C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres
    - C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres-old
- Rename pg_data-old to pg_data

  - Linux: rename /var/lib/mdicapsrv/pg_data-old to /var/lib/mdicapsrv/pg_data
  - Windows: rename **C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data-old** to **C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data**
- Install old MD ICAP Server from installation package
