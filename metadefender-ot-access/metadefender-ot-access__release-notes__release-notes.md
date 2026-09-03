<!-- source: https://www.opswat.com/docs/metadefender-ot-access/release-notes/release-notes -->

# Release Notes

## [Version 2.3.3](/docs/metadefender-ot-access/release-notes/release-notes#version-233)

Component versions: Admin UI 2.3.3, Management Console 3.02.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- Migrated the database to PostgreSQL to improve scalability and reliability.
- Added support for logging and monitoring events between OT Access and OT Gateway.
- Bug fixes.

## [Version 2.3.2](/docs/metadefender-ot-access/release-notes/release-notes#version-232)

Component versions: Admin UI 2.3.2, Management Console 3.02.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- SSH clientless recording.
- Endpoint Gateway (Management Console) UX improvements.
- New information banner.

- Bug fixes.

## [Version 2.3.1](/docs/metadefender-ot-access/release-notes/release-notes#version-231)

Component versions: Admin UI 2.3.1, Management Console 3.00.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- The Endpoint Gateway can now report to two different OT Access Servers.
- Bug fixes.

## [Version 2.3.0](/docs/metadefender-ot-access/release-notes/release-notes#version-230)

Component versions: Admin UI 2.3.0, Management Console 3.00.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- Support for the new Dashboard.
- Support for VNC Clientless.

## [Version 2.2.0](/docs/metadefender-ot-access/release-notes/release-notes#version-220)

Component versions: Admin UI 2.2.0, Management Console 2.2.0, Windows Client 3.00.0000, Windows Service Client 3.00.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- Added logging to track who approves or rejects request emails, including token expiration handling for third-party users.
- Unified the login page for a consistent authentication experience.
- Enhanced audit logging for Request and User workflows.
- Implemented automatic rejection of expired requests.
- Introduced tag management for users.
- Added filtering and export capabilities for the Connection Dashboard and Logs, based on attributes and timeframes.
- Improved overall back-end performance.

## [Version 2.1.0](/docs/metadefender-ot-access/release-notes/release-notes#version-210)

Component versions: Admin UI 2.1.0, Management Console 2.1.0, Windows Client 3.00.0000, Windows Service Client 3.00.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- MetaDefender Core integration across environments for consistent threat prevention and file sanitization.
- Automated file retrieval for secure delivery into OT networks, leveraging proven MFT technology.
- Enhanced flexibility for hybrid IT/OT architectures.
- Minor bug fixes.

## [Version 2.0.1](/docs/metadefender-ot-access/release-notes/release-notes#version-201)

Component versions: Admin UI 2.0.1, Management Console 2.0.1, Windows Client 3.00.0000, Windows Service Client 3.00.0000

### [Vulnerability Remediations](/docs/metadefender-ot-access/release-notes/release-notes#vulnerability-remediations)

- Updated Bootstrap to version 5.3.
- Fixed SSL certificate expiry.
- Fixed SSL Medium Strength Cipher Suites Supported (SWEET32).

## [Version 2.0.0](/docs/metadefender-ot-access/release-notes/release-notes#version-200)

Component versions: Admin UI 2.0.0, Management Console 2.0.0, Windows Client 3.00.0000, Windows Service Client 3.00.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- MetaDefender Core integration to allow remote users to send files to a MetaDefender Core instance for file scanning.
- OS updated to Debian 12.
- Several improvements on MFT integration.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed a bug that caused provider users to be able to access the Connection Dashboard and terminate services.
- Fixed a bug that caused admins to be unable to accept/reject requests under certain circumstances.
- Fixed a bug that caused screen recordings to not be generated under certain circumstances.

## [Version 1.8.1](/docs/metadefender-ot-access/release-notes/release-notes#version-181)

Component versions: Admin UI 1.8.1, Management Console 1.8.1, Windows Client 3.00.0000, Windows Service Client 3.00.0000

### [Improvements/Updates](/docs/metadefender-ot-access/release-notes/release-notes#improvementsupdates)

- MFT integration improvement to allow remote users to deliver transferred files directly to a shared folder after scanning.
- Improvement in the Connections Dashboard to allow superadmins to terminate active sessions instead of simply removing access.
- Configurable schedule time limits.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed a bug that caused an exported log to be empty in some circumstances.
- Fixed a bug that caused text display issues when using long inputs in the Requests section.

## [Version 1.8.0](/docs/metadefender-ot-access/release-notes/release-notes#version-180)

Release Date: March 14, 2025

Component versions: Admin UI 1.8.0, Management Console 1.8.0, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- MFT integration. An MFT instance can be integrated to work together with MetaDefender OT Access so a remote user can upload and download files in a safe manner.
- Splunk integration (HTTP Event Collector). MetaDefender OT Access can send logs to a Splunk instance.
- ServiceNow integration, to integrate access request and approval processes with ServiceNow.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed a bug that, under specific circumstances, allowed deleted users to log in on the Endpoint.

