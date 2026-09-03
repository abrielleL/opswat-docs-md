<!-- source: https://www.opswat.com/docs/ocm/release-notes/changelog -->

# Changelog

## [Version 7.38.0](/docs/ocm/release-notes/changelog#version-7380)

Release Date: May 9, 2025

Security Updates:

- Upgraded 3rd party libraries and updated server configuration to remediate related vulnerabilities

Enhancements:

- Proxy server setting supported IPv6-addresses.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Endpoint 7.6.2504.704 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Endpoint 7.3.2504.379 |  |
| macOS Persistent Endpoint 10.4.2504.182 |  |
| macOS On-demand Endpoint 10.5.2504.153 |  |

## [Version 7.37.0](/docs/ocm/release-notes/changelog#version-7370)

Release Date: April 3, 2025

Security Updates:

- Addressed potential security issues

Bugs Fixed:

- The remediation page for MetaDefender Endpoint contained outdated URLs to OPSWAT Central Management documentation.
- In User Management, when adding a new user directory, the management console was stuck and displayed an ambiguous error message "servers[0].host: Invalid address" after entering an invalid address for the Server Host field.

Other Changes:

- (Windows only) Updated Software Requirement

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Endpoint 7.6.2503.676 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Endpoint 7.3.2503.370 |  |
| macOS Persistent Endpoint 10.4.2503.178 |  |
| macOS On-demand Endpoint 10.5.2503.149 |  |

## [Version 7.36.0](/docs/ocm/release-notes/changelog#version-7360)

Release Date: November 14, 2024

Enhancements:

- MetaDefender Endpoint's patches for 3rd-party softwares
- Setting to configure how long the system should keep an old version of modules

Security Updates:

- Addressed potential security issues

Bugs Fixed:

- Processing History did not show scan events with certain scan result types such as "Blocked Verdict by DeepCDR".
- (Windows only) Memory leak in the OCMService.exe process.
- The system could not clean up old versions of modules.
- MetaDefender Endpoint instances could not communicate with the OPSWAT Central Management server due to an "invalid agent token" error.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Endpoint 7.6.2410.580 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Endpoint 7.3.2410.315 |  |
| macOS Persistent Endpoint 10.4.2410.149 |  |
| macOS On-demand Endpoint 10.5.2410.117 |  |

## [Version 7.35.0](/docs/ocm/release-notes/changelog#version-7350)

Release Date: August 21, 2024

Enhancements:

- Support single sign-out for single sign-on
- Interval to check system status

Bugs Fixed

- Could not update module packages if the file size is more than 3MB.
- OPSWAT Central Management cleaned up MetaDefender Core modules if no product instances download them for a long time.
- License expiration date was showed incorrect.

Other Changes:

- Updated Secure Connection settings

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Endpoint 7.6.2407.505 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Endpoint 7.3.2407.276 |  |
| macOS Persistent Endpoint 10.4.2407.143 |  |
| macOS On-demand Endpoint 10.5.2407.111 |  |

## [Version 7.34.0](/docs/ocm/release-notes/changelog#version-7340)

Release Date: April 26, 2024

Enhancements:

- Enhanced MetaDefender Kiosk Linux activation
- Improved user interface for license management page
- Auto-updated management status for MetaDefender Storage Security instances.

Security Enhancements:

- Addressed minor potential security issues

Bugs Fixed:

- The license was automatically deactivated due to a deployment ID change even though the machine running OPSWAT Central Management had not been modified.
- The demo video in the management console could not be played on recent versions of Google Chrome.
- Failed to retrieve processing history from Core instances if the previous job was hang.
- Moving Active Directory users between groups with different permission levels did not update the moved user's permission correctly until a server restart.
- The product instance list did not display properly when navigating to pages toward the end if there are more than 800 instances of a product type.

Other Changes:

- Updated MetaDefender Kiosk to MetaDefender Kiosk Windows
- Updated branding for MetaDefender for Secure Storage

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Endpoint 7.6.2404.465 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Endpoint 7.3.2403.246 |  |
| macOS Persistent Endpoint 10.4.2403.123 |  |
| macOS On-demand Endpoint 10.5.2403.94 |  |

## [Version 7.33.0](/docs/ocm/release-notes/changelog#version-7330)

Release Date: March 25, 2024

Enhancements:

- Security enhancements

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2403.434 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Endpoint 7.3.2403.246 |  |
| macOS Persistent Endpoint 10.4.2403.123 |  |
| macOS On-demand Endpoint 10.5.2403.94 |  |

