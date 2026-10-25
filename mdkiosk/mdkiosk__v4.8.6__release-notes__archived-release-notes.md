<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/release-notes/archived-release-notes -->

# Archived Release Notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## 4.8.5

| **Release date** | 18 Sept 2026 |
| --- | --- |
| **Enhancement** | |
| Enforce OPSWAT USB hub to use USB 2.0 mode | On OPSWAT Kiosk devices, administrators can now configure the OPSWAT USB hub to use USB 2.0 mode from Configuration > Advanced > Encrypted USB, allowing hardware-encrypted USB drives to be detected reliably.  When this option is not enabled, Kiosk can automatically detect when a hardware-encrypted USB drive fails to mount and switch to USB 2.0 mode. |
| Kiosk 4.8.5.9349 | |
| **Release date** | 8 Sept 2026 |
| **Bug Fixes** |  |
| Partially sanitized archives silently dropped when Only Copy Remediated Files is enabled | Fixed an issue where an archive that MetaDefender Core could only partially sanitize was treated as if it had not been sanitized at all, so it was silently dropped instead of copied when a workflow's File Handling settings for Blocked Files used Copy to Secondary Location with Only Copy Remediated Files enabled. |
| Kiosk 4.8.5.9268 |  |
| **Release date** | 31 August 2026 |
| **New Features** |  |
| Advanced Device Threat Attack Detection | Kiosk can now detect hardware- and firmware-level device attacks that traditional file scanning cannot see — including BadUSB-style device impersonation, keystroke-injection tools (e.g. Rubber Ducky), rogue network-adapter emulation, autorun-based threats, and USB Killer power-surge attacks (USB Killer detection only available on forthcoming hardware models Kiosk Tower 6 and Kiosk Desktop 5). These attacks bypass antivirus entirely because they exploit the USB hardware itself rather than a file, making them one of the hardest classes of physical-access threats to catch. This gives administrators a critical new detection layer, extending Kiosk's protection beyond file-based scanning to the device layer itself. |
| Dedicated Integration Workflow for Connected OPSWAT Products (IFW, MD Drive) | Kiosk now supports a dedicated, product-specific workflow for connected OPSWAT hardware such as the Industrial Firewall (IFW) and MD Drive. When a supported device is connected, Kiosk authenticates the user and launches the product's own configuration screen, exchanging configuration, reports, and file transfers with Central Management (CM10) through a workflow designed to extend to future product integrations. |
| Pre-Upgrade Health Check for Hardened-Image Upgrades | The Kiosk Console can now run an on-demand pre-upgrade check that validates conditions such as Core/CM connectivity, active scan sessions, available disk space, and BitLocker status before an upgrade proceeds, and shows an expected-downtime notice when the upgrade starts — helping administrators catch problems before they cause a failed or disruptive upgrade. |
| BeyondTrust Password Safe Integration for Console Login and Exit Password | Administrators can now back Kiosk Console login and the Kiosk UI exit password with BeyondTrust Password Safe-managed Active Directory credentials, so the account password is fetched and rotated automatically instead of being stored statically. |
| Network and System Diagnostics Tool | A new Diagnostics tab in the Kiosk Console lets administrators run a comprehensive set of checks covering connectivity (Core, MFT, My OPSWAT, AD, SSO, SMTP, Syslog), network configuration, Kiosk services, system resources, licensing, scanning engines, certificates, and hardware/BIOS, with packet capture and one-click remediation actions such as restarting services or clearing temporary files. |
| **Enhancement** |  |
| Exclude Individual Policy Settings from Central Management Sync | Administrators can now exclude specific settings — HTTPS/certificate, Proxy, Processing workflow manifest, and Retrieve Files workflow manifest — from Central Management (CM10) group policy sync on a per-instance basis, so an instance can keep its own individual certificate or configuration instead of being overwritten by the group's shared value. |
| More Accurate Scan Time Estimates (AI-Based ETA) | The remaining-time estimate shown during a scan is now produced by an AI-based prediction model that accounts for file size, type, media, and hardware characteristics, in place of the previous static calculation — giving a more accurate, stage-aware estimate that continues to refine as the scan progresses. |
| Scan Multiple Devices in One Session | Administrators can enable a multi-media session mode so that, after completing a scan, a user can choose "Scan another device" and continue directly to the next device without re-authenticating or re-answering pre-scan questions. The authenticated identity and answers carry over automatically, while each device still produces its own independent scan report. |
| Automatic Deep Network Diagnostics on Connection Failure | When Kiosk detects a network connection failure, it can automatically capture a deep network diagnostic report to help identify the cause, without waiting for an administrator to run one manually. Administrators can turn this on or off from Settings > Network > Advanced. |
| Manage Kiosk Autologon/RDP Password from Central Management (CM10) | Administrators can now set and rotate the Windows autologon password used by Hardened-Image Kiosk devices — the same account used for RDP access — centrally from a My OPSWAT Central Management (CM10) policy or at the individual device level, instead of only locally on each Kiosk. |
| Partition Details in Secondary Scan Reports | The secondary scan report for multi-partition disk images, including VHD/VHDX, VMDK, TIB, Clonezilla, and LVM, now shows a partition summary, the count of scanned and unscanned partitions, and includes the partition name in each file's path. |
| Italian and Traditional Chinese Language Support | The Kiosk interface now supports Italian and Traditional Chinese, including a QWERTY on-screen keyboard layout for Italian, extending localization for Italian- and Traditional-Chinese-speaking deployments. |
| Intermittent License Validation and Remote Deployment Deactivation | Online Kiosk instances periodically re-validate their license so status changes are detected without waiting for a restart, and a Deployment ID disabled in My OPSWAT can remotely deactivate the corresponding Kiosk instance. |
| Expanded Encrypted USB Device Support (WD My Passport) | Kiosk now supports WD My Passport utility-enabled encrypted hard devices secured, allowing it to be detected, unlocked, and scanned the same way as other supported encrypted USB devices. |
| **Bug Fixes** |  |
| RFID/passwordless kiosk login could lock the user's Active Directory account | Fixed an issue where an RFID or other passwordless kiosk login automatically attempted a Managed File Transfer (MFT) username/password login on every session, even though no password exists for that identity. The repeated failed attempts could accumulate against MFT's brute-force protection and lock the user's Active Directory account after a few ordinary kiosk visits. Kiosk now skips the automatic login attempt when no password is available for the session. |
| Intermittent file upload failures from RFID/passwordless kiosk sessions to MFT | Fixed an issue where Kiosk sent an ambiguous Active Directory account name as the sender identity for Managed File Transfer (MFT) group-transfer uploads from RFID or other passwordless kiosk sessions, which MFT could sometimes match to more than one account and reject with an intermittent "on/off" failure. Kiosk now sends the same resolved unique identity used by other login types. |
| Kiosk fails to detect VIASAT Eclypt encrypted drive on K3 devices | Fixed an issue where Kiosk could not detect or display the partitions of a VIASAT Eclypt hardware-encrypted USB drive on K3 (Kiosk 3000) hardware, preventing the device from being unlocked and scanned. |
| Windows Event log fills with Kiosk errors referencing omsPACENTER.exe | Fixed an issue where a mismatched 32-bit dependency bundled with the 64-bit Post Action Center helper caused it to fail to launch, so Kiosk's watchdog repeatedly logged relaunch errors to the Windows Event Log roughly every 10 seconds and the post-action-script feature was silently disabled. |
| Copy/upload to MFT server failed with no error reason shown | Fixed an issue where a failed file transfer to a Managed File Transfer (MFT) server showed only a generic "Failed to Copy/Move to MFT" message with no explanation, because a logging defect discarded the actual reason returned by MFT. Kiosk now surfaces the underlying reason, including guidance to contact the MFT administrator when the transfer is rejected due to MFT's own upload configuration. |
| **Known Issues** |  |
| Encrypted Drive Unlock Failure for Standard (Non-Admin) Windows Users (WD My Passport) | When running MetaDefender Kiosk under a standard (non-admin) Windows user session, unlocking utility-enabled WD My Passport encrypted drives fails even when entering the correct password. Operating the Kiosk within an administrative Windows user session is currently required to successfully unlock and access these encrypted drives |
| Kiosk fails to detect VIASAT Eclypt encrypted drive on K3 devices | When a VIASAT Eclypt hardware-encrypted USB drive is connected to a K3 (Kiosk 3000) unit, Kiosk fails to detect the device during new-drive detection, so its partitions never become visible and the encrypted data partition cannot be unlocked or scanned. |

## 4.8.4

| Kiosk 4.8.4.8500 - 6 August 2026 | |
| --- | --- |
| **Bug fixes** |  |
| Kiosk shows "Connection to MetaDefender has been interrupted" error during scanning | Resolved a regression introduced in 4.8.4 where Kiosk incorrectly displayed a "Connection to MetaDefender has been interrupted" error popup during scanning which caused by the unreadable files (locked) even though Core was active and healthy. The fix ensuring unreadable files are gracefully skipped instead of triggering false connection-loss alerts. |
| Kiosk 4.8.4.8437 - 4 August 2026 | |
| **Bug fixes** |  |
| Kiosk failed to connect over self-signed or non-CA HTTPS even when Verify SSL Certificate is disabled | Fixed an issue where the Verify SSL Certificate setting was not applied to Kiosk's outbound connections, so certificate verification was always enforced even when the option was disabled. As a result, HTTPS connections to Core, Central Management (CM10), and MFT servers that use self-signed or non-CA certificates were rejected, causing scans and other operations to fail. |
| Duplicated upgrade history records for a single application upgrade via CM10 | Fixed an issue where multiple upgrade history records were created for a single completed application upgrade performed through Central Management (CM10) |
| Unable to save an Encrypted USB profile when another profile is already imported | Fixed an issue where saving an Encrypted USB profile failed with a missing signature error when another profile had already been imported |
| Custom screensaver falls back to default after a group policy update | Fixed an issue where a custom screensaver reverted to the default after applying a group policy of an older version. |
| Kiosk 4.8.4.8406 - 30 July 2026 | |
| **New Features** |  |
| Restore Configuration from a Backup File During Setup | The Out-of-Box Experience (OOBE) can now restore configuration from a backup file during setup. This enables faster manual deployment. |
| Import Configuration from a USB Drive During Setup | Administrators can now browse and inject an INI configuration file from a USB drive as part of the OOBE for auto deployment. |
| Automatic Power-On When AC Power Returns (Wake-on-AC) | Administrators can now enable Wake-on-AC on supported Kiosk hardware so the device powers on automatically when AC power is restored, without pressing the physical power button. |
| View Detailed Engine Status on the Kiosk Screen | Users can now view detailed Engine status by interacting with the engine status icon on the Kiosk UI, improving operational monitoring, and troubleshooting. |
| Show User Details from Active Directory in the Kiosk UI | After login, the Kiosk GUI can display one or more configurable Active Directory attributes (for example, display name) to review and clarify the logged in user account. |
| Kiosk Hardened Image Upgrade Notification in the Kiosk Console | A notification in the Admin UI can be enabled to prompt for the upgrade, increasing awareness of the automated upgrade utility and reducing confusion around the upgrade process, including hardened image upgrades. |
| **Enhancement** |  |
| File Retrieval from MFT with a Local Windows Account | File Retrieval from an MFT server is now available when logging in to the Kiosk UI with a local Windows account, extending support beyond Active Directory accounts. |
| Consistent Unlock Behavior for DL4 Encrypted Devices | The unlock flow for DL4 hardware-keypad encrypted devices is now unified with the flow used by other encrypted devices, improving maintainability and preventing DL4 devices from being misidentified as standard CD-ROM media. |
| Wipe Destination Media Before Retrieving Files | When File Retrieval from an MFT server is enabled, administrators can now configure the destination media to be wiped before retrieved files are written, providing an additional layer of data control. |
| Key Combination Whitelist Moved Under Active Keyboard Filter | The "Allow the following key combinations" option is now a subtask of the Active Keyboard Filter, since the setting is only relevant when the Active Keyboard Filter is enabled. |
| Full File Paths for Blocked and Password-Protected Files in Reports | Scan reports now include the full file path for password-protected and blocklisted files within archives, not only for infected files, improving traceability and investigation. |
| Turkish Language Support | The Kiosk interface now supports Turkish, extending localization for Turkish-speaking users and environments. |
| Stable Memory Usage When Scanning Large Volumes of Data | Improved memory management to enhance stability and reliability when scanning large volumes of data, resulting in more consistent performance, better system responsiveness, and a smoother scanning experience. |
| Keep Folder Attributes When Copying | Folder attributes are now retained during copy operations. When copying a folder, its associated attributes are preserved in the destination rather than being lost during folder creation. |
| Support Excluding Email Recipients from CM10 Policies | Administrators can now exclude email recipients from the CM10 group policy, allowing customized email delivery for specific user groups. |
| Predefined MFT Account Now Available in the Guest Workflow | The predefined MFT account (admin-configured) option for copying to a secondary location is now available in the Guest workflow, extending functionality previously limited to the Employee workflow. |
| Option to Skip Media Processing | Administrators can now configure Kiosk to skip media processing and immediately end the scan session. This option is particularly useful when used with the Media Passport feature to quickly generate exempted Media Passports without performing a media scan. |
| Configurable and Transparent Telemetry Settings | Kiosk now always shows the telemetry settings (enabled, disabled, or greyed out) after installation and upgrade for transparency, and the settings can be configured through VPACK at the instance and group level for centralized control across Kiosk devices. |
| Enhanced Kiosk Upgrade in Air-Gapped Environments | Enhance support to upgrade Kiosk in the air-gapped environment where it could not reach Certificate Revocation List (CRL) for validation. |
| **Bug Fixes** |  |
| Files with "%" in the name not shown when retrieving from a network share | Fixed an issue where the Kiosk UI failed to list files from a Windows (SMB) network share in the Retrieve Files feature when a filename contained the "%" character. |
| Self-scan schedule set to an unexpected date after cancelling a scan | Fixed an issue where cancelling a self-scan job and re-saving the Self-Scan Schedule page caused the next scheduled scan to be set to an unexpected date and time. |
| Workflow matching failed for AD groups with special characters | Fixed an issue where workflow-to-AD-group matching failed for groups whose names contained LDAP-escaped characters (such as a leading "#"), causing affected users to fall back to the Default workflow instead of their assigned one. |
| Password prompt showed the wrong file for infected, encrypted archives | Fixed an issue where the Kiosk UI prompted for the password of the parent archive instead of the encrypted file inside when the archive contained an infected, encrypted file. |
| **Known Issues** | |
| Total Files Scanned Shows Incorrectly When Scanning Encrypted Disk Image | When scanning an encrypted VHDX disk image with the "Scan full VHDX" option enabled, the Total Files Scanned count in the processing log is reported incorrectly. The kiosk does not prompt for the encryption password and miscounts the files within the encrypted container. |
| Skipped Files Are Recorded to the Printout | When scanning a disk image with skip options enabled (e.g., Skip processing locked system files, Skip protected OS files, Skip hidden files), the skipped files still appear in the printed scan report. |

## 4.8.3

| Kiosk 4.8.3.7906 - 26 June 2026 |  |
| --- | --- |
| **New Features** |  |
| Support SSO Smartcard Authentication with Certificate-based Sign-in. | Users can now authenticate at the Kiosk using a smartcard which enables certificate-based sign-in for SSO authentication (such as Microsoft EntraID). This strengthens identity assurance for high-security environments that mandate hardware-based credentials. |
| Support Running The Kiosk UI under Standard User Accounts | The Kiosk UI can now run under a standard Windows user account instead of an administrator, reducing the attack surface and aligning deployments with least-privilege security policies. Administrators can optionally configure a separate admin account for tasks that require elevated privileges. |
| Encrypted USB Profile Capture Tool | Kiosk now includes a utility tool that allows administrators to capture the unlocking process of encrypted USB devices not natively supported by Kiosk. The captured profile can then be exported as a JSON file and imported into Kiosk, enabling it to recognize and unlock these devices automatically. This makes it easy to extend encrypted USB support and replicate configurations across multiple Kiosk deployments. |
| Execute Remote Script Execution from Central Management (CM10) | Central Management (CM10) can now support remotely triggering script execution commands on managed Kiosk devices, enabling centralized automation and maintenance without physical access to each Kiosk. |
| Dedicated Kiosk Hardened Image Upgrade Option in CM10 | Kiosk hardened image upgrades through Central Management (CM10) have been enhanced with a dedicated upgrade option, making it easier to manage and roll out image updates across individual devices or groups. Providing a more streamlined and intuitive upgrade management. |
| Telemetry for Product Improvement | A new telemetry capability collects operational and usage data to help OPSWAT continuously improve product quality and performance. This feature can be disabled at any time if preferred. |
| **Enhancement** |  |
| SSO Group-Based Kiosk Workflow Assignment | Administrators can now assign Kiosk workflows based on SSO group membership, enabling group-driven access, processing rules, and routing without configuring each user individually. |
| Enhanced SSO authentication in Management Console to support OIDC | Extending the existing SSO support in Management Console, Kiosk now also supports OIDC-based single sign-on, giving administrators more flexibility to centralize authentication and manage the user lifecycle through their organization's preferred identity platform. |
| Custom Logo for Media Passport & Session Logs | Administrators can now display a custom organization logo on the Media Passport and Session log, allowing these reports to be branded consistently with corporate identity for a more professional appearance. |
| Support Managed File Transfer (MFT) Browsing | Administrators can enable Managed File Transfer (MFT) browsing when uploading files through the Kiosk, streamlining secure file submission without leaving the Kiosk interface. |
| Support Variables in Custom Command-Line Scripts | Administrators can now pass variables and the end user's "User Question" response (%%%%) into custom command-line post-actions. |
| Pre-Configured Passwords for Original Encrypted Destination USBs | Administrators can pre-configure passwords for encrypted both original and destination USB drives, so file retrieval and write-back proceed automatically without prompting the end user to unlock the device manually. |
| Enhanced Offline Activation Instructions | The offline activation instructions exported to USB are now a professionally formatted PDF with a 5-step visual guide, embedded portal screenshots, deployment IDs, and OPSWAT branding, replacing the previous plain-text file for a clearer activation experience. |
| Enhance Back Button to Insert Media Screen | The back button has been enhanced to allow users to return to the insert media screen, making it easy to reinsert or swap media without restarting the entire session. This improves the experience when a drive is removed early or needs to be replaced with a different one. |
| Support scan LVM partitions in Acronis TIB disk images. | The Kiosk can now mount and scan LVM (Logical Volume Manager) partitions storing in Acronis TIB disk images, extending backup-image scanning coverage to a wider range of source media. |
| Improved Skipped File Reporting | Scan results in the Kiosk UI and logs now provide more detailed information about skipped files. This gives operators clearer visibility into scan outcomes and makes it easier to troubleshoot why specific files were not processed. |
| BitLocker-Encrypted USB Unlock with Recovery Key | Extend the existing support of BitLocker, the Kiosk can now unlock and scan BitLocker-encrypted USB drives using a provided recovery key. |
| System Resource Optimization for Large File Scans | Memory consumption has been optimized to improve stability when handling large scans, reducing the risk of resource exhaustion and unexpected failures during high-volume sessions. |
| Improved Paging Performance | Improved paging performance when displaying large scan sessions or long lists of application logs, resulting in faster load times and a more responsive experience |
| Improved Mobile Device Scanning | Improved performance when scanning files transferred from mobile devices such as phones and tablets, delivering faster and more efficient processing within the Kiosk workflow. |
| Display DHCP or Static IP in Device Info screen | The Device Information in Kiosk UI now shows whether the Kiosk's IP address is assigned via DHCP or statically configured. |
| Removed Legacy Microsoft Visual C++ Redistributable | Legacy Microsoft Visual C++ Redistributable have been evaluated and removed from the Kiosk installer, eliminating outdated dependencies that are no longer required for installation. Kiosk application now only uses Microsoft Visual C++ 2015-2022 Redistributable |
| Security Enhancements | Various security issues have been addressed to enhance the overall security of the system |
| Improved CloneZilla Disk Image Scan result | Improved scan result classification for CloneZilla disk image folders. Unmountable disk images scan results are now accurately classified as Blocked, ensuring more reliable scan outcomes. |
| Improved Email RFC Compliance | Kiosk-generated SMTP emails are now RFC-compliant with proper headers, sender/recipient formatting, and encoding for non-English content, preventing mail servers from rejecting or silently dropping messages. |
| **Bug Fixes** |  |
| Fixed Kiosk service crash when scanning virtual disk files containing non-ASCII filenames | Resolved an issue where the Kiosk service could restart unexpectedly while scanning virtual disk files (VHD/VHDX), particularly those containing non-ASCII filenames on non-English system locales. |
| Fixed blank SSO login screen when network is unavailable at startup | Resolved a race condition where the Kiosk showed a blank SSO authentication screen if the service started before the network was ready. |
| Fixed missing numeric keys on the Vietnamese on-screen keyboard | Resolved an issue where the Vietnamese on-screen keyboard did not expose number and symbol keys. |

