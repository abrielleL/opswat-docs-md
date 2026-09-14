<!-- source: https://www.opswat.com/docs/mdemail/configuration/users -->

# Users

In this chapter we discuss only the users of the web management console of Email Gateway Security.

## [User directories](/docs/mdemail/configuration/users#user-directories)

Users can be organized into separate user directories in Email Gateway Security.

There are three types of user directories:

1. Local
2. Active Directory
3. LDAP
4. OpenID Connect (OIDC)
5. Security Assertion Markup Language (SAML)

### [Default user directory](/docs/mdemail/configuration/users#default-user-directory)

Email Gateway Security will look up a username in the top user directory in the list of user directories. For example, in the example below, the default user directory is the `LOCAL` user directory.

Reordering user directories

The order of the user directories can be set by drag and drop using the ⋮⋮⋮ icon in front of the user directory entry (when the drag and drop is active, the mouse pointer changes to ).

Log in to non-default user directory

To log in to a non-default user directory, the name of the user directory must prefix the user name, with a backslash `\` character separating the two: `<user directory name>\<username>` .

With the example of the image above, when the user `tramone` wants to log in to the user directory `AD` the username must be provided as `ad\tramone`.

## [Local type user directories](/docs/mdemail/configuration/users#local-type-user-directories)

Local type user directories allow creating web management console users that exist locally on the Email Gateway Security product.

To protect user accounts of a local user directory against brute force password breaking attacks, the account can be locked after the defined *Number of failed logins* for the configured *Lockout time*.

No Administrators lockout

Lockout is not applied to users in the Administrators role.

If *Enable enhanced password policy* is set then then the following policy is enforced for new passwords (new accounts and changed passwords of existing accounts):

Enhanced password complexity policy

- The password must be at least 12 characters long;
- The password must contain at least one of each

  - Upper case Latin letter character ([A-Z]),
  - Lower case Latin letter character ([a-z]),
  - Arabic numeral character ([0-9]);
- The password must not contain the user name.
- The password must not be among the [10k worst passwords](https://github.com/OWASP/passfault/blob/master/wordlists/wordlists/10k-worst-passwords.txt).
Enhanced password policy is default

Since Email Gateway Security version 5.6.1 the enhanced password policy is enabled by default for local type user directories.

### [Unlock locked accounts](/docs/mdemail/configuration/users#unlock-locked-accounts)

All the locked user accounts that belong to a Local type user directory, can be released clicking the RELEASE LOCKOUT button.

## [LDAP and Active Directory type user directories](/docs/mdemail/configuration/users#ldap-and-active-directory-type-user-directories)

Active Directory type user directories allow users defined in an Active Directory to access Email Gateway Security’s web management console.

Active Directory type user directories do not provide the possibility to define login policies; these policies may be defined in the Active Directory directly.

Risk of information leak

As long as the *Encryption* field is set to *None* there is no encryption used between Email Gateway Security and the LDAP or Active Directory server. All passwords and other information are sent clear-text over the network.

Use *StartTLS* or *SSL* as *Encryption* whenever possible.

With *Anonymous bind* you can set whether to authenticate or not at the time of the bind request. Authentication at the time of the bind request is an additional security control for directory services. It may or may not be required by the server.

The *Bind username* and *Bind password* values must be the name as DN (distinguished name) and password of a user who has permissions to do searches in the directory.

Risk of password leak

As long as TLS is not configured for the web management console, passwords are sent clear-text over the network. For details see [Configuration/Transport Layer Security](/docs/mdemail/configuration/transport-layer-security).

The *User base DN* and the *Group base DN* values should provide the entries in the Active Directory tree where user and group entity lookups should be started.

## [Single sign-on](/docs/mdemail/configuration/users#single-sign-on)

Failed to get user ready

The`{"err":"Failed to get user ready"}`error message is typically returned when the calculated value of the _User identified by _field is empty as the claims configured for the field return empty value.

Must be enabled first

After successful setup, single sign-on user directories must be enabled clicking the  button first before they can be started to be used.

When a single sign-on user directory is enabled, the login page will display the *Sign In with SSO* link which redirects to the identity provider’s logon page.

Local users

Users in *Local* type user directories (e.g. local administrators) can log in using the usual method: providing their credentials in the login page of Email Gateway Security.

### [OpenID Connect](/docs/mdemail/configuration/users#openid-connect)

The *Public URL* and *Login callback URL* values are given or generated by Email Gateway Security, while the *IDP Issuer URL*, the *Client ID* and *Client Secret* values are given by the identity provider.

#### [Okta example](/docs/mdemail/configuration/users#okta-example)

In Okta, in the left side menu select *Applications* / *Applications*, then click on *Create App Integration*.

As the *Sign-in method* select *OIDC - OpenID Connect*, and as _Application type _select *Web Application*.

Provide the properties as follows:

#### [Monosign example](/docs/mdemail/configuration/users#monosign-example)

The general settings have to be configured the same way as in the **Okta example** above.

One additional step to be made is adding the *profile* scope to the scope list, because Email Gateway Security expects it, when the configuration is downloaded using the `Configuration Url`.

After that, in the claim mapping, the claims need to be set up which you want to use in Email Gateway Security in the `User identified by` field. For example map `name` to `{{UserName}}`:

### [Security Assertion Markup Language (SAML)](/docs/mdemail/configuration/users#security-assertion-markup-language-saml)

The *Public URL* and *Login callback URL* values are given or generated by Email Gateway Security, while the *IDP Issuer URL* value is given by the identity provider.

#### [Okta example](/docs/mdemail/configuration/users#okta-example)

In Okta, in the left side menu select *Applications* / *Applications*, then click on *Create App Integration*.

As the *Sign-in method* select *SAML 2.0*.

Provide the properties as follows:

### [Role mapping](/docs/mdemail/configuration/users#role-mapping)

Role mapping helps assign the appropriate role(s) to users that log in using the SSO user directory. There are two modes:

1. Default role: all users that login through this user directory get the selected role assigned (e.g. all users of the SSO user directory in the image below get the `Administrators` role)

2. Role mapping: users get the role(s) according to the mapping settings

#### [Role mapping configuration](/docs/mdemail/configuration/users#role-mapping-configuration)

A role mapping configuration helps matching *claims* provided by the SSO provider and assign roles to users based on these claim matches.

For each role mapping configuration one claim (e.g. the email address of the user) can be specified. Then for this claim with different regular expressions, different roles can be assigned (in the below example users with domain `opswat.com` in their email addresses get the `Administrators` role while users with domain `metadefender.com` in their email addresses get the `Help desk` role).

#### [Role mapping evaluation](/docs/mdemail/configuration/users#role-mapping-evaluation)

Role mapping configurations then the regular expressions inside a certain role mapping configuration are evaluated in a top-down fashion with a first match strategy. When a certain regular expression is matching, the user gets the role(s) from this matching regular expression and no further regular expressions and role mapping configurations are evaluated.

## [Notes](/docs/mdemail/configuration/users#notes)

The currently logged on user can not **disable** the user directory to which her account is assigned to.

The currently logged on user can not **delete** the following:

- Her own user account. For example the *admin* user can not delete the *admin* user account.
- The user directory to which her account is assigned to. For example the *admin* user can not delete the LOCAL user directory.

## [Roles](/docs/mdemail/configuration/users#roles)

To simplify controlling permissions roles can be assigned to users. This way *Role-Based Access Control* (RBAC) can be accomplished.

### [Default roles](/docs/mdemail/configuration/users#default-roles)

After installation the following default roles are created with the following parameters:

|  |  |  |
| --- | --- | --- |
| **Name** | **Display name** | **Permissions** |
| admin | Administrators | Full |
| security_admin | Security administrators | Full on Email History, Quarantine, Failed Emails, Refused Emails, Security rules, Server profiles, Quarantine reports and Global settings functions |
| security_auditor | Security auditor | Read-only on all functions |
| help_desk | Help desk | Read-only on Email History, Security rules, Server profiles and Global settings functions |

## [Permissions](/docs/mdemail/configuration/users#permissions)

Each role has a set of rights associated to it. Each of these rights represent the level of access to the appropriate function of Email Gateway Security’s web management console. A right can be set to one of three different values:

|  |  |
| --- | --- |
| **Right** | **Description** |
| NONE | Users with this effective right have no right to access the given function of the MetaDefender product's Web Management Console. The menu belonging to the function is not displayed. |
| READ-ONLY | Users with this effective right are granted to access the given function for observation purposes only. Users of this role can, however, not effectuate any modifications or any change to the function. |
| FULL | Users with this effective right have full access to the given function, including viewing any data belonging to it and modifying its configuration. |

Permissions for ongoing sessions

The users' permissions won't be modified during the session, even if one of their roles are modified in the meantime.

For example:

1. A user is assigned to the role *security_admin* and has Full permissions on C_onfig history_
2. She can see *Config history* changes
3. During her session the *Config history* permissions are set to *None* for the *security_admin* role.
4. The logged in user can still select the *Config history* menu and can see the configuration changes there.

Then new permissions will be effective only after a logout and new login.

### [Effective right](/docs/mdemail/configuration/users#effective-right)

A single user may have multiple roles assigned to it. There may be cases, when one of the assigned roles of the user would prohibit, while the other assigned role of the user would permit a certain function. In this case the more permissive right will be effective.

## [Users and groups](/docs/mdemail/configuration/users#users-and-groups)

Under **User Management > Users** accounts can be configured to have access to Email Gateway Security’s web management console.

## [Users in Local user directories](/docs/mdemail/configuration/users#users-in-local-user-directories)

The field *Roles* lists all the roles that are assigned to this user. For details see the *Roles* section.

Risk of password leak

As long as TLS is not configured for the web management console, passwords are sent clear-text over the network. For details see [Configuration/Transport Layer Security](/docs/mdemail/configuration/transport-layer-security).

Enhanced password policy

If *Enable enhanced password policy* is set for the user directory this user belongs to then the new password must fulfill the password complexity requirements listed at the *Local type user directories* section.

### [API keys](/docs/mdemail/configuration/users#api-keys)

The *Apikey* value provides access to the product's REST API for the user under editing with no authentication. If no such functionality is needed for the user then this field can be left blank.

There are two methods to create an API key for a user:

1. Generate the API key by using GENATE button next to the *Apikey* field,
2. Manually enter the API key value; it must match the following criteria:

API key validation criteria

- The length of the API key must be exactly 36 characters.
- It must contain numeric and lower case *a*, *b*, *c*, *d*, *e* and *f* letter characters only (e.g. "1x2y3z..." is invalid because of the *x*, *y* and *z* characters).
- It must contain at least 10 lower case *a*, *b*, *c*, *d*, *e* or *f* letter characters.
- It must contain at least 10 numeric characters.
- It is allowed to contain at most 3 consecutive lower case letter characters (e.g. "abcd1a2b3c..." is invalid because of the four consecutive letters).
- It is allowed to contain at most 3 consecutive numeric characters (e.g. "1234a1b2c3..." is invalid because of the four consecutive numeric characters).
## [Users in LDAP or Active Directory directories](/docs/mdemail/configuration/users#users-in-ldap-or-active-directory-directories)

To add a new user from an LDAP or Active Directory type directory, select *User* as the *Account type*.

Provide the name of the account in the *Account name* field and click the SEARCH button to look up the account in the LDAP or Active Directory. If the lookup succeeds then the *Display name* and the *Distinguished name* fields are filled automatically.

Exact name required

Do provide the account name precisely. There is no functionality to look up similar names or partial matches.

## [Groups in LDAP or Active Directory type directories](/docs/mdemail/configuration/users#groups-in-ldap-or-active-directory-type-directories)

Purpose

The purpose of adding an LDAP or Active Directory group to the product is to assign role(s) to all the users in that LDAP or Active Directory group.

The users of the LDAP or Active Directory group can authenticate with their LDAP or Active Directory credentials in the product's web management console and will be assigned with the roles assigned to the group.

To add a new group from an LDAP type or Active Directory type user directory, select *Group* as the Account type.

Provide the name of the group in the *Account name* field and click the SEARCH button to look up the group in the LDAP or Active Directory. If the lookup succeeds then the *Display name* and the *Distinguished name* fields are filled automatically.

Exact name required

Do provide the group name precisely. There is no functionality to look up similar names or partial matches.

## [Delete user](/docs/mdemail/configuration/users#delete-user)

Active sessions

Active sessions of the deleted user will be aborted at the time of the next interaction with the server.

## [User settings](/docs/mdemail/configuration/users#user-settings)

Each user can customize their user account, language, time zone and list length on a single page for themselves.

To access the settings of the current user:

1. Click on the account name in the top right corner

2. In the drop down list click User Settings

## [Change password](/docs/mdemail/configuration/users#change-password)

The current user can change her password in the user settings.
