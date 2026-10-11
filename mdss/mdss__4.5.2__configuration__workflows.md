<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/workflows -->

# Workflows

Workflows are configurable processing pipelines that define how files should be scanned, analyzed, and remediated. A workflow is required to be able to start a new scan with a specified set of rules. Each workflow consists of a set of remediation actions.

Remediation actions are automated post-processing tasks performed on files after they have been scanned. The following remediation options are currently available:

| Name | Description | Documentation |
| ---- | ---- | ---- |
| File Tagging | Adds metadata tags to files in S3-like storage units, providing processing information. | [File Tagging](https://www.opswat.com/docs/mdss/configuration/file-tagging) |
| Deep CDR | Applies OPSWAT’s Deep CDR (file sanitization) technology to files. | [Deep Content Disarm and Reconstruction (Deep CDR)](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-) |
| Keep, copy, move or delete | Keeps, copies, moves or deletes files based on configured rules, such as blocked or sanitized status. | [Keep, Copy, Move or Delete Files](https://www.opswat.com/docs/mdss/configuration/keep-or-move-or-copy-or-delete-files) |
| Other remediations | Delete a directory if it is empty after remediation (does not delete if the folder was empty to begin with). | [Delete Empty Folders](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders) |

> **REMEDIATION ACTION PROCESSING ORDER**
>
> The following order is used when applying remediation actions:
>
> 1. File Tagging
> 2. Sanitized Files (Deep CDR, Move or Delete)
> 3. Blocked Files (Keep, Copy, Move or Delete)
> 4. Allowed Files (Keep, Copy, Move or Delete)

> **NOTE**
>
> If you require a post-processing action not listed above, please [let us know](https://www.opswat.com/support/contact-support).
>
> We may be able to add it in a future update.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
