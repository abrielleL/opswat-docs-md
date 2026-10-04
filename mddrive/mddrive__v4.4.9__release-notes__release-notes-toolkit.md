<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/release-notes/release-notes-toolkit -->

# MetaDefender Drive Toolkit v3.8.9

|  |  |
| --- | --- |
| **Released on** **Sep 03, 2026** | This release includes improvements, bug fixes. |

**Improvements and Bug Fixes**

- With "remove report after synced" enabled, report files and their artifacts are cleared from the drive once synchronization completes, rather than accumulating in the report folder.

- Engine updates in MetaDefender Drive Toolkit no longer lose the existing backup and fail partway through copying, and each module is named while it is still downloading.
- Flashing several MetaDefender Drives in one session preserves each drive's stored scan hashes and logs, instead of silently discarding them when another drive is imaged at the same time.
- Starting MetaDefender Drive Toolkit no longer raises a command prompt window full of graphics errors, on any machine it is installed on.
- Drive Toolkit reports why a partition resize failed and retries the mount point rather than leaving the flash in an unusable state.
