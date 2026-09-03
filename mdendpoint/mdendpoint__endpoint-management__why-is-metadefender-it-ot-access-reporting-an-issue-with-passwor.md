<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/why-is-metadefender-it-ot-access-reporting-an-issue-with-passwor -->

# Why is MetaDefender IT-OT Access reporting an issue with password and lock-screen unexpectedly?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

The **Compliance** state shown in the MetaDefender IT-OT Access Console and API will always reflect the most recent report compiled by the MetaDefender Endpoint.

There may be cases in which no user is logged onto a device but MetaDefender Endpoint is still running in the background.

As a result, the system cannot report the compliance state of any user-specific settings. These user-specific settings include the **Lock-Screen** and **Password**.

> **For Example:**
>
> A common scenario is when a device is rebooted and then left at the login screen for an extended period.
>
> During this time, MetaDefender IT-OT Access will report that User Authentication settings are Non-Compliant. However, this status will be resolved the moment the user logs onto the device.

To avoid confusion in similar cases:

- Double check devices that report user-authentication non-compliance 30 minutes to an hour later.
- You will usually find that the status has automatically resolved, due to a user logging in after a phone call or lunch break.

Alternatively, there is a setting associated with this in your **MetaDefender IT-OT Access** **Console:**

1. Go to **Policy Management>Policies>Relevant Policy>Deep Compliance>User Authentication>Exception.**
2. Enable the option to **Skip user authentication check if no active user session has been initiated**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/5kba7tvae7000ojv2omz0a16wnrtn51o01der40tooxjsbmcgsh2nhjzl4pjoy8a.png)

3. Finally, click **Save** to apply the new setting.

With the above setting enabled, the associated devices will not be assessed in the **User Authentication** category *unless* an active user session is detected.

> **Support:**
>
> If you have followed the instructions above but have further queries or concerns regarding **MetaDefender IT-OT Access** **Reporting Issues With A Device’s Password And Lock-Screen**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
