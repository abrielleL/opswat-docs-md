<!-- source: https://www.opswat.com/docs/mddrive/release-notes/release-notes -->

# MetaDefender Drive v4.4.11

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

|  |  |
| --- | --- |
| **Released on** **Oct 29, 2026** | This release includes new features, improvements, bug fixes, and known issues. |

**New Features**

- **Threat Removal – In-Place Quarantine:** MetaDefender Drive can quarantine detected files in place during both Bare Metal and In-Session scans. Quarantined files stay on the source volume and can be restored when needed.

  - See [Quarantine Potential Threats In-Place](https://www.opswat.com/docs/mddrive/process/quarantine-potential-threats-in-place).
  - The [forensic collection](https://www.opswat.com/docs/mddrive/process/collect-forensic-data-from-a-windows-computer) now includes quarantined files, keeping a complete record of quarantined content.
- **Central Management enrollment from Kiosk:** Any MetaDefender Drive can be enrolled with OPSWAT Central Management through MetaDefender Kiosk when plugged in. See [Enroll MetaDefender Drive with Central Management via Kiosk](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-kiosk).
- **Scan Auto Run:** Administrators can choose Full Scan or Smart Scan to run automatically on system boot. See [Preferences → Auto Run](https://www.opswat.com/docs/mddrive/configuration/preferences-----auto-run).
- **In-Session works out of the box:** A drive pre-configured with an ignition file applies Central Management enrollment, one-time password authorization, and Wi-Fi settings when started In-Session, matching the Bare Metal experience.
- **Smart Scan for In-Session:** Operators can run Smart Scan during an In-Session scan, bringing In-Session to parity with Bare Metal scanning options. See [Perform In-Session Scans](https://www.opswat.com/docs/mddrive/process/processing-your-device-with-metadefender-drive-in-session).

**Improvements**

- **FileType Analysis setting:** FileType Analysis is now a separate setting from Archive Handling and can run on its own. Archive Handling requires FileType Analysis, so it is selected and locked while Archive Handling is on. See [Preferences → FileType Analysis and Archive Handling](https://www.opswat.com/docs/mddrive/configuration/preferences---archive-handling).
- **Scan time estimate:** The remaining time adjusts gradually as workload is discovered, rather than jumping in large increments, giving a more reliable indication of when the scan will complete.
- **Low-spec activation:** Machines with 4 GB of RAM or less are no longer blocked from activating a MetaDefender Drive license.
- **Download progress feedback:** Transfer speed and estimated time remaining are shown during downloads, so operators know the download is progressing.
- **License error clarity:** A license activation failure now names its cause (wrong key, date mismatch, firewall block, or a server-side error with its HTTP code) instead of a single generic message.
- **Update check indicator:** The "Checking for new update..." screen shows a progress indicator during the post-install check.
- **Selective report removal:** Administrators can select and remove individual reports instead of deleting all stored reports at once.
- **Report sync errors:** When a report fails to reach OPSWAT Central Management, hovering over the warning icon in the report list shows the reason for the failure.
- **Reporting totals:** Reports in OPSWAT Central Management include more information, including totals, so administrators can answer audit questions directly from the report.
- **Additional In-Session hardware information:** In-Session now collects additional host inventory, including domain membership and installed software, giving air-gapped environments more visibility.
- **In-Session device report:** Device inventory and vulnerability data collected during a Smart Touch In-Session scan is improved and available in OPSWAT Central Management through the reports API.
- **Smart Scan engines:** Smart Scan shows all licensed anti-malware engines immediately after enrollment, without manual reconfiguration.
- **USB speed alert:** When MetaDefender Drive is connected through USB 2.0 while USB 3.0 is available, users are told they can scan faster by switching ports.

**Bug Fixes**

- **Full scan interruption:** A full scan that encounters a service interruption no longer skips the remaining files, so scan results reflect the complete drive contents.
- **Ghost session error:** Reinserting a MetaDefender Drive after removal no longer shows a false "already running" message caused by processes that did not exit when the drive was unplugged.

**Known Issues**

- **Restore not shown in Central Management action logs:** Windows stores the computer's hardware clock in local time, while MetaDefender Drive reads it as UTC. If the computer last ran Windows in a time zone ahead of UTC, action logs for files restored from **Preferences → In-Place Quarantine** carry a future timestamp and may not show in OPSWAT Central Management. The restore itself is not affected.
- **In-Session quarantine fails with Microsoft Defender Real-Time Protection:** Real-Time Protection may remove an infected file before In-Session can quarantine it, so the quarantine fails. Temporarily turn off Real-Time Protection before the scan, and turn it back on afterward. See [Quarantine Potential Threats after an In-Session Scan](https://www.opswat.com/docs/mddrive/process/quarantine-threats-in-session-scan).
