<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/operating/upload-files -->

# Uploading Files

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

To upload files, click the "Upload Files" button. A new window will appear.

To configure advanced settings, click "Go to Advanced Settings."

Users can upload folders by dragging and dropping them into the file drop zone. The folder structure will remain the same as on the local machine.

Note: MetaDefender Managed File Transfer™ does not allow multiple folders with the same name.

When uploading archives, you can add a password to enable successful processing of password-protected archives.

Clicking the Upload button will either start the upload process or display the Duplicate Handling dialog if any duplicate files are detected.

### [Drag and Drop Upload](/docs/mdmft/v3.11.5/operating/upload-files#drag-and-drop-upload)

You can upload files and folders to My Files by dragging and dropping them onto the upload dropzone on the My Files page. If you drag items over a specific folder, the files will be uploaded directly into that folder. Otherwise, files are uploaded to the currently open folder by default.

Dropping a folder to an empty My Files

Dropping a folder to current folder

Dropping a folder to a sub folder

Info

If you forget to apply certain settings, such as adding an upload reason, setting a password for encrypted files, or sharing the file with someone, you can still configure these options after the upload is complete.

## [Secure Web Forms](/docs/mdmft/v3.11.5/operating/upload-files#secure-web-forms)

When a published secure web form with visible questions exists, you will be prompted to answer the questions before completing the upload. Questions are presented **one at a time** with a progress bar showing your completion percentage.

All required questions must be answered to proceed. Non-required questions can be skipped.

Question types will appear as follows:

- **Text Question**: A text input field for freeform answers.
- **Single Choice Question**: Radio buttons for selecting one answer.
- **Multiple Choice Question**: Checkboxes for selecting multiple answers.

Example upload question

### [Navigation](/docs/mdmft/v3.11.5/operating/upload-files#navigation)

- **Next**: Proceeds to the next question (disabled until a required question is answered)
- **Previous**: Returns to the previous question (hidden on the first question)
- **Back to Files**: Returns to the file selection screen without completing the questionnaire. Any answers entered so far are saved to the session and restored when you return
- **Complete Upload**: Appears on the last question. Submits all answers and starts the upload.

### [Dependent Questions](/docs/mdmft/v3.11.5/operating/upload-files#dependent-questions)

If the administrator has configured Sections with dependent questions [Secure Web Forms configuration](https://www.opswat.com/docs/mdmft/configuration/file-settings/secure-web-forms), follow-up questions may appear dynamically based on your answers:

1. When you select an answer on a Single Choice question that has a Section mapped to it, the Section's dependent questions are **automatically inserted** as follow-up questions after the current one
2. The progress bar recalculates to include the newly visible questions.
3. If you go back and **change your answer**, the previously shown dependent questions are removed and replaced with the dependent questions from the newly selected option's Section (if any). If the new answer has no Section mapped, no additional questions appear.

## [Duplicate Handling](/docs/mdmft/v3.11.5/operating/upload-files#duplicate-handling)

If a file with the same name and path already exists, the system prompts you to choose how to handle duplicates:

### [Override Items](/docs/mdmft/v3.11.5/operating/upload-files#override-items)

- Existing files will be moved to the trash **after** all uploads are complete
- Sharing settings from the original files will **not** be retained

Info

In an **MFT to MFT** setup, this **action is not propagated** to connected MFTs, which may result in duplicates.

### [Upload with Unique Names](/docs/mdmft/v3.11.5/operating/upload-files#upload-with-unique-names)

- Duplicate files will be renamed by appending a `-Copy(n)` suffix, where *n* is a number
- Renaming occurs **after** the upload finishes

Info

If the resulting filename exceeds 255 characters, renaming will fail and a duplicate may remain.

Info

In an **MFT to MFT** setup, this **action is propagated** to connected MFTs.

### [Skip Existing Items](/docs/mdmft/v3.11.5/operating/upload-files#skip-existing-items)

- Files that already exist in the system will not be uploaded
- If all selected files are duplicates, no files will be uploaded and you’ll return to the file selection screen

### [Cancel](/docs/mdmft/v3.11.5/operating/upload-files#cancel)

- No files will be uploaded
- You’ll return to the file selection screen with your selections preserved

Once a duplicate handling option is selected and confirmed, the upload process will begin.

## [Upload Process](/docs/mdmft/v3.11.5/operating/upload-files#upload-process)

An upload progress overlay will appear in the bottom-right corner.

After uploading, each file will display its upload timestamp.

Info

If the internet connection is lost during upload, the system will resume uploading files that were not successfully transferred once the connection is restored.

Info

The idle session timeout is temporarily suspended during file uploads. The absolute session timeout still applies and may interrupt uploads if exceeded.

## [Recovering from Errors During the Upload Process](/docs/mdmft/v3.11.5/operating/upload-files#recovering-from-errors-during-the-upload-process)

a { text-decoration: none; color: #464feb; } tr th, tr td { border: 1px solid #e6e6e6; } tr th { background-color: #f5f5f5; }

- logs out
- cancels the upload
- a { text-decoration: none; color: #464feb; } tr th, tr td { border: 1px solid #e6e6e6; } tr th { background-color: #f5f5f5; } closes the browser tab or window a { text-decoration: none; color: #464feb; } tr th, tr td { border: 1px solid #e6e6e6; } tr th { background-color: #f5f5f5; }

the files that were successfully uploaded prior to the interruption will remain persisted in MetaDefender Managed File Transfer™.

Warning

a { text-decoration: none; color: #464feb; } tr th, tr td { border: 1px solid #e6e6e6; } tr th { background-color: #f5f5f5; }

It is not possible to resume the upload process for files that were partially uploaded or had not yet begun uploading. These files must be uploaded again.

## [MetaDefender Core Workflow Rule Priority](/docs/mdmft/v3.11.5/operating/upload-files#metadefender-core-workflow-rule-priority)

In MetaDefender Managed File Transfer, Core Workflow rules govern how files are scanned during upload. Rules can be assigned at the **user** or **group** level.

### [Rule Application Logic](/docs/mdmft/v3.11.5/operating/upload-files#rule-application-logic)

- If a user has an assigned Core Workflow rule, that rule is used
- If the user selects a group during upload, the group’s Core Workflow rule takes precedence
- If no rule is assigned to the group, the default workflow is used
- If the user does not select a group, the default workflow applies

Info

Group selection is available for Active Directory users only. The Group Selection dropdown appears if:

- The user belongs to two or more AD groups, or
- Group selection is configured as optional (Settings → Global Settings → File Settings → Allow Users to Upload Files Without Specifying Group Membership).
### [Rule Priority Order](/docs/mdmft/v3.11.5/operating/upload-files#rule-priority-order)

1. User-/Group-assigned Core Workflow rule
2. Default Core Workflow rule

Info

User- and group-assigned rules are treated with equal priority. Group selection is available only for Active Directory (AD) users, while individual core selection is available for Local, External, and Guest users.

## [File Approval Based on Group Selection](/docs/mdmft/v3.11.5/operating/upload-files#file-approval-based-on-group-selection)

If a user belongs to two or more groups, or if group selection is optional, a group selection dropdown will appear during file upload.

When a group is selected, uploaded files will require approval from supervisors of that group and global supervisors.

If no group is selected, any supervisor assigned to the user's groups may approve the file.

The list of available groups can be configured. More info [here](/docs/mdmft/v3.11.5/operating/user-management#file-policies-for-groups).
