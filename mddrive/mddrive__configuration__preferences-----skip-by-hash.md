<!-- source: https://www.opswat.com/docs/mddrive/configuration/preferences-----skip-by-hash -->

# Preferences → Skip By Hash

**Skip by Hash** lets you exclude a specific file from being scanned on later runs, matched by its file hash rather than its name or path. In MetaDefender Drive 4.4.9, the list is managable from OPSWAT Central Management for a Drive enrolled to it — see [Manage MetaDefender Drives with OPSWAT Management](https://www.opswat.com/docs/mddrive/configuration/managing-drives-with-central-management) for enrollment details.

## [Add an entry](/docs/mddrive/configuration/preferences-----skip-by-hash#add-an-entry)

1. In OPSWAT Central Management, open the managed Drive's **Preferences** > **Skip by Hash**.
2. Click **Edit Settings**.
3. Click **Add**.
4. Enter the **File name**.
5. Enter the file's **SHA1** or **SHA256** hash.
6. Enter a **Reason** for skipping the file.
7. Click **Save**.

## [Field limits](/docs/mddrive/configuration/preferences-----skip-by-hash#field-limits)

| Field | Limit |
| --- | --- |
| File name | 255 characters |
| SHA1 hash | Exactly 40 hexadecimal characters |
| SHA256 hash | Exactly 64 hexadecimal characters |
| Reason | 30 characters |

## [Removing an entry](/docs/mddrive/configuration/preferences-----skip-by-hash#removing-an-entry)

Removing an entry from the list only affects scans run after the removal. A report already generated before the entry was removed keeps its original "Skipped by hash - <reason>" entry unchanged.

## [Import List of Hash](/docs/mddrive/configuration/preferences-----skip-by-hash#import-list-of-hash)

From version 4.4.10, administrator can import hash by a list. Refer to the document [Skip by Hash](/docs/mddrive/getting-started/skip-by-hash-using-dtk) to set it up.

The skipping hash can also be added remotely and centralized from Central Management. In Central Management, navigate to **Inventory → Devices → Settings → Skip by Hash** to add hash.
