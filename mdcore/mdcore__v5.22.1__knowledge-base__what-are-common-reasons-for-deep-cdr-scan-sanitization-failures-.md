<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-are-common-reasons-for-deep-cdr-scan-sanitization-failures- -->

# What are common reasons for Deep CDR scan/sanitization failures and how do I fix them?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Please Note:

In order to function, MetaDefender Core’s **Deep Content Disarm and Reconstruction** feature (Deep CDR) must be:

- included under your unique license key
- enabled via **MetaDefender Core Management Console>Inventory>Modules>Deep CDR**
- fully downloaded (engine and current database)
- listed as **Active** instead of **Inactive** as it is in the screenshot below.

Once these conditions are met, you should be ready to run all supported file types through MetaDefender’s Deep CDR engine as part of your chosen Workflow. If not, and if one or more of your deep CDR scans fail, this is likely due to one of the following:

**You are attempting to process a supported file type, but the version is outdated:**

- For example, CDR is unable to process an Office file format created before MS Office 97 or a DWG file created with AutoCAD before version 2004.

**You are attempting to process an invalid file structure:**

Files that have become corrupted (damaged and unreadable) by hardware or software malfunctions or by attackers, these files will be blocked by MetaDefender Core, but they cannot be sanitized by Deep CDR. Read [here](/docs/mdcore/v5.22.1/deep-cdr/troubleshooting-sanitization-failures) for more information.

When retrieving your scan results via REST API, Deep CDR sanitization failures will be clearly classified under the **post_processing** section in your JSON output, as illustrated in the screenshot below.

**File processing has exceeded your configured settings for Deep CDR:**

- Go to your **Core Management Console>Workflow Management>{Relevant Workflow}>Deep CDR** to configure settings such as Deep CDR, sanitization and encryption timeouts, illustrated in the screenshot below.

Always be sure to click **Save changes** before exiting the Workflow.

**You are attempting to process a password-protected file:**

- When a file is password protected or no active archive compression engine supports the encryption found, the file cannot be opened and will therefore not be sanitized by Deep CDR.

**Other, unknown reasons:**

- If unspecified failures occur, please reach out to the OPSWAT support team by following the instructions at the end of this article.

Support:

If you have followed the relevant instructions above but are still having difficulty **Scanning and Sanitizing Files With Deep CDR**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
