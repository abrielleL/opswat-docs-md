<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-is-my-excel-document-not-showing-hidden-sheets-after-deep-cd -->

# Why is my Excel document not showing hidden sheets after Deep CDR sanitization?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

#### [Overview](/docs/mdcore/v5.22.1/knowledge-base/why-is-my-excel-document-not-showing-hidden-sheets-after-deep-cd#overview)

When processing Excel documents with OPSWAT MetaDefender Core Deep CDR (Content Disarm and Reconstruction), users may notice that **hidden sheets are missing** from the sanitized output. This behavior is expected and depends on both the file format and the **Deep CDR configuration** settings.

#### [Cause](/docs/mdcore/v5.22.1/knowledge-base/why-is-my-excel-document-not-showing-hidden-sheets-after-deep-cd#cause)

The Deep CDR engine currently supports the removal of hidden sheets only for Excel files in the .XLS format (legacy Excel format). During sanitization, hidden sheets in .XLS files are detected as embedded objects. When the configuration setting remove_embedded_object is enabled in the Excel section of the Deep CDR policy, these hidden sheets are automatically removed as part of the sanitization process.

This is done to ensure that no potentially malicious or hidden content remains in the file.

#### [Example](/docs/mdcore/v5.22.1/knowledge-base/why-is-my-excel-document-not-showing-hidden-sheets-after-deep-cd#example)

For example, if an .XLS file contains a hidden sheet, and the Deep CDR configuration has the default remove_embedded_object setting enabled, the hidden sheet will be removed from the sanitized file.

How to Keep Hidden Sheets

If you need to preserve hidden sheets during sanitization, you can modify the Deep CDR configuration:

- Open your Deep CDR configuration file or navigate to the Excel section in your MetaDefender Core policy settings.
- Locate the following setting: “"remove_embedded_object": true”

- Change it to: “"remove_embedded_object": false”

- Save the configuration and reprocess the file.

With this change, the Deep CDR engine will no longer remove hidden sheets, and they will be preserved in the sanitized output.

#### [Important Notes](/docs/mdcore/v5.22.1/knowledge-base/why-is-my-excel-document-not-showing-hidden-sheets-after-deep-cd#important-notes)

- This behavior applies only to **.XLS** files.
- For modern Excel formats such as .XLSX, hidden sheets are not currently modified or removed by the Deep CDR engine.
- Always ensure that disabling embedded object removal aligns with your organization’s security policy, as it may increase the risk of allowing hidden or embedded malicious content.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
