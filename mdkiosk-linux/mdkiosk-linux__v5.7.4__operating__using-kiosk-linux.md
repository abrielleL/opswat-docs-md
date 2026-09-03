<!-- source: https://www.opswat.com/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux -->

# Using Kiosk Linux

The Kiosk is ready for use when **Insert Media to Start** is displayed.

If the Kiosk is not in use for some time, an instructional video plays on the screen. Any interaction with the screen returns the Kiosk back to the Insert Media page.

---

## [Workflows](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#workflows)

When multiple Workflows are enabled, inserting media will prompt the user to select the Workflow to use for the session.

---

### [Scan](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#scan)

If only the `Scan` workflow is enabled, inserting media immediately starts a processing session and navigates to the scan progress page.

If multiple workflows are enabled, Kiosk will start a processing session when the user selects `Scan`.

All contents of the media are scanned in this workflow; no file selection is allowed.

The progress bar at the top of the screen indicates current elapsed time and estimated remaining time for processing.

The middle of the screen shows the total Allowed and Blocked file counts and are updated as file results are identified. Under the total file counts, detailed file counts for Threat Detection, Zero-day Protection, Personal Data Detection, Vulnerabilities, and Supply Chain Risk update as the scan proceeds. Clicking any of these boxes after a scan completes opens the Scan Details page listing each file identified by the selected category.

**Threat Detection** - Total number of infected files found

**Zero-day Protection** - Total number of files where active content was detected. In a Scan and Copy workflow, Kiosk automatically copies a sanitized version of the file to the destination.

**Personal Data Protection** - Total number of files found with potentially sensitive data such as Social Security or Credit Card numbers

**Vulnerabilities** - Total number of CVE vulnerabilities identified in files

**Supply Chain Risk** - Total number of files blocked due to Country of Origin settings

After processing completes, [Viewing Scan Details](https://docs.opswat.com/mdkiosk-linux/operating#viewing-scan-details) can be done.

---

### [Scan and Copy to USB](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#scan-and-copy-to-usb)

`Scan and Copy to USB` workflow allows the user to select specific files to scan and copy to another USB drive. After inserting the source media device, the user will be presented with a screen alerting them to select files to copy:

Tap the **Select Files** button to select the files to scan and transfer to the destination media.

Kiosk will automatically keep track of the number of files selected and their total size so that you can choose a destination media with a large enough capacity to store these files. After clicking **Next** the user is prompted to insert the Destination Media.

After inserting Destination Media:

The user will be presented with an error message if there is an issue with the Destination Media such as not enough capacity or if the media is not writeable.

Tap **Process Files** to begin scanning and transferring the files. Kiosk alerts the user that the Destination Media will be wiped before scanning. This is to ensure only the scanned files exist on the media after the session completes.

Warning

The entire destination media's content will be gone after the wipe. If the destination media is encrypted, it no longer will be. If the destination media has multiple partitions, all partitions will be removed. The media's file system will be set to exFAT.

Tap **Wipe & Continue** to format the Destination Media and continue to the scanning and copying stage. The scanning process is similar to the `Scan` workflow and shows a similar progress and results page that shows the counts of files successfully copied rather than the total Allowed files.

Tapping on the **FILES COPIED** section will show how many modified and unmodified files were copied from this session. Modified means the file was sanitized by Zero-Day Protection or had sensitive data redacted by Proactive DLP, unmodified means the file was copied exactly as it was on the scan device.

After the `Scan and Copy to USB` session completes, the user will find all allowed and modified files copied to their destination media.

---

### [Scan and Copy to MetaDefender Managed File Transfer](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#scan-and-copy-to-metadefender-managed-file-transfer)

`Scan and Copy to MetaDefender MFT` workflow allows the user to select specific files to scan and copy to a guest account on the configured MetaDefender Managed File Transfer server. After inserting the source media device, the user will be presented with a screen alerting them to select files to copy:

Click the **Select Files** button to select the files to scan and transfer to the destination media.

After selecting your files and clicking **Next** the scan will begin immediately. The scanning process is similar to the `Scan` workflow and shows a similar progress page that shows the counts of files successfully copied to the Managed File Transfer server rather than the total Allowed files.

After a successful scan, you will be given your Managed File Transfer Access Code that you can use to log into the Managed File Transfer server to retrieve your files. The code is hidden by default for security purposes. Tap the icon next to the hidden code to reveal. There is also a QR code for an email template to send this Managed File Transfer Access Code to yourself or anyone else that needs access to these files. Tapping the screen takes you back to the Session Results.

If you need to see the Managed File Transfer Access Code page again, tap the **View Managed File Transfer details** button on the bottom of the Session Results page.

---

## [Viewing Scan Details](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#viewing-scan-details)

After processing completes, a button to **View scan details** will appear.

Tapping **View scan details** displays details on threats, vulnerabilities, zero day protection, personal data protection and blocked files due to country of origin that were detected during processing.

Infected files may be removed from the drive. Tapping the **Remove File** button will remove the selected infected file, while tapping the **Remove All** button will remove all infected files on the drive.

Info

Infected boot sectors cannot be removed.

Deleting files from encrypted drives is not currently supported.

Tapping on the header at the top of the file list displays a drop down where you can access the other scan details:

Tapping **Exit and Eject** ends the processing session and the media can be removed. Kiosk Linux goes back to the **Insert Media to Start** page and another scan can be started.

---

## [Control Menu](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#control-menu)

In the top right corner of the screen exists a menu to control additional aspects of the Kiosk.

### [Display](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#display)

The setting controls the brightness of the display.

Drag the control to the left to lower the brightness, drag the control to the right to increase the brightness.

### [About this Kiosk](/docs/mdkiosk-linux/v5.7.4/operating/using-kiosk-linux#about-this-kiosk)

Selecting this option brings up informational details of the Kiosk.
