<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-is-a-critical-issue-on-a-policy- -->

# What is a Critical Issue on a policy?

MetaDefender Endpoint reports a wide range of information from managed endpoint devices to My OPSWAT Central Management, and while certain compliance, contamination and vulnerability issues may be reported as critical by My OPSWAT Central Management alone, what constitutes a critical issue is largely dictated by administrator settings and configured policy.

> **For Example:**
>
> If an organization’s security regulations require that all hard drives on the network be encrypted, the administrator would ensure that all policies associated with network devices are set to consider and report **No encryption application is installed** as **Critical**. The setting for this example can be found via th**e** **Console>Policy Management>Policies>Relevant Policy>Laptops/Desktops>Deep Compliance>Encryption**, as shown below.
>
> ![](https://uploads.developerhub.io/prod/97qW/dae6fcgydxk354sn48mtt5b2jd37tcpzfiv2h04mvp0u0204lo9dietcbq2iepc9.png)
>
> The same setting for Mobile devices can be found at **Console>Policy Management>Policies>Relevant Policy>Mobile Devices>Deep Compliance>Security & Health**, also shown below.
>
> ![](https://uploads.developerhub.io/prod/97qW/2xo3wrogaksce2ozdgukrll8cfzzsovne40i7j5xd775qsu9e3anx1aqm7hvfh82.png)
>
> Once the settings are configured, the administrator will click **Save** to apply the updated policy.
>
> For more information on how to configure policies, please [Read This](https://docs.opswat.com/macloud-sdp/configuration---management/policy-management).

Policy configuration **( Console>Policy Management>Policies>Relevant Policy>Relevant Device Type)** means that, by expanding an issue category and selecting the severity, as illustrated below, administrators can configure a range of device parameters to be treated as **Issues** by My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/qllj70amy8fmmwnl9g5cbq7evc7oyq1dbpknhe3yok8kmxtw2s26nlfe5xuvv9ld.png)

Should administrators prefer that certain issues be prioritized as **Critical**, they should also select the box on the right, as illustrated below, before clicking **Save**.

![](https://uploads.developerhub.io/prod/97qW/0cws5pdp8dewjs1p05evod992h2egdv7rynhyhgn9fhimfve0sjxxa72krj8jdbi.png)

Administrators can view a list of all managed devices reporting with critical issues by following the instructions below.

3. Log into the **My OPSWAT Central Management Console** and navigate to **Inventory>Devices** or **Inventory>Device Groups>Relevant Group** ( to search for devices within a group).
4. Click the **Filters** button in the top, right-hand corner of the list, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/zoagcx45f8iwgadil6agaxxjvuyit9jpqfbum4tswphvjze3yqicjm0zoq4n3uob.png)

> **Pro Tip:**
>
> By configuring certain device parameters to be treated as **Warnings** and others to be treated as **Critical Issues**, administrators can establish various levels of approved access when integrating MetaDefender IT Access API into a secure access solution.
>
> For example, you may wish to set **Warnings** to trigger a warning or placement in a remediation VLAN, while devices with **Critical** issues  will be subject to a full network disconnect. To learn more, please [Read This](https://docs.opswat.com/macloud-sdp/integrations/nac-or-ssl-vpn).

> **Support:**
>
> For further queries or concerns regarding **What Constitutes A Critical Issue On A Policy**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
