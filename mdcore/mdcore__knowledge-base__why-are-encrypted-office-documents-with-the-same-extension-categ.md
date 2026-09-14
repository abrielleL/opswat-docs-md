<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-are-encrypted-office-documents-with-the-same-extension-categ -->

# Why are Encrypted Office Documents with the same extension categorized differently from unencrypted documents?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**Question:**

MetaDefender Core categorizes Office documents with the same extension (.docx, .xlsx, etc.) differently.

Some are identified as "Encrypted Microsoft Office Document," while others are identified as "Microsoft Excel Workbook" or "Encrypted Microsoft Excel Sheet." This article aims to provide clarifications about the logic behind this categorization.

**Clarification:**

MetaDefender Core detects encrypted Microsoft Office files differently based on their encryption type and file format version. Here's a breakdown, using Microsoft Excel document as an example:

- **Unencrypted and non-password-protected .xlsx** files are detected as "Microsoft Excel Workbook."
- **Encrypted .xlsx** files are detected as "Encrypted Microsoft Office Document" due to password protection or Microsoft Office Document Information Protection.

  - In MS Office 2007 and later (docx, xlsx, pptx): encrypted files share the **same structure** across Word, Excel, and PowerPoint, so the general term “Encrypted Microsoft Office Document” is used.
  - For more information on this file type, please refer to [Can MetaDefender Core process Microsoft Purview Information Protection Encrypted Files?](https://www.opswat.com/docs/mdcore/knowledge-base/can-metadefender-core-process-microsoft-purview-information-prot)
- **Older encrypted Excel files .xls** are detected as "Encrypted Microsoft Excel Sheet."

  - In MS Office 2003 (doc, xls, ppt): encrypted files have **distinct structures** for Word, Excel, and PowerPoint, so file type engine can clearly return “Encrypted Microsoft Excel Sheet.”

**Action Required:**

No action or configuration change is required on the user's side, as this is the expected behavior of MetaDefender Core.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
