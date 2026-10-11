<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/why-am-i-getting--the-stream-does-not-support-concurrent-io-read -->

# Why am I getting "The stream does not support concurrent IO read or write operations" during file uploads to MetaDefender Core?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version:

This article applies to all MFT versions.

**Issue:**

The error message “The stream does not support concurrent IO read or write operations” may appear during file uploads from Vault MFT. The issue is typically related to insufficient disk space on the MD Core installation drive, and not an issue with Vault’s streaming logic.

## [Process background:](/docs/mdmft/v3.11.5/knowledge-base/why-am-i-getting--the-stream-does-not-support-concurrent-io-read#process-background)

When a file is submitted to MFT, it is then sent to MD Core via a REST API. MFT sends simultaneous HTTP requests to MD Core for analysis and retrieval.

example logs from MD Core nginx:

"POST /file HTTP/1.1" 200 82 "batch_id:-" "data_id:be703c0b6cf8465cac5344e791febd01" "-" "-" 0.025 "GET /file/be703c0b6cf8465cac5344e791febd01 HTTP/1.1" 200 1284 "-" "-" 0.019 "GET /file/be703c0b6cf8465cac5344e791febd01 HTTP/1.1" 200 3048 "-" "-" 0.028 "GET /file/be703c0b6cf8465cac5344e791febd01 HTTP/1.1" 200 3048 "-" "-" 0.038 "GET /file/converted/be703c0b6cf8465cac5344e791febd01 HTTP/1.1" 200 13473 "-" "-" 0.010

During the scanning process from MD Core, it creates temporary `.tmp` files in its Resources or Temp directory. These files are required for deep analysis and sanitization.

The screenshot below illustrates the behavior observed in the Resources folder after uploading a 10GB archive file through MFT.

If the MD Core installation drive (for example, `E:\`) runs out of available space:

- MD Core cannot allocate additional temporary storage.
- The scanning process fails.
- The MFT will display the error message

ERROR Core Server VAULT IP set to unavailable because The stream does not support concurrent IO read or write operations.

**Resolution:**

Refer to the following articles for guidance on freeing up space on the installation disk or changing the temporary folder location to a drive with more available storage for processing temporary files:

- How can the Temp folder be changed? This article provides steps to reconfigure the temporary directory used by MetaDefender Core to a different location with sufficient disk space: <https://www.opswat.com/docs/mdcore/v5.9.0/knowledge-base/how-can-the-temp-folder-be-changed->
- What can I do when MetaDefender Core (Windows) has an insufficient disk space error? This article outlines methods to identify and resolve disk space issues impacting MetaDefender Core performance: <https://www.opswat.com/docs/mdcore/knowledge-base/what-can-i-do-when-metadefender-core--windows--has-an-insufficie>
