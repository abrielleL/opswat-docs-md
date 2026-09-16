<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-user-authentication-issues-on-macos -->

# How do I solve User Authentication issues on MetaDefender Endpoint managed macOS devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see My OPSWAT Central Management device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/m127qh4pbwisagxt3qa8ek2s8t4e6ttbhw23330hm12erqppor8fk8gjzqqedln6.png)

To remediate authentication-related device compliance issues on managed macOS devices, please follow the instructions below.

## My OPSWAT Central Management Compliance Warning: User Authentication - Lock Screen Timeout Is Not Set / User Password Protection Is Disabled

1. Open the **Apple** menu in the top left-hand corner of the screen,click on **System Preferences**, then navigate to the **Desktop & Screen Saver** section.

![](https://uploads.developerhub.io/prod/97qW/g0o6m032qwk1ypq3pvqf9xlso924af4waxq57vf7mrpzhenvfwcmynicczv03kf3.png)

2. Expand the **Screen Saver** tab, then adjust the screen saver timeout to **Start after** 5 minutes.

![](https://uploads.developerhub.io/prod/97qW/27ch9176o6qymm1rcwjpm2w5i5pg4cyqzii6f9lbgkdnzwgn6np2cv8m4hl5x937.png)

3. Go back to the **System Preferences** menu page, then click on **Security & Privacy**.

![](https://uploads.developerhub.io/prod/97qW/axrnqbk08vpxei4per7fj7d7foajij1v3bvmsb13n2imtdlucww50y57jw1yhyrl.png)

4. Expand the **General** tab, then click the **Lock** in the bottom left-hand corner to make changes.
5. Then, select the option to **Require password X after sleep or screen saver begins**, and adjust the duration to **immediately**, before clicking the **Lock** again to close it.

![](https://uploads.developerhub.io/prod/97qW/31frkcttr4wnfgnen2jbh5tgoi25w9xz3aun6wd6cr4nh3s7uetwytxvkc99k9nz.png)

6. Open **Finder**, click on **Applications**, then search the list for **OPSWAT Gears** and open it.
7. Once the app is running, click/right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/97qW/1ztoe04yb53xq080beg9rqykyaw8412ipoddhhlmnh6iqvk7d1sx02basjvkcxy4.png)

8. Wait for a few moments, then check** My OPSWAT Central Management Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication** again to see the updated issue report.

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Mangement Managed MacOS Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
