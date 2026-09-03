<!-- source: https://www.opswat.com/docs/mdkiosk-linux/release-notes/release-notes -->

# Release Notes

## [5.7.6](/docs/mdkiosk-linux/release-notes/release-notes#576)

| 8 April 2026 |  |
| --- | --- |
| Optimized scanning performance | Optimized the MetaDefender Linux Kiosk scanning pipeline to significantly improve performance when processing files, especially in large volumes of files. As a result, users experience shorter waiting periods and higher throughput on Kiosk used in high-volume environments |
| Improve Linux Kiosk UI stability during operation | Addressed an issue where MetaDefender Linux Kiosk could become unresponsive during operation. The fix ensures that the Kiosk UI and background services remain responsive even under heavy load or extended usage. |

## [5.7.5](/docs/mdkiosk-linux/release-notes/release-notes#575)

| 17 December 2025 |  |
| --- | --- |
| Enhanced hardware integrity checks | Enhanced validation process to improve hardware integrity checks on Kiosk L1002 and L2100, ensuring faster and smoother setup |
| Customize BIOS settings on Kiosk L1002 | Added support for customizing BIOS settings on Kiosk L1002, including Wi-Fi, Bluetooth, camera, microphone, and network boot options |
| Increased extraction size limit | Increased maximum extraction size limit to 128 GB, enabling larger data handling |

---

## [5.7.4](/docs/mdkiosk-linux/release-notes/release-notes#574)

| 24 July, 2025 | Release focused on Kiosk Desktop 3 & Kiosk Mini 4 hardware |
| --- | --- |
| **Features** |  |
| Support for new hardware models | Added support for the Kiosk Desktop 3 and Kiosk Mini 4 hardware models |

---

## [5.7.3](/docs/mdkiosk-linux/release-notes/release-notes#573)

| 11 December, 2024 | Release focused on deleting infected files, adjusting screen brightness and bug fixes |
| --- | --- |
| **Features** |  |
| Delete infected files | Infected files can now be deleted from scanned media at the end of a session |
| Screen brightness control | Added ability to adjust the brightness of the screen |
| **Fixed** |  |
| Sanitized/redacted files in media manifest | Corrected sanitized/redacted file handling to allow modified files through Media Firewall or Media Validation Agent |
| Volume License download | Fixed unusual circumstances where Kiosk would fail to apply an updated license |
| Support package retrieval | Improved support package generation to ensure it can be retrieved consistently |

---

## [5.7.2](/docs/mdkiosk-linux/release-notes/release-notes#572)

| 10 September, 2024 | Release focused on enabling L2100 and Mini 12 hardware |
| --- | --- |
| **Features** |  |
| Support for new form factors | Added support for the Mobile (L2100) and Mini (Mini 12) form factors |
| **Fixed** |  |
| Encrypted media handling | Switched Kingston & Ironkey unlock support to be configurable (disabled by default) |
| UI visibility | Re-adjusted the UI for better usability for the Mobile and Mini |

---

## [5.7.1](/docs/mdkiosk-linux/release-notes/release-notes#571)

| 7 August, 2024 | Release focused on enhancing usability |
| --- | --- |
| **Fixed** |  |
| File scan size limitation | Increased the capability for scanning files up to 32GB |
| Management enrollment | Optimized the enrollment process to synchronize settings more efficiently |
| Screensaver | Simplified the screensaver to avoid any misperception of an actual scan running |
| Session prompt title length | Increased the maximum allowed length for configuring Session Prompt titles |

---

## [5.7.0](/docs/mdkiosk-linux/release-notes/release-notes#570)

| 11 June, 2024 | Release focused on file selection in Scan workflow, enable L1002 hardware, and bug fixes |
| --- | --- |
| **Features** |  |
| File selection in the Scan workflow | Modified the `Scan` workflow to allow users the ability to select files to process |
| Support for Dell 7420 | Added support for the new L1002 hardware model |
| **Fixed** |  |
| Health status display | Corrected health status information to show Managed File Transfer connection status when the workflow is enabled |
| Device removal detection | Covered specific instances where scanned media removal were not detected |
| Expired license on startup | Removed hang encountered when Kiosk starts up with an expired license |
| syslog message logging | Adjusted syslog messages from `Notice` to `Informational` and modified message content |

---

