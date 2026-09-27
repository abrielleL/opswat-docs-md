<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-solve-bitlocker-drive-encryption-issues-on-metadefender -->

# How do I solve BitLocker drive encryption issues on MetaDefender Endpoint/MetaDefender IT-OT Access devices?

> **Check Your Product:**
>
> This article applies to Windows BitLocker, the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows Professional systems.

Users running MetaDefender Endpoint on one or more Windows Professional devices may occasionally see one of the following two MetaDefender IT-OT Access device compliance warnings/flags related to BitLocker drive encryption.

These warnings/flags are triggered by device issues, and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**.

> **Please Note:**
>
> The following remediation steps are applicable to Windows Professional systems only.
>
> If none of the steps outlined resolve your issue, please follow the instructions at the end of this article to contact OPSWAT Support.

Please follow the relevant steps below to remediate your BitLocker-related compliance issue.

## MetaDefender IT-OT Access Compliance Warning: Bitlocker Drive Encryption - Encryption State Is Not Enabled

1. Open the Windows **Start** menu and search for **This PC** app, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/bhd53vc5s147298eb7xkxg75d1zd21bayum6q9kns5sjljmioj9kz0h9x3eganrc.png)

2. In the **Windows Explorer** window, as illustrated below, select the **System Drive**.

![](https://uploads.developerhub.io/prod/2x2P/q6otytlndriahxx2idtnvxd6eud87dsigxff8joakfid0naz0r1bwchrxledd4l0.png)

3. Right-click on the **System Drive** then, from the pop-up menu, select the **Turn on BitLocker** option (Windows 11, Screenshot A); or right-click on the System Drive then, from the pop-up menu, select **Manage BitLocker** (Windows 10, Screenshot B).

**(A)**

![](https://uploads.developerhub.io/prod/2x2P/l15en5b1ginmjxp05o8sz3tgz905wnrpoycm193wrvrgpnd81mcynhgtd77fstby.png)

**(B)**

![](https://uploads.developerhub.io/prod/2x2P/xfwptf7dhihm77fblb3vrq1zoe9v563smuqkb6jbrn5bxb3ryaieb8kxs94k9t5g.png)

4. From the expanded window, click the **Turn BitLocker on** option, then enable BitLocker encryption by following the product’s built-in **Wizard**.

![](https://uploads.developerhub.io/prod/2x2P/zsbuf38w0rxu2pxcjb6apj6brnep2efrq6nisgq0lk7p0k33oo0gg96a0drq0mm6.png)

5. Open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **MetaDefender IT-OT Access** then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/2x2P/q3utjm2o3olw6kixrqb89e7b0l24sgxw911wvkj7t4djjmorszunufls4l3q1qj3.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/mv5ygfqpmski3euvdd1r751wvh3k19zhb7e4ajacfmghu2pm9s3vl8uux7d7atv3.png)

## MetaDefender IT-OT Access Compliance Warning: Bitlocker Drive Encryption - Encryption State Is Suspended

1. Open the Windows **Start** menu, search for **BitLocker**, then select the **Manage BitLocker** option.

![](https://uploads.developerhub.io/prod/2x2P/590uzfgxqsosr1j4rcmglzuea87qb2iy88bdxp8fmj7ag8ctvnrcws52al4mgf6b.png)

2. On the **Bitlocker Drive Encryption** screen, select the **Resume protection** option.

![](https://uploads.developerhub.io/prod/2x2P/exhfsv3fuvmtvasnu44n1zm01ebcfy7xvr9g7txnxu8qzks0stu251ldfmxl0k8m.png)

> **Please Note:**
>
> If your BitLocker protection was affected by an update to Windows, you may need to restart your machine in order to complete this process.

3. Open the Windows **Start** menu, search for the **MetaDefender Endpoint** or **MetaDefender IT-OT Access**, then select the **Run as administrator** option.

![](https://uploads.developerhub.io/prod/2x2P/1de4lbkqdgkb0oxkpb1is45krxoiqqwzp69xke52afr456h5nlfwgtj5uqo2yi6p.png)

3. Once the app is running, right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

![](https://uploads.developerhub.io/prod/2x2P/f97jlmv4ju1d4aj34o3htakl4kz91axu3uortjqqlv9qpzv5d3otqr2yy70hj1na.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience BitLocker Drive Encryption Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
