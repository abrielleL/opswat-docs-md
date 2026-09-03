<!-- source: https://www.opswat.com/docs/mdmft/configuration/active-directories -->

# Active Directories

Summarize Page    Connect to Cursor Connect to VS Code

Integrates MetaDefender Managed File Transfer™ with the organization's Active Directory or LDAP Directory to synchronize users.

The account used by MetaDefender Managed File Transfer™ to connect to Active Directory or LDAP Directory needs read permissions in the organization's User Directory.

## [Active Directory Integration Process](/docs/mdmft/configuration/active-directories#active-directory-integration-process)

Click the "Add User Directory" button to add a new user directory, which will prompt the "User Directory Account Settings" screen.

### [Pre-Setup Considerations for Active Directory Integration](/docs/mdmft/configuration/active-directories#pre-setup-considerations-for-active-directory-integration)

Before proceeding with the active directory setup, consider the following:

Info

If Single Sign-On (SSO) is configured and uses the same source as a configured active directory, a user logging in with SSO will have roles assigned based on the active directory configuration.

For example, if an email address is not registered as an administrator in the SSO configuration, but the user's active directory group is set as an administrator group, the user will have administrator privileges.

Warning

If SSO was configured and used before configuring an active directory pointing to the same source, all local users created through SSO must be deleted before they can log in. This is because the system cannot distinguish between the two occurrences of the same user.

After deleting the local user variant, both SSO and active directory logins will direct to the active directory user.

Warning

When a local MetaDefender Managed File Transfer™ user and an external directory user *share the same email address*, the login mechanism first tries to match the external directory for the credentials and then falls back to authenticate the local user.

Info

Adding two Domain Controller (DC) servers for the same domain (for redundancy purposes) is not yet supported. Multiple DCs for different domains are supported.

---

Follow the [Account Settings](/docs/mdmft/configuration/account-settings) page for information on how to configure the account settings.