## [5.6.2](/docs/mdkiosk-linux/release-notes/release-notes#562)

| 29 April, 2024 | Release focused on user selectable workflows, customized session information input, label printer support, and syslog. |
| --- | --- |
| **Features** |  |
| User selectable workflows | Converted `Operating Modes` into `Workflows` that users can select per session |
| Customized session information | Converted `User Identification` questions into customizable fields to prompt a user for information specific for the session |
| Label printer | A Brother QL-1100 printer can be used to print out a label containing essential session information tied to the scanned media |
| syslog | Support for configuring a remote syslog server for messages to be delivered to |
| Soft reset | Ability to reboot the Kiosk to refresh internal components without resetting the unit to factory settings |
| **Fixed** |  |
| License issue reporting | Corrected health status information that would incorrectly display a license download error when the issue had already been resolved. |
| Intermittent onboarding connection failure | Stability fixes around onboarding to a management server |
| Archive size limitations | Further increased the capability for scanning larger archives |

---

## [5.5.3](/docs/mdkiosk-linux/release-notes/release-notes#553)

| 29 January, 2024 | Patch focused on new L1001 model |
| --- | --- |
| **Features** |  |
| Support for Dell 7410 | Added support for the new L1001 hardware model |

---

## [5.5.2](/docs/mdkiosk-linux/release-notes/release-notes#552)

| 14 September, 2023 | Patch focused on preparing for future changes |
| --- | --- |
| **Fixed** |  |
| `My OPSWAT` integration | Preparation for supporting future `MY OPSWAT` management releases |
| Media Manifest | Adjusted media manifest content to support expanded validation details |

---

## [5.5.1](/docs/mdkiosk-linux/release-notes/release-notes#551)

| 14 August, 2023 | Release focused on bug fixes and stability |
| --- | --- |
| **Fixed** |  |
| Copy-to media and OMVA | Fixed issue with copy-to media being only allowed once via OMVA |
| Island mode stability | Enhanced error handling around particular Island mode usage |
| Upgrade hang | Corrected a hang seen when upgrading from older Kiosk versions |
| Support package generation | Patched various scenarios where the support package was not being generated |
| Hardware integrity check | Adjusted integrity check for L1001 models |

---

## [5.5.0](/docs/mdkiosk-linux/release-notes/release-notes#550)

| 30 March, 2023 | Release focused on Island mode, scan display enhancements, and bug fixes |
| --- | --- |
| **Features** |  |
| Island mode | New configuration mode that enables the ability to manage Kiosks that do not have a direct network connection to Central Management |
| Beta support for My OPSWAT | Enabled ability to preview managing a Kiosk from a `My OPSWAT` account |
| **Fixed** |  |
| Configuration options | Updated the look and feel of the configuration |
| More visible blocked reasons | Files that are too large to scan or encrypted are now shown in results |
| Scan progress display | Added displaying last file scanned to show current progress of a session |

---

## [5.4.0](/docs/mdkiosk-linux/release-notes/release-notes#540)

| 12 December, 2022 | Release focused on Evaluation mode, stability improvements and bug fixes |
| --- | --- |
| **Features** |  |
| Evaluation mode | Kiosks will now ship with Evaluation mode enabled by default. Evaluation mode is a trial period that allows users to experience Transferring files to a secondary media without the need for an active connection to Central Management. |
| System health status | System health status can be viewed per instance in Central Management's inventory list |
| Media Manifest cert validation | Media manifest certificates are validated upon upload to ensure correct operation |
| View password input for encrypted drives | Added ability to view the input for a password before unlocking an encrypted drive |
| **Fixed** |  |
| Kiosk startup | Improved the engine startup process stability when Kiosk is first turned on |
| Onboarding to Central Management | Revised Kiosk's ability to discover a Central Management with the hostname value provided |
| File size limitations | Increased the capability for scanning larger files and archives |
| Copying to removable hard disks | Fixed the ability to copy files to a removable hard disk |
| Ethernet settings & upgrades | Fixed issue where configured ethernet settings were not maintained through a firmware upgrade |
| Destination media warnings in Windows | Corrected issue where after copying files over, Window alerted that the destination media needed to be scanned and fixed |
| On-screen keyboard input | Fixed issues where input could not be deleted or text was inserted in incorrect positioning |

---

