<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/blocked-file-notifications -->

# Blocked file notifications

Blocked files notifications are sent for each blocked file that is found during an Instant, Scheduled or Real-Time processing.

To enable notifications for blocked file, select the option to **Send an notification for blocked files:**

You can choose to send this email to:

- All MetaDefender Storage Security registered users
- Only to the file owner
- To the file owner and all MetaDefender Storage Security registered users

Info

Please note that the notification to the file owner could be sent only for OneDrive, Box and MFT integrations.

The email contains the following information:

- File name
- File path
- Storage unit type and name
- The reason why the file is blocked
- [Remediation](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/configuration/workflows) actions details (delete/move blocked files), when these are configured for the storage that is processed
