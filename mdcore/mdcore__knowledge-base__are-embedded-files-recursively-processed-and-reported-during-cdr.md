<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/are-embedded-files-recursively-processed-and-reported-during-cdr -->

# Are Embedded Files Recursively Processed and Reported during CDR?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

> ### [**Summary:**](/docs/mdcore/knowledge-base/are-embedded-files-recursively-processed-and-reported-during-cdr#summary)
>
> This article explains how MetaDefender Core handles recursive processing and reporting when Content Disarm and Reconstruction (CDR) is enabled. It clarifies how embedded or internal files within a processed file are processed and displayed in the scan history.

### [**Issue**](/docs/mdcore/knowledge-base/are-embedded-files-recursively-processed-and-reported-during-cdr#issue)

During a CDR-enabled process, a file may contain other embedded or internal objects (for example, documents within archives, or images containing embedded files). It may be unclear whether these extracted components are also processed by CDR and whether the results are shown in the scan report.

### [**Cause**](/docs/mdcore/knowledge-base/are-embedded-files-recursively-processed-and-reported-during-cdr#cause)

While CDR can reconstruct and sanitize embedded content, recursive sanitization and detailed reporting depend on configuration settings and supported file types. If certain options are disabled, internal or embedded files may not be sanitized or reported individually.

### [**Resolution**](/docs/mdcore/knowledge-base/are-embedded-files-recursively-processed-and-reported-during-cdr#resolution)

To ensure that embedded or internal files are recursively processed and reported during CDR processing:

1. **Enable Recursive Scanning for Embedded File Types** Verify that recursion of embedded file types is enabled in the configuration. This allows CDR to sanitize internal files..
2. **Enable Detailed Sanitization Reporting** Turn on the **“Include Sanitisation Details / Processed Objects”** option. This ensures that the scan history includes detailed information about the sanitization actions and results of internal components.
3. **Confirm Supported File Types** Make sure the file types being processed support recursive scanning and sanitization. Some formats may not support deep recursion or detailed reporting. If a file type is not supported, CDR will act based on the “Remove embedded object” configuration to decide whether to remove the embedded file or not

When all of these settings are correctly configured, the CDR process will:

- Recursively scan embedded or internal files.
- Include the results and sanitization details of those components in the scan history report.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
