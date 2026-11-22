<!-- source: https://www.opswat.com/docs/mdcluster/operating/operating-workers -->

# Workers

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This section (**Library** > **Workers**) will allow the system administrator to add the MetaDefender Cluster (MD Cluster) Workers which will help deploy and monitor activities of MetaDefender Core, MD Cluster API Gateway and MD Cluster Callback Service.

Info

MD Cluster Callback Service is optional. However, if the scan result needs to be sent to a Webhook. This service must be installed in order to use the Callback Service feature.

### [Automatically Deploy Workers](/docs/mdcluster/operating/operating-workers#automatically-deploy-workers)

MD Cluster Workers can be automatically installed and enrolled using deployment scripts generated from MD Control Center (**Add Workers** > **Add by Script**). Administrators can follow the instructions to [retrieve the installation script](/docs/mdcluster/installation/md-cluster-worker#retrieve-the-installation-script) and then [run the installation script](/docs/mdcluster/installation/md-cluster-worker#execute-the-installation-script) on target hosts to deploy Workers with the required configuration and cluster enrollment settings. This automated approach simplifies large-scale deployments, reduces manual effort, and helps ensure consistent Worker configuration across all managed hosts.

---

### [Manually Add Workers](/docs/mdcluster/operating/operating-workers#manually-add-workers)

To manually add an MD Cluster Worker, select **Add Workers** > **Add Manually**, then enter the **Name**, **Host**, **Port**, and **Connection Key**. The **Port** and **Connection Key** must match the values configured in the Worker during installation. After completing the fields, select **Submit**. MD Cluster will validate the connection and indicate whether the Worker was added successfully.

Info

Manual addition is intended for Workers that are already installed but not currently connected to MD Control Center. For new deployments, use the automated deployment process whenever possible.

---

### [Bulk Import Workers](/docs/mdcluster/operating/operating-workers#bulk-import-workers)

System administrators can import MD Cluster Workers using a YAML file instead of adding them individually through the MD Cluster Control Center interface. To simplify the process, a downloadable template (**Download YML Template**) is available when selecting the **Import YML** tab in the **Add Workers Manually** dialog. The following example demonstrates a YAML configuration that includes an MD Cluster API Gateway and three MetaDefender Core instances:

YamlCopy- display_name: API-Gateway
host: 10.1.100.100
port: 8893
connection_key: 1234abcd
- display_name: Core-1
host: 10.1.100.101
port: 8893
connection_key: 1234abcd
- display_name: Core-2
host: 10.1.100.103
port: 8893
connection_key: 1234abcd
- display_name: Core-3
host: 10.1.100.104
port: 8893
connection_key: 1234abcd

Info

Importing a list of Workers is intended for Workers that are already installed but not currently registered with MD Control Center. This method provides a convenient way to add multiple existing Workers at once. For new deployments, use the automated deployment process whenever possible.

---

### [Upgrade Workers](/docs/mdcluster/operating/operating-workers#upgrade-workers)

MD Cluster Worker is included with MD Cluster Control Center. Whenever the Control Center is upgraded to a newer version, a corresponding version of MD Cluster Worker also becomes available for centralized upgrade directly from the Control Center console.

To upgrade Workers:

1. Navigate to `Library`> `Workers`.
2. Look for the notification banner displayed on the page indicating that a Worker upgrade is available.
3. Click `Upgrade Now` .

4. Confirm the action to begin the upgrade.

During the upgrade process:

- The banner displays the message: **“Worker update in progress”**
- Worker instances may temporarily show a **Disconnected** status while restarting.
- File scanning operations continue normally during the upgrade.

After the upgrade completes successfully, all Workers display the new version number (for example, **2.6.1**) in the **Version** column.

---

### [Deploy Instances](/docs/mdcluster/operating/operating-workers#deploy-instances)

Once MD Cluster Workers have been added and their status are shown as `Available`. The system administrator can now select **Deploy Workers** > **Deploy Workers** and deploy MetaDefender Core, MD Cluster API Gateway, MD Cluster Callback Service, and Download Service separately or all at the same time.

To deploy the MD Cluster API Gateway. Simply choose the **Installer** of MD Cluster API Gateway and select an available MD Cluster Worker.

The Log Level, Port, and custom Install Directory that will be assigned to MD Cluster API Gateway can be set by clicking `Advanced Settings`.

The system administrator can choose the **Installer** of MetaDefender Core that should be deployed on available MD Cluster Workers.

The system administrator can also modify the Log Level, Port, custom Install Directory, custom Temporary Directory, and Connection per File Service of MetaDefender Core that will be deployed by selecting `Advanced Settings`.

- `Install Directory`: Existing absolute path on the MD Cluster Worker host where this instance will be installed. Leave empty to use the default path.
- `Temporary Directory`: Existing writable absolute path on the MD Cluster Worker host for MD Core temporary scan files. On Linux, the path can be up to 67 characters. Leave this field empty to use the default path. You can also use a [RAM disk](https://www.opswat.com/docs/mdcluster/knowledge-base).

Click `Next` to open the **Confirm & Deploy** step, review the selection, then click `Deploy` to start deploying on the selected MD Cluster Workers. The **Final Review** step shows the result; click `Finish` to return to the Workers list.

---

### [Assign Workflows to Instances](/docs/mdcluster/operating/operating-workers#assign-workflows-to-instances)

By default, a deployed MetaDefender Core instance processes files for every workflow. From the **Workers** page, you can restrict an instance to specific workflows, which is the same setting as **Assigned Instances** on the workflow itself. The **Workflows** column shows the workflows each instance is currently assigned to.

1. In the MetaDefender Core row, click the three-dot menu and select **Edit Workflows**.

2. On the **Add Workflow** page, check the instance details at the top of the page (ID, name, status, CPU, RAM, and platform) to confirm you are editing the right instance, then select the workflows to change.
3. Click **Add to Worker** to assign the selected workflows, or **Remove from Worker** to unassign them. The **Assigned Status** column shows the result for each workflow.

Only MetaDefender Core instances can be assigned to workflows, so **Edit Workflows** is disabled for the API Gateway, the Callback Service and the Download Service. Assignment requires MetaDefender Core 5.22.0 or later.

A MetaDefender Cluster Worker cannot be undeployed or deleted while workflows are assigned to it. Remove all workflow assignments first.

---

### [Release Instances](/docs/mdcluster/operating/operating-workers#release-instances)

To release MD Cluster API Gateway, MD Cluster Callback Service, or MetaDefender Core on MD Cluster Workers, the system administrator can select `Deploy Workers` > `Undeploy Workers` in the top right corner.

On the **Undeploy Workers** page, from the list of hosting MD Cluster Worker instances, the system administrator can choose instances to release MD Cluster API Gateway, MD Cluster Callback Service or MetaDefender Core.

When the `Undeploy` button is selected. MD Cluster API Gateway, MD Cluster Callback Service, and/or MetaDefender Core on selected MD Cluster Worker instances are uninstalled. Once uninstalled, the MD Cluster Worker instances will become available to deploy new MD Cluster API Gateway, MD Cluster Callback Service or MetaDefender Core.

---

### [Upgrade Instances](/docs/mdcluster/operating/operating-workers#upgrade-instances)

When a new version of MD Cluster API Gateway, MD Cluster Callback Service, Download Service or MetaDefender Core is available and the installers have been uploaded to the Installers section, the system administrator can upgrade them by selecting `Deploy Workers` > `Upgrade`.

The system administrator can then choose the new version of MD Cluster API Gateway, MD Cluster Callback Service and MetaDefender Core to perform the upgrade. **Upgraded at Once** sets how many workers of each type go offline and upgrade at the same time; 1 upgrades them one by one.

The new versions of MD Cluster API Gateway, MD Cluster Callback Service, or MetaDefender Core are streamed to the MD Cluster Workers and remote upgrade process will takes place automatically.

Info

If there are scans currently active, MetaDefender Core will isolate itself by no longer taking scan requests and finish its current scans before upgrading. **Upgraded at Once** controls how many instances of each type upgrade at the same time; keep it at 1 to upgrade them one at a time so scans are uninterrupted.
