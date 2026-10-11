<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/release-notes/release-notes -->

# Release Notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Version 3.5.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-350)

Release date: June 17, 2026

New features:

- Support for Export/Import configuration. Details: [Export/Import Configuration](/docs/mddownloader/v3.5.0/operating/export-import-configuration)
- Support for custom installation path, details: [Installing Update Downloader using the Command Line](/docs/mddownloader/v3.5.0/installation/installing-update-downloader-using-the-command-line)
- Support Ubuntu 24.04 with CIS level 1 and level 2

Enhancements:

- Upgraded NGINX to v1.30.2
- Upgraded zlib to v1.3.2
- Upgraded OpenSSL to v3.5.6

## [Version 3.4.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-340)

Release date: Mar 04, 2026

New features:

- New OS support: Ubuntu 24.04
- API key protection:

  - Strengthening security by protecting users' API key (if created) in the database using SHA256 hashing. Then actual API key value could not be retrieved back for good.
  - By default, this feature is not enabled for backward compatibility. Administrators need to opt-in by enabling that. Expecting to see the following UI notification poped up upon signed in:
  - ***Warning:*** *Once enabled, administrators cannot turn back the feature for security enforcement. Before switching on this feature, it's strongly recommended to backup your users' API key in a secured vault / secrets manager.*
  - When this feature is enabled, API key will be hashed out in the database, and no one, including administrators, will be able to see actual API key value anywhere in the product.
  - In case API key is lost or not remembered, then administrators must re-create a new one. The new one will be displayed for only one time on the UI.
- Unified User Interface and Experience of Login and Guest Scan Screens
- Support add license for new OPSWAT product: Standalone SANDBOX

Enhancements:

- Upgrade encryption from DES to AES-256-GCM
- Upgraded Qt to 6.8.1
- Upgraded OpenSSL to 3.5.5
- Upgraded 7zip to 26.0
- Upgraded NGINX to 1.29.5
- Upgraded Angular to 19.2.17
- Updated Terms of Service

Bug fix:

- Fix bug when session token show in the URL
- Some minor UI bugs.

## [Version 3.3.1](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-331)

Release date: Nov 12, 2025

Enhancements:

- Upgraded OpenSSL to 3.5.4
- Upgraded Protobuf to 32.1
- Upgraded NGINX to 1.28.0
- Upgraded Yaml-Cpp to 0.8.0
- Upgraded OpenLDAP to 2.6.10
- Upgraded 7zip to 25.01

## [Version 3.3.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-330)

Release date: July 17, 2025

New features:

- New OS support: Windows Server 2025
- Support automation deployment via ignition file. More details at [Automation Deployment](/docs/mddownloader/v3.5.0/installation/automation-deployment-via-ignition-file#overview).
- Support configure logging via web console.

## [Version 3.2.3](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-323)

Release date: May 20, 2025

Enhancements:

- New API endpoint for health check which provides server disk space, updater connection status, product version. Document: [Monitoring](/docs/mddownloader/v3.5.0/operating/monitoring)
- Introduce configurable settings for idle timeout and absolute session timeout.
- Unlicensed engines now can be removed on Engines screen.
- Updated EULA.

## [Version 3.2.2](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-322)

Release date: April 10, 2025

Enhancements:

- Support offline licensing with On-prem License Management Server (OLMS).
- Introduce an ability to display a custom notice on signin screen.
- For vulnerability fixes:

  - Upgraded zlib to v1.3
  - Upgraded quazip to v1.4
  - Upgraded protobuf to v3.21.12
  - Upgraded openssl to v3.4.1

## [Version 3.2.1](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-321)

Release date: February 06, 2025

Enhancements:

- Upgraded NGINX to v1.26.2 for vulnerability fixes.
- Upgraded OpenSSL to v3.4.0 for vulnerability fixes.
- Upgraded 7z to v24.09 for vulnerability fixes.

Bug fix:

- Addressed an issues that caused intermittent operation of Post Action.

## [Version 3.2.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-320)

Release date: November 19, 2024

New features:

- Password policy enforcement
- New OS support: Rocky Linux 9

Bug fix:

- Addressed an issue that made the feature "Download All as ZIP" not work when engine version of embedded Sandbox engine was not visible yet.

## [Version 3.1.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-310)

Release date: July 18, 2024

New features:

- New OS support:

  - Debian 12
  - Ubuntu 22.04
  - Windows 11
  - Windows Server 2022
- OS support retirement: Debian 9.x, Ubuntu 16.04, Microsoft Windows Server 2008 R2 or newer (64 bit)
- Updated Terms of Service.
- Introduce the ability to remove specific engines from the user interface.
- Supported new engine types: Adaptive Sandbox, Reputation, COO (Country of Origin), and SBOM (Software Bill of Materials).
- Introduced the ability to download individual packages. Users can now selectively download specific packages, allowing for a more targeted and efficient approach to package management.
- Users can now add descriptions to products, providing valuable context and information facilitating better organization and tracking of updates.

Bug fixes:

- Addressed the issue that only the engine part was disabled, while the database part remained enabled.
- Resolved an issue that installation folder was not removed entirely after uninstalling the product.

## [Version 3.0.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-300)

Release date: February 17, 2023

New features:

- A brand-new user interface for the management console

## [Version 2.5.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-250)

New features:

- Support post actions (to auto trigger script whenever engines and databases are ready)

Bug fixes:

- Fixed unable to download all as .zip big package
- Fixed issue when engine can't reach ready state for MetaDefender Core v3
- UI minor fixes

## [Version 2.4.1](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-241)

Bug fixes:

- Fixed issues on update time rules
- Refined user guide

## [Version 2.4.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-240)

New features:

- Support multiple OPSWAT MetaDefender products
- Enhance engine package verification before allowing download all as .zip

## [Version 2.3.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-230)

New features:

- The available packages can be downloaded via web interface as one big ZIP file
- More informative dashboard

## [Version 2.2.1](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-221)

New features:

- New-looking user interface

## [Version 2.2.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-220)

New features:

- Full audit log about any configuration changes via Web user interface or REST API
- Able to disable exporting update in user configurable time periods
- Support to download OESIS updates
- Able to set up apikey for every user for easier REST API integration
- Improved hardware detection in license component
- Improved activation process feedback on web user interface

Issues fixed:

- Fixed message content format in Windows Event log
- Fixed system wide proxy usage on Windows
- Improved browser cache handling in case of product upgrades
- Patched internal nginx web server to fix CVE-2016-4450
- Improved logging of proxy usage
- Detailed logging in case of SSL connection issues

## [Version 2.1.2](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-212)

- Support package generation on Microsoft Windows
- Added hardware related info into generated support package
- Option added to log to a remote syslog server
- Improved system issue notification on Web Management Console
- Removed unmeaningful database age display of non-anti-malware engines

## [Version 2.1.1](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-211)

- Rebranded to Metadefender Update Downloader
- Download stability fixes

## [Version 2.1.0](/docs/mddownloader/v3.5.0/release-notes/release-notes#version-210)

- Initial release
