<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-scan-xdcam-drive-in-kiosk- -->

# How to scan XDCAM Drive in Kiosk?

## [Overview](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-scan-xdcam-drive-in-kiosk-#overview)

MetaDefender Kiosk (4.7.9 or later) now supports Sony XDCAM drives (specifically tested with Sony PDW-U2) and Professional Discs. Due to the unique file system restrictions of XDCAM media, specific handling for manifest files and remediated files has been implemented

## [Prerequisites](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-scan-xdcam-drive-in-kiosk-#prerequisites)

1. Install Sony driver/software (required)

To ensure Windows can correctly recognize the Professional Disc and show full file visibility in Explorer, Sony driver or software may be required to be installed on the Kiosk device. Check your vendor website for more information.

Missing Sony driver or software

Without this Sony software, Windows may show the disc as connected but only display some files (partial visibility), which can impact scanning completeness.

2. XDCAM Drive Device

- XDCAM Drive (Sony PDW-U2) connected via USB
- Sony Professional Disc inserted into the drive

## [Detect and Scan an XDCAM Professional Disc](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-scan-xdcam-drive-in-kiosk-#detect-and-scan-an-xdcam-professional-disc)

**Step 1 -** Prepare the Kiosk machine

- Install Sony XDCAM Drive Software
- Reboot if required by the Sony installer.

**Step 2 (Optional) -** Verify the Windows detection of XDCAM drive

- Exit the Kiosk UI to verify the XDCAM drive in Windows
- Connect the Sony PDW-U2 to the Kiosk machine via USB.
- Insert the Professional Disc into the drive.
- When Windows detected the XDCAM drive, confirm Windows can browse the disc contents

**Step 3 -** Start scanning in MetaDefender Kiosk

- Launch the MetaDefender Kiosk UI.
- Proceed with Kiosk authentication if needed
- When prompted to insert media, plug in the XD CAM Drive media
- Choose the scanning option and proceed the scanning
- Kiosk will start scanning files.

**Step 4 -** Verify expected results

- Once the scan is complete, verify the scan result

## [Additional notes](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-scan-xdcam-drive-in-kiosk-#additional-notes)

1. Manifest file

   - When manifest file is in used, is written to the `General\.OPSWAT` folder (instead of the root `.OPSWAT` folder used for other devices).
   - Kiosk is capable of searching for the manifest file in both the root .OPSWAT and General.OPSWAT folders to validate or reuse manifest files across all device types.
2. Write Restrictions

   - The XDCAM drive does not support writing sanitized or remediated files to XDCAM discs to avoid drive malfunctions or disk ejections caused by non-Sony writing processes.
3. **Manifest generation fails if C:\program.exe exists**

   - If a file literally named `program.exe` is present at the root of the Kiosk machine's `C:` drive, the Sony XDCAM Drive Utility software cannot open, which prevents Kiosk from generating a manifest file on the XDCAM media.
   - **Workaround:** Remove `C:\program.exe` from the Kiosk machine and restart it, then retry the scan.
   - This is a limitation of the Sony XDCAM Drive Utility software itself, not of MetaDefender Kiosk.
