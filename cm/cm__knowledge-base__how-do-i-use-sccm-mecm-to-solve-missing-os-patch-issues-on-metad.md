<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-use-sccm-mecm-to-solve-missing-os-patch-issues-on-metad -->

# How do I use SCCM/MECM to solve Missing OS Patch issues on MetaDefender Endpoint/My OPSWAT Central Management managed Windows devices?

> **Check Your Product:**
>
> This article applies to the Microsoft Endpoint Configuration Manager, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

Users running MetaDefender Endpoint on one or more Windows devices may occasionally see My OPSWAT Central Management device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches**.

> **Pro Tip:**
>
> Malware is frequently designed to exploit the vulnerabilities in outdated applications and operating systems in order to gain entry to and infect a system.
>
> This is why keeping your operating system, OS security patches and all associated apps up-to-date is an essential element of risk reduction in cyber-security.
>
> One way to ensure that the OS patches on your Windows devices are kept up-to-date is to configure Microsoft Endpoint Configuration Manager (MECM), previously known as Microsoft System Center Configuration Manager (SCCM).
>
> MECM/SCCM is a software management suite designed to streamline the deployment of updates and patches across networks of Windows computers.

To remediate Missing OS Patch related device compliance issues on your managed Windows devices, please follow the instructions for configuring the Microsoft SCCM below.

1. Check whether MECM is running on your device by opening the Windows **Start** menu, searching for **Task Manage**r and launching it.

![](https://uploads.developerhub.io/prod/1yda/fzn7zmh4x1edfhmo41npm88vsdwtv4qovnwwjla2tr4ahsz24pih0z8eiiiq0sxc.png)

2. In **Task Manager**, expand the **Details** tab, then search for **CcmExec.exe**. If you cannot find it, contact your administrator to remediate the issue.

![](https://uploads.developerhub.io/prod/1yda/uebw5ocw2ehlo11ooargn8ibhsm9bua3l5y40zxu5sj890ka2f5pg3esidzpplsl.png)

3. Next, you can install all missing patches on the device by going to the **Start** menu, then searching for **Microsoft System Center** and launching **Software Center**.

![](https://uploads.developerhub.io/prod/1yda/5s7dun42aez1d5a1jkv6vekt4wkmtm049a4wz1stam3d6evwrym3vb0je84qnot1.png)

4. Inside the **Software Center** app, click on the **Updates** tab in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/i8fcg9hxsz4cv2afqsc9kchxlvinap2p1f3apo2mkyaenhrisnkp6yxocdp9tgf6.png)

5. On the **Updates** page, click **Install All** to install all missing OS security patches.

![](https://uploads.developerhub.io/prod/1yda/3cuk36wt4vccyvukdk6upcqvpkz4xa6r8m4o447dl12c6bgjxkoosiz41wekumfr.png)

6. **Restart** your device if prompted to do so.
7. Open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **My OPSWAT Central Management**, then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/1yda/30ih0w5a5he7wmh773ctnwthjavt0ljwfdl4f2ysrks20uqhukxt0giwfh8iowqn.png)

8. Once the app is running, right-click on the MetaDefender Endpoint tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/1e98k2b7n7iqyznxdckknnzdx7lsqlzpglqyg2m7fw95drz82chmlw1xc3yqdlw3.png)

> **Pro Tip:**
>
> To remediate Missing OS Patch related device compliance issues on your managed Windows devices without MECM, please read [How do I use Windows Update Agent to solve Missing OS Patch issues on MetaDefender Endpoint/MetaDefender IT Access managed Windows devices?](https://www.opswat.com/docs/cm/knowledge-base/how-do-i-use-windows-update-agent-to-solve-missing-os-patch-issu)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management Managed Windows Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
