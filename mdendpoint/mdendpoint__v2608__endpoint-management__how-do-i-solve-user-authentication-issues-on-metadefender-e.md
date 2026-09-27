<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-solve-user-authentication-issues-on-metadefender-e -->

# How do I solve User Authentication issues on MetaDefender Endpoint/MetaDefender IT-OT Access managed Linux devices?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Linux systems.

Users running MetaDefender Endpoint on one or more Linux devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/koqc0b2a5agy0b1cst4vz1mqepvy5s85zzfdq1lschf2va6zwyyiytpy0hf3u8nv.png)

To remediate authentication-related device compliance issues on managed Linux devices, please follow the instructions below.

> **Please Note:**
>
> The following remediation guidelines were written based on CentOS 7 x64, and the process may vary depending on your distro and version.

## MetaDefender IT-OT Access Compliance Warning: User Authentication - User Password Protection Is Disabled

1. Click the **Power** icon in the top right-hand corner of the screen and, from the pop-up menu, select **Account Settings**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/m31fj9kwajgk64chdet21bewjh6jeyqhoq5obttghyceb5ssk98f2fnuwd7ergux.png)

2. Click the **Lock**, then enter your **Root** password to unlock the account settings.

![](https://uploads.developerhub.io/prod/2x2P/s6ree1jy5xpf3apryuwdqox5o7cnt613qlkucb83wuyaqivusdiqdyeemxkgczu6.png)

3. Click on the **Password** field, then change your **Password**.

![](https://uploads.developerhub.io/prod/2x2P/prr4exqp3u0cv6pfsvo6ya7oivo8qeq6ayoqdfi91wtmysq78e5z4d2qgo3f7dw0.png)

4. Once your password has been set, **Restart** the device to apply your settings.

![](https://uploads.developerhub.io/prod/2x2P/antes0d71yxmyp5ougq2zw3tl1z59pgjps3q8enjasrjon3x7hyj39kuqvckw5a6.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Managed Linux Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
