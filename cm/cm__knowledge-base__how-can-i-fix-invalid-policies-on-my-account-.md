<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-fix-invalid-policies-on-my-account- -->

# How can I fix invalid policies on my account?

> **Check Your Product:**
>
> This article applies to all My OPSWAT Central Management products deployed on Windows, macOS, Linux, Android and iOS systems.

As of 2 June 2020, My OPSWAT Central Management customers require a **paid** account in order to enable or use **Threat Detection** via MetaDefender Cloud.

This means that free My OPSWAT Central Management and free MetaDefender Cloud users can no longer enable or use Threat Detection via MetaDefender Cloud.

For more information on free VS paid account features, please [Read This](https://static.opswat.com/uploads/files/MetaAccess-Product-Free-en.pdf).

If your account does not support threat detection via multi-scanning with MetaDefender Cloud, and you attempt to enable threat detection with MetaDefender Cloud as a scan source in one of your policies, that policy will be considered **Invalid**.

In the event that you configure one or more invalid policies:

- You will not be permitted to confirm or implement any policy changes until the invalid setting has been corrected.
- MetaDefender Endpoint will not perform any threat detection scans, even if a scan is scheduled in policy.

> **Pro Tip:**
>
> All users can still leverage MetaDefender’s ground-breaking **Threat Detection** technology by adding one or more native **MetaDefender Core** servers to their account, if they have not done so already. To explore this option, or to explore qualifying **MetaDefender Cloud** options, please contact the [OPSWAT Sales](https://www.opswat.com/contact) team.

> **Please Note:**
>
> This update was made in alignment with OPSWAT’s current feature-based licensing tier system (for more information on our tier system, please [Read This](https://www.opswat.com/products/metaaccess#option_table) and [This](https://static.opswat.com/uploads/files/Product-Guide_compressed-1.pdf)).

To correct invalid policy settings on accounts without access to features associated with MetaDefender Cloud, please follow the instructions below.

1. Log into your **My OPSWAT Central Management Console** and navigate to **Policy Management>Policies>Relevant Invalid Policy>Settings.**
2. Read the **Error** notice at the top of the **Settings** page for a path to the invalid setting (see reference 1 in the screenshot below).
3. Click on the relevant tab to access the invalid setting.
4. Then, for example, select a valid alternative scan source (see reference 2 in the screenshot below, and see [How can I add my own MetaDefender Core servers to scan threats on devices?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-add-my-own-metadefender-api-servers-to-scan-threats-on)) or uncheck the selection box next to **Enable Threat Detection** (see reference 3 in the screenshot below).

![](https://uploads.developerhub.io/prod/1yda/yixgur4xk59zdy5r7yqh469kuep7x5jinqbrh7912bhdn1596yrx6yxfxb7kl6g5.png)

> **Pro Tip:**
>
> As mentioned, the red error warning/s at the top of the **Settings** page (see reference 1 in the screenshot above) will provide the necessary path/s for remediation.
>
> The following screenshot shows a range of error warnings with paths to various invalid settings requiring remediation.
>
> These examples feature invalid configurations for Mobile Devices, Windows and macOS, but if your error message points to another operating system or device setting, that is where you will make changes.

![](https://uploads.developerhub.io/prod/1yda/akmhfgn9s4mr8r2374dqkn47i2e9pi0xq40krwjn7cqnq8bdeec1cxmwgu1gvuup.png)

> **Pro Tip:**
>
> There are a diverse range of settings that may be responsible for your invalid policy configuration.
>
> To ensure that you adjust the right settings, follow the recommended path in the error message, then look out for text and entry fields displayed in red, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/aa2kbmz4ok2d7rtzlceee7yg9jzkq71cd9r0hh0ft0n6jxaxigvzvsjmocfoih5e.png)

5. Once you’ve obtained a valid configuration, click **Save** to apply your settings.

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Correcting Invalid Policy Settings On Your** **My OPSWAT Central Management** **Account**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
