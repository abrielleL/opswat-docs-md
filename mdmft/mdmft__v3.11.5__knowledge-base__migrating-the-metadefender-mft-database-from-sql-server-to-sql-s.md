<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s -->

# Migrating the MetaDefender MFT Database from SQL Server to SQL Server

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version:

This article applies to MFT version 3.8.0 to 3.11.0+ releases deployed on Windows.

Before proceeding with the database migration, please ensure that you back up the system or the VM where MD MFT is running.

For detailed backup instructions, refer to the official documentation: [MD MFT Backup Guide](https://www.opswat.com/docs/mdmft/installation/updating-metadefender-managed-file-transfer)

### [Prepare tools](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#prepare-tools)

#### [**SQL Server Management Studio**](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#sql-server-management-studio)

- **Purpose**: Required for easier execution of SQL operations.
- **Link**: [Install SQL Server Management Studio](https://learn.microsoft.com/en-us/ssms/download-sql-server-management-studio-ssms#download-ssms)
- **Where to install**: Any machine with access to both source and destination SQL Server

## [Limitations](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#limitations)

· SQL Authentication method must be unchanged. E.g. If using SQL authentication it must remain this way.

· Avoid special characters in the SQL login password if possible. It could be changed later as described in

· Destination SQL Server version and edition should be equal or higher than source.

### [1. Uninstall and Export Config](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#1-uninstall-and-export-config)

Uninstalling 3.11.0+:

- Uninstall MFT on the old server.
- When prompted, keep the existing databases.
- Export configuration files to a safe location outside the install directory (e.g., include secret.bin if present).

Uninstalling 3.8.0+ < 3.11.0

- Manually copy config files for backup purposes

  - Encryption secret

    - secret.bin: InstallDir\Services\secret.bin (may not exist if the first version installed was <3.3.1, and the encryption key never rotated)
  - Windows Service config files

    - Next service config: InstallDir\Services\appsettings.json
    - Caching service config: InstallDir\Services\cache.appsettings.json (3.9.2+)
    - Node manager service config: InstallDir\Services\node-manager.appsettings.json (3.10.2+)
    - Rest service config: InstallDir\Services\opswat.vault.rest.service.exe.config
    - Processor service config: InstallDir\Services\opswat.vault.processor.service.exe.config
    - Helper service config: InstallDir\Services\opswat.vault.helper.service.exe.config
    - Caching service config: InstallDir\Services\opswat.vault.caching.service.
  - Nginx configs

    - InstallDir\WebServer\nginx.conf
    - InstallDir\WebServer\conf\dynamic.conf
  - Localization files

    - InstallDir\WebClient\assets\i18n*.json
  - Config metadata

    - InstallDir\Services\config_meta_data.json
- Uninstall selecting “No” for Complete uninstallation: [Uninstalling MetaDefender Managed File Transfer - MetaDefender Managed File Transfer](https://www.opswat.com/docs/mdmft/v3.8.0/installation/uninstalling-metadefender-managed-file-transfer)

### [2. Backup Databases](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#2-backup-databases)

1. Connect to the SQL Server instance using the SQL Server Management Studio (SSMS):

2. Stop all the MD MFT services.
3. Backup both **sft_conn** and **sft_data** databases one by one

Right-click the **database name** and navigate to **Tasks > Back Up…**

Choose the destination directory and filename for the backup. Remove any other file from the list. Click **OK** to complete the process.

### [3. Restore on New Environment](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#3-restore-on-new-environment)

It's recommended to avoid special characters in the password during migration, as some characters may cause compatibility issues.

1. Copy both the `sft_conn` and `sft_data` backup files to the machine or VM where the remote MS SQL server is running.
2. Using the SQL Server Management Studio (SSMS),restore both databases from the backup files one by one:

Connect to the **remote SQL Server instance**

Right-click **Databases** and select **Restore Database…**

Choose Device, then locate and select the backup file.

Check Relocate all files to folder. Click on OK button

In such a case where the database user who restored the database is not the same one, additional steps needed:

- MFT database user should already exist in database instance
- After the restore, this user should be the owner for both `sft_conn` and `sft_data` databases
- Complete the mapping between the databases and the database user

### [4. Set Database Owner](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#4-set-database-owner)

- Assign the SQL login that MFT will use as the database owner (dbo) for both databases.

### [5. Install MFT on New Server](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#5-install-mft-on-new-server)

- Choose Existing database during setup (all MFT database versions supported that were last updated by a currently supported MFT version)
- Select SQL Server authentication.
- Provide the new SQL Server address and credentials.

### [6. Configure Encryption](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#6-configure-encryption)

- If available, provide secret.bin from the exported files during uninstallation to preserve encryption keys.
- The installer will verify if the provided secret.bin is correct or required at all

### [7. Accept Connection String Change](/docs/mdmft/v3.11.5/knowledge-base/migrating-the-metadefender-mft-database-from-sql-server-to-sql-s#7-accept-connection-string-change)

If the installer fail unexpectedly after the change. The change will not be rolled back in the database. Make sure to have a database backup before accepting this fix.

**Suggested follow-up**

For security reasons, it is **strongly recommended** to update database credentials and encryption keys after migration. This ensures that any sensitive information accessed during the process becomes invalid.

- **Update Database Credentials:** If you need to update the database username and password, use the SftDatabaseConfigurationTool.exe file. Refer to the [Database Configuration Tool](https://www.opswat.com/docs/mdmft/configuration/database-credentials-tool) documentation for detailed instructions.
- **Change the Encryption Key:** To generate a new encryption key, navigate to:
- *Settings → Security → Encryption** and create a new key. For more details, visit: [Encryption](https://www.opswat.com/docs/mdmft/configuration/encryption)

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
