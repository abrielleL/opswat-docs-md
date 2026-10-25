<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/user-management -->

# User management

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To manage the users of the product, go to the **Settings > User Management** menu in the Web Management Console.

## [Users and groups tab](/docs/mdicap/v5.15.0/configuration/user-management#users-and-groups-tab)

The USERS AND GROUPS tab lists the existing users, [LDAP groups and Active Directory groups](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-ADgroup) in the system.

## [Legacy default user](/docs/mdicap/v5.15.0/configuration/user-management#legacy-default-user)

Previous versions of the product created a default user during the installation with the following credentials and parameters. This default user may still exist if the product was upgraded from previous versions.

| Username | Password | Name | Email | Roles | User directory |
| --- | --- | --- | --- | --- | --- |
| admin | admin | Administrator | admin@localhost | Administrators | LOCAL |

## [Functions](/docs/mdicap/v5.15.0/configuration/user-management#functions)

Besides listing existing users, LDAP and AD groups, the USERS AND GROUPS tab provides the following functions:

- Add new user, LDAP or AD group
- Modify (and view) existing user's, LDAP or AD group's properties
- Delete existing user, LDAP or AD group

### [Add new user from a Local type user directory](/docs/mdicap/v5.15.0/configuration/user-management#add-new-user-from-a-local-type-user-directory)

To add a new user from a Local type user directory click the ADD NEW USER button and select a Local type user directory in the USER DIRECTORY drop down list.

The field ASSIGN TO ROLES lists all the roles that are assigned to this user. See section [Assign roles to a user, LDAP group or Active Directory group](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-assignroles) for details about role assignment.

Warning