## [Version 1.7.33](/docs/metadefender-ot-access/release-notes/release-notes#version-1733)

Release Date: August 28, 2024

Component versions: Admin UI 1.7.33, Management Console 1.7.33, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Implementation of SSO Console — SAML authentication.

## [Version 1.7.32](/docs/metadefender-ot-access/release-notes/release-notes#version-1732)

Release Date: June 25, 2024

Component versions: Admin UI 1.7.32, Management Console 1.7.32, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Allows providers to monitor the Connections Dashboard.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Stability improvement.

## [Version 1.7.31](/docs/metadefender-ot-access/release-notes/release-notes#version-1731)

Release Date: May 28, 2024

Component versions: Admin UI 1.7.31, Management Console 1.7.31, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Changed name to MetaDefender OT Access.

## [Version 1.7.30](/docs/metadefender-ot-access/release-notes/release-notes#version-1730)

Release Date: May 27, 2024

Component versions: Admin UI 1.7.30, Management Console 1.7.30, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Monitor active clientless sessions.

## [Version 1.7.29](/docs/metadefender-ot-access/release-notes/release-notes#version-1729)

Release Date: March 26, 2024

Component versions: Admin UI 1.7.29, Management Console 1.7.29, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Support for TOTP MFA.
- Applied the new OPSWAT product name.

## [Version 1.7.28](/docs/metadefender-ot-access/release-notes/release-notes#version-1728)

Release Date: February 2024

Component versions: Admin UI 1.7.28, Management Console 1.7.28, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Support for compliance checks in clientless service access.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed the client showing "Incorrect username/password" when the hostname of the compliance check configuration is invalid.

## [Version 1.7.27](/docs/metadefender-ot-access/release-notes/release-notes#version-1727)

Release Date: January 2024

Component versions: Admin UI 1.7.27, Management Console 1.7.27, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Allow site admins to see session recordings for their sites.
- Improved logging for web-based RDP sessions.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed being unable to kill a web-based RDP session.
- Fixed SMTP not working in on-premises environments.
- Fixed the client keeping the connection loading when it does not receive any service.

## [Version 1.7.26](/docs/metadefender-ot-access/release-notes/release-notes#version-1726)

Release Date: December 2023

Component versions: Admin UI 1.7.26, Management Console 1.7.26, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Enabled the Screen Recordings feature for web RDP in the cloud version.
- Provide a web-only access option for RDP resources.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed being unable to use the clientless service.
- Fixed no 2FA input being available in the merged client.
- Fixed admins being able to grant access for every user and every service through service ID and user ID.
- Fixed Apache Guacamole vulnerability to RCE and privilege escalation via vulnerability chaining.
- Fixed the client showing an incorrect status.

## [Version 1.7.25](/docs/metadefender-ot-access/release-notes/release-notes#version-1725)

Release Date: November 2023

Component versions: Admin UI 1.7.25, Management Console 1.7.25, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Administrators can enable the OT feature by MA group.
- Log compliance checks for multi-tenancy.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed getting an async access_key from MA when the server handles the compliance configuration form.
- Fixed always-on and auto-reconnecting behavior.

## [Version 1.7.24](/docs/metadefender-ot-access/release-notes/release-notes#version-1724)

Release Date: October 2023

Component versions: Admin UI 1.7.24, Management Console 1.7.24, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- The OT feature can be enabled from the MA console.
- The OT console supports configuring the compliance interval.
- Multi-tenancy.
- Allow users to configure compliance check settings from the OT console.
- OT client authentication can be used within the OPSWAT Client.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed site admins seeing logs that do not relate to their site.
- Fixed site admins seeing connections for a different site.
- The OT controller can check compliance status at login time for every client that is trying to authenticate.

## [Version 1.7.23](/docs/metadefender-ot-access/release-notes/release-notes#version-1723)

Release Date: September 2023

Component versions: Admin UI 1.7.23, Management Console 1.7.23, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed MetaAccess OT users not receiving the 2FA code (SMS) in the EMEA region.

## [Version 1.7.22](/docs/metadefender-ot-access/release-notes/release-notes#version-1722)

Release Date: July 2023

Component versions: Admin UI 1.7.22, Management Console 1.7.22, Windows Client 3.00.0000, Windows Service Client 3.0.0000

### [New Features](/docs/metadefender-ot-access/release-notes/release-notes#new-features)

- Option in settings to define the default 2FA option for all instance users.
- Allow specific user accounts to be exempted from password expiry.

### [Bug Fixes](/docs/metadefender-ot-access/release-notes/release-notes#bug-fixes)

- Fixed the login logo not scaling correctly.
- The Windows client now shows the password expiry notification.
- Persist end-user settings for browserless RDP resolution.
- Clientless (browser) access header change.

For releases prior to 2023, see Archived release notes.