## [Version 7.32.0](/docs/ocm/release-notes/changelog#version-7320)

Release Date: February 29, 2024

Enhancements:

- Security dashboard for MetaDefender Kiosk Dashboard
- SMTP's SSL certificate verification setting
- Terms of Service and Privacy Policy consent Bugs Fixed:
- An SSO user with the same email as the default administrator user had the default administrator privilege.
- MetaDefender for Secure Storage and MetaDefender Managed File Transfer instances' license was marked as "Expired" or "NA" even though it is still within the expiration date.

Other Changes:

- Updated branding package for MetaDefender Endpoint

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2401.411 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.2401.234 |  |
| macOS Persistent Client 10.4.2401.118 |  |
| macOS On-demand Client 10.5.2401.89 |  |

## [Version 7.30.0](/docs/ocm/release-notes/changelog#version-7300)

Release Date: November 15, 2023

Other Changes:

- Updated branding for MetaDefender Vault
- Security Updates

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2310.382 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.2309.209 |  |
| macOS Persistent Client 10.4.2309.92 |  |
| macOS On-demand Client 10.5.2309.67 |  |

## [Version 7.29.0](/docs/ocm/release-notes/changelog#version-7290)

Release Date: Sep 6, 2023

Enhancements:

- Support for UNC path
- Miscellaneous user interface enhancements

Bugs Fixed:

- Device Policies could not be renamed due to the error "Media security: Allowed list contains invalid device ids or invalid regex string" .
- Removed devices still counted toward the license limit.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2308.348 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.2308.199 |  |
| macOS Persistent Client 10.4.2308.89 |  |
| macOS On-demand Client 10.5.2308.63 |  |

## [Version 7.28.0](/docs/ocm/release-notes/changelog#version-7280)

Release Date: May 24, 2023

Enhancements:

- Miscellaneous user interface enhancements.
- Returned additional information to MetaDefender Endpoint.

Bugs Fixed:

- Could not update Local-type User Directories.
- Sent a Kiosk report with all zeros on systems that use comma for a decimal.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2305.273 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.2302.85 |  |
| macOS Persistent Client 10.4.2302.53 |  |
| macOS On-demand Client 10.5.2302.32 |  |

## [Version 7.27.0](/docs/ocm/release-notes/changelog#version-7270)

Release Date: Mar 15, 2023

Enhancements:

- HTTP Strict Transport Security (HSTS) settings.
- A new connection status of MetaDefender Kiosk Linux introduced: Pending.
- AD authentication via user principal name.
- Display lockout time on login page.
- Updated text for a scan result in the Processing History page .

Bugs Fixed:

- Could not update the vulnerability database to a newer version.
- A product group could be renamed to the same name as another existing group.
- The device details page showed blank SDK version for some cases.

Deprecation Announcement:

- End of support announcement for Windows Server 2012 and 2012R2 in 7.27.0.

Other changes:

- Workaround to install OPSWAT Central Management on Ubuntu 20.04 and 22.04.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2302.185 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.2302.85 |  |
| macOS Persistent Client 10.4.2302.53 |  |
| macOS On-demand Client 10.5.2302.32 |  |

## [Version 7.26.0](/docs/ocm/release-notes/changelog#version-7260)

Release Date: Dec 21, 2022

New Features:

- Removeable media allowlist for MetaDefender Endpoint

Enhancements:

- Support for Windows 11 and Windows Server 2022
- Last update information for MetaDefender Kiosk and MetaDefender Kiosk Linux Dashboard
- Miscellaneous user interface enhancements

Bugs Fixed:

- Failure to download a MetaDefender Core engine package did not trigger an alert or change the package's status to failure.
- Exported MetaDefender Kiosk reports contains illegible instance names.
- Managed devices' Action Logs did not correctly display the error message for a failed action.

Deprecation Announcement

- End of support announcement for Windows Server 2012 and 2012R2 in 7.27.0

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.2211.134 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.2211.58 |  |
| macOS Persistent Client 10.4.2211.27 |  |
| macOS On-demand Client 10.5.2211.18 |  |

## [Version 7.25.0](/docs/ocm/release-notes/changelog#version-7250)

Release Date: October 5, 2022

Enhancements:

- Enhanced MetaDefender Kiosk dashboard
- Enhanced MetaDefender Kiosk CSV reports
- Added a scheduled report for MetaDefender Kiosk instances

Bugs Fixed:

