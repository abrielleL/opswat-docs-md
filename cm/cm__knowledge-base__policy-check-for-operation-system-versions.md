<!-- source: https://www.opswat.com/docs/cm/knowledge-base/policy-check-for-operation-system-versions -->

# Could I configure a policy to check for operation system versions?

> **Info**
>
> This applies to all operating systems: Windows, macOS, and Linux. Some customizations may be only available for Windows clients only.

Under **Policies**, Administrators can set requirements for managed devices and what operating system versions the devices have installed.

To manage this, navigate to **Policies > Endpoint Security > Relevant Policy > Deep Compliance > Operating System.**

In this section, Administrators can enable **Device is not running an approved operating system version**. From there, release versions can be listed as approved.

![](https://uploads.developerhub.io/prod/97qW/m52mowohp3ou4evd0r9uat0l77yozb73wnek4hujmmyl9t3f7umhqwcjvawe9uxb.png)

Additional customization is available by first setting the condition severity to either **“Warning” or “Critical.”** You can then expand the operating system condition using the ‘+’ option, which allows you to define specific editions and exceptions as part of the compliance check.

> For example, if an administrator has Windows 10 devices and wishes to include all versions except build 10.0.10586, they should input the values as shown below.

![](https://uploads.developerhub.io/prod/97qW/5761czl7w95k62hr7w6w94l8rgshta8rp9nnldix77b1yqlu3931wk0o1cof30m2.png)

> **Support:**
>
> If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
