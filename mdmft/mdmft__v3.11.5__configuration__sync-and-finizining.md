<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/sync-and-finizining -->

# Synchronization and Finalizing Active Directory Setup

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Starting Synchronization](/docs/mdmft/v3.11.5/configuration/sync-and-finizining#starting-synchronization)

Click "Start synchronization" to start the synchronization process. This may take a while.

### [Over-Licensing Situation](/docs/mdmft/v3.11.5/configuration/sync-and-finizining#over-licensing-situation)

If over-licensing occurs, contact [OPSWAT Sales](https://www.opswat.com/contact) for a license upgrade or exclude more users from the [Role Mapping for Groups](/docs/mdmft/v3.11.5/configuration/role-mapping-for-groups) step.

Warning

Over-licensing can occur if new users are continuously added to your user directory. If this happens, a notification will appear, and an email notification will be sent to all administrators. New users will be unable to log in until the over-licensed state is resolved by either removing some users from the "Role Mapping For Groups" or requesting a license upgrade. Existing users can log in and upload files normally as long as they are not over-licensed.

Info

Refer to the [license page](/docs/mdmft/v3.11.5/configuration/license) to determine the permitted user count allowed by the license.

## [Run in Background](/docs/mdmft/v3.11.5/configuration/sync-and-finizining#run-in-background)

MetaDefender Managed File Transfer™ allows the user synchronization process to run in the background. Click "Run in background," and a progress popup will be displayed until the operation is complete.

## [Active Directory List](/docs/mdmft/v3.11.5/configuration/sync-and-finizining#active-directory-list)

After successfully configuring one or more user directories, the list will be displayed as follows:
