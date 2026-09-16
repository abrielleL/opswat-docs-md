<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-handle-split-archive-files- -->

# How to handle split archive files?

A **split archive file** is a compressed file that has been divided into multiple smaller parts, typically to simplify storage, sharing, or transfer of large data sets. These files usually follow a naming convention such as `.001`, `.002`, and so on. Each part contains a portion of the original data.

Some archive formats store metadata in each individual part, allowing partial extraction. However, others store metadata only in the first part (e.g., `.001`), meaning the remaining parts cannot be extracted independently.

The **Archive Extraction** module attempts to extract as much data as possible and passes the extracted content through a scanning process to ensure maximum security. However, due to the nature of split archives, the extraction process often results in outcomes like **“Partially Extracted”** or **“Corrupted Archive.”**

**What can customers do with split archive files?**

- If customers prefer not to have these files blocked under such conditions, they should avoid enabling specific options in the **Archive Extraction** tab within the workflow configuration.

- The [multipart upload API](/docs/mdcore/v5.22.0/integration/multipart-uploading-guideline#multipart-upload-and-other-facilities)works in some file types, such as zip and 7z, but not with all split archive file types (rar, …). This API concatenates the split files by appending their data, without properly reconstructing the archive structure. A proper combination of split archives requires dedicated extraction tools such as **7-Zip**, **WinRAR**, or similar. We recommend that all parts of a split archive be combined on the client side before being sent to MetaDefender Core. This ensures that the archive engine can properly extract the contents, and the scan process is applied to the complete file.
- If this approach is not feasible, customers may choose to **block split archives and investigate them manually at a later time**. This can be configured using the **Blocklist** option within a workflow.

- It is not suggested, but if customers want to skip the extraction for the split archive, please use this configuration in the Modules > Utilities> Archive extraction

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