- Could not start a self scan from a MetaDefender Kiosk instance's settings
- Only loaded the first page of devices that install an application in the application details page.

Other changes:

- Updated password complexity requirements

Known issues:

- MetaDefender Core instances could not download engine packages from OPSWAT Central Management if the HTTPs setting only enables TLSv1.3

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.575.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.677.0 |  |
| macOS Persistent Client 10.4.385.0 |  |
| macOS On-demand Client 10.5.308.0 |  |

## [Version 7.24.0](/docs/ocm/release-notes/changelog#version-7240)

Release Date: June 29, 2022

Bugs Fixed:

- MetaDefender Kiosk Dashboard showed no data if an account has at least one MetaDefender Kiosk v4.5.5 instance.
- MetaDefender Kiosk Linux Dashboard was not shown correctly on different time zones.

Other changes:

- Removed OAuth API module
- Removed Access Control module

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.575.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.677.0 |  |
| macOS Persistent Client 10.4.385.0 |  |
| macOS On-demand Client 10.5.308.0 |  |

## [Version 7.23.0](/docs/ocm/release-notes/changelog#version-7230)

Release Date: May 4, 2022

New Software Requirement:

- Visual C++ Redistributable Packages for Visual Studio 2013

Enhancements:

- Added health status for the MetaDefender Kiosk Linux's Inventory
- Delete all data related to a MetaDefender Kiosk Linux instance when it's deleted.
- (Windows only) Validated certificates against the Windows Certificate Store.
- Added support for the PKCS#1 format for [Secure Connection](/docs/ocm/configuration/enabling-https) settings
- Improve user experience

Bugs Fixed:

- Could not activate valid license key for OPSWAT Central Management on certain Windows systems with the error "Invalid Activation File"

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.552.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.672.0 |  |
| macOS Persistent Client 10.4.376.0 |  |
| macOS On-demand Client 10.5.201.0 |  |

## [Version 7.22.1](/docs/ocm/release-notes/changelog#version-7221)

Release Date: April 5, 2022

Enhancements:

- Enhanced Active Directory integration Security Enhancements:
- Mitigated Spring4Shell vulnerability

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.541.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.669.0 |  |
| macOS Persistent Client 10.4.369.0 |  |
| macOS On-demand Client 10.5.297.0 |  |

## [Version 7.22.0](/docs/ocm/release-notes/changelog#version-7220)

Release Date: March 16, 2022

Enhancements:

- Java Runtime Environment (JRE) 11 is bundled in the OPSWAT Central Management installer.
- Administrators can customize a message on the management console's login page.
- Administrators can disable fetching history processing data from Core instances.
- Additional information is added to MetaDefender Kiosk Linux scan reports.
- Connection status of a MetaDefender Drive instance is set as DISCONNECTED when it has not talked to OCM for more than 24 hours.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Client 7.6.541.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Client 7.3.669.0 |  |
| macOS Persistent Client 10.4.369.0 |  |
| macOS On-demand Client 10.5.297.0 |  |

## [Version 7.21.0](/docs/ocm/release-notes/changelog#version-7210)

Release Date: January 10, 2022

Enhancements:

- Send an alert in case the system failed to update engine modules with Internet mode.
- Increase upload size limit for MetaDefender Endpoint Update packages
- Improve user experience

Security Enhancements:

- Mitigate Apache Log4j critical vulnerabilities

Other Changes:

- Disable Product Survey

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.528.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.661.0 |  |
| macOS Persistent Agent 10.4.363.0 |  |
| macOS On-demand Agent 10.5.294.0 |  |

## [Version 7.20.0](/docs/ocm/release-notes/changelog#version-7200)

Release Date: December 8, 2021

Enhancements:

- Upgraded Java 8 to Java 11
- Improved user interface for the Apply Set Settings feature
- Additional information added to MetaDefender Kiosk Linux scan reports
- The Server URL was not automatically updated after disabling HTTPs setting
- Enhanced the Windows installer to support a long installation path
- Improved user experience

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.513.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.656.0 |  |
| macOS Persistent Agent 10.4.359.0 |  |
| macOS On-demand Agent 10.5.288.0 |  |

## [Version 7.19.0](/docs/ocm/release-notes/changelog#version-7190)

Release Date: October 27, 2021

New features:

- Security settings

Enhancements:

