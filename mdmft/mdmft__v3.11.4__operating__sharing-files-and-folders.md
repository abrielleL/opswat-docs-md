<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/operating/sharing-files-and-folders -->

# Sharing Files and Folders

Summarize Page    Connect to Cursor Connect to VS Code

This document outlines the features and steps for sharing files and folders with users, guest users, and groups. The sharing functionality supports single-item sharing as well as bulk operations for multiple files or folders.

## [Key Features](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#key-features)

1. Single File/Folder Sharing

   1. Share a single file or folder with a specific user, guest user, or group.
2. Bulk Sharing

   1. Share multiple files or folders simultaneously to streamline workflows.
3. Share Targets

   - Users**:** Internal users with registered accounts in your organization.
   - Guest Users**:** External users with limited access permissions.
   - Groups**:** Collections of users to simplify sharing with multiple recipients.
4. Share Roles

   1. Downloader
   2. Editor
   3. Uploader
   4. Viewer

## [Share Role permissions](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#share-role-permissions)

### [File](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#file)

| Actions | Editor | Downloader | Viewer | Uploader |
| --- | --- | --- | --- | --- |
| Preview |  |  |  |  |
| Download |  |  |  |  |
| Add/Remove password |  |  |  |  |
| Share |  |  |  |  |
| Rename |  |  |  |  |
| Move* |  |  |  |  |
| Edit tags |  |  |  |  |
| Delete** |  |  |  |  |

### [Folder](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#folder)

| Actions | Editor | Downloader | Viewer | Uploader |
| --- | --- | --- | --- | --- |
| View content |  |  |  |  |
| Download |  |  |  |  |
| Upload*** |  |  |  |  |
| Create folder |  |  |  |  |
| Share |  |  |  |  |
| Rename |  |  |  |  |
| Move* |  |  |  |  |
| Delete** |  |  |  |  |

Info

*Can move only to folders which belongs to the same user as the item(s) to be moved.

**Deleted files will be moved into trash bin of owner.

***The owner of the uploaded files will be the user who shared the folder.

Info

When upgrading from versions that don’t support 'Share Roles', all shares will be assigned the 'Downloader' role by default.

## [Sharing Methods](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#sharing-methods)

### [Single File/Folder Sharing](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#single-filefolder-sharing)

**Steps:**

1. Locate the file or folder in "My Files."

2. Right-click the item and select "Share" from the context menu or "More Actions(...)."

Context Menu

More Actions Menu

3. In the sharing dialog, enter the recipient(s):

   1. Type the name or group name in the appropriate field.
   2. Select from the dropdown suggestions or manually input the recipient details.
   3. Add some optional message for the recipients.
   4. Select 'Share Role'.

4. Click "Save" to complete the process. The outcome will be communicated with a toast notification. If the notification function is enabled in the MetaDefender® MFT, the recipients with a registered e-mail address will get an e-mail notification about the sharing, which will contain the given message.

---

### [Bulk Sharing](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#bulk-sharing)

**Steps:**

1. Select multiple files or folders by clicking the checkbox next to each item.

2. Right-click on the selection and choose "Share" or use the share option in the toolbar.

3. In the sharing dialog, enter the recipient(s), add optional message and select 'Share Role' as described above.

4. Confirm and click "Save" to complete the operation.

---

## [Managing Shared Files/Folders](/docs/mdmft/v3.11.4/operating/sharing-files-and-folders#managing-shared-filesfolders)

After sharing, you can manage access at any time:

1. View Shared Items**:**

   - Check the "Sharing" column in "My Files" to see if an item is marked as "Private" or "Shared."
   - Sharing a folder automatically marks all its contents as shared.
2. Stop Sharing**:**

   - Open "Share" on the proper file or folder, and click on 'Remove Access' to revoke access from all users/groups or click on the right chevron icon to open the detailed access control modal.
   - After managing users' or groups' access click on the back arrow.
   - Finally click on 'Save' to complete the operation.

Example: revoke all access

Example: the access for a user will be removed.

Example: the access is changed to 'Editor'.