## 4.8.2

| MetaDefender Kiosk 4.8.2 |  |
| --- | --- |
| **9 July 2026** (Kiosk 4.8.2.8007) |  |
| **Bug fixes** |  |
| Fix Kiosk unenroll during sleep/suspend cycle | Fixed an issue where Kiosk could automatically unenroll from Central Management after the device wakes from sleep or suspend. Kiosk now preserves enrollment state through sleep/suspend cycles, preventing devices from re-registering as new instances. |
| **20 Jun 2026** (Kiosk 4.8.2.7850) |  |
| **Enhancement** |  |
| Enhanced Internal Communication and Improved Resilience Against External Factors | Enhanced the internal communication between Kiosk components, ensuring more reliable and consistent behavior across system operations. It also strengthens resilience against external factors, avoiding issues where HTTPS configuration not being retained properly, and license-related errors |
| **5 Jun 2026 (Kiosk 4.8.2.7615)** |  |
| **Enhancement** |  |
| Security enhancements | Various security issues have been addressed to enhance the overall security of the system |
| **26 May 2026** (Kiosk 4.8.2.7413) |  |
| **Enhancement** |  |
| Enhance Kiosk-to-CM connection resilience under poor network conditions | Improve the reliability and responsiveness of the Kiosk's communication with Central Management (CM) when operating in degraded network environments (packet loss, high latency, half-open connections, slow TLS handshakes). |
| **Bug fixes** |  |
| Fixed Kiosk service crash on non-ASCII filenames | Resolved an issue where scanning files with non-ASCII characters in their filenames (e.g Japanese, Korean) caused the Kiosk service to crash. |
| Fixed the configuration restore issue after upgrading from 4.7.9 | Fixed an issue where upgrading from Kiosk 4.7.9 failed to restore configuration |
| **13 May 2026** (Kiosk 4.8.2.6758) |  |
| **Enhancement** |  |
| Support Data Locker Sentry 5 software version 7.1.x | Kiosk now support Data Locker Sentry 5 with a newer software version 7.1.x |
| **Bug fixes** |  |
| Resolve Intermittent My OPSWAT Enrollment Failure on Kiosk Upgrade | Fixed an issue where Kiosk with auto export log enabled intermittently hung during My OPSWAT enrollment after image upgrade, caused by duplicate records are stored in database. |
| Resolve Kiosk Service Restart Issue When Inheriting Newer Policy Version | Fixed an issue where the version of Kiosk instances with version 4.8.1 restarted continuously after inheriting a 4.8.2 policy in My OPSWAT Central Management. |
| **7 May 2026** (Kiosk 4.8.2.6718) |  |
| **New Features** |  |
| Single-Page Media Passport for Scanned Sessions | A new single-page Media Passport view provides security personnel with a consolidated summary of each scan session, including safe/unsafe status, session metadata, and file statistics. The layout is designed for quick review without requiring navigation across multiple screens or reports.  Additionally, MetaDefender Drive can also leverage this feature to automatically generate a one-page passport with high level information. |
| Independent Media Type Permissions for Processing, File Retrieval or use as secondary media | Administrators can now configure separate media type permissions for file processing, use as secondary media and file retrieval on a per-workflow basis. For example, a workflow can permit USB drives for processing only, SD cards for both processing and retrieval, and optical media for retrieval only. |
| Key Combination Whitelist for Anti-Tamper Hardening | Administrators can now define a whitelist of physical keyboard key combinations that Anti-Tamper Hardening will allow. This is particularly relevant for non-US keyboard layouts to type special characters without reducing the overall hardening posture. |
| Proxy Server Configuration in Kiosk Console | Administrator can now configure proxy settings directly from the Kiosk console. This simplifies network configuration in environments with restricted or managed outbound access. |
| Kiosk application upgrade rollback from Central Management (CM10) | Central Management (CM10) can now remotely trigger application rollback on Kiosk devices. This release also includes improvements to upgrade and rollback status reporting, enhanced log traceability, and resolution of issues identified during integration testing. |
| **Enhancements** |  |
| Streamlined Default Workflow Settings for New Installations | New Kiosk installations are now pre-configured with simplified default workflow settings, reducing the number of steps required during initial setup. Administrators can complete deployment faster without needing to manually configure standard options from scratch. |
| Support for Kingston DataTraveler Locker+ G3 Encrypted USB | Add support for Kingston DataTraveler Locker+ G3 hardware-encrypted USB drives |
| Support Swiss Frenc, Estonian and Russian On-Screen Keyboard | Swiss French (CH), Estonian (ET) and Russian (RU) keyboard layouts have been added to the Kiosk on-screen keyboard, supporting authentication for users whose credentials include locale-specific characters not available on standard layouts. |
| Enforce authentication with RFID card only | Administrators can now enforce the user authentication with RFID card only. Only users will a valid RFID badge will allow to scan media with the Kiosk devices. |
| Send scan report to specific email address | In the Employee workflow, administrator can configure to allow the end user to send the scan reports to certain email address. Combining with Active Directory setting enabled, Kiosk will automatically show the list of users as recipients. |
| Custom File Naming for Scan Reports | Administrators can now define custom naming patterns for session scan reports files. This enables consistent naming conventions across sessions and simplifies report organization, archival, and retrieval. |
| MBR Partition supports in CloneZilla Disk Imaging | Disk image processing via CloneZilla now supports MBR (Master Boot Record) partition alongside GPT. This extends compatibility to a broader range of storage media, including legacy devices that use older partitioning formats. |
| XFS filesystem support in VMDK disk images | The Kiosk can now mount and scan XFS-formatted partitions inside VMDK virtual disk images — unlocking seamless support for Linux-based media and expanding compatibility with a wider range of customer environments. |
| Post-Scan Media Wipe option | MetaDefender Kiosk can now be configured to allow wiping the source media after the process completed. |
| Auto file retrieval after the scan process completes | Administrator can now configure the Kiosk to automatically retrieve files from a specific network folder after the scan process completes. |
| Support Variables in Email Notification Subject | Administrators can now include variables, such as session ID, scan result, and username, in email notification subject lines. This allows recipients to assess notification priority and context without opening the message body. |
| USB Protocol Version Display During Scanning | The Kiosk UI now displays the USB protocol version, such as USB 2.0, 3.0, or 3.2 when a drive is connected. This assists users and administrators in identifying the USB version and correlating it with observed scan performance. |
| Improved Restore Console Setting Clarity | A dedicated "Kiosk Settings and Workflows" checkbox has been introduced in Kiosk restore page to improve the clarity. |
| Support sending to Entra ID SSO email address | Kiosk now allows administrator to configure sending email to Entra ID SSO user email addresses. This enables automatic delivery of scan reports to the logged-in user without requiring manual address input. |
| Security enhancements | Various enhancements have been applied to improve the overall security of the system |
| **Bug Fixes** |  |
| Kiosk fails to load on hardened image | Resolved a rare issue where the Kiosk could become unresponsive during startup after running for several days on a hardened system. The application now recovers gracefully, ensuring reliable, uninterrupted operation. |
| Disk not detected after upgrading to 4.8.1 | Fixed an issue where certain external hard disks were not recognized properly after an upgrade, appearing only as unreadable boot sectors. All supported disk types are now detected reliably right out of the box. |

## 4.8.1

| MetaDefender Kiosk 4.8.1 |  |
| --- | --- |
| **9 April 2026** (Kiosk 4.8.1.6440) |  |
| Fixed issue where copied files did not appear when media included an EFI system partition. | Fixed an issue where Kiosk could intermittently copy files to an EFI system partition instead of the intended user-data partition on multi‑partition media, making the copied files not appear in normal user views. Kiosk now ensures the files are copied to user-data-partitions. |
| Security enhancements | Various security issues have been addressed to enhance the overall security of the system |
| **25 March 2026** (Kiosk 4.8.1.6216) |  |
| Resolved Kiosk application upgrade via My OPSWAT | Resolved issues when upgrading Kiosk application via My OPSWAT:   - The upgrade may fail due to issue with Ngnix process is being used for other purposes. - When upgrading via My OPSWAT On-Prem over HTTPS, Kiosk may fail to download the installer. |
| **19 March 2026** (Kiosk 4.8.1.6194) |  |
| **New Features** |  |
| Encrypt USB with BitLocker when retrieving files | When files are retrieved to external USB media, Administrator can configure Kiosk to automatically encrypt the target USB device with BitLocker. This helps ensure that exported data remains protected when removed from the Kiosk environment. |
| Support local Kiosk user accounts for media scanning | Kiosk now supports local Kiosk user accounts. Administrators can create or import users directly in the Kiosk management console, and those accounts can then be used to sign in on the Kiosk UI for media scanning. This allows environments without Active Directory integration to control which individual users are allowed to operate the Kiosk while still keeping a clear audit trail of who performed each scan. |
| Kiosk supports cloning existing workflows | Administrators can now quickly clone an existing workflow instead of creating a new one from scratch. This makes it easier to roll out variations of a proven configuration (for different sites or user groups) while keeping settings consistent and reducing configuration errors. |
| Disable Kiosk scanning when AV definition is outdated | When configured, Kiosk can now prevent new scans from starting when the underlying AV definitions are too old, helping ensure that scans are performed only with up-to-date protection. Administrators can use this behavior to enforce security best practices. |
| Support change Loading Logo via Customize Theme | Kiosk now allows customization of the loading logo through the theme configuration. This enhancement enables organizations to better align Kiosk visuals with corporate branding. |
| Pre-defined suggestion for email input when sending to specific recipients | The email dialog has been improved to make sending reports faster and less error‑prone. Kiosk now supports predefined email addresses and domains, so users receive automatic suggestions and can simply click to complete the address. In addition, reports can now be sent to multiple recipients in a single action, improving usability for teams and shared distribution lists. |
| Retrieve Kiosk support package via My OPSWAT (CM10) | Administrators can now remotely collect and download Kiosk support packages directly from OPSWAT Central Management 10. This simplifies troubleshooting and reduces the need for on-site manual log collection. |
| **Enhancement** |  |
| Show extracted archive details while scanning | When Kiosk scans archive files, the result view now provides clearer details about extracted content, including the number of files and their status. This gives administrators and users better visibility into what was actually scanned inside each archive. |
| Display toolbar icons when Welcome screen is disabled | When the Welcome screen is disabled, toolbar icons are now still displayed as expected. This ensures consistent access to key functions regardless of the chosen startup configuration. |
| Configure custom screensaver remotely via MyOPSWAT | Administrators can now configure and deploy a custom Kiosk screen saver remotely from My OPSWAT. This enables consistent branding across distributed Kiosks without requiring manual on-site updates. |
| Back button to re-select the workflow | Kiosk now provides a Back option that allows users to reselect the desired workflow without restarting the entire process. This improves usability for environments with multiple workflows and reduces user error when an incorrect workflow is chosen. |
| Support DataLocker H350 encrypted USB drive | Kiosk now supports the DataLocker H350 encrypted USB drive, including device recognition and secure access during scanning and file transfer workflows. This expands coverage for customers standardizing on DataLocker hardware. |
| Enhance Auto Upgrade of Kiosk application | The automatic upgrade capability for the Kiosk application has been enhanced. Including bug fixes and adds support for upgrading from a folder source, providing more flexibility for controlled or offline environments. |
| Improved "Invalid Core Setup" messages for troubleshooting | When Kiosk detects an invalid MetaDefender Core configuration, it now displays more detailed troubleshooting information to help administrators quickly identify and correct misconfiguration issues. |
| Exclude default language setting in My OPSWAT group policy settings | The default language configuration is now excluded from My OPSWAT group policy settings, reducing the risk of unintentionally overriding language preferences when applying or updating the group policy |
| Improved media detection stability | Kiosk now includes multiple enhancements to ensure reliable media detection:   - Improved detection reliability for removable media with multiple partitions, including standard FAT12/16/32 volumes. - Improved handling of Windows auto‑mount to reduce cases where media is not detected on first insertion. - Adjusted device mounting and retry logic to better handle slow or delayed volume initialization. - Improved stability of media event handling to avoid long‑running operations blocking new device detection. - Improved integration with MDDrive to prevent sessions from hanging and requiring a full kiosk reboot. - Enhanced iPhone scan handling to improve behavior when a device disconnects during scanning. - Improved robustness of media detection to reduce cases where users must restart the Kiosk application or reboot the OS. |
| Fixed Bugs |  |
| Resolved MD Drive integration issue when Welcome screen is disabled | Fixed an issue where MetaDefender Drive integration could stop working if the Kiosk Welcome screen was disabled. With this fix, MD Drive workflows operate correctly regardless of whether the Welcome screen is enabled or disabled. |
| Fixed failback to primary MetaDefender Core when it becomes available | Addressed a problem where Kiosk continued sending scans to the secondary MetaDefender Core even after the primary Core became available again. The Kiosk now automatically fails back to the primary Core once it is online, without requiring a manual settings update. |
| Corrected “Full Media Scanned/Processed” indicators for USB full scans | Fixed an issue where scan reports incorrectly showed Full Media Scanned: NO and Full Media Processed: NO even when users performed a full scan of USB media. The full‑media status flags now accurately reflect when USB devices have been fully scanned and processed. |
| **Known issues** |  |
| Incorrect scan status for Virtual Disk contents | When a USB with a virtual disk is processed using “Process All,” the report still shows that files inside the virtual disk were not fully scanned. |
| Kiosk fails to copy files from DataLocker DL4 to DataLocker H350 | Kiosk will fail to copy files from DataLocker DL4 device to DataLocker H350 device. |
| MD Drive unexpectedly ejected after initial enablement | MD Drive is ejected unexpectedly without user interaction shortly after the feature is enabled for the first time. |
| MD Drive is detected as a normal USB after the Kiosk install or upgrade. | Following a fresh installation or upgrade from a previous version, the Kiosk may detect the MD Drive as a normal USB device instead of the expected integrated MD Drive.  **Workaround:** Reboot the Kiosk to get the integration working normally again. |

## 4.8.0

| **MetaDefender Kiosk 4.8.0** |  |
| --- | --- |
| **2 February 2026** (Kiosk 4.8.0.5836) |  |
| **Fixed Bugs** |  |
| Fixed issue when Kiosk workflows do not sync all CN attributes of users | Resolved an issue where adding users in Kiosk workflows whose Distinguished Name (DN) contained multiple CN attributes resulted in the Kiosk creating the user with only two CN attributes. |
| Fixed intermittent setup Wizard display after Kiosk upgrade from Kiosk 4.7.0 | Resolved an intermittent issue where the Kiosk console displayed the setup wizard after upgrading from Kiosk 4.7.0 to a newer version |
| Fixed issue with CD/DVD detection | Resolved an issue when CD/DVD sometimes could not be detected. |
| **27 January 2026** (Kiosk 4.8.0.5807) |  |
| **New Features** |  |
| Protection against BadUSB and malicious USB Devices | Kiosk now detects and blocks BadUSB, malicious devices, and other non–mass‑storage USB interfaces, helping protect against attacks that emulate keyboards, inject keystrokes, or create covert network connections. This enhancement strengthens device security by preventing unauthorized USB behavior before it can compromise the system. |
| Support Kiosk application upgrade | Kiosk now supports remotely upgrading Kiosk applications through direct Kiosk Console or via Central Management. Administrators can schedule upgrades, monitor progress, and roll back if needed, removing the need for manual on‑site updates. |
| Option to disable displaying the Welcome Screen | Administrators can now configure Kiosk to skip displaying the Welcome screen and go straight to the media detection prompt, streamlining the user flow in environments where the initial screen is unnecessary. |
| Support for RFID and AD Login via OPSWAT CM10 | Kiosk now supports authentication through CM10, allowing users to sign in using both RFID cards and Active Directory credentials. This enhancement improves access‑control flexibility and supports environments that require integrated RFID and AD authentication flows. |
| Kiosk supports scheduled shutdown and startup | Kiosk now supports scheduled shutdown and startup of the device, enabling automated power management for deployments that require predefined power cycles. |
| Retrieve files from Onedrive and Sharepoint | Kiosk now supports retrieving files from OneDrive and SharePoint using Entra ID, allowing users to browse and select files directly in the Kiosk UI for file retrieval. |
| Kiosk OOBE supports activation and deployment engine offline [Kiosk Hardened Image] | Kiosk OOBE now supports offline activation for both Kiosk and Core licenses, enabling administrators to complete the full setup in air‑gapped environments. This enhancement ensures smoother deployment in highly restricted or isolated networks, and administrators can also update engines offline as part of the setup process. |
| **Enhancement** |  |
| Option to exclude original files from the manifest when a sanitized version exists | Kiosk provides a new option allows administrators to exclude original files from the manifest, ensuring only sanitized versions are shown to users. When enabled, original files are automatically blocked if a sanitized copy exists. This enhancement improves safety and streamlines access to sanitized files on USB devices. |
| Use specific user to copy files to network locations | Kiosk now supports using a specific domain account to copy files to network locations, providing more flexible access control while retaining fallback to the OS logged‑in user when needed. |
| Real‑time file counting during file selection and scanning | Kiosk now displays a real‑time counter during file‑counting phases, showing the number of files detected as scanning progresses. This improvement provides clearer feedback and prevents confusion when scanning large directories. |
| Show only enabled source options when copy or retrieve files | Kiosk now allows to display only the source options that are enabled and properly configured, hiding all unavailable options for a cleaner and more intuitive user interface. |
| Configure file-size calculation per workflow | Administrators can now configure file‑size calculation settings per workflow directly in the Kiosk UI, replacing the previous global‑only configuration and offering more flexibility across different workflows. |
| Retrieve remediated files of allowed files only | Kiosk introduces a new option to only retrieve remediated version of the allowed files. Preventing retrieving sanitized or DLP-processed files when the original files were blocked. |
| Last modified date for blocked files | Kiosk now displays the last modified date for blocked files, helping administrators identify whether a file was altered between scan sessions. The implementation ensures accurate timestamps, resolves earlier translation issues |
| Added total scanned file size to logs and reports | Kiosk now includes the total scanned file size in both the session log and the scan report, providing clearer visibility into the overall data volume processed during each scan. |
| Print layout enhancements and paper size support | The print layout for Kiosk reports has been improved in Kiosk 4.8.0, providing a cleaner and more readable output in different paper size. |
| Media Detection Enhancements | Kiosk includes several enhancements to media detection, improving the speed, accuracy, and reliability of identifying across different media types. Deliver a smoother, more consistent user experience during the scanning process |
| Kiosk support Predictive AI engine | Kiosk confirms supporting the Predictive AI engine, enabling advanced file analysis and faster threat detection. This AI‑driven enhancement improves scanning accuracy and strengthens overall security. |
| Improved detection for VMDKs with multiple filesystems | Scanning for VMDK files with multiple filesystems has been improved to ensure all valid partitions are detected. The system now checks for inaccessible partitions and automatically switches to VHDX conversion when needed, preventing cases where only the UEFI partition was mounted. |
| Improved detection for Acronis TIBX backup files | Support for Acronis TIBX backups has been improved with more reliable mounting for both disk‑level and file‑level backups. Compatibility was enhanced across multiple Acronis versions, though numeric‑only filenames may still fail due to a known Acronis bug. |
| Update MetaDefender Drive engines from Kiosk UI | Kiosk now supports updating the MetaDefender Drive engine directly from the Kiosk UI using MyOPSWAT as the update source, providing a more flexible and streamlined update process. |
| USB Device information sent to My OPSWAT | Kiosk now sends full USB device information to My OPSWAT, improving visibility and reporting on USB usage across deployments. |
| Include new version of Paragon Linux File System for Windows (version 6.1.300) | Kiosk now includes an updated Paragon Linux File System for Windows (version 6.1.300), improving VHDX detection and mounting reliability |
| **Fixed Bugs** |  |
| Fixed issue with file transfer from mobile devices to MFT | Fixed an issue where file transfers from mobile devices (iOS and Android) to MFT via Kiosk would hang during scanning, causing sessions to stall and the UI to become unresponsive. The update ensures reliable detection and transfer of files from connected phones, preventing endless loading states and UI freezes. |
| Fixed issue with Kiosk 4.7.10 configuration reverting to OCMv7 defaults | Fixed an issue where the configurations on Kiosk 4.7.10 reverted to the OCMv7 default instead of retaining the configured value on Kiosk, ensuring the setting now synchronizes correctly across Guest and Employee workflows. |
| Fixed issue with Windows Services reverting to Manual Startup | Fixed an issue where certain Windows services were incorrectly changed from Automatic to Manual startup during Kiosk installation or upgrade. |
| **Known issues** |  |
| BadUSB detection popup not displaying when Kiosk interface timeout is disabled | When the kiosk interface timeout is disabled (User Timeout = 0 minutes), the BadUSB detection popup may not appear |
| Encrypted USB not detected in some rare case | In rare cases, an encrypted USB devicemay mistakenly detected as CD/DVD and only detected the boot sector. Reconnecting the device is required to proceed |
| Screensaver video preview not playing | When configuring the screensaver, the video preview may not play after selecting a file. However, the settings are saved successfully, and the screensaver functions correctly on the Kiosk UI. |
| Partitions in BitLocker-encrypted USB may not mount in some rare case | In rare cases, partitions on a BitLocker‑encrypted USB device may not mount. |

