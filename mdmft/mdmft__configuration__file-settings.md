<!-- source: https://www.opswat.com/docs/mdmft/configuration/file-settings -->

# File Settings

Summarize Page    Connect to Cursor Connect to VS Code

## [Upload Options](/docs/mdmft/configuration/file-settings#upload-options)

### [Set Upload Limit](/docs/mdmft/configuration/file-settings#set-upload-limit)

Enables setting a maximum size limit for uploaded files.

### [Set Upload Quota](/docs/mdmft/configuration/file-settings#set-upload-quota)

Limit user storage. When active:

- Users cannot upload files that exceed the quota.
- Current storage status will be shown at the user information dropdown list.

### [Hide File Upload](/docs/mdmft/configuration/file-settings#hide-file-upload)

Hides the "Upload Files" button.

### [Enable Pulling on Upload Files](/docs/mdmft/configuration/file-settings#enable-pulling-on-upload-files)

Expands the upload dialog to include an extra tab exclusively for pulling files when enabled.

For more detailed information, [click here](/docs/mdmft/configuration/pull-mft).

### [Allow Users to Upload Files Without Specifying Group Membership](/docs/mdmft/configuration/file-settings#allow-users-to-upload-files-without-specifying-group-membership)

For further details on Group selection behavior during upload, [click here](/docs/mdmft/operating/upload-files).

### [Enable File Classification](/docs/mdmft/configuration/file-settings#enable-file-classification)

Enabling this option will allow the admin to define classification labels. The users can label their uploaded files by selecting one of these pre-defined classifications during the upload process or after that directly from the My Files menu.

The saved classifications can be updated and deleted.

Warning

The deletion of a classification will remove it from all related files.

If the File Classification enabled, the MetaDefender® MFT can handle classifications received from MetaDefender Kiosk™. These classifications cannot be edited or changed by the admin or the users.

#### [Enforce File Classification](/docs/mdmft/configuration/file-settings#enforce-file-classification)

When enabled, users must select a file classification when uploading a file. Without selecting an existing classification, uploading a file is not permitted when this setting is turned on.

---

## [Processing Options](/docs/mdmft/configuration/file-settings#processing-options)

### [Sharing](/docs/mdmft/configuration/file-settings#sharing)

Specifies if file sharing between users is allowed.

### [Advanced Sanitization](/docs/mdmft/configuration/file-settings#advanced-sanitization)

Allows users to skip sanitization: users can skip data sanitization when uploading a file.

Block files without sanitization: Ensures that non-sanitized files do not become available for download and will reach a "Blocked: No Sanitization" state.

### [Re-upload Sanitized Versions of Blocked Files](/docs/mdmft/configuration/file-settings#re-upload-sanitized-versions-of-blocked-files)

The Re-upload Sanitized Versions of Blocked Files feature automatically re-uploads sanitized versions of files that were originally blocked during processing. Once re-uploaded, the sanitized file is treated as a brand-new upload from the same source, goes through the normal workflow, and receives its own independent verdict.

To ensure the re-uploaded sanitized version is genuinely safe MetaDefender Core™ must be configured to remove infected components during processing.

### [Allow Editing File Expiration Date by Users](/docs/mdmft/configuration/file-settings#allow-editing-file-expiration-date-by-users)

If disabled, users cannot change the file expiration time during upload. It is set by default.

### [Auto-Delete Empty Folders](/docs/mdmft/configuration/file-settings#auto-delete-empty-folders)

All folders that no longer contain any files due to file expiration will be deleted.

### [Fallback to Global Core Workflow](/docs/mdmft/configuration/file-settings#fallback-to-global-core-workflow)

Allows MetaDefender Managed File Transfer™ to use the integrated MetaDefender Core™ global workflow if no user-specific workflow is configured or if the workflow has been removed.

### [Use Dedicated Sync Workflow](/docs/mdmft/configuration/file-settings#use-dedicated-sync-workflow)

Allows MetaDefender Managed File Transfer™ to scan files received from another MetaDefender® MFT instance with a specific MetaDefender Core™ workflow instead of the default one.

### [Show File Security information for end-users](/docs/mdmft/configuration/file-settings#show-file-security-information-for-end-users)

Shows each user the security details for their own files (e.g., file risk level, detected threats, policy status). Turn off to limit this information to administrators only.

### [Show Scan Results for end-users](/docs/mdmft/configuration/file-settings#show-scan-results-for-end-users)

Shows each user the security scan results for their own files (e.g., detected threats, risk status, last scan time). Turn off to restrict scan result visibility to administrators only.

### [Expiration Date](/docs/mdmft/configuration/file-settings#expiration-date)

Every file has an expiration date and here you can specify a default value. Once a file expires it is permanently removed.

Info

You can configure custom file expiration days for users and groups separately.

#### [Configuration Precedence](/docs/mdmft/configuration/file-settings#configuration-precedence)

The expiration period is resolved using the following order of precedence:

1. **User-level configuration** If a File Expiration Days value is explicitly configured for a user.
2. **Group-level configuration** If no user-level value is configured, the system checks the user’s group. If a File is uploaded as a group member than the group's configured value will be used.
3. **Global configuration** If neither the user nor any of their groups has a configured value, the system applies the globally defined File Expiration Days setting.

---

## [Download Options](/docs/mdmft/configuration/file-settings#download-options)

### [Download Authentication Required](/docs/mdmft/configuration/file-settings#download-authentication-required)

Specifies whether users need to log in to download files from MetaDefender Managed File Transfer™.

### [Enable Password-Protected Download](/docs/mdmft/configuration/file-settings#enable-password-protected-download)

Administrators can download files or folders in password-protected archives.

Info

Password-protected download is disabled by default. During an upgrade, previously saved file settings will be retained unless they remain unchanged from the factory default, in which case the password-protected download will be disabled.

- Optional (default): Users can choose whether to use a password-protected archive for downloading on the download modal.

- Enforce: Requires users to download files or folders in password-protected archives.

- Enforce system password policy for download: Forces users to comply with the MetaDefender Managed File Transfer password policy, requiring a password of at least 12 characters that meets the required strength.

### [Archive File After Download](/docs/mdmft/configuration/file-settings#archive-file-after-download)

Enables file archiving when files are downloaded via the MetaDefender Kiosk integration.

### [Allowed Parallel Downloads](/docs/mdmft/configuration/file-settings#allowed-parallel-downloads)

Sets the maximum number of files that can be downloaded individually at the same time when a user selects multiple files. Accepted values are between **2 and 10**.

When a user selects multiple files for download, they can choose (in their personal **User Preferences**) whether to receive them bundled into a single ZIP archive or as individual parallel downloads. This setting controls the upper limit for the individual download option:

- If the number of selected files is within the configured limit, they are downloaded as separate files in parallel.
- If the number of selected files exceeds the configured limit, the individual download option is unavailable for that selection and the files are automatically bundled into a ZIP archive instead.
- If the selection contains **at least one folder**, the download is always delivered as a ZIP archive, regardless of the user's download preference and regardless of how many items are selected.

Info

If **Password-Protected Download** is set to **Enforce**, users cannot choose the individual download option — all downloads are delivered as a password-protected ZIP archive regardless of this setting, and the preference selector in User Preferences is disabled.
