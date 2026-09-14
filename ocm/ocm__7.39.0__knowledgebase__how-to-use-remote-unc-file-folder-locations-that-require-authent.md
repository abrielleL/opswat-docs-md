<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/how-to-use-remote-unc-file-folder-locations-that-require-authent -->

# How to use remote UNC file/folder locations that require authentication in Windows

From OPSWAT Central Management version 7.29.0, remote file/folder paths in UNC format are now supported for certain features such as [Update Settings](/docs/ocm/7.39.0/configuration/update-settings). However, there are certain caveats if the remote location requires authenticated access. Because OPSWAT Central Management service runs as the [LocalSystem user account](https://learn.microsoft.com/en-us/azure/active-directory/architecture/service-accounts-computer) by default, the administrators must take certain additional steps to provided authenticated access as the LocalSystem user account cannot possess saved credentials by default.

A failed authentication error looks similar to the image below:

There are two possible methods to provide authenticated access to remote UNC locations:

- Change the user account that is used for OPSWAT Central Management.
- Provide AD access permission for the LocalSystem account.

## [Change the user account that is used for OPSWAT Central Management](/docs/ocm/7.39.0/knowledgebase/how-to-use-remote-unc-file-folder-locations-that-require-authent#change-the-user-account-that-is-used-for-opswat-central-management)

Because the LocalSystem user account cannot possess saved credentials by default, one workaround is to change the user account OPSWAT Central Management runs as.

Open the Windows Service interface services.msc, find the OPSWAT Central Management service and right-click select **Properties.**

In the pop-up dialog, change to the **Log On** tab, select **This Account**, and enter the credentials. Please note that the specified account should be a local administrator account for OPSWAT Central Management to function properly.

Log in with the specified account and add the saved credential for the remote UNC location. You can use the cmdkey command in a command-line interface such as cmd.exe.

BashCopycmdkey /add:{ip_unc_folder_machine} /user:{username} /pass:{password}
## [Provide AD access permission for the LocalSystem account](/docs/ocm/7.39.0/knowledgebase/how-to-use-remote-unc-file-folder-locations-that-require-authent#provide-ad-access-permission-for-the-localsystem-account)

As described in [this Microsoft article](https://learn.microsoft.com/en-us/azure/active-directory/architecture/service-accounts-computer), the LocalSystem account represents the computer in the AD domain. You can use this method if the remote UNC location requires AD authentication and it share a domain trust relationship with the computer running OPSWAT Central Management.

In the Network Access setting for the remote UNC location. add the computer account (which by extension, grant access to the computer's LocalSystem account. In the example below, MANGO is the name of the computer running OPSWAT Central Management and MANGO$ is the associated computer account and by extension, that computer's LocalSystem account.