## 4.7.11

| MetaDefender Kiosk 4.7.11 |  |
| --- | --- |
| **5 December 2025** (Kiosk 4.7.11.5065) |  |
| **New Features** |  |
| Enhanced license activation and renewal | Kiosk now automatically renews licenses when services restart, reducing downtime and manual intervention. Administrators can also activate both Kiosk and Core licenses directly from the Kiosk UI, improving flexibility and user experience. |
| GPG file decryption support | Kiosk now introduces advanced support for decrypting GPG-encrypted documents and files using provided private keys. Files are automatically decrypted, scanned for threats, and processed without manual intervention. Ensuring security, compliance, and efficiency for sensitive data handling. |
| Support LVM Image Disk scanning | Kiosk now supports scanning LVM disk images, enabling deep security analysis of files and directories within LVM volumes without requiring conversion to other formats. This enhancement improves coverage for Linux-based storage and simplifies workflows for customers handling LVM images |
| File integrity verification when sending files to Core | Kiosk now supports has verification to ensure file integrity when sending files to Core for scanning. Files with mismatched hashes are automatically blocked and reported. |
| Question responses synchronization with MFT | Kiosk introduce a new option to enable synchronization of Kiosk questions and responses with MFT. When enabled, Kiosk sends user responses, allowing MFT to classify files based on the user response data. |
| Media manifest support for File Retrieval | Kiosk now supports generating a media manifest when retrieving files, enhancing the integration with other solutions such as MetaDefender Endpoint. |
| Delete files after retrieval from local or shared network directories | Kiosk now supports an option to delete files after retrieval from local or shared network directories, helping better maintain storage and streamline workflows by automatically removing files once they are successfully retrieved. |
| Support password attempt limitation | Kiosk now supports configurable limits on wrong password attempts when scanning encrypted documents or archives. This feature enhances security and user experience by allowing administrators to set maximum attempts and display warnings during the process. |
| Manage and deploy kiosk HTTPS certificates via central management | Kiosk now supports certificate configurations via My OPSWAT, including option to enable HTTPS. This enhancement enables centralized control of certificates, improving security and consistency across deployments. |
| Download Kiosk scan reports from My OPSWAT | Kiosk now supports automatic syncing of scan reports to My OPSWAT, allowing customers to download results in PDF, JSON, or TXT formats. Users can enable or disable report syncing, with an option to sync only when blocked files are |
| Detailed logs for ISO image scans | Kiosk now supports generating detailed logs for ISO image scans. Separate logs are stored in the Kiosk logs folder, improving visibility and troubleshooting during scanning sessions. |
| Exclude Core API from My OPSWAT group settings | Kiosk policies on My OPSWAT now allow administrators to exclude MetaDefender Core API values from being updated during group configuration pushes. This enhancement improves flexibility and security, enabling different kiosks to use unique API keys without risk of overwriting the setting. |
| Custom MFT folder names based on user input | Kiosk now supports naming the destination folder in MFT based on user input provided during the initial scan questions. After scanning, files are uploaded to MFT under a folder named according to the user’s response, replacing default session-based naming. This enhancement improves organization, traceability, and aligns with customer workflows. |
| **Enhancements** |  |
| Enhanced Copy Results Display | Kiosk UI now shows detailed copy results, including the number of files successfully copied and those that failed. This improvement provides better visibility and transparency during file transfer operations. |
| Improved media detection stability | Kiosk now includes multiple enhancements to ensure reliable media detection:   - Fine-tuned waiting time for detecting media partitions. - Verified Paragon service runs during detection. - Ensure notifications for hidden or unmounted partitions. |
| Enhanced syslog messages for Kiosk application upgrade process | Kiosk now sends application upgrade indicators to syslog, including events for upgrade, uninstall, backup success/failure, and upgrade failure. This enhancement improves visibility and monitoring of upgrade operations |
| Enhanced details of blocked file information in My OPSWA | Kiosk reports sent to My OPSWAT now include comprehensive details of all blocked files, including specific block reasons, hash lookups, and relevant metadata. The updated format ensures accurate and transparent reporting across dashboards and workflows. |
| Enhanced SCSI USB device unmounting | Kiosk now provides a faster and more reliable unmounting process for SCSI USB devices, reducing delays. Improvements include optimized handling for devices with multiple partitions, resolution of SSD eject issues, and better user experience during long unmount operations. These enhancements ensure smoother workflows for forensic and secure scanning environments. |
| Support Datalocker DL4 FE encrypted USB drive | Added support for Datalocker DL4 FE encrypted USB drive |
| My OPSWAT policy compatibility across Kiosk versions | Kiosk now supports backward and forward compatibility for policies across versions (4.7.9 or later). This enhancement allows multiple Kiosk versions to be added to a single My OPSWAT Kiosk policy while ensuring consistent policy application across different versions. |
| Improved progress feedback during scanning | Kiosk now displays real-time scanning progress for better clarity during large number of scans. Calculations were optimized to ensure accurate progress to improve the user experience. |
| Enhanced error messaging during Kiosk configuration | Enhancement to provide clear, informative error messages that pinpoint invalid or missing fields, helping users quickly identify and resolve issues. This improvement ensures a smoother configuration experience and reduces troubleshooting time. |
| **Bugs** |  |
| Fixed “Undefined” scan result for TIBX files | Resolved an issue where Kiosk incorrectly returned “Undefined” scan results for TIBX files instead of the correct verdict. The update ensures accurate result handling and improves reliability for disk image scans. |
| Fixed VMDK lock file (.lck) clean up issue | Resolved an issue where .lck files were not deleted after processing VMDK files. The fix ensures proper cleanup after session completion or scan cancellation |
| Fixed unable to mount large Clonezilla image issue | Resolved an issue where large CloneZilla images were not mounted properly. The logic has been updated to allow sufficient time for automatic drive letter detection, ensuring proper mounting and complete full scanning of all files in the CloneZilla images |
| **Known issues** |  |
| Size limitation of archive report in email attachment | When attaching archive reports as a ZIP file to session emails, files larger than 25 MB cannot be sent due to email size limitations. |

##

## 4.7.10

| MetaDefender Kiosk 4.7.10 |  |
| --- | --- |
| **14 October 2025** (Kiosk 4.7.10.4551) |  |
| **New Features** |  |
| Smartcard (PIV) authentication now supported on Kiosk | Kiosk now supports Smartcard (PIV) authentication, based on the FIPS 201 standard, ensuring secure and standards-compliant user access. |
| Single & Multiple Choice Support for User Questions | Kiosk now supports single and multiple-choice answers for user questions, allowing administrators to configure flexible input options for improved user validation and data collection. |
| Kiosk supports scanning Ivanti encrypted USBs | Kiosk now supports scanning media encrypted by Ivanti Device Control software, allowing administrators to manage and secure encrypted USB devices across both connected and air-gapped environments. |
| **Enhancements** |  |
| Enhanced Login page for Kiosk Management Console | The login page of Kiosk Management Console has been redesigned to improve usability and ensure a consistency user experience aligned with other OPSWAT products |
| Support remote install and upgrade via Microsoft SCCM | Kiosk can now be installed and upgraded remotely using Microsoft SCCM, enabling easier deployment and management for administrators. |
| Auto-deploy Kiosk with shared Core via .INI in Out-of-Box Experience | Kiosk now supports shared Core configuration through the .INI file during OOBE auto-deployment, allowing administrators to deploy a single Core instance shared across multiple Kiosks. |
| Kiosk supports integrations with MetaDefender Cluster | Kiosk now supports integration with MetaDefender Cluster, enabling scalable, distributed file scanning and centralized management for high-volume environments. |
| Improve UI of file copy progress | Enhanced file copy progress now includes a percentage bar, file count, and elapsed time. Providing clearer, more informative feedback to end users. |
| Enhance messaging during Network Share Permission checks | Kiosk now improves message display during network share permission checks, including a live timer to show elapsed time. These enhancements provide clearer user feedback and streamline the file retrieval experience. |
| Improved file retrieval in Kiosk UI | Kiosk now displays the total file count at the start of retrieval and removes background from file names during waiting, improving user clarity. |
| Kiosk enhanced Kingston encrypted USBs which configured different languages | Kiosk now supports detecting and unlocking the below Kingston encrypted USBs regardless of the device's language setting. This ensures seamless functionality across all supported UI languages. List of Kingston encrypted USBs supporting multiple languages:   - DataTraveler DTVP30 - DataTraveler DTVP30M - Iron Key D300S |
| Geolocation reporting for Kiosk devices in CM10 | Administrators can now enable geolocation reporting from KIOSK devices to OPSWAT Central Management (CM10), enhancing visibility and improving device management capabilities. |
| Support for Greenhouse PicoDrive Secure GH-UF3SRxG encrypted USB | Kiosk now supports Greenhouse PicoDrive Secure GH-UF3SRxG encrypted USB |
| Show the Redacted Hits in the KIOSK UI | Kiosk now enhances result visibility when sensitive information is detected by the Proactive DLP engine, allowing administrators to view specific scan results for better data oversight |
| Password Handling for Encrypted Files During MFT Retrieval | Kiosk now prompts users to enter passwords for encrypted archives or protected documents during MFT/Directory file retrieval, enabling secure decryption and continued processing via Core. Users can also pre-load passwords to streamline scanning and ensure allowed files are copied as per the standard workflow. |
| Flexible MFT file retrieval options | Administrators can now configure KIOSK to either retrieve all files or select specific files during MFT file retrieval, offering greater control and flexibility in data handling. |
| Improved scan result display of skipped files when scanning for Disk Image Files (VHD/VHDX) in KIOSK | Kiosk now marks disk image files (VHD/VHDX) as "partially scanned" or "skipped" if any child files are unreadable or skipped, improving scan result accuracy and transparency |
| Kiosk session logs include total of allowed and blocked files | Kiosk session logs now include totals for allowed and blocked files, making it easier for administrators to quickly assess scan results and take appropriate actions |
| Kiosk now uses CRLF line ending in email body | Kiosk now uses CRLF line endings throughout the email body to meet strict email security requirements, ensuring reliable delivery across various mail servers and configurations |
| Support for long path scan reporting in Virtual Disk Fiels | Kiosk now correctly generates scan reports for virtual disk image files with long file paths, ensuring accurate parent and child file reporting |
| Enhanced Pre-translation for Kiosk UI text messages | Kiosk UI now improve pre-translation text messages coverage across multiple languages, enhancing localization accuracy and delivering a better user experience for global deployments. |
| Reorder icons in menu bar customization | Reorder the icons in the customize menu bar, making it easier for administrators to locate and configure key functions efficiently |
| Enhanced disk space validation for Kiosk Hardened Image Upgrades [Kiosk Hardened Image] | Kiosk Hardened Image now includes improved disk space validation to prevent upgrade failures caused by insufficient space in the Recovery (RE) partition. This ensures reliable snapshot creation and avoids rollback issues during auto-upgrade |
| Enhanced media detection reliability | Increased Paragon’s media detection timeout to prevent missed detections when partitions take longer to mount. |
| Improved RTL display for user questions in KIOSK | Kiosk now ensures proper right-to-left (RTL) formatting for user question responses when Hebrew and Arabic languages are used, enhancing readability and localization accuracy. |
| **Bugs** |  |
| Fix for Datalocker Sentry 5 FIPS encrypted USB unlocking in KIOSK UI | This version resolved a bug where Datalocker Sentry 5 FIPS USB devices failed to unlock in KIOSK mode due to timeout issues. The new version of Kiosk ensures stable unlocking behavior in various network environments. |
| Fix for disclaimer language display issue after the Kiosk Hardened Image upgrade | Kiosk now correctly displays disclaimers in the selected language after upgrades, resolving a bug where only the default language appeared despite valid language files. |
| **Known issues** |  |
| Scan results of Proactive DLP not shown for archive child files | Kiosk does not display Proactive DLP scan result if the detected file is inside archive files. |
| Kiosk cannot mount Clonezilla if it is stored in a long folder name | Clonezilla fails to mount image folders when the folder name exceeds 255 characters due to filesystem limitations. |

## 4.7.9

| **MetaDefender Kiosk 4.7.9** |  |
| --- | --- |
| **29 August 2025 (Kiosk 4.7.9.4298)** |  |
| **New Features** |  |
| Import and export language packs | Kiosk now supports importing and importing translated language packs, making it easier to back up and reuse custom translations across Kiosk devices. |
| Support for NFC authentication (PC/SC mode) | Kiosk now supports NFC cards (PC/SC Mode) as a login method. Users can simply swipe their NFC card, and Kiosk will automatically authenticate the card ID with Active Directory to grant access. |
| Check device information on Kiosk UI | Administrators can now enable an option to display device information. End users can view system details directly, which can be helpful when working with administrators for troubleshooting |
| Options to skip protected system, hidden files and folder | Kiosk introduces two new options to skip processing certain files and folders, providing administrators more control on Kiosk scanning processes.   - Skip protected operating system files: Skips files and folders with 'S' (System file) attribute - Skip hidden files and folders: Skips files and folders with 'H' (Hidden file) attribute |
| Password entry timeout for encrypted files | Administrator can now configure a timeout for password entry on encrypted files. When the time limit is exceeded, the encrypted files will be automatically blocked, ensures unattended encrypted files don’t stay pending. |
| Windows login automatically start Kiosk scan session | Kiosk now supports a new login option “login with Windows authentication” for scan sessions. When enabled, users can log in with their Active Directory account or by swiping their smart card to access Windows. The Kiosk will then automatically log in with the same account to start the scanning session. |
| Kiosk UI supports Exit, Shutdown and Restart | Administrators can now enable to display control buttons for Exit, Shutdown, and Restart directly on the Kiosk device. |
| **Enhancements** |  |
| Support Sony XDCam drive | Add support for Sony XDCam drive |
| Support ELECOM (MF-PUVT3xxGA3 and MF-ENU3) and Datalocker Sentry 5 FIPS encrypted USB devices | Add support for ELECOM (MF-PUVT3xxGA3 and MF-ENU3) and Datalocker Sentry 5 FIPS encrypted USB devices |
| Security enhancements | Addressed a security issue in the Kiosk UI embedded console to enhance the overall security of the system |
| Support YubiKey Smart Card | Add support for YubiKey Smart card |
| Refined Kiosk Hardened Image upgrade settings layout [[Kiosk Hardened Image 25.08.0]] | In Kiosk Hardened Image upgrade, separated upgrade source and upgrade schedule settings to improve clarity and make configuration more intuitive. |
| Pop up warning for upgrade restrictions [Kiosk Hardened Image 25.08.0] | A popup message has been added to inform users of upgrade limitations before starting the upgrade, ensuring they are aware of restrictions in advance |
| Improved workflow navigation in Kiosk UI | When the number of workflows exceeds the available display space, the Kiosk interface now shows arrow buttons to indicate additional workflows are available for navigation |
| Improve message for permission checks when retrieving files | A loading indicator with the message “Checking access permissions for network share...” is now displayed during permission checks in the Retrieve File operation. This improves user feedback and prevents confusion while access validation is in progress. |
| Improve file count display when start retrieving files | The Kiosk now improves the display during large file retrievals from network shares. The total file count is displayed at the start of the retrieval process |
| Toast notification for core connection | When Kiosk integrates with multiple Core instances, a toast message is now displayed to indicate which Core the Kiosk is currently connecting to |
| **Bugs** |  |
| Resolved issue with Eclypt drive detection | Resolved an issue where the Kiosk failed to detect and unlock Eclypt devices |
| **Known issues** |  |
| The toast message is overlapped | The toast message when connecting to primary and backup Core will be overlapped with menu icons on Kiosk Tower, Kiosk Mini and Kiosk Mobile screen. |
| Switching login option may not apply | When switching from “Login with Windows Authentication” option to “Windows user login” option, the change doesn’t apply |

## 4.7.8

| **MetaDefender Kiosk 4.7.8** |  |
| --- | --- |
| **28 July 2025**  **(Kiosk 4.7.8.4064)** |  |
| **New Features** |  |
| Support custom script during the OOBE auto-deployment  [Kiosk Hardened Image 25.07.1] | Out-of-Box Experience (OOBE) auto-deployment now supports running a custom script during the auto setup process. If a script is defined in the OOBE initialization file, the Kiosk will automatically trigger and execute the script during the deployment process. This allows additional customization and automation as part of the Out-of-Box Experience. |
| Configure Core tunning via Kiosk Console | Kiosk now supports applying MetaDefender Core tuning configurations directly from the Kiosk console. This includes settings of parallel scan counts and queue size, allowing easier performance optimization without needing direct access to Core. |
| **Enhancements** |  |
| Enhanced Auto-Upgrade process for Kiosk Hardened Image - Excluded engines, Host name  [Kiosk Hardened Image 25.07.1] | The auto-upgrade for Kiosk Hardened image has been improved for greater stability.   - Support for excluded Core engines: Backup and upgrade now support MetaDefender Core configurations with excluded engines. Previously, such configurations could cause the upgrade to roll back. - Fix for Hostname restoration: Resolved an issue where the hostname was not properly restored, which caused the Core deployment ID to change unexpectedly. |
| Hostname as device naming in Central Management | Kiosk now registers with Central Management (CM10) using its hostname as the device Name, instead of the Deployment ID. This change enhances clarity for users managing multiple Kiosk devices in CM. |
| Kiosk reports associated Core Deployment ID to Central Management | Kiosk now sends the Deployment ID of the connected MetaDefender Core to Central Management (CM) during enrollment. This enables accurate device correlation and seamless access to scan reports from CM. |
| Device ID now shown on About Page | The Kiosk Device ID (Deployment ID) is now displayed on the About page, making it easier to identify the device. Especially when managing multiple Kiosks through Central Management |
| **Bugs** |  |
| VMDK files failed to mount due to missing drivers (Kiosk 4.7.4 or newer) | Fixed an issue in Kiosk 4.7.4 or newer where VMDK files could not be process due to required drivers are not being included during the Kiosk installation. |
| **Known issues** |  |
| Black screen on domain login without local Admin rights | When the Kiosk is joined to a domain, logging in with an AD user account that is not a member of the local Administrators group will result in a black screen after login. Ensure that any domain account intended to log in and operate the Kiosk is added to the local Administrators group on the Kiosk device. |
|  |  |

## 4.7.7

| **MetaDefender Kiosk 4.7.7** |  |
| --- | --- |
| **11 July 2025** (Kiosk 4.7.7.3922) |  |
| **New Features** |  |
| Kiosk Hardened Image - Auto-deploy Kiosk Out-of-Box Experience for the initial setup | Kiosk now support initial configuration files to automate the Out-of-Box Experience (OOBE) enable faster deployment at large scale. |
| Allow trusted files by digital signature | Kiosk now allows administrators to configure trusted files based on their digital signatures. This feature enables more precise control by allowing only files signed with specified certificates. |
| File search for scanning | Kiosk now allows users to search for specific files to scan, making file selection faster and more convenient. |
| Fallback to logged-in Windows user when retrieve files from shared directories | Kiosk now supports a fallback mechanism that attempts to access shared directories using the currently logged-in Windows user when the provided Active Directory (AD) credentials fail. This enhancement improves file retrieval reliability in environments where AD access may be restricted or inconsistent. |
| Option to wait for MFT scan completion | Kiosk introduces a new option that allows it to wait until all uploaded files are successfully scanned by MFT before closing the session. At the end of the session, Kiosk will also display the MFT scan result of each file. |
| **Enhancements** |  |
| Supports scanning Clonezilla images | Kiosk now supports scanning Clonezilla images |
| Improved permission error messages during file copy | Kiosk now provides clearer messages when file copy fails due to permission issues at the destination. This enhancement helps streamline troubleshooting. |
| Enhanced security with encrypted certificates in Kiosk database | Certificates and private keys used for secure connections (HTTPS) and manifest signing are now encrypted and securely stored in the Kiosk database. This enhancement strengthens security by eliminating local certificate exposure and preventing unauthorized access. |
| Support applying configurations to multiple Kiosk versions in Central Management 10 | Kiosks instances are now capable of apply settings across mixed versions in Central Mangement 10. Kiosks with older versions skip unknown settings and retain deprecated settings to ensure consistent behavior and compatibility. **Note:** This feature requires Central Management 10, which is not yet released. |
| Improved error message for incorrect password in encrypted files | When users enter an incorrect password for encrypted files, the error message is now clearer to avoid confusion and help users understand the issue. |
| Removed ‘Finding files’ screen | The ‘Finding files’ screen has been removed to simplify the file scan process. |
| Enhanced display for mixed English and Hebrew text lines | Improved text rendering for lines containing both English and Hebrew |
| Show Time remaining for specific workflow | A new option has been added to allow displaying the estimated remaining time while processing files |
| Option to show or hide remaining time per workflow | A new option allows Kiosk to show or hide the estimated remaining time for each workflow while processing files, enhancing user visibility and experience. |
| Improved file listing for large USB devices with over 250 files | Improved the file listing experience for USB devices containing over 250 files. Users can now continuously scroll through the list for a smoother and intuitive experience. |
| Improved session ID tracking for file Scans in Central Mangement 10 | Kiosk now includes the session ID with every file sent to Core, enabling better reporting in Central Management 10. This change ensures consistent tracking across all scanned files. |
| Exclude Manifest files when transferring files to the MFT server | Kiosk no longer copies manifest files when transferring files to the MFT server. This change helps avoid confusion in cases where manifest file transfers fail, ensuring a clearer and more consistent file transfer experience. |
| Supports domains containing hyphens “-” when integrating with Microsoft Entra ID (OIDC) | Kiosk now supports domains containing hyphens “-” when integrating with Microsoft Entra ID using the OpenID Connect (OIDC) protocol. |
| Accurate file size display for files skipped due to size | When a file is skipped by MetaDefender Core due to its size, Kiosk now accurately displays the actual file size instead of showing 0 Bytes. This improvement provides clearer scan results. |
| Reduced repetitive showing of “Access denied” when using with Load Balancer | When using Kiosk with the Load Balancer option, Kiosk no longer repeatedly show “Access denied” message from MetaDefender Core. This improvement helps minimize noise in the Kiosk logs |
| Improve display of languages when being switched | Language switching on the Kiosk user interface and question screens has been enhanced to ensure accurately display the selected language. |
| Language selection now managed via menu bar icon | The “Allow user to select languages” option has been removed. Language selection is now controlled through the customizable menu bar icon for a simpler configuration. |
| **Bugs** |  |
| Resolved issue with missing translation text when upgrading to Kiosk 4.7.6 | Kiosk resolved issues where some language translation texts could disappear when upgrading from older versions to Kiosk 4.7.6 |
| Resolved self-scan did not triggered at the scheduled time | Kiosk resolved an issue where the Self-Scan feature did not automatically trigger at the scheduled time. |
| Resolved high CPU and fan noise caused by CD/DVD drive | Kiosk resolved an issue where the CD/DVD drive could cause unusually high CPU usage, resulting in increased fan noise |

## 4.7.6

| **MetaDefender Kiosk 4.7.6** |  |
| --- | --- |
| **14 June 2025** (Kiosk 4.7.6.3642) |  |
| Fixed Bugs |  |
| Fixed invalid Core setup and blank Core console page due to exhausted connections | Fixed an issue in Kiosk 4.7.6 where repeated checks of the embedded Core engine status may exhaust available connections in some cases. This caused the Kiosk to display an "Invalid Core Setup" message and the Core management console to appear blank. |
| Fixed Self-scan skipping all files when using Core 5.14.2 | Fixed an issue in Kiosk 4.7.6 where the Self-scan feature skipped all files when used with Core 5.14.2 |
| Fixed double printing in Automatic Print feature | Fixed an issue in Kiosk 4.7.6 where “Automatic Print” feature triggered printing twice instead of once. |
| Fixed MFT transfer failure over HTTPS | Fixed an issue where Kiosk failed to transfer files to MFT over HTTPS when SSL certificate verification was disabled. This affected Kiosk versions 4.7.5 and 4.7.6 |
| **23 May 2025** (Kiosk 4.7.6.3514) |  |
| New Features | Central Management now supports centralized importing of YARA rules and file hashes via REST API. Kiosk will seamlessly apply these items to the embedded Core engine, enabling streamlined, centralized policy enforcement across all connected Kiosk devices. |
| Flexible icon visibility controls | Administrators can now choose to hide interface icons entirely or tuck them under the dropdown menu (“…”). These new options give you finer control over the Kiosk UI and let you deliver a cleaner, more customized experience for end users. |
| Supervisor MFT approval bypass option | Kiosk introduces a new setting that allows administrators to bypass supervisor MFT approval directly from the Kiosk console. This provides greater flexibility for configuring diverse use cases and streamlining workflows. |
| Optional domain selection for active directory login | Kiosk now offers administrators the option to enable domain selection on the login screen when integrated with Active Directory. Enabling this feature displays a domain dropdown, helping users select the correct domain and simplifying the login experience. |
| Enhanced validation for predefined question responses | Administrators can now specify input formats for predefined questions, choosing from free text, number, email, or custom regular expressions (Regex). Users must enter data in the required format to proceed, improving data accuracy and consistency |
| New scanning engine status indicator | The Kiosk UI now displays a status indicator for scanning engines. If an engine encounters issues, a warning (exclamation mark) or critical (cross) icon will appear, signaling the severity. This enhancement improves user awareness and helps administrators quickly identify and address engine problems. |
| Kiosk supports integration with MetaDefender Drive | Kiosk now supports direct integration with MetaDefender Drive. When an MD Drive is connected, Kiosk automatically uploads stored scan reports to the enrolled Central Management, removing the need for separate SDK installation and configuration. |
| **Enhancements** |  |
| Enhanced media detection across all Kiosk processing screens | Kiosk now detects inserted media (e.g., USB drives) from any screen. When media is inserted, a popup notification confirms detection. If media is inserted while on the Welcome screen, Kiosk will automatically proceed to the User Agreement screen and begin the scanning process. On the Media Detection screen, the detected media is automatically selected for scanning, streamlining the user experience |
| Manage scanning engines from Central Management | Kiosk now supports managing scanning engines via My OPSWAT and OPSWAT Central Management, enabling easier configuration and consistent engine updates across multiple devices. |
| Option to disable SD Card scanning | Kiosk now provides the ability to disable SD card scanning. This allows administrators to tailor the interface for a cleaner, more streamlined user experience when SD card support is not required. |
| Improved display for Smart Card or RFID as primary login option | When Smart Card or RFID authentication is enabled, Kiosk will now display it as the default login method. Users can still switch to username and password login if preferred, providing flexibility while prioritizing secure access. |
| Additional client identifier is included when uploading files to MetaDefender Core and MFT | When uploading files to MetaDefender Core and MFT, Kiosk now sends additional client identifiers (hostname, Kiosk ID, username and timestamp) to Core and MFT. This improves My OPSWAT’s ability to correlate data and enhances traceability for each scanned file. |
| New ‘Scanning Configurations’ tab in Kiosk console | Kiosk now includes an additional **‘Scanning Configurations’** tab, enabling administrators to configure basic workflow settings directly within the Kiosk console. More advanced settings will be introduced in future releases to further enhance this feature. |
| Improved display during file scan initialization | In previous versions, Kiosk displayed “0 files found” while searching for files to process, which caused confusion for end users. This has been improved to show “Initializing...” during the search to provide clearer feedback. |
| Improved unsent scan report synchronization | Kiosk will now automatically synchronize any unsent scanning reports (for example, due to connectivity disruptions) to My OPSWAT once the connection is restored. Additionally, when a Kiosk instance is newly enrolled, any existing locally stored scan data will be sent to My OPSWAT, ensuring improved data consistency and completeness. |
| Enhanced “About” page with system details | The Kiosk “About” page has been enhanced to display additional details, including the Core version, hardened image version, hardware specifications, service tag, and more. This expanded view provides valuable information for support and troubleshooting, improving the overall customer experience. |
| Unified Kiosk About page in Central Management | The Kiosk About page in Central Management is now aligned with the version displayed on the Kiosk console, ensuring consistency and improving usability across platforms. |
| Improved CD/DVD scanning performance | Kiosk now optimized CD/DVD scanning to reduce scan time and enhance the overall user experience, ensuring faster and more efficient processing of optical media. |
| Support for manifest generation with Unicode characters in file names | Kiosk now fully supports generating manifest files containing Unicode characters in file names (e.g Japanese). By leveraging Unicode APIs and converting file names to UTF-16, Kiosk ensures reliable manifest creation across systems with different locale settings and code pages, enhancing compatibility and reducing encoding-related issues. |
| Revert customization settings to default | Kiosk now includes an option to revert customization settings, such as logo, color scheme, and other visual elements, back to their default values, making it easier to undo changes and restore the original appearance. |
| Secondary logo now displayed on session end screen | Kiosk now displays the secondary logo on the session end screen, aligning with branding customizations and improving visual consistency across the user experience. |
| Improved Hebrew translation in Kiosk UI | Kiosk UI improved Hebrew translations, providing a clearer and more accurate user experience for Hebrew-speaking users. |
| Enhanced support for simultaneous SharePoint and Entra ID (OIDC) integration | Kiosk now supports configuring SharePoint and Microsoft Entra ID (OIDC) simultaneously. Files are correctly transferred under the authenticated user’s credentials, ensuring accurate file handling across both MFT and SharePoint/OneDrive workflows. |
| Support for export and import of offline activated Core | Kiosk now supports exporting and importing configurations of MetaDefender Core instances that were activated offline or via volume license on Central Management. This will also allowed Kiosk Hardened Image to be upgraded with offline-activated Core |
| Enhance Kiosk Hardened Image Upgrade for greater stability and error handling | Enhanced Kiosk Hardened Image Upgrade with improved stability and bug fix. Critical failures (such as failed to backup Core license) during configuration restoration are now logged in the upgrade history, and ensure the system will automatically roll back to a stable state when needed |
| Security enhancements | Various security issues have been addressed to enhance the overall security of the system |
| **Bugs** |  |
| Resolved Error when saving Syslog settings | Resolved an issue that caused an “Error Saving” message when setting up a Syslog server in Kiosk. The problem was related to how log level settings were handled. With this fix, Syslog configuration now works as expected, regardless of the selected log level. |
| **Known issues** |  |
| Backup and restore fails with embedded Core using HTTPS certificate requiring passphrase | Kiosk cannot perform backup and restore when the embedded Core is configured to use HTTPS with a certificate that requires a passphrase. |
| Upgrade fails when Network Policy Hardening is enabled | When the Network Policy Hardening is enabled, certain network services are disabled as part of the security configuration. This prevents some components (such as firewall and network settings) from being backed up, causing the Kiosk upgrade process failed. |
| Self-scan skips all files | Self-scan feature in Kiosk 4.7.6 does not work as expected with Core 5.14.2. When initiated a self-scan, all files are skipped. |

## 4.7.5

| **MetaDefender Kiosk 4.7.5** |  |
| --- | --- |
| **10 April 2025** |  |
| **New Features** |  |
| Sending files to specific MFT users or email addresses via Kiosk | Kiosk now enables end users to send files directly to designated MFT recipients using their username or email address, streamlining the file transfer process. |
| Send processed file to MFT accounts without authentication required | Kiosk introduces a new option that allows administrators to configure the Kiosk to send processed files to MFT accounts without requiring prior user authentication |
| Enforce user-selected file classification for file scanning and storing | Kiosk introduces file classification tags prior to scanning, ensuring compliance with data categorization policies. Classified files are seamlessly transferred to MFT along with their metadata. |
| Kiosk supports OpenID Connect (OIDC) protocol for SSO and Entra ID | Kiosk now supports OpenID Connect (OIDC) protocol for Single Sign-On (SSO) and Entra ID. With this new support, Kiosk allows users to transfer files without pre-logging into MFT first. |
| Hardening option to disable Network-related services from Kiosk WebMC | Kiosk now supports OpenID Connect (OIDC) protocol for Single Sign-On (SSO) and Entra ID. With this new support, Kiosk allows users to transfer files without pre-logging into MFT first. |
| Kiosk supports tombstone files on removal | Administrators can enable tombstone files to replace blocked files from both source and destination, providing traceability of removals. |
| Manage Network Settings from Kiosk WebMC and My OSPWAT | KKiosk now allows administrators to manage network settings directly through the Kiosk WebMC and My OPSWAT (CM7 not supported). System IP addresses and related configurations can be easily modified within the WebMC interface. |
| Dedicated workflow for Self-scan | Kiosk supports a dedicated Self-Scan workflow, enables administrators to configure scanning settings more effectively for user-specific needs. |
| Option to display question responses during file scans | Administrators can configure Kiosk to display question responses during file scans for improved usability and context awareness. |
| Apply background image to all Kiosk UI screens | Kiosk now allows administrators to apply a custom background image across all Kiosk UI screens, providing greater flexibility and branding opportunities for user interface customization |
| Support Biocryptodisk ISPX Track encrypted USB | Added support for Biocryptodisk ISPX Track encrypted USB device |
| **Enhancements** |  |
| Improve USB detection time in Kiosk devices with floppy drive connected | UOptimized USB detection performance in environments where floppy disk drive is present. |
| Enhance Kiosk Hardened Image Upgrade for greater stability and UX/UI | Enhanced Kiosk Hardened Image Upgrade with improved stability, better UX/UI, and bug fixes |
| Kiosk UI displays network status | The network status is now displayed directly on the Kiosk UI for better management and support. |
| "Upgrade Now" and "Rollback" are supported in My OPSWAT | "Upgrade Now" and "Rollback" options are now supported in My OPSWAT, allowing administrators to manage software updates more efficiently |
| UI enhancement in Media Selection to avoid confusion | Improve Kiosk UI in Media Selection screen to prevent certain elements from appearing as buttons to avoid confusions |
| Disable timeout on Kiosk UI | Administrators can disable the timeout for Kiosk UI entirely, preventing session interruptions and improving user experience. |
| Include file size in scan history | Processed files in scan history includes a file size column for improved visibility and tracking |
| Improve handling of unmountable VMDK and TIB files | Improve handling VMDK and TIB files that cannot be mounted. Kiosk will now block these files to maintain security. |
| Security enhancements | Various security issues have been addressed to enhance the overall security of the system. |
| **Bugs** |  |
| Resolved incorrect file assignment for non-existence MFT Users | Fixed an issue where files uploaded to a non-existent MFT user were incorrectly assigned to the admin account instead of the Guest account. |
| Resolved Kiosk crash during email parsing | Fixed an issue where Kiosk could crash while parsing email content. |
| Resolved Unexpected Return to Setup Wizard | Fixed an issue where Kiosk could unexpectedly return to the initial setup wizard. |
| **Known issues** |  |
| Files are uploaded to MFT Guest ID when uploads fail | When uploading multiple files from Kiosk to MFT, failed uploads may be incorrectly redirected to the MFT Guest account and displayed to the user |
| Kiosk may become unresponsive when wiping encrypted IronKey S1000 USB | When wiping an encrypted IronKey S1000 USB drive, it may cause the Kiosk to become unresponsive |

## 4.7.4

| **MetaDefender Kiosk 4.7.4** |  |
| --- | --- |
| **7 March 2025** |  |
| **Fixed Bugs** |  |
| Fixed issue with black screen after upgrade in-place from an older version | Fixed an issue where Kiosk got stuck on a black screen after an in-place upgrade from an older version with the "Boot Hardening" feature enabled. |
| **21 February 2025** |  |
| **New Features** |  |
| Enhanced Kiosk UI customization | Administrators can now update the logo and background image directly from WebMC. Additionally, you can customize the background and text colors for a more tailored user experience. |
| Select Blocked Files for Removal | Kiosk introduces a new option that allows users to select specific blocked files for removal, providing more control and flexibility |
| Kiosk-Generated Manifest File for Improved File Control | Administrators can configure to generate the manifest file directly from Kiosk system. This manifest enhances control over which files are allowed or blocked before being uploaded to MetaDefender Core, ensuring better integration with MD Endpoint and MD Firewall. |
| Support OAuth Email Authentication for Microsoft 365 (Graph API) | Kiosk now supports OAuth authentication for email integration with Microsoft 365 (Graph API) |
| SSO Integration with OIDC Support | Kiosk now supports integration with SSO Identity Providers using the OIDC protocol, verified with Manage Engine SSO |
| Support retrieving file from MFT with SSO OIDC | Supports retrieving files from MFT (version 3.9.0.1 or later) when configuring with SSO OIDC |
| Manage Core configuration directly in Kiosk WebMC | Kiosk WebMC now supports direct management of MetaDefender Core configurations, including scanning engine status and updates. Additional Core configuration options will be introduced in future updates |
| Option to disable screensaver while scanning files | Kiosk introduces a new option that allows administrators to disable the screensaver while scanning files and reviewing scan result. |
| User Questions support Multi-Language | User questions now support multiple languages. When switching to a different language, the user questions will automatically update to match the selected language |
| **Enhancements** |  |
| Enhanced Auto-Upgrade for Kiosk Hardened Image | The auto-upgrade for Kiosk Hardened image has been improved for greater stability. This release also includes refined wording and visual enhancements for a better user experience. Administrators can now upgrade Kiosk Hardened Image via OCM. |
| Kiosk application supports Windows 11 | Kiosk application now supports Windows 11, ensuring compatibility and performance on the latest operating system |
| Session log file information is now recorded in the manifest generated by Kiosk | Information of Session log files is now recorded in the manifest generated by Kiosk, ensuring compatibility with OMVA when media containing session log files is used |
| Restructure layout of settings in Kiosk WebMC | Layout of settings have been restructured for a cleaner and more intuitive experience |
| Improved AD Login Format Support in Kiosk WebMC and UI | Kiosk WebMC and UI now support Active Directory login using multiple formats, including:   - Username - Domain\Username - Username@Domain   This enhancement provides greater flexibility for user authentication. |
| Eject and Exit Button Now Visible in Kiosk UI Settings Bar | The Eject and Exit button is now displayed in the Kiosk UI settings bar, providing users with a clearer and more accessible way to exit the interface. |
| Support for filenames with special characters in OneDrive file transfers | Enhance file transfer to OneDrive by adding support for filenames with special characters |
| **Bugs** |  |
| Fixed Deployment ID change not reflecting in Kiosk UI | Resolved an issue where the Deployment ID change did not update correctly in the Kiosk UI, causing license activation failures. The UI now correctly reflects the Deployment ID |
| Fixed configuration save issue after upgrade | Kiosk version 4.7.4 fixed an issue where data fields is missing after upgrading from an older version (such as 4.6.3) prevented the Guest workflow configuration from being saved. |

## 4.7.3

| **MetaDefender Kiosk 4.7.2** |  |
| --- | --- |
| **27 December 2024** |  |
| **New Features** |  |
| Auto Upgrade Kiosk Hardened Image | In MetaDefender Kiosk version 4.7.3, administrators can initiate the upgrade for Kiosk Hardened Image (version 25.01.0) directly from Kiosk WebMC. The upgrade process backs up essential system and product configurations, automatically downloads the latest version of Kiosk Hardened Image, and performs the upgrade. In case of failure, Kiosk would automatically revert to the previous version to ensure continuity. |
| Enable RDP (Remote Desktop Protocol) from Kiosk WebMC | Administrators can enable RDP (Remote Desktop Protocol) through Kiosk WebMC. Once enabled, Kiosk will modify the necessary services and settings. |
| Support for RFID card authentication | Kiosk now supports RFID card authentication. The user can register and associate a new RFID card with their AD account. |
| Support timezone for syslog messages | Administrators can now configure timezone when integrating with the syslog server. |
| Support for new encrypted USB Devices | Kiosk supports the following encrypted USB devices:   - DataLocker Sentry 3.0 - DataTraveler Vault Privacy 3.0 (DTVP30M-R) |
| Support MongoDB password during Kiosk installation | During the Kiosk installation process, administrator can set a password for the MongoDB database for encryption. |
| **Enhancements** |  |
| Improved Configuration Backup and Restore | Additional information included in Configuration Backup and Restore:   - Computer host name - Custom Kiosk sound file - Windows Security Certificates - Configurations of MetaDefender Core |
| Kiosk does not automatically end the session | After the scanning session is completed, Kiosk pauses on the final screen for user acknowledgement. |
| Improved information in Kiosk UI startup process | The initial process of starting the Kiosk UI has been broken down into smaller steps to provide more detailed information and improve troubleshooting. |
| Show the created date of files when selecting files | Kiosk UI now shows the creation date of files on the selection screen for files processing. |
| Kiosk instance remains enrolled in My OPSWAT | Once a Kiosk instance is enrolled in My OPSWAT, it remains enrolled indefinitely and will not unenroll automatically. It can only be unenrolled if an administrator manually deletes or unenrolls the instance |
| Support SCSI USB devices | The Kiosk now supports copying processed files to SCSI USB devices |
| Improve character counting accuracy for foreign languages | Improve the character counting method to ensure greater accuracy when enforcing character limits for some foreign languages which require the use of Input Method Editor (IME), for example, Hebrew |
| Security enhancements | Various security issues have been addressed to enhance the overall security of the system |

