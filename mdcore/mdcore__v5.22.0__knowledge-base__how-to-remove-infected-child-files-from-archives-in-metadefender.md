<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-remove-infected-child-files-from-archives-in-metadefender -->

# How to Remove Infected Child Files from Archives in MetaDefender Core

Use case

Core scans an archive or container file, and one or more of the child files inside the archive are detected as infected. The desired result is to return a modified archive where the infected child file has been removed, rather than returning the original archive with the infected child file(s) sanitized.

Resolution

To remove infected child files from an archive, configure the workflow’s Compression and Deep CDR settings:

| Workflow area | Setting | Value |
| --- | --- | --- |
| Deep CDR | Enable Deep CDR | Status: Active |
| Compression | Enable archive sanitization | Enabled |
| Compression | Enable for archive compression filetypes | Select the required archive/container types |
| Compression | Skip Malicious Items | Enabled; configure the verdicts that should be treated as malicious |
| Compression | Include sanitized version of blocked child files | Disabled |
| Compression | Add tombstone file during archive process / archive sanitization | Optional, recommended for keeping track of infected files |
| Deep CDR | Enable for filetypes | Optional: enable for supported child file types if clean child files should be sanitized |