- Include MetaDefender Drive release notes in a new MD Drive firmware package.
- Allow admins to configure age of scan results in a manifest file for Removable Media Protection in a device policy up to 2 years.
- Updated the default TLS cipher suite for Nginx
- Improve user experience.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.496.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.646.0 |  |
| macOS Persistent Agent 10.4.343.0 |  |
| macOS On-demand Agent 10.5.272.0 |  |

## [Version 7.18.0](/docs/ocm/release-notes/changelog#version-7180)

Release Date: September 15, 2021

New features:

- Firmware update for MetaDefender Kiosk Linux and MetaDefender Drive

Enhancements:

- License reactivation for MetaDefender Vault
- Improve data collection for MetaDefender Kiosk Linux
- New event types for the Config History feature
- MetaDefender Core module updater's expanded support for additional OPSWAT products
- Miscellaneous enhancements for the user interface

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.488.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.640.0 |  |
| macOS Persistent Agent 10.4.343.0 |  |
| macOS On-demand Agent 10.5.272.0 |  |

## [Version 7.17.0](/docs/ocm/release-notes/changelog#version-7170)

Release Date: August 4, 2021

Enhancements:

- Expanded privacy settings for managed devices
- New device policy configurations for MetaDefender Endpoint
- New "Pending" state for managed devices
- Allow changing the email address registered for the default administrator account
- Updated report format for the Processing History feature
- Miscellaneous enhancements for the user interface

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.472.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.626.0 |  |
| macOS Persistent Agent 10.4.328.0 |  |
| macOS On-demand Agent 10.5.256.0 |  |

## [Version 7.16.0](/docs/ocm/release-notes/changelog#version-7160)

Release Date: June 23, 2021

New features:

- MetaDefender Kiosk Linux management

Enhancements:

- API-based MetaDefender Kiosk Dashboard
- (Windows only) Customizable installation directory
- Internet update mode for MetaDefender Endpoint and OESIS packages
- Increase the limit of manageable instances for each product type

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.459.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.615.0 |  |
| macOS Persistent Agent 10.4.325.0 |  |
| macOS On-demand Agent 10.5.254.0 |  |

## [Version 7.15.0](/docs/ocm/release-notes/changelog#version-7150)

Release Date: May 12, 2021

New features:

- Update function for OESIS packages
- New device policy configurations for MetaDefender Endpoint:

  - Scan files when they are copied from the host PC to a removable media device.
  - Threat scanning for boot sectors.
  - Anti-Keylogger and Screen Capture Protection.

Enhancements:

- Internet update mode for vulnerability database
- Enhanced Syslog integration with Logstash

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.453.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.608.0 |  |
| macOS Persistent Agent 10.4.319.0 |  |
| macOS On-demand Agent 10.5.252.0 |  |

## [Version 7.14.0](/docs/ocm/release-notes/changelog#version-7140)

Release Date: March 31, 2021

New features:

- Manual Upload function for OPSWAT Central Management's module pool
- Operator user role and product group permissions
- Logstash support for device management logs

Enhancements:

- Display the age of MetaDefender Core modules' database component
- Updating last seen time for devices does not require a compliance check
- Status port configuration for the Windows installer
- More information for MetaDefender Drive instances
- Support for the .csv format for the MetaDefender Kiosk Dashboard's Export Report function

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.441.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.598.0 |  |
| macOS Persistent Agent 10.4.317.0 |  |
| macOS On-demand Agent 10.5.250.0 |  |

## [Version 7.12.0](/docs/ocm/release-notes/changelog#version-7120)

Release Date: February 2, 2021

New features:

- TLSv1.3 support (Windows and Ubuntu only)
- MetaDefender Kiosk dashboard's Export Report function
- Customizable user interface for MetaDefender Endpoint

Enhancements:

- Java location configuration (Windows only).
- Allow users to configure the data collection frequency for MetaDefender Core instances' statistics and processing history for the MetaDefender Core dashboard
- Allow users to adjust the timeout setting for pushing configuration to MetaDefender product instances

Other changes:

- Add a survey to gather customer feedback.

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.429.0 | Detailed release notes for OPSWAT Client are [available here](/docs/ocm/release-notes/opswat-client). |
| Windows On-demand Agent 7.3.588.0 | - Built-in SDK 4.3.1614.0 |
| macOS Persistent Agent 10.4.313.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1415.0 |
| macOS On-demand Agent 10.5.246.0 | - Built-in SDK 4.3.1415.0 |

## [Version 7.11.0](/docs/ocm/release-notes/changelog#version-7110)

Release Date: December 15, 2020

