<!-- source: https://www.opswat.com/docs/macloud-sdp/release-notes/cloud-console -->

# Cloud console

## Release Date: March 26, 2025

Console Version: 3.53.0

**Additions in this release**

1. Added support log for IdP MFA
2. Added new OAuth Device Detail API to retrieve Public IP
3. Enhancement & bug fixes.

More details:

**Added support log for IdP MFA**

In this feature update, during the authentication process, once users successfully complete the authentication step, a device posture check is performed using OPSWAT IdP MFA. This ensures that the device meets security compliance requirements before access is granted. The entire activity is logged, allowing administrators to track who is using the service and monitor device compliance. This enhances security visibility and prevents unauthorized or non-compliant device access.

**Public IP added to get Device detail APIs**

The "Get Device" Detail APIs (Application Programming Interfaces) now include Public IP (Internet Protocol Address) information, improving network visibility and security monitoring. This update helps administrators track devices, detect unusual access patterns, and integrate data with security tools like Splunk. It also supports compliance auditing by providing better oversight of device activity. With this enhancement, IT teams can strengthen security, improve threat detection, and optimize network management.

## Release Date: February 19, 2025

Console Version: 3.52.0

**Additions in this release**

1. Few user Interface features renamed on IT Access console.
2. Support for Ping Federate integration with OPSWAT Identity Provider Multi-factor authentication
3. Enhancement and bug fixes.

## **More details:**

**Few user Interface renamed on IT Access console**

In this release, some features are renamed to make the interface more intuitive and user-friendly by using terminology that better reflects each feature's function. By aligning feature names with common user expectations and industry standards, we hope to reduce confusion and streamline navigation within the application. The changes are as follows:

Compliance → Deep Compliance

Patch Management → Application Patches

OS Updates → Windows / macOS Update

Vulnerable Application → Vulnerabilities

AppRemover → Application Remover

In this release, we have also updated the terminology in the IT Access Console, changing the text from "Local Engines" to "Embedded Engines". This renaming aims to provide greater clarity and accuracy in describing the functionality within the system.

The term "Embedded Engines" more precisely reflects their role, indicating that these engines are integrated directly into the system rather than operating as separate, standalone components. This change helps users better understand, reducing potential confusion when navigating the IT Access Console.

**Support for Ping Federate Integration with OPSWAT Identity Provider Multi-Factor Authentication**

In this release, This enhancement allows leveraging **Ping Federate's** authentication as part of Multi-Factor Authentication, which adds an additional layer of security to user authentication process.

By integrating Ping Federate with OPSWAT IdP MFA, users will experience seamless authentication while benefiting from advanced security measures. This integration ensures that access control is more robust, reducing the risk of unauthorized access and vulnerable devices while maintaining a smooth user experience.

## Release Date: January 20, 2025

Console Version: 3.51.0

Persistent Client for Windows: 7.6.2501.632

On-demand Client for Windows: 7.3.2501.345

Persistent Client for macOS: 10.4.2501.163

On-demand Client for macOS: 10.5.2501.132

Persistent Client for Redhat-based Linux: 15.6.2501.144

Persistent Client for Debian-based Linux: 15.4.2501.150

**Additions in this release**

1. "Peripheral Media Protection" and "Secure File Download" tabs shifted up in the navigation pane
2. New user interface implemented for Removable Media Protection
3. Enhancement and bug fixes.

## **More details:**

**"Peripheral Media Protection" and "Secure File Download" tabs shifted up in the navigation pane**

The order of the priority features is updated, as a result 'Peripheral Media Protection' and 'Secure File Download' is shifted up in the navigation pane.

**New user interface implemented for Removable Media Protection**

In this release, Removable Media Protection (RMP) has a new User interface (UI) in which the high level view visualizes all ports and their usage, while blocking policy management. In detail, the MetaDefender Endpoint shows 2 behaviors in new RMP feature, as below:

**Workflow:**

- **Full blocked mode:** When a USB drive is connected to a computer with USB Protection enabled, the user access to the drive will be automatically blocked. The user will be notified that a new USB device has been detected, but cannot view or access files on the drive.
- **Auto-blocked mode:** when a USB drive is connected, a user attempts to open or copy a file, the MetaDefender Endpoint will intercept this action and lock the file. This triggers a scanning pop-up to scan the file against the configured rules. The file is unlocked if the scan result is allowed, and remains locked if the scan result is blocked.

## Release Date: December 18, 2024

Console Version: 3.50.0

Persistent Client for Windows: 7.6.2412.609

On-demand Client for Windows: 7.3.2412.327

Persistent Client for macOS: 10.4.2412.156

On-demand Client for macOS: 10.5.2412.143

Persistent Client for Redhat-based Linux: 15.6.2412.143

Persistent Client for Debian-based Linux: 15.4.2412.149

**Additions in this release**

1. Improved Entra ID integration.
2. Improved Syslog Integration.
3. Improved License notification.
4. Improved SSO integration.
5. Allow admins to add local engines option for scanning
6. Enhancement and bug fixes.

## **More details:**

## **1.** **Improved Entra ID Integration.**

Improved Entra ID integration with IT Access. Administrators can customize the Entra-Company Branding page with a pre-defined URL from the OPSWAT Admin Console. This URL will be displayed on the Entra ID login or error page for users who are unable to log in. Users can access the remediation page to get the remediation instructions.

## **Copy pre-defined URL from** ***MD IT Access > Microsoft Entra ID***

## **Updated Company Branding at Entra Admin > Sign-in page’s Configuration**

**2. Improved Syslog Integration**

The enhanced Syslog integration stops if it fails to connect to the server after 100 error attempts.

Add notifications in the Syslog settings to alert users and ensure logs are written to Syslog events. It resets when the user clicks the enable button.

Change "Webhook Events" to "Integration Events" and add a new Syslog error notification.

Additionally, include a new Syslog Events option in the navigation bar.

Added new syslog error notification

Syslog events added to the navigation bar

Messages to notify users in syslog settings

**3. Improved License notification**

In this release, this feature helps to show a warning message if the current usage is over the contractual limit.

## **4.** **Improved SSO Integration**

Improve SSO - SP initiated flow between 3rd party Identity Provider and IT Access Console.

## **5.** **Allow admins to add local engines option for scanning**

Add support for local scanning engine to MetaDefender Endpoint, enhancing scanning capabilities and allowing for a more customized scanning environment tailored to specific needs.

## Release Date: November 14, 2024

Console Version: 3.49.0

Persistent Client for Windows: 7.6.2411.596

On-demand Client for Windows: 7.3.2411.321

Persistent Client for macOS: 10.4.2411.151

On-demand Client for macOS: 10.5.2411.119

Persistent Client for Redhat-based Linux: 15.6.2411.142

Persistent Client for Debian-based Linux: 15.4.2411.147

**Additions in this release**

1. Support Syslog integration.
2. Support Global & Group settings to show and hide the client features.
3. Enhancement and bug fixes.

## **More details:**

## **1.** **Support S3 Log Storage and Syslog on SIEM Integration.**

In this release, there is a new integration with syslog server. All the device events get saved in the syslog server.

## **2.** **Flexible Global & Group settings to increase Client Functionality**

Global Setting

In this release, this feature allows clients to tailor their requirements based on specific needs, improving efficiency and the overall client experience.

## Release Date: October 9, 2024

Console Version: 3.48.0

Persistent Client for Windows: 7.6.2410.580

On-demand Client for Windows: 7.3.2410.315

Persistent Client for macOS: 10.4.2410.149

On-demand Client for macOS: 10.5.2410.117

Persistent Client for Redhat-based Linux: 15.6.2410.141

Persistent Client for Debian-based Linux: 15.4.2410.146

**Additions in this release**

1. Added support process "Application Control" in the SOH report.
2. Added OS up-to-date posture check for Ubuntu Linux.
3. Bump OAuth API gets device details to version 3.11 and returns the domain controller, device model and device manufacturer details.
4. Enhancement and bug fixes.

## **More details:**

## **1. Added support process "Application Control" in the SOH report**

Enhancing the Patch Management (PM) processor to process "Application Control" checks on PM products mentioned in the SOH reports (applicable to Win and Mac)**

Policy setting

Device detail

## **2. Added** **OS up-to-date posture check for Ubuntu Linux**

**3. Bump OAuth API gets device details to version 3.11 and returns the domain controller, device model and device manufacturer details**

## Release Date: September 10, 2024

Console Version: 3.47.0

Persistent Client for Windows: 7.6.2409.556

On-demand Client for Windows: 7.3.2409.296

Persistent Client for macOS: 10.4.2409.148

On-demand Client for macOS: 10.5.2409.116

**Additions in this release**

1. Added support to display a warning message if the license is set to expire in the next 30 days.
2. Added support to download file transfer using Guest ID.
3. Bug fixes and UI enhancements.

**More details:**

**1. Added support to display a warning message, if the license is set to expire in the next 30 days**

In this release, the MD license expiration date is now clearly visible on the UI console, making it easier for the user to track and manage the subscription while removing the confusion and related difficulties.

**License expire soon**

## Release Date: August 20, 2024

Console Version: 3.46.0

Persistent Client for Windows: 7.6.2408.520

On-demand Client for Windows: 7.3.2408.281

Persistent Client for macOS: 10.4.2408.145

On-demand Client for macOS: 10.5.2408.112

Persistent Client for Redhat-based Linux: 15.6.2408.140

Persistent Client for Debian-based Linux: 15.4.2408.145

**Additions in this release**

1. Added support for Azure Conditional Access integration on Mac and Linux.
2. Improved the remediation page to display imminent issues.
3. Added support to show "device manufacturer" and "device model" information.
4. Added support to allow, block, or exempt peripheral devices.
5. Bug fixes and UI enhancements.

**More details:**

**Added support for Azure Conditional Access integration on Mac and Linux**

Administrators can configure Azure (Microsoft Entra ID) Conditional Access with OPSWAT Posture Check for macOS and Linux OS devices. Microsoft Intune is required for macOS and Linux Devices. The user can only log in to the Microsoft Portal or using Remote Desktop application if the device complies with the organization's policy.

