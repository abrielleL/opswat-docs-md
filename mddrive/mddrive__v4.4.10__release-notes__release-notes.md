<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/release-notes/release-notes -->

# MetaDefender Drive v4.4.10

View as Markdown Ask ChatGPT about this page Ask Claude about this page

|  |  |
| --- | --- |
| **Released on** **Oct 02, 2026** | This release includes new features, improvements, bug fixes. |

**New Features**

- **Automate Out-of-box Experience Setup**: A pre-filled configuration file placed on the drive before deployment handles registration, licensing, and network setup automatically, so MetaDefender Drive is operational without manual steps at the site. Refer to [Automate First-Boot Setup with an Ignition File](/docs/mddrive/v4.4.10/configuration/out-of-box-experience-setup) for this new method of setup MetaDefender Drive.
- **Centralized Scan Profiles with OTP Managed via Central Management:** Added manage OTP in Central Management. Refer to [Centralized Scanning Profile - Provisioning from OPSWAT Central Management](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-provision-from-ocm) for details.
- **Allow all preferences in Central Management** Add most common setting in MetaDefender Drive are in Central Management, **including settings for In-Session and KIOSK Certificates for Secure File Storage** (this requires Central Management v.10.7.26091 at minimum. Refer to [Central Management Release](https://www.opswat.com/docs/cm/release-notes) if needed)
- **Whitelist List Import from Central Management:** Hashes and file locations known to be safe can be imported from OPSWAT Central Management server and then distributed to MetaDefender Drive as an allowed list.
- **Longer Diff Scan Policy**: The Differential Scan baseline can be kept for up to 365 days on MetaDefender Drive 2 (1 TB)
- **Show More Status While Booting:** Rather than a static screen for several minutes while scan services load, MetaDefender Drive shows progress messages so the drive does not appear hung.

- **Sort scan progress**: Newer scan jobs sort to the top of the progress list, so faster jobs remain visibly active even when a slow job is running underneath them.
- **Expanded Device Inventory:** In-Session and Bare Metal scans now report device inventory to OPSWAT Central Management, adding BIOS type, secure boot status, CPU architecture, memory, Installed Applications, and operating system details.

**Improvements**

- **Provide clear indication engine ready for scan**: While engines are downloading or installing, the dashboard shows the current status so operators know why scanning cannot begin yet.
- **Kiosk enrollment on restricted networks:** On networks where certificate revocation list endpoints are unreachable, MetaDefender Drive Toolkit enrollment and engine updates against OPSWAT Central Management complete without error.
- **Custom scan controls:** Archive scanning and file type analysis can be toggled on or off individually on the Custom scan screen.

- **Missing engine guidance:** When no anti-malware engines are installed, the Custom scan screen replaces the Malware Multiscan checkbox with a message directing to the Engines tab.
- **Improve In-Session engines setup (splash screen)**: The engine setup phase that appears on launch of MetaDefender Drive In-Session Scan completes faster, cutting the wait before scanning can begin.
- **Email report signature:** Email scan reports include the digital signature file alongside the PDF.
- **License-aware engine sync:** License Info now gets synced to OPSWAT Central.

**Bug Fixes**

- Added upfront validation to block scans and clearly notify users when no mountable partitions are found
- Fixed an issue where Digital Display USBs dropped into the BusyBox prompt during startup
- Resolves an issue where update check failures in Boot Mode were falsely reported as 'Up to date'
- Resolves OPSWAT Central Management disconnection after restart
- Eliminates engine activation hangs caused by virtualized USB I/O emulation overhead
- MetaDefender Drive reconnects to OPSWAT Central Management when a lost connection is restored
- Resolves the issue where scan engines disappeared from the UI during boot updates and initialization
- Resolves the application crash during full In-Session scans
- Fixing the MetaDefender Drive Integration launcher deadlock eliminates intermittent Kiosk launch failures (14–19%)
- Enrollment failure messages now identify whether the problem is network-related
