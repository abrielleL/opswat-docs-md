<!-- source: https://www.opswat.com/docs/cm/knowledge-base/can-i-exempt-a-device -->

# Can I exempt a device from a My OPSWAT Central Management Access Policy?

> **Check Your Product:**
>
> This article applies to all My OPSWAT Central Management product releases deployed on Windows, macOS, Linux, Android and iOS systems.

Yes, you can.

Making exceptions is, unfortunately, a normal part of IT and security operations, but while it may be considered a last-resort, there should still be an elegant way of handling it. With this in mind, OPSWAT has created a straightforward policy exemption mechanism for your managed devices.

Additionally, because exempt devices can potentially create security holes in your network, we’ve made it easy to audit exemption events, find exempt devices, and reverse exemptions where necessary.

> **Pro Tip:**
>
> While in an exempt state, devices will respond to the registry API and REST API v2 as if they were compliant.
>
> Despite this, all compliance issues will continue to be reported in the **My OPSWAT Central Management** **Console>Inventory>Devices>Device Details** view and **API** detailed responses.

## Exempting devices from My OPSWAT Central Management policy

There are two options for exempting devices from a policy.

### Option 1:

1. Log into your **My OPSWAT Central Management Console** and go to **Inventory>Devices**.
2. Check the boxes alongside the devices you would like to exempt, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/nvvaxj85g73aad7je7i1uvqwxotnnm9evm99302x1d5b0apo5xbvzz7yusyfnscm.png)

3. Then click on the **Actions** dropdown menu in the top right-hand corner of the screen, framed in red in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/fah6oxz3lrjhc9ozo7qbayqs316sp5e1xra0u8z4o1kuzlfdfanx5yqwnc49ayyj.png)

4. From the dropdown menu, select the option to **Exempt**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/zdlmnce1kc2200da3dqk6f1az4c2zvdwb6kq1wmwpv4k3s4zvloj50doh1d0u72s.png)

5. Next, select the **Period** for which you’d like to exempt the device, then click **Exempt**.

![](https://uploads.developerhub.io/prod/97qW/duxkdwilg1586t1da0ickp7aapkzsutnp6cnaabm98ptfyanqnqsg2ovwrivgvyq.png)

### Option 2:

Here, you will use the **Device Action API** to program and manage each device’s exemption state. To learn more, refer to [Device Action](https://www.opswat.com/docs/cm/developer-guidelines/device-action) guidelines.

## Reversing an exemption

1. Log into your **My OPSWAT Central Management Console** and navigate to **Inventory>Devices**.
2. Select the devices you would like to exempt by checking the boxes in the first column.

![](https://uploads.developerhub.io/prod/97qW/c22qwerby4ijniogkdbc6cb43445yl5zxzpvg2m6m0fic3e7on15afcltig3gsk5.png)

3. Next, expand the **Actions** dropdown menu, framed in red below.

![](https://uploads.developerhub.io/prod/97qW/urfygm8xx1sdni03ewuwmhzm9mfawglen9e51rczc2ob7rnkve9uegyabofyi1a9.png)

4. Select the option to **Unexempt**.

![](https://uploads.developerhub.io/prod/97qW/12f58ag7i5iwcmwnjkummis4kbzpkz2uqpe7jusb0uhl5ty6116wi8jvwotxv987.png)

5. Finally, confirm the unexemption, as prompted.

![](https://uploads.developerhub.io/prod/97qW/57p32e9cb47lx4lih44ufjjfl9ke2oent0wf2la66lwc2q5cpta6ynqvapdhdnlp.png)

## Filter exempted devices

> **Pro Tip:**
>
> To streamline device management, diagnostics and threat response, the My OPSWAT Central Management Console’s **Filter** feature allows administrators to filter the devices displayed in their inventory for a wide range of characteristics, with categories including:
>
> - Malware detection
> - Compliance issues
> - Issue severity
> - Device status
> - Device type
> - Device tag
> - Installed Agent
> - Agent status
> - Operating system
> - Vulnerability severity
> - Repeated issues.
>
> When an administrator applies a filter for, for example, **Exempted Devices**, only exempted devices will be displayed in the device inventory.

1. Log into your My OPSWAT Central Management Console and navigate to **Inventory> Devices**.
2. Click on the **Filters** button in the top right-hand corner of your list, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/51jkmwa3y8x5rnhzhltj6x4e33wod1xch2rnrqz29wanveukwqdq8vu3q869epux.png)

3. A range of filtering options will be displayed, under **Device Status**, check the **Exempted** option.

![](https://uploads.developerhub.io/prod/97qW/5nv7rth5wfp3jpjc575l510nw2rbwogj64qlaycxhk38zvttlhv2w7rv8mq7k86c.png)

4. Finally, click **Update** to apply your filters.

![](https://uploads.developerhub.io/prod/97qW/yfc856d59yaktqc0l2bzaddkos2gk99qdumbrwyk54ep1a8rsju7rlv4qaxrkkjg.png)

## Audit log to track exemptions

My OPSWAT Central Management allows multiple administrators to manage a single account, so it’s essential that administrators have a way to track each other’s actions on the system.

To facilitate this, exemption actions have been added to the event logs for each device, located at **My OPSWAT Central Management** **Console> Logs>Device Events**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/nkk52es3lmahcu6sr1iwp0mk68ro3pm8sdkwy7pp33rp9m52v4mmgxaaqd9pf3r2.png)

Any actions taken to exempt or unexempt a device will appear in this log, along with the name of the logged-in administrator who performed the action (redacted in gray above).

The log can also be filtered so that, for example, only **Exempt/Unexempt** events appear.

> **Pro Tip:**
>
> Other administrative events, such as logins, logouts and policy updates, can be viewed under **My OPSWAT Central Management** **Console>Logs>Admin Events**.

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Exempting Or Unexempting Devices From A** **My OPSWAT Central Management** **Policy**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
