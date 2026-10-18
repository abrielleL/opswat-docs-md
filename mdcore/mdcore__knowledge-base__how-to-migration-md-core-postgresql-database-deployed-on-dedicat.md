<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat -->

# How to migration MD Core postgresql database deployed on dedicated PostgreSQL server?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MD Core releases deployed on Windows and Linux systems. This guide walks you through migrating your MetaDefender Core PostgreSQL database to a new server.

## [**Prerequisites**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#prerequisites)

- Set up a new PostgreSQL server that is network-reachable by all MD Core servers.

## [**Migration Steps**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#migration-steps)

### [**Step 1: Stop MD Core Services**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#step-1-stop-md-core-services)

Stop all MD Core instances that are connected to the shared MD Core database.

### [**Step 2: Back Up the Existing Database**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#step-2-back-up-the-existing-database)

On the **original** PostgreSQL server, back up the metadefender_core database:

*pg_dump.exe --file "C:\Core_DB_backup\metadefender_core.backup" --host "127.0.0.1" --port "5432" --username "postgres" --format=c --blobs --no-owner --no-privileges --verbose "metadefender_core"*

**Note:** Adjust --host, --port, and --username if your setup differs from the defaults shown above.

### [**Step 3: Create the New Database**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#step-3-create-the-new-database)

On the **new** PostgreSQL server, create an empty database using the **same name** as the original (metadefender_core).

### [**Step 4: Restore the Backup**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#step-4-restore-the-backup)

Restore the backup file onto the newly created database:

*pg_restore --host "127.0.0.1" --port "5432" --username "postgres" --dbname "metadefender_core" --verbose "C:\Core_Db_backup\metadefender_core.backup"*

**Note:** Adjust --host, --port, and --username if your setup differs from the defaults shown above.

### [**Step 5: Update MD Core Configuration**](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#step-5-update-md-core-configuration)

Point MD Core to the new PostgreSQL server by running(default path):

*C:\Program Files\OPSWAT\MetaDefender Core\ometascan-change-db-credentials.exe*

Follow the prompts to enter the new server's connection details.

## [Actions required after migration](/docs/mdcore/knowledge-base/how-to-migration-md-core-postgresql-database-deployed-on-dedicat#actions-required-after-migration)

Once configuration is updated:

1. **Start** your MD Core service.

2. **Login to MD Core UI**

3. **Verify** connectivity to the new database: “Settings” option à “Network” Tab à “Database” section

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
