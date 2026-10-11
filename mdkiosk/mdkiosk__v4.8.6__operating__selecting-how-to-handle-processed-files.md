<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files -->

# Selecting How to Handle Processed Files

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The File Handling page is divided into two sections: actions to take on blocked files and actions to be taken on allowed files. You can set different file handling options for each, including copying to either new media or a network path.

*"File Handling for Allowed Files" option on Kiosk Configuration page*

## [Remediated file handling](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#remediated-file-handling)

If file sanitization (Deep CDR) and redaction (Proactive DLP) have been configured on the MetaDefender Core, the Kiosk will download the remediated file which stands for the sanitized file or redacted file if any. There are three selections for handling a remediated file with the original media.

- **Do not copy the remediated version to the original media** (the default selection) Specifies that a remediated file will not be copied to the original media and the original file will be left untouched.
- **Attempt to replace the original file with the remediated version** Specifies that the remediated file will be copied to the original media and the original file will be deleted.
- **Copy the remediated version to the media and keep the original version** Specifies that the remediated file will be copied to the original media and the original file will be left untouched.

For a copy-to destination or custom command line script set:

- **Copy/use the remediated version** (the default selection) If a remediated version of a file exists, that will be copied to the destination, or utilized in the script, configured in favor of the original file.
- **Copy/use the remediated version & original file** If a remediated version of a file exists, it will be copied to the destination or utilized in the script configured along with the original file.

## [Stop processing media when a predefined number of blocked files are found](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#stop-processing-media-when-a-predefined-number-of-blocked-files-are-found)

Selecting this option will cause a Kiosk session to stop processing immediately when the preset number of blocked files is found. Kiosk will alert the user that preset numbers blocked files were found and go directly to the session summary after the user has acknowledged the message.

Info

- The number of blocked files can be higher than the setting.
- Max value of blocked files can be set is 1000.
## [Taking no action or removing files](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#taking-no-action-or-removing-files)

To take no action on blocked or allowed files, select the **No Action** radio button. To remove any non-remediated blocked files, select the **Remove file** radio button and select an option from the drop-down menu:

- **Quarantine blocked files in Kiosk**: blocked file will be added to the Kiosk quarantine and removed from the original media
- **Quarantine blocked files in Core**: blocked file will be added to the Core quarantine (if configured on Core) and removed from the original media
- **Remove all blocked files from media**: blocked file will be removed from the original media

  - **Prompt User for Confirmation**: user will be prompted whether to delete all blocked files at the results screen
- **Remove selected blocked files from media**: Kiosk will show all blocked files; and Administrator can select and remove the blocked files from the original media

  - **Prompt User for Confirmation**: user will be prompted whether to delete the selected blocked files

## [Copying Allowed files to Original Media](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#copying-allowed-files-to-original-media)

Warning

This option will delete all files and perform a disk format\wipe on the original media before copying ONLY the allowed files back to the original media.

This option is only available for allowed files. After enabling this option, standard wipe options of Format, 1, 3, or 7 pass wipe are selectable. Please note that the pass wipe options will take significantly more time to complete.

*"File Handling for Allowed files" on Kiosk configuration page*

## [Copying files to a designated locations](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#copying-files-to-a-designated-locations)

**Note:** If a file has been remediated by MetaDefender Core's Data Sanitization and Copy to is selected here, the remediated file will be copied to the desired location, not the original file.

You can configure files to be copied to a designated location in the Copy to section.

### [Prompt user before copying](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#prompt-user-before-copying)

By default, a user will have to initiate copying files from session results screen. If prompting is disabled, files will be copied automatically before the session results are displayed.

### [Folder structure](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#folder-structure)

MetaDefender Kiosk will copy files to the location specified by one of the three naming conventions selected:

- **Directory named with the unique session ID:** Copies files to a directory identified by the session ID.
- **Directory named with the session start time (GMT):** Copies files to a directory identified by the session start time.
- **Keep the same folder structure as on original media (no subfolders):** Copies files to the same directory as in the original media.

### [Processing virtual disk files](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#processing-virtual-disk-files)

You can select to copy the original files and child files of disk image files that were mounted to scan. By default, only the original files are copied.

