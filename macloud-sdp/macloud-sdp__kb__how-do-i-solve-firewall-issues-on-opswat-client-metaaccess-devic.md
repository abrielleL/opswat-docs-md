<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-solve-firewall-issues-on-opswat-client-metaaccess-devic -->

# How do I solve Firewall issues on MetaDefender Endpoint/MetaDefender IT Access devices?

This article applies to the current MetaDefender IT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

Users running MetaDefender Endpoint on one or more Windows, macOS or Linux devices may occasionally see MetaDefender IT Access device compliance warnings/flags related to their various associated Firewall products, although this depends entirely on policy configuration.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Firewall**.

## [MetaDefender IT Access Compliance Warning: Firewall Is Disabled](/docs/macloud-sdp/kb/how-do-i-solve-firewall-issues-on-opswat-client-metaaccess-devic#metadefender-it-access-compliance-warning-firewall-is-disabled)

1. Turn on the firewall of your preferred firewall product, following the relevant vendor guidelines.

Popular guidelines can be found:

- [Here](https://support.microsoft.com/en-us/help/4028544/windows-10-turn-windows-defender-firewall-on-or-off), for Windows Defender Firewall.
- [Here](https://support.apple.com/en-us/HT201642), for macOS Firewall.
- [Here](https://www.tecmint.com/start-stop-disable-enable-firewalld-iptables-firewall/), for Linux Firewall.

2. Open **MetaDefender Endpoint.**
3. Once the app is running, click/right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

Pro Tip:

To complete Step 3 on **Linux** devices, please navigate to **MetaDefender IT Access** **Console>Inventory>Devices**, select the box alongside the device for which you’d like to run the action and then, from the **Actions** drop-down menu in the top right-hand corner of the screen, select **Compliance Check**, as illustrated below.

4. Check under **MetaDefender IT Access Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Firewall** again.
5. If you have switched on your firewall but the problem persists, please follow the instructions below to contact **OPSWAT Support**, providing screenshots to show your Firewall’s enabled status, as well as MetaDefender Endpoint version details for the device/s reporting the error.

Support:

If you have followed the instructions above, and or the relevant linked guidelines, but **Continue To Experience Firewall Issues On Your** **MetaDefender Endpoint / MetaDefender IT Access** **Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
