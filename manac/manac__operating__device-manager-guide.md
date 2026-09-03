<!-- source: https://www.opswat.com/docs/manac/operating/device-manager-guide -->

# Device Manager Guide

The NAC solution provides real time Policy Status Data for managed devices via a Web-based portal, allowing Administrators and Help Desk personnel to view the real-time policy status of every active device connected to the enterprise network.

## [Overview](/docs/manac/operating/device-manager-guide#overview)

The purpose of this document is to provide the end user with an overview and basic familiarity with the NAC Device Manager. The NAC Device Manager is a central web based reporting tool that makes available information on the current environment and its devices and policy compliance. In addition to real time reporting, the NAC Device Manager offers several other important administrative features and functionalities which will be expanded upon further. This document will be broken down based on the sections summarized below.

Access to the features of the NAC Device Manager will vary depending on the read or write permissions granted to the end user from the User Management section of the NAC Configuration Manager.

## [Introduction](/docs/manac/operating/device-manager-guide#introduction)

To access the Device Manager, navigate to [https://portal.myweblogon.com:8443/manage/#/devices/core/1](https://auth.impulse.com:8443/manage/#/devices/core/1). “[portal.myweblogon.com](http://auth.impulse.com)” can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.

Users with “read” access to the Device Manager will be able to view everything in the Device Manager. The list of devices can be sorted by clicking on the column titles.

The main window shows all active devices on the network. The left column contains quick links to show devices that match the item listed. For example, a system that is out-of-compliance for antivirus not installed, can be found in the devices listed under the antivirus installed section which is listed in the Policy Compliance tab.

| Statistic | Description |
| --- | --- |
| Standard Views | Shows basic device statistics |
| Policy Groups | Shows the number of devices currently active on the network for each Policy Group |
| Device Types | Shows the number of a specific type of device currently going through NAC |
| Policy Compliance | Shows the number of devices out of compliance for each individual policy |
| Enforcement Devices | Shows the number of devices that are being enforced by a specific enforcement device |

## [Devices Tab](/docs/manac/operating/device-manager-guide#devices-tab)

The main section of the page displays devices enforced by NAC based on which filter has been chosen in the left column.

## [Details Page](/docs/manac/operating/device-manager-guide#details-page)

Clicking on an IP or MAC address will open the details page for the chosen client.

In the top right corner of the page are the options for client operations. This section should only be used when troubleshooting is necessary.

| Operation | Description |
| --- | --- |
| Open Access | Exempt the device from policy by putting it in the Open Access group |
| Block Access | Block the device's network access by putting it in the Block Access group |
| Force Login | Require a user to re-authenticate. You can choose to either clear credentials from history or reserve them for tracking. |
| Enroll Device | Used to grant access to devices that do not have a web browser and therefore cannot authenticate. |
| Expire Device | Treats the device as if it were new |
| Purge Device | Clears the device record |

- The **Device Details** section displays more information about the device. If multiple interfaces are present on a machine, the IP and MAC address information will reflect the interface that is used for policy group assignment.

| Detail | Description |
| --- | --- |
| MAC Address | MAC of current active NIC |
| IP Address | IP address reported by DHCP, RADIUS or the Policy Key |
| Device Profile | Displays the operating system of a computer, or the device type for other network connected devices |
| Username | Username for the endpoint machine, not always the username used to login to NAC |
| Primary Role | The LDAP group membership or the NAC user |
| Policy Group | What policy group the device is currently assigned to |
| Last Communication | Most recent DHCP update or Policy Key callback |
| Expires | Time the device's session will be reassessed as a new session if the Policy Key does not call back |
| Machine Name | Name reported by DHCP, netflow or the Policy Key |
| Machine Login | Username for the endpoint machine, not always the username used to login to NAC |

- The **Policy Compliance** tab shows more information about which policies are being applied to the device and whether it is compliant for them.

- The **Policy Group Details** tab shows the qualifiers that were used to determine why the device was placed in the current policy group.

- The **Device History** tab shows all basic information gathered from this device in the last 30 days.

| Transaction | Description |
| --- | --- |
| AddInterface | A different NIC has become active on the endpoint. Only appears for Policy Key devices. The Policy Key is available with a Device Security, Standard or Enterprise license. |
| Auth Failure | Unsuccessful captive portal authentication attempt. Rarely, can indicate the user's authentication status was revoked via the Device Manager's details page. |
| Authentication | The end user has successfully submitted authentication credentials at the captive portal page. This transaction will **not** appear for devices that authenticate via Single Sign-on. These can include cases where a Policy Key machine logs on to an AD domain, or where NAC receives Radius Accounting from WPA2 Enterprise or Aruba wireless controllers. Also will not appear for users whose credentials are validated via an IdP, as in SAML or Shibboleth. Also see “ST SSO - Pass” below for more details. |
| Expire Dash | Device session manually expired from the Device Details page. See "Expire Timeout" for details. |
| Expire Timeout | NAC is no longer aware the device is active. **The device has not been blocked**. It is simply no longer visible in the Active Devices view in the Device Manager. By default, this will occur at most 30 minutes after the last sign of network traffic from the endpoint. Relevant traffic could include Netflow or Sflow, RADIUS accounting, or DHCP lease grants or renewals. If the Policy Key is installed, PK traffic will also keep a record alive. If more network traffic is noted, the record will become active again. |
| Expired | NAC deactivated a record with partial information, preparing to reactivate an older, more complete record. This can happen if NAC only sees an endpoint's IP address initially, but later receives a MAC address as well. If the MAC address has a pre-existing record, NAC will deactivate the IP-only record, and link back the record by MAC address. |
| ExpireInterface | For customers with a Device Security license. This means the Policy Key indicated this NIC is no longer active on the endpoint. |
| Group Change | Device was placed into a different NAC policy group. |
| RemoveInterface | For customers with a Device Security license. This means the Policy Key indicated this NIC is no longer active on the endpoint. |
| Rotate IP | Device received a new IP. |
| RouterRedirect | Device was redirected by enforcement device. Multiple repeated instances of this can mean NAC is unable to remove a quarantine, even though the device is compliant. If you see this, please open a [support case](http://support.impulse.com) for help. |
| Scan PK | For customers with a Device Security license. This means the Policy Key reported a change of state for the endpoint in question. Covers a wide variety of circumstances, but notably: IP change, switching between wired and wireless networks, policy compliance change, asking the NAC enforcer for an updated set of policies. |
| SES Start Auth | Session started based off an authentication attempt. This should be a rare edge case. Indicates that NAC saw the attempted authentication event before receiving any other network indicators for the endpoint (e.g. DHCP syslog, RADIUS accounting, etc.). |
| SES Start Web | Session started by a device navigating directly to the SC appliance. Should be a rare edge case. See "SES Start Auth" for details. |
| Show Page | NAC displayed a policy compliance web message to the endpoint. The page can be either a Warning (non-blocking) or Quarantine (blocking) page. |
| ST SSO - Fail | Radius Accounting has supplied NAC with the end user’s network login credentials. However, NAC was unable to verify the credentials against the institution’s directory server(s). |
| ST SSO - Pass | Radius Accounting has supplied NAC with the end user’s network login credentials, which were then successfully validated against the institution’s directory server(s). |
| ST SSO - Rec | Radius Accounting has supplied NAC with the end user’s network login credentials, which were then recorded in the database without validation against the institution’s directory server(s). |
| Start SES | Session Tracker detected a new device session. Session Tracker is the broker service in NAC that correlates all the incoming network feeds, from DHCP requests and DHCP syslog, to RADIUS accounting and Netflow. |
| StartInterface | A new NIC has been detected, either via Session Tracker input (see above). With a a Device Security license, the Policy Key will also report a newly active NIC. |
| Startup PK | For customers with a Device Security license. This means the Policy Key client has requested new policies from NAC. This typically happens when |
| Stop SES | Session Tracker notified NAC that the endpoint's session has ended. This does **NOT** mean that NAC has blocked the device. The device will simply no longer appear under "Active Devices" in the Device Manager. This typically happens at most 30 minutes after the most recent evidence of network traffic. See "Start SES" above for details about what Session Tracker processes. This does **NOT** mean the device is no longer connected to the network. It might still be connected, but not pushing much traffic. |

- The **Advanced** tab shows more detailed device information such as its interfaces, user roles and attributes.

| Diagnostic Name | Description |
| --- | --- |
| Local IP |  |
| Previous IP | Most recent former IP assigned to the device |
| Enforcer IP Address | IP address of the enforcement device |
| Enforcer Label | Label of the enforcement device |
| Enforcer Type | Type of the enforcement device |
| Policy Key Build | Version of the Policy Key installed |
| Next Policy Key Contact | When the Policy Key should call back if policy compliance does not change |
| RBE Quarantine Role | Role the device should have on the controller if it is quarantined |
| RBE Compliant Role | Role the device should have on the controller if it is compliant |

## [Enrollment Tab](/docs/manac/operating/device-manager-guide#enrollment-tab)

The Enrollment page provides a way to enroll devices. Typical use cases for this include any device that cannot authenticate via a web browser, or any device that is not able to pass detection. For example, a network printer is a prime candidate for this feature.

The Device Enrollment window will display basic information about each current enrolled device. If a record has expired, the status value will display "Inactive".

Clicking on "Add" in the top right corner of the page will open a form to create a device enrollment.

The Role field is only required if the Policy Group for enrolled devices will use the role as a qualifier.

Once a device is enrolled, it will appear in the list of devices on the Enrollment page. Clicking the X button under the Modify column will delete the enrollment. Clicking the pencil button will allow the user to edit the enrollment.

Clicking on "Bulk Upload" in the top right corner of the page will open a pop up from which a worksheet template can be downloaded, filled with the required information for every new entry, and then uploaded. This is used to upload a large amount of enrollment entries which would be inconvenient to input one at a time.

Note that device roles must be entered in the Configuration Manager prior to enrolling devices and specifying a role.

## [Sessions Tab](/docs/manac/operating/device-manager-guide#sessions-tab)

The Sessions page can be used for viewing device session information. It stores 500,000 entries or one year's worth of data, whichever is smaller.

Any column can be used to search. The list of sessions can be sorted by clicking on the column titles.

This page does not show as much information as Device History, but it goes back much further in time, making it useful for looking up historical data.

## [Access Tab](/docs/manac/operating/device-manager-guide#access-tab)

The Access page allows a device to override a policy by either exempting a device from policy or blocking a device that is otherwise compliant. This function is useful in situations where an endpoint is having difficulty updating antivirus definitions and needs temporary access, or when an endpoint is compliant with policy, but is suspected of unusual network activity, such as spamming or a DMCA violation, and needs to be blocked from the network until it can be investigated further.

An endpoint's enrollment details can be edited by clicking the pencil button under the Modify column.

### [Open Access Tab](/docs/manac/operating/device-manager-guide#open-access-tab)

An endpoint can be exempted from policy by clicking the "Add" button in the top right while in this tab.

| Field | Description |
| --- | --- |
| Type | Option to enforce by IP address, MAC address (preferred) or username. |
| State | State of the enrollment. Can be Active, Inactive or Pending Approval. |
| Value | Value of the qualifier type. This is where the IP address, MAC address or username would go. |
| Expiration | When this enrollment will expire. Can be set to minutes, hours, days, years or never. This gives the endpoint a window of time to remediate their reason for being quarantined. |
| Note | Space for a brief explanation. |

Clicking "Save" will place the device in the Open Access group for the amount of time listed in the Expiration field. While in this group, the device will be able to freely use the network. A user can be removed from Open Access from this page by clicking the X button under the Modify column or by clicking "Remove Open Access" in its Device Details page.

### [Block Access Tab](/docs/manac/operating/device-manager-guide#block-access-tab)

An endpoint can be blocked from network access by clicking the "Add" button in the top right while in this tab.

| Field | Description |
| --- | --- |
| Type | Option to enforce by IP address, MAC address (preferred), or username. |
| State | State of the enrollment. Can be Active, Inactive or Pending Approval. |
| Value | Value of the qualifier type. This is where the IP address, MAC address or username would go. |
| Expiration | When this enrollment will expire. Can be set to minutes, hours, days, years or never. This gives the endpoint a window of time during which they will not have access. |
| Note | Space for a brief explanation. |
| Display note to end user while blocked | When checked, the text in the Note field will be displayed on a block page. The user will see the block message either the next time they generate web traffic, or after the next Policy Key callback. |

Clicking "Save" will place the device in the Block Access group for the amount of time listed in the Expiration field. While in this group, the device will be blocked from the network. A user can be removed from Block Access from this page by clicking the X button under the Modify column or by clicking "Remove Block Access" in its Device Details page.
