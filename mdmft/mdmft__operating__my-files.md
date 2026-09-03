<!-- source: https://www.opswat.com/docs/mdmft/operating/my-files -->

# My Files

Summarize Page    Connect to Cursor Connect to VS Code

The "My Files" page allows users to view and manage files they've uploaded in MetaDefender Managed File Transfer.

### [Available Actions on the "My Files" Page](/docs/mdmft/operating/my-files#available-actions-on-the-my-files-page)

- Create folders by clicking on "New folder"
- Download multiple folders and files
- Move multiple folders and files
- Delete multiple folders and files
- Select all files and folders
- Copy the download link for files or folders
- Refresh the page
- Edit file tags
- Edit password
- Delete password
- Retry processing (available only in case of failures)
- Sort files
- Search by name or tag
- Toggle column visibility
- Preview files
- Rename files

Users can select individual files for re-scanning using the actions menu in the right column:

Users can download individual files or folders on the "My Files" or "Shared with me" pages using the actions menu in the right column:

Info

When downloading multiple files, the sanitized version will be selected automatically if available. The option to download the original file is available only for individual files through the administrator.

Info

Upon download, users have the option to secure the downloaded file(s) by encrypting them into a password-protected ZIP archive. The use of a password may be mandatory if MetaDefender Managed File Transfer™ is configured to enforce this requirement.

Info

If an internet connection error occurs during the archive download process, the download will automatically resume once the connection is reestablished.

Users can select all files and folders on a page using the checkbox at the top left:

Users can copy the download link for files and folders using the action menu on the right:

### [**Edit Password**](/docs/mdmft/operating/my-files#edit-password)

MetaDefender Managed File Transfer supports adding or editing a password (both ASCII and non-ASCII) for an encrypted file from the "My Files" tab.

Info

If the correct password is entered and the file is not blocked, it will be available for download to all users with the appropriate permissions.

Info

If download authentication in "[Global Settings](/docs/mdmft)" is not required, any user has the right to insert passwords.

### [**Delete Password**](/docs/mdmft/operating/my-files#delete-password)

Passwords can be deleted from an encrypted file only if the correct one has not yet been added.

### [**Adding or Editing File Tags**](/docs/mdmft/operating/my-files#adding-or-editing-file-tags)

To add or edit a tag for a file (which can be used for later searches), click on the "More actions (...)" button and choose "Edit file tags" for one of the files in the grid.

You can add or edit any existing tags for this file in the "Edit file tags" window.

Info

Each file can have up to *20 tags*. A tag cannot exceed *50 characters* in length.

### [**Sorting**](/docs/mdmft/operating/my-files#sorting)

Currently, you can sort files by Name, Upload Date and Expiration Date on the "My Files" page.

### [**Filtering**](/docs/mdmft/operating/my-files#filtering)

You can filter files by Upload Date by clicking on the "Advanced" button and selecting either predefined time intervals or a custom date range.

When a date filter is active, you can remove it by clicking the **"**X**"** button.

### [**Hide / Show a Column**](/docs/mdmft/operating/my-files#hide--show-a-column)

You can show or hide columns by using the cogwheel icon at the top right of the table. Columns such as "Result," "Processing State," "Upload Date," and "Expiration Date" can be toggled.

### [**Favorites**](/docs/mdmft/operating/my-files#favorites)

Under My Files, you can click on the star icon of a **non-Blocked** file or folder to mark it as your favorite. When you click on the "Favorites" button, only items chosen as favorites will be visible in the list. To remove an item from favorites, simply click on the star icon again.

## [View Processing File](/docs/mdmft/operating/my-files#view-processing-file)

When you upload files, it’s common to have some that finish quickly and others that take a bit longer to process. To make it easier to keep track of what’s happening, you can use the Processing Files Filter. This filter shows you only the files that are still being processed, so you don’t have to search through everything you’ve uploaded.

## [Search Inside a Folder](/docs/mdmft/operating/my-files#search-inside-a-folder)

When searching by name or tag within a folder, the results will be returned from within that folder, not from all files in MetaDefender Managed File Transfer.
