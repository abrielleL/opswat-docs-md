<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/change-user-password -->

# Change user password

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The current user can change their password under **Settings -> Profile ->** **Password**

Note

The password change option is only available for users of *Local* type user directories.

Changing passwords in LDAP or Active Directory services is not supported.

Warning

If enhanced password policy is enabled for the user directory this user belongs to then the new password must fulfil the password complexity requirements listed at the [Local type user directories](/docs/mdicap/v5.15.0/configuration/change-user-password#src-4864728_id-3.3.1Changeuserpassword-userdirectorypolicy) section.

## [Important notes](/docs/mdicap/v5.15.0/configuration/change-user-password#important-notes)

Warning

As long as TLS is not configured for the Web Management Console, passwords are sent clear-text over the network. To set up TLS see [Configuring TLS](/docs/mdicap/v5.15.0/configuration/configuring-tls).
