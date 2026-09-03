<!-- source: https://www.opswat.com/docs/cm/configurations/global-settings -->

# Global Settings

This section guides you through the settings you can customize to tailor your account to your needs.

## Account

The Account section covers relevant information about your account like:

- Account Name
- Account Owner: Name and email
- Registration code: this is used to enroll products.
- PIN requirement setting: if this is enabled, users will be required to enter the user's PIN to make any changes on the account.
- user timeout setting: the idle time for user session to be expired.
- account time zone: Users can set their timezone to local or UTC time for data and time displays in My OPSWAT Central Management.
- Privacy settings

Administrators can **Revoke** a registration code which will generate a new registration code. Any managed devices will not need to be registered again, but this prevents any new devices to be registered with the old code.

A QR code is also available for administrators to copy and send to end users for mobile endpoints registration.

In regards to **Privacy Settings**, under **Account**, users are able to manage what My OPSWAT Central Management tracks:

- User name
- Host name
- Public IP
- MAC Address
- Local IP Address
- Geolocation (Windows Only)
- Applications that are not in categories enabled in a policy
- Serial number

Note: Ensure that [Endpoint Discovery](https://www.opswat.com/docs/cm/configurations/endpoint-discovery) feature is disabled in order to restrict privacy data.

The **Installer Privacy Prompt** is a customizable prompt that administrators can set up for users when they launch the MetaDefender Endpoint installer. In the prompt text, administrators can notify users of any privacy concerns before installing the product.

## Endpoint Clients

The Endpoint Clients section covers settings for MetaDefender Endpoint that will affect all devices. It is important to note that device group settings, in terms of endpoint client, will take precedence over the global endpoint client settings.

- Compliance Report
  - This section covers how often and what triggers (via agent start up vs. user log in) MetaDefender Endpoint will check compliance on devices.
- Client
  - This section covers endpoint settings such as version upgrades, version downloads, user interface visibility, and Secure IT Access settings.
    - **Automatically update to a specific version** - This will force an upgrade on all endpoints that are running older versions (three versions or less).
    - **Automatically update the agent SDK to the specific version** - This will force an upgrade on all endpoints that are running older versions.
    - **Enforce MetaDefender Endpoint version when a user downloads a client from the download page** - This will allow users to download the most recent to the latest version of the MetaDefender Endpoint available.
    - **Require password when a user uninstalls MetaDefender Endpoint on a device** - This will protect the MetaDefender Endpoint from being removed by end users. By requiring a password, only authorized users will be able to remove the software.
    - **Make MetaDefender Endpoint tray icon available to end-users** - This will allow end-users to have access to actions such as 'Export logs'.
    - **Make MetaDefender Endpoint user interface available to end-users** - For the persistent client only, users will be able to view the MetaDefender Endpoint's interface and have access to all the sections available for that account.
    - **Enable Secure IT Access for all endpoints** - This will install Secure IT Access on all endpoints within the Inventory.
    - Enable MetaDefender Managed File Transfer Integrationinfo
    - Enable Peripheral Inventory
    - **Use in-app browser to prompt for Secure IT Access credentials** - For SSO Secure IT Access users only, users will be able to log into Secure IT Access through the MetaDefender Endpoint without being re-directed to an authentication page.
    - **Require the MetaDefender Endpoint to register upon install**- This will prompt end users for valid organization credentials upon installation to authorize the device's registration. Note: This is only available if End User Authentication (SSO) is enabled.
    - Automatically migrate devices not belonging to DCs below to unknown device status upon registration
- Notification to Users
  - This sections covers when MetaDefender Endpoint notifies users on activities such as new applications installed, out-of-date agents, and reminding users how much time remains on application access.

## Endpoint Data

The Device Data section covers the settings for how long data is stored on My OPSWAT Central Management' backend.

- Data Retention
  - How long the system will auto-delete data such as event logs, reports. It is set to 30 days by default. If you wish to have longer data retention, you will have to reach out to OPSWAT sales for an account upgrade.
  - The retention behavior is how My OPSWAT Central Management will act upon a device being removed. If set to Archive, it will keep the data of the deleted device for 30 days. If set to Purge, it will remove all logs and events relevant to the deleted device.
- Retain the last group a device was manually assigned to when the device is deleted: this allows the device enrolled to the last group it was manually moved to.
- Unresponsive Device
  - This section determines how My OPSWAT Central Management treats unseen devices. Administrators are able to set how long the system should remove unseen devices from the account.
  - This section also includes the ability to remove non-compliant devices from My OPSWAT Central Management if they have reported non-compliant for X days consecutively.
- Non-compliant Device: configure how the system should apply to non-compliant devices such as moving them to a specific group or deleting them.

## MetaDefender Integration

The MetaDefender Integration section is relevant to any accounts utilizing MetaDefender to scan files on endpoints. Here you can add MetaDefender servers for your monitored devices to scan files for threats and exposures.

- Click Add Server
- Fill in required information
  - Name: for your memo
  - API Key that can scan files on MetaDefender Core
  - Server address

To find out more about MetaDefender, contact OPSWAT Sales for more information.

## Notifications

For more information in regards to notifications, please review this [guideline](https://www.opswat.com/docs/cm/reports-and-notification/email-notifications)

## Advanced

This setting allows administrators to capture custom information from end-users through the client. When the MetaDefender Endpoint is launched on the devices, the users will be prompted with a message that requests the user to enter a requesting information. Administrators can then use the custom information to track devices or individuals.
