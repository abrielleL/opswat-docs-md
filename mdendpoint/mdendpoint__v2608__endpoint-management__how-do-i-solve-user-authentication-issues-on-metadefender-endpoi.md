<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-solve-user-authentication-issues-on-metadefender-endpoi -->

# How do I solve User Authentication issues on MetaDefender Endpoint/MetaDefender IT-OT Access managed macOS devices?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to **User Authentication**, although this depends entirely on policy configurations.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/799gkgo2eafg0iqkqr6w63zc6juwn3spho84599x092ae2rhw0itr5wg5tgf4on0.png)

To remediate authentication-related device compliance issues on managed macOS devices, please follow the instructions below.

## MetaDefender IT-OT Access Compliance Warning: User Authentication - Lock Screen Timeout Is Not Set / User Password Protection Is Disabled

1. Open the **Apple** menu in the top left-hand corner of the screen,click on **System Preferences**, then navigate to the **Desktop & Screen Saver** section.

![](https://uploads.developerhub.io/prod/2x2P/ghcc6g7336hb229vzjyrcx6n974sl2g7svumpdobm5056hfl8bkeed9wkc4g6jqu.png)

2. Expand the **Screen Saver** tab, then adjust the screen saver timeout to **Start after** 5 minutes.

![](https://uploads.developerhub.io/prod/2x2P/l0dlrio6rwq6qv1tm4acyjckfemsiqtggbaoyyhobzxammnbh6jgtz0maeusfde3.png)

3. Go back to the **System Preferences** menu page, then click on **Security & Privacy**.

![](https://uploads.developerhub.io/prod/2x2P/x9l8632yggfldn2qx9kj8cwgahd901445j3hojfg27y3tfbq02uikm94denb7yf6.png)

4. Expand the **General** tab, then click the **Lock** in the bottom left-hand corner to make changes.
5. Then, select the option to **Require password X after sleep or screen saver begins**, and adjust the duration to **immediately**, before clicking the **Lock** again to close it.

![](https://uploads.developerhub.io/prod/2x2P/r1hhalb4pohykmei058hcnucrx5cr3gix1lq6g78ca9v164n02deiow9qxanznve.png)

6. Open **Finder**, click on **Applications**, then search the list for **OPSWAT Gears** and open it.
7. Once the app is running, click/right-click on the Client tray **Icon** and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/iymuqqrr28mx62zbjtqzvp989i9jm3e74uytig693qe0n7szrvtyqzwnfcebmsfu.png)

8. Wait for a few moments, then check **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>User Authentication** again to see the updated issue report.

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience User Authentication Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Managed MacOS Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
