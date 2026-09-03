<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server- -->

# How to Migrate MetaDefender MFT to a New External SQL Server?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to MetaDefender Managed File Transfer 3.11.0 and later releases deployed on Windows systems.

> ## [Overview](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#overview)

This article provides a step-by-step guide on how to update your MetaDefender Managed File Transfer (MFT) configuration to point to a new, external SQL server. This is necessary when upgrading SQL hardware, migrating to a new SQL instance, or changing the SQL server's network name. This process assumes you have already replicated your MFT databases to the new server.

## [Prerequisites](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#prerequisites)

- **MFT Version:** This process uses the MFT installer and is designed for version 3.11.0 and later. If you are on an earlier version, please contact OPSWAT Support for version-specific guidance.
- **Server Snapshot:** It is highly recommended to take a full snapshot of the MFT application server's virtual machine before proceeding. This allows for a quick and complete restore in case of any unexpected issues.
- **Database Replication:** Before starting, verify that the databases on the new SQL server are exact, functional replicas of the ones from the old server.
- **Authentication Type:** This guide focuses on using SQL Server Authentication. Migrating an installation that uses Windows Authentication may require additional, more complex steps and is not covered in this document.
- **Encryption Key:** The `secret.bin` file is critical for decrypting your data — if it exists on your server. Locate and securely back up this file before proceeding. Note that installations that have been continuously updated since before version 3.3.1 without ever rotating the encryption key may not have a `secret.bin` file, as they continue to use a hardcoded encryption seed rather than a file-based one.

## [Steps to Configure](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#steps-to-configure)

The migration is performed in four phases:

1. Preparation on the old server.
2. Uninstalling MFT from the old server.
3. Database Restoration on the new SQL server.
4. Installing MFT on the new application server.

### [Phase 1: Preparation on the Old MFT Server](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#phase-1-preparation-on-the-old-mft-server)

Note:

If you are running MFT version 3.11.0 or later, configuration settings will be exported automatically during the uninstall process in Phase 2. The manual steps below remain recommended as an additional safeguard.

1. **Backup Entire Installation Directory:** Manually copy the entire MFT installation directory (e.g., `C:\Program Files\MetaDefender MFT`) to a safe backup location. This preserves all configuration files, scripts, and logs.
2. **Locate and Backup the Encryption Secret (**`secret.bin`**):**

   - The encryption key file, `secret.bin`, is critical for decrypting your data after the move. It is typically found in the `[InstallDir]\Services\` folder.
   - **Action:** Create a secure copy of this file and save it outside of the installation directory (e.g., on a network share or secure USB drive). You will need this file during the installation on the new server.
3. **Backup the Databases:** Using SQL Server Management Studio (SSMS) or your preferred tool, perform a full backup of both MFT databases. Keep these backup files in a secure location.

### [Phase 2: Uninstall MFT from the Old Server](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#phase-2-uninstall-mft-from-the-old-server)

1. Run the MFT uninstaller from the Windows Control Panel (Programs and Features).
2. **CRITICAL STEP:** When the uninstaller presents the database uninstall option, you must select Keep.

### [Phase 3: Database Restoration on the New SQL Server](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#phase-3-database-restoration-on-the-new-sql-server)

1. **Restore Databases:** On your new SQL server, use SSMS to restore the two database backups you created in Phase 1.
2. **Keep Database Names Identical:** When restoring, ensure the database names are exactly the same as they were on the old server (`sft_conn` and `sft_data`). MFT does not support changing database names; the names must match between source and target SQL Server.
3. **Set Database Owner:** For both restored databases, verify that the SQL login that MFT will use (e.g., `sa` or a dedicated service account) is set as the database owner (`dbo`). You can modify this in the database properties under the Files page.

### [Phase 4: Install MFT on the New Server](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#phase-4-install-mft-on-the-new-server)

1. **Run the Installer:** Execute the MFT installer on your application server machine (either the existing one or the new one, depending on your scenario).
2. **Select "Existing Database":** When you reach the database configuration screen, choose the option for using an "Existing database".
3. **Provide New SQL Server Details:**

   - Select SQL Server Authentication.
   - In the server field, enter the address of your new SQL server (e.g., `NewServerName\Instance`).
   - Enter the credentials for the SQL login that owns the databases.
   - The installer should automatically detect the existing databases on the new server.
4. **Configure Encryption:** If your installation uses a file-based encryption secret, the installer will prompt you to provide the `secret.bin` file. This file is used to decrypt the connection string and other sensitive data stored in the database. Provide the full path to the `secret.bin` file you backed up in Phase 1. The installer will not proceed if an incorrect file is specified, so ensure you are pointing to the correct backup.
5. **Accept Connection String Change (If Prompted):** Because the SQL server name has changed, the installer will detect a mismatch between the new server address and the connection string stored in the database, and will prompt you to update it. You must accept this change. This automatic update is the key feature that requires MFT version 3.11.0 or later.

## [Verify the Change: How to Check if MFT's Sensitive Data Encryption is Currently Using a File-Based Secret?](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#verify-the-change-how-to-check-if-mfts-sensitive-data-encryption-is-currently-using-a-file-based-secret)

To determine whether your MFT installation uses a file-based encryption secret (as opposed to the hardcoded default seed), check for the presence of the encryption key file on your current server.

Note:

This is unrelated to SQL Server-level database encryption. The encryption referred to here applies specifically to the connection string, file-related settings, and other sensitive data stored within the MFT database.

> Navigate to the following path on your MFT application server: `[MFT Install Directory]\Services\`

Look for a file named `secret.bin`.

- **If the file exists:** Your installation uses a file-based encryption secret. You will need this file for the migration to be successful. Ensure you back it up as described in Phase 1.
- **If the file does not exist:** Your installation is still using the hardcoded default encryption seed rather than a random file-based one. This does not mean encryption is absent — it means the encryption secret has not been rotated to a file. No `secret.bin` backup is required in this case.

During the installation on the new server (Phase 4, Step 4), the installer will verify whether a `secret.bin` file is required based on the state of the restored databases. If the databases reference a file-based secret, the installer will prompt you for it. If they use the default hardcoded seed, it will proceed without it.

## [Troubleshooting](/docs/mdmft/knowledge-base/how-to-migrate-metadefender-mft-to-a-new-external-sql-server-#troubleshooting)

If you encounter any issues during this process, please provide the following information to OPSWAT Support for further assistance:

- The specific error messages received.
- Your MFT version number.
- A description of the step where the failure occurred.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswwat.com/support).
