<!-- source: https://www.opswat.com/docs/mdces3/knowledge-base/scanning-limits -->

# Scanning limits

Summarize Page

**MetaDefender** **Cloud Email Security**™ is designed to provide robust protection against email-borne threats by analyzing attachments using advanced engines. To maintain optimal performance, reliability, and resource allocation, the platform enforces specific scanning limits on files (attachments) and archives.

This article explains each of the current file scanning limitations.

| Parameter | Value | Description |
| --- | --- | --- |
| **Max file size** | 256MB | This is the maximum size of a single file that can be uploaded and scanned. |
| **Max archive file size** | 256MB | The total size of an archive (e.g., .zip, .rar) after decompression must not exceed this limit. |
| **Max archive depth** | 25 | This limits how deeply nested an archive can be. For example, an archive within an archive counts as one depth level. |
| **Max archive files** | 10,000 | The maximum number of files that can be extracted and scanned from an archive. |

### [Engine file type support](/docs/mdces3/knowledge-base/scanning-limits#engine-file-type-support)

Certain antivirus engines specialize in scanning only particular file types, ignoring others. The table below identifies each engine and its corresponding supported file types.

| Engine | File types |
| --- | --- |
| **OPSWAT Predictive Alin AI** | PE & PDF documents |
| **OPSWAT MetaDefender Aether** | Productivity files (PDF, Office etc.) |
| **RocketCyber** | Any windows file that contains a PE header. That would include the file format for Windows executables, object code, and DLLs in both 32-bit and 64-bit versions. |
| **Webroot SMD** | PE and JS embedded on PDF |

Info

Other antivirus engines, beyond those listed above, can scan all file types without restrictions.
