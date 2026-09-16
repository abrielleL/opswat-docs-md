<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-use-windows-update-agent-to-solve-missing-os-patch-issu -->

# How do I use Windows Update Agent to solve Missing OS Patch issues on MetaDefender Endpoint/My OPSWAT Central Management managed Windows devices?

> **Check Your Product:**
>
> This article applies to the Windows Update Agent, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

Users running MetaDefender Endpoint on one or more Windows devices may occasionally see My OPSWAT Central Management device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **Inventory>Devices>Select your device>Detailed Device Information>Missing Patches**.

> **Pro Tip:**
>
> Malware is frequently designed to exploit the vulnerabilities in outdated applications and operating systems in order to gain entry to and infect a system.
>
> This is why keeping your operating system, OS security patches and all associated apps up-to-date is an essential element of risk reduction in cyber-security.
>
> One way to ensure that the OS patches on your Windows devices are kept up-to-date is to configure the Windows Update Agent accordingly.

To remediate Missing OS Patch related device compliance issues on your managed Windows devices, please follow the instructions for configuring the Windows Update Agent below.

## Windows 10/11

1. Open the Windows **Start** menu, search for **Services** and then **Open** it.

![](https://uploads.developerhub.io/prod/1yda/o7n11y1c208a8jj1glpxqv1590q6g145x3rofnbcgzoqkpxn8e7qti193a2fz9qh.png)

2. In the **Services** app, search for **Windows Update** service and, when you find it, double-click on it.

![](https://uploads.developerhub.io/prod/1yda/wnwh8rrinjjn28musb0lsut8lfgtrd67pkwsvbnbdxu0vrpnwugrms5xo1bzk4is.png)

3. In the pop-up window, adjust the **Startup type** to **Automatic**, then click **Apply**.

![](https://uploads.developerhub.io/prod/1yda/1c2hpgcfc35yva70vhtiwzfqik8xsectvuv7jyy7uuy9km9zzlnudyvbbof75hcb.png)

![](https://uploads.developerhub.io/prod/1yda/taxndllprqeozjcdj1kf5pqmzi09qelhjxhl5r9nh3jfqvdwz4bhkcbsg86buthf.png)

4. Open the Windows **Start** menu, search for **Windows Update Settings** and then **Open** it.

![](https://uploads.developerhub.io/prod/1yda/3u1zgvuhpya587lw98bhx85lwracdceb1fx2bzdjb55h7pdazzhryai4w1asubvf.png)

5. In the **Update Settings** app, you can check for available updates by clicking **Check for updates**.
6. You can also install optional updates individually, by clicking **Download and install** under a specific update.

> **Pro Tip:**
>
> When you click **Check for updates**, the system should automatically download and install all missing patches that are available. You can check each download for additional information and progress, and **Restart** your device to apply certain updates as prompted.

7. To adjust your update settings and ensure that updates happen automatically, click on **Advanced options**, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/7rghw8e23itd8hucujmj9ru4fw14y78vhmrp9t67wyujt64b0m4o35n6r6jd9zht.png)

8. On the **Advanced options** page, enable the option to **Receive updates for other Microsoft products**, along with whichever advanced settings align with your organizational requirements, My OPSWAT Central Management policies and preference.

![](https://uploads.developerhub.io/prod/1yda/krc10qj5osb3mgnkl62efh8zyg3tnod5ijzz7be483iwv80a1gb8hydcr5y5nwlk.png)

9. Now, to check your device compliance again, open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **My OPSWAT Central Management**, then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/1yda/9u3etam4j1u2bz3v5i167r252p3az00zcgrhm17061wqg11g5cbope1njesckx9w.png)

10. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/3ag66xj53fo6uqrzhe4577wu97px4i4lf21od5pidp0sjn9gcbg62uw4bsdfo985.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management Managed Windows Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
