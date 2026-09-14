<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/processing-digital-media -->

# Processing Digital Media

1. Insert the media you want to proceed. The "Processing options" screen will appear on Kiosk UI.
2. Click **Browse** . (If you want to proceed the entire media, click **Process All** and skip to step 5) All detected removable media devices will be displayed.

**Note:** Click **Wipe Media** to remove all data from the detected media and overwrite the entire disk with random data, it will depends on the configuration settings in the MetaDefender Kiosk Management Console.

3. Select the drive, folders, or files (including system files) you want to scan and click **Continue**. Files are displayed on pages for directories with a large amount of files and can be navigated via the Previous Page and Next Page buttons. If a folder contains a large number of files, use the search bar to filter the list instead of scrolling — type part of a file or folder name to show only matching items in the folder you're currently viewing. Matching results support smooth scrolling even with thousands of files, and a **Select All** option lets you select up to 1,000 matching files or folders at once.

Note

Search only looks within the folder you currently have open — it does not search subfolders. Open a subfolder first if the file you need is nested inside it.

**Remark:** Boot Sector in the figure below are the Master Boot Record and Volume Boot Record; they will be proceeded when user click into that option on Kiosk UI.

Image: "Boot Sector" option on Kiosk UI

Note: If the Size Summary is set, users can observe the total size of selected files and folders.

Image: Total selected files and size on Kiosk UI (on the top right corner)

4. The "Processing files" on Kiosk UI displays following information:

   1. How many files scanned by the Kiosk (e.g. allowed files, blocked files, skipped files)
   2. Scanning duration: demonstrated by percentage number on USB icon, when the scanning is completed, the percentage number will be 100%.
   3. The number of files of processed out of the total number files to be processed
   4. Total elapsed time when scanning the files.
   5. Estimated remaining time for completion — Kiosk estimates the time remaining based on the files being scanned (their type and size) and your current engine configuration. The estimate updates periodically while the scan is running, and becomes more accurate over time as Kiosk learns from previous scans performed on that device.
   6. Which MetaDefender Core server (main or backup) is processing the session — shown briefly at the start of scanning

Note

This improved estimation currently applies to scans of USB and SSD media. Other media types — such as CD/DVD, floppy disks, and mobile devices — continue to use the standard estimation method. Scans that include many compressed or archive files (for example, ZIP or self-extracting EXE files) may show a less accurate estimate, since the time needed to expand and scan their contents is harder to predict in advance.

Disable the estimated remaining time

Starting from Kiosk version 4.7.7, administrator can configure to disable the estimated time to complete the scan from Console > Configuration > Kiosk UI > Kiosk Interface > Disable display scan estimation time.

Image: "Processing files" display concept on Kiosk UI

Image: "Processing files" display concept on Kiosk UI

> **Note:** If your organization has more than one MetaDefender Core server configured, Kiosk shows a brief message at the start of each scan confirming which one is handling that session. This message stays on screen for the whole scan, or for a few seconds if the scan finishes very quickly, so you don't miss it. If you cancel the scan, the message disappears immediately.

**Note:** If the inserted media does not have Windows-readable partitions, or if multiple partitions have been disabled in the MetaDefender Kiosk Management Console and the drive has multiple partitions, the **No volumes mounted for the selected device** error message appears and you will be returned to the Idle screen. This error message also appears if MetaDefender Kiosk is unable to read a partition because it is a private or encrypted partition.

5. If at least one encrypted archive is found and encrypted archive decryption is enabled in the MetaDefender Kiosk Management Console, a list of the encrypted files is displayed. See [9.5. Processing Encrypted Archives](/docs/mdkiosk/v4.8.5/operating/processing-encrypted-archives) for additional information.
6. When the scanning process is complete, the Sessions Results screen will be displayed. See [9.6. Viewing the Session Results](/docs/mdkiosk/v4.8.5/operating/viewing-the-session-summary).

**Note:** If you click **Cancel** during scanning process, the Session Results screen will be displayed. If media is removed during scanning, the session will end and return to the idle screen.

## [Wiping Media](/docs/mdkiosk/v4.8.5/operating/processing-digital-media#wiping-media)

Media can be wiped to delete all files on the device and the data hardly recovered even using specialized tools that can read the remnants of files that were previously on the disk.

Multiple removable media devices can be inserted at the wipe option selection screen, after that the wipe selection will be applied to all the removable media device plugged in. Detailed index of the devices will be displayed under each option.

There are four options:

- Format
- 1 Pass Overwrite
- 3 Pass Overwite
- 7 Pass Overwrite

Format is the fastest option, but it simply removes the references to the files on the drive without overwriting those portions of the drive. The 1, 3, and 7 pass wipe options write over the entire drive with differing algorithms, making it much more difficult to retrieve the data that was originally stored on the drive. The United States Department of Defense (DoD) recommends using a 7 pass wipe to clean media. OPSWAT does a low-level sector by sector wipe of the media.

Using the wipe feature will completely erase and reformat ALL information on the device. This includes the partition table and master boot record along with any file system information.

## [Algorithm Details](/docs/mdkiosk/v4.8.5/operating/processing-digital-media#algorithm-details)

| Num. of Passes | Algorithm Steps in Order | Security Standard |
| --- | --- | --- |
| 1 | 1. Pseudorandom | - British HMG Infosec Standard 5, Baseline Standard - Australian Government ICT Security Manual 2014 - Controls |
| 3 | 1. All 1's 2. All 0's 3. Pseudorandom | - U.S. DoD Unclassified Computer Hard Drive Disposition* - U.S. Air Force System Security Instruction 5020** - U.S. Navy Staff Office Publication NAVSO P-5239-26 - British HMG Infosec Standard 5, Enhanced Standard   _We use pseudorandom instead of a fixed pattern as our final pass *_We select 0xFF and 0x00 (reverse of standard), then pseudorandom data instead of a fixed character for our final pass |
| 7 | 1. All 1's 2. All 0's 3. Pseudorandom 4. Pseudorandom 5. Pseudorandom 6. Pseudorandom 7. Pseudorandom | - Bruce Schneier's Algorithm: Applied Cryptography, ISBN 0-471-12845-7 |

Wiping will occur among each media one-by-one with the final results displayed at the end.

Image: Wiping media on 1 removable media device using "3 Pass Overwrite" option

Image" Wipe media results on Kiosk UI

Info

The wiping of CD/DVD is not supported by Kiosk, `Wipe Media` button is not available with this media type.
