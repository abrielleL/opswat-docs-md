<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/knowledge-base/can-i-delete-modify-the-source-engine-folder-of-metadefender-upd -->

# Can I delete/modify the source engine folder of MetaDefender Update Downloader?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to **MetaDefender Update Downloader** deployment on **Windows** and **Linux** environment.

With Post Actions, this feature is only available since **Update Downloader version 2.5.0**.

## [Overview](/docs/mddownloader/v3.5.0/knowledge-base/can-i-delete-modify-the-source-engine-folder-of-metadefender-upd#overview)

This article addresses whether it is acceptable to configure an external transfer agent (such as a Data Diode) to delete files from the MetaDefender Update Downloader source directory immediately after transferring them to a secure zone.

## [Recommended Configuration](/docs/mddownloader/v3.5.0/knowledge-base/can-i-delete-modify-the-source-engine-folder-of-metadefender-upd#recommended-configuration)

The recommended way is to **not remove files from the source folder.**

The MetaDefender Update Downloader relies on the presence of existing files to track for incremental updates. If these files are deleted externally:

- The Update Downloader cannot track the deletion, leading to potential conflicts.
- The system will be forced to perform a **full re-download** of the entire database during every cycle, causing significant bandwidth usage and operational delays.

## [Workaround](/docs/mddownloader/v3.5.0/knowledge-base/can-i-delete-modify-the-source-engine-folder-of-metadefender-upd#workaround)

If your architecture requires the transfer agent to delete files after ingestion (common with **Data Diodes**), you should decouple the download process from the transfer process using **Post Actions**.

Instead of the Data Diode picking up files directly from the Download folder, configure the Update Downloader to copy the files to a secondary "Staging Folder" automatically.

### [Steps:](/docs/mddownloader/v3.5.0/knowledge-base/can-i-delete-modify-the-source-engine-folder-of-metadefender-upd#steps)

1. **Create a Seperated Folder:** Create a separate directory for the Data Diode to monitor.
2. **Configure Post Actions:** Use the MetaDefender Update Downloader **Post Actions** feature to trigger a script that copies the content from the Download folder to the Staging Folder.
3. **Configure Data Diode:** Point the Data Diode to the **Seperated Folder**. It can now safely ingest and delete files from this location without affecting the Update Downloader.

For detailed instructions on configuring this feature, please refer to our documentation:

- [**Post Actions - MetaDefender Update Downloader**](https://www.opswat.com/docs/mddownloader/operating/post-actions)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
