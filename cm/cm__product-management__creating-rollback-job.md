<!-- source: https://www.opswat.com/docs/cm/product-management/creating-rollback-job -->

# Roll Back Application

You can easily restore instances to their previous version using a **Rollback** job.

Note This feature is currently limited to **MetaDefender Kiosk Windows** and **MetaDefender Kiosk Harden Image** and supports reverting to the immediately previous version.

**Before you begin:**

- Verify that the previous version is available. See the [Importing Target Versions](https://www.opswat.com/docs/cm/product-management/update-application#importing-target-versions) guidelines for details.
- Check instance connectivity; all instances must be online and connected
- This capability applies only to instances previously updated via My OPSWAT Central Management

![](https://uploads.developerhub.io/prod/97qW/fjlme22dj3xxwdrdsdjov9uk00i1ypja99tf10u2val3ujtyi1qtzxphswqv38mk.png)

## Creating Rollback Job

Configurations for Rollback are mostly similar to Update Job. This section outlines the primary steps, for in-depth breakdown of each setting, refer to the  guideline.

Note Rollback will revert all settings to the previous version's defaults. Ensure you have configuration backups.

**Step 1**: To create a rollback, go to **Updates > Applications > Jobs**. Click **Create Rollback Job**.

**Step 2**: Define the job settings across the following core sections:

![](https://uploads.developerhub.io/prod/97qW/7gvpc0blsxiahpdxpaxhj5yyw6zo54o4pwsj9g2ffmrsz6hno2h1zo6ab95q00vr.png)

- **Job Information**: Enter a unique name and detailed description for the task
- **Target Selection**: Select the target instance groups or individual instances, then specify the target software version for the rollback.
- **Rollback Settings**: Configure timezones, execution frequency, and designated maintenance windows to execute the rollback.
- **Rollback Options**:
  - **Concurrency**: Update all instances simultaneously, or cap the number updated at a time. For fleets of 100 or more, a concurrency limit of 10–20 is recommended to reduce network load.
  - **Stop On Failure**: When enabled, the entire job halts if any single instance fails.
  - **Auto Reboot**: Automatically restarts Kiosk instance after a successful installation.
- **Report**: Add one or more email addresses to receive automated alerts when the job completes or any individual instance fails.

![Application rollback email report](https://uploads.developerhub.io/prod/97qW/26mhqnadl4o7l5v650u1lqtzet8vhaex4ckehee9v2wf45heiqcgzlaxpqoexb4p.png)

## Monitoring Rollback Job

Click any rollback job in the table to open its detailed view, where you can track overall progress and the status of each individual instance.

![](https://uploads.developerhub.io/prod/97qW/gp12k2hpx05lpuq62p3rhtf2ui50w4c90khf2w15ynum2whfwt250w5h4phshtrn.png)

**Rollback Status**

- **Pending**: Job is scheduled and waiting to run.
- **Downloading**: Actively downloading the target version.
- **Waiting for Rollback**: Download complete; waiting for the Maintenance Window.
- **Rolling Back**: Rollback is actively in progress.
- **Rollback Success**: Rollback completed successfully.
- **Download Failed**: Target version could not be downloaded.
- **Rollback Failed**: Rollback did not complete.