## [5.3.3](/docs/mdkiosk-linux/release-notes/release-notes#533)

| 1 November, 2022 | Patch addressing Ethernet connection issue |
| --- | --- |
| **Fixed** |  |
| Ethernet connection | Corrected issue where an Ethernet connection could not be detected or configured |

---

## [5.3.2](/docs/mdkiosk-linux/release-notes/release-notes#532)

| 27 September, 2022 | Patch focused on support for new L1001 model and internal stability fixes |
| --- | --- |
| **Features** |  |
| Support for Dell 7400 | Added support for the new L1001 hardware model |
| **Fixed** |  |
| ClamAV startup failure | Corrected issue where ClamAV would fail to start up at boot and cause the Kiosk to hang |

---

## [5.3.1](/docs/mdkiosk-linux/release-notes/release-notes#531)

| 11 April, 2022 | Patch focused on NetWall USG support and on-board process enhancement |
| --- | --- |
| **Features** |  |
| Support for uploading files to Vault via NetWall USG | Added ability to upload files via a NetWall Unidirectional Security Gateway to a Vault server |
| **Fixed** |  |
| On-board process | Enhanced the initial on-boarding process under-the-hood and reduce any issues with engines starting up |

Info

MetaDefender Kiosk Linux supports NetWall version 4.1.0+

---

## [5.3.0](/docs/mdkiosk-linux/release-notes/release-notes#530)

| 27 January, 2022 | Release focused on Vault integration and internal improvements |
| --- | --- |
| **Features** |  |
| Transfer files to Vault mode | Additional transfer mode that allows users to copy files to a Vault server |
| **Fixed** |  |
| System startup process | Enhanced the startup process to complete faster |
| Configuration save to apply | Modified configuration settings to require saving changes to apply to a Kiosk instance |

Info

MetaDefender Kiosk Linux supports Vault version 2.1.10+

---

## [5.2.0](/docs/mdkiosk-linux/release-notes/release-notes#520)

| 13 December, 2021 | Release focused on Transfer mode, UI updates, and expanding language & media support |
| --- | --- |
| **Features** |  |
| Transfer files to USB mode | Configuration can enable users to select files and copy allowed files to a secondary USB media |
| User Identification | When enabled, at the start of a session, users can input information about themselves to later be included in reports (e.g. Name, Email, Additional Info) |
| Personal Data Detection | DLP engine detects any visible credit card\social security numbers in files |
| SD Card & Disc scanning | Expanded support to allow scanning SD Cards, Compact Flash, & CD/DVD media |
| UI/UX refresh | - Added support for L3001 - Scan detail result view updated - Added Arabic and Hebrew languages, along with RTL view support |

---

## [5.1.0](/docs/mdkiosk-linux/release-notes/release-notes#510)

| 28 September, 2021 | Release focused on downloading updates from Central Management |
| --- | --- |
| **Features** |  |
| Updates from Central Management | Enhanced Kiosk's ability to only obtain updates from the Central Management it is connected to |

Info

MetaDefender Kiosk Linux requires a Central Management version 7.18+

---

## [5.0.2](/docs/mdkiosk-linux/release-notes/release-notes#502)

| 22 July, 2021 | Patch focused on minor configuration change |
| --- | --- |
| **Fixed** |  |
| Zero-day Prevention configuration | Added ability to enable\disable Zero-Day Prevention |

---

## [5.0.1](/docs/mdkiosk-linux/release-notes/release-notes#501)

| 7 July, 2021 | Initial release of the MetaDefender Kiosk Linux |
| --- | --- |
| **Features** |  |
| Central Management support | Kiosk Linux is solely configured and monitored from Central Management (v7.16+) |
| Process USBs | Can process USB media and some select encrypted USBs |
| Threat Detection \ Rootkit Detection | 5 or 10 AV engines to detect malware and scan the boot sector of inserted media |
| Zero-Day Prevention | CDR engine outlines the active content existing in files |
| Vulnerabilities | Vulnerability engine detects any known CVEs associated with scanned binaries |
| Supply Chain Risk | Logic to detect the origin country of an executable and block if the country is on the configured forbidden list |
| Automatic updates | Kiosk Linux will automatically update itself when a new version is released. Updates can additionally be configured to be applied during specific hours to best adhere to hours of operation. |
