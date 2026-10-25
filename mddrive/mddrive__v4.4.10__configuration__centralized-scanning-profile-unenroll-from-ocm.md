<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-unenroll-from-ocm -->

# Centralized Scanning Profile - Unenrolling from OPSWAT Central Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Unenrolling removes the Centralized Profile from a MetaDefender Drive. The profile loses its approver and its security code. You can do this from OPSWAT Central Management (OCM).

To set the profile up, see [Centralized Scanning Profile - Provisioning from OPSWAT Central Management](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-provision-from-central-management).

## [Unenroll the Centralized Profile](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-unenroll-from-ocm#unenroll-the-centralized-profile)

1. In OPSWAT Central Management, open the drive's settings and open **Centralized Profile Settings**. The dialog shows the assigned approver.
2. Select **Unenroll**.
3. In the **Unenroll Centralized Profile** dialog, read the message: "Are you sure you want to unenroll this Centralized Profile? This profile will lose its approver and security code."
4. Select **Unenroll** to confirm. Select **Cancel** to keep the profile.

## [After you unenroll](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-unenroll-from-ocm#after-you-unenroll)

- The profile no longer has an approver or a security code.
- Remove the drive's entry from the approver's authenticator app.
- To use the profile again, enroll it again. See [Provisioning from OPSWAT Central Management](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-provision-from-central-management).

## [Related pages](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-unenroll-from-ocm#related-pages)

- [Centralized Scanning Profile](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile)
- [Centralized Scanning Profile - Provisioning from Drive Toolkit](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-provision-from-toolkit)
- [Manage MetaDefender Drives with OPSWAT Management](/docs/mddrive/v4.4.10/configuration/managing-drives-with-central-management)
