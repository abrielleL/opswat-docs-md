<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/release-notes/release-notes-toolkit -->

# MetaDefender Drive Toolkit v3.8.8

|  |  |
| --- | --- |
| **Released on** **Aug 04, 2026** | This release delivers new features, improvements, and bug fixes for MetaDefender Drive Toolkit. |

**New Features**

- **View In-Session Reports in Toolkit Inventory:** Drive Toolkit now shows In-Session scan reports in the Toolkit Inventory, giving security teams unified visibility across all scan types.

**Improvements**

- MetaDefender Drive Toolkit now warns when an enrolled MetaDefender Drive has been tampered with or corrupted, and tells you whether to unenroll or reflash.
- MetaDefender Drive Toolkit now upgrades and relaunches correctly when installed in a folder whose path contains spaces or parentheses.
- Enrolling MetaDefender Drive Toolkit to OPSWAT Central Management no longer requires any additional third-party software to be installed first.

**Bug Fixes**

- Offline definition updates delivered from a flashed drive are now picked up on boot, so Smart Touch devices update over poor networks without consuming bandwidth.
- Flashing errors now show a clear, friendly message instead of a raw internal error, so users understand what went wrong and how to proceed.
- Drives whose partition letter has been removed are remounted automatically instead of appearing damaged or unlicensed, so users can flash and use them without manual disk repair.
- Update checks are blocked while engines are downloading or verifying, so engine definitions no longer restart their download and finish in one pass.
