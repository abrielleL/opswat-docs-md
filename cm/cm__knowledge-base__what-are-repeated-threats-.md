<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-are-repeated-threats- -->

# What are Repeated Threats?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, any feature-supported anti-malware software installed on your managed devices, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

> **Please Note:**
>
> Repeated-threat detection is distinct from threat detection via integration with MetaDefender Cloud or MetaDefender Core API, and is available for all free and paid My OPSWAT Central Management users.
>
> For more about **My OPSWAT Central Management** **Threat Detection**, please [Read This](https://www.opswat.com/docs/cm/kb/what-is-threat-detection-on-metaaccess-) .

My OPSWAT Central Management reviews the history of threats detected by your installed, local anti-malware software, to pinpoint and flag repeated occurrences of the same threat.

If your local anti-malware product is repeatedly reporting the same threat, this indicates that either that anti-malware is unable to remove the threat, or the user is not taking the necessary, recommended steps to remediate the problem.

Administrators have the option to configure this feature via the **My OPSWAT Central Management** **Console>Policy Management>Policies>Endpoint Security>Relevant Policy>Advanced Endpoint Protection** tab, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/v6fg7so9q3pw8w010qido952qc1yqk6ru5ivj5yq99zvmhaek88kf4pvx3h8a9g1.png)

Here you will find, and can adjust, the following settings:

- **A local anti-malware detects a threat** ***X*** **times or more in the last** ***X*** **days.**
- **Skip a threat if an infected file doesn’t exist on the system anymore.**
- **Consider an infection as a warning/critical issue if a threat is detected** ***X*** **or more repeated times.**

After adjusting your **Repeated Threat** settings, remember to click **Save**.

> **Support:**
>
> For further queries, concerns or issues regarding **Repeated-Threat Detection On** **My OPSWAT Central Management,** please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
