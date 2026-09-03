<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/devices -->

# Devices

Within **Inventory**, administrators are able to view endpoints and their data retrieved by MetaDefender IT Access. Administrators can also utilize the actions and search component within the **Devices** page to sort devices and take proactive measures to ensure a device's compliance.

## [Add a device into MetaDefender IT Access](/docs/macloud-sdp/configuration---management/devices#add-a-device-into-metadefender-it-access)

Endpoint devices can be added into MetaDefender IT Access by obtaining an installer for the MetaDefender Endpoint. Administrators can also go a step beyond and have their devices be sorted into groups via auto-assignment. For more information on device groups and auto-assignment, please use the links below:

- [Device Groups](https://docs.opswat.com/macloud-sdp/configuration---management/device-groups)
- [Auto-Assignment](https://docs.opswat.com/macloud-sdp/configuration---management/device-group-auto-assignment)

To add devices into MetaDefender IT Access, administrators need to do the following:

1. Log into MetaDefender IT Access.
2. Select the **+Device** button in the right hand corner.
3. A popup will appear with downloading steps. *Note: if utilizing the auto-assignment via installation package, please refer to the auto-assignment document above.*
4. Select **Download MetaDefender Endpoint for Distribution**, and a new window will appear. Select the desired client version specific to the endpoint's operating system, as well as the type of client the endpoint needs.
5. Once completed, run the installer on the endpoint. When the installation is finished, verify that the device is present under **Inventory > Devices**.

## [Device Status](/docs/macloud-sdp/configuration---management/devices#device-status)

MetaDefender IT Access informs users of the device's status in relation to MetaDefender IT Access' policies. Below are the statuses and their definitions:

- Compliant - This refers to devices that are in compliance with the MetaDefender IT Access policy they are assigned to.
- Non-Compliant - This refers to devices that are out of compliance with the MetaDefender IT Access policy they are assigned to.
- In Grace - This refers to devices that fall under a rule with a device check condition applied (**Policies > Policy Detail > Rules**). The device is flagged as 'in grace' when the Administrator has time to fix it's compliance issues before the device falls into the Non-Compliant status.
- Exempted - This refers to devices that are exempted from compliance checks in order to access resources.
- Unknown - This refers to discovered devices that do not have the OPSWAT agent or Domain Controller agents reporting a device that does not exist in the database.
- Ignored - This refers to discovered devices that have been manually set to 'ignored'. All ignored devices do not have the MetaDefender Endpoint installed and the device does not need a compliance status.
- Agent Installed - This refers to all devices that have an installed agent (no matter the license status).
- Out of License Usage - This refers to device that have an installed agent, but the maximum device limit set in the license has been met. To take a device out of this status, the Administrator needs to contact Sales to increase the limit or delete devices to go below the limit.
- Monitored - This refers to all devices that have an installed agent and have registered with a successful license.

## [Device Actions](/docs/macloud-sdp/configuration---management/devices#device-actions)

MetaDefender IT Access provides administrators with actions that can be performed on a singular device or on a multi-device level. Below are the actions and their definitions:

- Assign to Group - This action allows an administrator to move the device from one group to another. Note: This affects auto-assignment precedence, we recommend you reviewing our auto-assignment documentation for more information [here](https://docs.opswat.com/macloud-sdp/configuration---management/device-group-auto-assignment).
- Compliance Check - This action allows an administrator to request a compliance check for a device or set of devices. Note: MetaDefender IT Access will run a compliance check once every X minutes.
- Scan Threats - This action will allow a device to be scanned for threats ad-hoc on specific paths/categories.
- Exempt - This action allows a device to be exempted from MetaDefender IT Access' compliance check.
- Unexempt - This action allows an administrator to reverse exemption on a device for MetaDefender IT Access' compliance check.
- Fetch log - This action allows an administrator to request client logs from a device remotely. To download the log file, go to a device details and click on **Events > Actions**.
- Ignore - This action, referring to Device Discovery, allows an administrator to label unknown devices that do not contain the MetaDefender Endpoint as 'ignored' so that their compliance status does not affect the overall account compliance.
- Undo Ignore - This action allows an administrator to reverse the 'Ignore' status and the status will return to Unknown.
- Re-Identify - This ad-hoc action pushes the device to re-attempt to prompt users for their [custom information](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-).
- Submit Ticket - This action allows an administrator to report a device and any potential issue to the Customer Experience team.
- Delete - This actions allows an administrator to remove a device from MetaDefender IT Access.

## [Search and filters](/docs/macloud-sdp/configuration---management/devices#search-and-filters)

Administrators can navigate through the **Devices** page and utilize the search and filter components to drill down their device list.

The search component enables administrators to search the inventory by device ID, device name, IP address, and MAC address. Simply type in the search bar the desired value and press enter. From this state, users can further apply filters on their current list, export the current list, or apply actions to the devices currently in that list.

The filter component is split into smaller categories and values that assist the users with narrowing down the device list based on desired fields such as compliance or operating system. Based on the set rules and requirements within a policy, a device will hold specific values to those fields and will be trackable via the filters. From this state, users can further apply filters on their current list, export the current list, or apply actions to the devices currently in that list.
