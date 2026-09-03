<!-- source: https://www.opswat.com/docs/cm/product-management/backup---restore -->

# Backup & Restore

Backup & Restore is a feature in My OPSWAT Central Management that lets you automatically back up the full system image of Windows endpoints across your organization.

You create backup jobs, choose which devices to protect, decide where the backups are stored, and set a schedule for them to run automatically. The system sends the commands to each device, tracks progress, and reports results directly in the console.

> Restore is not available in the current release. This guide covers the backup workflow only. Restore will be supported in a future version.

![](https://uploads.developerhub.io/prod/97qW/clyubaaec00x6574qajci5pal0umbrnygkb4dvy1nlcvn3lo360gqk43se9tv5jo.png)

You open the feature from the left-hand menu under **Endpoint Security** **→ Backup Restore**.

## Before You Begin

Keep the following in mind before creating a backup job:

1. This feature requires the **MA-BKR license** (SKU MA-BKR). It is not available unless your account is licensed for MA-BKR.
2. Backup is available on **Windows devices running** **MetaDefender Endpoint version 7.6.2607.xxx and later**. Non-Windows devices and devices on older versions are automatically excluded from any target you select.
3. You need at least one reachable storage destination (for example a shared folder path such as \\\\server\\share). An unreachable or misconfigured destination is rejected when you create the job.
4. Each run stores a complete image (see Backup scope and mode below), so make sure the destination has enough free space.

## **Main Screen**

The Backup screen has three tabs.

- **Active Jobs** lists every backup job that is currently set up, with its status, target, schedule, and a per-status device count.
- **History **keeps a record of past runs so you can review their results.
- **Backup Storage **lets you browse the backups that have been stored, organized by device or by file.

![](https://uploads.developerhub.io/prod/97qW/mc4piy7sloqmh7fbzeadytnqxnkmwqdt8d8mb3vwvrrlcylx89vx8g65okphw5j7.png)

### **Active Jobs**

Each job row shows device counts by status: Pending, In Progress, Partial Success, Success, and Failed. This gives you a quick view of how the latest run is going across all targeted devices.

![](https://uploads.developerhub.io/prod/97qW/h7jh3ggpfow41y3zpyvy0cw7wqiug198wdp8pkxf3euyiz6xrd7jcao0w2e7ad60.png)

When a job finishes a run, it moves automatically to the **History** tab. If the job is recurring (Hourly, Daily, Weekly, or Monthly), a new active job is created automatically to handle the next scheduled run.

### **History**

The **History **tab records each completed run with its start and end time and the number of devices that ended in each status. Use it to audit past backups and confirm whether they succeeded.

![](https://uploads.developerhub.io/prod/97qW/ikib155i7ngml1e18eacnyr399w5naj0m1wl60727o2fu6l0wrcn58rj9gntylp7.png)

### **Backup Storage**

The **Backup Storage** tab shows what has actually been stored. You can view it By Device or By File, and see the backup scope, destination, size, and the time of the last backup for each device.

![](https://uploads.developerhub.io/prod/97qW/9e5wvmsjiqdvnfqbo18mjc8938fw98frkz37o9l5wwg773wd85t95ovc88p82xlr.png)

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

1. **Enter a Job Name and Description**. The job name must be unique within your account; a duplicate name will be rejected.

![](https://uploads.developerhub.io/prod/97qW/oln5xzzhkptvi7xgjhjsbilof15ph733bq9at11ganx69gdpjxl2jroywd878ale.png)

2. **Choose target devices to back up**. *Please note only Windows devices running MetaDefender Endpoint 7.6.2607.xxx or later can be backed up.*
   1. All Groups applies to every device group.
   2. Specific Groups applies only to the groups you pick.
   3. Specific Devices applies only to the individual devices you select.

![](https://uploads.developerhub.io/prod/97qW/hasrupvajzobxrsex409s5eycd3opixk2lziyardul3tz9spoj5j46r04whqpy0t.png)

3. **Configure Backup Scope and Backup Mode**.
   1. Backup Scope is currently fixed to **Full Image.** It captures all volumes needed to restore the operating system, including the system, boot, and recovery partitions; non-OS data volumes are excluded.
   2. Backup Mode is currently fixed to **Full**, which captures all selected data on every run. Because every run stores a complete image, make sure your destination has enough free space.

![](https://uploads.developerhub.io/prod/97qW/d5hlpif3aksxyz0ach2d8melmupqlvsmqbq15c8q3zgzvk3104disq8bcv1rvxjy.png)

4. **Configure Backup Destination**. Choose where backups are stored.
   1. Mirror sends the backup to all destinations at the same time
   2. Failover sends it to the primary destination and falls back to the others if that one is unavailable.
   3. For each destination, pick a Type (such as a shared folder) and enter the path (for example \\\\server\\share). Use **Add Destination** to add more. An unreachable or misconfigured destination will be rejected.

![](https://uploads.developerhub.io/prod/97qW/nedd3z0pll12temeibihi60zq0t7ny9xqoj3ik7qm736kcwt2m9r957jp2j1f033.png)

5. **Set up a schedule when backups run on target devices**.
   1. **Frequency** can be Once, Hourly, Daily, Weekly, or Monthly; depending on the choice, the form asks for the matching details (for example days of the week for Weekly, or a day of the month for Monthly).
   2. For **Timezone**, choose Local device time to run by each device’s own local time, or pick a specific timezone (such as UTC+7) so all devices run at the same moment. For a one-time schedule, the system rejects a start time that is already in the past.
   3. **Max Backup Duration **(optional) limits how many hours a backup may run on a device. If a device exceeds this window before finishing, that run is marked Failed. If you leave it empty, a default limit of about 24 hours applies.

![](https://uploads.developerhub.io/prod/97qW/at4rczw0a6us2rr0xu833iphd4ii32nfg0g4xtogmf694i7gimlkmascuuoasicm.png)

6. When the form is complete, click **Create **to save the job, or **Discard** to cancel.

## Manage Backup Job

Click a job in the **Active Jobs** list to open its detail view, which shows its status, target, scope, mode, destination, schedule, and Max Backup Duration. Use the **Action menu **at the top right to manage the job:

![](https://uploads.developerhub.io/prod/97qW/f1k9rgmiucj8yek9b40wueom9yhvgztiz4db4akjv0k6awcu3wo11teik0efxsbh.png)

| Action | What it does |
| ---- | ---- |
| **Clone** | Duplicate the job's settings into a new job. |
| **Stop** | Stop a running or pending job. Devices that are backing up receive a stop command and are marked as failed by force stop, while devices that have not yet started are removed from the queue. A stopped job can be started again with** Start**, which recalculates the next run time from the schedule. |
| **Edit** | Change the job's settings, such as its schedule or targets. |
| **Delete** | Remove the job. You cannot delete a job while it is running, so stop it first. |

## Monitor Progress and Results

While a backup runs, each device reports its progress and you can watch the completion percentage rise. When a device finishes, it ends in one of these results: Success, Failed, or Partial Success (finished but with some issues).

These results are summarized on the** Active Jobs** list and recorded in the **History** tab. Every backup event is also written to the event log, so you can review a per-device history such as backup started, in progress with a percentage, completed, failed, or completed with some issues. Log entries expire automatically according to the data retention policy.

![](https://uploads.developerhub.io/prod/97qW/ikib155i7ngml1e18eacnyr399w5naj0m1wl60727o2fu6l0wrcn58rj9gntylp7.png)

## Important Notes

A few things to keep in mind:

- The feature requires the MA-BKR license (SKU MA-BKR).
- Any credentials used to reach a storage destination are always stored encrypted, so passwords are never exposed.
- Each device has an execution time limit; if a backup runs too long (around 24 hours by default when no custom Max Backup Duration is set), it is marked as Failed.
- The backup feature is available only on Windows devices running MetaDefender Endpoint version 7.6.2607.xxx or later.
