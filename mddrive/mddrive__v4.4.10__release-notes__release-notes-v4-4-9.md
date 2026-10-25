<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/release-notes/release-notes-v4-4-9 -->

# MetaDefender Drive v4.4.9

View as Markdown Ask ChatGPT about this page Ask Claude about this page

|  |  |
| --- | --- |
| **Released on** **Sep 03, 2026** | This release includes new features, improvements, bug fixes. |

**New Features**

- **Operator Accept Skipped/Threat Risk** Admins can define approved skip reasons so Operators can bypass files or large archives that are unnecessarily delaying a scan, while also pre-approving known safe or false positive files by hash. This helps scans complete faster while keeping skip decisions controlled and consistent.
- **Skip By Hash** Provide ability to skip trusted files by hash, reducing scan time and false-positive overhead.
- **User reports include deleted files** Scan reports now include a dedicated section listing each file that was removed during scanning, with its original path and cryptographic hash included before any boot-sector entries.
- **MetaDefender Drive uses time and TimeZone on Smart Touch** Smart Touch Operator can set the time zone on Smart Touch and keep its clock in step, so scan times and reports carry the correct local time.
- **Get all logs in any support package** A support package collected from any one of MetaDefender Drive, MetaDefender Drive Toolkit, Smart Touch, or MetaDefender Drive In-Session are all included in the SupportPackage, so a single upload is enough to diagnose an issue.
- **Provide posture check on MetaDefender Drive In-Session** MetaDefender Drive In-Session verifies endpoint security posture before scanning, checking EDR, OS updates, and disk encryption in a single workflow.
- **Dedicated workflow for Drive-Kiosk integration** Kiosk Drive Integration is configured and managed under a dedicated workflow and with a new user interface.
- **Centralized Scanning Profile now is applied for In-Session** After enrolled with Drive Toolkit, operator will be prompted for OTP when running Memory and Custom Scans from In-Session. To see how it works, refer to [Centralized Scanning Profile - Unlock in MetaDefender Drive In-Session](/docs/mddrive/v4.4.10/configuration/centralized-scanning-profile-in-session)

**Improvements and Bug Fixes**

- MetaDefender Drive, MetaDefender Drive Toolkit, and Smart Touch now display unified enrollment statuses so customers can instantly see whether their device is managed by Central Management.
- Administrators can push a MetaDefender Drive firmware upgrade from OPSWAT Central Management, so enrolled drives are updated centrally rather than one at a time by hand.
- A support package captured by booting MetaDefender Drive with Smart Touch carries the Smart Touch service logs alongside the drive's own, so a Smart Touch-layer fault can be diagnosed from that one archive.

- Files held inside an archive are reported with the correct verdict, so what a scan says about a compressed container matches what it actually contains.
- Scans that previously stuck at 98% finish normally rather than hanging for extended periods.
- A drive disconnected without shutting down can still be updated in MetaDefender Drive Toolkit: its file system is repaired first, and unreadable files are reported before flashing continues.

- MetaDefender Drive reconnects to OPSWAT Central Management when a lost connection is restored, so drive remains enrolled without manual intervention.
