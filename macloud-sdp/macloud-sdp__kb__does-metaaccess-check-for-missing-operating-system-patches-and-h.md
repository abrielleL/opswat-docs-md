<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/does-metaaccess-check-for-missing-operating-system-patches-and-h -->

# Does MetaDefender IT Access check for missing operating system patches and hotfixes?

This article applies to all OPSWAT MetaDefender IT Access product releases deployed on Windows, and macOS systems.

Yes, it does.

MetaDefender IT Access is designed to check the operating systems on each of your managed endpoints for any missing patches or hotfixes.

To do this, OPSWAT uses the relevant operating system’s classification of mandatory and optional patches, where **M andatory** generally means **Critical** or **Severe**.

If missing patches or hotfixes are detected, the MetaDefender IT Access Console will report these missing patches, along with their severity and timestamps, under **Inventory>Devices>Relevant Device>Device Details View>Missing Patches**, as illustrated below.

To remedy a missing patch or hotfix issue, visit the device **Remediation Page**, where you will find remediation requirements as well as a link to detailed remediation instructions.

If no patches or hotfixes are missing, **Patch Management** will show an **Up To Date** status.

Pro Tip:

To configure the frequency of MetaDefender IT Access scans and reports on missing patches, go to **MetaDefender IT Access** **Console>Settings>Global>Device Agents**.

Here, you will find an adjustable time setting under the **Compliance Report** heading, as illustrated in the screenshot below.

Once configured, click **Save** to apply your settings.

Support:

For any queries, concerns or issues regarding **MetaDefender IT Access** **Scanning, Reporting And Remediation Of Missing Operating System Patches And Hotfixes**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
