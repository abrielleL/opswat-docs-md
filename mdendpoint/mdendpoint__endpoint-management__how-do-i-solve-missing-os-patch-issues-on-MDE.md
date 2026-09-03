<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/how-do-i-solve-missing-os-patch-issues-on-MDE -->

# How do I solve Missing OS Patch issues on MetaDefender Endpoint/MetaDefender IT-OT Access managed macOS devices?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches**.

> **Pro Tips:**
>
> Malware is frequently designed to exploit the vulnerabilities in outdated applications and operating systems in order to gain entry to and infect a system.
>
> This is why keeping your operating system, OS patches and all associated apps up-to-date is an essential element of risk reduction in cyber-security.
>
> One way to ensure that the OS patches on your macOS device are kept up-to-date is to configure the macOS Update Agent.

To remediate Missing OS Patch related device compliance issues on your managed macOS devices, please follow the instructions for configuring the macOS Update Agent and updating App Store apps below.

> **Please Note:**
>
> These instructions are based on macOS Catalina 10.15.7, and will vary slightly depending on your macOS version.

1. Click on the **Apple** menu in the top left-hand corner of the screen then, from the drop-down menu, select **System Preferences**.

![](https://uploads.developerhub.io/prod/2x2P/7zwvxchvzds0xhtb70zn8xcyggb6tgdj7v9nl03ilrqp9qszweik4qs11i9pfy1y.png)

2. On the **System Preferences** window, click on **Software Update**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/0k579yqestrjzh44esg88axfynodx391q96ezjglyd3lf6m3clw561cdsjgnkp4b.png)

3. If there are any updates available, click the **Update Now** button to install them, or click **More info…** to discover details about each update and to select specific updates to install.

![](https://uploads.developerhub.io/prod/2x2P/sqa7ltwhk0ay6ieqcq78s3sv7g1d6fi0sn2ywufl5ie2vqmteih1fkjorhtrdbxg.png)

![](https://uploads.developerhub.io/prod/2x2P/cqlud5mhjqdeks0j1oi5j54oezllrarqwyr5pguhohhpsw2t68mwbqg7zel6j2hi.png)

4. Once you’ve selected **Install Now** and all updates have been installed, the screen should look as follows. Ensure you check the option to **Automatically keep my Mac up to date**.

![](https://uploads.developerhub.io/prod/2x2P/yo6ie2zyo878rbn9q6l3cw6tq5f29kqtymwalt962qxymraijscsx6cao2vcixni.png)

5. For applications and tools that aren’t native to the OS, but were downloaded separately from the **App Store**, you can keep these up to date by clicking on the **Apple** menu in the top left-hand corner of the screen, then clicking on **App Store**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/9imxwwed9bxzz03vclrey1kavhjp23pooi0u1vp4ymghkgmeq1wt6b8waq3hkk4j.png)

6. In the **App Store**, click on **Updates** in the left-hand navigation panel and, if there are any app updates to install, you can install them individually as required, or click the **Update All** button in the top right-hand corner of the screen.

![](https://uploads.developerhub.io/prod/2x2P/w6srt93br0gwg7idcpbq7frfspzpoi40y5ewp3kqzmuyt6rba5vlf28py1jnljlh.png)

7. Finally, open **Finder**, click on **Applications**, then search the list for **OPSWAT Gears** and launch it.

![](https://uploads.developerhub.io/prod/2x2P/ecrzfimphky2big62qg6aujj8j139am8350twc9xvassnph109fchut15s7d6bdt.png)

8. Once the app is running, click/right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/0ptknq6i9394jff57gelq9v68606rq2fzxzxc0fwfrboldpnijg08ne7y9k3nenm.png)

9. Wait for a few moments, then check **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches** again to see the updated issue report.

> **Support:**
>
> If you have followed the relevant guidelines but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Managed MacOS Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
