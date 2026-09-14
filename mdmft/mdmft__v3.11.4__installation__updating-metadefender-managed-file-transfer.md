<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer -->

# Backup MetaDefender Managed File Transfer

Summarize Page    Connect to Cursor Connect to VS Code
## [Backup](/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer#backup)

Ensure that you backup each system on similar schedule, to ensure they remain consistent with each other.

### [Backup operating system (OS)](/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer#backup-operating-system-os)

Create a backup of the computer where MetaDefender Managed File Transfer™ is installed, depending on your scenario.

| **Scenario** | **Action** | **Validation** |
| --- | --- | --- |
| **Virtual Machine (VM)** | Create a snapshot using the HW hypervisor (e.g., VMWare) | 1. Create a new VM using the snapshot 2. Restore the snapshot into a new VM without Network Interface Card (NIC) |
| **On-Premises (On-Prem)** | Use software (SW) to back up the full OS | Test restoration on different hardware without network connection |

### [Backup Databases (DB)](/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer#backup-databases-db)

Create a backup of both MetaDefender Managed File Transfer™ databases, depending on your scenario.

Warning

Ensure that the chosen database backup method supports consistent backup of the database while it is in use, and supports the database server type.

| **Scenario** | **Action** | Validation |
| --- | --- | --- |
| **Local Database (DB)** | Include database backup along with the OS backup | Database can be restored as part of the OS backup process |
| **Remote Database (DB)** | Back up databases using appropriate methods (e.g., SQL Server Backup) | Restore databases into the test DBs following [Microsoft documentation](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/quickstart-backup-restore-database?view=sql-server-ver16&tabs=ssms) |

### [Backup User Uploaded Files (Optional)](/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer#backup-user-uploaded-files-optional)

Info

Storing MetaDefender Managed File Transfer user uploaded files in a separate storage drive or remote storage is optional. Consider the additional storage requirements and time constraints associated with the data transfer process.

| **Scenario** | **Action** | Validation |
| --- | --- | --- |
| **Local Folder** | Save the uploaded files onto a separate storage drive or remote storage, or as part of the OS backup | Restore files to disk and verify they are downloadable. |
| **Remote Storage** | Backup the storage on a similar schedule as the database | Restore files to disk and verify they are downloadable. |
