<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore -->

# Backup & Restore for MetaDefender Endpoint

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Backup & Restore lets you back up configuration of every MetaDefender Endpoint. If a Endpoint is misconfigured or needs to be rolled back, you restore it to a known-good configuration from the same console.

- [Backup Workflows](/docs/cm/endpoint-security-solution/backup---restore#backup-workflows)

  - [Create Backup Job](/docs/cm/endpoint-security-solution/backup---restore#create-backup-job)
  - [Manage Backup Job](/docs/cm/endpoint-security-solution/backup---restore#manage-backup-job)
  - [Monitor Backup Progress and Results](/docs/cm/endpoint-security-solution/backup---restore#monitor-backup-progress-and-results)

- [Restore Workflows](/docs/cm/endpoint-security-solution/backup---restore#restore-workflows)

  - [Create Restore Job](/docs/cm/endpoint-security-solution/backup---restore#create-restore-job)
  - [Manage Restore Jobs](/docs/cm/endpoint-security-solution/backup---restore#manage-restore-jobs)
  - [Monitor Restore Progress and History](/docs/cm/endpoint-security-solution/backup---restore#monitor-restore-progress-and-history)
- [Dashboard](/docs/cm/endpoint-security-solution/backup---restore#backup--restore-dashboard)
- [Notifications](/docs/cm/endpoint-security-solution/backup---restore#notifications)
- [Reports](/docs/cm/endpoint-security-solution/backup---restore#reports)

## [Before You Begin](/docs/cm/endpoint-security-solution/backup---restore#before-you-begin)

Keep the following in mind:

| Requirement | Backup | Restore |
| --- | --- | --- |
| **License** | MA-BKR | MA-BKR |
| **Operating System** | Windows | Windows |
| **Supported Devices** | Windows devices running MetaDefender Endpoint **version 7.6.2607.xxx or later**. Non-Windows devices and devices on older versions are automatically excluded from any target you select. | Windows devices running MetaDefender Endpoint **version 7.6.2609 or later.** Non-Windows and older version devices are excluded. |
| **Encryption** | Encryption with passphrase requires MetaDefender Endpoint **version 7.6.2611 or later.** Encryption works for every backup scope: Files or Folders, Partitions and System Image. | |
| **Storage** | You need at least one reachable storage destination (for example a shared folder path such as `\\server\share`). An unreachable or misconfigured destination is rejected when you create the job. | At least one successful backup of the source device, taken on My OPSWAT Central Management 10.7.26092 or later. |

1. Devices that don't meet the OS or version requirement are excluded from the target list automatically.
2. Restore needs a newer device version than backup does. On the same fleet, the restore device picker can show fewer devices than the backup picker. If you can back up a device but can't restore it, check its MetaDefender Endpoint version first.
3. Every full backup stores a complete image, so make sure the destination has enough free space.

### [**Backup & Restore Job Status**](/docs/cm/endpoint-security-solution/backup---restore#backup--restore-job-status)

A job is in one of these states:

| Status | Meaning |
| --- | --- |
| **Scheduled** | The job is enabled and waiting for its next scheduled run |
| **In Progress** | A run is underway and devices are backing up |
| **Stopped** | The job has been stopped manually and will not run until you start it again |

A run is considered complete once every targeted device has reached a terminal result of Success, Failed, or Partial Success.

Note These are job-level states. The per-status counts on each job row (Pending, In Progress, Success, Failed, and so on) describe individual devices, not the job as a whole.

## [Backup Workflows](/docs/cm/endpoint-security-solution/backup---restore#backup-workflows)

You create backup jobs, choose which devices to protect, decide where the backups are stored, and set a schedule for them to run automatically. The system sends the commands to each device, tracks progress, and reports results directly in the console.

### [Create Backup Job](/docs/cm/endpoint-security-solution/backup---restore#create-backup-job)

Navigate to **Backup Restore → Backup → MetaDefender Endpoint tab → Create Backup Job**

| Step | Details |
| --- | --- |
| **Step 1: Enter a job name and description** | The job name must be unique within your account; a duplicate name will be rejected |
| **Step 2: Choose target devices to back up** | *Please note only Windows devices running MetaDefender Endpoint 7.6.2607.xxx or later can be backed up.*   1. All Groups applies to every device group 2. Specific Groups applies only to the groups you pick 3. Specific Devices applies only to the individual devices you select |
| **Step 3: Configure Backup Scope and Backup Mode** | 1. Backup Scope is currently fixed to **Full Image.** It captures all volumes needed to restore the operating system, including the system, boot, and recovery partitions; non-OS data volumes are excluded    2. Backup Mode: Select preferred backup mode     1. **Full**: captures all selected data on every run. Because every run stores a complete image, make sure your destination has enough free space    2. **Incremental**: the job's first run still captures a complete (full) image; every run after that captures only what changed since the previous backup, so it finishes faster and takes less space. A full backup plus the incremental backups that follow it form a **chain** |
| **Step 4: Configure Backup Destination** | Choose where backups are stored:   1. Mirror sends the backup to all destinations at the same time 2. Failover sends it to the primary destination and falls back to the others if that one is unavailable. 3. For each destination, pick a **Type** and enter the path     1. **Shared Folder**: enter the UNC path (for example `\\server\share`)    2. **Vault**: select a pre-configured Storage Vault to store backups in a managed, cataloged repository. To set one up first, see [Storage Vault Catalog](/docs/cm/endpoint-security-solution/backup---restore#storage-vault-catalog) 4. Use **Add Destination** to add more. An unreachable or misconfigured destination will be rejected |
| **Step 5: Encryption** | Encryption requires **MetaDefender Endpoint 7.6.2611 or later**.  Tick **Encrypt backups with a passphrase**, then type in passphrase and confirm (12 to 100 characters, including spaces).      Note Keep the passphrase safe. My OPSWAT Central Management never shows it again. If it is lost, the backups cannot be restored, you'll need to create a new job with new passphrase |
| **Step 6: Set up a schedule when backups run on target devices** | 1. **Frequency** can be Once, Hourly, Daily, Weekly, or Monthly; depending on the choice, the form asks for the matching details (for example days of the week for Weekly, or a day of the month for Monthly) 2. For **Timezone**, choose Local device time to run by each device’s own local time, or pick a specific timezone (such as UTC+7) so all devices run at the same moment. For a one-time schedule, the system rejects a start time that is already in the past 3. **Max Backup Duration** (optional) limits how many hours a backup may run on a device. If a device exceeds this window before finishing, that run is marked Failed. If you leave it empty, a default limit of about 24 hours applies |
| **Step 7: Complete** | Click **Create** to save the job, or **Discard** to cancel |

### [Storage Vault Catalog](/docs/cm/endpoint-security-solution/backup---restore#storage-vault-catalog)

Backup destinations are now managed centrally through a Storage Vault Catalog, eliminating the need to type connection details into each backup job individually.

To access the Vault Catalog, go to **Settings > Integrations > Vault Catalog** tab.

#### [**Add a new Vault**](/docs/cm/endpoint-security-solution/backup---restore#add-a-new-vault)

1. Click **Add Vault**
2. In the popup dialog, fill in the required fields
3. Click **Add** to save

Note Deleting a Vault **is not supported** in current phase. Vaults referenced by active jobs cannot be removed. To change connection details, create a new vault and update your job(s) to point to it.

#### [**Use a Vault in a Backup Job**](/docs/cm/endpoint-security-solution/backup---restore#use-a-vault-in-a-backup-job)

When you create or edit a backup job and add an SMB destination, select an existing vault from the dropdown instead of entering credentials manually.

### [Manage Backup Job](/docs/cm/endpoint-security-solution/backup---restore#manage-backup-job)

Click a job in the **Active Jobs** list to open its detail view, which shows its status, target, scope, mode, destination, schedule, and Max Backup Duration.

Use the **Action menu** at the top right to manage the job:

| Action | What it does |
| --- | --- |
| **Clone** | Duplicate the job's settings into a new job |
| **Stop** | Stop a running or pending job. Devices that are backing up receive a stop command and are marked as failed by force stop, while devices that have not yet started are removed from the queue. A stopped job can be started again with **Start**, which recalculates the next run time from the schedule |
| **Edit** | Change the job's settings, such as its schedule or targets. When you edit an encrypted job, the passphrase cannot be viewed or changed. |
| **Delete** | Remove the job. You cannot delete a job while it is running, so stop it first |

### [Monitor Backup Progress and Results](/docs/cm/endpoint-security-solution/backup---restore#monitor-backup-progress-and-results)

While a backup runs, each device reports a completion percentage. When it finishes, each device ends in one of these results:

- **Success**: the backup completed.
- **Partial Success**: the backup finished but with some issues.
- **Failed**: the backup didn't complete, ran past its Max Backup Duration, or was force-stopped.

For Encrypted job, you'll see an **Encrypted** tag next to the job name.

Results are summarized in **Active Jobs** and recorded in **History**. Every backup event is also written to the event log, so you can review each device's history: started, progress percentage, completed, failed, or completed with issues. Log entries expire according to your data retention policy.

#### [Download Backup Files](/docs/cm/endpoint-security-solution/backup---restore#download-backup-files)

You can download backed-up files directly from the console without navigating to the storage destination manually.

**Step 1: Download the backup files**

1. Open **File Browser** (or **History**)
2. Locate the completed backup entry
3. Open the action menu (**⋮**) and select **Download**
4. A dialog opens with a **script** you copy and run on the target Windows machine to pull the backup files down from the destination

**Step 2: Run the script**

- Run in Windows **Command Prompt** (`cmd.exe`), not PowerShell
- Run the script on any Windows machine that can reach the job's SMB destination(s) on your network
- The script prompts you for a username and password when it starts. No credentials are embedded in the script text

**What gets downloaded**

| Backup type you selected | Files downloaded |
| --- | --- |
| **Full** | Only that backup's files |
| **Incremental** | Downloads the full chain required to restore to that point, starting from the original full backup, through each increment, up to and including your selected one.  **Example:** In a chain Full → 1 → 2 → 3 → 4, selecting increment **2** downloads Full, 1, and 2 only. |

Please Note

- Files are copied into a new folder next to where you run the script
- If the job has multiple destinations (Mirror/Failover), the script tries them in order and automatically falls back to the next if one is unreachable
- Temporary network connections are disconnected when the script finishes
- Download is only available for backups that completed successfully

#### [**Browse Backup Contents**](/docs/cm/endpoint-security-solution/backup---restore#browse-backup-contents)

You can inspect the exact contents of a completed backup directly in My OPSWAT Central Management, no need to access the storage destination.

1. Open **File Browser** on a completed backup entry
2. The File Browse Tree starts at the top-level drives that were backed up (e.g., C:, D:, E:)
3. Click a drive to expand its folders and files
4. Continue drilling down the same way you would in a file explorer

| Behavior | Detail |
| --- | --- |
| **Progressive loading** | Only the current folder's contents load at a time |
| **Incremental backups** | The tree shows the complete captured contents up to that point in time, not just the files that changed in that run |
| **Retention limit** | Only the most recent backups per device retain a browsable tree. Older backups display a "tree not available" message |

## [Restore Workflows](/docs/cm/endpoint-security-solution/backup---restore#restore-workflows)

Restore a device to an earlier, known-good state, for example after a failed update, a ransomware incident, or a corrupted OS. A restore takes **one completed backup from one source device** and writes it to **one or more target devices**.

Two differences from backup affect most of the restore rules:

- **A restore runs once.** It has no frequency or recurring schedule.
- **A full image restore takes the device offline.** A machine can't overwrite the disk it's running from. The device reboots into a recovery environment, writes the disk, then reboots back into Windows. While this happens, the device can't be reached and doesn't report to the console.

### [Create Restore Job](/docs/cm/endpoint-security-solution/backup---restore#create-restore-job)

To restore an endpoint from a captured backup point, navigate to **Backup Restore > Restore** and click **Create Restore Job**.

| Configuration | Details |
| --- | --- |
| **General** | Enter a unique **Job Name** (duplicate names are rejected) and an optional **Description** |
| **Source & Restore Point** | Select the source device, then choose a restore point. Only devices with at least one successful backup are offered  How much is restored depends on the backup's mode:   - **Full Backup**: Restores the standalone system image - **Incremental Backup**: Automatically verifies and replays the chain from the baseline full image to the selected increment    - **Automatically restart the device:** Choose whether to restart the device automatically. This option appears only for full image restore points, and it's on by default. |
| **Backup Passphrase** | Type in the backup passphrase of that backup job |
| **Target Devices** | - Select one or more specific devices to write the backup onto. - Restore supports specific devices only. You can't target groups. - A target can be the source device itself or a different machine. |
| **Schedule** | Choose **Run immediately** or **Run on schedule** with designated date, time, and timezone     - **Max Restore Duration**: Set timeout limit (default: **48 hours**). Devices exceeding this window fail automatically. |

**Note Backups taken before version 10.7.26092 release can't be restored by a job.** A backup appears as a restore point only if it recorded its storage vault and its path inside that vault. Devices started recording both in this release. Older backups are still on your storage and aren't lost. Use [Download Backup Files](/docs/cm/endpoint-security-solution/backup---restore#download-backup-files) to retrieve them then restore them manually outside the console.

**Current Limitations**

Restoring to different hardware isn't supported. My OPSWAT Central Management doesn't check that an incremental chain is complete before you pick a restore point, and Max Restore Duration has no upper limit.

### [What Happens During a Restore](/docs/cm/endpoint-security-solution/backup---restore#what-happens-during-a-restore)

1. **The job starts and checks its targets.** Devices that have been removed, downgraded, or no longer have the agent since you created the job are skipped.
2. **Each device gets the restore command at its next check-in** and fetches the backup files it needs.

   1. A **full** restore point needs only its own files.
   2. An **incremental** restore point needs every backup in the chain, from the original full backup up to the point you selected. If any backup in that range can't be found (for example, its vault was removed from the catalog), the device rejects the whole restore **before copying anything**. This prevents an incomplete, unbootable disk.
3. **The device copies the backup locally** and reports progress.
4. **For a full image restore, the device reboots into recovery and writes the disk.** It's offline during this step.
5. **The device restarts and reports its result.**
6. **When every device has finished**, the run completes and the job moves to **Restore → History**.

Tip A device that goes quiet in the middle of a restore is usually still writing the disk offline. Wait until its Max Restore Duration runs out before you troubleshoot it.

### [Manage Restore Jobs](/docs/cm/endpoint-security-solution/backup---restore#manage-restore-jobs)

Open a restore job from the job list to manage it. Restore jobs support **Clone**, **Start, Stop, Edit**, and **Delete**.

| Action | What it does |
| --- | --- |
| **Stop** | Stops only the devices that haven't started yet. Those devices are marked **Failed**, with the reason that an administrator cancelled them. Devices that are **already restoring keep going**, because their disk is partway through being rewritten. Before you confirm, the dialog lists the devices that will be stopped      What happens after **Stop** depends on whether the job has run:   - **Never run:** the job stays in the list as **Stopped**. You can edit it and start it again - **Already running:** the job moves to History once its last active device finishes |
| **Start** | Re-enables a job that **has never run**. A job that has already run can't be started again. Re-running it could send a second restore to devices that are still rewriting their disks |
| **Edit** | Changes the job's settings. Available only when the job **has no run in progress**  For encrypted job, you can edit:   - Pick other encrypted restore point from the same device - Pick an encrypted point from another device - Pick an unencrypted point |
| **Delete** | Removes the job. Unlike backup jobs, you can delete a restore job in any state, without stopping it first |
| **Clone** | Duplicate the restore job's settings into a new job. Clone of an encrypted restore job asks for the passphrase again. |

### [Monitor Restore Progress and History](/docs/cm/endpoint-security-solution/backup---restore#monitor-restore-progress-and-history)

Track a restore from the **Ạctive Jobs** list while it runs.

**Statuses**

Each device ends as **Pending**, **In Progress** **Success**, or **Failed**.

- A restore has no **Partial Success**. Either the device was rebuilt or it wasn't.
- Devices that were stopped by an administrator, ran out of time, or failed on their own are all marked **Failed**. The **reason** on the row tells you which one happened.

#### [Restore History](/docs/cm/endpoint-security-solution/backup---restore#restore-history)

Go to **Backup Restore → Restore → History**. History lists every restore run in your account, newest first. You can filter by status and search by name. Each restore job runs once, so History shows one row per finished restore.

- Job status is **Pending**, **In Progress**, or **Completed**.
- A job stopped before any device started never produces a run. It stays in the job list as **Stopped** and doesn't appear in History.

#### [History Details](/docs/cm/endpoint-security-solution/backup---restore#history-details)

Select a run to open its record. History works as an **audit trail**: the header shows the job **as it was when the run started**, and later edits or deletion don't change it.

The header includes:

- Name, description, and creator
- Source device and the full restore point details: when the backup was taken, the backup job that created it, mode, scope, destination, size, and, for incremental backups, the chain and position in the chain
- Target devices, schedule, Max Restore Duration, and whether automatic restart was on

Below the header, a table lists each device with its group, agent version, final status, restore duration, and failure reason (if any). Use the status tabs, filter, or device search to narrow down large runs.

---

## [Dashboard](/docs/cm/endpoint-security-solution/backup---restore#dashboard)

Go to **Backup Restore → Dashboard** for real-time visibility into Endpoint backup and restore coverage across your fleet.

- **Filters:** Filter by **Endpoint Group** (evaluates current device membership) and **Timeframe** (24h, 7d, 30d, or Custom).

| Panel | Details |
| --- | --- |
| **Endpoint Backup Coverage** | Every eligible device falls into exactly one of three buckets:   - **Fully backed up**: latest backup succeeded or partially succeeded - **Missed a recent backup**: previous backup exists, but the latest attempt failed or timed out. - **Never completed a backup**: Device lacks a recorded baseline backup.   Note Devices that aren't targeted by any active backup job are **left out** rather than counted as unprotected. If you stop the only job covering a group, that group's devices drop off the panel instead of turning red. To find devices with no backup job, use the Report. |
| **Endpoint Backup Coverage Trend** | The same three buckets over the last 14 days, one point per day. A flat line is normal for weekly backups. Days with no data appear as gaps, not zeros. |
| **Backup Statuses** | Backup runs in the timeframe: **Succeeded**, **Partial Success**, **Pending**, **Running**, **Failed**, and **Timeout** (the device never picked up the run before its window closed) |
| **Restore Statuses** | Restore runs in the timeframe: **Succeeded**, **Pending**, **Running**, and **Failed**. Timed-out and stopped restores count as Failed. |
| **Top Backup Failure Reasons** | The failure reasons devices reported, most common first. If every row shows zero, there were no classified failures in the timeframe |
| **Needs Attention** | The 10 most recent problems. The **Backup** tab lists failed and timed-out backup runs, and the **Restore** tab lists failed restore runs. There's one row per run, so a device that failed twice appears twice. |

## [Notifications](/docs/cm/endpoint-security-solution/backup---restore#notifications)

Configure automated notifications across In-app and Email channels under **Backup & Restore > Notifications** > Click **Add** button.

| Setting | Options |
| --- | --- |
| **Event Types** | Backup completed, Backup failed, Restore completed, Restore failed |
| **Channel** | - **In-app**: appears under the notification bell in the console for every administrator in the account. It has no recipient list. - **Email**: sent to 1–100 addresses you enter. Recipients don't need to be console users. |
| **Execution Rules** | - Maximum of **8 rules** per account (1 In-app + 1 Email per event) - You can disable a rule without deleting it. It keeps its settings but stops sending notifications. - Notifications generate **per device** (e.g., 50 devices = 50 notifications) - In-app notifications appear immediately. Emails queues processes **10 emails every 5 minutes**   Tip Use **In-app** for success events and **Email** for failure events. An Email rule on **Backup completed** for a large fleet sends one email per device for every run. |

Note If hostname privacy is turned on for your account, device names show as `<private>` here and everywhere else in the console.

## [Reports](/docs/cm/endpoint-security-solution/backup---restore#reports)

A **report** is a saved configuration: what to report on, the time period, which groups, how often, and who receives it. Each time it runs, it creates a **report run** that you can view in the console, export as PDF or CSV, and email as a download link.

There are two report types: **Backup Summary Report** and **Failed and Overdue Agents**.

### [Create a Report](/docs/cm/endpoint-security-solution/backup---restore#create-a-report)

Navigate to **Backup & Restore > Reports >** Select **Create Report** to start.

| Configuration |  |
| --- | --- |
| 1. Choose a **Report Type** and enter a **Report Name** | Up to 100 characters, unique within your account |
| 2. Choose a **Generating Schedule** | Every schedule runs at a fixed time, with no day or time to set:   - One time: Once at the next 00:00 UTC, then it turns itself off - Daily: Every day at 00:00 UTC - Weekly: Every Monday at 00:00 UTC - Monthly: The 1st of every month at 00:00 UTC |
| 3. Choose a **Time Frame** | Last 24 hours, Last 7 days, Last 30 days, or Custom Range |
| 4. Choose the **Groups** to include. | Leave this empty to include all groups |
| 5. (Optional) Turn on **Share report by email** | Enter:   - **Recipients**: one or more email addresses, separated by commas (required) - **Email Content**: a message of up to 1,000 characters. A default message is filled in, and you can replace it - **Full Report Format**: **PDF** or **CSV** |
| 6. Preview and Save | **Preview** shows the layout of the report before you save it; **Back to Form** returns you to the settings.      Note Preview uses sample data. Use it to judge layout, not your own numbers. |

**What Recipients Receive?**

Each recipient gets an email carrying your Email Content and a download link valid for seven days from the moment the run completed.

Report download links in emails are **public**. Anyone with the link can download the report without signing in. Send reports only to trusted recipients, and treat the email as confidential. Reports carry a "Confidential — for internal use only" banner.

### [Manage Reports and Runs](/docs/cm/endpoint-security-solution/backup---restore#manage-reports-and-runs)

**Report history**

Click a report's name to open it:

- **Generated**: When the run completed, in your local time
- **Status**: Generating, Completed or Failed
- **Recipients**: Who that run was addressed to
- **Type**: Scheduled if the schedule produced it, Manual if someone clicked Generate Now

| Function | Meaning |
| --- | --- |
| **The ⋮ menu** | - **View Report**: Open it in the console - **Export as** PDF or CSV (CSV is always a .zip archive) - **Delete**: removes that run, its files and its download link; other runs and the configuration are untouched)   View and Export are only available on a **Completed** run |
| **Generate Now** | If **Share report by email** is turned on, clicking **Generate Now** will still email the full recipient list with a download link, even if the schedule is disabled. |
| **Edit** | Changes the report settings |
| **Turn a schedule on or off** | The schedule toggle only controls recurring automated generation; it does NOT suppress email sharing when manually triggering reports |

**Report Limits and Retention**

- **Tables are capped at 1,000 rows.** Larger tables show "Showing the first 1000 rows. This table was truncated." Export as CSV to get the full data.
- **Only the 20 most recent runs of each report are kept.** That's about three weeks of history for a daily report, or almost two years for a monthly one. Older runs are removed along with their files and links, so export anything you need to keep.

## [Important Notes](/docs/cm/endpoint-security-solution/backup---restore#important-notes)

A few things to keep in mind:

- The feature requires the MA-BKR license (SKU MA-BKR).
- Any credentials used to reach a storage destination are always stored encrypted, so passwords are never exposed.
- Each device has an execution time limit; if a backup runs too long (around 24 hours by default when no custom Max Backup Duration is set), it is marked as Failed.
- Encrypted passphrase is stored until all endpoints finish or time out, or the restore job is stopped or deleted. If a job is stopped during an active restore, the passphrase is retained until all ongoing restores finish; to restart a job stopped before execution, edit the job and re-enter the passphrase.
- The backup feature is available only on Windows devices running MetaDefender Endpoint version **7.6.2607.xxx or later**. Restore requires **7.6.2609.xxx or later**. Backup with encrypted passphrase requires **version 7.6.2611** or later.
