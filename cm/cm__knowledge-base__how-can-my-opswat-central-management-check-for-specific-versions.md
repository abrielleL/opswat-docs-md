<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-my-opswat-central-management-check-for-specific-versions -->

# How can My OPSWAT Central Management check for specific versions of an operation system?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

My OPSWAT Central Management offers administrators the option to check their device inventory for specific, administrator-approved operating system versions.

To set up this feature, please follow the instructions below.

1. Log into your **My OPSWAT Central Management Console** and navigate to **Policy Management>Policies>Relevant Policy>Deep Compliance>Operating System**.
2. Check the **Device is not running an approved operating system** option, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/qih1bq3o55rq4h5jp8epfm4czfep36mrngwuk4ze9x1ma9bjtddm4xaqjrpo73ze.png)

3. Click the **Add operating system condition** button to access the settings field.
4. Stipulate your conditions by adding the scope of approved release versions, or click the **+** sign to select filters from the pop-up menu, as illustrated below.
   - For Windows, administrators can filter by edition, and exclude specific builds.
   - For Linux, administrators can filter by vendor, in addition to the release version.

> **Please Note:**
>
> Release versions may differ from the release title/OS name.
>
> For example:
>
> - Windows 7’s release version is 6.1
> - MacOS High Sierra’s release version is 10.12
>
> Release version information can be sourced from vendor websites, or by contacting the operating system vendor directly.

![](https://uploads.developerhub.io/prod/97qW/2z7lc232fggugbad6gaxey9fa49r81wwlx3wwyimmqg0fui6c71vxj37o3zqipgc.png)

![](https://uploads.developerhub.io/prod/97qW/9d6codo3lr1dx8rau6z216f1lazvz32a2wgdhrlokxj2hypt5zccdxs7yp2nb0f4.png)

> **Pro Tip:**
>
> For the policy to save this setting as **Enabled**, you will need to add at least one operating system condition.

5. Once all of your conditions are set, click **Save** to confirm your changes.

> **Please Note:**
>
> The My OPSWAT Central Management process approves operating systems systematically. Even if a device meets one listed condition, My OPSWAT Central Management will first check all remaining conditions, in order, before confirming compliance.

> **Support:**
>
> If you have followed the instructions below but have further queries or concerns regarding **Checking For Specific Operating System Versions With** **My OPSWAT Central Management**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
