<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-solve-user-authentication-issues-on-metadefender-end -->

# How do I solve User Authentication issues on MetaDefender Endpoint/MetaDefender IT-OT Access managed Windows devices?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

Users running MetaDefender Endpoint on one or more Windows devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/pifbey07lcbknmm0nh4dvysdu5sbse8jt8n54hxhnjimn8tgbmtj18jor94afwmm.png)

To remediate authentication-related device compliance issues on managed Windows devices, please follow the relevant instructions below.

## MetaDefender IT-OT Access Compliance Warning: User Authentication - User Password Protection Is Disabled

### Windows 11

1. Go to the Windows **Start** menu, search for **Change your password**, then click on it to open the settings, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/orki1cbzne7izhii3iwkqqx72rh0bb4eetzaahh5ewe3ec234umkn717g9f0owni.png)

2. Click to expand the **Password** section, then click **Change**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/72satebozon7po95682sgwh5v508a16bwlzfcq9zehv25wh3ebuiaiopa0bnzfxb.png)

3. Follow the wizard to set your account **Password**.
4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/wsjdopqxk36o4cnvtgp8cml53tv5jazj75ld8ogullzmirmnmjub6u645ol5gdse.png)

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/if9jg7fa8hvzrglb6dbuhdcahjd0gs1w4hnmt51e0hfc773ek7kiwskbrc71jfdk.png)

### Windows 10

1. Go to the Windows **Start** menu, search for **Change your password**, then click on it to open the settings, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/q7buudc4erdb0y0u0p37jbsakzbex6hzet05rmptd0e6eke0r8j84oyoqvvj14al.png)

2. In the **Password** section, click on the **Change** button.

![](https://uploads.developerhub.io/prod/2x2P/5n0kxb4k69px2t2zck6sz2c1poq1hliinabvs4glfx2p5ygtulykfo1vgjmw5ybf.png)

3. Follow the wizard to set your account **Password**.
4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/gpnxfzvz6vpwufguvydota8fbwd64ab34yye8ws4jwl97yhbidwvqpcvyhiravim.png)

5. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/iom0arrceba9l8tree6hxad6yc1h4ocwzqml4bhvyb4exznxecx30i8ndaqf5b76.png)

## MetaDefender IT-OT Access Compliance Warning: User Authentication - Lock Screen Timeout Is Not Set

### Windows 10/11

1. First, ensure that your **Password** is set and established on your device, by following the process outlined above.
2. With your password set, go to **Settings>Personalization>Lock screen** and click on **Screen saver** settings.
3. On the **Screen saver** settings page, set a timeout that complies with your organization’s relevant MetaDefender IT-OT Access **Policy** requirements, by adjusting the period in the **Wait** drop-down box.
4. Check the option to **On resume, display logon screen**.

![](https://uploads.developerhub.io/prod/2x2P/zk9ouhcd7gfwoztzz2if1v50e7e37zo4r8rit07zuao7tstig15im15pnl9m6doq.png)

- There are two settings on **Screen and Sleep** settings. Use the first two to set Screen timeout. Then, use the last two set when your computer Sleeps.
  - The settings in the screen section will lock your screen (turns your display off) if you are inactive for the specified period of time. On the other hand, the settings in the Sleep section put your PC to sleep if you are inactive for a specified period of time.
- It is also important to note that each of the sections has a setting for when your PC is plugged to power or running on battery power.

> **Pro Tips:**
>
> On some devices, users may be required to restart their machine in order to apply the new settings.

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/p8fgyx52f31ti012yo95pxxut8vuvlxt99zy04x9zve986863ik3i6a4dgggjfsc.png)

6. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/gell71j4iu6sd6ui93nh2gfmjzoakln41hhjp3dg48wfjmcoqp9tth4dj5ptv4rz.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint / MetaDefender IT-OT Access** **Managed Windows Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
