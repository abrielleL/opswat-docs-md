<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files- -->

# How does the MD Core Handle Archive Files?

This article applies to all MD Core versions.

### [**Overview:**](/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files-#overview)

When an archive file (such as .zip or .7z) contains child files (like Word documents, PDFs, or images), MD Core extracts the archive file, and while the parent file is being extracted, the child files are processed in parallel. After all child files have been extracted and processed, MD Core then processes the parent file with the other engines

### [**Process steps: File intake & initial inspection (MD Core)**](/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files-#process-steps-file-intake--initial-inspection-md-core)

- The archive file is ingested by MD Core for initial validation.
- Basic metadata, headers, and file signatures are verified to ensure the archive is valid and not corrupted.

### [**File Type Detection (FileType Engine)**](/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files-#file-type-detection-filetype-engine)

- The FileType Engine determines the archive type (e.g., .zip, .7z, .rar).
- This step helps prevent spoofing attacks where malicious files disguise themselves as harmless archives.

### [**Archive Extraction (Archive Extraction Engine)**](/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files-#archive-extraction-archive-extraction-engine)

- The archive is extracted to access its contents.
- If the archive contains child files (such as .docx or .pdf), these files are treated as individual items.
- For complex document formats (like Office files), note:

  - Office files (.docx, .xlsx, .pptx) are ZIP-based containers with XML and media files inside.
  - The Archive Extraction Engine extracts the container structure and files. Analyzing internal elements like macros, embedded objects, or external links is handled by the Deep CDR engine (and FSV in the future).
- If extraction fails or exceeds configured limits (e.g., file count, recursion depth), the file is blocked without further scanning.

### [**Scanning Child Files (Layered Analysis)**](/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files-#scanning-child-files-layered-analysis)

After extraction, each child file is scanned independently. The following engines are processed sequentially in this order:

- Multiscan (Antivirus Engines): Scans each file for known malware signatures and suspicious patterns.
- Data Loss Prevention (DLP): Identifies sensitive or confidential data (such as credit card numbers or personal IDs).
- Deep Content Disarm & Reconstruction (Deep CDR):

  - Removes potential threats from documents and PDFs.
  - Generates a safe, rebuilt version of the file, free from harmful elements.
- Recursive scanning: If a child file is another archive or container file (e.g., a ZIP inside a ZIP), the engine repeats the extraction and scanning process until the configured recursion limit is reached.

Note:

*DLP moves before Deep CDR to match the actual processing order.*

### [**Recompression & Final Output**](/docs/mdcore/v5.21.0/knowledge-base/how-does-the-md-core-handle-archive-files-#recompression--final-output)

After all child files are scanned, cleaned, or blocked, the remaining clean files are:

- Recompressed back into an archive (if necessary).
- Delivered individually, depending on system settings.
- MD Core generates a final result, including scan logs and detailed threat reports.

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
