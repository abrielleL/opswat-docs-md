<!-- source: https://www.opswat.com/docs/mdmediafirewall/release-notes/release-notes -->

# Release Notes

## [4.0.1](/docs/mdmediafirewall/release-notes/release-notes#401)

| 20 May, 2026 | Release focused on My OPSWAT Central Management support, Port Alarm Protection and bug fixes |
| --- | --- |
| **New Features** |  |
| Remote Management via CM10 | Enables the Media Firewall to be configured remotely through My OPSWAT Central Management (CM10). This includes support for remote configuration upload, writeback and syslog settings, certificate management, and enhanced session reporting. |
| Port Alarm Protection — USB Tamper Detection with FOB Monitoring | Enhances the Media Firewall's tamper detection by adding FOB monitoring to detect when blocking USB fobs are removed from host ports, triggering Alert Mode with visual (red LEDs), audible (speaker alarm), and remote notifications (My OPSWAT health report, syslog). This feature also supports keyboard and mouse passthrough, allowing HID peripherals to remain connected to the host without triggering false alarms. |
| **Bug fixes** |  |
| Bug Fixes & Stability Improvements | Several bug fixes have been included to improve overall performance and stability, covering areas such as boot time optimization, media detection reliability, firmware upgrade compatibility, storage validation, logging improvements, and configuration persistence. |
| **Known issues** |  |
| LED status displays incorrectly after removing and reinserting OTG device | The LED status may freeze or display incorrectly after unplugging and re-plugging the OTG cable following a scan; in some rare cases the MMF storage also does not properly eject after media removal. |
| Device version not updated in CM10 after MMF upgrade via USB | After upgrading MMF via USB while enrolled in CM10, the device version shown in CM10 may not update even though the upgrade completes successfully. |

---

## [3.4.0](/docs/mdmediafirewall/release-notes/release-notes#340)

| 28 April, 2025 | Release focused Port Alarm Protection, syslog functionality, and bug fixes |
| --- | --- |
| **Features** |  |
| Port Alarm Protection | Media Firewall now has the ability to monitor its connection to a Host. When connection is lost, the Media Firewall will alert to notify administrators via syslog. |
| syslog support | Support for configuring a remote syslog server for delivering system event messages |
| **Fixed** |  |
| Copy files to media | Fixed instances where a copied file would sometimes be empty.  Simplified the copy process to no longer require a disconnect from the Host.  The ability to allow copying is now configurable. |
| Internal improvements | Upgraded internal components for further stability and security |

---

## [3.3.0](/docs/mdmediafirewall/release-notes/release-notes#330)

| 6 January, 2025 | Release focused on allowing files to be copied to media and minor adjustments to LED display |
| --- | --- |
| **Features** |  |
| Copy files from host to media | Files can now be copied from a connected host system to the scanned media |
| **Fixed** |  |
| LED display | Changed white to cyan to avoid any confusion in progress display |

---

## [3.2.1](/docs/mdmediafirewall/release-notes/release-notes#321)

| 12 December, 2024 | Release focused on internal improvements for future releases |
| --- | --- |
| **Fixed** |  |
| MMF hardware readiness | Improved internal processes for releasing MMF hardware |

---

## [3.2.0](/docs/mdmediafirewall/release-notes/release-notes#320)

| 30 September, 2024 | Release focused on improving system stability, LED display, & upgrade mechanism |
| --- | --- |
| **Features** |  |
| Multiple manifest support | Added ability to support validating media that contains multiple media manifests |
| **Fixed** |  |
| System hang | Improved system performance to correct irregular media validation hang observed after some use |
| File handling stability | Adjusted file handling to support filenames with different encodings |
| File validation | Revised file categorization that would previously block files that should have been allowed |
| LED display | Modified the power-on sequence and display when an upgrade is performed |
| MyOPSWAT connection | Corrected issue where the connection to management would drop intermittently |
| Online upgrade | Fixed situations where retrieving firmware upgrades from `MyOPSWAT` would fail |
| Update stability | Enhanced the update mechanism for stability in future upgrades |

---

## [3.1.0](/docs/mdmediafirewall/release-notes/release-notes#310)

| 25 September, 2023 | Initial release of the MetaDefender Media Firewall |
| --- | --- |
| Validate media processed by Kiosk | With Media Manifest usage enabled in a Kiosk, the Media Firewall can validate media processed with a Kiosk and expose access to allowed files |
| Central Management | View dashboard statistics, device health, and reports from `MyOPSWAT` |
| Updates | Media Firewall will automatically update itself when a new version is released when setup to connect to the internet.  Optionally, an upgrade package can be applied to systems manually if they are air-gapped. |

Minimum supported Kiosk versions

Windows Kiosk: 4.6.3

Linux Kiosk: 5.5.2
