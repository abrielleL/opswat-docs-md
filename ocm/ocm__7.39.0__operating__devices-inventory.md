<!-- source: https://www.opswat.com/docs/ocm/7.39.0/operating/devices-inventory -->

# Devices Inventory

OPSWAT Central Management offers visibility about endpoint security across the entire organization at **Inventory > Devices**.

The Device management page allows administrators to quickly apply actions to specific devices. Select devices you want to perform a specific action, then click **Action** to select an action.

- **Assign to Groups**: Assign the selected devices to an existing group. Please refer to [Device Groups](/docs/ocm/7.39.0/operating/device-groups) for more detail.

- **Compliance Check** : Choose one or more actions in **Compliance Check** : **Scan Threats** (SOT), **Check OS patch** (SOV), **Check applications security** (SOH). There are 3 types of report corresponding to each action you choose: SOT, SOV and SOH which agent will send to system. You can check it in each **Device Detail** .

- **Scan Threats:** Perform a threat scan on the selected devices.

- **Exempt/Unexempt:** Exempt for a specific amount of time or revoke an existing exemption for a device from the policy of the group they belong to (or the default policy for ungrouped devices). Please refer to [Device Policies](/docs/ocm/7.39.0/operating/device-policies) for more detail.

- **Fetch log:** Remotely fetch the MetaDefender Endpoint's log. A fetch log command will be sent to the client on the selected devices to submit log to OPSWAT Central Management when the devices connect to OPSWAT Central Management. Administrators can download the log on the action's completion.

- **Ignore:** This is applicable for unknown devices which has no MetaDefender Endpoint installed. When an administrator reviews unknown devices, they can ignore an unknown device if needed.

- **Undo Ignore:** Remove the Ignored status for the selected devices if applicable. The affected devices will be converted to Unknown status

- **Re-identify:** Request users on selected devices to re-provide their information. This is applicable if you enable Custom Information feature at **Settings > Global Settings > Advanced > Custom Information**

- **Delete:** Remove devices from OPSWAT Central Management. This action will uninstall MetaDefender Endpoint on the deleted devices when they next connect to OPSWAT Central Management.
