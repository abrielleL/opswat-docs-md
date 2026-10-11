<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-do-i-deploy-metadefender-core-to-an-offline-windows-envir -->

# How do I deploy MetaDefender Core to an offline Windows environment?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed in offline Windows environments.

Pro Tip:

MetaDefender Core supports deployment in either online or offline environments.

There are four steps to getting the product up and running in an offline environment:

1. **Install MetaDefender Core on the offline server.**
2. **Activate your license.**
3. **Install and configure the MetaDefender Update Downloader utility.**
4. **Apply the offline updates that are downloaded by the update utility to the offline MetaDefender Core server.**

## [A. Installing MetaDefender Core](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-deploy-metadefender-core-to-an-offline-windows-envir#a-installing-metadefender-core)

Please Note:

The MetaDefender Core installation packages can be downloaded from [My OPSWAT](https://my.opswat.com/home/metadefender-core).

1. After logging into the portal, go to the Downloads page to select the MetaDefender Core package you wish to download.
2. The supported platforms include Windows 7 and later releases.
3. Download the appropriate installer and run it on the Windows system:

## [B. Activating your license](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-deploy-metadefender-core-to-an-offline-windows-envir#b-activating-your-license)

**After MetaDefender Core is installed, you will need to activate your MetaDefender Core installation:**

1. Log in to your MetaDefender Core **Management Console** at <http://localhost:8008/>. Complete the required steps of the [Basic Configuration Wizard](/docs/mdcore/v5.22.1/installation/initial-setup-using-configuration-wizard).
2. Go to **Settings > License > Activate > Offline**.
3. Here, you can follow the steps to:

   1. Copy your **Deployment ID** to the clipboard, then open a new browser tab.
   2. Log in to the [My OPSWAT](https://my.opswat.com/license-management/my-organization) and navigate to the **License Management** page and click on **Activate License** button on the top right.
   3. Fill in the required details to retrieve your **Activation File**.

d. Return to the Management Console to upload your **Activation File.**

e. Finally, **Activate** your license, as shown in the screenshots below.

## [C. Installing the MetaDefender Update Downloader utility](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-deploy-metadefender-core-to-an-offline-windows-envir#c-installing-the-metadefender-update-downloader-utility)

Please Note:

If your MetaDefender Core server is deployed offline, you will need to install the **Update Downloader** utility to download the anti-malware definition updates to be applied to the server.

You can download the **Downloader** utility from [My OPSWAT](https://my.opswat.com/home/metadefender-core) under **Modules & Utilities**.

**Once you have installed the Update Downloader, apply your license key to activate the product:**

1. Log into the **Update Downloader Management Console at http://<server>:8028/**.

2. Add your product on the **Inventory** page, **Product** tab.

3. Update the configuration for update download and package generation on the **Settings** page of the **Management Console.**

## [D. Applying offline updates](/docs/mdcore/v5.22.1/knowledge-base/how-do-i-deploy-metadefender-core-to-an-offline-windows-envir#d-applying-offline-updates)

**Once the update packages have been downloaded, you can apply them to the offline MetaDefender Core server through the MetaDefender Core Management Console:**

1. Copy all of the update packages from the directory where the **Update Downloader** saves the updates, to the offline MetaDefender Core system.
2. Upload the updated packages through the MetaDefender Core **Management Console**.

3. To save the update packages, select the engine update packages from the directory where the **Update Downloader** is configured.

Support:

If you have any difficulty setting up MetaDefender Core in an offline Windows environment, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
