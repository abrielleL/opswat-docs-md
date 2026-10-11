<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-does-metadefender-kiosk-do-file-type-detection- -->

# How does MetaDefender Kiosk perform File Type detection?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows or Linux systems.

## [Overview](/docs/mdkiosk/v4.8.6/knowledge-base/how-does-metadefender-kiosk-do-file-type-detection-#overview)

One of the key capabilities of MetaDefender Kiosk is **advanced file type detection**, also known as **file type analysis**/**file mismatch analysis**. This feature helps identify discrepancies between a file's true type and its extension, ensuring only trusted file types are processed.

File type detection in Kiosk is powered by its integration with **MetaDefender Core**, meaning the actual file type detection is done on the **MetaDefender Core** side.

---

## [Enabling File Type Detection](/docs/mdkiosk/v4.8.6/knowledge-base/how-does-metadefender-kiosk-do-file-type-detection-#enabling-file-type-detection)

To use file type detection, you need to ensure the engine is enabled in MetaDefender Core Modules as well as the Workflow used by the Kiosk.

### [Step 1: Configure File Type Detection in MetaDefender Core](/docs/mdkiosk/v4.8.6/knowledge-base/how-does-metadefender-kiosk-do-file-type-detection-#step-1-configure-file-type-detection-in-metadefender-core)

1. Open the **Core Management Console**.
2. Go to **Inventory > Modules > Utilities**
3. Make sure the Filetype engine is enabled and successfully deployed.
4. Navigate to Workflow Management > Workflows > [The Workflow that will be used on Kiosk]
5. Navigate to the **File Type** tab.
6. Make any necessary changes or enable detection settings as needed (e.g, “Detect FileType Mismatch“).

### [Step 2: Enable the configured workflow in MetaDefender Kiosk](/docs/mdkiosk/v4.8.6/knowledge-base/how-does-metadefender-kiosk-do-file-type-detection-#step-2-enable-the-configured-workflow-in-metadefender-kiosk)

1. Open the **Kiosk Management Console**.
2. Navigate to the **Workflows** tab.
3. Click the **edit icon** next to the workflow you want to configure.
4. Under the **Processing > Workflow** section, assign a Core workflow that has file type detection enabled (configured via Core).

### [**Note:**](/docs/mdkiosk/v4.8.6/knowledge-base/how-does-metadefender-kiosk-do-file-type-detection-#note)

The **“Extensions to block”** setting, located under **Kiosk Console > Workflows > [Your Workflow] > Processing**, only evaluates the literal file extension in the filename (e.g., `.exe`, `.bat`). Kiosk does not perform true file type detection at the file selection stage; this analysis is carried out later by the **FileType engine** during processing on **MD Core**.

Pro Tip:

For the full list of 4500+ file-types supported by MetaDefender Core’s file-type detection feature, please [Read This Article](https://docs.opswat.com/mdcore/utilities-engines/filetype-supported-file-types)

Support:

If you have any difficulty **Configuring and Assigning Workflows to Enable Kiosk’s File-Type Detection Feature**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
