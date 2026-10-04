<!-- source: https://www.opswat.com/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm -->

# Centralized Scanning Profile - Provisioning from OPSWAT Central Management

You can set up the Centralized Scanning Profile of a MetaDefender Drive from OPSWAT Central Management (OCM). The profile assigns an approver to the drive. The approver adds the drive to a 2-FA authenticator app and provides the 6-digit code to operators who need to unlock restricted actions.

This page covers enrolling the profile. To remove it, see [Centralized Scanning Profile - Unenrolling from OPSWAT Central Management](/docs/mddrive/configuration/centralized-scanning-profile-unenroll-from-central-management).

## [Before you begin](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm#before-you-begin)

- A MetaDefender Drive that is enrolled in OPSWAT Central Management.
- The name of the approver.
- A 2-FA authenticator app on the approver's phone.

## [Enroll the Centralized Profile](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm#enroll-the-centralized-profile)

1. In OPSWAT Central Management, open the drive's settings and open **Centralized Profile Settings**.
2. In **Assigned Approver**, enter the approver's name. The field is filled in with `MDD-` followed by the drive's serial number. You can keep it or replace it.

   > **Note:** Once confirmed, this Approver Name cannot be changed.
3. Select **Confirm**. Select **Cancel** to leave without enrolling.
4. Click **Done** to finish. Cancel to leave.

## [After enrollment](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm#after-enrollment)

Once the profile is enrolled, **Centralized Profile Settings** shows the assigned approver and the **Security Code** buttons:

| Item | What it does |
| --- | --- |
| **Assigned Approver** | The approver's name. It cannot be changed. |
| **Show QR Code** | Shows the QR code and the key for the authenticator app. |
| **Show 6-Digit Code** | Shows the current 6-digit code. |
| **Unenroll** | Removes the profile. See [Unenrolling from OPSWAT Central Management](/docs/mddrive/configuration/centralized-scanning-profile-unenroll-from-central-management). |
| **Close** | Closes the dialog. |

## [Add the drive to an authenticator app](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm#add-the-drive-to-an-authenticator-app)

1. Select **Show QR Code**.
2. On the approver's phone, open the 2-FA authenticator app and scan the QR code. If you cannot scan, enter the key shown next to the QR code manually.
3. Select **Hide QR Code** when you are done.

## [Show the 6-digit code](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm#show-the-6-digit-code)

Select **Show 6-Digit Code** to see the current code without opening the authenticator app. The code refreshes automatically, and the dialog shows how many seconds are left. Select **Hide 6-Digit Code** to hide it.

You can show the QR code and the 6-digit code at the same time.

Give the code to the operator who is asking to unlock the drive. See [Centralized Scanning Profile - Unlock in MetaDefender Drive](/docs/mddrive/configuration/centralized-scanning-profile-bare-metal).

## [Related pages](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-ocm#related-pages)

- [Centralized Scanning Profile](/docs/mddrive/configuration/centralized-scanning-profile)
- [Centralized Scanning Profile - Provisioning from Drive Toolkit](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-toolkit)
- [Centralized Scanning Profile - Provisioning from Smart Touch](/docs/mddrive/configuration/centralized-scanning-profile-provision-from-smart-touch)
- [Manage MetaDefender Drives with OPSWAT Management](/docs/mddrive/configuration/managing-drives-with-central-management)