Follow [this document](https://docs.opswat.com/macloud-sdp/integrations/microsoft-entra-id-integration) for the integration.

**Improved the remediation page to display imminent issues**

Imminent issues will be shown on the Remediation Page to remind users before their device status is changed to non-compliant.

**Added support to show "device manufacturer" and "device model" information**

Now, Administrators can collect the "device manufacturer" and "device model" information.

## Release Date: July 16, 2024

Console Version: 3.45.0

Persistent Client for Windows: 7.6.2407.505

On-demand Client for Windows: 7.3.2407.276

Persistent Client for macOS: 10.4.2407.143

On-demand Client for macOS: 10.5.2407.111

Persistent Client for Redhat-based Linux: 15.6.2407.139

Persistent Client for Debian-based Linux: 15.4.2407.144

**Additions in this release**

1. Added support for CIS Standards Compliance Dashboard.
2. Improved macOS Application Control
3. Added support accepts devices joined from specific domains
4. Added support excludes virtual ISO drives
5. Added support to enable/disable Bad USB protection
6. Bug fixes and UI enhancements.

**More details:**

**Added support for CIS Standards Compliance Dashboard**

- **Note:** This feature is in Controlled Release. Please contact OPSWAT Support if you would like to experience this feature.

**Improved macOS Application Control**

**Added support accepts devices joined from specific domains**

When enabling the setting and defining domains, all non-corporate devices will appear as unknown devices and require approval from administrators to become managed devices.

**Added support excludes virtual ISO drives**

**Added support to enable/disable bad USB protection**

## Release Date: June 18, 2024

Console Version: 3.44.0

Persistent Client for Windows: 7.6.2406.492

On-demand Client for Windows: 7.3.2406.268

Persistent Client for macOS: 10.4.2406.142

On-demand Client for macOS: 10.5.2406.110

Persistent Client for Redhat-based Linux: 15.6.2406.138

Persistent Client for Debian-based Linux: 15.4.2406.143

**Additions in this release**

1. Added support Azure Conditional Access integration
2. Added support history logs for OAuth APIs
3. Improve 3rd party SSO integration.
4. Added support notification when adding CVEs or applications to the allowlist.
5. Added support End of Life OS detection for iOS and Android.
6. Retired CVSS 2.0 score.
7. Added support new option that allows/blocks files by extension.
8. Added support Secure File Download for Chrome browser.
9. Bug fixes and UI enhancements.

**More details**

**Added support Azure Conditional Access integration**

Administrators can configure Azure (Microsoft Entra ID) Conditional Access with OPSWAT Device Posture Check. The user can only log in to the website or Remote Desktop application if the device complies with the organization's policy. Follow [this document](https://docs.opswat.com/macloud-sdp/integrations/microsoft-entra-id-integration) for the integration

Notes: support Windows devices only in this version.

**Added support history logs for OAuth APIs**

Administrators can now view the history logs when 3rd party vendor runs the device posture check via OAuth API

Enable the Log Event from the OAuth application setting to enable this feature.

**Improve 3rd party SSO integration**

The first time 3rd party users access to the console, they must enter the secret code sent to their email

**Added support notification when adding CVEs or applications to the allowlist.**

**Added support End of Life OS detection for iOS and Android**

**Retired CVSS 2.0 score**

OPSWAT no longer supports CVSS 2.0 score on vulnerability policy rules.

**Added support new option that allows/blocks files by extension.**

**Added support Secure File Download for Chrome browser.**

## Release Date: May 22, 2024

Console Version: 3.43.0

Persistent Client for Windows: 7.6.2405.482

On-demand Client for Windows: 7.3.2405.264

Persistent Client for macOS: 10.4.2405.139

On-demand Client for macOS: 10.5.2405.105

Persistent Client for Redhat-based Linux: 15.6.2405.136

Persistent Client for Debian-based Linux: 15.4.2405.141

**Additions in this release**

1. MetaDefender IT-OT Access is now changed to MetaDefender Access
2. Ability to view client ID logs as the submitter
3. Added new options to Reporting History
4. Ability to flag as issues if certain applications are not installed or running
5. Automatic scanning mode is available on MetaDefender Endpoint
6. Bug fixes and UI enhancements: Improved performance and user experience

- **MetaDefender IT-OT Access is now changed to MetaDefender Access**

MetaDefender IT-OT Access is rebranded as MetaDefender IT Access. This name change is reflected across platforms, including the OPSWAT website, MetaDefender IT-OT Access Admin Console, MetaDefender Endpoint UI, MetaDefender IT-OT Access Documents, and MetaDefender IT-OT Access Email Alert Notification.

- **Ability to view client ID logs as the submitter**

When performing any action using API, administrators are now able to view Client IDs as the submitter instead of the account owner in log details.

To display the information, follow these steps:

1. Navigate to '**Logs'** > '**Device Events'**.
2. Choose the desired action and click on '**View details'** for more information.

- **Added new options to Reporting History**

If your endpoints remains non-compliant for consecutive days, it will be automatically removed. You can now view the details via newly added option '**Removed due to continuous non-compliance**'.

1. Navigate to '**Logs**' > '**Device Events**'.
2. In the filter dashboard, choose '**Removed due to continuous non-compliance**'.
3. Click '**Save**' to apply filter. You are now able to view details of the device deleted by configuration.

- **Ability to flag as issues if certain applications are not installed or running**

Application Control now lets you set mandatory applications for your organization. Any device not equipped with or running these essential programs will be flagged for non-compliance.

To enable this feature, follow these steps:

1. Navigate to '**Policy**' > '**Policy Management**' and choose your policy from the list.
2. Go to '**Application Control'** section.
3. Choose the applications and set your desired statuses.
4. Click **'Save**' to apply new settings.

- **MetaDefender Endpoint now supports automatic scanning mode**

When users use removable media (e.g: USB drives, SD cards, DVDs,...) and access files, automatic scanning mode is available through MetaDefender Endpoint, ensuring higher security for external files.

Enable this from MetaDefender IT Access console:

1. Navigate to '**Policy**' > '**Policy Management**' and choose your policy from the list.
2. Go to '**Advanced Endpoint Protection**' > '**Enable Threat Detection for Windows'**.
3. Choose '**On-Access File Scanning**', make sure you have turned on '**Enable Removable Media Protection**'.
4. Click '**Save**' to apply new settings.

Once enabled, you will be able to see file details from MetaDefender Endpoint.

## Release Date: Apr 17, 2024

Console Version: 3.42.0

Persistent Client for Windows: 7.6.2404.457

On-demand Client for Windows: 7.3.2404.253

Persistent Client for macOS: 10.4.2404.136

On-demand Client for macOS: 10.5.2404.104

Persistent Client for Redhat-based Linux: 15.6.2404.131

Persistent Client for Debian-based Linux: 15.4.2404.135

**Additions in this release**

1. OS update check is available for macOS users
2. Enable Security Score function in MetaDefender Endpoint
3. Added new charts for Compliance Dashboard
4. Ability to download past allowlist CVE uploads
5. Improve mismatch issues between SDK and Window Update Agent
6. Manage Multi-factor Authentication with MyOPSWAT and MetaDefender IT-OT Access
7. Action logs now include more device information
8. MetaDefender Endpoint System Tray is available on Ubuntu Linux
9. Bug fixes and UI enhancements: Improved performance and user experience

- **OS update check is available for macOS users**

Mac users can now easily perform OS update checks for their devices.

Within the **'Deep Compliance'** section, navigate to **'Operating System'** and configure the desired frequency for these checks. Additionally, select the severity level to ensure your devices comply with the most critical updates.

- **Enable Security Score function in MetaDefender Endpoint**

Security Score is a function that helps score your cyber risk based on various factors, giving you a comprehensive view of security and improvement tips**.** You can now enable it with 2 options:

1. For Global Settings:

   1. Go to '**Settings' > 'Global'**
   2. Navigate to the **'Device Client'** section
   3. Scroll down and enable **'Show Security Score page'**
   4. Click **Save** to apply the changes

2. For Group Settings:

   1. Go to **'Inventory'** > '**Device Group'**
   2. In **'Settings'** section, enable **'Agent'**
   3. Choose **'Show Security Score page'**
   4. Click **Save** to apply the changes

Once enabled, you'll see the Security Score tab within MetaDefender Endpoint.

- **Added new charts for Compliance Dashboard**

We've added new chart options to your Compliance Dashboard to help you easily identify and track key metrics. Newly added options include: Critical & Warning Issues Trend, Device Status Trend, Category Trends.

Add those charts to your dashboard simply by:

1. Navigate to '**Dashboard'** > '**Compliance"**
2. Click on '**Edit mode'**
3. Choose the charts you want to add
4. Click **Save** to finalize your updated dashboard

- **Ability to download previous allowlist CVE uploads**

Users can now view and download previous allowlist CVE uploads, enabling easier backup and bulk editing.

The list appears in chronological order when you navigate to **'Vulnerabilities**' > '**Allowlist CVEs**'.

- **Improve mismatch issues between SDK and Windows Update Agent**

Compatibility issue issues between SDK and Windows Update Agent is currently resolved. Users can expect smoother and less interrupted performance.

- **Manage Multi-factor Authentication with MyOPSWAT and MetaDefender IT-OT Access**

We've updated our multi-factor authentication (MFA) management process. Your MFA settings are now located within MyOPSWAT.

For users previously using MFA with MetaDefender IT-OT Access**:** Simply navigate to '**Manage Account' > 'User Profile'** and scroll down to '**Multi-factor Authentication'**. A pop-up message will guide you through the process.

- **Action logs now include more device information**

We've improved your action logs to provide richer device information for exported data. This update includes: Device MAC, Device ID, Device User, Group.

- **MetaDefender Endpoint System Tray is available on Ubuntu Linux**

The MetaDefender Endpoint System Tray is now available for Ubuntu Linux users. This addition provides basic functionalities.

## Release Date: Mar 19, 2024

Console Version: 3.41.0

Persistent Client for Windows: 7.6.2403.434

On-demand Client for Windows: 7.3.2403.246

Persistent Client for macOS: 10.4.2403.123

On-demand Client for macOS: 10.5.2403.94

Persistent Client for Redhat-based Linux: 15.6.2403.128

Persistent Client for Debian-based Linux: 15.4.2403.130

**Additions in this release**

1. Added support customize remediation page to provide a means for users to trigger the creation of a service desk ticket if remediation page does not help
2. Added support the capability to enforce devices to update their antivirus to a minimum of one version behind, enhancing security protocols
3. Added support option to automatically relocate non-compliant devices to the designated group after a defined period
4. Added support Key Rotation Schedule feature within OAuth Applications
5. Improved OS update configuration options
6. Bug Fixes and UI Enhancement: Resolved issues and improved user interface for a smoother experience.

- **Added support customize remediation page to provide a means for users to trigger the creation of a service desk ticket if remediation page does not help**

Administrators now have the ability to include a service desk link directly within the remediation page, enabling users to easily contact the organization's administrators for assistance.

1. Navigate to the '**Rebranding**' section within Settings.
2. Select '**Service Desk URL**' under '**Support Type**' within Rebranding section.
3. Enter your organization's service desk link in the provided '**Link**' section.
4. Click Save to apply the changes.

- **Added support the capability to enforce devices to update their antivirus to a minimum of one version behind, enhancing security protocols**

In the Anti-Malware section of Deep Compliance, select 'Version Behind' from the drop-down menu, and specify the number of allowed versions within the '*Signature definition is updated at least every*' option. Selecting the criticality is essential to ensure that devices comply accordingly.

- **Added support option to automatically relocate non-compliant devices to the designated group after a defined period**

Administrators can now have the ability to configure devices to be seamlessly moved to specific groups if they persist in non-compliance, enhancing the efficiency of compliance management.

1. Go to **'Globa**l' under Settings.
2. Select 'Move devices to the [Default] group if they remain non-compliant for [number] consecutive days.'
3. Specify the designated group and set the allowed number of days.

- **Added support Key Rotation Schedule feature within OAuth Applications**

Administrators can now activate the Key Rotation Schedule within OAuth Applications. When the OAuth 2 Key Pair Rotation Checker is executed, users can access the rotated key within OAuth Applications section by clicking 'Show' on the top notification. Users will receive automatic email notifications, and the system will log this information for auditing purposes.

Enter the generated key and secret to obtain a new client key and client secret under OAuth Keys.

- **Improved OS update configuration options**

Administrators now possess the ability to meticulously configure OS updates. This includes

1. Automatically update required missing patches
2. Hide the option missing patches from the client UI

**OS updates within Policy Control Settings**

## [Release Date: Feb 20, 202](https://docs.opswat.com/macloud-sdp/release-notes/cloud-console)4

Console Version: 3.39.0

Persistent Client for Windows: 7.6.2401.411

On-demand Client for Windows: 7.3.2401.234

Persistent Client for macOS: 10.4.2401.118

On-demand Client for macOS: 10.5.2401.89

Persistent Client for Redhat-based Linux: 15.6.2401.125

Persistent Client for Debian-based Linux: 15.4.2401.124

**Additions in this release**

1. More options in application version control
2. NERC CIP Email Report is available
3. AppRemover is now supported to uninstall applications for macOS
4. The application allowlist can now be applied for specific policies or devices
5. Added support "Exclude unformatted media" option
6. Added support "Get Full Report option" after scanning on Linux device
7. Added "workflow rule" information in Malware Scan Report
8. UI Improvements and bug fixed

- **More options in application version control**

Administrators can now specify application versions greater or lower than a specified one, providing finer control over application blocking rules.

- **NERC CIP Email Report is available**

The NERC CIP Report widget in the dashboard now supports an email report feature, allowing administrators to receive comprehensive reports directly in their inbox.

- **AppRemover is now supported to uninstall applications for macOS**

AppRemover function is now fully supported on macOS. Users can now use AppRemover to uninstall unneeded applications seamlessly on their macOS devices.

- **The application allowlist can now be applied for specific policies or devices**

Administrators now have the ability to add particular applications to the allowlist and apply them to specific policies or individual devices.

- **Added support "Exclude unformatted media" option.**

The "Exclude Unformatted Media" option has been added to the MetaDefender IT-OT Access/ MetaDefende IT-OT Access On-prem console. Users can use this to filter out any unformatted media within the "Removable Media Protection" field.

- **Added support "Get Full Report option" after scanning on Linux device**

Upon completing a scan on Linux devices, users can now access a detailed report through the "Get Full Report" option.

- **Added "workflow rule" information in Malware Scan Report**

In Removable Media Protection and Malware Scan, a workflow rule is now included in the scan report (available in PDF/CSV format) when the Cloud workflow rule is empty, ensuring improved reporting clarity.

- **UI Improvements**

Updated new design for scanning notification (Windows)

Updated font for the MetaDefender Endpoint in both Windows and MacOS agents

- **Major Bug Fix: Media Eject Functionality**

Addressed a critical issue regarding the non-functionality of the Media Eject feature. New Eject function is now available for seamless experience. _ _

## [Release Date: Jan 16, 202](https://docs.opswat.com/macloud-sdp/release-notes/cloud-console)4

Console Version: 3.39.0

Persistent Client for Windows: 7.6.2401.411

On-demand Client for Windows: 7.3.2401.234

Persistent Client for macOS: 10.4.2401.118

On-demand Client for macOS: 10.5.2401.89

Persistent Client for Redhat-based Linux: 15.6.2401.125

Persistent Client for Debian-based Linux: 15.4.2401.124

**Addition in this release**

- Rebranded **MetaAccess** to **MetaDefender IT-OT Access**
- Rebranded **OPSWAT Client** to **MetaDefender Endpoint**
- Ability to support Apple Silicon M1/M2 chip

This name change is reflected across various platforms, including the OPSWAT website, MetaAccess Admin Console, OPSWAT Client UI, MetaAccess Documents, and MetaAccess Email Alert Notification.

## [Release Date: Dec 19, 202](https://docs.opswat.com/macloud-sdp/release-notes/cloud-console)3

Console Version: 3.38.0

Persistent Client for Windows: 7.6.2312.398

On-demand Client for Windows: 7.3.2312.229

Persistent Client for macOS: 10.4.2312.109

On-demand Client for macOS: 10.5.2312.82

Persistent Client for Redhat-based Linux: 15.6.2312.124

Persistent Client for Debian-based Linux: 15.4.2312.123

**Additions in this release**

1. Added support download metadata file for IdP MFA integration
2. Added support Browser Extension policy rule
3. Added support approved OS version for Debian Linux distro
4. Added support check Firewall status based on inbound and outbound rules
5. Added support Vulnerability Severity and OS-Patch Severity by days
6. Improved OPSWAT Client Vulnerability user experience
7. Bug Fixes and UI Enhancements: Resolved issues and improved user interface for a smoother experience.

**Added support download metadata file for IdP MFA integration .**

Administrators now have the ability to download IdP metadata file and import to the Service Provider.

**Compliance**

- **Added support Browser Extension policy rule**

Administrators now can identify and monitor unexpected browser extensions on the device. OPSWAT provides a list of bad browser extensions. The list will be maintained and updated by the OPSWAT team. Administrators also can block a specific extension by using the custom list.

- **Added support approved OS version for Debian Linux distro.**

Administrators now can configure an approved version for the Ubuntu Linux distro

- **Added support check Firewall status based on inbound and outbound rules**

**Vulnerabilities and Patch Management**

- **Added support Vulnerability Severity and OS-Patch Severity by days**

The administrator now can have the ability to configure different days for patches and vulnerabilities based on patch severity level, categories, or vulnerability severity level

- **Improved OPSWAT Client Vulnerability user experience**

## [Release Date: Nov 22, 202](https://docs.opswat.com/macloud-sdp/release-notes/cloud-console)3

Console Version: 3.37.0

Persistent Client for Windows: 7.6.2310.391

On-demand Client for Windows: 7.3.2311.219

Persistent Client for macOS: 10.4.2310.106

On-demand Client for macOS: 10.5.2311.79

Persistent Client for Redhat-based Linux: 15.6.2311.120

Persistent Client for Debian-based Linux: 15.4.2311.120

Additions in this release

1. Enhance Inventory Device View Filtering
2. Aged Device Management in Inventory
3. Ensure all necessary patches are included in Windows Updates
4. Advanced Endpoint Protection. Implement Scan Threat Detection for Linux system
5. Advanced Endpoint Protection. Enhance USB Security with manifest files
6. OPSWAT Client. Provide update status for devices with On-Demand OPSWAT Client
7. OPSWAT Client. Enable MetaAccess account switching in OPSWAT Client
8. Bug Fixes and UI Enhancements: Resolved issues and improved user interface for a smoother experience.

**Enhance Inventory Device View Filtering.**

Administrators now have the flexibility to customize the display of information within the device list. While essential details like status, name and agent remain mandatory, you can tailor the view by toggling the display of additional information columns.

**Aged device management in Inventory**

Administrators now have the capability to identify and monitor unresponsive device, categorizing them into a designated group for streamlined inclusion in the automatic deletion process. Within **Device Data** in **Global Settings**, choose '**Force the unresponsive device to group before deleting it.**'

**Compliance**

- **Ensure all necessary patches are included in Windows Updates.**

Some essential patches may not be available through standard Windows Updates. To enhance security issues by addressing all patch updates, MetaAccess ensures the implementation of all OS updates on managed devices. Select "**Ensure to include all patches listed on Microsoft Update page, even those that may not be applicable within Windows Updates on your device**." under **Policy > Deep Compliance > Operating System > Windows**.

This rule encourages users to regularly update their operating system through a proactive approach including manual methods. For additional details on addressing update issues, please refer to [this page](https://docs.opswat.com/macloud-sdp/kb/how-do-i-address-os-update-issues-on-opswat-client-metaaccess-am).

**Advanced Endpoint Protection**

- **Implement Scan Threat Detection for Linux system.**

Here are two methods to enable Threat Detection for Linux:

1. **Via Console Interface:** Navigate to Policies, select Advanced Threat Detection, and enable Threat Detection for Linux by configuring the scanning server and setting the interval. The action log will be reflected similarly to Windows and Mac.
2. **Using Command (806):** Activate Threat Detection by executing command 806.

Both actions will generate reports accessible through the MetaAccess Console.

- **Enhance USB Security with manifest files**

Navigate to Policies, under Removable Media Protection, where administrators can:

1. Enable "**Use Media Manifest**" to permit the unblocking of USB devices that were previously scanned and contain with manifest files. This enhancement now initiates the scan of multiple manifest files simultaneously. In case of USBs that were not scanned before, users are allowed to perform manual actions within the OPSWAT Client UI.
2. Activate **"Blocks all files not found on Media Manifest"** allowing OPSWAT Client to automatically scan and unblocked USBs with allowed files that have been previously scanned.

For additional information and details of Media Manifest, refer to [this page](https://docs.opswat.com/mdkiosk/knowledge-base/setting-up-media-manifest).

**OPSWAT Client**

- **Provide update status for devices with On-Demand OPSWAT Client**

Users will now receive progress update notification, enhancing their awareness of the update process.

- **Enable MetaAccess account switching in OPSWAT Client.**

Users can seamlessly switch between different MetaAccess accounts without the need to delete and reinstall OPSWAT Client. Simply click the ellipsis (...) icon, choose "Switch Account," and input the Registration Code, Server Address, and Group ID for the new account.

## [Release Date: Oct 18, 202](https://docs.opswat.com/macloud-sdp/release-notes/cloud-console)3

Console Version: 3.36.0

Persistent Client for Windows: 7.6.2310.381

On-demand Client for Windows: 7.3.2310.212

Persistent Client for macOS: 10.4.2310.103

On-demand Client for macOS: 10.5.2310.76

Persistent Client for Redhat-based Linux: 15.6.2310.114

Persistent Client for Debian-based Linux: 15.4.2309.117

Additions in this release

1. Application Control**:** Implement application control for Linux systems
2. Enable Browser Extension Detection in MetaAccess
3. OPSWAT Client: The capability to delete files before scanning
4. Bug Fixes and UI Enhancements: Resolved issues and improved user interface for a smoother experience.

**Compliance**

- **Application Control:** **Implement application control for Linux systems.**

To utilize the application control for Linux system, simply access the Application Control section within Policies and select the dedicated operating system for configuring controls

For more details, please visit [Application Control](https://docs.opswat.com/macloud-sdp/3.34.0/configuration---management/application-control--blocking-applications) page.

- **Enable Browser Extension Detection in MetaAccess.**

Now, OPSWAT Client can detect browser extensions installed on managed devices and report them to the MetaAccess Control Management system. Administrators can easily view these extensions:

1. Accessing Browser Extensions in MetaAccess:

   - Navigate to 'Browser Extensions' under 'Inventory' in MetaAccess.
2. Filtering Extensions by Browser:

   - Click the filter icon in the top right corner.
   - Select the specific browser you want to filter.
   - Click 'Update' to view the filtered results.
3. Viewing Installed Devices or Versions: - - Choose the Extension ID to see the installed devices or installed versions.

OPSWAT Client

- **The capability to delete files before scanning.**

Users can now remove unwanted files before initiating the scan.

## Release Date Sep 20, 2023

Console Version: 3.35.0

Persistent Client for Windows: 7.6.2309.370

On-demand Client for Windows: 7.3.2309.209

Persistent Client for macOS: 10.4.2308.92

On-demand Client for macOS: 10.5.2309.67

Persistent Client for Redhat-based Linux: 15.6.2309.1112

Persistent Client for Debian-based Linux: 15.4.2309.114

Additions in this release

1. Application Control**:** Refine the application control user interface, elevating its usability and delivering and effortlessly smooth experience when managing your application control
2. In-Grace Period: Pause the grace period settings when the device is offline
3. Add end-of-support applications to Potential Unwanted Application
4. Introduce auto-update OS compliance enforcement settings
5. Enable automatic application updates in macOS
6. Switch from PIN to requiring password when uninstall OPSWAT Client
7. OPSWAT Client: Revamp the design for Removable Media Protection, with a focus on enhancing aesthetics, functionality, and user experience
8. OPSWAT Client: Enable users to burn specific files to a CD through Advanced Endpoint Protection, especially when the policy is configured to block removable drives
9. Bug Fixes and UI Enhancements: Resolved issues and improved user interface for a smoother experience.

**Compliance**

- **Application Control: Refine the application control user interface, elevating its usability and delivering and effortlessly smooth experience when managing your application control.**

In our latest update, we've introduced visual enhancements to the application control settings, enhancing the comprehensiveness of the user interface and ensuring a seamlessly usable experience. These improvements affect the navigation within this section, particularly in two key areas:

1. Applying controls to categories.
2. Applying controls to applications within those categories.

To utilize these enhancements, simply access the Application Control section within Policies and select the dedicated operating system for configuring controls.

Applying controls to categories:

- Click the dropdown to set criticality for categories with installed applications.
- Define expected actions.
- Click 'Save' to apply settings.

Applying controls to individual applications within categories:

- Use the 'Search for Application' field to find the desired application.
- Specify the version.
- Set criticality for the category if the application is installed or running.
- Define expected actions.
- Click 'Save' to confirm your changes.

For more details, please visit [Application Control](https://docs.opswat.com/macloud-sdp/3.34.0/configuration---management/application-control--blocking-applications) page.

- **In-Grace Period: Pause the grace period settings when the device is offline.**

In MetaAccess, policies are established to enable devices to enter a grace period for remediation and full compliance. Recognizing that many devices may be offline or out of network during this grace period, administrators now have the ability to pause the grace period when a device is offline. To activate this:

1. Go to the '**Grace Period**' section under '**Device Client**' in the Global settings.
2. Enable the option *'Allow devices within the grace period to enter pause state while offline.'*

- **Add end-of-support applications to Potential Unwanted Application.**

As Internet Explorer has become outdated and is no longer supported by Microsoft, our platform will no longer support this application. To accommodate this change, we have moved Internet Explorer into the Potentially Unwanted Application (PUA) section. Administrators can now configure it as either a blocked or allowed application as needed.

1. Navigate to the Potential Unwanted Application within Policies.
2. To allow or block End of Life applications, click the 'Add Exception' button.

- **Introduce auto-update OS compliance enforcement settings.**

Now administrators can enforce automatic operating system updates by going to **Operating System** under **Policies**. Simply click '*Attempt to enforce automatic updates for all outdated OS patches*'

Vulnerabilities & Patch Management

- **Enable automatic application updates in macOS.**

Administrators can easily enforce application patching by selecting 'Automatically update 3rd-Party software' in the 'Application Updates' section under Patch Management of Policies.

**Advanced Endpoint Protection**

- **Switch from PIN to requiring password when uninstall OPSWAT Client.**

For enhanced security, administrators can now set a shareable password with a minimum requirement of four characters, including numbers, letters, and special characters, when uninstalling the OPSWAT Client from devices.

Set sharable password when users uninstall OPSWAT Client on devices

Set sharable password when device group uninstall OPSWAT Client on devices

**OPSWAT Client**

- **Revamp the design for Removable Media Protection, with a focus on enhancing aesthetics, functionality, and user experience.**

When the administrator configures Removable Media Protection in the Threat Detection section, the OPSWAT Client will present the 'Removable Media' tab, enabling device scanning and monitoring of scanned files.

- **Enable users to burn specific files to a CD through Advanced Endpoint Protection, especially when the policy is configured to block removable drives.**

Once administrators configure Removable Media Protection, the OPSWAT Client will automatically scan devices upon detecting removable media. Users can access the 'Removable Media' section to monitor scanned files and perform actions such as unblocking, copying, or burning discs.

**Hotfix**

On September 28, we deployed a hotfix that updated the device name from 'Hostname-Laptop' to 'Hostname's Laptop' and also included the 'host_name' as 'hostname-Laptop'.

## Release Date: Aug 16, 2023

Console Version: 3.34.0

Persistent Client for Windows: 7.6.2308.348

On-demand Client for Windows: 7.3.2308.199

Persistent Client for macOS: 10.4.2308.89

On-demand Client for macOS: 10.5.2308.63

Persistent Client for Redhat-based Linux: 15.6.2308.109

Persistent Client for Debian-based Linux: 15.4.2308.111

**Additions in this release**

1. Application Control**:** Enhance the application control capabilities to encompass a wider range of product versions and variations
2. Compliance Dashboard: Fine-tune its statistic with a better intuitive approach to manage and monitor non-compliant devices
3. Export Events: enhance the progress while export events among Device List and Known-Exploited-Vulnerabilities
4. Revamp OS patch detection mechanism for an accurate and efficient identification and report upon operating system patches
5. The ability to filter supported KEV (Known-Exploited-Vulnerabilities) information via OAuth API
6. A secure download feature for WhatsApp application
7. OPSWAT Client offers the capability for handling NTFS ADS (NTFS Alternate Data Streams) file scanning
8. OPSWAT Client enhances batch processing within Media Scan
9. Bug Fixes and UI Enhancements: Resolved issues and improved user interface for a smoother experience.

**Compliance**

- **Compliance Dashboard: Fine-tune its statistic with a better intuitive approach to manage and monitor non-compliant devices**

Our latest visual enhancement provides you with a comprehensive overview of device compliance statuses. This includes the number of devices categorized as compliant, in the grace period, non-compliant, and exempted.

Administrators can now proactively manage and enhance compliance by monitoring device statuses. By utilizing these insights, you can effectively work towards reducing the percentage of non-compliant devices.

**Vulnerabilities & Patch Management**

- **Export Events: enhance the progress while export events among Device List and Known-Exploited-Vulnerabilities.**

Admin can effortlessly monitor the status of exported events and take necessary actions based on real-time information.

- **The ability to filter supported KEV (Known-Exploited-Vulnerabilities) information via OAuth API.**

API-based KEV detections let administrators identify KEVs and map its CVE. To view the API documentation:

1. [Get vulnerabilities of a device](https://docs.opswat.com/macloud-sdp/developer-guide/get-vulnerabilities-of-a-device)
2. [Get vulnerabilities](https://docs.opswat.com/macloud-sdp/developer-guide/get-vulnerabilities)

**Advanced Endpoint Protection**

- **A secure download feature for WhatsApp application.**

Enabling Secure Download for WhatsApp Application in the Threat Detection Section empowers administrators to monitor downloaded files effectively. Once activated, this feature facilitates tracking the status of files downloaded via WhatsApp in the OPSWAT Client's Secure Download module.

1. "Blocked" indicates files that are not permitted, providing visibility into disallowed content.
2. "Allowed" indicates files that are permissible, offering insight into approved content.

- **OPSWAT Client offers the capability for handling NTFS ADS (NTFS Alternate Data Streams) file scanning**

NTFS ADS file scanning presents two distinct modes.

1. Default Mode: Seamlessly scans the file's mainstream components without generating warnings
2. Warning Mode: When activated, if ADS are present, OPSWAT Client will include a cautionary message in the PDF or CSV report, stating 'Alternate data streams were detected and ignore."

- **OPSWAT Client enhances batch processing within Media Scan**

When processing a batch of files, the OPSWAT Client now consolidates the results of the specific batch scan into a single entry within the history section. This enhancement empowers administrators with efficient tracking and access to comprehensive details.

## [Release Date: Jul 19, 2023](https://docs.opswat.com/macloud-sdp/release-notes/release-notes)

Console Version: 3.33.0

Persistent Client for Windows: 7.6.2306.298

On-demand Client for Windows: 7.3.2306.158

Persistent Client for macOS: 10.4.2306.80

On-demand Client for macOS: 10.5.2306.54

Persistent Client for Redhat-based Linux: 15.6.2306.103

Persistent Client for Debian-based Linux: 15.4.2306.106

**Additions in this release**

1. Geofencing: Introducing location-based compliance checks for enhanced security.
2. "Fetch-log" Option: Simplify troubleshooting for admins with quick log fetching in OnDemand Client.
3. Vulnerability Dashboard Widget: Highlight unpatched vulnerabilities for better prioritization.
4. Improved Vulnerability Calculation: A revised formula to reflect total number of vulnerabilities.
5. Auto-Enable Antiphishing: Enhance browser security with automatic antiphishing activation.
6. Minimum ChromeOS Version Policy: Set compliance rules for minimum ChromeOS versions.
7. Checksum-Hash Support: Verify download authenticity on the Client Download Page.
8. Bug Fixes and UI Enhancements: Resolved issues and improved user interface for a smoother experience.

**Compliance**

- **Geofencing: Introducing location-based compliance checks for enhanced security.**

With geolocation-based controls, users gain the power to define and regulate device compliance rules based on their geographical location. Administrators now have the flexibility to select specific countries as "blocked countries," categorizing devices from these regions as non-compliant. Consequently, access to designated resources can be restricted based on your secure access configuration.

1. Activate the compliance and click select.
2. By default, when administrators activate Geofencing service, all countries will be added to allowed list. The administrator can choose the unauthorized countries into block list.

Enable Location Service

Administrators must enable Location Service to successfully fetch the local location's log from device. To enable Location Service, go to Global Setting to activate it.

- **Minimum ChromeOS Version Policy: Set compliance rules for minimum ChromeOS versions.**

Admin now can set the minimum allowable ChromeOS to latest or specific version.

- **Auto-Enable Antiphishing: Enhance browser security with automatic antiphishing activation.**

Administrator can enforce devices to automatically enable Antiphishing within allowable browsers such as Google, Firefox, and Microsoft Edge by clicking "Attempt to enable Antiphising" in Policy Configuration.

As reflected by above action, devices are required to remediate by enabling Antiphising to compliance.

**Vulnerabilities & Patch Management**

- **Vulnerability Dashboard Widget: Highlight unpatched vulnerabilities for better prioritization.**

MetaAccess are now publishing the overview dashboard to vulnerabilities. The total number of Vulnerabilities by Severity is reflected by the total number of CVE in all devices within an organization. By clicking in the no. of outstanding remediations to view the detailed CVEs.

**Advanced Endpoint Protection**

- "Fetch-log" Option: Simplify troubleshooting for admins with quick log fetching in OnDemand Client.

Administrators can fetch device log from OPSWAT Client to support request, even when device is not actively connect to MetaAccess.

- **Checksum-Hash Support: Verify download authenticity on the Client Download Page.**

To allow admins to validate the downloaded file before distribution , hash file info will be displayed in the client's Download page.

## Release Date: June 20, 2023

Console Version: 3.32.0

Persistent Client for Windows: 7.6.2306.298

On-demand Client for Windows: 7.3.2306.158

Persistent Client for macOS: 10.4.2306.80

On-demand Client for macOS: 10.5.2306.54

Persistent Client for Redhat-based Linux: 15.6.2306.103

Persistent Client for Debian-based Linux: 15.4.2306.106

**Additions in this release**

1. Added support User Interface for Mac Client.
2. Added support Geolocation for Mac Client.
3. Added location information in Client UI.
4. Rearrange tabs and contents on the Policy menu

1. Improve performance for SIEM integration.

**Compliance**

1. Added support new grace period rule for Vulnerability and Patch Management categories.

- Administrators can configure a grace period for the Vulnerability and Patch Management categories and give the user a period of time to resolve the issue before the device status changes to non-compliant. During this time, a warning message will be displayed on the remediation page and remind the user to fix the issue.

2. Added support new policy rule to control the frequency of the OS reboot for mobile devices

**Advance Endpoint Protection**

1. Added support ejecting an USB inside the OPSWAT Client UI

## [Release Date: May 16, 202](https://docs.opswat.com/macloud-sdp/release-notes#release-date-december-21-2021)3

Console Version: 3.31.0

Persistent Client for Windows: 7.6.2305.262

On-demand Client for Windows: 7.3.2305.138

**Additions in this release**

1. Added device information when exporting the list of installed applications.

2. Improved user experience on Policy configuration.

3. Improved the session timeout on the Console.

**Compliance**

1. Added support posture checks for end-of-life macOS.

2. Improved AppRemover page on Client UI.

**Vulnerability and Patch Management**

1. Added support posture checks for required missing patches.

- **Note:** When "required missing patches" is selected, MetaAccess will not require users to install the optional OS missing patches to fix vulnerabilities associated with optional OS missing patches.

**Advance Endpoint Protection**

1. Added more detail for scanning time on Client UI.

2. Enhanced the Removable Media feature
3. Enhanced scanning for System Volume Information files
4. Added support Encrypted USB DataTraveler 4000 G2

## [Release Date: April 18, 202](https://docs.opswat.com/macloud-sdp/release-notes#release-date-december-21-2021)3

Console Version: 3.30.0

Persistent Client for Windows: 7.6.2304.247

On-demand Client for Windows: 7.3.2304.117

Persistent Client for macOS: 10.4.2304.66

On-demand Client for macOS: 10.5.2304.40

Persistent Client for Redhat-based Linux: 15.6.2303.102

Persistent Client for Debian-based Linux: 15.4.2303.105

**Additions in this release**

1. Added support for geolocation of devices. The administrator can see the number of compliant or non-compliant devices on the map. To collect the device geolocation, the administrator needs to update the privacy setting on the MetaAccess console and end-users need to accept OPSWAT Client collect the geolocation.

2. Added support for new filter: deleted devices by admin via OAuth API.

3. Improved the Device filter

4. Added support for new versions of some OAuth APIs

- Get Logs, version 3.3: added a new filter *deleted_api* for filter.events
- Account Detail, version 3.2: Added a new “score_type”
- Get vulnerabilities, version 3.1: Added support for multiple CVSS scores on the response data
- Get vulnerabilities of a device, version 3.1: Added support for multiple CVSS scores on the response data

**Compliance**

1. Added support for auto-remediation for Firewall and Antimalware issues on the Compliance page

2. Added support for new filter for compliance issues in the Operating System category.

**Vulnerability and Patch Management**

1. Added support for manual updates for OS missing patches in the OPSWAT Client.

- **Note:** this feature is in Controlled Release, contact OPSWAT Support if you would like to experience this feature.

**Advance Endpoint Protection**

1. Allow users to switch the scan source between multiple MD Cores (or MD Cloud) in the OPSWAT Client

## [Release Date: March 21, 202](https://docs.opswat.com/macloud-sdp/release-notes#release-date-december-21-2021)3

Console Version: 3.29.0

Persistent Client for Windows: 7.6.2303.194

On-demand Client for Windows: 7.3.2303.101

Persistent Client for macOS: 10.4.2303.59

On-demand Client for macOS: 10.5.2303.35

Persistent Client for Redhat-based Linux: 15.6.2303.102

Persistent Client for Debian-based Linux: 15.4.2303.105

SDP Gateway: 1.6.4

**Additions in this release**

1. Updated SSL Certificate.
2. Added support for device compliance information when exporting devices.

**Compliance**

1. Added support for auto-remediate lock screen timeout.

2. Added support for encryption policy check for Linux on additional local volumes and removable volumes.

3. Added support for new option to override group assignment when using Playbooks.

4. Added subtitles to explain features for each compliance category policy.

**Vulnerability and Patch Management**

1. Enhanced vulnerability features to reflect selected CVSS score.
2. Added support for trend of vulnerable devices in your organization.

**Advance Endpoint Protection**

1. Refinements to the layout and messaging in the OPSWAT Client UI.
2. Added more details to the Scanning Report regarding encrypted files and skipped files.

**Secure Access**

1. SDP: Windows client supports more kinds of locked down environments.
2. SDP: Windows and Mac clients support SAML users with very large numbers of groups defined in the IDP.
3. SDP: Various bug fixes related to have too many resources available to a client.

## MetaAccess 3.28.0 - February 21, 2023

**1. Improve onboarding experience.**

- Added a wizard to help new user set up their account easier and faster.

**2.** **Compliance Policy**

- Improved the handling of the OS Patch compliance
- Added ability to change device status after the grace period expires, whether the device is online at the time or not

**3.** **Malware Detection**

- Added the ability to exclude specific files or hashes when scanning for threats.

**4. Vulnerability and Patch Management**

- Added ability to choose CVE scoring system from the global setting

**5.** **Account Global Setting**

- Added support to choose local timezone or UTC timezone CVE scoring system from the global setting

**6.** **Dashboard**

- Added support two new widgets:

  - Operating System EOL
  - Operating System Out-of-date

**7.** **Fix several bugs**

## MetaAccess 3.27.0 - January 17, 2023

**1.** **Policy**

- Added a new compliance check for Communication Tools.

**2.** **Device Authentication**

- Added support for registering endpoint based on user identity

  - **Note:** apply for .exe file only

**3.** **OAuth APIs**

- Added support to get field *in_grace_period* on devices v3.5 and device detail v3.7

**4. Webhooks**

- Added support for new *in_grace_period* events

**5. Fixed several bugs**

## MetaAccess 3.26.0 - December 20, 2022

**1.** **Dashboard**

- Add support for new NERC CIP dashboard

  - **Note:** this feature is in Controlled Release, contact OPSWAT Support if you would like to experience this feature.

**2.** **Vulnerabilities**

- Added support for Known Exploited Vulnerabilities as reported by CISA

**3.** **New look for remediation pages**

- As can be seen in the Rebranding options, a new version of the remediation pages are available. This includes both a light theme and dark theme. Existing customers will need to manually change to the new look if they have made any rebranding customizations.

  - **Note:** June 1, of 2023, all customers will be moved to the new look.

**4.** **Application Updates**

- Added support to automatically update applications on an endpoint. This relies on the OPSWAT Client's ability to update software.
- Added support to limit apps in the Client's UI. Includes the ability for administrators to prevent end-user from updating specific applications, either manually or via auto-updates.

**5. Policy**

- Added a new compliance check for Peer-to-Peer (P2) applications
- Added a new compliance check for Web Conferencing applications
- Added a new check for minimum supported OS

**6.** **Fixed several bugs**

## MetaAccess 3.25.0 - November 15, 2022

**1.** **Account Summary Report**

- Added new report section as a list of compliance violations
- Added new trending bar chart for how well an account is handling compliance issues.

**2.** **Policy**

- Added support for Data Loss Prevention compliance

**3. Download page**

- Added support for downloading macOS persistent Client as a .zip file instead of a .dmg file to support low-functional browsers
- **Note:** this feature is in a controlled release, contact OPSWAT Support if you would like to experience this feature

**4. Console**

- Enhance the user profile header.

**5.** **Fixed several bugs**

## MetaAccess 3.24.0 - October 18, 2022

**1.** **Policy**

- Added a new option to antiphishing to check if the default browser has antiphishing enabled. Note: Most browsers have broader settings for security that do more than just antiphishing, and it is these new options, named like safe browsing or secure browsing, that are checked in MetaAccess.

**2.** **Automatically delete non-compliant devices**

- Along side the existing option to automatically delete devices that are consistently being seen as non-compliant (in Settings->Global->Device Data), there is now also the ability to delete devices that have been non-compliant for a consecutive number of compliance checks. This setting can be overridden at a Device Group basis under the Lost Device section.

**3. SIEM integration**

- To provide updates on changes to device compliance or security in a more timely fashion, the the interval of forwarding events to AWS S3 has been decreased from 30 minutes to 5 minutes. This relates to the configuration done in Settings->Integrations->SIEM Integration.

**4. Device detail**

- Added support for editing the Custom Information field from the MetaAccess Console, within the Device Details. Note this relates to the feature where a end-user can be prompted to add additional information during the install of the OPSWAT Client. If the user misentered the information, before this enhancement, there was no way for the administrator to correct this field's content.

**5. Application Control**

- Added support for two new categories of applications to the Application Control section of the policy editor: Data Loss Prevention and Browser

**6.Fixed several bugs**

## MetaAccess 3.23.0 - September 20, 2022

**1.** **Customizable disclaimer**

- Added support for customized disclaimer on the Windows OPSWAT Client during install. Especially useful to warn BYOD users of the data being collected.

**2.** **Playbook**

- Added a new Device Task to support multiple custom check scripts in the Playbooks.

**3.** **Advance Endpoint Protection**

- Added support for anti-copy-pasting across applications. This can prevent users from copying and pasting content from one application to another. Users can still copy-paste within the same application.

**4. Operating System Policy**

- Added support for a minimum operating system requirement check for Linux

- More granular control of the OS version through the support of the UBR (Update Build Revision number)

**5. Webhook**

- Added additional info to the details sent in the Webhook events

**6. Notification**

- Added support for Gateway Update events

**7.Fixed several bugs**

## MetaAccess 3.22.0 - August 16, 2022

**1. Policy Management**

- Added support for fallback checks using playbooks. This can be used to condition a playbook based on a built-in check. For example, if the built-in check for antimalware triggers an issue, the playbook could conditionally move the device to another device group configured to check with a different antimalware solution.

**2. Gateway**

- Added support for multi-site SDP deployments by permitting users to pick the Gateway Pool they will connect to. This can also help with availability by permitting a user to pick an alternate site manually if the primary site is unavailable.

**3. Device**

- Added support for device discovery of the network. The discovery is done from a desktop device running the OPSWAT Client that the administrator selects. When this feature is enabled, the MetaAccess Console also shows Discovered Devices within the Inventory.

**4. Lost Device**

- Added support for automatically deleting non-compliant devices that are found non-compliant for some configurable number of days. This can help both with licensing and noise, as often the non-compliant devices that repeatedly fail compliance are no longer being used to access resources MetaAccess protects. When the user does again use that deleted device, they will be again prompted to become compliant.

**5. Webhook Integration**

- Added support for spaces (blanks) in the API key

**6.Fixed several bugs**

## MetaAccess 3.21.0 - July 19, 2022

**1. Policy Management**

- Support Playbooks for Linux

  - **Note:** this feature is in Controlled Release, contact OPSWAT Support if you would like to experience this feature
  - This feature enables administrators to visually design custom compliance checks, or as we are referring to them "Playbooks"

**2. Integration**

- Support SIEM integration with AWS S3

**3. OAuth API**

- Support "Get Devices" API version 3.4

**4. Fixed several bugs**

## MetaAccess 3.20.0 - June 21, 2022

**1. Policy Management**

- Compliance Playbooks

  - **Note:** this feature is in Controlled Release, contact OPSWAT Support if you would like to experience this feature
  - This feature enables administrators to visually design custom compliance checks, or as we are referring to them "Playbooks"

** **

**2. Secure Access**

- Support IdP MFA

**3. Fixed several bugs**

## MetaAccess 3.19.0 - May 17, 2022

**1. Report**

- Support report customization

** **

**2. Device**

- Support the On-Demand OPSWAT Client's /reassessment switch which forces the device to be reassessed when the On-Demand OPSWAT Client is starting.

  - For information on the /reassessment switch, see <https://docs.opswat.com/macloud-sdp/configuration---management/on-demand-client-cli>

**3. PIN**

- Support enable/disable PIN security

**4. Fixed several bugs**

## MetaAccess 3.18.0 - April 19, 2022

**1. Policy**

- Allow excluding specific patches that are missing

- Add more granularity to the unwanted applications

**2. Dashboard**

- Support Device Group filtering

## MetaAccess 3.17.0 - March 15, 2022

**1. Admin Events**

- Support writing logs whenever a console user changes their passwords

**2. User Role**

- Support write permission for Dashboard

**3. Fixed several bugs**

## MetaAccess 3.16.0 - February 15, 2022

**1. Policy**

- Allow import and export of policies

**2. Dashboard**

- Support dashboard customization

**3. Inventory**

- Support adding devices to a group from an upload list

**4. Fixed several bugs**

## MetaAccess 3.15.0 - January 18, 2022

**1. Report**

- Enhance account email summary report.

**2. Dashboard**

- Enhance multiple dashboards.

**3. Webhooks**

- Support account events and gateway events notification.

**4. Compliance**

- Optionally check compliance when user logs in (rather than when OS boots).

**5. Integrations**

- Allow cross-origin requests from specific domains.

**6. Fixed several bugs**

## MetaAccess 3.14.0 - December 21, 2021

**1. Agent Setting**

- Auto-upgrade to a specific OPSWAT Client or SDK version.

**2. Device Groups**

- Auto-assign devices to groups based on the device's domain.

**3. Policy**

- Visually classify anti-malware as Platinum or Gold certified.

**4. Webhooks**

- Enhanced webhooks notification.

**5. Bug fixed**

- Fixed several bugs

## MetaAccess 3.13.0 - November 16, 2021

**1. Rebranding**

- Added customization for the remediation page to configure which client end-users are prompted to download.

  - Show or Hide download button
  - Download Persistent or On-Demand Client
  - Auto assign device to a specific Device Group

**2. Event Logs**

- An event is triggered when a user updates their PIN or logs out of MetaAccess.

***3. Policy***

- Allow administrators to add version numbers to their list of approved patch management applications.

- Add support for blocking certain apps.

**4. Improvement**

- Optimize the communication between Client & backend services.

**5. Devices**

- Added support to filter device inventory by Persistent or On-Demand agents.

**6. Bug fixed**

- Fixed several bugs

## MetaAccess 3.12.0 - October 19, 2021

**1. Rebranding**

- Convert the remediation style from legacy view to modern view.

**2. Event Logs**

- Write an event to the log when a client upgrades to a newer version.

**3. User Management**

- Support different levels of access in the console based on the IdP groups.

**4. OAuth APIs**

- More granular, role-based control of permissions.

**5. Policy**

- Support vulnerability and patch management policy rule for Linux.

**6. SDP Private Gateway**

- Add charts to display health statistics.

**7. Bug fixed**

- Can not open OPSWAT Client on iOS - Salesforce Application
- The device is still non-compliant although matched with the default rule (set as compliant)

## MetaAccess 3.11.0 - September 21, 2021

**1. User Roles**

- Allow administrators to define a custom user role and assign the permission that user role can do on the account

**2. Policy**

- Provide a fallback option based on the Window Security Center's assessment of Anti-malware protection

**3. OAuth APIs**

- Add new *serial_number* field to get device details API

**4. Bug fixed**

- Device displayed multiple times in Console

## MetaAccess 3.10.0 - August 24, 2021

**1. Policy**

- Added new policy rule to check if a device has any CVEs in a customer provided list.

**2. Download page**

- Updated the OPSWAT Client Download Page for clarity.

**3. Remediation page**

- Updated several of the remediation instructions shown to an end user when warned or blocked.

**4. Bugs Fixed**

- Device detail API should return a non-compliant device if a MAC address in the query has been used by multiple devices and at least one device is non-compliant

## MetaAccess 3.9.0 - July 27, 2021

**1. Secure Access**

- Admins can enable SDP for all devices using an account's default gateway pool. However, an admin can still override this setting for specific groups, if needed, in a group's settings.

- Admins can now also audit access activities to protected apps when the apps are protected via SDP Gateways.

- Admins can disconnect a session/all sessions of a user from Secure Access > Activities > Gateway Sessions Logs. The user can re-connect to SDP Gateway by re-authenticating with SDP Client again. We recommend the admins disable the user on your IdP (or IAM system) if you would like to prevent the user from reconnecting to the SDP gateways.

- Admins can turn on a daily/weekly/monthly SDP sessions report to be sent to specific emails (Settings > Reports > Email Reports). A report in CSV format is in CSV format.

- Admins can view events related to gateways on an account at Logs > Gateway Events. The admins are also able to configure email notifications for these events.

**2. Email Notifications**

- Admins can create multiple notification groups with different recipients and event triggers

- Admins can assign notification groups to an account notification level or a group level

**3. Policy**

- Removable Media Protection: Admins can enable an option to allow users to copy only allowed files from a local drive to a removable media in a policy (Policy > Settings > Removable Media Protection). When this setting is enabled, the OPSWAT Client will perform a scan while copying files and only files that are marked as allowed are copied.

**4. OAuth API**

- A new version of Device Details API v3.4 that includes Policy Name of a policy that assigned to a device
- A new version of Get Logs API v3.2 that supports Device Report event log type

**5. Remediation page**

- Auto-convert a customized remediation package from Legacy to Modern View to help customers migrate to Modern View easier. When a user switches to Modern View from a Legacy View with a customized rebranding package, the user can download the current rebranding package in the Modern View template. The system will try to keep messages/settings that can exist on both Legacy View and Modern View; other messages/settings that are only available on the Modern View will be set with the default messages/settings. **The legacy view will be deprecated in September 15, 2021.**

**6. Bugs Fixed**

- A device changed status to non-compliant each day if policy rule considers a device as non-compliant based on the agent version condition
- A device was marked as a virtual machine when a device enrolled to the account and has not reported compliance data to the system

## MetaAccess 3.8.1 - June 27, 2021

1. Fixed an issue where users couldn't log into protected apps via IdP workflow on mobile devices.

## MetaAccess 3.8.0 - June 15, 2021

- Introduced a new view of the remediation page.

  - Issues are now classified into 2 sections:

    1. Required - issues that users need to address to be compliant
    2. Recommended - issues that users should address to make their device fully comply with a policy

This helps users focus on required issues to get their device back to compliant state.

- - Simplify messages to help users focus on the actions they should take on each issue

- Admins can switch to the new remediation page at a time they wish. However, **the legacy view of the remediation page will be deprecated in September 15, 2021**. By that time, rebranding packages that are still in Legacy mode will be switched to the modern mode automatically.
- Enhanced the rebranding package with the modern view: messages for each category are now in an individual JSON file.

**2. Policy**

- Enhanced the Operating System policy to allow admins configure approved OSes based on versions and editions for Windows devices

**3. Other enhancements**

- The device details view shows details on why a device is compliant/non-compliant and what policy rule the device met.

**4. Bugs Fixed**

- The system did not send an email notification for the event Admin Logged On if an admin logged on MetaAccess console with a customer's own IdP.

## MetaAccess 3.7.1 - June 01, 2021

**1. Secure Access**

- Enhanced IdP-based secure access flow related to checking the device compliance status before granting a device access to an application.
- Private Gateways are now available for Microsoft Azure deployment

**2. SDP Private Gateways**

- Private Gateway is now available on Microsoft Azure
- Built-in troubleshooting tools to help administrator troubleshoot gateway issues such as the SDP Client could not connect to a private gateway

**3. Bugs Fixed**

- A user couldn't upload the metadata file to configure Single Sign On for admins and SDP users.
- The system did not request the OPSWAT Client to not report patch management and other applications when the application privacy setting is turned on and those are not enabled on a policy.

## MetaAccess 3.7.0 - April 21, 2021

1. **Security Enhancement**

- No longer support TLS 1.0 and TLS 1.1. [Learn more.](https://www.opswat.com/blog/metaaccess-support-for-tls-1-0-and-1-1-ending)

**2. Privacy Data**

- Added a new setting to Settings > Global > Account > Privacy Settings, ***Applications that are not in categories enabled in a policy,*** to restrict OPSWAT Client from collecting applications disabled in a policy

**3.Policy**

Admins can configure a device status based on

- a device type such as virtual machine
- a client version of each agent type
- a device severity with a time period

**4. OAuth API**

- Add a new API, Get Logs v3.1, to allow users fetch event logs from an account.

**5. Secure Access**

- With IdP Method, MetaAccess re-signs a SAML request before sending it to IdP if a Service Provider signed the SAML request for SP-Initiated SSO workflow.

**6. Other enhancements**

- Show the last user who logged into a device when there is no active user on the device.
- Record an event log when an admin makes any changes on OAuth applications on OAuth portal.

**7. Bugs Fixed**

- The console showed an session extension popup even when a user was inactive on a page for a long time sometimes
- An access token for an OAuth app was not reset even when a user reset a client key and client secret for that app.

## MetaAccess 3.6.1 - April 8, 2021

**Bugs fixed:**

- Fixed an issue that multiple devices may share the same device ID in some cases

## MetaAccess 3.6.0 - March 16, 2021

**1. Policies:**

- Added a new scan option, Boot Sectors, to Device Scan in a policy.

**2. Secure Access**:

- Added a new setting, *Visible to Users*, for a SDP protected app to make the app visible or invisible to end-users
- Allow admins to assign users/group when the admin edits an app
- Enhance user experience when a user adds/edits a protected app

**3. Endpoint Vulnerability**

- Admins can allowlist CVEs for specific devices

- Admins can view CVEs associated to a Linux device

**4. Settings:**

- Add a new setting *" Allow agents to automatically update the agent SDK to the latest version"* at an Account level (Settings > Global >Device Agents > Agent) and a Group level (a group > Settings > Agent) to allow admins to control SDK upgrade on devices

**5. OAuth API**

- Enhance user experience for OAuth Portal

**6. Other enhancements:**

- Added details on what missing patches a user should patch on their device to be complied with a policy

- Policy Check API will return a device status as *Non-compliant* if it finds at least one Non-compliant device that associates with a queried MAC address
- The system will record a log event when an admin fails to log in through OPSWAT SSO based on customers' request.
- Allow admins to perform an on-demand compliance check on devices that run the OPSWAT On-demand Client.
- Datetime on event logs is shown up to seconds

**7. Bugs fixed:**

- The email notification when a device report malwares was not in a correct format
- The system didn't update last login time for an admin user correctly when the admin switches to a managed account
- The system didn't send out an email notification when an admin updates a group's settings.

## MetaAccess 3.5.0 - February 02, 2021

1. **Group Settings:**

- Lost Devices and Compliance Report:

  - Now admins can override these Global Device Agent settings in specific groups. When enabled and overridden by a Group, only the devices in the Group will use the overrides.
  - Disabled by default in the Groups

2. **Policies:**

- Now admins can configure in a Policy which approved Patch management products are required.

3. **Custom check enhancements**:

- Allow admins to configure the custom check as Failed/Passed if the OPSWAT Client failed to run a script or the script returns timout/errors/invalid format
- Enhanced an event log message to include the filename of the custom script when an admin updates the filename in the Policy

4. **OAuth APIs**

- Added a new API, Get CVEs, to allow users to retrieve CVEs that are associated to a device

5. **Minor enhancements:**

- Trend of Risky Devices under the Compliance dashboard now shows history of devices that have issues by categories

- Enhanced user experience on the Account Summary report
- Admins can now configure how long they want to exempt devices
- The Devices Export file now contains separate columns for the CVE categorizes that are associated to a devices
- The MetaAccess Entity ID is now exposed for SDP SSO configuration (navigate to: User Management > SSO > SDP)
- Allow admins to configure IdP Start URL to protected app settings via IdP SAML method (a new setting for an IdP protected application)

6. **Bugs fixed:**

- The email notification when a device report malwares was not in a correct format
- An admin could not update/add a protected app if (s)he configures iOS and Android package schema.
- No email was sent to a user who submitted a support ticket from MetaAccess console

## MetaAccess 3.3.0 - December 22, 2020

1. Support **Anti-keylogger** in policies: MetaAccess prevents keyloggers and advanced malware from  accessing  sensitive data by intercepting and encrypting keystrokes. This module requires an additional license.

2. Support **Screen capture protection** in policies: MetaAccess prevents malicious and accidental screenshots. It prevents unauthorized or accidental screenshots and recording by users, VDI, web collaboration tools, and malicious applications. It protects against data loss issues from web collaboration tools such as Zoom, Microsoft Teams, Cisco WebEx, and others. This module requires an additional license.

3. **Gateway Pools:**

- Allow admins group gateways into a pool to support a global deployment. Each gateway pool can be assigned to one or multiple groups.
- Allow admins can leverage both OPSWAT Hosted Gateway, if licensed, and private gateway.

4. **Introduce Group Settings:**

- SDP settings

  - allow admins enable SDP features on devices belong to a group
  - allow admins to assign a gateway pool to a group. Devices in the group will be routed to gateways of the gateway pool assigned to the group.
- Agent settings:

  - allow admins overwrite agent settings in Global settings in specific groups. If a group doesn't enable this section, devices belong to the group will receive agent settings from Global Settings.
  - Disable by default.

5. **Security enhancement:** change the algorithm used to store/exchange sensitive data that secures your account. This can cause devices that running an old version of OPSWAT Client couldn't uninstall the client by end-users. Admins need to delete devices from the management console in that case.
6. Custom check enhancements:

- Support custom check for Linux devices.
- support multiple scripts for Windows and macOS devices. Administrators can implement multiple scripts and combine them in a main script, then upload the script package to a policy.

7. Support retain the last group a device was assigned to when a device re-enrolls to an account.

8. Secure Access enhancement:

- Secure Access via SDP: Support users log into SDP via SSO from the SDP UI (SP Initiate)
- Secure Access via IdP: support SHA-2 Signing

9. Client User Interface: Administrator can now enable client UI on the persistent OPSWAT Client for Windows. This setting is available at Global Settings and Group Settings. It's disable by default.

- the new OPSWAT Client UI and SDP UI run parallel
- SDP UI is always enabled when SDP feature is enabled on a device even the Client UI setting is disable.

10. Minor enhancements:

- Add a new field, **show_issues_with_severity**, to the content.json file in a rebranding package to indicate what issues should be shown on the remediation page.
- Add NPS survey

11. Bugs fixed:

- The system was not applied specific apps conditions in access rules for SDP apps.
- The system didn't allow users to select approved anti-malware products for macOS devices by a major version.
- The system didn't assess device compliance status if a device reports no network adapters.
- A user couldn't add a protected app if an URL contains two hyphen characters (--)
- Admin event logs didn't show admin's email sometimes.

## MetaAccess 3.2.0 - October 29, 2020

1. User authentication for MetaAccess management console is switched to a new OPSWAT Single Sign-on (SSO) system (<https://id.opswat.com>) . A user has to reset his/her password on the new OPSWAT SSO system. This only impacts users who log into MetaAccess console through OPSWAT SSO, if you are logging into MetaAccess console through your own SSO, it will not be impacted.
2. Enhanced account summary report which is sent daily/weekly/monthly based on email report settings (Settings > Reports > Email Reports).
3. An admin can view access status of a device for all protected applications
4. Bugs fixed:

- In some cases, a csv file didn't have devices' information when a user export devices
- A user couldn't view threats detected by a local anti-malware product
- The remediation page is slow in some regions
- A user was switched back to his/her own account when his/her session reached timeout
- A user couldn't download the OPSWAT On-demand Client for macOS devices sometimes

## MetaAccess 3.1.1 - October 13, 2020

1. Bugs fixed:

- Admins could not log into MetaAccess console through Okta
- The system stopped Webhook setting even the callback API has not responded any error
- A user couldn't add a protected app with the application type as Other
- The system did not update MAC address of network adapters when local IP address is enabled on Privacy Settings

## MetaAccess 3.1.0 - September 29, 2020

1. The MetaAccess console will be hosted in different domains. The system will auto-redirect you to the new domain when you access the old domain.

| Tenant | Old Domain |  | New Domain |  |
| --- | --- | --- | --- | --- |
|  | Console | API | Console | API |
| US Tenant A | metaaccess-a.opswat.com | metaaccess-a.opswat.com | console.metaaccess-a.opswat.com | metaaccess-a.opswat.com |
| US Tenant B | gears.opswat.com | gears.opswat.com dapi.opswat.com | console.metaaccess-b.opswat.com | gears.opswat.com dapi.opswat.com |
| EU Tenant | gears-eu.opswat.com | gears-eu.opswat.com | console.metaaccess-eu.opswat.com | gears-eu.opswat.com |

2. The console is refreshed with a new look and and user experience.

- The system will walk you through steps to protect your applications
- Policy management is re-organized to improve navigation and usability
- The left navigation is re-organized

  - "*Device Groups*" is moved into "*Inventory"*
  - "*Access Control*" is renamed to "*Secure Access"* and offers more access control options to protect your applications and networks.
  - "*Single sign-on*" settings for admin log into the console is moved into "*User Management"*
  - *"Event Log"* is broken down to *"Admin Events", "Device Events", and "Webhook Events"*

3. Software Defined Perimeter (SDP) is now offered on MetaAccess platform to protect your applications and networks. The SDP approach to zero trust networking flips the traditional approach of securing access to network resources on its head. Instead of connecting then authorizing, the client is required to first authenticate, authorize, be checked for compliance, and only then is it allowed access. Check out [our document](https://onlinehelp.opswat.com/metaaccess/3.2._Software_Defined_Perimeter_%28SDP%29_Method.html) for more details. SDP requires and additional license.

- Administrators can now protect applications and networks in their critical infrastructure via [SDP](https://onlinehelp.opswat.com/metaaccess/3.2._Software_Defined_Perimeter_%28SDP%29_Method.html) no matter where a user connects from. The users' devices will be checked to make sure they are complied with your organization's security policies.
- Administrators can configure access rules to grant/deny access to applications
- Administrators can grant users/groups access to applications.
- Administrators can control device groups that users can use to access to protected applications and networks
- Administrators can integrate with 3rd party single sign-on service for end-users authentication and import groups from IdP to MetaAccess.
- Administrators can audit user sessions.
- Administrators can also select either Private Gateway or OPSWAT Hosted Gateway to be their applications' gateway

  - Private Gateway: admins need to install SDP gateways in their datacenter or their own cloud infrastructure
  - OPSWAT Hosted Gateway: no need to install any thing, but it requires an additional license.

4. User experience enhancements

- Users can filter vulnerabilities based on a allowlist status
- Users can search packages on a Linux device
- Users can select how many items shown in one page

5. Bug fixes:

- Read-only users couldn't export device inventory
- The system couldn't load devices when a user navigated to the last pages in some cases.
- The Get Devices API returned error when the page parameter is set to last pages in some cases.

## MetaAccess 2.8.2 - August 18, 2020

1. Administrators can now indicate what privilege OPSWAT Client should run a custom script with. By default, OPSWAT Client runs custom script as system on Windows or user on macOS.
2. Allow admins to export selected devices only instead of all devices which match to search/filter criteria.
3. Bug fixes:

- Device export file for macOS devices didn't have correct data for some fields
- The system false alerted to users who log into MetaAccess through 3rd-party single sign-on service that their account runs out of license.
- The remediation page showed all vulnerable applications instead of only vulnerable applications which violates a policy's criteria.

## MetaAccess 2.8.1 - July 07, 2020

1. Administrators now can audit files a user copied from local drives to a removable media by enabling the *Report a copy result when a user copies files from local drives to a removable media* setting under Removable Media Protection.
2. MetaAccess customers can now leverage more commercial engines for Advanced Threat Detection with MetaDefender Cloud. New engines are available for both existing and new policies. They are un-selected by default for existing policies, administrators have to update policies manually.
3. Enhanced the access control workflow to support device compliance check when a user logs into G-suite via Azure single-sign on.
4. Bug fixes:

- Missing authentication header in the callback.

## MetaAccess 2.8.0 - June 02, 2020

1. Updated Threat Detection with MetaDefender Cloud based-on [MetaAccess Tiers](https://www.opswat.com/products/metaaccess#option_table). If an account is a Free account, MetaDefender Cloud is not available for multi-scanning feature, and a policy, that configured a scan source for Threat Detection as MetaDefender Cloud, will be considered as an invalid policy. However, you can use your own MetaDefender Core servers for this feature.

- You need to fix invalid policies before making any changes to the policies. Otherwise, you couldn't save your changes. Check out [our KB](https://onlinehelp.opswat.com/metaaccess/How_can_I_fix_invalid_policies_on_my_account_.html) to know how to to fix invalid policies.
- OPSWAT Client will NOT scan a device as its policy and the system will not process any threat reports from the device if the policy is invalid.
- You will get an error when you send an on-demand threat scan from the console to devices which assigned to an invalid policy
- Administrators will see an error banner notification that indicates what policies are invalid.
- The Policies page also marks invalid policies with a red dot

2. Added more options to a rebranding package to allow administrators to customize the below information on remediation pages. Detailed guidelines can be found [here](/kb/how-can-i-customize-remediation-pages-for-a-group-)

- *customcheck_output_message:* when this element is set, an output message from a custom script will be exposed to end-users on the remediation page when a device failed the script. Otherwise ("customcheck_output_message":""), the output message will not be shown to the end-users.
- *device_info:* administrators can show any device information by setting a value for an element in the device_info object or leaving it blank to hide it_._
- *font_name:* customize a font for text on the remediation page.

3. Minor enhancements

- added "Device Group" into email notifications for device events

4. Bug fixes:

- A device didn't fetch a new custom script if it is assigned to a new device group
- Device Inventory report format was broken if a device's system information has special characters
- Vulnerabilities assessment was wrong for Cisco Jabber product on macOS.

## MetaAccess 2.7.1 - April 28, 2020

1. Administrators can now export a policy to a json file.
2. Administrators can enable/disable showing a notification when a user installs a new applications on Android phone at ***Settings > Global Settings > Device Agents > Notifications to users***. By default, this setting is enabled. This is only applicable for Android agent version 2.55.33 or newer.
3. Minor changes

- Add one more event to trigger a webhook call: Device changes status to Exempted. This event trigger is disabled by default.
- Support administrators perform an on-demand compliance check for Linux devices. This action is only applicable for Linux agent version 15.4.11.0/15.6.9.0 or newer.

4. Bug fixes:

- Device name was not updated accordingly when a device reports a new hostname even no admins manually update the device name.
- A free account couldn't enable cross-domain API setting.

## MetaAccess 2.7.0 - March 25, 2020 - Hotfix

Changes in this hotfix:

- Device Policy Check v2.2 API : updated to POST method instead of GET method. This fixes an VMWare UAG integration issue.

## MetaAccess 2.7.0 - March 24, 2020

1. Administrators can enable webhook on MetaAccess to report device status when an event is triggered to a defined callback URL. MetaAccess supports the events below:

- Device added
- Device deleted
- Device changed status to compliant
- Device changed status to non-compliant
- Device changed status to out of license usage

This feature is disabled by default for all accounts (existing and new accounts).

Notes:

- This webhook will be disabled if MetaAccess fails to send reports to the defined callback URL in 100 times. Administrators need to log into MetaAccess console to re-enable it
- This feature is only available for enterprise customers

2. Device reports now includes CVE-IDs associated with each device.
3. Minor changes

- Showing the last report time as a datetime instead of a duration on the remediation page

4. Bug fixes:

- If a user's email has an uppercase character, the user was unable to log into MetaAccess through their own IdP and received an invalid email address error

**MetaAccess 2.6.0: February 11, 2020**

1. Enhanced User Profile page to show usage of accounts (s)he is managing.
2. Added a new setting to notify end-users who is running outdated on-demand agent. This setting is disabled by default.
3. Administrators can now set a trigger to send an email notification to configured emails when an account runs out of license. This trigger is disabled by default.
4. Minor enhancements:

- Added a column, Group, into a Device Event Logs report to indicate what group a device was associated to at that timestamp
- Added more missing patch categories: definition_update, feature_pack

5. Bugs fixed:

- Device ID is now fully shown on the remediation page instead of being shortened if its length is long
- Device Details v3.1, v3.2, v3.3 now returns timestamp for the parameter **infection.metascan .last_scan** in GMT format as the API documents instead of UNIX format
- Applications inventory couldn't be loaded sometimes

**MetaAccess 2.5.0: January 07, 2020**

1. MetaAccess enhanced policy configuration to allow administrators to configure more granular policies for each operating system and focus on security requirements at an organization. With this enhancement, admin can hide categories that they don't want to monitor.
2. Minor changes:

- added "Enrolled At" information into a device report when an administrator exports devices from the MetaAccess console

**MetaAccess 2.4.2: November 26, 2019**

1. Administrators can monitor only OS updates in specific categories. All policies will be set with "any missing patches" as a default option when this release is rolled out.
2. Administrators can configure OPSWAT Client to delay the collection of compliance data after it starts. This way, it gives other applications time to start before the OPSWAT Client reports compliance data to reduce false-positive detection.
3. Enhancement:

- Device reports will be put in a queue to be processed against a policy. The OPSWAT Client will receive a compliance result in the next check-in, up to a minute.

4. Bugs fixed:

- MetaAccess will not send an unknown devices report if there is no unknown device found
- A device was able to enroll in an account even the account limit is reached. The system will change status of a device to Out-of-license-usage if a device was enrolled after the limit reach.

**MetaAccess 2.4.2: October 22, 2019**

1. Administrators can now perform an on-demand compliance check on devices from the management console
2. Added new APIs:

- [Account Config](/developer-guide/account-config) enable administrators to retrieve a registration code for mobile devices
- [Get Remediation Link](/developer-guide/get-remediation-link) v3.0 to return "remediation_link" when a device has no issue

3. Administrators can now monitor the progress of an on-demand threat scan from the management console
4. Bugs fixed

- Device Details API didn't return data for some categories such as Unclassified applications, detected patches, mobile apps
- The last reboot time of a mobile device was not shown correctly
- Installed applications on Linux devices were not listed on the Applications inventor

5. Minor enhancement

- Remove OPSWAT Client SDK on "Add Devices" popup

**MetaAccess 2.4.1: September 17, 2019**

1. Administrators can now configure different encryption state requirements for additional local volumes and additional removable volumes. These settings will be set based on the "Additional volumes are not encrypted by an approved application" setting in a policy before the release

| Before Release | After Release |  |
| --- | --- | --- |
| Additional volumes are not encrypted by an approved application | Additional local volumes are not encrypted by an approved application | Additional removable volumes are not encrypted by an approved application |
| Enable | Enable | Enable |
| Disable | Disable | Disable |

2. The date time on the console UI now reflects the local timezone
3. Bugs fixed

- Device Policy Check API returned a device was not found if the MAC Address is in uppercase. The API now accepts MAC address in either lowercase or uppercase.

**MetaAccess 2.4.0: August 06, 2019**

1. Allowlist Vulnerabilities: Administrators can now allowlist vulnerabilities for policies or entire accounts after reviewing risks and assess impact of vulnerabilities. By allow-listing vulnerabilities, vulnerabilities associates to a device will not be counted for issues if they are allowlisted on a policy the device is assigned to.
2. Enhanced vulnerabilities view: provides administrators a better view on what applications,OS patches and CVEs are associated, and what policies it is allowlisted on
3. The system will not send a threat summary report if the system doesn't detect any threat in the last report duration.
4. Added new OAuth APIs:

- [Device Action](/developer-guide/device-action) supports a new action , scan_threats, to allow administrators to send an on-demand threat scan to devices
- [Get Reports](/developer-guide/get-reports) supports administrators to retrieve a result for on-demand threat scan action.

5. Bug fixed: the system didn't send a request to the agent to open a remediation page if the device reports issues in N consecutive reports and N is greater than the non-compliant threshold.
6. Minor enhancement:

- Added an agent type information under System Information on Device Details view
- The system will keep MAC address information of devices which registered or reported duplicated MAC address. By this way, administrators can search for devices which reports the same MAC address
- Added a new default rebranding package with Japanese language

**MetaAccess 2.3.1: June 25, 2019**

1. "Managed By" information on remediation pages will be shown with Account Name instead of an email address of the account.
2. Enhanced performance to process requests.

**MetaAccess 2.3.0: June 04, 2019**

1. Enhanced threat detection to allow administrators to configure how a file is considered a threat. Criteria can be based on the number of engines and trusted engines when a device scans threats against MetaDefender Cloud. Admins can configure a policy to leverage MetaDefender Core for Threat Detection, when used this way, MetaAccess respects scan results from MetaDefender Core: only files with a BLOCKED status will be considered as threat.

| Scan Source | Before The Release | After The Release |
| --- | --- | --- |
| MetaDefender Cloud | Threat Scan   - Filter threats based on trusted engines. A file is detected as threat if at least one trusted engine detects it as a threat   Device Issue   - Considered an issue if a file is detected as threat by N engines if enabled - Considered a critical issue if a file is detected as threat by M engines if enabled | Threat Scan   - Filter threats based on number of trust engines. A file is detected as threat if at least N trust engines detect it as threat   Device Issue   - Considered an issue if a device reports any threats if enabled - Considered a critical issue if a threat detected by M engines if enabled |
| MetaDefender API (Core) | Threat Scan   - Filter threats based on trusted engines. A file is detected as threat if at least one trust engine detects it as threat   Device Issue   - Considered an issue if a file is detected as threat by N engines if enabled - Considered a critical issue if a file is detected as threat by M engines if enabled | Threat Scan   - A file is detected as threat if MetaDefender API (Core) scan result is BLOCKED   Device Issue   - Considered an issue if a device reports any threats if enabled - Considered an issue if a device reports any threats if enabled |

2. Administrators can now enable OPSWAT Client to auto-block mobile PTP/MTP devices when a user inserts a mobile PTP/MTP devices to an endpoint. This option is disabled by default. If you wish to enable it, please log into MetaAccess console and update policies.
3. If OPSWAT Client reports free hard disk space as not supported, MetaAccess does not consider this as an issue. This affects macOS 10.13+ devices

**MetaAccess 2.2.1: May 24, 2019**

- Fixed issues

  - couldn't download agents from the download pages
  - couldn't fetch agent log

**MetaAccess 2.2.0: May 14, 2019**

1. Administrators can now configure agents to upload allowed/blocked files to a MetaDefender Vault when a user unblocks or copies files from portable media drives. This setting is disabled by default.
2. Administrators now have an option to exclude CD/DVD from auto-blocking portable media drives. This setting is disabled by default.
3. Administrators can see a timestamp when a device is enrolled to an account
4. MetaAccess adds a Live Chat snippet on the console to help users reach out to our support for help in less time
5. Add new APIs, Get Devices v3.3 and Device Details v3.3, to return a timestamp, enrolled_at, when a device is enrolled to an account,
6. Minor changes:

- Increased Nickname length limit to 100 characters
- Re-organized the left navigation menu: moved the "Group" menu out of the "Inventory" menu

**MetaAccess 2.1.1: April 17, 2019**

1. Fixed: when a user downloads an installer from a download link that contains a tag name/group id, the Cloud does not generate the installer with the tag name/group id
2. Fixed: the link to go to the OPSWAT support portal on Help Center

**MetaAccess 2.1.0: April 02, 2019**

1. MetaAccess now enables administrators to detect advanced threats within file systems in addition to active running processes powered by MetaDefender technologies. Administrators can schedule scans with multiple options such as a Full System Scan or a Custom Scan (memory, system volume, additional volumes, a specific path).
2. Administrators can also perform an on-demand scan on selected devices and obtain a threat report remotely.
3. Added oAuth API [Device Information](/developer-guide/device-information) return pre-processing data for a device.

**MetaAccess 1.3.3.0: February 26, 2019**

1. Enhanced dashboard to provide a consolidated view of your security and device landscape across your organization . Beside an overview dashboard, administrators now can access detailed security view for Secure Access, Vulnerabilities, Compliance, and Threat Detection.
2. Administrators can do localization and globalization for each device group by customizing the remediation page for groups. Administrators can add a customized package for remediation pages at Settings > Rebranding and assign it in Group details

**MetaAccess 1.3.2.0: January 22, 2019**

1. MetaAccess now returns parameters in the response header to indicate API rate limits (X-RateLimit-Limit), how many calls left (X-RateLimit-Remaining), when the rate limit is reset (X-RateLimit-Reset-Time)
2. Added new OAuth APIs:

- Account Details v3.1: return details about device status, device with vulnerabilities by severity, devices with issues by severity
- Device Action v3.1: support more actions to allow administrators retrieve OPSWAT Client log on devices
- Get Reports v3.0: support download OPSWAT Client log if available

3. Bugs fixed

- A co-administrator could not invite another user to manage the co-admin account
