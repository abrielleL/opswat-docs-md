<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-active-directory--lightw -->

# How do I troubleshoot issues related to Active Directory, Lightweight Directory Access Protocol, and Single Sign-On?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

When configuring authentication sources for MetaDefender Managed File Transfer (MFT), you may encounter some issues related to Active Directory (AD), Lightweight Directory Access Protocol (LDAP), or Single Sign-On (SSO). Here are some common issues and how to troubleshoot them.

## [Unable to log in to the same user account with both AD and SSO](/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-active-directory--lightw#unable-to-log-in-to-the-same-user-account-with-both-ad-and-sso)

Issue: When setting up both AD and SSO integration for MFT, you may notice that when a user logs in with AD or SSO, their user account is different and not the same account (i.e. 1 user account for AD, and 1 user account for SSO).

Solution: To authenticate into an existing AD synced user account through SSO, the SSO integration must return claims containing the same username that a user through AD sync already exists.

The SSO claims for username are the following:

1. upn
2. preferred_username
3. name

If there is already an AD synced user with the resolved username, the SSO login will authenticate into that user. For example:

- An AD user named “user” is synced in MFT. SSO returns username claim “user” → SSO will authenticate into existing AD user.
- An AD user named “user” is synced in MFT. SOO returns username claim “user@domain.com” → SSO will authenticate into a different user account.

## [Unable to log in to SSO after setting up AD of the same source](/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-active-directory--lightw#unable-to-log-in-to-sso-after-setting-up-ad-of-the-same-source)

Issue: If SSO was configured and used before configuring an active directory pointing to the same source, the MFT system cannot distinguish between the two occurrences of the same user (local user created by SSO integration, and active directory user created by AD integration).

Solution: Delete all local users created through the SSO integration before logging in. After deleting the local user occurrence, both SSO and AD logins will direct to the active directory user.

## [AD users/groups are missing](/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-active-directory--lightw#ad-usersgroups-are-missing)

Issue: After finalizing AD setup and synchronizing AD users/groups, some users/groups are missing and cannot be logged in.

Solution: By default, if no AD organizational unit (OU) and security group are specified during steps 4 and 5 of the AD setup process, all users will be licensed to use MFT. However, if some OUs and security groups are specified, only users in those groups will be licensed to use MFT.

If AD users/groups are missing, please go back to steps 4 and 5 of AD setup and review your include/exclude list according to this [documentation page](/docs/mdmft/v3.11.5/configuration/organizational-units-and-groups-configuration).

## [“Something unexpected happened” when syncing AD](/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-active-directory--lightw#something-unexpected-happened-when-syncing-ad)

Issue: After finalizing AD configuration and start to sync, the error “Something unexpected happened” occurs and the process fails.

Solution: This type of issue that occurs during AD synchronization is mostly due to configuration mistakes. To fix this, please go back to [User Directory Account settings page and review the configuration](/docs/mdmft/v3.11.5/configuration/account-settings).

## [“Invalid OAuth authorization request was received” when logging in with SSO](/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-active-directory--lightw#invalid-oauth-authorization-request-was-received-when-logging-in-with-sso)

Issue: When logging in with SSO (in this case AD FS), the following error appears: Error details: MSIS9224: An invalid OAuth authorization request was received. The received ‘redirect_uri’ parameter is not a valid registered redirect URI for client identifier ‘…’.

Solution: In this case, the URL used to access (and consequently, the SSO redirect endpoint) hasn’t been registered as a redirect URI for the application in AD FS management console.

Take the above example:

- In step #5 of the **Application Group setup on AD FS management console**, only <https://mft.ciplab.local:8010/vault_rest/authenticate-sso> is added as a Redirect URI.
- However, when an end user is accessing MFT, they might also be using the URL [https://ciplab-pc02.ciplab.local:8010](https://ciplab-pc02.ciplab.local:8010/) instead, resulting in the error message when logging in with SSO:

To fix this issue, add **any additional redirect URI** that an end user might encounter when logging in with SSO, like so:

Support:

For assistance with Troubleshooting issues related to Authentication Sources in MetaDefender Managed File Transfer, please follow the instructions at [Creating Support Packages](https://www.opswat.com/docs/mdmft/troubleshooting/how-to-create-support-package) before submitting a [Support Ticket](https://my.opswat.com/support).
