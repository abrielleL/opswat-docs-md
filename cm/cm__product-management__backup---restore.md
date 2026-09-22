<!-- source: https://www.opswat.com/docs/cm/product-management/backup---restore -->

# Backup & Restore

Backup & Restore is a feature in My OPSWAT Central Management that lets you automatically back up the full system image of Windows endpoints across your organization.

You create backup jobs, choose which devices to protect, decide where the backups are stored, and set a schedule for them to run automatically. The system sends the commands to each device, tracks progress, and reports results directly in the console.

> This feature is available only through on-demand configuration. Please contact [OPSWAT Support](https://www.opswat.com/support/contact-support) for assistance.

> Restore is not available in the current release. This guide covers the backup workflow only. Restore will be supported in a future version.

You open the feature from the left-hand menu under **Endpoint Security** **→ Backup Restore**.

- [Main Screen](https://www.opswat.com/docs/cm/product-management/backup---restore#main-screen)
- [Create Backup Job](https://www.opswat.com/docs/cm/product-management/backup---restore#create-backup-job)
  - [Storage Vault Catalog](https://www.opswat.com/docs/cm/product-management/backup---restore#storage-vault-catalog)
- [Manage Backup Job](https://www.opswat.com/docs/cm/product-management/backup---restore#manage-backup-job)
- [Monitor Progress and Results](https://www.opswat.com/docs/cm/product-management/backup---restore#monitor-progress-and-results)
  - [Download Backup Files](https://www.opswat.com/docs/cm/product-management/backup---restore#download-backup-files)
  - [Browse Backup Contents](https://www.opswat.com/docs/cm/product-management/backup---restore#browse-backup-contents)

## Before You Begin

Keep the following in mind before creating a backup job:

1. This feature requires the **MA-BKR license** (SKU MA-BKR). It is not available unless your account is licensed for MA-BKR.
2. Backup is available on **Windows devices running** **MetaDefender Endpoint version 7.6.2607.xxx and later**. Non-Windows devices and devices on older versions are automatically excluded from any target you select.
3. You need at least one reachable storage destination (for example a shared folder path such as \\\\server\\share). An unreachable or misconfigured destination is rejected when you create the job.
4. Each run stores a complete image (see Backup scope and mode below), so make sure the destination has enough free space.

## **Main Screens**

![](https://uploads.developerhub.io/prod/97qW/l70eo2sfebw3hr91as4onp1fjrbr398t9l4dnux3ko6um1tu0erl3zoz90cm68fc.png)

The Backup Restore has **three sub-pages**:

| Sub-pages | Details |
| ---- | ---- |
| **Backup** | Two tabs: 1. **Active Jobs** lists every backup job that is currently set up, with its status, target, schedule, and a per-status device count. This gives you a quick view of how the latest run is going across all targeted devices ![](https://uploads.developerhub.io/prod/97qW/h7jh3ggpfow41y3zpyvy0cw7wqiug198wdp8pkxf3euyiz6xrd7jcao0w2e7ad60.png) When a job finishes a run, it moves automatically to the **History **tab. If the job is recurring (Hourly, Daily, Weekly, or Monthly), a new active job is created automatically to handle the next scheduled run 2. **History **tab records each completed run with its start and end time and the number of devices that ended in each status. Use it to audit past backups and confirm whether they succeeded ![](https://uploads.developerhub.io/prod/97qW/ikib155i7ngml1e18eacnyr399w5naj0m1wl60727o2fu6l0wrcn58rj9gntylp7.png) |
| **Devices** | Lets you browse the backups that have been stored by device, as well as  the backup scope, destination, size, and the time of the last backup for each device ![](https://uploads.developerhub.io/prod/97qW/h74feo6yw54f922ddr5bo0ze907kbmh7is16zowa05bahfu5ewz4glndf73boorn.png) |
| **File Browser** |  Shows what has actually been stored by file, you can see the backup scope, destination, size, and the time of the last backup for each device ![](https://uploads.developerhub.io/prod/97qW/9timxoqrd1psocm287sd9ugkwdppl7aazpkfpff5lskpkifdep2aodv47lysptva.png) |

### **Job Status**

A job is in one of these states:

| Status | Meaning |
| ---- | ---- |
| **Scheduled** | The job is enabled and waiting for its next scheduled run |
| **In Progress** | A run is underway and devices are backing up |
| **Stopped** | The job has been stopped manually and will not run until you start it again |

A run is considered complete once every targeted device has reached a terminal result of Success, Failed, or Partial Success.

Note These are job-level states. The Pending / In Progress / Partial Success / Success / Failed counts shown on each job row describe individual devices, not the job as a whole.

## Create Backup Job

Navigate to** Endpoint Security →  Backup & Restore → Create Backup Job**

| Step | Details |
| ---- | ---- |
| **Step 1: Enter a job name and description** | The job name must be unique within your account; a duplicate name will be rejected ![](https://uploads.developerhub.io/prod/97qW/oln5xzzhkptvi7xgjhjsbilof15ph733bq9at11ganx69gdpjxl2jroywd878ale.png) |
| **Step 2: Choose target devices to back up** | *Please note only Windows devices running MetaDefender Endpoint 7.6.2607.xxx or later can be backed up.* 1. All Groups applies to every device group 2. Specific Groups applies only to the groups you pick 3. Specific Devices applies only to the individual devices you select ![](https://uploads.developerhub.io/prod/97qW/hasrupvajzobxrsex409s5eycd3opixk2lziyardul3tz9spoj5j46r04whqpy0t.png) |
| **Step 3: Configure Backup Scope and Backup Mode** | 1. Backup Scope is currently fixed to **Full Image.** It captures all volumes needed to restore the operating system, including the system, boot, and recovery partitions; non-OS data volumes are excluded ![](https://uploads.developerhub.io/prod/97qW/d5hlpif3aksxyz0ach2d8melmupqlvsmqbq15c8q3zgzvk3104disq8bcv1rvxjy.png) 2. Backup Mode: Select preferred backup mode    1. **Full**: captures all selected data on every run. Because every run stores a complete image, make sure your destination has enough free space    2. **Incremental**: the job's first run still captures a complete (full) image; every run after that captures only what changed since the previous backup, so it finishes faster and takes less space. A full backup plus the incremental backups that follow it form a **chain** ![](https://uploads.developerhub.io/prod/97qW/pznldy8wnluwitpccpfygii1keqvj09dpr7q0wrzr2lywpztc4z0i2wjweggwtim.png) |
| **Step 4: Configure Backup Destination** | Choose where backups are stored: 1. Mirror sends the backup to all destinations at the same time 2. Failover sends it to the primary destination and falls back to the others if that one is unavailable. 3. For each destination, pick a **Type **and enter the path    1. **Shared Folder**: enter the UNC path (for example `\\server\share`)    2. **Vault**: select a pre-configured Storage Vault to store backups in a managed, cataloged repository. To set one up first, see [Storage Vault Catalog](https://www.opswat.com/docs/cm/product-management/backup---restore#storage-vault-catalog) 4. Use **Add Destination** to add more. An unreachable or misconfigured destination will be rejected ![](https://uploads.developerhub.io/prod/97qW/nedd3z0pll12temeibihi60zq0t7ny9xqoj3ik7qm736kcwt2m9r957jp2j1f033.png) |
| **Step 5: Set up a schedule when backups run on target devices** | 1. **Frequency** can be Once, Hourly, Daily, Weekly, or Monthly; depending on the choice, the form asks for the matching details (for example days of the week for Weekly, or a day of the month for Monthly) 2. For **Timezone**, choose Local device time to run by each device’s own local time, or pick a specific timezone (such as UTC+7) so all devices run at the same moment. For a one-time schedule, the system rejects a start time that is already in the past 3. **Max Backup Duration **(optional) limits how many hours a backup may run on a device. If a device exceeds this window before finishing, that run is marked Failed. If you leave it empty, a default limit of about 24 hours applies     ![](https://uploads.developerhub.io/prod/97qW/at4rczw0a6us2rr0xu833iphd4ii32nfg0g4xtogmf694i7gimlkmascuuoasicm.png) |
| **Step 6: Complete** | Click **Create **to save the job, or **Discard** to cancel |

### Storage Vault Catalog

Backup destinations are now managed centrally through a Storage Vault Catalog, eliminating the need to type connection details into each backup job individually.

To access the Vault Catalog, go to** Settings > Integrations > Vault Catalog** tab.

![](https://uploads.developerhub.io/prod/97qW/02k2awfumprf4b0awhiks2dsbf43niccggjn6irnpxuz7ublyjkmrkr375ofbyq7.png)

#### **Add a new Vault**

1. Click **Add Vault**
2. In the popup dialog, fill in the required fields
3. Click** Add **to save

![](https://uploads.developerhub.io/prod/97qW/bm2asak7vfzofakybl3t8m7d9f69ua3tihmert31x5ojjlh86k2r0y1h2lpyqwrf.png)

Note Deleting a Vault is not supported in current phase. Vaults referenced by active jobs cannot be removed. To change connection details, create a new vault and update your job(s) to point to it.

#### **Use a Vault in a Backup Job**

When you create or edit a backup job and add an SMB destination, select an existing vault from the dropdown instead of entering credentials manually.

![](https://uploads.developerhub.io/prod/97qW/n3rg10o4kfc0gew0stegismw3edbj8f0i6iti1vytho9qguyqahc96v7w60clhrs.png)

## Manage Backup Job

Click a job in the **Active Jobs** list to open its detail view, which shows its status, target, scope, mode, destination, schedule, and Max Backup Duration. Use the **Action menu **at the top right to manage the job:

![](https://uploads.developerhub.io/prod/97qW/f1k9rgmiucj8yek9b40wueom9yhvgztiz4db4akjv0k6awcu3wo11teik0efxsbh.png)

| Action | What it does |
| ---- | ---- |
| **Clone** | Duplicate the job's settings into a new job |
| **Stop** | Stop a running or pending job. Devices that are backing up receive a stop command and are marked as failed by force stop, while devices that have not yet started are removed from the queue. A stopped job can be started again with** Start**, which recalculates the next run time from the schedule |
| **Edit** | Change the job's settings, such as its schedule or targets |
| **Delete** | Remove the job. You cannot delete a job while it is running, so stop it first |

## Monitor Progress and Results

While a backup runs, each device reports its progress and you can watch the completion percentage rise. When a device finishes, it ends in one of these results: Success, Failed, or Partial Success (finished but with some issues).

![](https://uploads.developerhub.io/prod/97qW/9e5wvmsjiqdvnfqbo18mjc8938fw98frkz37o9l5wwg773wd85t95ovc88p82xlr.png)

These results are summarized on the** Active Jobs** list and recorded in the **History** tab. Every backup event is also written to the event log, so you can review a per-device history such as backup started, in progress with a percentage, completed, failed, or completed with some issues. Log entries expire automatically according to the data retention policy.

### Download Backup Files

You can now download backed-up files directly from the console without navigating to the storage destination manually.

**Step 1: Download the backup files**

1. Open **File Browser** (or **History**)
2. Locate the completed backup entry
3. Open the action menu (⋯) and select **Download**
4. A dialog opens with a **script** you copy and run on the target Windows machine to pull the backup files down from the destination

**Step 2: Run the script**

- Run in Windows **Command Prompt** (`cmd.exe`), not PowerShell
- Run the script on any Windows machine that can reach the job's SMB destination(s) on your network
- The script prompts you for a username and password when it starts. No credentials are embedded in the script text

![](https://uploads.developerhub.io/prod/97qW/0tjj4gvyg0rqv617z2shsm4nwfik9al2446yq3frr53glljlz10i0eonz8mfhl2k.png)

**What gets downloaded**

| Backup type you selected | Files downloaded |
| ---- | ---- |
| **Full** | Only that backup's files |
| **Incremental** | Downloads the full chain required to restore to that point, starting from the original full backup, through each increment, up to and including your selected one. > **Example:** In a chain Full → 1 → 2 → 3 → 4, selecting increment **2** downloads Full, 1, and 2 only. |

Please Note

- Files are copied into a new folder next to where you run the script
- If the job has multiple destinations (Mirror/Failover), the script tries them in order and automatically falls back to the next if one is unreachable
- Temporary network connections are disconnected when the script finishes
- Download is only available for backups that completed successfully

### **Browse Backup Contents**

You can inspect the exact contents of a completed backup directly in My OPSWAT Central Management, no need to access the storage destination.

1. Open **File Browser** on a completed backup entry
2. The File Browse Tree starts at the top-level drives that were backed up (e.g., C:, D:, E:)
3. Click a drive to expand its folders and files
4. Continue drilling down the same way you would in a file explorer

![](https://uploads.developerhub.io/prod/97qW/wcuctsmj18vsrvh9c5zcbh5jvg1ds71q2v88w7uoojwocug2wy28vsa7flz02f1z.png)

| Behavior | Detail |
| ---- | ---- |
| **Progressive loading** | Only the current folder's contents load at a time |
| **Incremental backups** | The tree shows the complete captured contents up to that point in time, not just the files that changed in that run |
| **Retention limit** | Only the most recent backups per device retain a browsable tree. Older backups display a "tree not available" message   |

## Important Notes

A few things to keep in mind:

- The feature requires the MA-BKR license (SKU MA-BKR).
- Any credentials used to reach a storage destination are always stored encrypted, so passwords are never exposed.
- Each device has an execution time limit; if a backup runs too long (around 24 hours by default when no custom Max Backup Duration is set), it is marked as Failed.
- The backup feature is available only on Windows devices running MetaDefender Endpoint version 7.6.2607.xxx or later.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
