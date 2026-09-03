<!-- source: https://www.opswat.com/docs/cm/configurations/backup-and-restore -->

# Backup and Restore

## Backup

Ensure that all systems are backed up on a synchronized schedule to keep them consistent with one another.

You can configure **automatic** backups or **manually** trigger a backup of your system data. These backups include system configuration and operational data.

![](https://uploads.developerhub.io/prod/97qW/kae1xulnsgmu13m0261z541sqmajofflpmyxechqhjhuxesgewx22w9x04lma790.png)

**Configure Scheduled Backup**

To configure a scheduled backup:

1. Go to **Settings > Servers > Backup**.
2. Check the option **"Enable scheduled backup"**.
3. Set the **Frequency** (e.g., Daily).
4. Choose the time that My OPSWAT Central Management triggers a backup (e.g., `08:00 UTC`).
5. Click **Save**.

When the backup schedule is triggered, My OPSWAT Central Management will backup its data and configuration and store inside its data folder.

> **Info**
>
> Backups are automatically retained for **30 days** before deletion.

**Trigger a Manual Backup**

Backups can also be triggered manually by administrators:

- Click the **backup icon** on the backup management screen.
- Confirm if prompted.

**Backup Information**

Each backup entry includes the following:

- **Status**: Indicates if the backup was successful (e.g., "Completed").
- **Creation time** and **Completion time**.
- **Created by**: The user who triggers the backup.
- **Action type**: "Manual" or "Scheduled".
- **Size**: File size of the backup (e.g., 34 MB).
- **Actions**: Download or delete the backup file.

## Restore the system from a Backup

You can restore My OPSWAT Central Management from a backup file during the Setup Wizard. Please note that the process may take time and could result in downtime while data is restored and services are restarted.

![](https://uploads.developerhub.io/prod/97qW/rhha4hzap2lugjishjzobcn4ibn8la0enbchk94lig83peue76t5grpax0sitznk.png)

**Step 1 - Select the Restore Option:** On the Setup wizard screen after you install My OPSWAT Central Management successfully, select **“Restore the Backup”**.

**Step 2 - Import a Backup File:**

1. Click **Choose File** to upload a `.CMX` backup file that you would like to restore from.
2. Click **Continue**.

**Step 3 - Review Information through the Setup Wizard**

- **Administrator User**: Confirm or create a new admin user.
- **Server Settings**: Review/update, if needed, server settings.
- **Summary**: Review the configuration before initializing the server.

> **Warning**
>
> Restoring from a backup will overwrite current system settings. Ensure the backup file is from a trusted and valid source.

**Best Practices**

- Schedule backups during low-traffic periods to reduce system load.
- Regularly download and store backup files externally for disaster recovery.
- Monitor backup status logs to ensure consistency and reliability.
