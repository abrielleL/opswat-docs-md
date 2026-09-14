<!-- source: https://www.opswat.com/docs/mddrive/release-notes/release-notes-v4-4-8 -->

# MetaDefender Drive v4.4.8

|  |  |
| --- | --- |
| **Released on** **Jul 30, 2026** | This release includes new features, improvements, and bug fixes. |

**New Features**

- **Device Inventory:** Capture device inventory information during In-Session scans and share it with My OPSWAT for viewing and export to Asset Discovery tools.

- **MetaDefender Drive Inventory API:** Provides a centralized API for integrating MetaDefender Drive Inventory data into existing data lakes, enabling centralized visibility, reporting, and analysis. This will require newer version of OPSWAT Central Management. Please check [Retrieve account inventory or a specific product inventory.](https://www.opswat.com/docs/cm/direct-instance-management#get-metadefender-drive-scanned-host-list)

**Improvements for MetaDefender Drive**

- Adds a clear UI message informing users that PIN-based BitLocker unlock is not supported on Linux.
- MetaDefender Drive recommends an engine set matched to the machine's processor, USB and memory capacity, so scans run well on lower-specification hardware.
- You can create a new destination folder while choosing where to save a forensic collection, so results can be organized without leaving the workflow.
- Reports now indicate when a scan was a differential scan, so readers understand that only changed files were examined.
- A mistyped OPSWAT Central Management address can now be corrected in place during enrollment, instead of forcing you to retype the entire entry.
- Engines disabled in preferences now stay disabled across every scan type, and hardware recommendations pick only from the engines you allow.

**Improvements for In-Session**

- Every in-session report now records the scan type and final verdict directly, so emails and passports can be generated from any report format without depending on one file being present.
- Support packages now include MetaDefender Drive In-Session logs, so In-Session issues can be diagnosed from a single collected package.

**Improvements for Kiosk Integration**

- Emailed MetaDefender Drive passports now show whether the scan was run in-session or on bare metal, so you can tell the two kinds of result apart.
- Delivers a fully reliable Kiosk Integration experience across airgapped, on-premise, and cloud environments
- The console screen in Kiosk now shows both the Kiosk and MetaDefender Drive Toolkit integration versions, so you can confirm what is installed without digging elsewhere.

**Improvements for Central Management Integration**

- MetaDefender Drive version is reported to OPSWAT Central Management on every connection, so administrators always see the current version rather than the one recorded at enrollment.

**Bug Fixes**

- New MetaDefender Drive units register and unlock with current security codes, so replacement drives can be put into service without being locked out.
- Full scans on large drives now run faster and complete reliably instead of slowing to a halt and reporting internal errors part way through.
- MetaDefender Drive now starts its scan engine reliably and shows a clear message when activation or installation fails, so users know whether it is still starting or genuinely broken.

- In-session scan reports now sync reliably from MetaDefender Drive through the kiosk to central management, so results are not silently lost on upload.
