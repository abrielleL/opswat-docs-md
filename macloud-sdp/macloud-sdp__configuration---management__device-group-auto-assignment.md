<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/device-group-auto-assignment -->

# Device Group Auto-Assignment

This document covers the options that MetaDefender IT Access provides for auto-assignment for endpoints as they are added into your account. These settings can be added or removed at any time by navigating to **Inventory > Device Groups >** and selecting the device group you would like to update.

## [Auto-Assignment via installation package](/docs/macloud-sdp/configuration---management/device-group-auto-assignment#auto-assignment-via-installation-package)

This setting allows devices to be assigned to the group automatically via the installation package. When creating an installation package, a pop up window in MetaDefender IT Access will prompt an administrator to select **Devices will be automatically assigned to this group:**. By turning on the option to **auto-assign via installation package**, administrators will be able to select their device group in the pop up window before downloading a new installation package.

## [Auto-Assignment via the domain](/docs/macloud-sdp/configuration---management/device-group-auto-assignment#auto-assignment-via-the-domain)

This setting allows devices to be assigned to the group automatically via the domain the device is joined to (as detected by the MetaDefender Endpoint). By turning on this option, administrators can enter the designated domain. This method will take precedence over the **auto-assignment via installation package**, meaning MetaDefender IT Access will always sort it based on the domain value first, and the installation package after if the domain option is enabled for any group.

## [Manual Assignment via Administrator](/docs/macloud-sdp/configuration---management/device-group-auto-assignment#manual-assignment-via-administrator)

This is an action that is performed by an administrator when selecting the action **"Assign to Group"** in MetaDefender IT Access. To move a device manually, an administrator will navigate to **Inventory > Devices** and select a device (more information [here](https://docs.opswat.com/macloud-sdp/kb/how-can-i-manage-devices-by-groups-)). The system will not move a device to another group with auto-assignment options enabled if it has been assigned to another group by an administrator at any time. This action is of higher precedence than **auto-assignment via the domain**.

## [Override Device Group Assignment via Playbooks](/docs/macloud-sdp/configuration---management/device-group-auto-assignment#override-device-group-assignment-via-playbooks)

This is an override setting found under the Move Device action in Playbooks. This is the highest override, and will override all auto or manual assignments. To learn more about playbooks, click [here](https://docs.opswat.com/macloud-sdp/configuration---management/playbooks).

## [Additional Notes](/docs/macloud-sdp/configuration---management/device-group-auto-assignment#additional-notes)

- Under **Settings > Global > Device Data > Data Retention** , the setting **Retain the last group a device was manually assigned to when the device is deleted** will take precedence over the auto-assignment settings under the device group as it qualifies as an administrator requested assignment. In the case that the MetaDefender Endpoint is uninstalled and then reinstalled, the device will be placed back into the last group it was in. If this is not desired, please uncheck this option.
- The MetaDefender IT Access system will organize assignment precedence by the following order from **highest** to **lowest**:

  - Override Device Group Assignment via Playbooks.
  - Manual Assignment via Administrator
  - Auto-assignment via the domain
  - Auto-assignment via installation package
- To review device movement between groups, Administrators can use **Device Events** found under **Logs > Device Events**. Administrators are also able to export this information within **Device Events**.
