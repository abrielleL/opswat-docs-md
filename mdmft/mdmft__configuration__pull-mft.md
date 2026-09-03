<!-- source: https://www.opswat.com/docs/mdmft/configuration/pull-mft -->

# Pull MFT

Summarize Page    Connect to Cursor Connect to VS Code

Pull MFT allows transferring files from another MetaDefender® MFT directly into your current logged in account.

Warning

To configure this feature you must have administrator privileges.

## [Setup Instances](/docs/mdmft/configuration/pull-mft#setup-instances)

Navigate to "Settings" --> "Integrations" --> "MFT".

Add instances by inputing the source URL as shown and a display name for easier identification.

Info

Enable the "Ignore Certificate Warnings" option for self-signed SSL certificates.

Click 'Update.'

## [Enable Pull](/docs/mdmft/configuration/pull-mft#enable-pull)

This feature is disabled by default. To enable it, go to "Settings" --> "Global Settings" --> "File Settings".

Click "Enable Pulling on Upload Files".

If no MFT instance has been previously configured, you will receive a warning notification.

You can also choose to make the Pull MFT feature available to all users or only to users with administrator roles.

## [Pull Files](/docs/mdmft/configuration/pull-mft#pull-files)

### [Authentication](/docs/mdmft/configuration/pull-mft#authentication)

To initiate a Pull, click "Upload Files" --> "Pull from MFT" to select a Pull MFT instance to pull files from.

Enter your login credentials.

#### [Multi-Factor Authentication](/docs/mdmft/configuration/pull-mft#multi-factor-authentication)

If the MetaDefender Managed File Transfer™ instance has Multi-Factor Authentication (MFA) enabled, then users are required type in their One-time Password(OTP). If their account does not have MFA, then they are required to go MetaDefender Managed File Transfer™ instance and set it up before using Pull MFT feature.

User has 2FA and required to provide their OTP code

admin user needs to setup 2FA in Low Security MFT instance

### [Choosing Files](/docs/mdmft/configuration/pull-mft#choosing-files)

Browse and select files to pull.

Info

You can only select files, not folders.

Access folders by clicking on their respective rows.

Info

Certain files may be inaccessible for pulling due to their status. In these cases, the checkbox next to the file name will be grayed out, indicating that only processed and available files can be pulled.

Once your files are selected, click "Pull Files".

The system will inform you that the Pull process has started, and the files will upload to the MetaDefender MFT instance.

A corner modal will appear with information about the process, including the count of files left, the currently processed file, and the destination. Closing the modal will not affect the pulling process.

Info

Occasionally, some files might not be pulled even though they appear available while browsing. This could be due to network issues, changes in file status during the process, or configuration differences between the two MFT instances that permit certain files on one but not the other.
