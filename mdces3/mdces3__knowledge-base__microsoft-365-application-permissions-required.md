<!-- source: https://www.opswat.com/docs/mdces3/knowledge-base/microsoft-365-application-permissions-required -->

# Microsoft 365 Application permissions

Summarize Page
## [Overview](/docs/mdces3/knowledge-base/microsoft-365-application-permissions-required#overview)

**MetaDefender** **Cloud Email Security**™ (MDCES) requires specific Microsoft Graph and Office 365 Exchange Online API permissions to operate correctly and securely within your Microsoft 365 environment.

When installing and granting consent to MDCES, your administrator will authorize the following permissions. The table below summarizes each permission and provides a brief description of its purpose.

| API/Permission name | Type | Description |
| --- | --- | --- |
| **Microsoft Graph** |  |  |
| Contacts.Read | Application | Allows MDCES to read contact information in all mailboxes (used for email processing and routing logic). |
| Directory.Read.All | Application | Allows MDCES to read directory data (users, groups, domains, and more) to determine protection scope and apply mail flow rules & policies. |
| Domain.Read.All | Application | Allows MDCES to read the domains in your tenant to support domain-based routing and configuration. |
| Group.Read.All | Application | Allows MDCES to read all groups (used for applying policies to specific groups). |
| GroupMember.Read.All | Application | Allows MDCES to read group memberships (used to apply policies to group members). |
| Mail.ReadWrite | Application | Allows MDCES to read & write email content in mailboxes for security analysis when protection mode is enabled. |
| ProfilePhoto.Read.All | Application | Allows MDCES to read profile photos of users and groups (used for enhancing the admin portal UX). |
| User.Read | Delegated | Allows MDCES to sign in and read the profile of the signed-in user (basic sign-in and profile read functionality). |
| User.Read.All | Application | Allows MDCES to read all users' full profiles (used to support user-based policies and visibility). |
| **Office 365 Exchange Online** |  |  |
| Exchange.Manage* | Delegated | Allows MDCES to manage Exchange configuration (e.g., mail flow rules, connectors) when performing setup or adjustments. |

** Only used when selecting automatic integration mode*

### [**Why These Permissions Are Required**](/docs/mdces3/knowledge-base/microsoft-365-application-permissions-required#why-these-permissions-are-required)

MDCES uses these permissions to:

- Apply and manage Exchange mail flow rules and connectors
- Apply protection policies based on users, groups, and domains
- Analyze email content for security threats
- Support monitoring mode (BCC email copy) and protection mode (email routing)
- Provide visibility and control via the MDCES admin portal
- Ensure seamless integration with your Microsoft 365 tenant
