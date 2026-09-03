<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-files-are-copied-to-admin-accounts-instead-of-ad-account-in- -->

# Why files are copied to Admin accounts instead of AD account in MFT?

This article applies to all Kiosk versions and MFT version 3.8.0 or newer

## [Problem](/docs/mdkiosk/v4.8.5/knowledge-base/why-files-are-copied-to-admin-accounts-instead-of-ad-account-in-#problem)

Kiosk and MFT are configured to the same Active Directory. After upgrading MFT to 3.8.0 or later, you may encounter the following issue:

When users log in with Active Directory credentials, files that are supposed to be uploaded to the user's directory on MFT are instead uploaded to the admin's MFT directory.

In the kiosk log, you may see entries like the following:

In the MFT rest log, you may see errors such as:

## [Root cause](/docs/mdkiosk/v4.8.5/knowledge-base/why-files-are-copied-to-admin-accounts-instead-of-ad-account-in-#root-cause)

Starting in version 3.8.0, MFT introduces the ability for administrator to manage both Active Directory and Local groups on the “Trusted Network” page. This feature allows administrators to specify which groups are permitted or denied access to upload and download files, providing better control over file access and security.

In earlier MFT versions, upload requests from Kiosk to MFT did not require group membership to be specified. However, starting in MFT 3.8.0, if group membership is not provided, the request failed. To prevent data loss, files are instead assigned to the admin account by default.

## [Solution](/docs/mdkiosk/v4.8.5/knowledge-base/why-files-are-copied-to-admin-accounts-instead-of-ad-account-in-#solution)

Go to **MFT management console** and navigate to: **Settings** > **Global Settings** > **File** tab, then enable the following option: “**Allow Users to Upload Files Without Specifying Group Membership”**

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
