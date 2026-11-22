<!-- source: https://www.opswat.com/docs/mddrive/process/restore-quarantined-threats -->

# Restore Quarantined Threats

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Quarantine Records](/docs/mddrive/process/restore-quarantined-threats#quarantine-records)

After being quarantined, **by either Bare Metal or In-Session**, each quarantined file is:

- Moved to `\OPSWAT_Quarantine\` on the same source volume as the original file.
- Stored as a **ZipCrypto-encrypted** ZIP.
- Accompanied by a plain-text Quarantine Record that identifies the original file, with details about **scan results** as well as **ZIP password.**

- Sample content of a quarantine record

  =====================================================================
  METADEFENDER DRIVE QUARANTINE RECORD
  =====================================================================
  MetaDefender Drive quarantined
  2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b
  because malware was detected during the scan.
  The file was removed from its original location and stored in a
  password-protected ZIP in the OPSWAT_Quarantine directory on the
  same volume.
  Keep this record with the quarantined file. It contains the information
  needed to identify and restore the file, even if the MetaDefender Drive
  used to perform the scan is no longer available.
  Original File:
  \testData\theZoo(infected)\theZoo\Duqu2\Duqu2\IOC\2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b
  Quarantined File:
  \OPSWAT_Quarantine\2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b(3).zip
  Scan Result:
  Infected
  Engines Detected:
  8 of 8
  Engine Results:
  AhnLab Infected Trojan/Win32.Duqu
  Avira Infected TR/W32.Spyware
  Bitdefender Infected Trojan.Duqu.E
  CrowdStrike Falcon ML Infected win/malicious_confidence_100
  ESET Infected Win32/Duqu.E trojan
  K7 Infected Trojan ( 004c57c01 )
  OPSWAT Predictive Alin AI Infected Win/malicious_83
  Trellix Infected PWS-Duqu.b
  Scan SHA256:
  2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b
  Quarantined SHA256:
  2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b
  ZIP Password:
  footman-unskilled-sitter
  Scan Type:
  Bare Metal
  Quarantine Time:
  2026-10-29T02:37:32Z
  =====================================================================
  RESTORE INFORMATION
  =====================================================================
  MetaDefender Drive can restore this file from the Quarantine view.
  To restore the file manually, open the ZIP using the password above
  and return the file to its original location:
  \testData\theZoo(infected)\theZoo\Duqu2\Duqu2\IOC\2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b
  =====================================================================
  MACHINE-READABLE INFORMATION
  =====================================================================
  The JSON below contains the same quarantine information for use by
  MetaDefender Drive or other automation.
  JSON_BEGIN
  {
  "version": 1,
  "original_path": "testData/theZoo(infected)/theZoo/Duqu2/Duqu2/IOC/2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b",
  "quarantine_path": "OPSWAT_Quarantine/2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b(3).zip",
  "scan_result": "Infected",
  "scan_sha256": "2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b",
  "quarantined_sha256": "2ecb26021d21fcef3d8bba63de0c888499110a2b78e4caa6fa07a2b27d87f71b",
  "zip_password": "footman-unskilled-sitter",
  "quarantine_time": "2026-10-29T02:37:32Z",
  "engines": [
  {
  "name": "AhnLab",
  "result": "Infected",
  "threat": "Trojan/Win32.Duqu"
  },
  {
  "name": "Avira",
  "result": "Infected",
  "threat": "TR/W32.Spyware"
  },
  {
  "name": "Bitdefender",
  "result": "Infected",
  "threat": "Trojan.Duqu.E"
  },
  {
  "name": "CrowdStrike Falcon ML",
  "result": "Infected",
  "threat": "win/malicious_confidence_100"
  },
  {
  "name": "ESET",
  "result": "Infected",
  "threat": "Win32/Duqu.E trojan"
  },
  {
  "name": "K7",
  "result": "Infected",
  "threat": "Trojan ( 004c57c01 )"
  },
  {
  "name": "OPSWAT Predictive Alin AI",
  "result": "Infected",
  "threat": "Win/malicious_83"
  },
  {
  "name": "Trellix",
  "result": "Infected",
  "threat": "PWS-Duqu.b"
  }
  ]
  }
  JSON_END

User can chose to restore the quarantined files from within the same boot bare metal session or from the same working session. The follow instructions are applicable for files that are quarantined by Bare Metal and In-Session.

Warning

Restoring a file moves a detected threat back to the source volume. Verify that the file poses no risk before restoring it.

## [Restore Quarantined Files from within Bare Metal session](/docs/mddrive/process/restore-quarantined-threats#restore-quarantined-files-from-within-bare-metal-session)

To return a quarantined file to its original location, use the restore workflow in **Settings**.

1. Open **Settings** and navigate to the **In-Place Quarantine** section.
2. Click **Open**. The dialogue appears calculating for quarantine files exist on local disks.
3. **Select the files to restore** using the checkboxes, then click **Restore selected** button if you want to restore the files. *Please note that the total files counted here including all of the quarantined files from all previous scan sessions too.*
4. Confirm the restore with clicking **Confirm** button.
5. Wait for restoration...
6. And when restoration finishes, you can close it

## [Restore Quarantined Files with In-Session](/docs/mddrive/process/restore-quarantined-threats#restore-quarantined-files-with-in-session)

1. From **main screen of In-Session**, click **Malware Scan**, click the **History** icon to view previous malware scan results
2. Click **Quarantine tab**
3. Click a file to view the details
4. Select file/files to restore by the checkboxes and click red **Restore** button
5. **Acknowledge** and **confirm** the warning
6. Quarantined files will be restored back, wait for the process to be done

   In case File Already Exists

   The message will appear when for any reason the extractor finds that files are still there in the original path. Chose **Restore as Copies** or **Keep In Quarantine.**
7. The **Restoration** finishes

## [Restore Quarantined Files from working Windows session](/docs/mddrive/process/restore-quarantined-threats#restore-quarantined-files-from-working-windows-session)

1. From the **OPSWAT_Quarantine folder**, navigate to find the quarantined file.
2. Find the associated quarantine record
3. Make sure the SHA256 are matching
4. Look for the ZIP password
5. Right click the quarantined file, choose to extract with any unarchiver utility available, then fill in the password got from step 4 and hit OK
