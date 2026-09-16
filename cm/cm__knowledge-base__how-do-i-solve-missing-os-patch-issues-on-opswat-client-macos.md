<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-missing-os-patch-issues-on-opswat-client-macos -->

# How do I solve Missing OS Patch issues on MetaDefender Endpoint/My OPSWAT Central Management managed macOS devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see MetaDefender IT Access device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches**.

> **Pro Tip:**
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

![](https://uploads.developerhub.io/prod/97qW/2egjt4ooxui420nize4m1m3nm5ytvr09shwm0f8sgwotku6hg0wlg6mwp3xeqyvb.png)

2. On the **System Preferences** window, click on **Software Update**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/8n4yw3sw31mus05bc10ehpa6p91mcrz89xb4lzi3hj5oxhfwjoja13qzou7h2zjb.png)

3. If there are any updates available, click the **Update Now** button to install them, or click **More info…** to discover details about each update and to select specific updates to install.

![](https://uploads.developerhub.io/prod/97qW/vu25rt5d3xhhpw2lxgi730si4xbaw246iri840q16x2gj335jztx22fhyu8kst2l.png)

![](https://uploads.developerhub.io/prod/97qW/2jxn5ewiz796f5lknt1tcpw3m2xjut98j7p1hku05puug8neib38200qbz96sqai.png)

4. Once you’ve selected **Install Now** and all updates have been installed, the screen should look as follows. Ensure you check the option to **Automatically keep my Mac up to date**.

![](https://uploads.developerhub.io/prod/97qW/5tr6pcewakvy1o9c2tbqbydof4p2wlmuxxn153caqsp81vhw6ariqnh2q8qlulw0.png)

5. For applications and tools that aren’t native to the OS, but were downloaded separately from the **App Store**, you can keep these up to date by clicking on the **Apple** menu in the top left-hand corner of the screen, then clicking on **App Store**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/350xbs3d52cyh5n2bprmgstxl2pq73zkne8xph6ttn71skarmy25xx4u2joa9u29.png)

6. In the **App Store**, click on **Updates** in the left-hand navigation panel and, if there are any app updates to install, you can install them individually as required, or click the **Update All** button in the top right-hand corner of the screen.

![](https://uploads.developerhub.io/prod/97qW/3o6nnhmtqxopwi0kv8n2q2xct8s1qr8t9beunrrqlyu2f1iwq2xtodb2rng9unew.png)

7. Finally, open **Finder**, click on **Applications**, then search the list for **OPSWAT Gears** and launch it.

![](https://uploads.developerhub.io/prod/97qW/8avsxx8ddruofhzqya95rbeptkgsg67cret1pp12st6vhuus3p2gptdk1uvprhke.png)

8. Once the app is running, click/right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

![](https://uploads.developerhub.io/prod/97qW/x0j8jkp7lz2zlfcsatmq8auxt9vz02agbdwygaa09wwik5kq02ocjlip172omoe6.png)

9. Wait for a few moments, then check **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches** again to see the updated issue report.

   ** **

> **Support:**
>
> If you have followed the relevant guidelines but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management Managed MacOS Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
