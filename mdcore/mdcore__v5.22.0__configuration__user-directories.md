<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/user-directories -->

# User directories

Users can be organized into separate user directories. User directories help to enforce the following login policies:

1. Lockout after a number of consecutive failed login attempts
2. Disable logins for all users of the user directory

The Users tab lists the existing user directories in the system.

## [Default user directory](/docs/mdcore/v5.22.0/configuration/user-directories#default-user-directory)

After installation a default user directory is created with the following parameters:

| User directory type | Name | Number of failed logins before lockout | Lockout time [minutes] |
| --- | --- | --- | --- |
| Local | LOCAL | 3 | 5 |
| Local | SYSTEM | 0 | 0 |

Two types of user directories exist in MetaDefender Core:

1. Local
2. Active Directory/LDAP

## [Local type user directories](/docs/mdcore/v5.22.0/configuration/user-directories#local-type-user-directories)

Local type user directories allow creating users that locally exist on the MetaDefender Core.

To protect user accounts of a local user directory against brute force password breaking attacks, policy settings may be applied:

- **Number of failed logins before lockout**: After this number of consecutive failed login attempts the account gets locked.
- **Lockout time [minutes]**: The account remains locked for the given minutes.

  - When the lockout time elapses, the account lock gets released automatically.
  - Users with appropriate permission may release the account lock earlier using the *RELEASE LOCKOUT button*.
- **Enable enhanced password policy**: Check out more at [Password Policy](/docs/mdcore/v5.22.0/configuration/password-policy).

## [Active Directory/LDAP type user directories](/docs/mdcore/v5.22.0/configuration/user-directories#active-directoryldap-type-user-directories)

LDAP and Active Directory type user directories allow users defined in an LDAP or Active Directory to access MetaDefender Core.

These types of user directories do not provide the possibility to define login policies; these policies may be defined in the LDAP or Active directory directly.

## [Functions](/docs/mdcore/v5.22.0/configuration/user-directories#functions)

Besides listing existing user directories the **User directories** tab provides the following functions:

- Add new user directory
- Modify (and view) existing user directory
- Delete existing user directory
- Enable or disable existing user directory
- Unlock locked accounts

### [Add new Local type user directory](/docs/mdcore/v5.22.0/configuration/user-directories#add-new-local-type-user-directory)

Click the *ADD NEW USER DIRECTORY* button and select **Local** in the USER DIRECTORY TYPE drop down list.

For explanation of the **Number of failed logins before lockout** and **Lockout time [minutes]** fields read the [Local type user directories](/docs/mdcore/v5.22.0/configuration/user-directories#local-type-user-directories) section.

### [Add new Active Directory](/docs/mdcore/v5.22.0/configuration/user-directories#add-new-active-directory)

Click the *ADD NEW USER DIRECTORY* button and select **Active Directory** in the USERDIRECTORY TYPE drop down list.

The USERNAME and PASSWORD values should be the name as DN (distinguished name) and password of a user who has permissions to do searches in the directory.

Warning

As long as TLS is not configured for the Web Management Console, passwords are sent clear-text over the network. To set up TLS see [Enabling HTTPS](/docs/mdcore/v5.22.0/configuration/enabling-https).

Warning

As long as ENCRYPTION field is set to *None* there is no encryption used between the MetaDefender Core and the Active Directory server. All passwords and other information are sent clear-text over the network.

Use *StartTLS* or *SSL* as ENCRYPTION whenever possible and don't forget to install the certificate of the issuer of the AD server's certificate on the server that runs MetaDefender Core.

The USER BASE DN and the GROUP BASE DN values should provide the entries in the Active Directory tree where user and group entity lookups should be started. For tips about finding the proper values for these fields see [Active Directory/LDAP attributes](/docs/mdcore/v5.22.0/configuration/active-directory-attributes).

In the section "Privileged Access Management Manger"

- Select None - if you don't have any external application for manage AD accounts
- Select BeyondTrust Password Safe - if you use Password Safe for manage AD accounts - More details in here: [Integrate Active Directory with BeyondTrust Password Safe](/docs/mdcore/v5.22.0/configuration/integrate-active-directory-with-beyondtrust-s-password-safe)

Click the *TEST* button to test the Active Directory settings. If the test succeeds, then the user directory can be added to the list with the *ADD* button.

### [Add new LDAP Directory](/docs/mdcore/v5.22.0/configuration/user-directories#add-new-ldap-directory)

Click the *ADD NEW USER DIRECTORY* button and select **LDAP** in the USERDIRECTORY TYPE drop down list.

The following information should be given to configure an LDAP user directory:

- **bind username**: The name as DN of a user who has permissions to do searches in the LDAP directory.
- **user base DN**: The DN from where all users can be reached.
- **group base DN**: The DN from where all groups can be reached.
- **user object class**: The name of the object class (objectClass) that is for user objects. (e.g. posixAccount or person)
- **user account attribute**: The name of the LDAP attribute that contains the login name of the users.
- **group object class**: The name of the object class (objectClass) that is for group objects. (e.g. posixGroup or group)
- **group account attribute**: The name of the attribute that contains the name of the group of the users.

Note

Please note that using only DC components for the user/group DNs may result in searches to be executed from the top of the directory information tree and potentially slow down LDAP server responses a lot and thus have an impact on MetaDefender Core password validation. The rule of thumb here is that the more specific the user/group DN the faster the server response.

Taking the above example into consideration: a user search DN of "OU=People,DC=example,DC=com" could potentially result in much faster server response than "DC=example,DC=com" and should be preferred assuming all users reside under "OU=People,DC=example,DC=com" in the directory information tree.

Note

Please also note that users and groups may reside in different parts of the directory information tree, as a consequence applying the same, more specific DN both as USER BASE DN and GROUP BASE DN may cause MetaDefender Core not to find group accounts in the directory information tree. So, these DNs should be chosen carefully.

### [Unlock locked accounts](/docs/mdcore/v5.22.0/configuration/user-directories#unlock-locked-accounts)

All the locked user accounts that belong to a Local type user directory, can be released clicking the *RELEASE LOCKOUT* button.

## [Notes](/docs/mdcore/v5.22.0/configuration/user-directories#notes)

The currently logged on user cannot disable the user directory to which her account is assigned to. For example, the admin user cannot disable the LOCAL user directory.

The currently logged on user cannot delete the following:

- Her own user account. For example, the admin user cannot delete the admin user account.
- The user directory to which her account is assigned to. For example, the admin user cannot delete the LOCAL user directory.
