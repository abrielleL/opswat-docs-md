<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/configuration/preferences-----skip-by-hash -->

# Preferences → Skip By Hash

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The **Skip by Hash** feature enables you to exclude a specific file from subsequent scans, identified by its file hash, rather than its name or path. In MetaDefender Drive 4.4.9, the list can be managed from OPSWAT Central Management for any enrolled MetaDefender Drive. See [Manage MetaDefender Drives with OPSWAT Management](https://www.opswat.com/docs/mddrive/configuration/managing-drives-with-central-management) for enrollment instructions.

## [Add an entry](/docs/mddrive/v4.4.9/configuration/preferences-----skip-by-hash#add-an-entry)

1. Navigate to **Preferences** > **Skip by Hash**.
2. Click **Edit Settings**.
3. Click **Add**.
4. Enter the **File name**.
5. Enter the file's **SHA1** or **SHA256** hash.
6. Enter a **Reason** for skipping the file.
7. Click **Save**.

## [Field limits](/docs/mddrive/v4.4.9/configuration/preferences-----skip-by-hash#field-limits)

| Field | Limit |
| --- | --- |
| File name | 255 characters |
| SHA1 hash | Exactly 40 hexadecimal characters |
| SHA256 hash | Exactly 64 hexadecimal characters |
| Reason | 30 characters |

## [Removing an entry](/docs/mddrive/v4.4.9/configuration/preferences-----skip-by-hash#removing-an-entry)

Removing an entry from the list only affects scans run after the removal. A report already generated before the entry was removed keeps its original "Skipped by hash - <reason>" entry unchanged.

Info

In 4.4.9, entries are added and removed one at a time from this list. Bulk import and adding a hash directly from a scan report are planned on a later version.