New features:

- AdoptOpenJDK support
- Pop-up scan reports' behavior configuration
- Enterprise UI configuration
- Removable device scan setting for unformatted drives

Enhancements:

- Additional configuration options for MetaDefender Core's module update
- Version information for MetaDefender Endpoint packages and vulnerability database
- Database information for MetaDefender Core instances
- Advanced download function for processing history results
- Clearer error messages for the MetaDefender Endpoint and vulnerability database update functions
- Improved user interface

Other changes:

- Removed the obsolete scheduler interface

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.374.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1614.0 |
| Windows On-demand Agent 7.3.541.0 | - Built-in SDK 4.3.1614.0 |
| macOS Persistent Agent 10.4.294.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1415.0 |
| macOS On-demand Agent 10.5.222.0 | - Built-in SDK 4.3.1415.0 |

## [Version 7.10.0](/docs/ocm/release-notes/changelog#version-7100)

Release Date: October 28, 2020

New features:

- SafeConnect NAC management
- OPSWAT Media Validation Agent repository
- Instructional videos for OPSWAT Product integration

Enhancements:

- Updated OPSWAT MetaAccess feature
- Updated loading page
- Improved MetaDefender Core dashboard
- Timestamp for last MetaDefender Core module update in Folder mode
- Breached password checker
- Port 9026 is now used in place of port 9001
- Improved logging

Other changes:

- Replace Memcached with Redis

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.350.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1513.0 |
| Windows On-demand Agent 7.3.525.0 | - Built-in SDK 4.3.1513.0 |
| macOS Persistent Agent 10.4.294.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1415.0 |
| macOS On-demand Agent 10.5.222.0 | - Built-in SDK 4.3.1415.0 |

## [Version 7.9.0](/docs/ocm/release-notes/changelog#version-790)

Release Date: September 12, 2020

New features:

- MetaDefender Core Dashboard
- Update History

Enhancements:

- Improved Config History feature
- Immediate update of MetaDefender Core instance's module list
- Expand the event types supported by the Event Log feature
- Import/export support for MetaDefender for Secure Storage instances

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.330.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1416.0 |
| Windows On-demand Agent 7.3.507.0 | - Built-in SDK 4.3.1416.0 |
| macOS Persistent Agent 10.4.289.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1301.0 |
| macOS On-demand Agent 10.5.217.0 | - Built-in SDK 4.3.1301.0 |

## [Version 7.8.0](/docs/ocm/release-notes/changelog#version-780)

Release Date: July 22, 2020

New features:

- Config History
- Support vulnerability package update
- Basic integration with MetaDefender for Secure Storage
- MetaDefender Endpoint file scanning reports' storage

Enhancements:

- MetaAccess feature update
- Automatic update of MetaDefender product's vpack data
- Editable retention length

Other changes:

- Removed the function to search for syslog by log type in the MetaDefender Kiosk Dashboard.

| **Built-in OPSWAT Client version** |  |
| --- | --- |
| Windows Persistent Agent 7.6.313.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1334.0 |
| Windows On-demand Agent 7.3.496.0 | - Built-in SDK 4.3.1334.0 |
| macOS Persistent Agent 10.4.283.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.1210.0 |
| macOS On-demand Agent 10.5.212.0 | - Built-in SDK 4.3.1210.0 |

## [Version 7.7.0](/docs/ocm/release-notes/changelog#version-770)

Release Date: June 10, 2020

New features:

- MetaDefender Kiosk Dashboard
- Update MetaDefender Core modules from folder
- Ubuntu 18.04 support

Enhancements:

- Support IPv6 address for the Device Management feature
- Enhance user experience according to Section 508 guideline.
- Automatically update MetaDefender product's vpack data
- Increase data retention length
- Improve license information for MetaDefender Vault

## [Version 7.6.0](/docs/ocm/release-notes/changelog#version-760)

Release Date: April 17, 2020

Enhancements:

- Updated OPSWAT MetaAccess feature
- Expanded proxy configuration feature
- A D Users
- Improved UI

## [Version 7.5.0](/docs/ocm/release-notes/changelog#version-750)

Release Date: February 25, 2020

New features:

- Proxy Configuration
- Support package tool

Enhancements:

