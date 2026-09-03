<!-- source: https://www.opswat.com/docs/mdmft/operating/recycle-bin -->

# Trash

Summarize Page    Connect to Cursor Connect to VS Code

The Trash allows administrators to recover deleted files, permanently delete files, download files, and empty the bin.

**Read Only Administrators** can view files in the Trash but cannot restore or delete files permanently, except their own.

**Regular users** (including guests and external users) can restore and download their own available files. Administrators can configure whether users are allowed to permanently delete files.

### [Retention Period](/docs/mdmft/operating/recycle-bin#retention-period)

Files stored in the Trash for longer than the retention period are automatically deleted.

The default retention period is 30 days, but administrators can adjust this value.

### [Configuration](/docs/mdmft/operating/recycle-bin#configuration)

Administrators can:

- configure the retention period
- allow/deny users the ability to permanently delete files

These options are accessible by clicking the "Configure" button located on the "Trash" page.

### [Actions](/docs/mdmft/operating/recycle-bin#actions)

#### [Emptying the Bin](/docs/mdmft/operating/recycle-bin#emptying-the-bin)

Administrators can permanently delete all files by clicking the "Empty Trash" button. A confirmation popup will appear.

Warning

This action is *irreversible* and may lead to data loss. Use with caution.

Info

Only authorized users can empty the Trash with their own content.

#### [Restoring Files](/docs/mdmft/operating/recycle-bin#restoring-files)

Clicking the "Restore File" action allows users to recover files while maintaining the folder hierarchy. Users can restore only their own files. File restorations that would result in file name duplicates in their corresponding parent folders are declined.

Files owned by deleted users cannot be recovered. The system will display an error message that the owner is no longer available.

#### [Downloading Files](/docs/mdmft/operating/recycle-bin#downloading-files)

Administrators can download files by clicking the "Download File" action. This option is available even for files whose owners have been deleted.

Users can only download their own available files. Blocked or unsupervised files are restricted.

Warning

"Bulk downloads" are not supported yet. Files must be downloaded one at a time.
