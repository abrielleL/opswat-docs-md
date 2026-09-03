<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/what-is-a-critical-issue-on-a-policy- -->

# What is a Critical Issue on a policy?

This article applies to the current MetaDefender IT Access Console and all MetaDefender IT Access product releases deployed on Windows, macOS, Linux, Android and iOS systems.

MetaDefender Endpoint reports a wide range of information from managed endpoint devices to MetaDefender IT Access, and while certain compliance, contamination and vulnerability issues may be reported as critical by MetaDefender IT Access alone, what constitutes a critical issue is largely dictated by administrator settings and configured policy.

For Example:

If an organization’s security regulations require that all hard drives on the network be encrypted, the MetaDefender IT Access administrator would ensure that all policies associated with network devices are set to consider and report **No encryption application is installed** as **Critical**. The setting for this example can be found via th**e MetaDefender IT Access** **Console>Policy Management>Policies>Relevant Policy>Laptops/Desktops>Deep Compliance>Encryption**, as shown below.

The same setting for Mobile devices can be found at **MetaDefender IT Access** **Console>Policy Management>Policies>Relevant Policy>Mobile Devices>Deep Compliance>Security & Health**, also shown below.

Once the settings are configured, the administrator will click **Save** to apply the updated policy.

For more information on how to configure policies, please [Read This](https://docs.opswat.com/macloud-sdp/configuration---management/policy-management).

Policy configuration **( MetaDefender IT Access** **Console>Policy Management>Policies>Relevant Policy>Relevant Device Type)** means that, by expanding an issue category and selecting the severity, as illustrated below, administrators can configure a range of device parameters to be treated as **Issues** by MetaDefender IT Access.

Should administrators prefer that certain issues be prioritized as **Critical**, they should also select the box on the right, as illustrated below, before clicking **Save**.

Administrators can view a list of all managed devices reporting with critical issues by following the instructions below.

3. Log into the **MetaDefender IT Access Console** and navigate to **Inventory>Devices** or **Inventory>Device Groups>Relevant Group** ( to search for devices within a group).
4. Click the **Filters** button in the top, right-hand corner of the list, as illustrated below.

Pro Tip:

By configuring certain device parameters to be treated as **Warnings** and others to be treated as **Critical Issues**, administrators can establish various levels of approved access when integrating MetaDefender IT Access API into a secure access solution.

For example, you may wish to set **Warnings** to trigger a warning or placement in a remediation VLAN, while devices with **Critical** issues will be subject to a full network disconnect. To learn more, please [Read This](https://docs.opswat.com/macloud-sdp/integrations/nac-or-ssl-vpn).

Support:

For further queries or concerns regarding **What Constitutes A Critical Issue On A Policy**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