- Support for system proxy settings' exclusion list
- Port configuration on the installer
- Improved MetaDefender Core Processing History feature
- Server URL setting now automatically update with the current port configuration
- Improved UI

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.264.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.771.0 |
| Windows On-demand Agent 7.3.460.0 | - Built-in SDK 4.3.771.0 |
| macOS Persistent Agent 10.4.269.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.911.0 |
| macOS On-demand Agent 10.5.198.0 | - Built-in SDK 4.3.911.0 |
| Enhancements | - Support self-sign certificate for SSL settings - Exit button is removed from tray icon to prevent accidental termination. |

## [Version 7.4.0](/docs/ocm/release-notes/changelog#version-740)

Release Date: January 9, 2020

New features:

- Red Hat Enterprise Linux 7.7's support
- MetaDefender Core Processing History

Enhancements:

- MetaDefender ICAP and MetaDefender Email Security offline configuration support
- Import/Export improvement
- SSO configuration without license
- Port configuration for the console interface
- Event log now displays all available data since initial installation

| Built-in OPSWAT Client version |  |
| --- | --- |
| Windows Persistent Agent 7.6.248.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.771.0 |
| Windows On-demand Agent 7.3.443.0 | - Built-in SDK 4.3.771.0 |
| macOS Persistent Agent 10.4.255.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.911.0 |
| macOS On-demand Agent 10.5.187.0 | - Built-in SDK 4.3.911.0 |

## [Version 7.3.0](/docs/ocm/release-notes/changelog#version-730)

Release Date: November 22, 2019

New features:

- MetaDefender Drive management
- Single sign-on (SSO) support

Enhancements:

- Added password reset function for administrator account
- MetaDefender Core modules disabled during the update process now continue downloading instead of abort midway.
- Added log files containing the history of installed OPSWAT Central Management versions.
- Various UI enhancements to improve readability and usability.

| Built-in OPSWAT Clients |  |
| --- | --- |
| Windows Persistent Agent 7.6.248.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.771.0 |
| Windows On-demand Agent 7.3.443.0 | - Built-in SDK 4.3.771.0 |
| macOS Persistent Agent 10.4.255.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.911.0 |
| macOS On-demand Agent 10.5.187.0 | - Built-in SDK 4.3.911.0 |

## [Version 7.2.0](/docs/ocm/release-notes/changelog#version-720)

Release Date: October 4, 2019

New features:

- Product Set and Group management
- User and User Group management
- Active Directory integration
- MetaDefender Core module updater
- Improved import/export function
- MetaDefender ICAP and Email Gateway Security management (Preview mode)

Enhancements:

- Added a mechanism to automatically detect system proxy
- Updated configuration wizard
- MetaDefender Core and Vault instances can now recognize being managed by OPSWAT Central Management.
- Separate HTTPS configuration from the main nginx's configuration file.
- Added a warning message when adding a disconnected product instance.
- Improved UI's consistency.

| Built-in OPSWAT Clients |  |
| --- | --- |
| Windows Persistent Agent 7.6.248.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.771.0 |
| Windows On-demand Agent 7.3.443.0 | - Built-in SDK 4.3.771.0 |
| macOS Persistent Agent 10.4.244.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.631.0 |
| macOS On-demand Agent 10.5.179.0 | - Built-in SDK 4.3.631.0 |

## [Version 7.1.1](/docs/ocm/release-notes/changelog#version-711)

Release Date: August 15, 2019

Enhancements:

- Added a mechanism to handle high load
- Updated the software requirements to JRE instead of JDK

| Built-in OPSWAT Clients |  |
| --- | --- |
| Windows Persistent Agent 7.6.242.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.771.0 |
| Windows On-demand Agent 7.3.436.0 | - Built-in SDK 4.3.771.0 |
| macOS Persistent Agent 10.4.242.0 | - Supported MetaDefender Core Load-Balancer Layer 7 - Built-in SDK 4.3.631.0 |
| macOS On-demand Agent 10.5.172.0 | - Built-in SDK 4.3.631.0 |

## [Version 7.1.0](/docs/ocm/release-notes/changelog#version-710)

Release Date: July 2, 2019

Built-in clients

- Windows Persistent Agent 7.6.236.0
- Windows On-demand Agent 7.3.436.0
- macOS Persistent Agent 10.4.226.0
- macOS On-demand Agent 10.5.172.0

New features:

- Inventory Management for OPSWAT Products (Kiosk, Core and Vault)
- Configuration Management for OPSWAT Products (Kiosk, Core and Vault)
- License Management for OPSWAT Products (Kiosk, Core and Vault)
- Policy Management for OPSWAT Products (Kiosk, Core and Vault)
- Health Check
- Import from URL
