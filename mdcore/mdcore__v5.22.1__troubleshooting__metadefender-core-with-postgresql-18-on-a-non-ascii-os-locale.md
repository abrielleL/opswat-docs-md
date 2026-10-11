<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale -->

# Upgrade to MetaDefender Core 5.21.0 or later on Windows systems with a non-ASCII locale

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check your MetaDefender Core version and Operating System**

This guide applies to MetaDefender Core on **Windows**, when **upgrading** to version **5.21.0 or later**.

## [**Summary**](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#summary)

Starting with MetaDefender Core 5.21.0, the product bundles **PostgreSQL 18**. PostgreSQL 18 cannot initialize its database cluster if the Windows system locale name contains non-ASCII characters. For example, Turkish Windows uses the locale `Turkish_Türkiye.1254`, which contains `ü`.

**Check if your system is affected**

Before upgrading, open PowerShell and run:

Get-WinSystemLocale

If the returned locale name contains non-ASCII characters, your system is affected and you must follow the procedure below.

If the locale name contains only ASCII characters, no action is required — upgrade as usual.

**Alternative: upgrade without preserving processing history**

If your system is affected but you do not need to retain your processing history, you can use the following simpler procedure instead of the database backup and restore steps.

1. [Export current configuration.](https://www.opswat.com/docs/mdcore/operating/import-export-configuration#export)
2. Fresh install new MetaDefender Core v5.21.0 or latest version
3. [Import back the configuration](https://www.opswat.com/docs/mdcore/operating/import-export-configuration#import) to new installed MetaDefender Core.
## [**How to upgrade safely**](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#how-to-upgrade-safely)

Follow these steps in order. Your scan history, license, and settings will be preserved at the end.

### [**Step 1 — Back up your data from current installed Core**](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#step-1--back-up-your-data-from-current-installed-core)

1. Open **Command Prompt as Administrator**.
2. Change to the PostgreSQL binary directory of the current installation: `<Installation Folder>\postgres\bin` . Example:

   cd "C:\Program Files\OPSWAT\MetaDefender Core\postgres\bin"
3. Export the database:

   pg_dumpall.exe -h <pg_host> -p <pg_port> -U <pg_user> -f <backup_location>\Core_backup.sql
   1. Example: `pg_dumpall -h localhost -p 5432 -U postgres -f C:\OPSWAT\Core_backup.sql`
4. If you are prompted for a password, enter the password configured for the bundled PostgreSQL instance.
5. Confirm that `Core_backup.sql` was created and is not empty.

### [Step 2 — Edit the backup file](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#step-2--edit-the-backup-file)

1. Open `Core_backup.sql` in a text editor.
2. Remove **every occurrence** of the keyword `UNLOGGED`. This prevents errors when the dump is restored into the new database.
3. Save the file.

**Example:**

- **Before** (what's in the dump file):

  CREATE UNLOGGED TABLE cached_scan.schema_version (
  version smallint,
  instance_id smallint
  )
  PARTITION BY LIST (instance_id);
- **After** (what it should look like):

  CREATE TABLE cached_scan.schema_version (
  version smallint,
  instance_id smallint
  )
  PARTITION BY LIST (instance_id);

### [Step 3 — Uninstall current MetaDefender Core](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#step-3--uninstall-current-metadefender-core)

Uninstall the current MetaDefender Core.

### [Step 4 — Install new MetaDefender Core version](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#step-4--install-new-metadefender-core-version)

Run the Core installer. Once installation completes, do not activate or configure anything yet.

### [Step 5 — **Restore your data**](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#step-5--restore-your-data)

1. Stop the **MetaDefender Core** service.
2. Following this [guideline](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-backup-and-restore-standalone-database-for-metadefender-c#how-to) to manually start the bundled PostgreSQL service.
3. Open **Command Prompt** as Administrator and change to the PostgreSQL binary directory:

cd "C:\Program Files\OPSWAT\MetaDefender Core\postgres\bin"

3. List all databases to find the MetaDefender Core database name:

psql.exe -h localhost -p 5435 -U postgres -c "\l"

Look for the database whose name begins with `metadefender_core_` — for example, `metadefender_core_h21nqf`. Note this name; you need it in the following steps.

4. Drop the existing database:

psql.exe -h localhost -p 5435 -U postgres -c "DROP DATABASE \"metadefender_core_h21nqf\";"

5. Create an empty database with the same name:

psql.exe -h localhost -p 5435 -U postgres -c "CREATE DATABASE \"metadefender_core_h21nqf\";"

6. Restore the backup into the new database:

psql.exe -h localhost -p 5435 -U postgres -d metadefender_core_h21nqf -f "C:\OPSWAT\Core_backup.sql"

Depending on the size of the dump, the restore may take several minutes.

7. Start the **MetaDefender Core** service.

> **Note:** Replace `metadefender_core_h21nqf` in the commands above with the actual database name you identified in step 3. The suffix is generated per installation and differs on every system.

### [Step 6 **— Verify**](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#step-6---verify)

Open the MetaDefender Core web management console and confirm the following:

- **Processing History** shows your previous scan records.
- **Settings** retain your previous configuration.
- Your license is still active.

---

### [**Need help?**](/docs/mdcore/v5.22.1/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale#need-help)

If you encounter errors during the restore step or MetaDefender Core does not start after the upgrade, contact [OPSWAT Support](https://www.opswat.com/support) for help.
