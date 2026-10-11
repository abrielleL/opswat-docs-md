<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore -->

# Backup & Restore

Backup & Restore is a feature in My OPSWAT Central Management that lets you automatically back up the full system image of Windows endpoints across your organization. When a machine fails or needs to be rolled back, you can restore it to a known-good point in time from the same console.

You open the feature from the left-hand menu under **Backup Restore**.

> This feature is available only through on-demand configuration. Please contact [OPSWAT Support](https://www.opswat.com/support/contact-support) for assistance.

![](https://uploads.developerhub.io/prod/97qW/l4e6t610iq9g43os8fvxk1pzpq1im6jmxuvogupi6igd5hin85mzpu3ngtz341el.png)

- [Main Screens and Navigation](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#main-screen)
- [Backup Workflows](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#backup-workflows)
  - [Create Backup Job](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#create-backup-job)
  - [Manage Backup Job](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#manage-backup-job)
  - [Monitor Backup Progress and Results](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#monitor-backup-progress-and-results)

- [Restore Workflows](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#restore-workflows)
  - [Create Restore Job](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#create-restore-job)
  - [Manage Restore Jobs](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#manage-restore-jobs)
  - [Monitor Restore Progress and History](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#monitor-restore-progress-and-history)
- [Dashboard](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#backup--restore-dashboard)
- [Notifications](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#notifications)
- [Reports](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#reports)

## Before You Begin

Keep the following in mind before creating a backup job:

| Requirement | Backup | Restore |
| ---- | ---- | ---- |
| **License** | MA-BKR | MA-BKR |
| **Operating System** | Windows | Windows |
| **Supported Devices** | Windows devices running MetaDefender Endpoint **version 7.6.2607.xxx or later**. Non-Windows devices and devices on older versions are automatically excluded from any target you select. | Windows devices running MetaDefender Endpoint **version 7.6.2609 or later.** Non-Windows and older version devices are excluded. |
| **Storage** | You need at least one reachable storage destination (for example a shared folder path such as `\\server\share`). An unreachable or misconfigured destination is rejected when you create the job. | At least one successful backup of the source device, taken on  M OPSWAT Central Management 10.7.26092 or later. |

1. Devices that don't meet the OS or version requirement are excluded from the target list automatically.
2. Restore needs a newer device version than backup does. On the same fleet, the restore device picker can show fewer devices than the backup picker. If you can back up a device but can't restore it, check its MetaDefender Endpoint version first.
3. Every full backup stores a complete image, so make sure the destination has enough free space.

## **Main Screens and Navigation**

![](https://uploads.developerhub.io/prod/97qW/79i6o5c08111kb7kruej7b41y25fvfktuxt5cv1xetg8lx5labaxa7pbdiba8uj0.png)

Backup & Restore has the following **sub-pages:**

| Sub-pages | Details |
| ---- | ---- |
| **Dashboard** | See fleet-wide backup coverage, run statuses, top failure reasons, and the devices that need attention ![](https://uploads.developerhub.io/prod/97qW/438mv3nijeux9kk178xnyasfiv08nm5uf1j3supoi3s06jdqtfcse1rxogg11kro.png) |
| **Backup** | Create and manage backup jobs, including two tabs: 1. **Active Jobs** lists every backup job that is currently set up, with its status, target, schedule, and a per-status device count. This gives you a quick view of how the latest run is going across all targeted devices ![](https://uploads.developerhub.io/prod/97qW/h7jh3ggpfow41y3zpyvy0cw7wqiug198wdp8pkxf3euyiz6xrd7jcao0w2e7ad60.png) When a job finishes a run, it moves automatically to the **History **tab. If the job is recurring (Hourly, Daily, Weekly, or Monthly), a new active job is created automatically to handle the next scheduled run 2. **History **tab records each completed run with its start and end time and the number of devices that ended in each status. Use it to audit past backups and confirm whether they succeeded ![](https://uploads.developerhub.io/prod/97qW/ikib155i7ngml1e18eacnyr399w5naj0m1wl60727o2fu6l0wrcn58rj9gntylp7.png) |
| **Devices** | Lets you browse the backups that have been stored by device, as well as  the backup scope, destination, size, and the time of the last backup for each device ![](https://uploads.developerhub.io/prod/97qW/z2jmdl37zzlcc0izbn6biut5tan60rjhroyvh5vm0j8pljjbzs9draxikf8ksvlz.png) |
| **File Browser** |  Shows what has actually been stored by file, you can see the backup scope, destination, size, and the time of the last backup for each device ![](https://uploads.developerhub.io/prod/97qW/piul2fas0khrl2c3kn3zecxux3lhjcqpatpywsdmeb4p2pw5ojqghnzu6ecowy1c.png) |
| **Restore** | Create and manage restore jobs. The job list shows restores that are scheduled or in progress, and the **History** tab records finished restores. ![](https://uploads.developerhub.io/prod/97qW/io64hm9hh0kbfb0kfh7mytb1rojnmmdmfre91drx21wllb4nrgl0pum3bbmt1qql.png) |
| **Reports** | Automated and on-demand report definitions (PDF/CSV) with scheduled stakeholder email delivery ![](https://uploads.developerhub.io/prod/97qW/ijzexkz17kxpp2qp3ux1qtvgwd5bhef9gi1cfjfaj3bmgjudcakhj6bueohyyott.png) |
| **Notifications** | ![](https://uploads.developerhub.io/prod/97qW/8mmpeus45qgpscu5eyvcganow2t8n60pfvt7jr4nlgfr33347zio0hp96ibmx43s.png) |

### **Backup & Restore Job Status**

A job is in one of these states:

| Status | Meaning |
| ---- | ---- |
| **Scheduled** | The job is enabled and waiting for its next scheduled run |
| **In Progress** | A run is underway and devices are backing up |
| **Stopped** | The job has been stopped manually and will not run until you start it again |

A run is considered complete once every targeted device has reached a terminal result of Success, Failed, or Partial Success.

Note These are job-level states. The per-status counts on each job row (Pending, In Progress, Success, Failed, and so on) describe individual devices, not the job as a whole.

## Backup Workflows

You create backup jobs, choose which devices to protect, decide where the backups are stored, and set a schedule for them to run automatically. The system sends the commands to each device, tracks progress, and reports results directly in the console.

![](https://uploads.developerhub.io/prod/97qW/abbdkmh33x160dn1oa2xfvowvj3uwkx2y7mnzikch5621iduw9nt9os4hviwu6bv.png)

### Create Backup Job

Navigate to** Backup Restore → Backup → Create Backup Job**

| Step | Details |
| ---- | ---- |
| **Step 1: Enter a job name and description** | The job name must be unique within your account; a duplicate name will be rejected ![](https://uploads.developerhub.io/prod/97qW/oln5xzzhkptvi7xgjhjsbilof15ph733bq9at11ganx69gdpjxl2jroywd878ale.png) |
| **Step 2: Choose target devices to back up** | *Please note only Windows devices running MetaDefender Endpoint 7.6.2607.xxx or later can be backed up.* 1. All Groups applies to every device group 2. Specific Groups applies only to the groups you pick 3. Specific Devices applies only to the individual devices you select ![](https://uploads.developerhub.io/prod/97qW/hasrupvajzobxrsex409s5eycd3opixk2lziyardul3tz9spoj5j46r04whqpy0t.png) |
| **Step 3: Configure Backup Scope and Backup Mode** | 1. Backup Scope is currently fixed to **Full Image.** It captures all volumes needed to restore the operating system, including the system, boot, and recovery partitions; non-OS data volumes are excluded ![](https://uploads.developerhub.io/prod/97qW/d5hlpif3aksxyz0ach2d8melmupqlvsmqbq15c8q3zgzvk3104disq8bcv1rvxjy.png) 2. Backup Mode: Select preferred backup mode    1. **Full**: captures all selected data on every run. Because every run stores a complete image, make sure your destination has enough free space    2. **Incremental**: the job's first run still captures a complete (full) image; every run after that captures only what changed since the previous backup, so it finishes faster and takes less space. A full backup plus the incremental backups that follow it form a **chain** ![](https://uploads.developerhub.io/prod/97qW/pznldy8wnluwitpccpfygii1keqvj09dpr7q0wrzr2lywpztc4z0i2wjweggwtim.png) |
| **Step 4: Configure Backup Destination** | Choose where backups are stored: 1. Mirror sends the backup to all destinations at the same time 2. Failover sends it to the primary destination and falls back to the others if that one is unavailable. 3. For each destination, pick a **Type **and enter the path    1. **Shared Folder**: enter the UNC path (for example `\\server\share`)    2. **Vault**: select a pre-configured Storage Vault to store backups in a managed, cataloged repository. To set one up first, see [Storage Vault Catalog](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#storage-vault-catalog) 4. Use **Add Destination** to add more. An unreachable or misconfigured destination will be rejected ![](https://uploads.developerhub.io/prod/97qW/nedd3z0pll12temeibihi60zq0t7ny9xqoj3ik7qm736kcwt2m9r957jp2j1f033.png) |
| **Step 5: Set up a schedule when backups run on target devices** | 1. **Frequency** can be Once, Hourly, Daily, Weekly, or Monthly; depending on the choice, the form asks for the matching details (for example days of the week for Weekly, or a day of the month for Monthly) 2. For **Timezone**, choose Local device time to run by each device’s own local time, or pick a specific timezone (such as UTC+7) so all devices run at the same moment. For a one-time schedule, the system rejects a start time that is already in the past 3. **Max Backup Duration **(optional) limits how many hours a backup may run on a device. If a device exceeds this window before finishing, that run is marked Failed. If you leave it empty, a default limit of about 24 hours applies     ![](https://uploads.developerhub.io/prod/97qW/at4rczw0a6us2rr0xu833iphd4ii32nfg0g4xtogmf694i7gimlkmascuuoasicm.png) |
| **Step 6: Complete** | Click **Create **to save the job, or **Discard** to cancel |

### Storage Vault Catalog

Backup destinations are now managed centrally through a Storage Vault Catalog, eliminating the need to type connection details into each backup job individually.

To access the Vault Catalog, go to** Settings > Integrations > Vault Catalog** tab.

![](https://uploads.developerhub.io/prod/97qW/cmqbbxhy4srnse62apszlh3qoy2s1jpz70aw7z6hwvenpeyp6d7fkzfevgn6o4qn.png)

#### **Add a new Vault**

1. Click **Add Vault**
2. In the popup dialog, fill in the required fields
3. Click** Add **to save

![](https://uploads.developerhub.io/prod/97qW/bm2asak7vfzofakybl3t8m7d9f69ua3tihmert31x5ojjlh86k2r0y1h2lpyqwrf.png)

Note Deleting a Vault** is not supported **in current phase. Vaults referenced by active jobs cannot be removed. To change connection details, create a new vault and update your job(s) to point to it.

#### **Use a Vault in a Backup Job**

When you create or edit a backup job and add an SMB destination, select an existing vault from the dropdown instead of entering credentials manually.

![](https://uploads.developerhub.io/prod/97qW/n3rg10o4kfc0gew0stegismw3edbj8f0i6iti1vytho9qguyqahc96v7w60clhrs.png)

### Manage Backup Job

Click a job in the **Active Jobs** list to open its detail view, which shows its status, target, scope, mode, destination, schedule, and Max Backup Duration.

Use the **Action menu **at the top right to manage the job:

![](https://uploads.developerhub.io/prod/97qW/f1k9rgmiucj8yek9b40wueom9yhvgztiz4db4akjv0k6awcu3wo11teik0efxsbh.png)

| Action | What it does |
| ---- | ---- |
| **Clone** | Duplicate the job's settings into a new job |
| **Stop** | Stop a running or pending job. Devices that are backing up receive a stop command and are marked as failed by force stop, while devices that have not yet started are removed from the queue. A stopped job can be started again with** Start**, which recalculates the next run time from the schedule |
| **Edit** | Change the job's settings, such as its schedule or targets |
| **Delete** | Remove the job. You cannot delete a job while it is running, so stop it first |

### Monitor Backup Progress and Results

While a backup runs, each device reports a completion percentage. When it finishes, each device ends in one of these results:

- **Success**: the backup completed.
- **Partial Success**: the backup finished but with some issues.
- **Failed**: the backup didn't complete, ran past its Max Backup Duration, or was force-stopped.

![](https://uploads.developerhub.io/prod/97qW/9e5wvmsjiqdvnfqbo18mjc8938fw98frkz37o9l5wwg773wd85t95ovc88p82xlr.png)

Results are summarized in **Active Jobs** and recorded in **History**. Every backup event is also written to the event log, so you can review each device's history: started, progress percentage, completed, failed, or completed with issues. Log entries expire according to your data retention policy.

#### Download Backup Files

You can download backed-up files directly from the console without navigating to the storage destination manually.

**Step 1: Download the backup files**

1. Open **File Browser** (or **History**)
2. Locate the completed backup entry
3. Open the action menu (**⋮**) and select **Download**
4. A dialog opens with a **script** you copy and run on the target Windows machine to pull the backup files down from the destination

![](https://uploads.developerhub.io/prod/97qW/3iivfi2pvisppagytpaslzziou4vlcbai3n0qeflbbsmaz9ei5s8hcmmm2yauas8.png)

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

#### **Browse Backup Contents**

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

## Restore Workflows

Restore a device to an earlier, known-good state, for example after a failed update, a ransomware incident, or a corrupted OS. A restore takes **one completed backup from one source device** and writes it to **one or more target devices**.

![](https://uploads.developerhub.io/prod/97qW/me4961p86jvzy1xwms0w2zy6l1ngzi47y09ee13cyt4y9rm3bao520pwctr54m7x.png)

Two differences from backup affect most of the restore rules:

- **A restore runs once.** It has no frequency or recurring schedule.
- **A full image restore takes the device offline.** A machine can't overwrite the disk it's running from. The device reboots into a recovery environment, writes the disk, then reboots back into Windows. While this happens, the device can't be reached and doesn't report to the console.

### Create Restore Job

To restore an endpoint from a captured backup point, navigate to **Backup Restore > Restore** and click **Create Restore Job**.

![](https://uploads.developerhub.io/prod/97qW/63jbdn6hdqwal5z163ys2n8hnjjd78yoap6ic6encw8s1xuyz0i4rtomg3f5h6s6.png)

| Configuration | Details |
| ---- | ---- |
| **General** | Enter a unique **Job Name** (duplicate names are rejected) and an optional **Description** ![](https://uploads.developerhub.io/prod/97qW/looll2whgf20eqgxjt3011vivy9x12hlgvjxa4472sjip0mn1yqymx27rnlwe9bn.png) |
| **Source & Restore Point** | Select the source device, then choose a restore point. Only devices with at least one successful backup are offered How much is restored depends on the backup's mode: - **Full Backup**: Restores the standalone system image - **Incremental Backup**: Automatically verifies and replays the chain from the baseline full image to the selected increment ![](https://uploads.developerhub.io/prod/97qW/hlf0axr5ayyqfrb52mzo0xvps9l363jagjjvbmyrq7odckgoe7cc3fu2fefmbe5m.png) - **Automatically restart the device:** Choose whether to restart the device automatically. This option appears only for full image restore points, and it's on by default. |
| **Target Devices** | - Select one or more specific devices to write the backup onto.  - Restore supports specific devices only. You can't target groups. - A target can be the source device itself or a different machine. ![](https://uploads.developerhub.io/prod/97qW/bqsnf377bm4ejkp0pjf98yw1k1lo23hrj35kb658lpw3wwgbfvigkb1vlbgy9rfz.png) |
| **Schedule** | Choose **Run immediately** or **Run on schedule** with designated date, time, and timezone ![](https://uploads.developerhub.io/prod/97qW/en2eokaale8uzsvp8e7lzcc16uxvpdz97kixor2te0ue42ik3dr4yy4r8edhkrra.png) - **Max Restore Duration**: Set timeout limit (default: **48 hours**). Devices exceeding this window fail automatically. |

Note** Backups taken before version 10.7.26092 release can't be restored by a job.** A backup appears as a restore point only if it recorded its storage vault and its path inside that vault. Devices started recording both in this release. Older backups are still on your storage and aren't lost. Use [Download Backup Files](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore#download-backup-files) to retrieve them then restore them manually outside the console.

> **Current Limitations**
>
> Restoring to different hardware isn't supported. My OPSWAT Central Management doesn't check that an incremental chain is complete before you pick a restore point, and Max Restore Duration has no upper limit.

### What Happens During a Restore

![](https://uploads.developerhub.io/prod/97qW/jsbxokbmrkg25ejd9i6sm0njphhvykkwfpgp4qpsu0l5fw4fpiomzr5d83zvrc9g.png)

1. **The job starts and checks its targets.** Devices that have been removed, downgraded, or no longer have the agent since you created the job are skipped.
2. **Each device gets the restore command at its next check-in** and fetches the backup files it needs.
   1. A **full** restore point needs only its own files.
   2. An **incremental** restore point needs every backup in the chain, from the original full backup up to the point you selected. If any backup in that range can't be found (for example, its vault was removed from the catalog), the device rejects the whole restore **before copying anything**. This prevents an incomplete, unbootable disk.
3. **The device copies the backup locally** and reports progress.
4. **For a full image restore, the device reboots into recovery and writes the disk.** It's offline during this step.
5. **The device restarts and reports its result.**
6. **When every device has finished**, the run completes and the job moves to **Restore → History**.

Tip A device that goes quiet in the middle of a restore is usually still writing the disk offline. Wait until its Max Restore Duration runs out before you troubleshoot it.

### Manage Restore Jobs

Open a restore job from the job list to manage it. Restore jobs support **Clone**, **Start, Stop, Edit**, and **Delete**.

![](https://uploads.developerhub.io/prod/97qW/uywwzf6mvwt73nr6fz1cjstao43m6mls94m6bn0x3vjanaevvrj09patesv3hj5x.png)

| Action | What it does |
| ---- | ---- |
| **Stop** | Stops only the devices that haven't started yet. Those devices are marked **Failed**, with the reason that an administrator cancelled them. Devices that are **already restoring keep going**, because their disk is partway through being rewritten. Before you confirm, the dialog lists the devices that will be stopped ![](https://uploads.developerhub.io/prod/97qW/mpx6n62v8g3rcdxodsicdc3z54t5812fuem1hgau7j0gl4roxzvnxf06x6r2yvpk.png) What happens after **Stop** depends on whether the job has run: - **Never run:** the job stays in the list as **Stopped**. You can edit it and start it again - **Already running:** the job moves to History once its last active device finishes |
| **Start** | Re-enables a job that **has never run**. A job that has already run can't be started again. Re-running it could send a second restore to devices that are still rewriting their disks |
| **Edit** | Changes the job's settings. Available only when the job **has no run in progress** |
| **Delete** | Removes the job. Unlike backup jobs, you can delete a restore job in any state, without stopping it first |
| **Clone** | Duplicate the restore job's settings into a new job |

### Monitor Restore Progress and History

Track a restore from the **Ạctive Jobs** list while it runs.

![](https://uploads.developerhub.io/prod/97qW/jnae46pagdfeqx54v3l30enjdy37kivekbfuopox0rqshmai3zyiuji9cyesjlgn.png)

**Statuses**

Each device ends as **Pending**, **In Progress** **Success**, or **Failed**.

- A restore has no **Partial Success**. Either the device was rebuilt or it wasn't.
- Devices that were stopped by an administrator, ran out of time, or failed on their own are all marked **Failed**. The **reason** on the row tells you which one happened.

#### Restore History

![](https://uploads.developerhub.io/prod/97qW/q2xl7hhpupcgtiwz440io2343jx6xh0falrpislpdoiib6ltytf9e44joki8bvvx.png)

Go to **Backup Restore → Restore → History**. History lists every restore run in your account, newest first. You can filter by status and search by name. Each restore job runs once, so History shows one row per finished restore.

- Job status is **Pending**, **In Progress**, or **Completed**.
- A job stopped before any device started never produces a run. It stays in the job list as **Stopped** and doesn't appear in History.

#### History Details

Select a run to open its record. History works as an **audit trail**: the header shows the job **as it was when the run started**, and later edits or deletion don't change it.

![](https://uploads.developerhub.io/prod/97qW/eg7l8l3xovevtq2ju4lgn0u6bqs38nw7c71dvfeorzjnr8db58kwv0qimsqjv5g8.png)

The header includes:

- Name, description, and creator
- Source device and the full restore point details: when the backup was taken, the backup job that created it, mode, scope, destination, size, and, for incremental backups, the chain and position in the chain
- Target devices, schedule, Max Restore Duration, and whether automatic restart was on

Below the header, a table lists each device with its group, agent version, final status, restore duration, and failure reason (if any). Use the status tabs, filter, or device search to narrow down large runs.

---

## Dashboard

Go to **Backup Restore → Dashboard** for real-time visibility into Endpoint backup and restore coverage across your fleet.

![](https://uploads.developerhub.io/prod/97qW/l4e6t610iq9g43os8fvxk1pzpq1im6jmxuvogupi6igd5hin85mzpu3ngtz341el.png)

- **Filters:** Filter by **Endpoint Group** (evaluates current device membership) and **Timeframe** (24h, 7d, 30d, or Custom).

![](https://uploads.developerhub.io/prod/97qW/h502v5gie12k843wboi7csgigwkqik0ijan7zdw49v493sjhiqqt7i7mmxgu8xsp.png)

| Panel | Details |
| ---- | ---- |
| **Endpoint Backup Coverage** | Every eligible device falls into exactly one of three buckets: - **Fully backed up**: latest backup succeeded or partially succeeded - **Missed a recent backup**: previous backup exists, but the latest attempt failed or timed out. - **Never completed a backup**: Device lacks a recorded baseline backup. Note Devices that aren't targeted by any active backup job are **left out **rather than counted as unprotected. If you stop the only job covering a group, that group's devices drop off the panel instead of turning red. To find devices with no backup job, use the Report. ![](https://uploads.developerhub.io/prod/97qW/8hdinuybrrvp84xgh3iwu5bu714s6v6bx53lsg5fd7hrm03ztftvr24l84h7tpz1.png) |
| **Endpoint Backup Coverage Trend** | The same three buckets over the last 14 days, one point per day. A flat line is normal for weekly backups. Days with no data appear as gaps, not zeros. ![](https://uploads.developerhub.io/prod/97qW/u2rnh3s43ufa6ljsph8kr23gd2wc2ulucqk01wc8dekr24910icrr2htm7byt0ng.png) |
| **Backup Statuses** | Backup runs in the timeframe: **Succeeded**, **Partial Success**, **Pending**, **Running**, **Failed**, and **Timeout** (the device never picked up the run before its window closed) ![](https://uploads.developerhub.io/prod/97qW/hvb7fqee3p1g5gfcz3b5kr81xig44rpqbq7i3hqbofafqiboohpaqmhn33xpgbxu.png) |
| **Restore Statuses** | Restore runs in the timeframe: **Succeeded**, **Pending**, **Running**, and **Failed**. Timed-out and stopped restores count as Failed. ![](https://uploads.developerhub.io/prod/97qW/as6nipnyyy6gvex7cswdnyrvtsp9vytrgt0fsdzvepl2p14uy1yo4vn42ae6lzl0.png) |
| **Top Backup Failure Reasons** | The failure reasons devices reported, most common first. If every row shows zero, there were no classified failures in the timeframe ![](https://uploads.developerhub.io/prod/97qW/hywh8w4z2d9rqpuaobw0cy148ku3r2pau4t1xzpwrrcmp714hm0rc2esys4ts8xx.png) |
| **Needs Attention** | The 10 most recent problems. The **Backup** tab lists failed and timed-out backup runs, and the **Restore** tab lists failed restore runs. There's one row per run, so a device that failed twice appears twice. ![](https://uploads.developerhub.io/prod/97qW/hywh8w4z2d9rqpuaobw0cy148ku3r2pau4t1xzpwrrcmp714hm0rc2esys4ts8xx.png) |

## Notifications

Configure automated notifications across In-app and Email channels under **Backup & Restore > Notifications** > Click **Add** button.

![](https://uploads.developerhub.io/prod/97qW/8mmpeus45qgpscu5eyvcganow2t8n60pfvt7jr4nlgfr33347zio0hp96ibmx43s.png)

| Setting | Options |
| ---- | ---- |
| **Event Types** | Backup completed, Backup failed, Restore completed, Restore failed ![](https://uploads.developerhub.io/prod/97qW/d4xwl6txefrn2lmaqzsp996fyo2v16oys3bc09gkb3mwnk4zdzxmagpx54eu4op1.png) |
| **Channel** | - **In-app**: appears under the notification bell in the console for every administrator in the account. It has no recipient list.  - **Email**: sent to 1–100 addresses you enter. Recipients don't need to be console users. ![](https://uploads.developerhub.io/prod/97qW/fqerz6zzj466a3ui4fbowbfhe8j81sf69v9qm7dc8ilv199t8jx2kfglf25fzqvh.png) |
| **Execution Rules** | - Maximum of **8 rules** per account (1 In-app + 1 Email per event) - You can disable a rule without deleting it. It keeps its settings but stops sending notifications. - Notifications generate **per device** (e.g., 50 devices = 50 notifications) - In-app notifications appear immediately. Emails queues processes **10 emails every 5 minutes** Tip Use **In-app** for success events and **Email** for failure events. An Email rule on **Backup completed** for a large fleet sends one email per device for every run. |

Note If hostname privacy is turned on for your account, device names show as `<private>` here and everywhere else in the console.

## Reports

A **report** is a saved configuration: what to report on, the time period, which groups, how often, and who receives it. Each time it runs, it creates a **report run** that you can view in the console, export as PDF or CSV, and email as a download link.

![](https://uploads.developerhub.io/prod/97qW/ijzexkz17kxpp2qp3ux1qtvgwd5bhef9gi1cfjfaj3bmgjudcakhj6bueohyyott.png)

There are two report types: **Backup Summary Report** and** Failed and Overdue Agents**.

### Create a Report

Navigate to **Backup & Restore > Reports >** Select** Create Report** to start.

![](https://uploads.developerhub.io/prod/97qW/iw9i2nc386un5vkjbao9pbx4j59mjks5ms5rs94klcpcvwgc3j88wfzz2t36ohca.png)

| Configuration |  |
| ---- | ---- |
| 1. Choose a **Report Type** and enter a **Report Name**  | Up to 100 characters, unique within your account ![](https://uploads.developerhub.io/prod/97qW/h7ze3td004717isizqifdf59rmlso1e7mg0qvn1l5hg3ctrg9doig2nonmsljatx.png) |
| 2. Choose a **Generating Schedule** | Every schedule runs at a fixed time, with no day or time to set: - One time: Once at the next 00:00 UTC, then it turns itself off - Daily: Every day at 00:00 UTC - Weekly: Every Monday at 00:00 UTC - Monthly: The 1st of every month at 00:00 UTC ![](https://uploads.developerhub.io/prod/97qW/v2g2cz00d5cya5rihmt3dbeo43htsqkcb3lr06ftmkroymvifpwm6bhb7gj8p96t.png) |
| 3. Choose a **Time Frame** | Last 24 hours, Last 7 days, Last 30 days, or Custom Range ![](https://uploads.developerhub.io/prod/97qW/c44myelrhel8nt2s39bliwnrzgbid23o160u0yfhkkyk20dlkduxcr12e8sjv8qm.png) |
| 4. Choose the **Groups** to include.  | Leave this empty to include all groups ![](https://uploads.developerhub.io/prod/97qW/uwvo11mzdwhuboxcspor3qend336jvoikl8agve2lrn6sy4mokdpqnejy9jg991w.png) |
| 5. (Optional) Turn on **Share report by email** | Enter: - **Recipients**: one or more email addresses, separated by commas (required) - **Email Content**: a message of up to 1,000 characters. A default message is filled in, and you can replace it - **Full Report Format**: **PDF** or **CSV** ![](https://uploads.developerhub.io/prod/97qW/f1pksa6038cq2jmtmyctbagcvupbfruxqte26l4stjdmmdcldk4yfhyclsba1jrn.png) |
| 6. Preview and  Save | **Preview** shows the layout of the report before you save it; **Back to Form** returns you to the settings. ![](https://uploads.developerhub.io/prod/97qW/uvk3044h55e8ql06sgt512uv58lwsx5okq9rumkysan0t3jbiwqowvu10kuo6zc8.png) Note Preview uses sample data. Use it to judge layout, not your own numbers.  |

**What Recipients Receive?**

Each recipient gets an email carrying your Email Content and a download link valid for seven days from the moment the run completed.

![](https://uploads.developerhub.io/prod/97qW/0ulbyt71vc9zrvyz0fxjbdt8lxqqit68xrhg8rhluwipjt5xe85e3vdcganvy11b.png)

Report download links in emails are **public**. Anyone with the link can download the report without signing in. Send reports only to trusted recipients, and treat the email as confidential. Reports carry a "Confidential — for internal use only" banner.

### Manage Reports and Runs

**Report history**

Click a report's name to open it:

- **Generated**: When the run completed, in your local time
- **Status**: Generating, Completed or Failed
- **Recipients**: Who that run was addressed to
- **Type**: Scheduled if the schedule produced it, Manual if someone clicked Generate Now

![](https://uploads.developerhub.io/prod/97qW/oxmlz3hw2xq55ng8j4gsayqcjkjfp4ktglef1vf57mnvjqaft4unq7f4d6nbekwy.png)

| Function | Meaning |
| ---- | ---- |
| **The ⋮ menu** | - **View Report**: Open it in the console - **Export as** PDF or CSV (CSV is always a .zip archive) - **Delete**: removes that run, its files and its download link; other runs and the configuration are untouched) View and Export are only available on a **Completed** run |
| **Generate Now** | If **Share report by email** is turned on, clicking **Generate Now** will still email the full recipient list with a download link, even if the schedule is disabled. |
| **Edit** | Changes the report settings |
| **Turn a schedule on or off** | The schedule toggle only controls recurring automated generation; it does NOT suppress email sharing when manually triggering reports ![](https://uploads.developerhub.io/prod/97qW/36fkyg2l6vpkoc9r0fz9tffxdr31y0a1v59wfgbsdoyfanmhl40l5zr4uzgwsx5m.png) |

**Report Limits and Retention**

- **Tables are capped at 1,000 rows.** Larger tables show "Showing the first 1000 rows. This table was truncated." Export as CSV to get the full data.
- **Only the 20 most recent runs of each report are kept.** That's about three weeks of history for a daily report, or almost two years for a monthly one. Older runs are removed along with their files and links, so export anything you need to keep.

## Important Notes

A few things to keep in mind:

- The feature requires the MA-BKR license (SKU MA-BKR).
- Any credentials used to reach a storage destination are always stored encrypted, so passwords are never exposed.
- Each device has an execution time limit; if a backup runs too long (around 24 hours by default when no custom Max Backup Duration is set), it is marked as Failed.
- The backup feature is available only on Windows devices running MetaDefender Endpoint version **7.6.2607.xxx or later**. Restore requires **7.6.2609.xxx or later**.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
