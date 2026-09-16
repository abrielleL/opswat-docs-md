<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/does-opswat-metadefender-core-support-scanning-txf-files- -->

# Does OPSWAT MetaDefender Core Support Scanning TXF Files?

**Check your version:**

This article applies to MetaDefender Core and is applicable to all MetaDefender Core V5 releases deployed on Windows and Linux systems.

Yes, TXF (Tax Exchange Format) files are supported by OPSWAT MetaDefender Core.

Support for scanning TXF files was introduced starting with **File Type Module version 7.8.0**. If your system is running an earlier version of the File Type Module, TXF files may not be properly recognized or scanned.

**Resolution / Steps**

To ensure TXF files are supported:

1. Verify your current File Type Module version in MetaDefender Core.
2. Update your modules to the latest available version.
3. Confirm that the File Type Module is at **version 7.8.0 or later**.

In order to check the File Type Module status and version, in your MetaDefender Core web UI, navigate to: Inventory > Modules > Utilities > File Type. Make sure the engine is enabled - **Engine status: Active**, and there is a **green checkmark next to Version and Database.**

Modules overview highlighting the File Type engine enabled with version 7.8.1-10393 aligned with its database, last updated on April 15, 2026.

File Type module showing active engine status with version 7.8.1-10393 matching the database, last updated on April 15, 2026.

Keeping your modules up to date is essential to ensure full file type coverage and optimal detection capabilities.

**Additional notes:**

No additional configuration is required once the appropriate module version is installed.

Regular module updates are recommended to maintain support for newly added file formats and improvements.

**Support:**

If you have questions, concerns or issues regarding **MetaDefender** **Core**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
