<!-- source: https://www.opswat.com/docs/product-management/release-notes/changelog -->

# Changelog

## [Version: 2025.2.1](/docs/product-management/release-notes/changelog#version-202521)

Release date: April 12, 2025, UTC

**Bugs Fixed:**

- Could not process MetaDefender Core's reports
- Could not save configuration after upgrading MetaDefender Core to 5.14.0

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2025.1.3](/docs/product-management/release-notes/changelog#version-202513)

Release date: February 14, 2025, UTC

**Enhancements:**

- Improved performance for MetaDefender Core dashboard and processing history features.
- Improved user experience and interface.

**Bugs Fixed:**

- MetaDefender Kiosk L-Series instances failed send scan reports that have large file size.
- The MetaDefender Core dashboard displayed incorrect results in the Processing Overview section after batched scan reports were submitted.

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2025.1.2](/docs/product-management/release-notes/changelog#version-202512)

Release date: January 17, 2025, UTC

**Enhancements:**

- Improved product instance list export.
- Improved a process to manage product configuration versions.
- Performance improvement.
- Improved user experience and interface

**Bugs Fixed:**

- In Event Log, configuration synchronization events for certain product types were missing.
- In Processing History, the exported .csv file contained different result filters than those that were selected on the user interface.
- In Processing History, the time range of 1 day (i.e, 1/1/2025 to 1/1/2025) could not be selected.
- When the server is under high load of product reports, the Security dashboard reported an "Unknown" error.
- After applying a product group configuration to an instance that already had the same configuration, that instance's configuration status was stuck in "Pending".

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2025.1.1](/docs/product-management/release-notes/changelog#version-202511)

Release date: January 3, 2025, UTC

**Enhancements:**

- Updated user interface

**Bugs Fixed:**

- When a MetaDefender ICAP Server or MetaDefender File Transfer instance unenrolled from My OPSWAT, its scan reports were not deleted.
- The processing overview and blocked files APIs for MetaDefender Kiosk and MetaDefender Core returned data from all instances when an invalid instance or group ID filter was used.

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2024.4.5](/docs/product-management/release-notes/changelog#version-202445)

Release date: December 12, 2024, UTC

**New Features:**

- MetaDefender Industrial Firewall
- MetaDefender Transfer Guard

**Enhancements:**

- MetaDefender ICAP Server
- MetaDefender Kiosk K-Series
- MetaDefender Core
- Updated user interface

**Bugs Fixed:**

- The product instances page occasionally fails to load correctly when navigating to the second page and beyond.
- MetaDefender Kiosk Summary report was not sent at the configured time after upgrading My OPSWAT.
- Could not load Active Directory (AD) users/groups if a username doesn't include a domain when configuring MetaDefender Kiosk K-Series.

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2024.4.3](/docs/product-management/release-notes/changelog#version-202443)

Release date: November 6, 2024, UTC

**Enhancements:**

- MetaDefender Kiosk L-Series management
- Updated user interface

**Bugs Fixed:**

- MetaDefender Managed File Transfer dashboard did not display any data when the time filter was set to 1 day.
- Event Log entries had the incorrect product type in the Impacted column for certain type of events.

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2024.4.2](/docs/product-management/release-notes/changelog#version-202442)

Release date: October 17, 2024, UTC

**New Features:**

- MetaDefender Managed File Transfer - Dashboard
- MetaDefender Kiosk K-Series's - Remote Command
- Public API: added a new API to retrieve Kiosk processing overview

**Enhancements:**

- Enhanced performance
- Improved user experience and interface

**Bugs Fixed:**

- Scan reports in .json file type had different filename format compared to .txt and .pdf file types.
- Missing Event Log entry for when a MetaDefender Kiosk L-Series instance requested license data.
- In the product dashboard pages, when applying the 24H (24 hours) and 12M (12 months) filters, the charts failed to display the correct timestamps.
- MetaDefender Kiosk summary reports' "End time" data field was incorrect when the email notification setting was set to daily recurrence.
- Previously disconnected MetaDefender Core instances did not have their status updated after sending scan reports successfully.

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2024.4.1](/docs/product-management/release-notes/changelog#version-202441)

Release date: October 17, 2024, UTC

**Note:**

- No changes for this release. Reference for My OPSWAT On-premises 2024.4.1

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.
- The Event Log page is loading slowly.

## [Version: 2024.3.4](/docs/product-management/release-notes/changelog#version-202434)

Release date: September 18, 2024, UTC

**New Features:**

- Public APIs
- MetaDefender ICAP Server management

**Enhancements:**

- Improved performance

**Bugs Fixed:**

- Scheduled tasks such as firmware updates did not run at the configured time due to time zone issue.
- When adding offline license files for product instances, only 1 file was uploaded even if multiple files were selected.
- Self-scan reports for MetaDefender Kiosk K-Series could not be downloaded with an "Unable to acquire report" error.
- In a MetaDefender Core instance's Processing History page, scan results showed as In Progress and did not match with the instance's own web interface.
- MetaDefender Kiosk L-Series instances did not updated their licensing status when updating its license.
- Could not view a MetaDefender Kiosk L-Series instance if it submitted a scan report with large file size.
- Using product group filter in the MetaDefender Core dashboard returned an incorrect result for Processing Overview.
- The Security Alert page had incorrect data if the server was processing a large amount of scan reports.
- Some product instances changed status to "Unmanaged" after the My OPSWAT update.

**Other Changes:**

- My OPSWAT - Product Management rebranding

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.
- The Event Log page is loading slowly.

## [Version: 2024.3.2](/docs/product-management/release-notes/changelog#version-202432)

Release date: August 07, 2024, UTC

**New Features:**

- MetaDefender ICAP management
- MetaDefender File Transfer management

**Enhancements:**

- Improved user experience and interface

**Bugs Fixed:**

- When creating a product group, the available instance count was not accurate.
- The product dashboard's data was incorrect if multiple filters were used in combination for the Configuration Status field.
- When updating a MetaDefender Core instance's configuration, My OPSWAT returned a 413 Request Entity Too Large error.
- Changing Kiosk Report Summary settings did not create an Event Log entry.
- Email notifications from the Reports & Notification feature contained incorrect content such as incorrect date range or invalid URL.
- The Reports & Notification feature did not send email if users choose a weekly recurrence pattern.
- The summary reports created by the Reports & Notification feature contained incorrect data.
- Organization name change did not apply immediately in the console.
- MetaDefender Kiosk L-Series license could not be activated.

**Other Changes:**

- Update branding for OPSWAT NetWall products

**Known Limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.
- The Event Log page has slow loading performance.
- Selfscan reports for MetaDefender Kiosk K-Series could not be downloaded with an "Unable to acquire report" error.
- Some product instances changed status to "Unmanaged" after the My OPSWAT update.

## [Version: 2024.3.1](/docs/product-management/release-notes/changelog#version-202431)

Release date: July 05, 2024, UTC

**New Features:**

- MetaDefender Kiosk K-Series Management
- MetaDefender Endpoint - Response Code Generator

**Enhancements:**

- Performance enhancement

**Bugs Fixed:**

- The MetaDefender Core's Processing History failed to load when a user conducted a search using specific special characters.

**Known limitations:**

- When configuring a MetaDefender Kiosk K-Series instance through My OPSWAT, searching for users only returns results from 1 local Active Directory even if multiple are available.

## [Version: 2024.2.1](/docs/product-management/release-notes/changelog#version-202421)

Release date: June 06, 2024, UTC

**New Features:**

- MetaDefender Core Management
- MetaDefender Software Supply Chain
- License Management
- MetaDefender Kiosk summary report
- Modules Update

## [Version: 2024.1.1](/docs/product-management/release-notes/changelog#version-202411)

Release date: January 31, 2024, UTC

**Enhancements:**

- Security Issue Alerts
- Security Overview
- Re-arrange modules on MetaDefender Media Firewall dashboard

**Bugs Fixed:**

- Could not download an instance report that had been renamed to contained special characters such as "/".
- Instance report in .pdf format did not follow the same file naming convention as the .json and .txt format.
- In the MetaDefender Kiosk dashboard, the average files scanned per session statistic was calculated incorrectly.
- The documentation URL for MetaDefender OT Security was broken.

**Other Changes:**

- Updated branding for OPSWAT Filescan Sandbox

## [Version: 2023.4.4](/docs/product-management/release-notes/changelog#version-202344)

Release date: December 21, 2023, UTC

**Enhancements:**

- Custom Dashboard
- Improved user experience and interface

**Bugs Fixed:**

- Failed to download MetaDefender Kiosk reports in .txt or .pdf format if the report size is over 4MB

**Other Changes:**

- Updated branding for OPSWAT Neuralyzer

## [Version: 2023.4.3](/docs/product-management/release-notes/changelog#version-202343)

Release date: November 30, 2023, UTC

**Enhancements:**

- Enhanced MetaDefender Kiosk Dashboard.
- Applied user's time zone to datetime on console.
- Improved user experience and interface.

**Bugs Fixed:**

- Navigating to My Products from my.opswat.com changed the current organization context to a different organization that the users belong to. Other Changes:

**Other Changes:**

- Updated branding for MetaDefender Vault

## [Version: 2023.4.2](/docs/product-management/release-notes/changelog#version-202342)

Release date: October 31, 2023, UTC

**New Features:**

- MetaDefender Media Firewall Dashboard

## [Version: 8.1.9](/docs/product-management/release-notes/changelog#version-819)

Release date: June 7, 2023, UTC

**Other Changes:**

- Updated **Request Support** and **Community Portal** hyperlinks in the left sidebar

## [Version: 8.1.8](/docs/product-management/release-notes/changelog#version-818)

Release date: April 26, 2023, UTC

**Bugs Fixed:**

- The management console could not display product license information at all if the organization possesses a bundle license.

## [Version: 8.1.7](/docs/product-management/release-notes/changelog#version-817)

Release date: April 5, 2023, UTC

**Enhancements:**

- Added description for each activation, if any, to a license key report
- Improved user interface and experience

**Bugs Fixed:**

- A JSON report of a MetaDefender Kiosk L1001 instance was empty if the instance's name contains special characters
- Users that had not registered an OPSWAT account did not receive an email invitation upon being invited to join an organization via email.

## [Version: 8.1.6](/docs/product-management/release-notes/changelog#version-816)

Release date: March 2, 2023, UTC

**New Features:**

- OPSWAT's product update notifications
- OPSWAT FileScan license management
- Support MetaDefender Kiosk Secure Image

**Enhancements:**

- Improved system status notifications
- Data Retention setting
- More information for MetaDefender Kiosk L1001 instances list report
- Improved user interface and experience

**Bugs Fixed:**

- MetaDefender Cloud license was not available for a user that originally belong to an account that does not have MetaDefender Cloud license.
- A file uploaded via the Upload Large File feature was corrupted.
- A user's status stayed as Invited even the user logged in if the user was invited to more than one account.

## [Version: 8.1.5](/docs/product-management/release-notes/changelog#version-815)

Release date: January 4, 2023

**New Features:**

- OEM Products management
- Upload large files
- Support MetaDefender Kiosk Secure Image

## [Version: 8.1.4](/docs/product-management/release-notes/changelog#version-814)

Release date: November 30, 2022

**New Features:**

- Anti-Malware Engine Status

## [Version: 8.1.3](/docs/product-management/release-notes/changelog#version-813)

Release date: November 22, 2022

**Enhancements:**

- User interface and experience improvement

## [Version: 8.1.2](/docs/product-management/release-notes/changelog#version-812)

Release date: November 16, 2022

**Enhancements:**

- Provided a way for users to switch to OPSWAT Portal.

## [Version: 8.1.1-beta](/docs/product-management/release-notes/changelog#version-811-beta)

Release date: October 17, 2022

**New Features:**

- SaaS Security Management Platform
- License visibility
- User Management
- Product Installers
- OPSWAT services status
