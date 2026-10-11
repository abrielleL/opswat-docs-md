<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/what-is-a-remediated-file---kiosk- -->

# What does Remediated File mean in MetaDefender Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows or Linux systems.

A remediated file is any file that has been processed by MetaDefender Kiosk to remove hidden (and possibly malicious) content, including embedded objects and potential exploits or redact sensitive information, while preserving the visible contents of the file.

The remediated file will maintain its original file format and extension, unless the Kiosk (and MetaDefender Core) has been explicitly set up to convert suspicious files to another format as part of the sanitization process.

For example, a remediated PDF will maintain the PDF format and extension, and will be accessible by a PDF reader.

Some of the actions performed as part of remediation include:

## [Sanitization](/docs/mdkiosk/v4.8.6/knowledge-base/what-is-a-remediated-file---kiosk-#sanitization)

- Removal of all attachments and document action
- Removal of all annotations
- Removal of JavaScript from other scripts within the document
- Making any form fields present in PDF files uneditable and inaccessible, so that the user cannot update values within the file
- Removal of all hyperlinks.

## [Redaction](/docs/mdkiosk/v4.8.6/knowledge-base/what-is-a-remediated-file---kiosk-#redaction)

- Redact/Substitution sensitive information
- Watermark files

MetaDefender Kiosk supports remediation for many of the most common document file types. Should you have a requirement for a file type that is not currently supported by the Kiosk, please follow the instructions below to contact support.

Although we cannot make any commitments regarding inclusion of a suggested file type, we are always striving to include new, commonly used file types to better meet the needs of our customers.

Support:

If you have any issue regarding the **File Remediation in MetaDefender Kiosk**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
