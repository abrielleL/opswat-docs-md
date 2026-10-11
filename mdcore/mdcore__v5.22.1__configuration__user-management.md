<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/user-management -->

# User management

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To manage the users of the MetaDefender Core go to the **User Management** menu in the Web Management Console.

The Users and groups tab lists the existing users in the system.

## [Default user](/docs/mdcore/v5.22.1/configuration/user-management#default-user)

After installation, a default local admin user needs to be created under LOCAL user directory following the welcome wizard

## [Special user accounts](/docs/mdcore/v5.22.1/configuration/user-management#special-user-accounts)

Some user accounts are reserved in the product for system internal usage. These accounts are documented in this section.

Warning

The special accounts documented in this section are for internal usage. Do not directly modify these accounts through the user management functions cause it may give unexpected results.

## [SYSTEM/management account](/docs/mdcore/v5.22.1/configuration/user-management#systemmanagement-account)

The SYSTEM/management account is reserved for [Central Management](https://docs.opswat.com/ocm)

When the product is connected to *Central Management* as a managed instance, then this account is automatically created by *Central Management* at the first successful connection with the following parameters:

| Username | Password | Name | Email | Roles | User directory |
| --- | --- | --- | --- | --- | --- |
| management | *N/A* | MetaDefender Central Management | management@localhost | Administrators | SYSTEM |

All consecutive connection attempts are performed by *Central Management* using the SYSTEM/management account.

## [Functions](/docs/mdcore/v5.22.1/configuration/user-management#functions)

Besides listing existing users and AD groups the **Users** tab provides the following functions:

- Add new user or AD group
- Modify (and view) existing user's or AD group's properties
- Delete existing user or AD group

## [Add new user from a Local type user directory](/docs/mdcore/v5.22.1/configuration/user-management#add-new-user-from-a-local-type-user-directory)

To add a new user from a Local type user directory click the ADD NEW USER button and select a Local type user directory in the USER DIRECTORY drop down list.

The field ASSIGN TO ROLES lists all the roles that are assigned to this user.

Warning

As long as TLS is not configured for the Web Management Console, passwords are sent clear-text over the network. To set up TLS see [Configuring TLS](/docs/mdcore/v5.22.1/configuration/enabling-https).

Warning

If enhanced password policy is enabled for the user directory this user belongs to, then the new password must fulfil the password complexity requirements listed on the User directories](/configuration/user-directories) page.

The APIKEY value provides access to the MetaDefender Core REST API for this user with no authentication. If no such functionality is needed for the user then this field can be left blank.

There are two ways to have an APIKEY for a user.

- generating by using *Generate* button next to APIKEY field,
- typing one that matches the following criterias:

  - The length of the API key must be exactly 36 characters.
  - It must contain numeric and lower case letter characters only [0-9a-z].
  - It must contain at least 10 lower case letter characters.
  - It must contain at least 10 numeric characters.
  - It is allowed to contain at most 3 consecutive lower case letter characters (e.g. "abcd1a2b3c..." is invalid).
  - It is allowed to contain at most 3 consecutive numeric characters (e.g. "1234a1b2c3..." is invalid).

Admin can also request to the users, they need to change the password on the First Login.

## [Add new users from an Active Directory type user directory](/docs/mdcore/v5.22.1/configuration/user-management#add-new-users-from-an-active-directory-type-user-directory)

To add a new user from an [Active Directory type user directory](/docs/mdcore/v5.22.1/configuration/user-directories) click the ADD NEW USER button and select an Active Directory type user directory in the USER DIRECTORY drop down list. Select USER as the ACCOUNT TYPE.

Provide the name of the account and click the *FIND ACCOUNT* button to look up the account in the Active Directory. If the lookup succeeds, then the ACCOUNT DISPLAY NAME and the DISTINGUISHED NAME fields are filled automatically.

Note

Do provide the account name precisely. There is no functionality to look up similar names or partial matches.

The field ASSIGN TO ROLES lists all the roles that are assigned to this user.

## [Add new group from an Active Directory type user directory](/docs/mdcore/v5.22.1/configuration/user-management#add-new-group-from-an-active-directory-type-user-directory)

Info

The purpose of adding an Active Directory group to the MetaDefender Core is to assign role(s) to all the users in that Active Directory group.

The users of the Active Directory group can authenticate with their Active Directory credentials in MetaDefender Core Web Management Console and will be assigned with the roles of the group.

To add a new group from an [Active Directory type user directory](/docs/mdcore/v5.22.1/configuration/user-directories) click the ADD NEW USER button and select an Active Directory type user directory in the USER DIRECTORY drop down list.

Note

Select GROUP as the ACCOUNT TYPE.

Provide the name of the group and click the *FIND ACCOUNT* button to look up the group in the Active Directory. If the lookup succeeds then the ACCOUNT DISPLAY NAME and the DISTINGUISHED NAME fields are filled automatically.

Note

Do provide the account name precisely. There is no functionality to look up similar names or partial matches.

The field ASSIGN TO ROLES lists all the roles that are assigned to all users of this group.

## [Assign roles to a user or an Active Directory group](/docs/mdcore/v5.22.1/configuration/user-management#assign-roles-to-a-user-or-an-active-directory-group)

Role(s) must be assigned to users and Active Directory groups in order they can use the Web Management Console.

The field ASSIGN TO ROLES in the **Add/assign new user(s)** and **Modify user** dialogs lists all the roles that are assigned to the user.

The following is the role assignment policy:

1. At least one role must be assigned to a user or Active Directory group
2. Optionally multiple different roles can be assigned

   1. In this case the highest available permission applies to each function. Example:

| Roles assigned | Effective permissions |  |
| --- | --- | --- |
|  | Full permission | Read only permission |
| security_admin | Scan history, Update history, Security rules, Security zones, Analysis workflows, Scan nodes, Engines, Update settings, Scan settings |  |
| security_auditor |  | All except External settings |
| security_admin AND security_auditor | Scan history, Update history, Security rules, Security zones, Analysis workflows, Scan nodes, Engines, Update settings, Scan settings | Config history, Data retention, User management, License |

## [Delete user](/docs/mdcore/v5.22.1/configuration/user-management#delete-user)

Note

Active sessions of the deleted user will be aborted at the time of the next interaction with the server.
