<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-metaaccess-check-for-specific-versions-of-operating-syst -->

# How can MetaDefender IT Access check for specific versions of operating system?

This article applies to the current MetaDefender IT Access Console and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

MetaDefender IT Access offers administrators the option to check their device inventory for specific, administrator-approved operating system versions.

To set up this feature, please follow the instructions below.

1. Log into your **MetaDefender IT Access Console** and navigate to **Policy Management>Policies>Relevant Policy>Deep Compliance>Operating System**.
2. Check the **Device is not running an approved operating system** option, as illustrated in the screenshot below.

3. Click the **Add operating system condition** button to access the settings field.
4. Stipulate your conditions by adding the scope of approved release versions, or click the **+** sign to select filters from the pop-up menu, as illustrated below.

   - For Windows, administrators can filter by edition, and exclude specific builds.
   - For Linux, administrators can filter by vendor, in addition to the release version.

Please Note:

Release versions may differ from the release title/OS name.

For example:

- Windows 7’s release version is 6.1
- MacOS High Sierra’s release version is 10.12

Release version information can be sourced from vendor websites, or by contacting the operating system vendor directly.

Pro Tip:

For the policy to save this setting as **Enabled**, you will need to add at least one operating system condition.

5. Once all of your conditions are set, click **Save** to confirm your changes.

Please Note:

The MetaDefender IT Access process approves operating systems systematically. Even if a device meets one listed condition, MetaDefender IT Access will first check all remaining conditions, in order, before confirming compliance.

Support:

If you have followed the instructions below but have further queries or concerns regarding **Checking For Specific Operating System Versions With** **MetaDefender IT Access**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