## 4.7.2

| MetaDefender Kiosk 4.7.2 |  |
| --- | --- |
| **04 November 2024** |  |
| Hidden MD Core Console from KIOSK UI | In this new KIOSK version, access to the MD Core Console has been disabled in the KIOSK UI to address certain security concerns. |
| **18 October 2024** |  |
| **New Features** |  |
| Support for Smartcard authentication | Kiosk now supports Smartcard for user authentication.  **Limitation:** Authentication for MFR file retrieval is not supported |
| Embedded Management Console within Kiosk UI for streamlined configuration | Administrators now can access and manage configurations directly from the Kiosk UI without exiting the application. A gear icon on the top right opens Kiosk Management Console for configuration. |
| Support copying processed files to SharePoint and OneDrive | Administrator now can configure the option to copy processed files to SharePoint or OneDrive directories. Before utilizing this feature, it is necessary to setup Microsoft Entra ID with API integration. If the destination path is left empty, Kiosk will automatically copy the files to the root folder. |
| Configuration backup and restore enhancement | This update includes additional configurations for backup and restore functionality. Administrators can choose the specific configurations to restore:   - Local Windows Certificates: Restore all trusted certificates from Certificate Microsoft Management Console (MMC) - System Hosts file: Restore the custom Hosts file at C:\Windows\System32\drivers\etc\hosts - License: Restore the activated Kiosk license - Branding and Logo Customization: Restore logo and branding files found in C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client\en\resources - Secure connection: Restore the security certificate and enable Secure Connection option - User management: Restore configured User Directories (AD, SSO and Entra ID) and accounts - Known Wi-Fi network: Restore the known Wi-Fi networks   (***Notes********* _**** __ ***** ***** *** _ __ : this feature is only available in Kiosk version 4.7.2 or later*) |
| Change logon password on Kiosk Hardened Image | Administrators can now change user logon password directly from Kiosk Management Console on Kiosk Hardened Image.  (***Notes:*** *This feature is only available on Kiosk Hardened Image. This settings cannot configured via My OPSWAT and the* *Set setting of OCM*) |
| **Enhancements** |  |
| Permission control on end user folders when copying files | When Kiosk is configured to copy processed files to a destination folder, the Administrator can choose to copy the files to the end user's folder with specific permissions.   - Inherited: Files and folders will inherit the same permissions as the parent folder - Restricted: Only the file owner will have the permissions to access the files and folders |
| Support on-screen French (AZERTY) keyboard layout | Kiosk now supports on-screen keyboard for French (AZERTY) layout. |
| Support on-screen Chinese (Traditional) layout | Kiosk now supports on-screen keyboard for Chinese (Traditional) layout. |
| Display file progress and results for file retrieval | Kiosk now shows the file scanning progress and results when retrieving files. |
| Hide on-screen keyboard with physical keyboard connected | When a physical keyboard is connected, Kiosk will automatically hide the on-screen keyboard. Administrators can click the keyboard icon on the top right corner to toggle the visibility of the on-screen keyboard. |
| Improve stability when generating Kiosk support package | Improve stability when generating Kiosk support package. |
| Improve stability of database when scanning files | Improved stability of database to avoid performance impact when scanning large volumes of files |
| Improve AD authentication mechanism to prevent user account lockout | In the previous versions, multiple failed sign-in attempts to the Kiosk UI could cause users to be locked out due to Active Directory policies. This new version enhances the AD authentication mechanism to prevent unnecessary fallback methods, reducing the risk of user account lockouts during login attempts. |
| Enhanced Self-scan on all drives | All drives in the system will be scanned when using Self-scan feature, including the boot sector. When malicious files are detected in the boot sector, Kiosk will lock the system and inform the Administrator. |
| Support more variables in Email Session Report template | Kiosk supports more variables in Email Session Report template:   - session_id: Kiosk session ID - start_time: Start time - end_time: Finish time - device_model: Media model - device_serial_number: Media serial number - device_media_type: Media type - device_id: Media ID - total_files_scanned: Total files were scanned - blocked_files: Number of files were blocked - allowed_files: Number of files were allowed - skipped_files: Number of files were skipped scanning - remediated_files: Number of files were remediated |
| Enable select files or process all files at workflow level | In the new version, Administrator can configure enable select files or process all on each individual workflow.   - Select files: User can select files for processing - Process all files: User has to process all files in the media - Select or process all files: User can select between ‘Select files’ or ‘Processing all files’ option - Disable file processing: Kiosk does not process file - Use Global Settings: Apply the Global Settings (under configurations > Kiosk UI > Choose Files Scanning Option) |
| Support unlocking encrypted USBs with passwords containing special characters | Kiosk supports unlocking encrypted USB devices with passwords containing special characters. |
| Enhanced visual appeal and engagement for Kiosk UI | Several components of the Kiosk UI have been updated with a modern design, enhancing visual appeal and user engagement. |
| **Known Issues** |  |
| Cannot apply Disclaimer via OCM or My OPSWAT Set settings | After applying a custom Disclaimer from the Set settings in OCM or My OPSWAT, the custom Disclaimer does not apply to instance within the Set. This will be addressed in the next version. |

## 4.7.1

