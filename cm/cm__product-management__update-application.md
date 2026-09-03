<!-- source: https://www.opswat.com/docs/cm/product-management/update-application -->

# Update Application

In this guide, we'll walk you through step by step on how to roll out application updates for connected product instances from My OPSWAT Central Management.

- [Importing Target Versions ](https://www.opswat.com/docs/cm/product-management/update-application#importing-target-versions-): Import or upload target software versions to My OPSWAT Central Management for centralized distribution across your network.
- [Package Storage & Cleanup](https://www.opswat.com/docs/cm/product-management/update-application#package-storage--cleanup): How update packages are stored within My OPSWAT Central Management.
- [Creating Update Job](https://www.opswat.com/docs/cm/product-management/update-application#creating-update-job): Initiate and configure update jobs for one or more instance.
- [Monitoring Update Job](https://www.opswat.com/docs/cm/product-management/update-application#monitoring-update-job): Track real-time download and installation progress across all selected instances.

To create a rollback job, refer to our dedicated [Roll Back Application](https://www.opswat.com/docs/cm/product-management/creating-rollback-job) guideline.

## Supported Products

Remote Application Update supports the following products:

- **MetaDefender Kiosk Windows**:  Version 4.8.0.xxxx or later
- **MetaDefender Kiosk** **Hardened Image**:  Version 4.8.3.xxxx or later
- **MetaDefender Core**: Version 5.20.x or later. The Automatic Application Upgrade setting must be enabled within the individual MetaDefender Core instance.
- **MetaDefender Industrial Firewall**: Version 3.4.1.xxxx or later. The Automatic Application Upgrade setting must be enabled within the individual MetaDefender Industrial Firewall instance.

## Importing Target Versions

Before you can update any instances, the target versions must be downloaded and imported to My OPSWAT Central Management.

Note All target versions are downloaded directly from **My OPSWAT Portal**.

![](https://uploads.developerhub.io/prod/97qW/9qfsna9pockn0byalxjbnc03bgygdahs9nn30j5fobrxd8oh9pd40z43z9y3gx0c.png)

### **Online Import**

To use this method, ensure your environment has internet connectivity.

- Navigate to **Updates > Software.**
- Select the product you wish to update and click the **Packages** tab.
- Click **Check new versions.**
- In the dialog, select the target version you need and click **Import.** The system will automatically download and import the package from My OPSWAT Portal.

![](https://uploads.developerhub.io/prod/97qW/e7m6l7lnp43tx5mtd28cjkg22ssy9rz5mr46w4rn8khvxg2gmhsdhzfrvdgl83xy.png)

### **Manual Import**

Use this method for air-gapped or isolated environments without internet access.

**Step 1: Obtain software packages**

You'll need to manually download the target version from My OPSWAT Portal and transfer it into your isolated environment.

- Log into the [My OPSWAT Portal](https://my.opswat.com/).
- In the left-side menu, click **Product Downloads**.
- Search or scroll for specific product to open its details page.
- Click **Download**, then select the specific system and version you need.

![](https://uploads.developerhub.io/prod/97qW/yhubjnl63inzf4iu21pdvp9s1yjqp7y7t2u0udddrdskcb4dl3lycsmpq5287t3j.png)

**Step 2: Import target version to My OPSWAT Central Management**

- Open My OPSWAT Central Management, navigate to **Updates >** **Software**.
- In the **Package File** section, upload the target version and click **Import**.

Note Please ensure the file size is under 20GB limit.

![](https://uploads.developerhub.io/prod/97qW/xwa9phsinw02ad69i3b10bx10h1v2cjx90v6pkf2nyrhz929ss210hnedq9wmumv.png)

### Package Storage & Cleanup

1. **SaaS deployment**: Update packages are not stored within My OPSWAT Central Management.
2. **On-Premises**: Update packages are stored on My OPSWAT Central Management server machine after being downloaded or manually uploaded by administrators.
   1. Example Path: C:\Program Files\OPSWAT\MOCM\data-agent\volumes\fusion-updater

![](https://uploads.developerhub.io/prod/97qW/622l6krquweuudsa5vvpy1cjldevexkomfo9ovpc1sgmt6tic2u34o92nc7m5kua.png)

3. **Package retention & cleanup**
   1. My OPSWAT Central Management does not automatically delete downloaded update packages. Package retention and cleanup are managed by administrators.
   2. Administrators can remove packages directly from My OPSWAT Central Management when they are no longer needed or to free up disk space.

Please Note Only delete packages after all update jobs have completed successfully or have been stopped. Deleting a package while an update job is running may cause errors.

![](https://uploads.developerhub.io/prod/97qW/9mkxt9im16q7g3vrk5x5esekifh551mgvzda6tf9g1u102mmfg3m84ysz4imabnf.png)

### **Import Status**

The Import Status column reflects whether a target version is ready for use in an update job.

![](https://uploads.developerhub.io/prod/97qW/letkeiaqxnilztcc608oxmbfoyx3vlqrdyst7bnld8r4vwafoco459emkh68n985.png)

- **In Progress**: The target version is currently being processed. Wait for it to complete before proceeding
- **Completed**: Target version is ready for deployment
- **Waiting for Review**: Administrator confirmation is required before the target version can be used.
- **Failed**: The import encountered an error.
- **Supported Actions**:
  - **Retry**: Click Retry on a failed entry to attempt the import again.
  - **Delete**: Click the icon to remove the package from the list.

### **Troubleshooting**

If you run into the following issues, try the following solutions:

- **Import stuck "In Progress"**: Likely a network timeout. Wait 30 minutes; if it doesn't clear, delete the entry and retry.
- **Upload fails**: Ensure the file size is under the 20GB limit.
- **Target version missing from Create Update Job**: Only target version with a Completed status would appear in update job configuration. Confirm it has finished uploading.
- **Cannot import target versions**: Check your license status. If it has expired, contact OPSWAT Support.

## Creating Update Job

An update job defines which instances to update, which target version to deploy, and how the rollout should be scheduled and executed.

Before you begin, confirm that:

- All product instances are connected to My OPSWAT Central Management
- The target version appears in the **Packages** tab with a **Completed** status.

To create an update, navigate to **Updates >** **Software > For Application.**

- Select the product you wish to update and click the **Job** tab.
- Click **Create Update Job**.

![](https://uploads.developerhub.io/prod/97qW/2v6koztz28pqoepoofh9u7kpailpl97oungresut7lvhvcaxx2gpcckzfke1omrk.png)

### **Step 1: Update Job Information**

Provide a name and description to identify and track the job.

![](https://uploads.developerhub.io/prod/97qW/zdu4kyoo7x7ba1ne4otmh0k74npd64opus86un17htopmhs7k6wc1hidux1lkohe.png)

- **Name**: A short, recognizable label for the job,
- **Description**: Briefly note the target instances, purpose, and expected outcome.

### **Step 2: Target Selection**

**Group/Instances**

Define which instances will receive the update. You can target by group or by individual instance.

![](https://uploads.developerhub.io/prod/97qW/aqaywpe3yz07y6vsg8d8wzjtreq9m4dozlemzq9702u2tqf0bw066pwpa00a8zuz.png)

- **Specific Groups**: The update applies to all instances within the selected groups.
- **Specific Instance**: The update applies only to the individually selected instances.

**Target Version**

Once you've defined the target, select the Target Version from the dropdown.

![](https://uploads.developerhub.io/prod/97qW/q7op2s1dbfuahfa6nmilqdue9xec9yojisti1177i9pwii6vfh3m6hzl8a8j5fwj.png)

### **Step 3: Update Settings**

Update jobs are split into two distinct phases: **Update Preparation** and **Maintenance Window**. This separation allows large target version to download in the background during normal operations, limiting service interruption to a short, scheduled window.

**Update Preparation**

Defines when instances begin downloading the target version in the background.

![](https://uploads.developerhub.io/prod/97qW/hyy90lkbiff1u7fu2e9b7pzdxzfpnqz1coxasdt403p2p7o5nh6lhgfhcpg2m8ah.png)

- **Start Time**: When instances begin downloading target version.
- **End Time (Optional)**: When the download window closes.
  - If not set, the window remains open until all instances complete with the download.
- **Timezone**: Choose timezone for update preparation.
  - **Fixed Timezone**: All instances download at the same absolute time.
  - **Local Timezone**: Each instance uses its own local timezone.

Tips Set a wide preparation window (one to two days) to ensure instances that are temporarily offline still have time to complete their download.

**Maintenance Window**

Defines when instances execute the actual application update.

![](https://uploads.developerhub.io/prod/97qW/8ypjbaosdgiejb60pjyls1ys06l0tleyy8uf4evk6qz2thew0j92zyw4q3a80avc.png)

- **Recurrence**: Choose Daily or Weekly.
  - **Daily**: Update can occur any day
  - **Weekly**: Update only occurs on selected days (e.g., weekends only)
- **Time Window**: Set the specific "From" and "To" times during which update is allowed to execute.
- **Timezone**: Choose timezone for the update.
  - **Fixed timezone**: All instances update at the same absolute time.
  - **Local timezone**: Each instance uses its own local timezone.

### **Step 4: Update Options**

Fine-tune rollout behavior to maintain network stability and system health.

![](https://uploads.developerhub.io/prod/97qW/87im4livgv5c7qk8jvvytvv1tez2eb2g9oiovu8wzwtlhpdaoqwlywzji34j5cmn.png)

- **Concurrency**: Update all instances simultaneously, or cap the number updated at a time. For fleets of 100 or more, a concurrency limit of 10–20 is recommended to reduce network load.
- **Stop On Failure**: When enabled, the entire job halts if any single instance fails.
- **Auto Reboot (for Kiosk only)**: Automatically restarts Kiosk instance after a successful installation.

### **Step 5: Preserved Folder**

Please note This step is only applicable for for **MetaDefender Kiosk Hardened Image** update

Provide your folder path and check the option to "Run command line script" if required for your setup.

![](https://uploads.developerhub.io/prod/97qW/ffjleguw0kw7jhkvlvnea19cst3ybzfanp310vz6ndr1w0r32c3vnrkfmmo94fj0.png)

### **Step 6: Report**

Add one or more email addresses to receive automated alerts when:

- The job completes.
- Any individual instance fails.

![](https://uploads.developerhub.io/prod/97qW/8fxoh7zae0iyintyni2kdxjfomzohxqqw2chc936it4fuyv58x4upu2dn6xwdnbm.png)

![](https://uploads.developerhub.io/prod/97qW/r28lvwbsgmqbt90mhpggdcpnt3m5zrgc91a440n6pcd4g8irxzpkl783bh0wgcak.png)

## Monitoring Update Job

After creating a job, you can track its progress and manage it from the **Jobs** tab. To get there, navigate to **Updates >** **Software** and select **Jobs**.

![](https://uploads.developerhub.io/prod/97qW/l58ano0qa7ij1e46dtik7lu07pojswizcri64fa679kssfeintkuqg6q234l13ar.png)

### **Job Details**

Click any update job in the table to open its detailed view.

#### **Summary Panel**

The top panel provides a high-level summary of the update job.

![](https://uploads.developerhub.io/prod/97qW/k9j2tchtgt332bp7d61k7iauryig1vkl0paq0e48zqop7mw7ch8hb20teu54sp59.png)

- **General information** including Job Status, Description, Created By, Target, Update Preparation schedule, Maintenance Window, Update Options, and notification recipients.
- **Job Status**:
  - **Scheduled**: The job is waiting for the download window to begin.
  - **Running**: At least one instance is actively processing.
  - **Completed**: All instances have finished processing, whether successfully or with failures.
  - **Stopped**: The job was manually stopped or halted due to a failure.
- **Supported Actions**
  - **Delete**: Permanently removes a job. Available when the job status is Completed, Stopped, or Scheduled. Click Delete on the job, then click Confirm to proceed.

#### **Update Job Progress**

Below the summary panel, you can filter instances by their update status.

- Use the tabs to switch between views:
  - **All:** Every instance in the job, regardless of status.
  - **Success**: Instances that completed the update successfully.
  - **Pending**: Instances waiting to start the update job.
  - **In Progress**: Instances currently processing the update job.
  - **Failed**: Instances where the download or installation failed.

![](https://uploads.developerhub.io/prod/97qW/glisvcgbgrtnxps5olg6y3k2dfx1qecu6lk8csxstzx7q405g8l07ybjlei34lkk.png)

- View detailed information like Update Status. Name, Group, Platform, Current Version, Target Version, Activity, Last Update.
- **Instance Update Status:** Each instance has its own granular status that reflects exactly where it is in the update process:
  - **Pending**: Waiting to start.
  - **Downloading**: Actively downloading the target version.
  - **Waiting for Update**: Download complete; waiting for the Maintenance Window.
  - **Updating**: Actively installing target version.
  - **Update Success**: Installation completed successfully.
  - **Download Failed**: Target version could not be downloaded.
  - **Update Failed**: Target version could not be installed.
