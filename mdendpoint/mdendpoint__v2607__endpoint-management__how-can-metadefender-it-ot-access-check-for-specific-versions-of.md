<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-can-metadefender-it-ot-access-check-for-specific-versions-of -->

# How can MetaDefender IT-OT Access check for specific versions of operating system?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

MetaDefender IT-OT Access offers administrators the option to check their device inventory for specific, administrator-approved operating system versions.

To set up this feature, please follow the instructions below.

1. Log into your **MetaDefender IT-OT Access Console** and navigate to **Policy Management>Policies>Relevant Policy>Deep Compliance>Operating System**.
2. Check the **Device is not running an approved operating system** option, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/rlzof63o1rktitnc9icmbjm3uvgpc5ax6w60pa981pr421q7qbjbvrjg0v00l4a6.png)

3. Click the **Add operating system condition** button to access the settings field.
4. Stipulate your conditions by adding the scope of approved release versions, or click the **+** sign to select filters from the pop-up menu, as illustrated below.
   - For Windows, administrators can filter by edition, and exclude specific builds.
   - For Linux, administrators can filter by vendor, in addition to the release version.

> **Please note:**
>
> Release versions may differ from the release title/OS name.
>
> For example:
>
> - Windows 7’s release version is 6.1
> - MacOS High Sierra’s release version is 10.12
>
> Release version information can be sourced from vendor websites, or by contacting the operating system vendor directly.

![](https://uploads.developerhub.io/prod/2x2P/1vmj95m5c2o0jkrpqiskcuklot14g8ucp11nwdvym3w3ju1ausr1mocdy4e61qyi.png)

![](https://uploads.developerhub.io/prod/2x2P/lvd0o90g3z8vf39otflfp64gg34jzg4rzednhq2tsf0ld8xiv73h3c8xxpu8lhrk.png)

> **Pro Tips:**
>
> For the policy to save this setting as **Enabled**, you will need to add at least one operating system condition.

5. Once all of your conditions are set, click **Save** to confirm your changes.

> **Please note:**
>
> The MetaDefender IT-OT Access process approves operating systems systematically. Even if a device meets one listed condition, MetaDefender IT-OT Access will first check all remaining conditions, in order, before confirming compliance.

> **Support:**
>
> If you have followed the instructions below but have further queries or concerns regarding **Checking For Specific Operating System Versions With** **MetaDefender IT-OT Access**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
