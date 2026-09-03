<!-- source: https://www.opswat.com/docs/mdmft/configuration/notifications -->

# Notifications

Summarize Page    Connect to Cursor Connect to VS Code
## [SMTP Configuration](/docs/mdmft/configuration/notifications#smtp-configuration)

To enable notifications, configure the SMTP settings located under "Notifications" → "SMTP" in the sidebar menu.

Be Aware

During SMTP configuration, the connection test email is both **sent from** and **delivered to** the **configuring user’s email** address (or notification email address, if set). Ensure this address is **not blocked** or **restricted** by any **whitelist** or **blocklist** rules on your SMTP server.

Info

You must have a valid email address to **receive a** **test email** of successful configuration.

### [Standard Settings](/docs/mdmft/configuration/notifications#standard-settings)

Enter the SMTP server's IP or DNS in the host field. Adjust the port if necessary.

### [Advanced Settings](/docs/mdmft/configuration/notifications#advanced-settings)

Select "Enable SSL/TLS" to use TLS for accessing the SMTP host. Select "Ignore Certificate" to bypass SSL certificate warnings.

Info

Do not select "Enable SSL/TLS" if the server uses STARTTLS.

The SMTP connection timeout can be configured between 15 (default) and 60 seconds.

Enter credentials if authentication is required.

(Leave the "Domain" field empty if not required.)

## [Notification Settings](/docs/mdmft/configuration/notifications#notification-settings)

Configure when email notifications are sent under "Notifications" → "Notifications Settings."

Info

These settings are available only if a valid SMTP server is configured.

### [Upload Notifications](/docs/mdmft/configuration/notifications#upload-notifications)

- Successful File Upload: Email is sent to the owner upon successful upload.
- Failed File Upload: Email is sent to administrators if an upload fails.

Info

**MFT to MFT Notification Process**

When MFT to MFT configuration is enabled, the following notification process is in place:

1. If a user with the same username as the uploader from the primary MetaDefender Managed File Transfer™ exists in the destination MetaDefender Managed File Transfer™, the file is assigned to that user, and they will receive an email notification.
2. If no matching user exists, the notification is sent to the default admin user, and the file is assigned to them.
### [Download Notifications](/docs/mdmft/configuration/notifications#download-notifications)

- Receive a download notification whenever a file is downloaded.

  - First Download**:** Notification for the first download only.
  - All Download: Notification for every download.

### [Sharing Notifications](/docs/mdmft/configuration/notifications#sharing-notifications)

- File/Folder Shared: Email is sent when a file/folder is shared with you.
- File/Folder Access Removed: Email is sent when a file/folder is unshared.

### [Supervisor Approval Notifications](/docs/mdmft/configuration/notifications#supervisor-approval-notifications)

- Notify File Owner Upon Approval: Email is sent to the owner when a file is approved.
- Notify File Owner Upon New Approval Steps: Email is sent to the file owner for each supervisor approval in Multi-stage/Step-based approval mode.
- Notify File Owner Upon Rejection: Email is sent to the owner when a file is rejected.
- Notify All Supervisors When a File is Awaiting Approval: Email is sent to all supervisors when a file is pending approval.
- Notify File Owner When Supervisor is Commenting During Approval: Email is sent to the owner when a supervisor comments during approval/rejection.
- Notify User Upon Being Selected as Supervisor: Email is sent when a user is delegated as a supervisor.

### [Global Supervisor Notifications](/docs/mdmft/configuration/notifications#global-supervisor-notifications)

- Global supervisors do not receive notifications to reduce spam.

Info

If no supervisors are assigned, notifications are sent to global supervisors. Supervisor approval process must be enabled.

### [File Scanning Notifications](/docs/mdmft/configuration/notifications#file-scanning-notifications)

- Notify User When a File is Blocked: Email is sent when a file is blocked by MetaDefender Core.
- Receive Bundled Notifications Regarding Blocked Files: If the option above is enabled, you can specify a time interval between 1 minute and 1 week for automated job notifications. With this setting, the job owner will receive bundled notifications about blocked files only at the selected frequency.

Note**:** If any "Delete the File" option is enabled in the "MetaDefender Core Integration" section, notifications will not be sent.

- Notify User When a File is Available for Download: Email is sent when a file is unlocked and available for download.

### [New User Welcome Notifications](/docs/mdmft/configuration/notifications#new-user-welcome-notifications)

- Notify Local, External or Active Directory Users Upon Account Creation: Email is sent to new users (local, external, or AD) upon account creation.
- Notify Guest Users Upon Account Creation (set as default): Email is sent to guest users and their creator users upon account creation if an email has been provided to their account. Emails can be added or modified later on.

Info

**MFT to MFT Notification Process for Guest Welcome**

When MFT to MFT configuration is enabled:

- Notifications are sent and configured individually for each MetaDefender Managed File Transfer. Duplicate notifications may occur if both MetaDefender Managed File Transfers are enabled to send them. Each MetaDefender MFT can be configured differently and notification settings such as "sender address" and "login URL" may vary.
- Duplicate notifications are sent to creators ignoring the "Aggregate all file/folder actions to a single user" MetaDefender MFT setting.
### [Automated Jobs Notifications](/docs/mdmft/configuration/notifications#automated-jobs-notifications)

- Notify User Upon Successful Job Completion: Email is sent to the job owner upon successful completion.
- Notify User Upon Job Failure: Email is sent to the job owner when the job fails.

### [Notification URL](/docs/mdmft/configuration/notifications#notification-url)

This is the hostname used in emails to generate links to the MetaDefender Managed File Transfer application. By default, it is set to the Managed File Transfer server's hostname.

Info

The Notification URL will be overridden if the server's hostname changes.
