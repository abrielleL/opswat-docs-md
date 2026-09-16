<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-user-authentication-issues-on-window -->

# How do I solve User Authentication issues on MetaDefender Endpoint/My OPSWAT Central Mangement managed Windows devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Mangement Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

Users running MetaDefender Endpoint on one or more Windows devices may occasionally see My OPSWAT Central Mangement device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under** My OPSWAT Central Mangement Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/aa9fmnvwjgxektuylstf0xzrrmgn5r7vq0e61bslwbf92xoft7pf7vymy88hpn3b.png)

To remediate authentication-related device compliance issues on managed Windows devices, please follow the relevant instructions below.

## My OPSWAT Central Mangement Compliance Warning: User Authentication - User Password Protection Is Disabled

### Windows 11

1. Go to the Windows **Start** menu, search for **Change your password**, then click on it to open the settings, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/4ynsxg6mvzgxfl96s93nrn53uj30xw9fwjvht424j59ik9p3l8kmjooeusx6rp64.png)

2. Click to expand the **Password** section, then click **Change**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/ln7hsv9oj5m1syhyaudrnqfq30daem20fk9g5t4skd3awgn15xqzzd0ax4azke1d.png)

3. Follow the wizard to set your account **Password**.
4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or** My OPSWAT Central Mangement**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/97qW/yfa9sdsxt4r7b6secoy4avu0ws011j03ujleqf7a4aq54ghhm1ap5yxfo96yh7jx.png)

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Mangement  servers again.

![](https://uploads.developerhub.io/prod/97qW/kbdmn9z9f4wctfshf8lmnx6za4bhsv78wtwn6yqn84p2vdy2wm5fegn4bmtp8yqd.png)

### Windows 10

1. Go to the Windows **Start** menu, search for **Change your password**, then click on it to open the settings, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/wr3nzhibf9tkk9yzyqevmazs4bjy4uri06t0xhkxf1u2uryf9h2f7v6esr4cakoc.png)

2. In the **Password** section, click on the **Change** button.

![](https://uploads.developerhub.io/prod/97qW/cjivnzwmdha19a66t469cx6kzuxvj7x69ipa5qezmxqcqkmq9eafga8l12heb2w8.png)

3. Follow the wizard to set your account **Password**.
4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or My OPSWAT Central Mangement ) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/97qW/5ep2jzdyj1cayltwiv4bftgwylz8bjxx7yxetsvu2ke81752xyeyx633cpez2c5s.png)

5. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

![](https://uploads.developerhub.io/prod/97qW/cilfbqtuovnx70d89417utq2svb02ts8rbjh0puxzivxuh7lkc9tqoezvpali5ru.png)

## My OPSWAT Central Mangement Compliance Warning: User Authentication - Lock Screen Timeout Is Not Set

### Windows 10/11

1. First, ensure that your **Password** is set and established on your device, by following the process outlined above.
2. With your password set, go to **Settings>Personalization>Lock screen** and click on **Screen saver** settings.
3. On the **Screen saver** settings page, set a timeout that complies with your organization’s relevant **My OPSWAT Central Mangement Policy** requirements, by adjusting the period in the **Wait** drop-down box.
4. Check the option to **On resume, display logon screen**.

![](https://uploads.developerhub.io/prod/97qW/bzff7xgted1rbc9mw0pnb8f7r5153h9g57qnu8jz25p1w75wq7de9mqumx4khl52.png)

- There are two settings on **Screen and Sleep** settings. Use the first two to set Screen timeout. Then, use the last two set when your computer Sleeps.
  - The settings in the screen section will lock your screen (turns your display off) if you are inactive for the specified period of time. On the other hand, the settings in the Sleep section put your PC to sleep if you are inactive for a specified period of time.
- It is also important to note that each of the sections has a setting for when your PC is plugged to power or running on battery power.

> **Pro Tip:**
>
> On some devices, users may be required to restart their machine in order to apply the new settings.

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or My OPSWAT Central Mangement ) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/97qW/awcgq9du87w5jpg5hnshfjasecfq7v6kx6x56vbuws1cobyoiyzsjbg1sund1rrn.png)

6. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Mangement  servers again.

![](https://uploads.developerhub.io/prod/97qW/tt07itzr5whg1gls6nmqbxvcc2r5v2gwso2k67pr0u896oiex2ux8fnel7d47h0m.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint / My OPSWAT Central Mangement Managed Windows Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
