<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration -->

# Device Self-Enrollment Configuration

## [Overview](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#overview)

NAC provides the ability for users to enroll their gaming consoles, media players, smart TVs, web-enabled blu-ray players, network printers and other browser-less devices. These are devices that are not able to use WPA2 Enterprise wireless to authenticate. Device enrollment allows you to associate identity to devices on your network that would not otherwise be able to provide identity due to lack of a functional web browser. This document will guide you through setting up device enrollment for your network.

The purpose of this document is to introduce you to the configuration and operation of the Device Self-Enrollment module of NAC. This document provides all the information needed to fully configure the Device Enrollment module. This document will also step you through how a user will enroll their device and receive subsequent notification when their device is ready for use on the network. This document assumes that standard URLs will be used. If a branded deployment is in use, please refer to the appendix for information on branded URLs.

NAC device self-enrollment provides a portal style system to allow end users to enroll their own devices so they can access the network. The default notification requirements and device “Time to Live” durations are completely configurable. All device information is viewable and editable by an administrator through the Enrollment tab on the NAC Device Manager. Administrators have the ability to choose from one of two approval methods, depending on the level of control required:

- Automatic Approval with a notification sent to administrators
- Notification sent to administrators with administrative approval required

## [End User Experience](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#end-user-experience)

## [Device Enrollment Overview](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#device-enrollment-overview)

The end user navigates to <https://portal.myweblogon.com:9443/enroll> (In a branded deployment, replace this standard URL with your branded URL) and fills out their network user name and password.

- A link to the enrollment page should be placed on the organizations helpdesk webpage.

The end user fills out the enrollment form, providing a valid mac address and device type. If users wish to be notified upon successful approval, their email address, cell phone number and cell phone carrier should be provided. After all information is correct, the user can click on ‘Add this Entry’.

*A MAC address is required for device enrollment. Instructions for finding the MAC address should be placed on the organizations helpdesk webpage. Instructions for find the MAC address are beyond the scope of this document.

After the device is enrolled, the device status will appear in the bottom section of the page. If they chose to be notified, they will receive a text message and/or email informing them that their device is now active on the network. Active devices will show an Account State of ‘Active’, and devices pending approval will show an Account State of ‘Pending’. If the user needs to remove a device enrollment, they can click on the ‘delete’ icon.

## [Administrator Device Enrollment Approval Overview](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#administrator-device-enrollment-approval-overview)

The Device Enrollment approval process will vary depending on the approval option that is in use by NAC

- **Automatic with Notification:** The Device Enrollment is automatically approved. An email is sent to administrators alerting them of the granted notification request. If necessary, an administrator can revoke enrollment via the administrative ‘Device Enrollment’ tab of the Device Manager.
- **Approval Required for Notification:** If approval is required for device enrollment, an email is sent to administrators alerting them of the pending request. Administrators can click on the link in the email to approve the request.

***Note:** If NAC detects that the user is attempting to enroll a device that has previously been detected as a different device type, this email will be sent with high importance and include the following information:

1. The vendor of the devices MAC address
2. The previously detected Device Type
3. The previous Policy Group of the MAC address

The ‘Enrollment’ tab of the Device Manager shows all active enrollments and pending requests. Pending requests can be edited by clicking on the edit icon.

To allow the device access and send the user a notification:

1. Change the State to ‘Active’
2. Click on ‘Add/Update This Entry’

If messaging is enabled, and contact information is present, the end-user will receive a notification via SMS or email. If the user does not receive the notification, they can call the helpdesk or navigate back to <https://portal.myweblogon.com:8443/enroll> to check on the status of their enrollment request.

## [Configuration](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#configuration)

## [Email Configuration](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#email-configuration)

Device Self-Enrollment requires email for sending notifications. Steps to configure email can be found [here](/docs/manac/nac-v8.1.1/operating/email-setup).

## [Helpdesk Webpage Modifications](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#helpdesk-webpage-modifications)

For users to use Device Self-Enrollment, the organizations helpdesk webpage should include both a link to the Device Self-Enrollment page and instructions on how to locate the MAC address on their device.

The default URL for the Device Self-Enrollment page is: <https://portal.myweblogon.com:8443/enroll> (In a branded deployment, replace this standard URL with your branded URL). How you will link to the page is completely up to you.

Instructions for how to find the MAC address of devices should also accessible from the organizations helpdesk webpage. Specific instructions are beyond the scope of this article.

## [Device Self-Enrollment Configuration](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#device-self-enrollment-configuration)

The configuration for Device Enrollment can by navigating to "Configuration Manager > Self-Enrollment Portals > Device Enrollment'.

To continue, click on the 'Enable Configuration Mode…' button in the upper left to activate any of the “Edit” buttons on this screen and then click the 'edit' icon next to 'Device Enrollment'.

