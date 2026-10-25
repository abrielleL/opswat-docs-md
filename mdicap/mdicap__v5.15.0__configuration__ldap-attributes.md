<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/ldap-attributes -->

# LDAP attributes

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This page contains tips on how to obtain the BIND USERNAME, the USER BASE DN and GROUP BASE DN attributes, the LDAP USER SCHEMA SETTINGS and the LDAP GROUP SCHEMA SETTINGS when creating an LDAP type user directory.

Note

Normally a domain administrator should provide these values.

Success

The BIND USERNAME, the USER BASE DN and GROUP BASE DN attributes must be expressed using a valid LDAP syntax.

## [Bind username](/docs/mdicap/v5.15.0/configuration/ldap-attributes#bind-username)

Normally an LDAP administrator should provide these values, however there is a way to get the BIND USERNAME as an LDAP DN, that is needed for the product to do searches in the directory information tree. To get this information, there is, however, some information about the LDAP tree, that must be known in advance:

| LDAP property | Notes | Example |
| --- | --- | --- |
| DN of the LDAP tree node that has the bind user as a child. | This will be the base for the search. If selected improperly then the search may be very slow or won't find the appropriate user. | ou=users,dc=test |
| Attributes and their values that uniquely identify the bind user account. | These will be used as filter conditions to find the proper user. | uid=bind |

To find the bind user, perform the following steps:

1. Log on to a Windows machine that has connectivity to the LDAP server
2. Choose a user that is intended for this purpose (ie: has rights to do searches in the tree)
3. Open the LDP.exe tool with elevated rights (Run as Administrator)
4. Assuming the example properties above are correct, do the following search:

Note! The search above will return the attributes for the user in question:

The DN should look something like this:

`cn=bind,ou=users,dc=test`

Please note, the actual user DN will most probably look completely different than the above example, as it depends on the structure of the underlying directory information tree in the LDAP server.

Info

On non-server Windows machines the LDP.exe tool can be obtained with installing the [Remote Server Administration Tools (RSAT)](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

## [User base and group base DN](/docs/mdicap/v5.15.0/configuration/ldap-attributes#user-base-and-group-base-dn)

Once the bind user DN is obtained, an easy way to get the DNs for the user and group searches is by taking all the DC parts of the user DN and leaving the rest out. Using the examples above the result DN will be the following:

dc=testNote

Please note that using only DC components for the user/group DNs may result in searches to be executed from the top of the directory information tree and potentially slow down the LDAP server responses a lot and thus have an impact on the MetaDefender product's password validation. The rule of thumb here is that the more specific the user/group DN, the faster the server response is.

Note

Please also note that users and groups may reside in different parts of the directory information tree, as a consequence applying the same, more specific DN both as USER BASE DN and GROUP BASE DN may cause the MetaDefender product to not find group accounts in the directory information tree. So these DNs should be chosen carefully.

## [LDAP user schema settings](/docs/mdicap/v5.15.0/configuration/ldap-attributes#ldap-user-schema-settings)

Similarly to the search in [Bind username](/docs/mdicap/v5.15.0/configuration/ldap-attributes#bind-username), we can search for users and determine the appropriate values.

## [Example](/docs/mdicap/v5.15.0/configuration/ldap-attributes#example)

1. Let's assume the following search is executed:

2. That gives the following result:

3. The LDAP USER SCHEMA SETTINGS may be the following:

| User schema setting | LDAP attribute |
| --- | --- |
| USER OBJECT CLASS | user |
| USER ACCOUNT ATTRIBUTE | uid or samaccountname |
| USER EMAIL ATTRIBUTE | mail |
| USER DISPLAY NAME ATTRIBUTE | cn |

## [LDAP group schema settings](/docs/mdicap/v5.15.0/configuration/ldap-attributes#ldap-group-schema-settings)

Similarly to the search in [LDAP user schema settings](/docs/mdicap/v5.15.0/configuration/ldap-attributes#ldap-user-schema-settings), we can search for users and determine the appropriate values.
