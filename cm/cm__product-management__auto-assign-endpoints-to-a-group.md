<!-- source: https://www.opswat.com/docs/cm/product-management/auto-assign-endpoints-to-a-group -->

# Auto-Assign Endpoints to a Group

This document covers the options that My OPSWAT Central Management provides for auto-assignment for endpoints as they are added into your account. These settings can be added or removed at any time by navigating to **Inventory > Groups >** and selecting the device group you would like to update.

## Auto-Assignment via installation package

This setting allows devices to be assigned to the group automatically via the installation package. When creating an installation package, a pop up window in My OPSWAT Central Management will prompt an administrator to select **Devices will be automatically assigned to this group:**. By turning on the option to **auto-assign via installation package**, administrators will be able to select their device group in the pop up window before downloading a new installation package.

## Auto-Assignment via the domain

This setting allows devices to be assigned to the group automatically via the domain the device is joined to (as detected by the MetaDefender Endpoint). By turning on this option, administrators can enter the designated domain. This method will take precedence over the **auto-assignment via installation package**, meaning My OPSWAT Central Management will always sort it based on the domain value first, and the installation package after if the domain option is enabled for any group.

## Manual Assignment via Administrator

This is an action that is performed by an administrator when selecting the action **"Assign to Group"** in My OPSWAT Central Management. To move a device manually, an administrator will navigate to **Inventory > Devices** and select [Inventory](https://www.opswat.com/docs/cm/product-management/inventory). The system will not move a device to another group with auto-assignment options enabled if it has been assigned to another group by an administrator at any time. This action is of higher precedence than **auto-assignment via the domain**.

## Override Device Group Assignment via Playbooks

This is an override setting found under the Move Device action in Playbooks. This is the highest override, and will override all auto or manual assignments. To learn more about playbooks [here](https://www.opswat.com/docs/cm/product-management/playbooks).

## Additional Notes

- Under **Settings > Global > Endpoint Data > Data Retention** , the setting **Retain the last group a device was manually assigned to when the device is deleted** will take precedence over the auto-assignment settings under the device group as it qualifies as an administrator requested assignment. In the case that the MetaDefender Endpoint is uninstalled and then reinstalled, the device will be placed back into the last group it was in. If this is not desired, please uncheck this option.
- The My OPSWAT Central Management system will organize assignment precedence by the following order from **highest** to **lowest**:
  - Override Device Group Assignment via Playbooks.
  - Manual Assignment via Administrator
  - Auto-assignment via the domain
  - Auto-assignment via installation package
- To review device movement between groups, Administrators can use **Device Events** found under **Logs > Device Events**. Administrators are also able to export this information within **Device Events**.
