<!-- source: https://www.opswat.com/docs/cm/knowledge-base/can-i-block-certain-applications-on-endpoints- -->

# Can I block certain applications on endpoints?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and all MetaDefender Endpoint releases deployed on Windows and macOS systems.

With the incalculable number of applications available for users to download and install (sometimes actively, sometimes inadvertently) it is critical that IT and security professionals establish maximum visibility and control over their network of managed devices.

Shadow IT, riskware, grayware, potentially unwanted applications and potentially unsafe applications are all very real threats that can dramatically increase the chances of a breach, infection, data theft, or other harmful event.

> **Pro Tip:**
>
> MetaDefender Endpoint is designed to rapidly detect and categorize installed applications on each device on which it is installed, while observing which of them are actively running and when.
>
> This information is then encrypted and sent to the My OPSWAT Central Management cloud, where it is added to the database for that device, to be acted upon by the administrator.

To set up application controls for your managed devices via the My OPSWAT Central Management Console, please follow the instructions below.

1. Go to your **My OPSWAT Central Management Console>Policy Management>Policies>The Relevant Policy>Application Control**.
2. You will now see a list of software categories for Windows and macOS devices, along with checkboxes for indicating which rules to be apply to applications in each category, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/zjriw8duomkxqcendb0xmvzy0fs6ul2cvvbazem5foww47xv6dxs12773u933qdr.png)

3. For each category, you can set rules for reporting/consideration, actions to take, and device types to include for each rule.

To set these rules, simply check the appropriate boxes. If you want the system to automatically uninstall or disable certain applications, check the appropriate boxes in the **Actions** column.

4. Click **Save** to apply your settings.

> **Please Note:**
>
> If you set **Actions** (**Uninstall** or **Disable**)  in step 3, no further action is needed. The following steps only apply if, in step 3, you set a policy to treat certain applications (**Installed or Running**) as an issue, but opted not to configure an **Actions** setting.

5. Once your device policy is configured, additional issue categories and/or issue warnings will appear in your **Inventory>Devices>Relevant Device>Detailed Device Information>All Categories** view.

This is illustrated in the screenshot below, where a policy was set against **Antiphishing** software, and so **Antiphishing** appears as an issue warning in red.

![](https://uploads.developerhub.io/prod/97qW/22r2nvnh92fh25m6p7luni5kg96a7hotc7tmpvxef25kuvpw9hrgt1gn9j0phe1z.png)

6. When you click on the issue warning, you will be redirected to the **Application Control** policy page, where you can choose to take further action by either uninstalling or disabling the offending software.

This is done by checking the appropriate box, and clicking **Save**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/4bcc5ivnm9w25fjt2affux72z8f9nc9nr30db0y2nuo6xu4fuuhc0qujx9e7sbne.png)

> **Support:**
>
> If you have any difficulty **Implementing Policies To Block Unwanted Applications Via MetaDefender Endpoint**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
