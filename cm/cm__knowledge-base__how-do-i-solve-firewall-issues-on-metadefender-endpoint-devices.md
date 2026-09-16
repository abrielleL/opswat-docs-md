<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-firewall-issues-on-metadefender-endpoint-devices -->

# How do I solve Firewall issues on MetaDefender Endpoint/My OPSWAT Central Mangement devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

Users running MetaDefender Endpoint on one or more Windows, macOS or Linux devices may occasionally see My OPSWAT Central Management device compliance warnings/flags related to their various associated Firewall products, although this depends entirely on policy configuration.

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Firewall**.

## My OPSWAT Central Management Compliance Warning: Firewall Is Disabled

1. Turn on the firewall of your preferred firewall product, following the relevant vendor guidelines.

Popular guidelines can be found:

- [Here](https://support.microsoft.com/en-us/help/4028544/windows-10-turn-windows-defender-firewall-on-or-off), for Windows Defender Firewall.
- [Here](https://support.apple.com/en-us/HT201642), for macOS Firewall.
- [Here](https://www.tecmint.com/start-stop-disable-enable-firewalld-iptables-firewall/), for Linux Firewall.

2. Open **MetaDefender Endpoint.**
3. Once the app is running, click/right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/l3dg85wcpsj2nqxzi2emun9t5pqcoqblq6yo0d0qhm8l3n1cxwa5g7k4p13i8iw7.png)

> **Pro Tip:**
>
> To complete Step 3 on **Linux** devices, please navigate to **My OPSWAT Central Management** **Console>Inventory>Devices**, select the box alongside the device for which you’d like to run the action and then, from the **Actions** drop-down menu in the top right-hand corner of the screen, select **Compliance Check**, as illustrated below. ![](https://uploads.developerhub.io/prod/1yda/03yrzvo49h07g507chyoijmj28mvl3nkp5xbq8e1ybnuvva0rzk7tpwxf1qmop8h.png)

4. Check under **My OPSWAT Central Management Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Firewall** again.
5. If you have switched on your firewall but the problem persists, please follow the instructions below to contact **OPSWAT Support**, providing screenshots to show your Firewall’s enabled status, as well as MetaDefender Endpoint version details for the device/s reporting the error.

> **Support:**
>
> If you have followed the instructions above, and or the relevant linked guidelines, but **Continue To Experience Firewall Issues On Your** **MetaDefender Endpoint / My OPSWAT Central Management** **Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