| **MetaDefender Kiosk 4.7.1** |  |
| --- | --- |
| **24 September 2024** |  |
| **Enhancements** |  |
| Support burning files over 2GB to DVDs and Blue-rays | Users can now burn single or multiple files larger than 2GB to DVDs and Blu-rays, removing size limitations. |
| Enhance logging for troubleshooting | Logs have been enhanced to include additional information, providing more context and details for troubleshooting. |
| **Fixed Bugs** |  |
| Issue with entire email displayed in Bold text when Heading was used | Resolve the issue that caused entire body of email to appear in Bold text when Heading setting was used. Only intended section will now use bold format, ensuring accurate email presentation. |
| Issue with failing to create backup file | Resolved issue where Kiosk failed to generate backup files when large crashdump files were present, causing the backup process to fail. This fix excludes crashdump files from the backup, including only the necessary files to ensure a smooth backup and restore process. |
| Unable to modify AD settings when AD server is unreachable | After upgrading Kiosk, users were unable to modify Active Directory (AD) server settings if the AD server was not reachable. If the AD server is accessible, the settings can be changed without any issues. This fix ensures settings can be changed even when the AD server is unreachable. |
| Empty workflow page after importing configuration backup | Resolve issue when importing a configuration backup, the workflow page appeared empty due to certain fields not being included in the backup. This fix ensures that all necessary fields are automatically included when importing a backup. |
| Cannot enable Boot Hardening feature | Resolve issue where users were unable to enable Boot Hardening feature. After enabling the setting and refreshing the page, the setting reverted to being disabled. This fix ensures that the Boot Hardening setting remains enabled after being applied. |
| Kiosk UI became unresponsive when scanning large files containing numerous encrypted archive files | Kiosk UI became unresponsive when scanning large files containing numerous encrypted archive files. This fix optimizes the scanning process to improve stability and prevent the UI from becoming unresponsive when handling large files with many encrypted archives. |
| High memory consumption in Kiosk service during scan results display | The Kiosk service was consuming a high amount of memory when displaying scan results for a large number of files. This fix optimized memory usage when displaying large scan results. |
| Kiosk UI hangs when connection to Core is lost | Resolve issue where Kiosk UI would hang when the connection to the Core was lost. This fix ensures that the Kiosk UI automatically attempts to reconnect to the Core when the connection is lost, allowing it to resume file scanning. |
| Security enhancements | Various security issues have been addressed to enhance the overall security of the system. |
| **30 August 2024** |  |
| **New Features** |  |
| Screen Brightness Controls | Users can adjust screen brightness directly on the KIOSK UI, which is particularly useful for installations in low-light environments. |
| Display OS Name and IP Address | The OS name and IP address of the KIOSK are now displayed on the KIOSK console, making it easier to identify and manage the OS and network configuration of the device. |
| Support for new encrypted USB Devices | The KIOSK supports the following encrypted USB devices:   - USB DataTraveller DTVP30M-R - USB IronKey D300S - USB IronKey D500S |
| Session log storage on secondary media | Administrators can now configure the KIOSK to save session logs to secondary media during file copy operations. Previously, session logs were stored on the source USB only.  *(Note: Session logs are currently not included in the manifest file, so the USB will not be unblocked with OMVA. You can use MetaDefender Endpoint (Standalone) to access the files on the USB.)* |
| MFT Guest ID verification support | Administrators can now control Guest IDs rather than relying on automatic generation by the KIOSK. Before starting a scan using the Guest workflow, users must input pre-existing MFT Guest IDs generated on the Managed File Transfer (MFT) system. |
| Manifest storage configuration | Administrators can configure the KIOSK to store the manifest only on the secondary USB instead of both the source and secondary USBs, ensuring the integrity of the source USB data. |
| Log file size retention support | Enhanced logging control and optimized storage space by supporting log file size retention. |
| **Enhancements** |  |
| Windows Registry Interaction Update | To mitigate security risks flagged by some Endpoint Detection and Response (EDR) systems, functions previously relying on reg.exe to interact with the system registry have been updated to use the Windows API, improving system integrity and compliance with security standards. |
| Copy to Original DVD Support in Copy&Go | The KIOSK now supports copying clean data back to the original DVD during the Copy&Go process, addressing customer needs for this functionality. |
| Additional hash information in Manifest File | SHA-1 and MD5 hash values have been added to the manifest file, allowing customers to audit and query scan information more easily. |
| Support for double quote character in passwords | The KIOSK now allows the double quote character (") in passwords when adding certificates to the system. |
| Sanitized files list in KIOSK UI results | The KIOSK UI now shows a list of files that were sanitized, providing users with detailed scan results and a better understanding of why certain files were blocked or allowed. |
| Fallback Mechanisms for File Copy Operations | Implemented essential fallback mechanisms to handle exceptions during file copy operations to the secondary USB, ensuring more robust and reliable performance. |
| Watchdog Feature Improvement | Enhanced the Watchdog feature to ensure that the KIOSK does not restart after pressing the keyboard combination (ALT + S) when the "Reboot at the end of session" option is enabled. This improvement prevents unintended restarts and ensures a smoother user experience. |
| MFT Guest Code Visibility | Users can now configure the visibility of the MFT Guest Code in the KIOSK UI, allowing more time to record the code for easier file retrieval. |
| Security Enhancements | Various security issues have been addressed to enhance the overall security of the system. |
| **Fixed Bugs** |  |
| Issue with Custom Authentication Configuration on OCM7 | Resolved an issue where administrators were unable to edit the configuration of custom authentication on OCM7. This fix restores full control over authentication settings for administrators. |

## 4.7.0

| **MetaDefender Kiosk 4.7.0** |  |
| --- | --- |
| **09 August 2024** |  |
| Webpage loading on KIOSK Console | Optimized resources on the webpage to enhance the user experience. |
| **Fixed Bugs** |  |
| Issue with Certificate Configuration | Resolved issues related to configuring certificates on the KIOSK Console, making it easier for admins to manage certificates.  (**Note**: *From this version onwards, to enhance security, KIOSK will no longer support private keys using insecure DES encryption.*) |
| Issue with Configuring "Exit Credential" | This version addresses the issue where KIOSKs were unable to update the "Exit Credential" configuration from OCM/My OPSWAT through Set/Group settings. |
| **29 July 2024** |  |
| **New Features** |  |
| Innovate the KIOSK Web Management Console | The KIOSK Web Management Console has been totally revamped with a more streamlined and user-friendly design, making it easier than ever to configure your KIOSK. |
| Support Microsoft Entra ID Authentication on Kiosk UI and Web Management Console | Officially support to configure Microsoft Entra ID as new authentication method for both KIOSK UI and Console through the SAML 2.0 protocol. See [Microsoft Entra ID Integration](Microsoft Entra ID Integration) for more details. |
| Encrypted Drive Verification and Approval | The Kiosk system protection functionality will check file integrity in the unlocked partitions of encrypted peripheral media devices before decryption. The encrypted devices containing unauthorized data will be spotted and require approval before being added to the data whitelisting and usable with the Kiosk system. See [Encrypted Device Verification And Approval](Encrypted Device Verification And Approval) for more details. |
| Continuous support for My OPSWAT integration | The administrator can now centrally manage KIOSK(s) from My OPSWAT with the following additional product functionalities:   - Configuration - Workflows - Logs - Product license activation - Uploading custom disclaimer |
| Support UK keyboard layout | Users can now input UK characters from the Kiosk UI by using the UK keyboard. |
| **Enhancements** |  |
| Enhance stability and security of KIOSK application | Carry out database improvements and update third-party dependencies to the most recent stable version. |
| Enable searching through the KIOSK Console session history by submitting a large file | The user can now submit a file larger than 200MB to search for in the KIOSK Console session history. |
| Compatible support with the new version of CimTrak | Compatible support when integrating with CimTrak 4.1.41 |
| Improve the printing process | Eliminate KIOSK usage or creation of PowerShell script when utilizing the printer to align with the whitelisting service. |
| **Fixed Bugs** |  |
| Issue copying the remediated file after scanning | Fixed the issue cannot copy the remediated file that was downloaded from MD Core after scanning to a shared folder with Kiosk logged-in user permission |
| Issue when retrieving files from the network share | Ensure that the authorized AD user can retrieve files from a network share. |
| Issue when unlocking Kanguru Defender 3000 with the latest firmware | Enhance KIOSK compatibility when unlocking the encrypted USB Kanguru Defender 3000 with firmware version 5.6.7.0 |
| **Known Issues** |  |
| Issue wheIssue when upgrading in-place from older versionsn upgrading in-place from older versions | KIOSK has upgraded several 3rd party components in this version. Therefore, when upgrading from very old KIOSK versions, administrators should uninstall the current KIOSK version to clean up the system before reinstalling version 4.7.0. After reinstalling, configurations will be retained as they were before. |
| Issue with Custom Authentication on OCM7 | Administrators cannot edit the configuration of custom authentication on OCM7. This will be addressed in our next versions. |

## 4.6.8

| 4.6.8 |  |
| --- | --- |
| **16 May 2024** |  |
| **New Features** |  |
| Support for Trellix Encrypted USB | KIOSK can now decrypt and scan Trellix encrypted USB drives using a USB password. |
| Post-Scan Actions for files inside disk image files | After scanning, KIOSK can copy files from within disk image files to a network share/MFT/Media. Details here: [Processing virtual disk files](Processing virtual disk files) |
| Support for scanning nested Disk Image Files | The KIOSK functionality enables comprehensive deep scanning of disk image files by seamlessly mounting and scanning all nested files within, ensuring thorough analysis even in the presence of multiple layers of disk image files. |
| **Enhancements** |  |
| Enhanced Scan Limits setting for file extensions | Administrator can configure file extensions that users are not allowed to select for processing in the KIOSK UI. **Note:** Scan limits do not apply to the Simplified Workflow. |
| Improved UX for scanning disk image files | KIOSK now displays the scanning progress for files inside disk image files, and users can view detailed scan results for these files after scanning (via the KIOSK UI or session logs). |
| Improved application log for engines status | Detailed engines information and status are now shown in the application log when issues occur. |
| On-Screen Keyboard on KIOSK UI for ADFS Login | An on-screen keyboard is now available for login using ADFS on the KIOSK UI. |
| Enhanced Authentication with Nested AD Groups | KIOSK now more accurately authenticates users within nested AD groups. |
| Improved detection of external CD/DVD ROM | Users can scan CD/DVD after starting a session on KIOSK and connecting an external USB CD/DVD ROM. |

## 4.6.7

| **4.6.7** |  |
| --- | --- |
| **17 April 2024** |  |
| Memory Optimization | Addressed an issue where the KIOSK UI experienced excessive memory usage when scanning with a high number of threads. Optimizations have been applied to the memory management processes of KIOSK UI, specifically tailored to handle large-scale thread operations more efficiently. |
| **12 April 2024** |  |
| **Features** | **Descriptions** |
| Customizable Disclaimer Page | Administrators can customize the disclaimer page of the KIOSK user interface. Admins can create a custom disclaimer page using an HTML file and upload this custom page for the corresponding language. (**Note**: Currently, there is a limitation where customized disclaimer files cannot be applied to group instances from CM7.) |
| **Enhancements** |  |
| File Limit Settings | Implemented features to limit file size, total number of files, and total file size when users choose to copy files to a network shared drive without processing through Metadefender Core. (**Note**: These limits do not apply to retrieving files from MFT). |
| Disable USB Scan | Administrators can now disable the USB scan feature on the KIOSK UI. Administrators need to disable the "Allow user to browse for files" and "Allow user to process all files" options in the KIOSK console. In this case, users will only be able to perform other actions (such as: Retreive file from MFT) on the KIOSK UI. |
| Improved UX for Copying Files to CD/DVD | Enhanced user experience when copying files to CD/DVD. Currently, KIOSK does not support wipe for CD/DVD. If an administrator configures wipe before copying files to CD/DVD and a user attempts to copy files to a CD/DVD with existing data, KIOSK will display an error message and allow the user to change to another blank CD/DVD to copy files. |
| **Fixed Bugs** |  |
| MFT File Retrieval Issue | Fixed an issue where files could not be retrieved from MFT when the option "Do not process files with Metadefender or MFT server" was enabled. This issue has been resolved in this version. |
| Login Issue for Users in AD Groups with Hebrew Characters | Fixed an issue where users couldn't log in if they belonged to an Active Directory group with Hebrew characters in the group's common name. |
| **Known Issues** |  |
| The simplified workflow with the file size limitation | The simplified workflow is currently optimized to streamline user operations. So the limits related to file size/total file are not yet supported on the simplified workflow. |

## 4.6.6

| 4.6.6 |  |
| --- | --- |
| **26 March 2024** |  |
| Security Update | Improved security measures for the KIOSK Console to enhance overall system security. |
| **27 February 2024** |  |
| **Features** | **Descriptions** |
| Support for ADFS Authentication in KIOSK UI and Console | Admin can configure authentication for KIOSK (Console/UI) through the SAML protocol. [More info](More info) |
| Password Requirements Before Copying Files to USB | User can enter a password to encrypt files retrieved from MFT before copying them to the destination USB. |
| File Size Limitation for Scanning | Limit the size of files that users can select for scanning. Admins can configure the maximum size of files on the KIOSK/CM console that users are allowed to scan through KIOSK UI. |
| Total File Size Limitation | Limit the total size of files that users can select for scanning. Admins can configure the maximum size of the total files on the KIOSK/CM console that users are allowed to scan through KIOSK UI. |
| Total File Quantity Limitation | Limit the total number of files that users can select for scanning. Admins can configure the total file quantity on the KIOSK/CM console that users are authorized to scan through the KIOSK UI. |
| File Blocking by Extension | Supports users blocking files by file name extension. Admins can configure file extensions that they want to block on the KIOSK/CM console. KIOSK will block these file extensions without uploading them to MD Core server to get scanning results. |
| Display Incident Detections on CM Console | Supports users tracking incident detections on the CM Console. Admins can track incidents originating from KIOSK, users, or sessions. |
| Support for Encrypted USB Viasat UK Freedom 100 | Added support for encrypted USB Viasat UK Freedom 100. |
| Embedded Sandbox Engines in KIOSK | Supports scanning files with an embedded Sandbox engine in KIOSK. |
|  |  |
| **Enhancements** |  |
| Improved File Copy Speed | Improved file copy performance by increasing the number of threads copying files simultaneously. Admins can configure the thread count on the KIOSK/CM console. [More info](More info) |
|  |  |
| **Fixed Bugs** |  |
| Could not select files for scanning Issue | Fixed the issue where users could not select files for scanning when the "Email current user" option is enabled. |
| Issue with custom language configuration on KIOSK Console | Enhanced upgrade mechanism to ensure system configurations are updated correctly. |
| KIOSK UI Freezing | Addressed issue where KIOSK UI would occasionally freeze when performing tasks with encrypted USB. |
| Black Desktop Screen on Hardened Image | Fixed issue where the screen turns black after running KIOSK for a period of time on the hardened image. |
| CD/DVD Ejection Issue | Fixed issue where KIOSK would fail to perform tasks after users ejected CD/DVD while scanning with KIOSK. |
| Issue with Manifest File | Improved checks and handling for manifest files to ensure more accurate system operation with manifest files in the new version. |
| Unable to save user password at "Enter Vault server to upload files to" option | Fixed issue the users were unable to save their password after updating the password for "Enter Vault server to upload files to" previously. |
| Wipe Data on Bitlocker Drive | Fixed issue where users couldn't delete data on Bitlocker drive when wiping the drive with KIOSK. |
|  |  |

## 4.6.5

| **4.6.5 Hotfix**  **5 Jan 2024** | **Major release with new features and enhancements** |
| --- | --- |
| Failed to copy archives with large child files | A critical issue when transfering a large amount of files to MFT has been found and fixed |
|  |  |
| **4.6.5**  **28 Dec 2023** |  |
| **Features** |  |
| Navigate to Sub-Folders on Network Drive | Users can now navigate to sub-folders on a network drive when performing a Copy-To operation |
| Hidden Partition Information in Scan Report | Added information about hidden partitions in the scan report for comprehensive insights |
| Improved Remaining Scan Time Calculation | Enhanced the accuracy of calculating the remaining scan time |
| Enforce Local Login Setting | Introduced a setting to enforce local login, enhancing security measures |
| Stop Processing Files on Block | Added support to halt the scanning process when a specific number of files are blocked |
| Hide Default English Language in KIOSK UI | The administrator now has the option to hide the default English language in the KIOSK UI |
| Improved Scan Result Display Speed | Enhanced the speed of displaying scan results for a more efficient user experience |
| Anti-Tamper Feature Configuration | Enhanced the anti-tamper feature, allowing detailed configuration from the KIOSK console. (UI restart required after updating "Active Keyboard Filter" setting) |
|  |  |
| **Enhancements and fixes** |  |
| Improved AD User Authentication | Improved the ability to authenticate with Active Directory (AD) user credentials without requiring domain information input on the KIOSK UI |
| Syslog Result Log Suppression | Enhanced KIOSK to suppress result logs to syslog at the beginning of the scanning process |
| Enhanced Security | Implemented additional security measures for a more robust system. |
|  |  |
| **Fixed Bugs** |  |
| DataLocker Sentry ONE Unlock Issue | Resolved the issue where DataLocker Sentry ONE did not unlock during slow connections to its management server |
| UI Hang during Copy-To to Insufficient USB Capacity | Fixed the UI hang issue when performing Copy-To to a USB with insufficient capacity |
| KIOSK User Login Issue after Assigning to Primary AD Group | Fixed the issue where users couldn't log in with KIOSK after being assigned to the primary group in AD |
| Disk Management issue with OMVA | In the latest release of OMVA (version 2.0.9), we have addressed an issue where OMVA was not functioning optimally with Symantec and Disk Management. |
|  |  |
| **Known Issues and limitations.** |  |
| Exit Credential Feature Configuration Reset | There is a known issue where the configuration of the Exit Credential feature may be reset after upgrading to the new version |
| Unable to save user password at "Enter Vault server to upload files to" option | Will be addressed in the next version |
| Data are not deleted after wipe Bitlocker |  |

## 4.6.4

| **14 November 2023** | **Major release with new features and enhancements** |
| --- | --- |
| **Features** |  |
| Enhance Security with Anti-tamper Hardening OptionCopy&Go secondary media handling | When enabling the feature from WebMC, default Windows input compounds will be blocked and cannot be exploited to escape KIOSK mode.   - ***Notes: The shortcut to turn off KIOSK application is changed to ALT+S*** |
| Automatically unlock and process encrypted USBs with organization password | Organization-level alternative decryption security keys can be provided in management console and used as pre-configured password (max to 2 entries) to unlock encrypted USBs. |
| Simplified workflow | This new and minimal workflow is introduced to support plug-and-play media scanning with automatic decryption and result display (notes: when it is ON, the full workflows for Employee and Guest are disabled.) |
| Support files redaction, complete the workflows with Data Leak Prevention | Besides sanitizing infected files and detecting potential leak, KIOSK now is able to redact/substitute sensitive information and watermark files.   - ***Notes: The new term for sanitized and redacted is now Remediated*** |
| Support rescan retrieved files from Vault | - Previously KIOSK allows to rescan the retrieved files from a directory, now this feature is available for an integrated Vault. |
| Support HCI network volume | The new version of OMVA 2.0.8 comes with new KIOSK is compatible with Cluster Shared Volumes in HCI (Hyperconverged infrastructure) |
|  |  |
| **Enhancements and fixes** |  |
| For Hardened image | - KIOSK is compatible with Windows Defender - KIOSK starts from service. |
| Improve the self-scan feature | It’s now possible to schedule self-scan on a certain weekday |
| Enhance the labeling of CD-ROM/DVD/BD-ROM in the scan result | Scan results and log now show the correct media type for CD/DVD and Blueray disc |
| Several defects have been addressed. |  |
| **Known Issues and limitations.** | Will be addressed in our next versions. |
| The power options in Start Menu sometimes disappear after closing KIOSK. |  |
| Sometimes, File Explorer will be triggered behind KIOSK Application. |  |
| KIOSK currently does not have the capability to retry entering the password for Kanguru Defender 3000. |  |
| Set Settings cannot apply Anti-tamper Hardening to all KIOSK instances. |  |
| Cannot trigger Self Scan by clicking SCAN NOW because Simplified workflow already starts a session. | **Workaround solution:** Admin can configure Schedule Self Scan and enable option ***Allow Self Scan to cancel any currently running scan*** to trigger Self Scan |
|  |  |

## 4.6.3

| 31 August, 2023 | Release focused on enhancements and bug fixes |
| --- | --- |
| **Features** |  |
| Copy&Go secondary media handling | Introduced new button to allow choosing to insert secondary media at the start or end of a Copy&Go session  A new config option now exists in File Handling of a workflow to only allow inserting secondary media at the end of a session |
| Exit Kiosk with administrator AD credentials | Extended the configuration to allow exiting the Kiosk with AD administrator credentials |
| NTFS ADS detection | Added ability to detect and warn that an Alternative data stream was found in a processed file. This information can be seen in session history and in the reports. |
| Disable Vault ID display | Vault server configuration allows to disable showing any Vault ID information on the UI |
| Support for additional encrypted devices | - DataLocker Sentry ONE - Viasat Freedom 600 |
| `My OPSWAT` integration | Initial preparation for basic inventory & license reporting support in a future `My OPSWAT` release (end of September) |

## 4.6.2

| 26 June, 2023 | Vulnerability fixes  OMVA Release: 2.0.7.174 |
| --- | --- |
| **Features** |  |
| Security note | The system administrators are required to make Kiosk machine more secured by following actions:   1. Set a BIOS password 2. Enable TPM and Secure Boot in the Windows system 3. Turn on BitLocker encryption |
| **Fixes** |  |
| System hardening | - Disable keystrokes to maintain uninterrupted Kiosk operation and reduce interference ([CVE-2023-36657](https://nvd.nist.gov/vuln/detail/CVE-2023-36657)) - Prevent unintended executables to be ran ([CVE-2023-36658](https://nvd.nist.gov/vuln/detail/CVE-2023-36658)) - Prevent overly long input ([CVE-2023-36659](https://nvd.nist.gov/vuln/detail/CVE-2023-36659)) |

---

## 4.6.1

| 8 May, 2023 | Security patch release - 4.6.1.9996 |
| --- | --- |
| **Fixes** |  |
| System hardening | Optimized Windows system settings to maintain uninterrupted Kiosk operation and reduce interference |

| 18 April, 2023 | Release - 4.6.1.9995 |
| --- | --- |
| **Features** |  |
| Preloading passwords for encrypted archives | Allows users to preload list of passwords for encrypted archives before the scanning |
| Enforce remote login | Administrators can disable remote login for local, AD, or SSO users |
| Screensaver | Kiosk can play a video after a predefined amount of idle time |
| SDMS MkIII AES Duoulock support | SDMS MkIII AES Duoulock can be unlocked and processed |
| Media types | The admin can configure Kiosk to accept encrypted USBs only |
| **Fixes/Enhancements** |  |
| SSL certificates | Certificates added in the management console are stored in the Microsoft Certificate Store |
| Copying to disc | Fixed issue that prevented copying from one disc to another in the same session |
| Password protected archive\document handling | Corrected issue where certain passwords would not unlock files and Kiosk would re-prompt for input.  Improved encrypted archive handling when scanning with Vault. |
| Time filter in custom log display | Removed the custom time setting in Dashboard, Application Log, Windows Event Log, & Visitor Log |
| Verbose log compression | The support package is compressed at the highest level |
| Time format of [time] for Vault server | hh:mm:ss is changed to hh-mm-ss |
| Scanning duration | Enhancement of performance when utilizing existing process results |
| Copy&Go | All preparation actions need to be done prior to the scanning and the session ends without additional user actions |

---

## 4.5.8

| 11 October, 2022 |  |
| --- | --- |
| **Features** |  |
| Statistic information for Central Management | Added a periodic system health check and provided detail of session statistics for Central Management, for tracking purposes. |
| Hide Vault access ID on UI | The Vault access ID is now hidden on the UI. Users can temporarily reveal the ID for 3 seconds. |
| Sessions finish automatically | Enhanced the ability to complete session automatically without waiting for user actions. The session waits on pages where user input is required or results are necessary to view. |
| Visitor Management configuration | Specific visitor questions can now be enabled/disabled.  Management or Contact persons can be configured to not receive session reports attached to visitor check-in emails.  If no further questions are configured in a workflow, visitors are navigated to media detection screen immediately. |
| **Fixes/Enhancements** |  |
| UI unresponsiveness | Scanning a large amount of data may cause the Kiosk UI to hang indefinitely. Kiosk can detect this hanging, terminate and revive the UI to the state where hanging occurred. |
| Scanning archive files | Fixed mounting issues with TIB/VMDK/VHD archive files. |
| File retrieval | Encrypted devices are now supported in file retrieval. |

---

## 4.5.7

| 30 August, 2022 |  |
| --- | --- |
| **Features** |  |
| SMTP configuration | Sender input is mandatory for email settings (e.g., `From` field). The configured user for SMTP access needs to have permission to send as a configured email sender. |
| Email improvements | Session reports can be emailed to multiple recipients.  Pre-defined variables can be inserted into the body of the email to show some select data from a session. |
| Password change required on first login | Newly created users are required to change their password on their first login to the Management Console |
| Active Directory configuration in Visitor Management | Administrators can configure both AD users and groups as Contacts for Guests |
| Auto-selection of workflow | Administrators can either let employees select a workflow or automatically move forward with the first matched workflow an employee can use |
| **Fixes/Enhancements** |  |
| Custom command script | The syntax now works the same as on a DOS terminal |
| Scanning Pause/Resume | Pausing a scan requires additional confirmation |
| User authentication | Corrected the display for custom authentication on changes of `Display disclaimer screen`.  Authentication performance was also improved. |
| Performance enhancement for AD queries | Sped up the performance when connecting/querying to AD server |

---

## 4.5.6

| 24 May, 2022 | This release focused on new features  OMVA Release: 2.0.6.167 |
| --- | --- |
| **Features** |  |
| Non-authenticated workflows | Kiosk administrator can create multiple workflows for guests to select on demand. |
| Email template | Emails can now be customized with logos, text colors, and font sizes for workflows. |
| **Fixes/Enhancements** |  |
| Visitor configuration | Corrected issue where loading a large amount Active Directory users would take a long time for Visitor Contact configuration. |
| Retrieval page | Direct navigation to the Vault retrieval page occurs when only one retrieval option is enabled. |
| syslog data | Expanded session data in json format for syslog messages. |

---

## 4.5.5

| 28 March, 2022 | This release focused on new features and bug fixes/enhancements |
| --- | --- |
| **Features** |  |
| Upgrade in-place | Upgrade of Kiosk no longer requires uninstallation of the previous version. This allows for history logs to be maintained in between version upgrades. The original upgrade method still operates the same. |
| Copy empty folder | Empty folders from scanning sources are copied to local/network destination after scanning |
| **Fixes/Enhancements** |  |
| Skipped file reporting | Files not able to send to Core for scanning are now considered as Skipped files. Customer can configure to show/hide skipped files in their workflow printing options. |
| Trust self-signed certificates | Administrators can add self-signed certificates to trust directly in the Management console |
| File integrity monitoring | Corrected issue where Kiosk would be disabled by file monitoring when the feature was disabled |
| Stale processing results | Any change to a Core workflow will require a file to be analyzed to ensure results reflect the latest policy configured |
| Self Scan | Inaccessible system files are skipped during a Self Scan to avoid indefinite retries to scan |

---

## 4.5.4

| 20 December, 2021 | This release focused on new features and bug fixes/enhancements |
| --- | --- |
| **Features** |  |
| Country of Origin | The Country of Origin feature helps administrators add more restrictions on the scanning result by specifying which countries a publisher resides in as forbidden. Files published from forbidden countries are considered blocked. |
| Configurable printing per session type | Allows printing to be enabled/disabled separately for each action Scan/Retrieve/Wipe |
| **Fixes/Enhancements** |  |
| Scan result for encrypted archives in Copy&Go mode | Fixed issue that showed both Allowed and Blocked status on the same file |
| Slow processing time for a large dataset | Improved performance in processing large datasets |

---

## 4.5.3

| 2 November, 2021 | This release focused on bug fixes and enhancements |
| --- | --- |
| **Features \ Enhancement** |  |
| Skip Print button displayed for all session flows | Added `Skip Print` button when `Print` button is displayed |
| Editing workflow with many AD members assigned | Optimized performance with workflow loading to allow workflows with a large amount of members assigned to be edited |
| Support for updated encrypted device software versions and retrieving files | Added support for updated versions of some encrypted device software and corrected instances where retrieved files were download to incorrect volumes leading to failures |
| **Fixed** |  |
| Reports being stripped from emails | Modified content type in email reports to prevent specific email policies from blocking attachments |
| Retrieve files to disc | Fixed issue that prevented files to be retrieved and copied to a disc |
| Session history failing to load in certain cases | Corrected background sorting of session history that caused for sessions to not be displayed in the Management Console |

---

## 4.5.2

| 16 September, 2021 | This release focused on support for nested group login, archive file selection, session report sent for Visitor Management and bug fixes |
| --- | --- |
| **Features** |  |
| Nested group support for login | Active Directory with nested group supported for login in Kiosk UI |
| Archive file selection | Support multiple selection of password protected archives to scan |
| Visitor Management | Session report is sent to Manager, Contact, and Guest |
| **Fixed** |  |
| Phone detection | Fixed issue with phones not being detected |
| Central Mgmt config push affecting SSL settings | Prevented export/upgrade of certificate settings |
| Mismatch file result display in Session History | Corrected the display of mismatch result in session report |
| Configuration import | Fixed issue where certain settings were not maintained on a configuration import |
| Email session report | Correct cases where email was sent without a sender |
| Browse window | Refined UI browsing page |

---

## 4.5.1

| 27 July, 2021 | This release focused on blank disc detection, CM set settings, and OMVA logging enhancements.  OMVA Release: 2.0.5.137 |
| --- | --- |
| **Features** |  |
| OMVA Logging | Accessible logging in json format generated when plugging & validating media into a machine with OMVA installed |
| Printer Status | New icon on UI to show current printer status |
| Session history username filtering | Able to filter Session History in the Management Console by username |
| **Fixed** |  |
| Copy file to disc | Corrected detection of a blank disc as destination media to copy files to |
| "Set Settings" applied to all instances | Fixed issues causing Central Management failing to "set settings" to other Kiosks. Extending timeout settings in CM may be necessary |
| Workflow selection | Adjusted workflow selection for better usability |
| Session log saved to network share | Fixed case where the session log was not properly saved to a network shared folder |
| Management Console login | Modified Management Console behavior to only allow a user to be logged in from a single browser |
| USB whitelisting | Serial number to include vendor name and model |

---

## 4.5.0

Note

Management Console support for Internet Explorer has been dropped

| 15 June, 2021 | This release focused on User workflow selection, adding Spanish translation and other bug fixes.  OMVA Release: 2.0.4.130 |
| --- | --- |
| **Features** |  |
| User workflow selection | A user may now be assigned to multiple workflows either by direct assignment or group assignment.  When logging in to a Kiosk session, users will be presented with their assigned workflows to choose. |
| Spanish translation | Added support for default Spanish translation |
| Mail configuration test | When configuring SMTP settings, administrators may now test their settings within the mgmt console |
| **Fixed** |  |
| OMVA failing to validate media after a reboot | Fixed issue where media validation no longer worked after reboot in certain domain environments |
| Saving session logs to network shares | Corrected issue that prevented session logs from saving to networks shares due to permission issues |
| Allow sessions to end automatically | Modified session flow to adhere to UI timeout settings when the session is done |
| Active Directory load when editing workflows | Further enhancements to speed up the AD user & group loading when a workflow is edited |
| Local user password restrictions | Removed extra restrictions on passwords for local users and increased the minimum length to 12 characters |

---

## 4.4.12

| 6 May, 2021 | This release focused on file limit configuration with Vault processing, correcting VMDK with Linux file systems and other bug fixes. |
| --- | --- |
| **Features** |  |
| Vault processing - File size limit | File sizes can now be limited to dictate what is uploaded to Vault for processing |
| Vault processing - File count limit | The amount of files can now be limited when processing files with Vault |
| Copy-to media device info in logging | When files are copied to secondary media, the device information of this media is now included in the session logging |
| **Fixed** |  |
| Processing VMDKs with Linux file systems | Fixed issue with failing to process contents in a VMDK with Linux file systems |
| Processing discs with CDFS file system | Corrected detection error the prevented processing discs with CDFS file system |
| Hebrew language display | Restored Hebrew display when browsing for files and selecting copy-to directories |
| Management Console login case insensitivity | Modified mgmt console login to not require case sensitive username input |
| Retrieve available files from Vault | Enhanced Vault file retrieval to not display files that are not approved by a supervisor |
| Email reports | Fixed issue where email reports were sent to incorrect recipients with similar names |

---

## 4.4.11

| 6 April, 2021 | This release focused on syslog support for TLS over TCP and other features & bug fixes. |
| --- | --- |
| **Features** |  |
| syslog support for TLS over TCP | syslog can now be configured to send messages using TLS |
| USB Copying Whitelist and Retrieving files | The whitelist to allow USBs to copy files to now also applies to retrieving files from Vault or directory |
| Battery percentage display | If MetaDefender Kiosk is deployed on a battery powered system (i.e. tablet\laptop) a battery power indicator will be displayed on the user interface in the bottom right corner |
| Disable hash calculation for non-processing session | For workflows where no processing is configured, the hash calculation of files can be disabled to allow for a faster session completion time |
| Fallback to OS logged in user when copying files to a directory | File handling to copy files to a directory now has the ability to enable copying files as the OS logged-in user if copying using the Kiosk user session credentials fails |
| **Fixed** |  |
| Media detection | Corrected further issues with media detection:   - encrypted devices being detected as CDROM - media insertion not being detected after a wipe event |
| Wipe functionality | Corrected further issues with wiping media:   - encrypted device handling attempting to wipe the un-encrypted disc partition - wiping hanging on completion - device detection not operating after a wipe event |
| AD User & Group load in workflows | Improved the mechanism to load the list of AD users & groups to better handle large amounts |
| Retrieve files from Vault | Fixed a case where authenticating a user to Vault for retrieving files was failing |
| Send email only when blocked files are found | Restored the expected behavior of the workflow email setting to only send a session report email when a blocked file is found in a session |

Notes

Added a survey in the Management Console to collect feedback

---

## 4.4.10

| 4 February, 2021 | This release focused on Digital session log signing and bug fixes. |
| --- | --- |
| **Features** |  |
| Digital signing of session logs | Session logs can now be digitally signed with a configured certificate to ensure logs have not been tampered with |
| Supported browsers for the Management Console | The Management Console supports Chrome, Firefox, and Edge browsers. Internet Explorer and others are not officially supported |
| **Fixed** |  |
| Media detection | Enhanced media detection logic to reduce inconsistent issues with misdetection or improper identification of media |
| Copy & Go and copying to user media destination | Copying files to a secondary media is now supported when Copy & Go processing is enabled |
| SSO Management console login from a remote system | Fixed a redirection issue that caused users to not be navigated into the mgmt console after a successful SSO login |
| Guest workflow file retrieval | Corrected issue where Guests were not allowed to retrieve files if certain user authentication settings were set |

---

## 4.4.9

| 12 January, 2021 | This release focused on user experience enhancements & bug fixes.  OMVA Release: 2.0.3.96 |
| --- | --- |
| **Features** |  |
| Estimated time remaining display during processing | Processing progress indicator now shows current time elapsed and estimated time remaining |
| Retrieve files from Vault as a Guest | Guests can retrieve files from Vault using a Guest ID |
| Multiple copy-to directory support | Multiple copy-to directories can be configured in file handling. Users can select which directory to copy to when the user copy selection is enabled. |
| Browse file selection totals | Options for browsing files can now be set to display the number of files selected and the total size of the selection |
| **Fixed** |  |
| File\Session history export | Corrected issues with the export taking too long to generate and timing out connections |
| Retrieve files from Vault as an AD user | Fixed problems with retrieving files from Vault for certain AD user configurations |
| OMVA multiple media manifest support | Adjusted OMVA support for handling multiple media manifests on a device |

---

## 4.4.8

| 8 December, 2020 | This release focused on Single Sign On user login to the Management Console & bug fixes.  OMVA Release: 2.0.2.94 |
| --- | --- |
| **Features** |  |
| SSO authentication for the Management Console | Management Console login settings have been expanded to allow connecting an Identity Provider via SAML 2.0 |
| **Fixed** |  |
| Custom workflow editor load time for a large AD | Reduced the amount of time it takes to load the AD user\group list when editing a custom workflow |
| Periodic Core test | Fixed eicar test string generation that was affecting the detection rate |
| OMVA non-ascii path support | Corrected OMVA support for handling file paths with non-ascii characters which would result in blocking media |

---

## 4.4.7

| 10 November, 2020 | This release focused on Active Directory user login to the Management Console & bug fixes. |
| --- | --- |
| **Features** |  |
| Allow AD users to log in to the Management Console | Management Console login settings have been expanded to allow connecting Active Directories to allow users/groups to login |
| **Fixed** |  |
| Session log directory in Central Management | Fixed validation error that prevented setting the session log directory from Central Mgmt |
| Automatic export | Corrected non-ascii errors with automatic export and added Scanning System information to the csv |

---

## 4.4.6

| 13 October, 2020 | This release is focused on bug fixes. |
| --- | --- |
| **Features** |  |
| Configurable result for un-processed large files | Management Console administrators can now specify if a file should be allowed or blocked if it exceeds the file size limit for sending a file to MetaDefender Core. |
| **Fixed** |  |
| Floppy drives consistently spinning | Fixed issue where certain floppy drive models would spin up consistently while Kiosk was running |
| Workflow login selection | Corrected instances where mapping a logged in user to a workflow did not follow the configured order |
| File size process limit | Adjusted file size calculation to prevent errors with setting file size limit for processing files |
| Core URL validation | Repaired error detection that would prevent connecting a Core via hostname |

---

## 4.4.5

| 15 September, 2020 | This release is focused on simplifying HTTPS configuration within the Management Console and bug fixes. |
| --- | --- |
| **Features** |  |
| Configure HTTPS from the Management Console | Management Console administrators can now configure listening port and HTTPS settings from within the Management Console |
| Configurable boot sector processing | Boot sector files can now be disabled from appearing in browsing for files to process and not included when processing all contents of media |
| **Fixed** |  |
| UNC file path support for retrieving files | Fixed issues where retrieving files from a UNC path would fail |
| User question display in session export | Session export data now displays the user question and answer to the question in order |
| Copying files to disc | Corrected instances where long file paths were failing to be copied to discs |

---

## 4.4.4

| 18 August, 2020 | This release is focused on Configuring the order workflow profiles are used to map a user to, periodic testing of Core servers and bug fixes. |
| --- | --- |
| **Features** |  |
| Configure order of workflow profiles | Custom workflow profiles can now be manually adjusted to indicate the order in which users are identified to belong to |
| Periodic Core test | Kiosk can be configured to periodically send an EICAR file to ensure Core's detection is functioning |
| **Fixed** |  |
| Email session report | Corrected issues with connecting to SMTP, sending emails to the logged in user and guest users |
| Authentication failure when Remote AD SSL is enabled | Fixed active directory communication to not attempt the default LDAP port when SSL is enabled |
| Automatic export of session\file history logs | Export log path configuration was failing to save and the file history export was lacking information, this has all been corrected |
| UNC path support for session logs | Fixed issue that prevented configuring a UNC path for specifying where session logs were written out to |

---

## 4.4.3

| 16 July, 2020 | This release is focused on Copy & Go processing, ability to retrieve files from a directory and configuring the install password for OMVA  OMVA Release: 2.0.1.92 |
| --- | --- |
| **Features** |  |
| Copy & Go processing | New Core processing option that allows copying files to the system and removing media before file processing begins |
| Retrieving files from a directory | Ability to retrieve files from a local or network share and run the files through Core before copying to the inserted media |
| OMVA configurable uninstall password | The uninstall password can now be modified for deployments to endpoints |
| Whitelist for secondary media | Whitelist can now be specified for copy-to media |
| **Fixed** |  |
| Language import | Corrected issue where languages were not allowed to be edited after importing configuration of a previous release |
| IP support for SMTP host configuration | Fixed issue where connecting to an SMTP host configured by IP would fail |
| Hostname for syslog | syslog server can now be configured by either IP address or hostname |
| Users and Groups synced in workflows on Central Mgmt | The users and groups re-assigned to other workflows on Central Mgmt now updates as expected and syncs to the Kiosk instance's settings |

---

## 4.4.2

| 5 June, 2020 | This release is focused on fixing issues with remote Active Directory support |
| --- | --- |
| **Fixed** |  |
| Remote Active Directory connection and assigning users and groups to a workflow | Fixed domain identification issues that would block adding an AD server. Corrected problems where displaying the users and groups of a server would fail. |
| Usability of selecting groups to assign to a workflow | Added the ability to search the groups list to find specific entries |

---

## 4.4.1

| 15 May, 2020 | This release is focused on adding support for multiple AD servers and log retention |
| --- | --- |
| **Features** |  |
| Multiple Active Directory support | Multiple active directories can now be added to expand the coverage of users allowed to use Kiosk |
| Automated log retention | Application logs and session history can now be set to automatically clean up records older than a configured time span |
| **Fixed** |  |
| Issues with user authentication and foreign language passwords | Fixed issues where users could not authenticate when their passwords contained foreign characters |
| Username & user response variables for the copy-to directory | Copy-to directory validation has been fixed to allow the user name and user response variables |
| UI exit password setting | Fixed an issue where the exit password was changed when user authentication settings were modified |
| Offline systems could not locally access the mgmt console | Updated internal management console settings to allow offline systems to access the console locally |
| Selecting groups to add to a workflow | Only allowed groups are displayed to assign to a workflow |
| Central Management v7 configuration sync | Corrected many issues where settings disappeared from the Central Management view or were applied incorrectly |

---

## 4.4.0

| 16 April, 2020 | This release is focused on adding NGINX to serve the Management Console, allowing Guests to receive summary reports via email, and providing passwords with encrypted archives when processing with Vault |
| --- | --- |
| **Features** |  |
| NGINX serving the Management Console | IIS Express has been replaced with NGINX to power the Management Console |
| Guests can email session reports | Guests are now prompted to enter an email to session reports, when emailing reports is enabled |
| Send passwords with encrypted archives when processing with Vault | When an encrypted archive is identified, a password can be input to submit the file to Vault for processing |
| Support for Kanguru Defender Elite 200 | Added support for processing Kanguru Defender Elite 200 USB |
| **Fixed** |  |
| Setting custom export date range | Fixed the date selection to allow setting a custom date range to export session or file history |
| OMVA install via automated deployments | Modified OMVA installation to work successfully in remote deployments |
| Hash verification copy failure with extension-less files | Corrected an issue with hash verification failing on files without an extension |
| Copying files to a network share as Guest | Copying to a network share now utilizes the credentials of the user logged in to the system to copy files in the Guest workflow |

---

## 4.3.11

| 13 March, 2020 | This release is focused on the flexibility with the Vault copy-to directory structure, file deletion confirmation for users and other bug fixes |
| --- | --- |
| **Features** |  |
| Specify Vault copy-to directory structure | Administrators can now indicate the directory structure of how files are uploaded to Vault when configuring a Vault server |
| Allow users to confirm to delete all blocked files | When blocked file handling is set to delete files, an Administrator can now allow users to confirm whether the blocked files should be deleted or not |
| **Fixed** |  |
| Copy-to media blocked with OMVA | Copying all allowed files to a secondary media that was wiped would still cause OMVA to block the media. This workflow has been modified to allow OMVA to unblock the media as expected. |
| Configure syslog settings from Central Management | A managed instance's syslog settings can now be configured via Central Management v7 |
| Single password use to unlock multiple encrypted archives | Fixed an issue where the checkbox to supply a single password to multiple encrypted archives was not being respected |
| AD groups are only allowed to be added to a workflow profile | Only AD group objects will be allowed to be added to a workflow profile to reduce confusion with authentication issues |
| Sanitized file handling with the custom command line script | Corrected an issue where sanitized files were not handled in a configured script |

---

## 4.3.10

| 11 February, 2020 | This release is focused on bug fixes |
| --- | --- |
| **Fixed** |  |
| Detection of multiple Linux partitions | A device with multiple non-Windows partitions can now be browsed through and processed |
| Vault entry changes applied automatically to selections | Any changes made to an entry in the Vault server list are automatically applied across all configured selections of that specific server |
| Windows XP+ support for OPSWAT Media Validation Agent | OMVA now supports Windows XP and above |
| Report files quarantined by Core | Files quarantined by Core are now reported on the session summary without having to configure to have the files removed |
| Language menu button on the on-screen keyboard | Corrected button behavior where the keyboard language button would remain open despite clicking away from it |

---

## 4.3.9

| 14 January, 2020 | This release is focused on Vault upload to user configuration and bug fixes |
| --- | --- |
| **Features** |  |
| Specify Vault user to upload files to | New configuration option allows for specifying a Vault user to upload files to in addition to the previous settings of uploading to the user logged into Kiosk or a guest account |
| **Fixed** |  |
| Retrieve files from Vault | Fixed issues with downloading files from Vault among multiple users |
| File sizes displayed in browse | Corrected the file size display when browsing for files |

---

## 4.3.8

| 10 December, 2019 | This release is focused on Imaging Media and bug fixes |
| --- | --- |
| **Features** |  |
| Image Media | New process flow allows for an image to be created of the inserted media and uploaded to a specified location (e.g. Vault or directory) |
| **Fixed** |  |
| IIS Express 10 support | Kiosk REST service now runs uninterrupted if the underlying IIS Express is upgraded to version 10 |
| Updated German language strings | German language strings are now up-to-date |
| Blocked sound playback | Fixed an issue where the sound byte to alert for blocked files would not play at times |

---

## 4.3.7

| 12 November, 2019 | This release is focused on Visitor Management and bug fixes |
| --- | --- |
| **Features** |  |
| Visitor Management | Visitor management allows the ability for guest users to check-in to an organization via the Kiosk. During the check-in process the guest user accepts any agreements specified by the organization, a badge for the visitor can be printed and contact\admin personnel are automatically notified when a guest has arrived. |
| **Fixed** |  |
| Korean keyboard character composition | Onscreen Korean keyboard has been fixed to correctly combine Hangul characters |
| Device whitelisting applies to destination media | Device whitelisting is now applied to destination media, in addition to the source media used for processing |
| Copy files to IronKey USB | Corrected behavior where files were copied to the wrong volume for specific IronKey USBs |

---

## 4.3.6

| 8 October, 2019 | This release is focused on Management Console enhancements when Kiosk is managed and bug fixes |
| --- | --- |
| **Features** |  |
| Management Console settings locked when instance is managed | The Management Console now has the ability to show details when it is managed. If managed, changes to settings are disabled. Currently supported for Central Management v5, v7 in the future. |
| Configure the length of time a Vault guest account is valid | Administrators can now specify how long a created Vault guest account can remain valid |
| **Fixed** |  |
| Processing system files | Enhancements made in attempting to process system files that may be potentially locked |
| File integrity monitor event | Upgraded the visibility of a file integrity monitor event to be included in the syslog application events |

---

## 4.3.5

| 10 September, 2019 | This release is primarily focused on bug fixes |
| --- | --- |
| **Features** |  |
| Delete after retrieving files | Retrieving files from Vault can now be configured to delete the files from the server after download |
| **Fixed** |  |
| Copy to disc folder structure | Copying to disc no longer creates a Session ID directory when the no subfolders option is enabled |
| Settings display on Central Mgmt v7 | Fixed issues with some fields being improperly displayed in Central Mgmt |
| LDAP groups workflow profile assignment | Corrected an error where a users logging in to Kiosk were not identified under a user group assigned to a workflow profile |

---

## 4.3.4

| 13 August, 2019 | Release focused on adding Kiosk high availability, Layer 7 load balancer support and bug fixes |
| --- | --- |
| **Features** |  |
| Ability for Kiosk to use multiple backup servers during a session | Multiple backup servers can now be configured in the global configuration.  Within a workflow profile, it can be designated for Kiosk to attempt processing a file among any available MetaDefender server during a session. |
| Support for Layer 7 Load Balancer with MetaDefender | A Load Balancer can now be selected as the primary server for processing files |
| Regular expression support for media whitelisting | Media whitelisting can accept regular expression rules for more flexibility in configuring allowed devices |
| Option to disable SSL verification | Certain offline environments cannot successfully verify SSL certificates due to the network structure.  Kiosks in these special instances can be configured to workaround these limitations. |
| **Fixed** |  |
| Issue with MetaDefender verification only working through TLS 1.0 | MetaDefender connection testing in the Management Console has been fixed to utilize the latest security protocols when available (e.g. TLS 1.2) |
| Virtual keyboard input | Corrected ability to insert/delete characters within an input text box rather than only at the ends of the input |
| Unlock for IronKey D300 Managed devices | Updated ability to handle different versions of IronKey D300 Managed devices |
| Interface timeout not triggered while waiting for media to be inserted | Fixed the interface timeout to apply while waiting for media to be inserted |
| Updated Custom Authentication Module template | Custom Authentication Module template & tester have been updated to 64bit |

---

## 4.3.3

| 9 July, 2019 | Release focused on adding Kiosk self scan and bug fixes |
| --- | --- |
| **Features** |  |
| Kiosk self scan | Allows the user to periodically or on demand utilize the MetaDefender Kiosk to scan its file system for possible infection |
| File handling option to copy allowed files to the original media | New copy-to route will wipe the original media and copy all allowed files back to it |
| Select to not submit special archive files, mounted by Kiosk, to Core | Only applicable to Acronis backups, virtual hard disks and/or VMware virtual machines. Can now choose to withhold these files from Core if its contents have already been processed. |
| Prompt users for the password to password protected documents | When password protected documents are encountered (Word, PDF, Excel), they will now be prompted for passwords for processing their contents. |
| Generate a log message and warn the user when disk capacity reaches 80% | To help our customers ensure that the Kiosk has sufficient space to operate, it will generate a log message when disk capacity has reached 80% or higher. |
| Updated Custom Authentication Module sample code to include 64-bit | To better facilitate CAM users in upgrading from V3 to V4, the CAM sample code has been cleaned up and generated in 64-bit |
| **Fixed** |  |
| Kiosk failing to quarantine read-only files | Read-only files are now supported for quarantining |
| Fixed VHD mounting that was broken by recent Windows 10 updates | Windows 10 updates changed the case of the name of the drive being attached. Fixed parsing to handle variable case string. |

---

## 4.3.2

| 11 June, 2019 | Release focused on adding the OPSWAT Media Validation Agent, support for Avira-Iron-Drive, and bug fixes |
| --- | --- |
| **Features** |  |
| Added the OPSWAT Media Validation Agent | The OPSWAT Media Validation Agent can be downloaded from the Management Console Resources section. This agent can be used to ensure media is processed by a Kiosk before it can be mounted on an endpoint. |
| Support for Avira-Iron-Drive | Files can now be processed within or copied to an Avira-Iron-Drive. |
| **Fixed** |  |
| Changes made to the disclaimer not being updated | Corrected issue where making changes to the disclaimer content were not reflected in the UI |
| Sentry 3 FIPS unlock enhancement | Enhanced the unlock mechanism for Sentry 3 FIPS to correctly unlock versions with different behavior |
| Disabling boot hardening may hang | Fixed disabling the boot hardening to not cause a hang and fail to update the correct status on the mgmt console for some cases |
| Central Mgmt synchronization error | Added more protection to avoid issues with Central Mgmt configuration pushes failing |

---

## 4.3.1

| 15 May, 2019 | Release focused on fixing Management Console logins for all timezones |
| --- | --- |
| **Fixed** |  |
| Login to the Management Console | Corrected issue where login to the Management Console would fail on certain systems |

---

## 4.3.0

| 14 May, 2019 | Feature release focused on adding user support for the Management Console, support for Non-Windows file systems and minor bug fixes |
| --- | --- |
| **Features** |  |
| User login for the Management Console | User login is now required to access the Management Console *In keeping parity with MetaDefender, custom integrations to the REST API with passwords will no longer function. You must set up an API key per user. When installing, you must use the creation wizard to create your first admin user. Admin credentials are no longer created automatically. |
| Support for Non-Windows file systems | Processing media content in Ext2/3/4, HFS Plus, HFSX, and APFS file systems is supported |
| Discs allowed to retrieve files from Vault | Retrieving files from Vault can now be downloaded to a disc |
| **Fixed** |  |
| Enabling boot hardening | Security enhancements made to allow boot hardening for all systems |
| File handling count display | A count of the current file progress is now displayed when files are copied/moved to a destination |
| Product activation through a proxy | Online activation can now complete successfully via a proxy server |

---

## 4.2.15

| 18 April, 2019 | Feature release focused on internal enhancements for Central Management |
| --- | --- |
| **Fixed** |  |
| Improvements for Central Management | Under the hood enhancements to allow the management of Kiosk instances to be smoother |

---

## 4.2.14

| 9 April, 2019 | Feature release focused on adding support for VMware virtual machines and bug fixes |
| --- | --- |
| **Features** |  |
| Mount and scan VMware virtual machines | Added support for processing within VMDK files |
| French translation | French language can now be selected as one of the default languages |
| Upload files to Vault | Vault upload in the file handling of a workflow can now be specified to upload files singularly (with the addition of file scan results) or all packaged within a zip |
| Password prompt for nested encrypted archives | Password prompt will be displayed for encrypted archives found within encrypted archives |
| Integral Courier encrypted USB support | Integral Courier can be unlocked and processed |
| Kingston IronKey D300 Managed support | Kingston IronKey D300M can be unlocked and processed |
| **Fixed** |  |
| CEF Extension field format | The Extension field in the CEF messages have been fixed to conform to correct CEF standard |
| German language | German language strings have been expanded upon |

---

## 4.2.13

| 12 March, 2019 | Feature release focused on processing contents within virtual hard disks and minor fixes |
| --- | --- |
| **Features** |  |
| Mount and scan VHD & VHDX | Added support for processing within virtual hard disk files |
| **Fixed** |  |
| Copying sanitized files would fail for certain users logged into a Kiosk session | All users are now able to copy sanitized files to the desired destination |
| LDAPS connection | Connecting to a directory server via LDAPS has been improved |

---

## 4.2.12

| 12 February, 2019 | Feature release focused on system boot hardening, folder navigation on Vault and allowing copying original with sanitized files |
| --- | --- |
| **Features** |  |
| System boot hardening | With boot hardening enabled the taskbar on the desktop will be not be loaded, thereby disallowing any PC functionality to a user until the Kiosk starts. |
| Folder navigation when retrieving files from Vault | When browsing for files to download from Vault, folders can be accessed and downloaded to the desired media. |
| Copy the original file along with the sanitized version | New configuration option added for Copy-To actions that will allow an administrator to specify copying the original file along with the sanitized version. |
| **Fixed** |  |
| Emails not being sent to the user logged into the Kiosk session | Kiosk can now identify the email address of the logged in user from a remote AD server. |
| LDAPS authentication failure | Users can authenticate using LDAPS functionality with improved routing. |
| Handling sanitized file naming convention | Now an incremental number is only appended to the file name during copy to avoid file collisions. |

---

## 4.2.11

| 8 January, 2019 | Feature release focused on allowing multiple devices to be wiped in one session and stability enhancements |
| --- | --- |
| **Features** |  |
| Wipe multiple devices in one session | Multiple devices can be inserted at the wipe option selection screen for the wipe to be performed on all devices |
| Warning message is displayed if a file is not processed by MetaDefender | A warning message is displayed before the session results screen if any file is not processed by MetaDefender |
| **Fixed** |  |
| Backup server selection when the primary MetaDefender instance is unable to process files | The decision to use a backup MetaDefender server has been enhanced to ensure a primary MetaDefender instance is not used when it is unable to process files. Any MetaDefender instance that reports problematic issues will be noted on the Mgmt Console and the issue logged in the application log. |
| syslog message format for TCP | Some syslog messages were missing line breaks which caused parsing issues for some syslog management systems when receiving data over TCP |
| Enhanced retry mechanism for files that are unable to be opened | Certain files have some permissions that block Kiosk from accessing them to upload the file to MetaDefender for processing. The ability to retry on these files and allow for successful upload has been enhanced. This does not apply to locked system files. |
| Processing an iPhone with iTunes installed | After installing iTunes and then selecting files from an iPhone to process, the selected files would not be processed. Functionality has been restored. |

---

## 4.2.10

| 11 December, 2018 | Feature release focused on expanding support for processing non-Windows file systems and simplifying blocked files reported in session reports. |
| --- | --- |
| **Features** |  |
| Blocked results directly reported from MetaDefender | Beforehand, Kiosk would group specific blocked reasons under special categories (e.g. Encrypted Archive & Password Protected Document → Password Protected). This would result in confusion when reading session summary reports and verifying specific file counts against the MetaDefender processing history. Blocked results are no longer grouped under special categories, they are grouped according to the result returned from MetaDefender. |
| **Fixed** |  |
| Blocked results directly reported from MetaDefender | Beforehand, Kiosk would group specific blocked reasons under special categories (e.g. Encrypted Archive & Password Protected Document → Password Protected). This would result in confusion when reading session summary reports and verifying specific file counts against the MetaDefender processing history. Blocked results are no longer grouped under special categories, they are grouped according to the result returned from MetaDefender. |
| Custom command line script not running | There was an issue with the component that runs custom command line script - failing to start and complete the configured actions. This has been fixed. |
| syslog CEF format | syslog messages sent in CEF were not formatted according to specifications which caused parsing issues in SIEM servers. The main body of the message is now sent in the Extension section and the log type is sent in the Name section. The severity level has also been corrected to meet the CEF specification. |
| Processing mobile phones with Vault | Fixed upload failures when attempting to process a mobile phone with MetaDefender Vault. |

---

## 4.2.9

| 13 November, 2018 | Feature release focused on email, user selection of copy-to directories and stability improvements |
| --- | --- |
| **Features** |  |
| Configuration to only send an email report when a blocked file is detected | The email report can now be specified to be sent only when a blocked file in a session is found, rather than sending an email after every session. |
| Allow users to select the folder structure of copied files | Users can now be allowed to select whether to create a high level directory for files to be copied to or maintain the same folder structure as the original processed media. |
| **Fixed** |  |
| Enhanced progress display for processing TIB files | Modified TIB processing experience to follow the archive processing flow. Files within a TIB are displayed during progress, the TIB itself is counted as one file & an indicator in the right hand corner will notify the user that an archive is being processed. |
| UI will remain responsive when processing large datasets | Processing large datasets would cause the UI to stop showing updated progress from being displayed near the completion of a session, giving the impression that the UI was hanging. Progress reporting has been modified to allow the UI to be responsive under large datasets for the duration of a session. |
| Finding users in groups assigned to workflow profiles | With a group assigned to a workflow profile, when a user would log in to Kiosk, there were instances where a user that is a member of the group was not correctly associated not provided the expected workflow profile. This has been fixed. |
| SD card detection failure | Certain SD card readers present information of the media differently, which caused the Kiosk to not detect it. Media detection has been updated to handle this case. |
| Hash verification when copying to a network share | Hash verification has been fixed to work with verifying files were copied correctly to a network share. |
| Translated strings not updating on the UI | A few translatable strings were not being updated for display in the UI. These have been identified and fixed. The default Japanese language strings have also been updated. |

---

## 4.2.8

| 22 October, 2018 | Maintenance release focused on Central Management compatibility |
| --- | --- |
| **Fixed** |  |
| Tab selection in Central Management | Scrolling through configuration sections has been removed in the latest Central Management 5.2.3. Overflow sections are now selectable from a dropdown menu. |
| Vault server configuration import from Central Management | Due to the change in how Vault server settings are saved in Kiosk, only partial Vault settings were being imported over. This has been rectified. |

---

## 4.2.7

| 11 October, 2018 | Feature release focused on media manifest validation and improvements for stabilized processing |
| --- | --- |
| **Features** |  |
| Media Manifest Validation | Previously, Kiosk only saved signed manifests to the media that had been processed. Kiosk can now be configured to validate and utilize results from a manifest found on the media to process. |
| Logo and Intro Text on Receipt Printout | A logo and introduction text can be configured to print onto a session receipt. |
| **Fixed** |  |
| Process failure logging is now more transparent | If Kiosk fails to send a file to the MetaDefender server, the reason will be displayed in the UI and session result log & printout. Any network connection errors contributing to failures or MetaDefender failures reported to Kiosk will be logged in the Application Log in the Kiosk Management Console. Messages will contain HTTP codes, description and network error messages to enable admins to take proactive action. |
| Updated bundled 7z component to version 18.05 | Due to vulnerability issues with older versions, the bundled 7z binaries were updated to the latest version. |
| Retry logic improved when retrieving results from MetaDefender | In previous versions, if an error from MetaDefender prevented Kiosk from obtaining results, it would fail quickly and show that the file failed to process. Kiosk will now try harder to receive correct results from MetaDefender if a file has been successfully sent for processing. |
| Removed curl error logging when a session is canceled | Canceling a session can result in canceling active connections between the MetaDefender server & Kiosk. This would result in an unnecessary large amount of curl error logs that are now removed under this specific condition. |

## 4.2.6

Release Date: 11 September, 2018

#### Features

- Added support for processing iPhones
- Ability for users to select which file handling actions to take
- Added support for DataLocker Sentry 3 FIPS
- syslog messages can output in CEF format

#### Fixed

- Files sizes are displayed when browsing files to process
- Added more display data to the session log & printout

  - File attributes, partition information, symbolic links found
- Fixed issues with session log generation
- Added ability to navigate through user questions
- Enhanced loading process upon startup
- Core quarantine results are now reflected in the Kiosk results

## 4.2.5

Release Date: 14 August, 2018

#### Features

- Offload processing to a Vault server connected to MetaDefender
- Ability to Pause and Resume file processing
- Enable/disable the Default workflow to restrict user login

#### Fixed

- Adjustments to automatic printing at the end of a session
- Fixed copying to a network share when a Remote Active Directory is configured
- Support copying between encrypted media of the same type
- Configurable footer printing for the session receipt

## 4.2.4

Release Date: 10 July, 2018

#### Features

- Added support for processing android phones
- Added support for processing within Acronis TIB files
- Ability to view and assign user groups to a workflow profile

#### Fixed

- Syslog messages can be configured to send over TCP
- Defined more event codes for syslog messages
- Enhanced ability to handle large nested directories
- WebMC session history will display if a result is from a hash lookup

## 4.2.3

Release Date: 12 June, 2018

#### Features

- Added LDAPS support for Remote AD servers
- Ability to set the apikey during installation
- Display file names of files in a large archive during processing

#### Fixed

- Extended syslog support to multiple servers
- Fixed login issue with users assigned to a workflow profile
- Corrected browsing for files in nested directories with similar names
- Improved the speed for copying files

## 4.2.2

Release Date: 21 May 2018

#### Features

- Functionality to alert if a popup is open on the underlying system
- Events can be configured to broadcast to a syslog server

#### Fixed

- File browse window can handle large number of files in a directory
- Fixed issue with querying users from a remote AD
- Ensuring a session ID is always generated for reports
- Updated Central Mgmt integration to further validate configuration settings
- Added ability to view the MetaDefender Privacy Policy from the Management Console

## 4.2.1

Release Date: 16 April, 2018

#### Features

- Ability to download files from Vault
- Configure session and file history CSV export run automatically
- Added support for Kingston DataTraveler 400 G2
- Email session reports to the logged in Kiosk session user

#### Fixed

- Modified font display with foreign languages
- Fixed issue with Central Mgmt settings import
- Enhanced various logging with more specific information

## 4.2.0

Release Date: 20 February, 2018

#### Features

- Rebranded Kiosk
- Ability to be managed by Central Management
- Added support for Kanguru Defender Elite 300
- Session and file history can be exported to CSV
- Kiosk can be configured to allow file handling to run automatically

#### Fixed

- Fixed issue with reporting wipe progress for large devices
- Improved media handling
- Added new configuration

  - allow users to skip entering passwords for McAfee drives
  - disable warning of network errors
- Enhanced license activation

## 4.1.1

Release Date: 30 November, 2017

#### Features

- None

#### Fixed

- Fixed issue in uploading files to SFT accounts when authentication is done by a custom authentication module
- Sanitized files are copied to temporary storage instead of original media
- Fixed issue in creating a new language
- Fixed issue where session finish time was reported incorrectly in Kiosk logs

## 4.1.0

Release Date: 26 October, 2017

#### Features

- Support for additional models of encrypted USB drives

  - Ironkey S1000
  - Ironkey D300
  - Kingston DataTraveler Vault Privacy 3.0
  - Kingston DataTraveler 2000
  - Kingston DataTraveler 4000
- Answers to user questions can be used in the path specified for post scan file handling
- When copying blocked files, administrators have the option of only copying files that have been sanitized

#### Fixed

- The Metadefender Kiosk Management Console now has a default password ('admin') after installation
- Cancelling a scan will cancel scans in progress on the Metadefender Core server
- Kiosk will retry scans that initially fail on the Metadefender Core server
- Improvements in the Japanese language keyboard
- Language keyboards can be disabled from the Kiosk UI

## 4.0.2

Release Date: 18 September, 2017

#### Features

- Metadefender Kiosk can be configured to check for existing scan results before sending a file to Metadefender Core

#### Fixed

- The Browse and Scan All options will not be displayed in the Kiosk UI if they are disabled
- Media wipes are now logged as sessions
- Media manifests are uploaded with files that are copied to a Metadefender SFT server
- Vulnerability details are displayed if Metadefender Core has the Metadefender Vulnerability engine enabled

## 4.0.1

Release Date: 28 July, 2017

#### Features

- Signed scan manifests can be written to processed media (requires Metadefender Core 4.8.0 or later)

#### Fixed

- Improvements in uploading files to a Metadefender SFT server
- Session scan logs are included in a configuration export

## 4.0.0

Release Date: 5 July, 2017

#### Features

- New Kiosk user interface
- Optional 'Disclaimer' Screen in Kiosk workflow
- Support for user selected language

#### Fixed

- Re-implementation of drive wipe functionality
- Move to new licensing mechanism
- 32-bit operating systems are no longer supported
- Minimum required version of Metadefender Core is 4.7.2
- Configuration can not be imported from versions prior to 4.0.0

## 3.4.6

Release Date: 25 July, 2017

#### Features

- None

#### Fixed

- Fixed issue where Kiosk sometimes didn't launch after system restart
- Minor bug fixes

## 3.4.5

Release Date: 25 April, 2017

#### Features

- Alert dialog shown to the user when a non-memory USB device is inserted
- Devices can be limited to those whitelisted by device ID

#### Fixed

- The only Metadefender Kiosk workflows included by default will be the 'Default' and 'Guest' workflows
- Mechanism to retrieve device serial IDs has been improved

## 3.4.4

Release Date: 14 March, 2017

#### Features

- None

#### Fixed

- Metadefender Kiosk will now attempt to detect a second media if the first one detected fails
- Error message shown when files can not be removed by Metadefender Kiosk

## 3.4.3

Release Date: 7 February, 2017

#### Features

- Support for USB Flash Security encrypted drives
- Option to whitelist files larger than a specified size
- Allow administrator to disable 'Process All' option

#### Fixed

- Addressed issue in using Kiosk over HTTPS
- Better handling of scan results from Metadefender Core 4.x
- System files on Bitlocker encrypted devices can optionally be excluded from scanning

## 3.4.2

Release Date: 13 December, 2016

#### Features

- Metadefender Kiosk can now be configured to abort scans as soon as a blocked file is found
- Multiple Metadefender Core servers can be defined for redundancy
- Support for wiping encrypted USBs
- Alert sound can be customized

#### Fixed

- Better reporting of mismatched files that are found within archives
- SMTP settings for emailed session reports are now configured globally
- Estonian keyboard layout is now supported for the onscreen keyboard
- Options for handling multiple partitions have been simplified to either block devices with multiple partitions or scan all available partitions

## 3.4.1

Release Date: 9 November, 2016

#### Features

- None

#### Fixed

- Kiosk user will now be prompted to confirm before destination media is wiped before files are copied to it

## 3.4.0

Release Date: 27 October, 2016

#### Features

- Each Metadefender Kiosk workflow specifies a specific Metadefender Core workflow or rule to use
- Files identified as potentially vulnerable by Metadefender Core's vulnerability engine are shown in the scan results
- Metadefender Kiosk will now scan the boot sector of any media

#### Fixed

- The Metadefender Kiosk session log page user interface has been updated
- Potential security vulnerability with Ctrl-L key combination has been closed
- Better handling of McAfee encrypted USB devices
- Requires Metadefender Core 3.12.4 or later

## 3.3.6

Release Date: 30 September, 2016

#### Features

- Built in user authentication now supports remote Active Directory authentication.

  - Note that for remote Active Directory authentication provided user credentials are not used when files are copied as a post action.

#### Fixed

- Metadefender Kiosk will validate SSL certificates when using HTTPS to communicate to the Metadefender Core server. If Metadefender Core is using a self-signed certificate, this certificate must be installed on the Metadefender Kiosk machine, otherwise validation will fail.
- The Metadefender Kiosk UI will reset after the scanned media has been removed when at the scan results page

## 3.3.5

Release Date: 1 September, 2016

#### Features

- Encrypted drives can now be used as the "Copy To" destination
- Drives that are being copied to can now be wiped before files are copied

#### Fixed

- Server settings for e-mail notifications are now configured in Metadefender Kiosk instead of in Metadefender Core

## 3.3.4

Release Date: 8 July, 2016

#### Features

- Compatible with Metadefender Core 4.4 and later versions
- Support for Kanguru 2000 and 3000 encrypted USBs
- More flexibility allowed in the destination directory when "Copy To" post action is enabled
- Scan session log can be saved as a PDF

#### Fixed

- High security workflow included by default in installation
- Kiosk UI now scales to higher resolutions
- Count of files sent to a Metadefender Secure File Transfer server added to Management Console dashboard

## 3.3.3

Release Date: 31 May, 2016

#### Features

- Non-guest Metadefender Kiosk profiles can now upload to Metadefender SFT guest accounts

#### Fixed

- Updated onscreen Japanese keyboard
- Metadefender Kiosk can now be used with a Metadefender Core server that has an API key set
- Fixed bug where files on read-only media that are sanitized were not getting copied as part of the file handling part of the workflow
- Several hotkeys are now automatically disabled when the UI is running
- Additional minor bug fixes

## 3.3.2

Release Date: 19 April, 2016

#### Features

- Scan reports can now be sent by e-mail after the scanning session is complete
- The file upload chunk size for uploading files to a Metadefender SFT server is now configurable.

#### Fixed

- The sender e-mail address is no longer required when uploading files to a Metadefender SFT server
- Additional strings have been added to the Kiosk UI and can be modified through the Management Console
- The encryption method for passwords saved in the Metadefender Kiosk configuration has changed. Importing configuration from versions prior to Metadefender Kiosk 3.3.2 will not import passwords.

## 3.3.1

Release Date: 15 March, 2016

#### Features

- None

#### Fixed

- Better cancellation of a scan in progress
- Fixed issue when browsing blank media
- Correct detection of unencrypted Kanguru devices
- Database and Windows events can be viewed through the Management Console

## 3.3.0

Release Date: 30 January, 2016

#### Features

- The name of the product is now Metadefender Kiosk
- Administrators have the option to restrict access to domain users when Windows authentication is enabled

#### Fixed

- Fixed bug in importing saved configuration
- IIS Express component has been upgraded to version 8.0

## 3.2.0

Release Date: 23 December, 2015

#### Features

- Metadefender now uses Metascan workflows (Metascan versions 3.10.1 and later)
- Custom authentication modules are supported
- Windows 10 support

#### Fixed

- None

## 3.1.0

Release Date: 31 October, 2015

#### Features

- Metascan functionality can now be configured within the Metadefender Management Console. This is only supported for Metascan servers version 3.9.5 or later.
- Support for floppy disks as the copy destination in post-actions

#### Fixed

- Custom time periods can be set for the statistics displayed on the Metadefender dashboard

## 3.0.12

Release Date: 30 September, 2015

#### Features

- Upload to Policy Patrol Secure File Transfer (Requires version 2.2 or later of SFT) is now available as a post action
- The Metadefender Management Console has an updated look and feel, matching the Metascan Management Console

#### Fixed

- The security and compatibility of the Metadefender Management Console has been improved by replacing the PHP component with JavaScript
- Stability of the data sanitization post-action has been improved
- Fixed issue where floppy disk drives on non-English operating systems were not being recognized
- Fixed issue where in certain circumstances Metadefender might not start automatically upon system restart

## 3.0.11

Release Date: 31 August, 2015

#### Features

- None

#### Fixed

- Updated kiosk UI strings for non-English languages
- Improved support for

  - Ironkey D250 encrypted USBs
  - Kanguru Elite Defender 30 USBs
  - Kingston encrypted USBs
- If Windows authentication is enabled, non-local (i.e. domain) users are now required to specify their domain

## 3.0.10

Release Date: 30 July, 2015

#### Features

- None

#### Fixed

- Resolved issue where files would fail to copy to network locations when SHA-256 hash verification was enabled
- Resolved issue in displaying large number of files in Metadefender's browse dialog
- Support for file type conversion from image files has been removed. Conversion from PDF is now only supported to sanitized PDF. For customers that will be exporting Metadefender workflows that used this functionality OPSWAT recommends that these conversions are disabled before exporting.

## 3.0.9

Release Date: 30 June, 2015

#### Features

- None

#### Fixed

- Reduced the latency in loading workflow configuration when there are many user accounts on the associated active directory server
- Resolved race condition where Metadefender occasionally did not start upon system startup when installed on Windows 8 or newer operating systems
- Improved behavior when multiple instances of Metadefender are running on the same system

## 3.0.8

Release Date: 22 May, 2015

#### Features

- Windows 8.1 and 2012 R2 are now supported
- Buffalo RUF2-hsc-2gt Encrypted USBs are now supported
- McAfee Complete Data Protection Encrypted USBs are now supported
- EncryptDisc media is now supported
- Kanguru Defender Elite 30 USB devices are now supported
- Metadefender Idle Screen can be customized
- German and Korean translations of the Metadefender kiosk UI

#### Fixed

- Hashes of files are re-verified when the 'Copy To' post action command is used
- Better handling of network failures when scanning with a remote Metascan server

## 3.0.7

Release Date: 22 December, 2014

#### Features

- Scan logs can be saved to the media being scanned
- Recent sessions now listed in the Metadefender Management Console logs page
- Support for Buffalo SecureLock encrypted devices
- Receipt can be configured to print automatically

#### Fixed

- More details available in the scan result screen for files that failed to scan
- Kiosk user can be alerted when Metadefender license is close to expiration
- New HTML documentation available through the Management Console
- Romaji input supported on Japanese keyboard
- More robust support for Kingston DataTraveler encrypted USBs
- Bitlocker encrypted drives are now supported on Windows 8.1
- Other minor changes

## 3.0.6

Release Date: 4 November, 2014

#### Features

- Support for Ironkey D250 encrypted USBs
- Support for BitLocker (password) encrypted devices
- Vietnamese and Japanese user interface available by default

#### Fixed

- User account credentials used for post actions when Windows authentication is enabled
- Better indication when potential threats are found
- Additional scan result details included in text log file
- Debug log package available for download in Management Console
- Additional printout configuration options

## 3.0.5

Release Date: 1 August, 2014

#### Features

- Added Support of KIOSK UI localization
- Added predefined KIOSK UI Localization for Hebrew & Arabic
- Added additional predefined profiles
- More configuration for printouts

#### Fixed

- Fixed error when scanning empty media
- Improved accuracy of timestamps in logs
- Improved error handling and logging for errors
- Updated logs to include scan failure reason
- Clearer notification when a threat is found
- Add ability to set password in Metadefender Management Console
- Various bug fixes

## 3.0.4

Release Date: 8 May, 2014

#### Features

- Copy to user provided media as post-action
- Username is available as a variable in post-actions when Windows login is enabled

#### Fixed

- Improved archive handling
- Improved physical keyboard support
- Scan is aborted if connection with Metascan server is interrupted (when Metascan is on separate machine)
- Improved handling when Metascan server is operating at maximum capacity
- Fixed potential issue where Metadefender failed to launch due to latency of Windows desktop preparation
- Better logging for interruptions during post processing
- Minor bug fixes
- UI improvements

## 3.0.3

Release Date: 8 November, 2013

#### Features

- None

#### Fixed

- Fixed print formatting issues

## 3.0.2

Release Date: 27 September, 2013

#### Features

- Search for processing result by file upload
- Ability to export processing logs
- Allow search results to be bookmarked for later reference
- Display more detailed progress during file enumeration
- Improved Metadefender Management Console
- Improved formatting for built-in kiosk printers

#### Fixed

- Fixed bug that was preventing restoration of default and guest profiles
- Prevent users from being added to more than one workflow profile

## 3.0.1

Release Date: 5 July, 2013

#### Features

- User Authentication
- Customizable User Profiles
- Configurable User Questions
- Filtering by File Type
- Web-Based Metadefender Management Console
- System Restore with Deep Freeze
- File Type Conversions
- Enhanced Post-Processing Options
- New End User Workflow
- Option to Restart After Each Session
- Comprehensive Logging for all Processed Files
- Support for Kingston encrypted USB drives
- Handling USB with partially corrupted file system
