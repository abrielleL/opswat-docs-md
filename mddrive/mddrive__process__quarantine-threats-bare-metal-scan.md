<!-- source: https://www.opswat.com/docs/mddrive/process/quarantine-threats-bare-metal-scan -->

# Quarantine Potential Threats after a Bare Metal Scan

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

After a scan completes, MetaDefender Drive can move detected threats to an encrypted quarantine area on the same source volume. This page describes how to enable quarantine, what happens during the quarantine step, how to interpret quarantine results, and how to restore quarantined files.

## [Configure Quarantine Settings](/docs/mddrive/process/quarantine-threats-bare-metal-scan#configure-quarantine-settings)

Quarantine behavior is controlled by two checkboxes in **Settings → Preferences → Quarantine Files**. Both are unchecked by default. These settings sync from Central Management via vpack and persist across reboots.

1. Open **Settings → Preferences** and click **Edit** on the **Quarantine Files** card.
2. Check **Enable Quarantine** to activate the quarantine step after each scan. While this checkbox is off, **Automatically quarantine detected files** is greyed out and cannot be changed.
3. Check **Automatically quarantine detected files** to quarantine all detected threats without a manual confirmation step.

   **In-Place Quarantine Card with options in Preferences**
4. Save your changes.
5. The **Open** button in In-Place Quarantine card will allow you to **restore the quarantined files** from an available record. Follow [Restore Quarantined Threats](/docs/mddrive/process/restore-quarantined-threats) for more.

## [Quarantine Process](/docs/mddrive/process/quarantine-threats-bare-metal-scan#quarantine-process)

When **Enable Quarantine is ON** and **Automatically quarantine detected files is OFF**, a **Quarantine detected files** pop up runs right after the scan finish, before the report is generated, confirming if user wants to quarantine the infected files.

User will

- **Leave the detected threats as they are** by selecting nothing and clicking Skip button, ending up threats will not be quarantined.
- Or **Agree with quarantine process** by selecting detected files or select them all, then clicking **Quarantine selected** button.

The **Quarantine detected files** pop up will not appear if **Enable Quarantine is ON** and **Automatically quarantine detected files is ON,** and the Quarantine process will be run automatically after any threats detection.

The scan screen replaces the processing status with **Quarantining files... x (counter) of y (total)**, displays a separate progress bar, and shows the path of the file currently being processed.

Each quarantined file is:

- Moved to `\OPSWAT_Quarantine\` on the same source volume as the original file.
- Stored as a **ZipCrypto-encrypted** ZIP.
- Accompanied by a plain-text Quarantine Record that identifies the original file.

When **Automatically quarantine detected files is OFF** (manual mode), if you cancel while the quarantine step is running, the file currently being processed either completes normally or is rolled back. Files already quarantined before the cancel are kept.

## [Quarantine Results](/docs/mddrive/process/quarantine-threats-bare-metal-scan#quarantine-results)

When quarantine process finishes, a quarantine results shows up.

| Result | Meaning |
| --- | --- |
| Success | The file was quarantined successfully. |
| Success – File changed since scan | The file was quarantined, but its contents changed between the scan and the quarantine step. |
| Failed | The file could not be quarantined. A reason is shown alongside the result. |
| Not Quarantined | The file was identified as a threat but was not processed by the quarantine step. |

Each file processed during the quarantine step receives one of the following results. These are shown in the **Quarantined** column of the scan report and in the **Quarantine Files** tile.

### [Hibernated volumes](/docs/mddrive/process/quarantine-threats-bare-metal-scan#hibernated-volumes)

If the source volume belongs to a Windows installation that was not fully shut down, the file cannot be moved and the Failed result includes one of the following messages:

- **Windows is hibernated or Fast Startup is on. Shut down Windows fully, then scan again.**
- **...then try again.**

Shut the target machine down fully — not using Hibernate or Fast Startup — then boot MetaDefender Drive and scan again before attempting to quarantine.

## [Rescan Behavior](/docs/mddrive/process/quarantine-threats-bare-metal-scan#rescan-behavior)

When MetaDefender Drive scans a volume that already contains quarantined files, valid quarantine ZIPs in `\OPSWAT_Quarantine\` are skipped and are not reported as threats.
