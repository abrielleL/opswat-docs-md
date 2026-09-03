<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-migrate-metadefender-core-from-postgresql-local-to-postgr -->

# How to migrate MetaDefender Core from PostgreSQL local to PostgreSQL remote?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

Migrating MetaDefender Core from a local PostgreSQL database to a remote PostgreSQL setup is a critical task for organizations seeking enhanced scalability, performance, and security. This transition allows MetaDefender Core to leverage the robustness of remote database management while maintaining data integrity and ensuring smooth operational continuity. By decoupling the application from the local database, businesses can optimize their infrastructure, manage resources more effectively, and better support growing data demands. In this guide, we will explore the key steps and considerations for successfully migrating your MetaDefender Core environment to a remote PostgreSQL database.

Here are the steps:

- First, we should export the settings: if anything is wrong, we can still have a backup for local users and settings.

  - Goto UI, Settings → Export/Import → export the configuration to a zip file
- Export the whole database to a file:

  - We can use pgAdmin or `pg_dump` to export all the databases:

    - SharedDB: `metadefender_core` or Standalone: `metadefender_core_xxxx`
    - NOTE: **When backup we need to check this option so the exported DB will not have the restriction on privileges when importing back**

- **Example with pg_dump: --no-owner --no-privileges**

WindowsCopypg_dump.exe --file "d:\\opswat\\backup_db" --host "127.0.0.1" --port "5432" --username "postgres"
--format=c --blobs --no-owner --no-privileges --verbose "metadefender_core_q6es6e"LinuxCopypg_dump --file "/opswat/backup_db" --host "127.0.0.1" --port "5432" --username "postgres"
--format=c --blobs --no-owner --no-privileges --verbose "metadefender_core_q6es6e"

- Remove the current MetaDefender Core - Reinstall MetaDefender Core with the **same version** in the **same mode (standalone/shareddb)**→ This time we will config this MetaDefender Core to connect to **remote PG** - Stop MetaDefender Core - Delete current db of MD Core in remote server: `metadefender_core_xxx` / `metadefender_core` - Create a whole brand new db with the same name: `metadefender_core_xxx` / `metadefender_core` - Using pgadmin or `pg_restore` to restore the backup file into the remote PG

- Example with `pg_restore`:

WindowsCopypg_restore.exe --host "remote_pg_ip" --port "5432" --username "postgres"
--dbname "metadefender_core_q6es6e" --verbose "d:\\opswat\\backup_db"LinuxCopypg_restore --host "remote_pg_ip" --port "5432" --username "postgres"
--dbname "metadefender_core_q6es6e" --verbose "/opswat/backup_db"Support:

If you have followed all of the steps above but are still unable to **migrate MetaDefender Core from PostgreSQL local to PostgreSQL remote**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before logging a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
