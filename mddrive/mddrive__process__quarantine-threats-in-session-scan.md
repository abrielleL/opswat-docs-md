<!-- source: https://www.opswat.com/docs/mddrive/process/quarantine-threats-in-session-scan -->

# Quarantine Potential Threats after an In-Session Scan

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Configure Quarantine Settings for MetaDefender Drive In-Session](/docs/mddrive/process/quarantine-threats-in-session-scan#configure-quarantine-settings-for-metadefender-drive-in-session)

Quarantine behavior is controlled by two checkboxes in **Settings → Enable Quarantine**. Both are unchecked by default. These settings sync from Central Management and persist across reboots.

1. Open **Settings → Enable** **Quarantine**.
2. Check **Enable Quarantine** to activate the quarantine step after each scan. While this checkbox is off, **Automatically quarantine detected files** is greyed out and cannot be changed.
3. Check **Automatically quarantine detected files** to quarantine all detected threats without a manual confirmation step.
4. Save your changes.

## [Quarantine Process](/docs/mddrive/process/quarantine-threats-in-session-scan#quarantine-process)

When **Enable Quarantine is ON **and **Automatically quarantine detected files is OFF**, a **Quarantine detected files** pop up runs right after the scan finish, before the report is generated, confirming if user wants to quarantine the infected files.

User will

- **Leave the detected threats as they are** by selecting nothing and clicking **Skip** button, ending up threats will not be quarantined and result into a normal scan report.
- Or** Agree with quarantine process** by selecting detected files or select them all, then clicking **Quarantine (x)** button.

The **Quarantine detected files** pop up will not appear if **Enable Quarantine is ON **and **Automatically quarantine detected files is ON, **and the Quarantine process will be run automatically after any threats detection.

The scan screen replaces the processing status with **Quarantining x (counter) blocked files** displays a separate progress bar, and shows the path of the file currently being processed.

When **Automatically quarantine detected files is OFF** (manual mode), if you cancel while the quarantine step is running, the file currently being processed either completes normally or is rolled back. Files already quarantined before the cancel are kept.

## [Quarantine Results](/docs/mddrive/process/quarantine-threats-in-session-scan#quarantine-results)

When quarantine process finishes, a quarantine results shows up with **Quarantine Files** tab filtering the files have been successfully quarantined.

If you click **Open folder** of a quarantined file a message shows up explaining the reason why file is not accessible.

Quarantine fails when Windows Real-Time Protection is on
> If Microsoft Defender Real-Time Protection is enabled on the scanned device, it may detect and remove an infected file before MetaDefender Drive can quarantine it. The quarantine then fails because the file no longer exists. To quarantine these files, temporarily turn off Real-Time Protection before the scan, and turn it back on afterward.

## [Reopen Quarantine Reports](/docs/mddrive/process/quarantine-threats-in-session-scan#reopen-quarantine-reports)

To review quarantine reports from previous sessions, navigate to Malware Scan, click History to View previous malware scan results.

Click Quarantine tab to view all of the quarantined throughout the history.

From this screen you can restore the quarantined files, follow [Restore Quarantined Threats](https://www.opswat.com/docs/mddrive/process/restore-quarantined-threats) for more.

## [Rescan Behavior](/docs/mddrive/process/quarantine-threats-in-session-scan#rescan-behavior)

When MetaDefender Drive scans a volume that already contains quarantined files, valid quarantine ZIPs in `\OPSWAT_Quarantine\` are skipped and are not reported as threats.
