<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-bitlocker-drive-encryption-issues-on-metadefender -->

# How do I solve BitLocker drive encryption issues on MetaDefender Endpoint devices?

> **Check Your Product:**
>
> This article applies to Windows BitLocker, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows Professional systems.

Users running MetaDefender Endpoint on one or more Windows Professional devices may occasionally see one of the following two My OPSWAT Central Management device compliance warnings/flags related to BitLocker drive encryption.

These warnings/flags are triggered by device issues, and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**.

> **Please Note:**
>
> The following remediation steps are applicable to Windows Professional systems only.
>
> If none of the steps outlined resolve your issue, please follow the instructions at the end of this article to contact OPSWAT Support.

Please follow the relevant steps below to remediate your BitLocker-related compliance issue.

## My OPSWAT Central Management Compliance Warning: Bitlocker Drive Encryption - Encryption State Is Not Enabled

1. Open the Windows **Start** menu and search for **This PC** app, then launch it.

![](https://uploads.developerhub.io/prod/1yda/go7hm0pktcq0timjsdy7o06ijj9qwyhod9co4hniyaapeex1cv554m8ada8auzxl.png)

2. In the **Windows Explorer** window, as illustrated below, select the **System Drive**.

![](https://uploads.developerhub.io/prod/1yda/t3ousoaczfj3rnwb0ongdh7cvbtra4f1mfuu1au99mnz71c9bcpod2vzeb2qs5r5.png)

3. Right-click on the **System Drive** then, from the pop-up menu, select the **Turn on BitLocker** option (Windows 11, Screenshot A); or right-click on the System Drive then, from the pop-up menu, select **Manage BitLocker** (Windows 10, Screenshot B).

**(A)**

![](https://uploads.developerhub.io/prod/1yda/b8so3hnydedvw15j4lh6uupoi4xoqveqalcrqxkee2hoqub3xy6v20256boxs8gi.png)

**(B)**

![](https://uploads.developerhub.io/prod/1yda/wbenqwzyilij9esfao4x296gb10ghwidmji5ar6w36z5lds7z1rjg23mog42lwki.png)

4. From the expanded window, click the **Turn BitLocker on** option, then enable BitLocker encryption by following the product’s built-in **Wizard**.

![](https://uploads.developerhub.io/prod/1yda/yv2ylr8fe9ky61t883rybs3uzkpco784a9zvca6a284n8oo9w3k43vdiuyklw5tm.png)

5. Open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **My OPSWAT Central Management** then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/1yda/5okakz1hxdvmawy14jbonf4ncjje2ic35fgdsrprr22ri5anmpv2e42wqsp8m3ig.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/o9cnuyz0l3j7ha7zgrt4x4edujrcmmlwisehx9n8m3itqhy7og3k7bx23zoqj2py.png)

## My OPSWAT Central Management Compliance Warning: Bitlocker Drive Encryption - Encryption State Is Suspended

1. Open the Windows **Start** menu, search for **BitLocker**, then select the **Manage BitLocker** option.

![](https://uploads.developerhub.io/prod/1yda/wflycgvb6nufl4sih50qnidkdrjxrovyqp4o2j5tj48a98qcsz6ugb13rk2mzcij.png)

2. On the **Bitlocker Drive Encryption** screen, select the **Resume protection** option.

![](https://uploads.developerhub.io/prod/1yda/00qf7hai5pyvyudmykuzjf0g591nh6mu4zgp33u35h2zp9zyr3x8xauvkslhqlp7.png)

> **Please Note:**
>
> If your BitLocker protection was affected by an update to Windows, you may need to restart your machine in order to complete this process.

3. Open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **My OPSWAT Central Management**, then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/1yda/tdtua4qa2ewyh5nif6xmafgurb5oafgavx48zqjigtfpyt0bdkgua1i4inoyeqg8.png)

4. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

![](https://uploads.developerhub.io/prod/1yda/j1iy5a36xtj02vc0bqw3z24a166r5vlgcchxhovrgfwlq21ooeuiu8rvfleva8ye.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience BitLocker Drive Encryption Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management** **Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form.
