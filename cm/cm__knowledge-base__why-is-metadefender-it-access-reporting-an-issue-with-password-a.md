<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-is-metadefender-it-access-reporting-an-issue-with-password-a -->

# Why is My OPSWAT Central Management reporting an issue with password and lock-screen unexpectedly?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

The **Compliance** state shown in the My OPSWAT Central Management Console and API will always reflect the most recent report compiled by the MetaDefender Endpoint.

There may be cases in which no user is logged onto a device but MetaDefender Endpoint is still running in the background.

As a result, the system cannot report the compliance state of any user-specific settings. These user-specific settings include the **Lock-Screen** and **Password**.

> **For Example:**
>
> A common scenario is when a device is rebooted and then left at the login screen for an extended period.
>
> During this time, My OPSWAT Central Management will report that User Authentication settings are Non-Compliant. However, this status will be resolved the moment the user logs onto the device.

To avoid confusion in similar cases:

- Double check devices that report user-authentication non-compliance 30 minutes to an hour later.
- You will usually find that the status has automatically resolved, due to a user logging in after a phone call or lunch break.

Alternatively, there is a setting associated with this in your **My OPSWAT Central Management** **Console:**

1. Go to **Policy Management>Policies>Relevant Policy>Deep Compliance>User Authentication>Exception.**
2. Enable the option to **Skip user authentication check if no active user session has been initiated**, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/yjoqj4p9dle2iei9hfagra0fobozj2vzkctox9v8dbcfw4h8syxf1xst0qrr5o0a.png)

3. Finally, click **Save** to apply the new setting.

With the above setting enabled, the associated devices will not be assessed in the **User Authentication** category *unless* an active user session is detected.

> **Support:**
>
> If you have followed the instructions above but have further queries or concerns regarding **My OPSWAT Central Management** **Reporting Issues With A Device’s Password And Lock-Screen**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
