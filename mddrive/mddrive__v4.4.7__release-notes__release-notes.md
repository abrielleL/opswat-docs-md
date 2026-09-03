<!-- source: https://www.opswat.com/docs/mddrive/v4.4.7/release-notes/release-notes -->

# MetaDefender Drive v4.4.7

|  |  |
| --- | --- |
| **Released on** **Jul 09, 2026** | This release includes new features, improvements, and bug fixes. |
| **New Features** | **Configurable Smart Scan Button:** Allows administrators to create a policy-locked scan button on the Dashboard with preset engines, technologies, and directory types, ensuring operators run only the intended scan configuration without modification — enforcing consistency and reducing scan time. |
| **Improvements and Bug Fixes** |  |
|  | Fixed an issue where the "Last Successful Update" timestamp was incorrectly displayed after offline or Central Management engine updates. It now shows properly, giving operators immediate confirmation that their device definitions are current. |
|  | Fixed an issue where operators could copy incomplete engine packages to Drives. The system now warns them when engines are still updating, avoiding partial deployments in offline environments. |
|  | Fixed an issue specifically affecting the Dell Precision 3660 with Intel I225-V NICs that left scan engines stuck in a "Scheduled" state. |
|  | Fixed an issue where engines could get stuck in a "Scheduled" state on workstations with Intel I225-V NICs. |
|  | Fixed an issue where the kernel intermittently panicked during boot. |
|  | Fixed an issue where a corrupted OS partition could expose the GRUB boot menu on startup; the system now halts immediately to prevent unauthorized bootloader access. |
|  | Confirmed compatibility with Windows Server 2025. |
|  | Fixed an issue where a long-running Live Session scan could crash unexpectedly without user intervention, now ensuring scan stability so sessions complete reliably even during extended multi-hour scans. |
|  | Fixed inaccurate Live Session estimated completion time (for example, jumping from ~30h to ~12h on previously scanned hosts). Scan-time estimates are now reliable for production planning. |
|  | Fixed an issue where not all In-Session scan engines started because engine definitions were removed during download; platform-specific cleanup now runs independently. |
|  | Fixed an issue where an In-Session scan hung at the splash screen, now ensuring scans start reliably. |
|  | Fixed missing user information fields in the Device Passport — blank values now display as "N/A". |
|  | Fixed missing user information and incorrect labels in Passport Reports, now generating accurate and complete reports. |