### [Default Device Enrollment Configuration](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#default-device-enrollment-configuration)

For “Device Enrollment” options, clicking on the edit button will open the base configuration form. The “Account State” option is the on/off switch for Device Enrollment. The default setting for this is “Active”; the “Disabled” option turns it off.

### [General Options](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#general-options)

Clicking on the “General Options…” button will expand the dialogue box to include options for defining the maximum number of devices a user can enroll and a default expiration time for new devices.

A maximum number of devices a user can enroll can be changed by editing the value for ‘Maximum Number of Enrollments per user’. Using the ‘Enrollment Expiration’ drop down menu, the administrator can define how long a device can be active. Whatever is set here will be the default for all new device enrollments. Enrollment expiration can be defined to be active for a given number of minutes, hours or days. There is also an option to set enrollments to 'Never Expire'. Devices can be inactivated on a per device basis using the ‘Enrollment’ tab of the Device Manager.

### [Notification/Validation Options](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#notificationvalidation-options)

The Device Enrollment module comes with expiration and notification/validation settings. The notification options have two validation levels and can be seen in the illustration below:

- **Active Immediately – Notification Sent** – Once the device is enrolled it is immediately active. A notification email is sent to the configured administrative notification email address. The enrolled device will show up in the Device Enrollment management page and can be modified or deleted by an administrator.
- **Verification by Admin needed before Active** – Once the device is enrolled, it is inactive. A notification email is sent to the configured administrative notification email address with the option to accept or decline the enrolled device. The enrolled device will show up in the Device Enrollment management page and can be modified or deleted by an administrator. The administrator also has the option to activate the enrolled device from the Device Enrollment Page.

Both a Notification and a Sender email address is required for email notifications to work properly. These addresses must be different.

**NOTE:***If required, please ensure that the sender address is valid in your directory structure.*

### [Authentication Options](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#authentication-options)

Clicking on the “Advanced Options…” button will expand the dialogue box to include options for setting roles and defining an authentication server.

The role for new device enrollments can be set from this page using the drop down menu. Device Self-Enrollment roles are NAC specific. If there are no roles available, new roles can be added by following the [steps outlined here](/docs/manac/nac-v8.1.1/configuration/role-setup-for-guest-and-device-enrollment). The authentication server for device enrollment can also be specified from this page.

## [Policy Manager Configuration](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#policy-manager-configuration)

### [Enrolled Devices Policy Groups](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#enrolled-devices-policy-groups)

Two policy groups must be created to handle enrolling devices. Please refer to NAC Policy Manager documentation for the creation of the policy group. The policy groups should be configured as follows:

Gaming & Media - Registered Policy Group:

1. Network Qualifier set to IP address Range or Subnet
2. Device Qualifier set to Gaming and Media Devices
3. Identity Qualifier set to role used for Device Enrollment
4. No policies!

Gaming & Media - Not Registered Policy Group:

1. Network Qualifier set to IP address Range or Subnet
2. Device Qualifier set to Gaming and Media Devices
3. Always Block Policy

After both policy groups are created, it is important to ensure that the 'Registered' policy group has a higher group priority than the 'Not Registered' policy group:

With this setup, devices will fall in the 'Not Registered' group by default and be quarantined. Devices that have been enrolled will automatically have a role applied that will move then to the 'Registered' policy group after the device is enrolled.

Once the policy groups are created, click 'Apply and Use' in the policy manager to publish the changes.

## [Device Enrollment Links](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#device-enrollment-links)

- Device Enrollment Portal:

  - Standard: <https://portal.myweblogon.com:8443/enroll>
  - Branded example: [https://nac.customer.edu:9443/enroll](https://metaaccessnac.customer.edu:9443/enroll)
- Administrative Links:

  - Standard: [https://portal.myweblogon.com:8443/](https://auth.impulse.com:8443/config.s)[manage](https://portal.myweblogon.com:8443/manage)
  - Branded example: [https://nac.customer.edu:9443/](https://metaaccessnac.customer.edu:9443/config.s)[manage](https://safeconnect.customer.edu:9443/manage)

    - User Options >> Device Enrollment
    - SMS Carriers
- Notes

  - In a clustered deployment, please reference the manager IP.
  - The standard default port is 8443, however in a branded deployment it will default to 9443.

## [Manually Enroll Devices through the Device Manager](/docs/manac/nac-v8.1.1/configuration/device-self-enrollment-configuration#manually-enroll-devices-through-the-device-manager)

In some cases, it may be desirable to manually enroll devices through the Device Manager. To reach the device enrollment tab of the Device Manager page, navigate to 'Device Manager > Enrollment'. Click the 'Add' button to create a new enrollment record.

If you wish for the device to be automatically placed in a policy group, the device type and role must match an existing policy group and a username must be specified.
