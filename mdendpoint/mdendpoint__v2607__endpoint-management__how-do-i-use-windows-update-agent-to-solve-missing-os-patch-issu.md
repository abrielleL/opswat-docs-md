<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-use-windows-update-agent-to-solve-missing-os-patch-issu -->

# How do I use Windows Update Agent to solve Missing OS Patch issues on MetaDefender Endpoint/MetaDefender IT-OT Access managed Windows devices?

> **Check Your Product:**
>
> This article applies to the Windows Update Agent, the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

Users running MetaDefender Endpoint on one or more Windows devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **Inventory>Devices>Select your device>Detailed Device Information>Missing Patches**.

> **Pro Tips:**
>
> Malware is frequently designed to exploit the vulnerabilities in outdated applications and operating systems in order to gain entry to and infect a system.
>
> This is why keeping your operating system, OS security patches and all associated apps up-to-date is an essential element of risk reduction in cyber-security.
>
> One way to ensure that the OS patches on your Windows devices are kept up-to-date is to configure the Windows Update Agent accordingly.

To remediate Missing OS Patch related device compliance issues on your managed Windows devices, please follow the instructions for configuring the Windows Update Agent below.

## Windows 10/11

1. Open the Windows **Start** menu, search for **Services** and then **Open** it.

![](https://uploads.developerhub.io/prod/2x2P/cuqxd7sq269v2w8l42vpknzxditoqzhzbwkfmvfiq2tkgjnqp6vor0vpvrwrptfe.png)

2. In the **Services** app, search for **Windows Update** service and, when you find it, double-click on it.

![](https://uploads.developerhub.io/prod/2x2P/eqguolw0bcubcx3h8sb50j6nnb6uy8v9myqwfzciz5b588ih057j9hwmjlch941q.png)

3. In the pop-up window, adjust the **Startup type** to **Automatic**, then click **Apply**.

![](https://uploads.developerhub.io/prod/2x2P/4bn4gprw0tch2e9pio4ko2446lifysd9m2zz10dhglbhtuvsjfmff25i3gwe2h11.png)

![](https://uploads.developerhub.io/prod/2x2P/zbmgt107nlw7nyp4fukr4utkgra93p2yn1o2wi82rpoo9ba3fcu1xpxs1n0e0y07.png)

4. Open the Windows **Start** menu, search for **Windows Update Settings** and then **Open** it.

![](https://uploads.developerhub.io/prod/2x2P/k3e9qg8xx5cf0mhgjuyputtg6789huxo0ypiocvup5kmhmaul9lrcpvk9vqymr7e.png)

5. In the **Update Settings** app, you can check for available updates by clicking **Check for updates**.
6. You can also install optional updates individually, by clicking **Download and install** under a specific update.

> **Pro Tips:**
>
> When you click **Check for updates**, the system should automatically download and install all missing patches that are available. You can check each download for additional information and progress, and **Restart** your device to apply certain updates as prompted.

7. To adjust your update settings and ensure that updates happen automatically, click on **Advanced options**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/n6eqxe7n6vzsxtmv3czjl3x66jpzm6djbfgzytobxcjqh1wqub880i3uya7wa124.png)

9. On the **Advanced options** page, enable the option to **Receive updates for other Microsoft products**, along with whichever advanced settings align with your organizational requirements, MetaAccess policies and preference.

![](https://uploads.developerhub.io/prod/2x2P/jgpx5w1epq4pprhu1kjx2oa1xqh60dmsblhyk3lexdaphjo2ph71dgv7a35k371i.png)

9. Now, to check your device compliance again, open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **MetaDefender IT-OT Access**, then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/1yda/9u3etam4j1u2bz3v5i167r252p3az00zcgrhm17061wqg11g5cbope1njesckx9w.png)

10. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/b6jwrbw50gew52fs1nv6xen0bhm4ua2nfv7o6he3fwj8cre6hkmhc4t06oapao6d.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Managed Windows Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