As long as TLS is not configured for the Web Management Console, passwords are sent clear-text over the network. For details see [Transport Layer Security](/docs/mdicap/v5.15.0/configuration/user-management#transport-layer-security).

Warning

If enhanced password policy is enabled for the user directory this user belongs to then the new password must fulfil the password complexity requirements listed at the [Local type user directories](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-userdirectorypolicy) section.

#### [API keys](/docs/mdicap/v5.15.0/configuration/user-management#api-keys)

The APIKEY value provides access to the product's REST API for the user under editing with no authentication. If no such functionality is needed for the user then this field can be left blank.

There are two methods to create an APIKEY for a user:

1. Generate the APIKEY by using Generate link next to the APIKEY field,
2. Manually enter the APIKEY value; it must matches the following criteria:

Info

APIKEY validation criteria

- The length of the API key must be exactly 36 characters.
- It must contain numeric and lower case *a*, *b*, *c*, *d*, *e* and *f* letter characters only

(e.g. "1x2y3z..." is invalid because of the *x*, *y* and *z* characters).

- It must contain at least 10 lower case *a*, *b*, *c*, *d*, *e* or *f* letter characters.
- It must contain at least 10 numeric characters.
- It is allowed to contain at most 3 consecutive lower case letter characters (e.g. "abcd1a2b3c..." is invalid because of the four consecutive letters).
- It is allowed to contain at most 3 consecutive numeric characters (e.g. "1234a1b2c3..." is invalid because of the four consecutive numeric characters).

### [Add new users from an LDAP type or Active Directory type user directory](/docs/mdicap/v5.15.0/configuration/user-management#add-new-users-from-an-ldap-type-or-active-directory-type-user-directory)

To add a new user from an [LDAP type or Active Directory type user directory](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-aduserdirectory) click the ADD NEW USER button and select an LDAP type or Active Directory type user directory in the USER DIRECTORY drop down list. Select USER as the ACCOUNT TYPE.

Provide the name of the account in the ACCOUNT NAME field and click the FIND ACCOUNT button to look up the account in the LDAP or Active Directory. If the lookup succeeds then the ACCOUNT DISPLAY NAME and the DISTINGUISHED NAME fields are filled automatically.

Note

You must provide the account name precisely. There is no functionality to look up similar names or partial matches.

The field ASSIGN TO ROLES lists all the roles that are assigned to this user. See section [Assign roles to a user, LDAP group or Active Directory group](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-assignroles) for details about role assignment.

Add new group from an LDAP type or Active Directory type user directory

Info

The purpose of adding an LDAP or Active Directory group to the product is to assign role(s) to all the users in that LDAP or Active Directory group.

The users of the LDAP or Active Directory group can authenticate with their LDAP or Active Directory credentials in the product's Web Management Console and will be assigned with the roles assigned to the group.

To add a new group from an [LDAP type or Active Directory type user directory](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-aduserdirectory) click the ADD NEW USER button and select an LDAP type or Active Directory type user directory in the USER DIRECTORY drop down list.

Note

Select GROUP as the ACCOUNT TYPE.

Provide the name of the group in the ACCOUNT NAME field and click the FIND ACCOUNT button to look up the group in the LDAP or Active Directory. If the lookup succeeds then the ACCOUNT DISPLAY NAME and the DISTINGUISHED NAME fields are filled automatically.

Note

Do provide the group name precisely. There is no functionality to look up similar names or partial matches.

The field ASSIGN TO ROLES lists all the roles that are assigned to all users of the selected group. See section [Assign roles to a user, LDAP group or Active Directory group](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-assignroles) for details about role assignment.

### [Assign roles to a user, LDAP group or Active Directory group](/docs/mdicap/v5.15.0/configuration/user-management#assign-roles-to-a-user-ldap-group-or-active-directory-group)

Role(s) must be assigned to users, LDAP groups and Active Directory groups in order they can use the Web Management Console. The roles assigned to a certain user determine what pages that user can access in the Web Management Console and wheter she can only read, or modify as well values on a page.

The field ASSIGN TO ROLES in the *Add/assign new user(s)* and *Modify user* dialogs lists all the roles that are assigned to the user.

The following is the role assignment policy:

1. At least one role must be assigned to a user, LDAP group or Active Directory group
2. Optionally multiple different roles can be assigned

   1. In this case the most permissive available right applies to each function.

Info

For details about the permissiveness of roles see the [Roles tab](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-roles) section.

Example:

| Roles assigned | Effective permissions |  |
| --- | --- | --- |
|  | Read only permission | No permission |
| security_auditor | Config history, Global settings |  |
| help_desk | Global settings | Config history |
| security_admin AND security_auditor | Config history, Global settings |  |

### [Delete user](/docs/mdicap/v5.15.0/configuration/user-management#delete-user)

Note

Active sessions of the deleted user will be aborted at the time of the next interaction with the server.

## [Special user accounts](/docs/mdicap/v5.15.0/configuration/user-management#special-user-accounts)

Some user accounts are reserved in the product for system internal usage. These accounts are documented in this section.

Warning

The special accounts documented in this section are for internal usage. Do not directly modify these accounts through the user management functions cause it may give unexpected results.

### [SYSTEM/management account](/docs/mdicap/v5.15.0/configuration/user-management#systemmanagement-account)

The SYSTEM/management account is reserved for [*Central Management*](https://onlinehelp.opswat.com/centralmgmt/).

When the product is connected to *Central Management* as a managed instance, then this account is automatically created by *Central Management* at the first successful connection with the following parameters:

| Username | Password | Name | Email | Roles | User directory |
| --- | --- | --- | --- | --- | --- |
| management | *N/A* | Metadefender Central Management | management@localhost | Administrators | SYSTEM |

All consecutive connection attempts are performed by *Central Management* using the SYSTEM/management account.

## [Roles tab](/docs/mdicap/v5.15.0/configuration/user-management#roles-tab)

Roles can be assigned to users. This simplifies controlling permissions. The Roles tab lists the existing roles in the system.

## [Default roles](/docs/mdicap/v5.15.0/configuration/user-management#default-roles)

After installation the following default roles are created with the following parameters:

| Rolename | Display name | Default member username | Permissions |
| --- | --- | --- | --- |
| admin | Administrators | admin | Full on all functions |
| security_admin | Security administrators |  | Full on ICAP history, Security rules, Server profiles and Global settings |
| security_auditor | Security auditor |  | Read-only on all functions |
| help_desk | Help desk |  | Read-only on ICAP history, Security rules, Server profiles and Global settings |

## [Permissions](/docs/mdicap/v5.15.0/configuration/user-management#permissions)

Each role has a set of rights associated to it. Each of these rights represent the level of access to the appropriate function of the MetaDefender product's Web Management Console.A right can be set to one of three different values:

| Right | Description |
| --- | --- |
| NONE | Users with this effective right have no right to access the given function of the MetaDefender product's Web Management Console. The menu belonging to the function is not displayed. |
| READ-ONLY | Users with this effective right are granted to access the given function for observation purposes only. Users of this role can, however, not effectuate any modifications or any change to the function. |
| FULL | Users with this effective right have full access to the given function, including viewing any data belonging to it and modifying its configuration. |

### [Effective right](/docs/mdicap/v5.15.0/configuration/user-management#effective-right)

A single user may have multiple roles assigned to it. There may be cases, when one of the assigned roles of the user would prohibit, while the other assigned role of the user would permit a certain function. In this case the more permissive right will be effective.

See section [Assign roles to a user, LDAP group or Active Directory group](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-assignroles) for details about assigning multiple roles to a single user.

## [Functions](/docs/mdicap/v5.15.0/configuration/user-management#functions)

Besides listing existing roles the Roles tab provides the following functions:

- Add new role
- Modify (and view) existing role
- Delete existing role

Note

The default role *Administrators* can not be deleted or modified.

### [Modify role](/docs/mdicap/v5.15.0/configuration/user-management#modify-role)

Warning

The users' permissions won't be modified during the session, even if one of their roles are modified in the meantime.

For example:

1. A user is assigned to the role *security_admin* and has Full permissions on C_onfig history_
2. She can see *Config history* changes
3. During her session the *Config history* permissions are set to *None* for the *security_admin* role.
4. The logged in user can still select the *Config history* menu and can see the configuration changes there.

Then new permissions will be effective only after a logout and new login.

Delete role

Note

A role can not be deleted as long as it is assigned to any user.

As a consequence deleting a role can not affect active sessions of users.

## [User directories tab](/docs/mdicap/v5.15.0/configuration/user-management#user-directories-tab)

Users can be organized into separate user directories. User directories help to enforce the following login policies:

1. [Lockout after a number of consecutive failed login attempts](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-userdirectorypolicy)
2. [Disable logins for all users of the user directory](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-disableuserdirectory)

The Users tab lists the existing user directories in the system.

## [Default user directories](/docs/mdicap/v5.15.0/configuration/user-management#default-user-directories)

After installation two default user directories are created with the following parameters:

| User directory type | Name | Number of failed logins before lockout | Lockout time [minutes] | Enable enhanced password policy | Purpose |
| --- | --- | --- | --- | --- | --- |
| Local | LOCAL | 3 | 5 | False | This user directory can be used to add local user accounts to the system. |
| Local | SYSTEM | 0 | 0 | False | This user directory is used to add special, (e.g. machine-to-machine) user accounts to the system. This user directory is for system internal use, do not modify (delete, assign users, etc.) it manually. |

Three types of user directories exist in MetaDefender products:

1. Local
2. LDAP
3. Active Directory

## [Local type user directories](/docs/mdicap/v5.15.0/configuration/user-management#local-type-user-directories)

Local type user directories allow creating users that locally exist on the MetaDefender product.

To protect user accounts of a local user directory against brute force password breaking attacks, the following policy settings may be applied to each local type user directory:

- NUMBER OF FAILED LOGINS BEFORE LOCKOUT: After this number of consecutive failed login attempts the account gets locked.
- LOCKOUT TIME [MINUTES]: The account remains locked for the given minutes.

  - When the lockout time elapses, the account lock gets released automatically.
  - Users with appropriate permission may release the account lock earlier using the [RELEASE LOCKOUT button](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-unlock).
- ENABLE ENHANCED PASSWORD POLICY: If enabled, then the following policy is enforced for new passwords:

Info

Enhanced password complexity policy

- The password must be at least 8 characters long;
- The password must contain at least one of each

  - Upper case Latin letter character ([A-Z]),
  - Lower case Latin letter character ([a-z]),
  - Arabic numeral character ([0-9]);
- The password must not contain the user name.
## [Active Directory type user directories](/docs/mdicap/v5.15.0/configuration/user-management#active-directory-type-user-directories)

Active Directory type user directories allow users defined in an Active Directory to access the MetaDefender product.

Active Directory type user directories do not provide the possibility to define login policies; these policies may be defined in the Active Directory directly.

## [LDAP type user directories](/docs/mdicap/v5.15.0/configuration/user-management#ldap-type-user-directories)

LDAP type user directories allow users defined in an LDAP directory to access the MetaDefender product.

LDAP type user directories do not provide the possibility to define login policies; these policies may be defined in the LDAP directory directly.

## [Functions](/docs/mdicap/v5.15.0/configuration/user-management#functions)

Besides listing existing user directories the USER DIRECTORIES tab provides the following functions:

- Add new user directory
- Modify (and view) existing user directory
- Delete existing user directory
- Enable or disable existing user directory
- Unlock locked accounts

### [Add new Local type user directory](/docs/mdicap/v5.15.0/configuration/user-management#add-new-local-type-user-directory)

Click the ADD NEW USER DIRECTORY button and select *Local* in the USERDIRECTORY TYPE drop down list.

For explanation of the NUMBER OF FAILED LOGINS BEFORE LOCKOUT and LOCKOUT TIME [MINUTES] fields read the [Local type user directories](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-userdirectorypolicy) section.

### [Add new LDAP type or Active Directory type user directory](/docs/mdicap/v5.15.0/configuration/user-management#add-new-ldap-type-or-active-directory-type-user-directory)

1. Click the ADD NEW USER DIRECTORY button and select *LDAP* or *Active Directory* in the USERDIRECTORY TYPE drop down list respectively. Learn more about the [differences between LDAP and Active Directory type user directories](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-differences).
2. Multiple LDAP or Active Directory servers can be configured to provide high availability of the directory services.

   1. Server preference:

      1. The configured servers are taken for a connection attempt in a top-bottom fashion.

2. Failover conditions

1. If the connection to a certain LDAP or AD server fails (for a reason other then authentication error) then

2. The next server in the preference order is attempted.

3. Server properties The following properties must be specified for each LDAP or AD server:

- SERVER PORT: The TCP port on which the directory service is listening
- ENCRYPTION: What kind of encryption to use when establishing the connection
- None: No encryption, communication on a clear-text channel

Warning

As long as ENCRYPTION field is set to *None* there is no encryption used between the MetaDefender product and the LDAP or Active Directory server. All passwords and other information are sent clear-text over the network.

Use *StartTLS* or *SSL* as ENCRYPTION whenever possible.

2. StartTLS: The connection is established on a clear-text channel, then upgraded to TLS (TLS over LDAP)

3. SSL: The connection is established on a TLS encrypted channel (LDAP over TLS)

Note

For *StartTLS* and *SSL* type encrypted connections the LDAP or Active Directory server must authenticate itself with a certificate that's validity can be verified by the MetaDefender product. This can happen in basically two ways:

1. Trusted certificate: the certificate's root certificate is issued by a trusted certificate authority (e.g. Comodo, Symantec, GoDaddy, GlobalSign, IdenTrust, DigiCert, StartCom, Entrust, Trustwave, Verizon, etc.) These root certificates are usually pre-installed in modern operating systems and as a result can be verified by the MetaDefender product.
2. Self-signed certificate: the certificate (or it's root certificate) is added to the system as a trusted root certificate. For details about adding a certificate as a trusted root certificate, see the manuals of the operating system of your MetaDefender product. For your convenience here are the necessary commands for Windows and some Linux distributions (the path to the self signed certificate file is C:\Path\To\certificate.crt or /path/to/certificate.crt on Windows or Linux respectively):

**Windows**

`> certutil -addstore -f "ROOT" C:\Path\To\certificate.crt`

**Ubuntu/Debian**

> sudo cp -f certificate.crt /usr/local/share/ca-certificates

> sudo update-ca-certificates

**CentOS/RHEL**

#install ca-certificates

> sudo yum install -y ca-certificates

#install certificate

> cp -f certificate.crt /etc/pki/ca-trust/source/anchors/

> sudo update-ca-trust enable

> sudo update-ca-trust extract

3. Select whether to authenticate or not at the time of the bind request. Authentication at the time of the bind request is an additional security control for directory services like host based authentication at SSH. It may or may not be required by the server.

   1. Selecting the ANONYMOUS BIND option will try to attempt to bind to the directory service with no username and password.

Info

If the ANONYMOUS BIND option is selected, then the values specified for BIND USERNAME and BIND PASSWORD are ignored, their text fields are disabled.

Note

Some LDAP and Active Directory servers may be configured to not permit anonymous bind requests .

2. Specify the BIND USERNAME and BIND PASSWORD values. These values must be the name as DN (distinguished name) and password of a user who has permissions to do searches in the directory.

Warning

As long as TLS is not configured for the Web Management Console, passwords are sent clear-text over the network. For details see [Transport Layer Security](/docs/mdicap/v5.15.0/configuration/user-management#transport-layer-security).

4. The USER BASE DN and the GROUP BASE DN values should provide the entries in the LDAP or Active Directory tree where user and group entity lookups should be started.

Info

For further LDAP specific property details see [LDAP attributes](/docs/mdicap/v5.15.0/configuration/user-management#ldap-attributes).

For further Active Directory specific property details see [Active Directory attributes](/docs/mdicap/v5.15.0/configuration/user-management#active-directory-attributes).

5. Click the TEST button to test the LDAP or Active Directory settings. If the test succeeds then the user directory can be added to the list with the ADD button.

#### [Differences between LDAP and Active Directory type user directories](/docs/mdicap/v5.15.0/configuration/user-management#differences-between-ldap-and-active-directory-type-user-directories)

From MetaDefender products' perspective LDAP directories are supersets of Active Directory directories. In other words, an Active Directory configuration can be specified using LDAP user directory type, setting certain properties to predefined values.

The following properties must be set to the following values to implement an Active Directory type user directory with LDAP type user directory

| Property | Value |
| --- | --- |
| USER OBJECT CLASS | user |
| USER ACCOUNT ATTRIBUTE | samaccountname |
| USER EMAIL ATTRIBUTE | mail |
| USER DISPLAY NAME ATTRIBUTE | cn |
| GROUP OBJECT CLASS | group |
| GROUP ACCOUNT ATTRIBUTE | samaccountname |
| GROUP DISPLAY NAME ATTRIBUTE | cn |

### [Delete user directory](/docs/mdicap/v5.15.0/configuration/user-management#delete-user-directory)

Note

Users of the deleted user directory will be deleted as well. As a consequence: active sessions of the users of the deleted user directory will be aborted at the time of the next interaction with the server (for details see [Delete user](/docs/mdicap/v5.15.0/configuration/user-management#src-4864724_id-3.3Usermanagement-deleteuser)).

### [Enable or disable user directory](/docs/mdicap/v5.15.0/configuration/user-management#enable-or-disable-user-directory)

To disable a user directory hover over the user directory's entry in the list and click the *Disable user directory* icon.

When disabling a user directory, all users that are assigned to it will be blocked from logging in.

Note

Active sessions of users of the disabled user directory will not be aborted. The user will be blocked at the time of the next login.

When a user directory is disabled then the user directory's entry in the list displays the **x** mark. To enable the user directory click the *Enable user directory* icon.

### [Unlock locked accounts](/docs/mdicap/v5.15.0/configuration/user-management#unlock-locked-accounts)

All the locked user accounts that belong to a Local type user directory, can be released clicking the RELEASE LOCKOUT button.

## [Transport Layer Security](/docs/mdicap/v5.15.0/configuration/user-management#transport-layer-security)

Transport Layer Security (TLS) is a cryptographic protocol that provides communications security over a computer network. Websites, like the Web Management Console, are able to use TLS to secure all communications between their servers and web browsers.

The TLS protocol aims primarily to provide confidentiality (privacy) and data integrity between two communicating computer applications.

For instructions to set up TLS see [3.2 Configuring TLS](/docs/mdicap/v5.15.0/configuration/configuring-tls)

## [LDAP attributes](/docs/mdicap/v5.15.0/configuration/user-management#ldap-attributes)

For further details see [3.3.3 LDAP attributes](/docs/mdicap/v5.15.0/configuration/ldap-attributes)

## [Active Directory attributes](/docs/mdicap/v5.15.0/configuration/user-management#active-directory-attributes)

For further details see [3.3.2 Active Directory attributes](/docs/mdicap/v5.15.0/configuration/active-directory-attributes)

## [Notes](/docs/mdicap/v5.15.0/configuration/user-management#notes)

The currently logged on user can not disable the user directory to which her account is assigned to. For example the *admin* user can not disable the LOCAL user directory.

The currently logged on user can not delete the following:

- Her own user account. For example the *admin* user can not delete the *admin* user account.
- The user directory to which her account is assigned to. For example the *admin* user can not delete the LOCAL user directory.
