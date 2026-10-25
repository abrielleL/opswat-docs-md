<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/user-based-licensing -->

# User based licensing

View as Markdown Ask ChatGPT about this page Ask Claude about this page No processing for unlicensed users

Email Gateway Security won’t apply any processing (not even bypassed disclaimers, for details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy)) to emails that are to be delivered to email addresses that are not licensed.

## [Synchronization to Active Directory](/docs/mdemail/6.4.2/operating/user-based-licensing#synchronization-to-active-directory)

With synchronization users that have been removed from the Active Directory can get unlicensed from Email Gateway Security.

### [Scheduled](/docs/mdemail/6.4.2/operating/user-based-licensing#scheduled)

For details see [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings).

### [On-demand](/docs/mdemail/6.4.2/operating/user-based-licensing#on-demand)

To synchronize licensed users with Active Directory click the *Synchronize licensed users* button under **License**.

## [Automated user management](/docs/mdemail/6.4.2/operating/user-based-licensing#automated-user-management)

To manage users automatically in Email Gateway Security we recommend the following:

1. Assign license to users automatically (for details see [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings))
2. Synchronize licensed users with Active Directory (for details see [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings))

User management in Active Directory

Using the settings above users can be managed in Active Directory. Only the exceptions need to be managed in Email Gateway Security directly.
