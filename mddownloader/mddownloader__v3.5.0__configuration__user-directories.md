<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/configuration/user-directories -->

# User directories

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Users can be organized into separate user directories. User directories help to enforce the following login policies:

1. Lockout after a number of consecutive failed login attempts
2. Disable logins for all users of the user directory

The Users tab lists the existing user directories in the system.

## [Default user directory](/docs/mddownloader/v3.5.0/configuration/user-directories#default-user-directory)

After installation a default user directory is created with the following parameters:

| User directory type | Name | Number of failed logins before lockout | Lockout time [minutes] |
| --- | --- | --- | --- |
| Local | LOCAL | 3 | 5 |
| Local | SYSTEM | 0 | 0 |

Two types of user directories exist in Metadefender Update Downloader:

1. Local
2. Active Directory

## [Local type user directories](/docs/mddownloader/v3.5.0/configuration/user-directories#local-type-user-directories)

Local type user directories allow creating users that locally exist on the Metadefender Update Downloader.

To protect user accounts of a local user directory against brute force password breaking attacks, the following policy settings may be applied to each local type user directory:

- **Number of failed logins before lockout**: After this number of consecutive failed login attempts the account gets locked.
- **Lockout time [minutes]**: The account remains locked for the given minutes.

  - When the lockout time elapses, the account lock gets released automatically.
  - Users with appropriate permission may release the account lock earlier

## [Active Directory type user directories](/docs/mddownloader/v3.5.0/configuration/user-directories#active-directory-type-user-directories)

Active Directory type user directories allow users defined in an Active Directory to access Metadefender Update Downloader.

Active Directory type user directories do not provide the possibility to define login policies; these policies may be defined in the Active directory directly.

## [Functions](/docs/mddownloader/v3.5.0/configuration/user-directories#functions)

Besides listing existing user directories the **User directories** tab provides the following functions:

- Add new user directory
- Modify (and view) existing user directory
- Delete existing user directory
- Enable or disable existing user directory
- Unlock locked accounts

## [Add new Local type user directory](/docs/mddownloader/v3.5.0/configuration/user-directories#add-new-local-type-user-directory)

Click the *ADD NEW USER DIRECTORY* button and select **Local** in the USERDIRECTORY TYPE drop down list.

For explanation of the **Number of failed logins before lockout** and **Lockout time [minutes]** fields read the [148078792](/docs/mddownloader/v3.5.0/configuration/user-management/user-directories#src-2573274) section.

## [Add new Active Directory type user directory](/docs/mddownloader/v3.5.0/configuration/user-directories#add-new-active-directory-type-user-directory)

Click the *ADD NEW USER DIRECTORY* button and select **Active Directory** in the USERDIRECTORY TYPE drop down list.

The USERNAME and PASSWORD values should be the name as DN (distinguished name) and password of a user who has permissions to do searches in the directory.

Warning

As long as TLS is not configured for the Web Management Console, passwords are sent clear-text over the network. To set up TLS see [Configuring TLS](https://opswat.atlassian.net/wiki/display/MDM/%5BICAP%5D+3.1+Configuring+TLS).

Warning

As long as ENCRYPTION field is set to *None* there is no encryption used between the Metadefender Update Downloader and the Active Directory server. All passwords and other information are sent clear-text over the network.

Use *StartTLS* or *SSL* as ENCRYPTION whenever possible.

The USER BASE DN and the GROUP BASE DN values should provide the entries in the Active Directory tree where user and group entity lookups should be started.

Click the *TEST* button to test the Active Directory settings. If the test succeeds then the user directory can be added to the list with the *ADD* button.

## [Delete user directory](/docs/mddownloader/v3.5.0/configuration/user-directories#delete-user-directory)

Note

Users of the deleted user directory will be deleted as well. As a consequence active sessions of the users of the deleted user directory will be aborted at the time of the next interaction with the server (see the Delete user section).

To remove a user directory, hover the mouse pointer over the user directory's entry in the list and click **Remove user directory** icon.

## [Enable or disable user directory](/docs/mddownloader/v3.5.0/configuration/user-directories#enable-or-disable-user-directory)

To disable a user directory hover over the user directory's entry in the list and click the **Disable user directory** icon.

When disabling a user directory, all users that are assigned to it will be blocked from logging in.

Note

Active sessions of users of the disabled user directory will not be aborted. The user will be blocked at the time of the next login.

When a user directory is disabled then the user directory's entry in the list displays the **x** mark. To enable the user directory click the **Enable user directory** icon.

## [Unlock locked accounts](/docs/mddownloader/v3.5.0/configuration/user-directories#unlock-locked-accounts)

All the locked user accounts that belong to a Local type user directory, can be released clicking the *RELEASE LOCKOUT* button.

## [Notes](/docs/mddownloader/v3.5.0/configuration/user-directories#notes)

The currently logged on user can not disable the user directory to which her account is assigned to. For example the admin user can not disable the LOCAL user directory.

The currently logged on user can not delete the following:

- Her own user account. For example the admin user can not delete the admin user account.
- The user directory to which her account is assigned to. For example the admin user can not delete the LOCAL user directory.
