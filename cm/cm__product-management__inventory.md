<!-- source: https://www.opswat.com/docs/cm/product-management/inventory -->

# Inventory

Within **Inventory**, administrators are able to view devices/services enrolled into My OPSWAT Central Management.

You can find devices of the below products inside the **Devices** page

- MetaDefender Endpoint
- MetaDefender Kiosk
- MetaDefender Drive
- MetaDefender Industrial Firewall

You can find instances of the below products inside the **Services** page

- MetaDefender Core
- MetaDefender ICAP Server
- MetaDefender Managed File Transfer (MFT)
- MetaDefender Aether

The All Devices tab gives you an overview of the health status, version, location, group, last seen and last time a device reported data to My OPSWAT Central Management within an account.

Each product tab gives you an overview of the health status, compliance status, version, location, group, last seen and last time a device reported data to My OPSWAT Central Management within an account for a specific product.

### Product Health Status

A product instance periodically reports its health status back to My OPSWAT Central Management. It can have one of the below status

- Unknown: a product instance reported a status as Unknown or a status My OPSWAT Central Management could not recognize.
- Operational
- Minor issues
- Significant issues
- Critical issues
- Blocker issues

### Product Status

My OPSWAT Central Management sets a status for each product instance based on its connection to My OPSWAT Central Management

- Connected
- Disconnected: if an instance has not connected to My OPSWAT Central Management for more than 24 hours

### Endpoint Status

My OPSWAT Central Management informs users of the device's status in relation to My OPSWAT Central Management' policies. Below are the statuses and their definitions:

- **Compliant** - This refers to devices that are in compliance with the My OPSWAT Central Management policy they are assigned to.
- **Non-Compliant** - This refers to devices that are out of compliance with the My OPSWAT Central Management policy they are assigned to.
- **In Grace Period** - This refers to devices that fall under a rule with a device check condition applied (**Policies > Policy Detail > Rules**). The device is flagged as 'in grace' when the Administrator has time to fix it's compliance issues before the device falls into the Non-Compliant status.
- **Exempted** - This refers to devices that are exempted from compliance checks in order to access resources.
- **Unknown** - This refers to discovered devices that do not have the OPSWAT agent or Domain Controller agents reporting a device that does not exist in the database.
- **Ignored** - This refers to discovered devices that have been manually set to 'ignored'. All ignored devices do not have the MetaDefender Endpoint installed and the device does not need a compliance status.
- **Agent Installed** -  This refers to all devices that have an installed agent (no matter the license status).
- **Out of License Usage** - This refers to device that have an installed agent, but the maximum device limit set in the license has been met. To take a device out of this status, the Administrator needs to contact Sales to increase the limit or delete devices to go below the limit.
- **Monitored** - This refers to all devices that have an installed agent and have registered with a successful license.

## Actions

My OPSWAT Central Management provides administrators with actions that can be performed on devices/instances. Below are the actions and their definitions:

- **Assign to Group** - This action allows an administrator to move devices/instances from one group to another.  Note: This affects auto-assignment precedence, we recommend you reviewing our auto-assignment documentation for more information [here](https://www.opswat.com/docs/cm/product-management/auto-assign-endpoints-to-a-group)
- **Delete** - This actions allows an administrator to remove a device from My OPSWAT Central Management.
- **Export** - export devices/instances based on search/filter result.
- **Compliance Check** - This action allows an administrator to request a compliance check for a device or set of devices. Note: My OPSWAT Central Management will run a compliance check once every X minutes.
- **Scan Threats** - This action will allow a device to be scanned for threats ad-hoc on specific paths/categories.
- **Exempt** - This action allows a device to be exempted from My OPSWAT Central Management' compliance check.
- **Unexempt** - This action allows an administrator to reverse exemption on a device for My OPSWAT Central Management' compliance check.
- **Fetch log** - This action allows an administrator to request client logs from a device remotely. To download the log file, go to a device details and click on **Events > Actions**.
- **Ignore** - This action, referring to Device Discovery, allows an administrator to label unknown devices that do not contain the MetaDefender Endpoint as 'ignored' so that their compliance status does not affect the overall account compliance.
- **Undo Ignore** - This action allows an administrator to reverse the 'Ignore' status and the status will return to Unknown.
- **Re-Identify** - This ad-hoc action pushes the device to re-attempt to prompt users for their [custom information](https://docs.opswat.com/macloud-sdp/kb/how-can-i-capture-custom-information-from-end-users-).
- **Submit Ticket** - This action allows an administrator to report a device and any potential issue to the Customer Experience team.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
