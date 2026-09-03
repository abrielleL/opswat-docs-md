<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/global-settings -->

# Global Settings

Within the **Settings** component of MetaDefender IT Access, Administrators can set and adapt configurations for their entire account and their devices.

## [Account](/docs/macloud-sdp/configuration---management/global-settings#account)

The Account section covers relevant information about the MetaDefender IT Access account like:

- Devices Monitored
- Devices Limit
- License Key
- Account Name
- Account Owner
- Email

This section also includes the account's registration code. This can be entered manually into the free client on a desktop or mobile device.

Administrators can **Revoke Code** which will generate a new registration code. Any already registered devices will not need to be registered with this code, but this prevents any new devices to be registered with the old code.

A QR code is also available for administrators to copy and send to end users for mobile registration.

The Account section also covers:

- PIN Security Prompt - Users are given the option to enable or disable their PIN on their account. If a user also has managed access to another MetaDefender IT Access account, they will be required to follow the configurations of that account, and MetaDefender IT Access will ignore their customized settings.
- Account Session Timeout- Users can change the idle time for their session to expire.
- Account Timezone- Users can set their timezone to local or UTC time for data and time displays in MetaDefender IT Access.
- Privacy Settings

In regards to **Privacy Settings**, under **Account**, users are able to manage what MetaDefender IT Access tracks:

- User name
- Host name
- Public IP
- MAC Address
- Local IP Address
- Geolocation (Windows Only)
- Applications that are not in categories enabled in a policy
- Serial number

Note: Ensure that **Unknown Device Discovery** feature is disabled in order to restrict privacy data. For more information, review the Advanced section.

The **Installer Privacy Prompt** is a customizable prompt that administrators can set up for users when they launch the MetaDefender Endpoint installer. In the prompt text, administrators can notify users of any privacy concerns before installing the product.

## [Device Agents](/docs/macloud-sdp/configuration---management/global-settings#device-agents)

- Compliance Report

  - This section covers the globally set time that compliance reporting will run, and what will trigger the reporting to run (via agent start up vs. user log in).
- Agent

  - This section cover the globally set agent configurations such as version upgrades, version downloads, user interface visibility, and Secure IT Access settings.

    - **Automatically update to a specific version** - This will force an upgrade on all devices within the Inventory that are running older versions (three versions or less).
    - **Automatically update the agent SDK to the specific version** - This will force an upgrade on all devices within the Inventory that are running older versions.
    - **Enforce agent version when a user downloads an agent from the download page** - This will allow users to download the most recent to the eldest version of the MetaDefender Endpoint available.
    - **Require PIN when a user uninstalls agents on a device** - This will protect the MetaDefender Endpoint from being removed by end users. By requiring a PIN, only authorized users will be able to remove the software.
    - **Make MetaDefender Endpoint tray icon available to end-users** - This will allow end-users to have access to actions such as 'Export logs'.
    - **Make MetaDefender Endpoint user interface available to end-users** - For the persistent client only, users will be able to view the MetaDefender Endpoint's interface and have access to all the sections available for that account.
    - **Enable Secure IT Access for all devices** - This will install Secure IT Access on all clients within the Inventory.
    - **Use in-app browser to prompt for Secure IT Access credentials** - For SSO Secure IT Access users only, users will be able to log into Secure IT Access through the MetaDefender Endpoint without being re-directed to an authentication page.
    - **Require the MetaDefender Endpoint to register upon install**- This will prompt end users for valid organization credentials upon installation to authorize the device's registration. Note: This is only available if End User Authentication (SSO) is enabled.
- Notification to Users

  - This sections covers when to notify users on activity involving the MetaDefender Endpoint such as new applications installed, out-of-date agents, and reminding users how much time remains on application access.

## [Device Data](/docs/macloud-sdp/configuration---management/global-settings#device-data)

The Device Data section covers the settings for how long data is stored on MetaDefender IT Access' backend.

- Data Retention

  - The length of time is set at a default of 365 days for all accounts. For a longer length of time, users will have to reach out to OPSWAT sales for an account upgrade.
  - The retention behavior is how MetaDefender IT Access will act upon a device being removed. If set to Archive, it will keep the data of the deleted device for 365 days. If set to Purge, it will remove all logs and events relevant to the deleted device.
- Lost Device

  - This section determines MetaDefender IT Access' approach to unseen devices. Administrators are able to set timers on when to remove unseen devices from the account.
  - This section also includes the ability to remove non-compliant devices from MetaDefender IT Access if they have reported non-compliant for X days consecutively.

## [MetaDefender Servers](/docs/macloud-sdp/configuration---management/global-settings#metadefender-servers)

The MetaDefender Servers section is relevant to any account utilizing MetaDefender Cloud. Here you can add your MetaDefender servers for your monitored devices to scan files for threats and exposures.

To find out more about MetaDefender, contact OPSWAT Sales for more information.

## [Notifications](/docs/macloud-sdp/configuration---management/global-settings#notifications)

For more information in regards to notifications, please review this [document](https://docs.opswat.com/macloud-sdp/configuration---management/email-notifications).

## [Advanced](/docs/macloud-sdp/configuration---management/global-settings#advanced)

The Advanced section covers custom information. This setting allows administrators to capture custom information from end-users through the client. When the MetaDefender Endpoint is launched on the devices, the users will be prompted with a message requesting the custom set information. Administrators can then use the custom information to track devices or individuals.