The child files inside the disk image will be copied to the destination on the folder whose name is constructed from the original file name and timestamp suffixes. The child file folder will be in the same folder structure as the original files.

*Original and child files are copied to destination folder*

**Notes:**

- This option is available for both allowed and blocked file settings.
- Kiosk will not modify the content of original disk image files.
- This option only takes effect for the disk image type that is enabled mounting and scanning option at [global configuration for disk image files](https://docs.opswat.com/mdkiosk/advanced-deployment/configuring-global-kiosk-settings#disk-image-files). If the disk image type is disabled mount and scan, only the original file is scanned and copied to destination.

### [Allow user to select folder structure for copy to directory and user media](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#allow-user-to-select-folder-structure-for-copy-to-directory-and-user-media)

This allows users to select the folder structure (outlined above) before copying files.

### [Allow user to select copy option](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#allow-user-to-select-copy-option)

This allows users to select which enabled copy option to run at the end of a session. For example, if copying to a Directory and User Media is set, a user can choose to run both, neither or only one. If multiple directories are configured, a user will be able to choose among the list of configured directories.

### [Directory](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#directory)

The Directory option allows you to specify locations for blocked or allowed files. Files will be copied to all configured directories by default. The copy to directory uses AD user's credentials that is logged into the Kiosk session for copying privileges.

- **Path**: indicates the destination location files will be copied to.
- **Display Name:** indicates the value that is displayed on the UI to the user for selection.
- **Access Control** (only available on Employee workflow): grant permissions of the files and folders when copying destination locations.

  - **Inherited**: Files and folders will inherit the same permissions as the parent folder
  - **Restricted**: Only Kiosk authenticated users will have the permissions to access their files and folders
- **Use specific AD user**: Have Kiosk copy files to this destination using one fixed Active Directory account you configure — instead of the credentials of whoever is currently using the Kiosk. This is useful when you want every copy to a given share to run under a single, auditable account regardless of who signed in. Turn this on for the destination and provide a Domain (optional — leave it blank if the same account works across every domain you use), Username, and Password. This option is set independently for each configured directory destination. See [Using a specific account for network-share copies](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#using-a-specific-account-for-network-share-copies) below for details.
- **OS logged in user:** A fallback identity, used only if **Use specific AD user** is turned on for the same destination and its credentials fail to complete the copy (for example, the account can't reach the share, or the password has changed). Kiosk does not automatically fall back to the credentials of whoever is signed in at the Kiosk — only to this option, and only if you've enabled it.

Info

- Maximum number of directories can be added is 100
- ***Path*** and ***Display Name*** must be unique
- ***Access Control*** option is only available on Kiosk version 4.7.2 or newer
- If ***Allow user to select copy option*** is enabled, then the user will be able to browse and select which directories will be utilized, including the sub-directories

You can copy files to a remote server (i.e. network share) by providing a UNC path. To allow for more restrictive permissions on a network share, a MetaDefender Kiosk workflow will need to be created containing users that have, at minimum, write permission to the network share. When a user logs into a session, MetaDefender Kiosk will attempt to use the permissions of the user to copy files to the network share.

Pro tips

The predefined ‘%%%%’ variable can be used within the designated location in the ***Path*** field to allow MetaDefender Kiosk to copy files to a folder (e.g. ‘username’). This is for the user logged into the session.

Responses to user questions can also be utilized in the ***Path*** field via the predefined '%%%userresponse#%%%' variable, where '#' is the number of the response to the corresponding user question. For example, to utilize the answer to the question 2, the variable to use would be '%%%%'. If no response to the question was given or no such question exists for the user response to exist (e.g. %%%%), then the variable will exist in the path created.

Restricted directories

Following directories are restricted and cannot be used:

- C:\Windows
- C:\Program Files
- C:\Program Files (x86)
- C:\ProgramData
- C:\Users
## [Using a specific account for network-share copies](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#using-a-specific-account-for-network-share-copies)

If a network-share destination should always be accessed with one dedicated account — rather than whichever identity happens to be signed in at the Kiosk — turn on **Use specific AD user** on that directory entry and provide the account's credentials. Kiosk uses this account for that destination going forward, whether the person using the Kiosk signed in with Single Sign-On, an Active Directory account, a local Windows account, or as an unauthenticated guest.

### [What you need](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#what-you-need)

- The account's **Username** and **Password**.
- A **Domain**, only if the account belongs to a specific domain and you want to restrict it to that domain. Leave Domain blank if the same username and password should work against any domain your shares use.
- Read/write permission for that account on the destination share.

### [Setting it up](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#setting-it-up)

1. Open the workflow's **File Handling** settings and, under **Allowed Files** or **Blocked Files**, configure a directory entry under **Copy to > Directory** (Path and Display Name) if you haven't already.
2. On that directory entry, turn on **Use specific AD user**.
3. Enter the account's **Domain** (optional), **Username**, and **Password**.
4. Save your changes. If you leave Username or Password blank while this option is turned on, saving is blocked until you fill them in.

> **Note:** If you also want Kiosk to try the locally logged-in Windows account as a backup when the specific account can't complete the copy, turn on **OS logged in user** on the same directory entry as well. Without that fallback turned on, a failed specific-account copy simply fails — Kiosk never substitutes the identity of whoever is using the Kiosk.

### [Letting users browse the share](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#letting-users-browse-the-share)

If **Allow user to select copy option** is also turned on for the workflow, the person using the Kiosk can browse into the destination and its subfolders before choosing where to copy their files — using the specific account's permissions, not their own. If **Copy & Go** is turned on instead, the copy (and, if configured, the retrieval) happens automatically using the specific account, with no prompt shown to the user.

**Example:** A walk-up kiosk is used by a mix of guests, SSO users, and badge-in employees, but every copy should land in the same locked-down department share that none of those individual users has direct access to. An administrator creates one service account with write access to the share, enables **Use specific AD user** on the Directory destination, and enters that account's credentials. From then on, every session — regardless of how the person signed in — copies its files to the share using that one account, and no individual user's own network permissions come into play.

### [User media](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#user-media)

Selecting the `User media` checkbox will prompt users to insert secondary media to copy files to.

Supported media are USB, CD/DVD (must be blank and non-finalized), and Floppy.

`Insert the media after processing` - (option **only** applies to a Copy&Go session) this locks users to insert the media after all files are processed. If disabled, users can insert the secondary media at the start of a session.

`Allow Copying to Floppy Drives` - displays a floppy disk detection button to copy files to floppy.

`Wipe user media before copying` - displays the wipe option to automatically apply to the destination media before files are copied to it.

Warning for wiping user media

The wiping of CD/DVD is not supported by Kiosk, if user try to copy to a disc with data, the warning message will be shown and inform user to try again with blank disc.

This process may take a long time if the destination media is large or multiple pass wipes are configured

These encrypted media types do not support secure wipe: BitLocker, McAfee, and Flash Security

### [MetaDefender Managed File Transfer Server](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#metadefender-managed-file-transfer-server)

- **MFT Server:** See [6. Configuring with MFT](/docs/mdkiosk/v4.8.6/configuration/configuring-with-metadefender-vault) for instructions and more details
- **Select a MFT account option for file uploads:** Choose a MFT account option in this section
- **Select how files will be uploaded to MFT:** Choose a file upload option
- **File Chunk Upload Size:** Size of chunks a file will be broken into for uploading to MFT
- **Synchronize with Data Diode**: Alleviates any issues seen with uploading files through a data diode (**note**: *this will increase overall upload time*)

#### [MFT account options for file uploads](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#mft-account-options-for-file-uploads)

- **Always upload to a MFT guest account** A temporary guest login ID is created and displayed to the Kiosk user both on the scan results screen as well as in the digital and printed logs.
- **Attempt to use user credentials if they are available** Kiosk uploads files to the user account that matches the one used during authentication
- **Enter MFT user to upload files to** Kiosk uploads files to the user account supplied (this can be useful when custom authentication users do not match users synced with MFT)
- **Browse and choose an upload folder** — instead of always uploading to the root folder of the selected MFT account, you can let users browse that account's folder structure and pick a specific destination folder before the upload starts. This can be turned on separately for allowed files and for blocked files.

Note

Starting in Kiosk 4.8.4, you can also configure a single, administrator-specified MFT account for **Guest workflow** uploads — the same option already available for the Employee workflow. This is available for both allowed and blocked files. For blocked files, only the temporary guest account and the administrator-specified account are offered; the option to upload under the current user's own credentials applies to allowed files only.

**Example:** An administrator wants every file a walk-up guest uploads to MFT to land under one shared department account, rather than a different temporary guest identity each session. After selecting the administrator-specified account option for the Guest workflow's allowed and blocked file handling and entering the account's username, uploads from guest sessions go to that account automatically — guests are never prompted to choose or enter an account themselves.

Info

If upload using the user credentials authentication fails, files will be uploaded to the MFT using guest account

#### [MFT file upload options](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#mft-file-upload-options)

- **Upload files and preserve directory structure** Files are upload to MFT while maintaining the directory structure
- **Upload files, preserve directory structure and send scan results** In addition to the previous option, files are uploaded along with their scan result obtained from Core. MFT will opt to use these results rather than rescanning the uploaded files.
- **Upload a zip archive containing the allowed files** Files are packaged into one zip resulting in one file upload to MFT.

### [Choosing an upload folder](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#choosing-an-upload-folder)

By default, files copied to MFT are uploaded to the root folder of the account selected under **MFT account options**. If you'd rather let users pick a specific folder each time, turn on folder selection for allowed files, blocked files, or both.

When folder selection is on, the folders a user sees are based on that account's own access — for example, if MFT accounts are matched by username, a user browsing after signing in only sees folders that account can already see, they aren't given broader access than they'd otherwise have. If you use a specific MFT user account and require users to enter a username or email address, they're prompted for that first, and then see the folder structure for the account they entered.

Note

Folder browsing only appears if the workflow is set to prompt users before copying. If files are copied automatically with no prompt, or if Copy & Go is turned on for the session, folder selection isn't available and files upload to the account's root folder instead.

**Example:** An administrator wants users to choose where their allowed files land on the MFT server, using each user's own MFT account. After turning on **prompt before copying** and MFT folder selection for allowed files, users are shown a folder browser — with breadcrumbs for navigating into subfolders — after their files finish processing, and their upload goes to whichever folder they select.

### [Only Copy Remediated Files](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#only-copy-remediated-files)

Info

This option only exists for blocked files.

If enabled, only remediated versions of blocked files will be copied to the destination. Any blocked file that was not remediated will not be copied.

### [SHA-256 Verification](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#sha-256-verification)

If enabled, MetaDefender Kiosk compares the hash value of files on the target directory with the ones from the original directory. Any mismatches are displayed and logged. No retry of the copy is performed in the case of a hash value mismatch.

### [Delete after copy](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#delete-after-copy)

Select this checkbox if you want MetaDefender Kiosk to delete the blocked or allowed file after copying it to the specified location.

### [Tombstone files for blocked files](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#tombstone-files-for-blocked-files)

When a file is blocked, MetaDefedener Kiosk provides an option to create a tombstone file. This file serves as a placeholder and allows you to trace the blocked file when it is copied to a secondary location.

The tombstone file represents the original blocked files and includes the key metadata such as file's ID, hash and scan result.

- Metadata

  - Data ID
  - File Hash
  - Scan result
- File name format: `<original child file name>.tombstone.txt`

To enable Tombstone files option,

1. **When copying files to a secondary location (such as Directory, Media and MFT)**

Open Kiosk Console, navigate to Workflow > File Handling > Blocked files > Copy to > Additional Settings > enable "Replace blocked files with tombstone files"

2. **When removing blocked files in the original media**

Open Kiosk Console, navigate to Workflow > File Handling > Blocked Files > Remove file > select "Replace blocked files with tombstone files"

Tombstone files on archive files

If you want tombstone files to replace blocked child files within an archive, this must be configured via MetaDefender Core settings. For detailed instruction, please refer to the relevant [Knowledge Base article](https://www.opswat.com/docs/mdcore/deep-cdr/tombstone-file)

## [Run custom command line script](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#run-custom-command-line-script)

Administrator Caution

Enabling Custom Command Line Script may introduce potential security risks. It is recommended that only experienced administrators enable and manage this setting, taking full responsibility to implement appropriate security measures and monitor for any vulnerabilities.

Kiosk will execute the custom command line script at post-processing phase. See [Custom Command Line Script](/docs/mdkiosk/v4.8.6/operating/custom-command-line-script) for more details.
