<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/why-is-the-exclude-cd-feature-in-opswat-client-not-working-on-on -->

# Why is the Exclude CD feature in MetaDefender Endpoint not working on one or more of my managed devices?

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

OPSWAT Central Management administrators, who have enabled and configured **Threat Detection** on a given **Device Policy**, may find that the **Exclude CD** option, configurable under the **OPSWAT Central Management Console>Device Policies>Threat Detection>Removable Media**, does not seem to be working on one or more of the managed endpoints assigned to that policy, even though the option is enabled.

This is more than likely the result of certain devices still running **MetaDefender Endpoint** **V7.6.575.0 (Windows) or prior**, or **MetaDefender Endpoint** **V10.4.385.0 (macOS) or prior,** which versions do not support the **Exclude CD** functionality. To remedy this issue, please follow the instructions below.

## [Add a version compliance rule to flag outdated devices](/docs/ocm/7.39.0/knowledgebase/why-is-the-exclude-cd-feature-in-opswat-client-not-working-on-on#add-a-version-compliance-rule-to-flag-outdated-devices)

1. Log into the OPSWAT Central Management Console and navigate to Device Policies>Chosen Policy>Compliance, then click the Add New Rule button, as illustrated below.

2. In the vacant slot, click the **Plus** symbol, as illustrated below, then select **Add an agent version condition** from the pop-up menu.

3. In the space provided, type the minimum MetaDefender Endpoint version required for this feature, namely **7.6.575.0**.
4. Repeat the process by clicking the **Plus** symbol and adding the same rule for macOS, if applicable, but substituting with **10.4.385.0**, which is the macOS equivalent for support of this feature.

There is no need to click the **Add New Rule** button in the upper right again, as all variations will fall within the same rule.

Operating systems can be selected by clicking the underlined **Window**s text that appears in the default rule, then selecting the operating system from the pop-up list, as illustrated below.

5. With your new rule configured, click the **Add Rule** button, then click the **Save** button in the lower right-hand corner of the screen.

6. Enter your administrator **PIN** in the pop-up box, as prompted, then click **Save** again to implement your settings.

Pro Tip:

You can now easily track Non-Compliant devices by navigating to the **OPSWAT Central Management Console>Dashboard>Compliance**, and noting which devices have been flagged for running a prohibited Client version.

If you see non-compliant devices that are flagged for this reason, continue with the remediation instructions in the last section of this article to configure automatic, remote updates.

Pro Tip:

Unless the automatic updates are disabled (via the **OPSWAT Central Management Console>Settings>Global Settings>Device Agents** tab), the PersistentMetaDefender Endpoint will update automatically as new versions are released.

If the device is offline for an extended period, the version will update as soon as the device is back online.

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

For more information on updating the Persistent and On-Demand MetaDefender Endpoint from the endpoint side, please Read This.

---

## [Manually checking device versions to see whether some devices are running an outdated Client version](/docs/ocm/7.39.0/knowledgebase/why-is-the-exclude-cd-feature-in-opswat-client-not-working-on-on#manually-checking-device-versions-to-see-whether-some-devices-are-running-an-outdated-client-version)

1. Log into the **OPSWAT Central Management Console** and navigate to the **Inventory>Devices** tab.
2. Manually scan the list, or enter the device IDs, usernames, group names, IP addresses, or MAC addresses of devices under the relevant policy into the search field and run the **Search**.
3. Client version details will be listed in the **Agent Version** column, as illustrated below. Look for devices running **MetaDefender Endpoint version 7.6.575.0 or prior**, and if any are present, follow the instructions in the next section of this article to remediate.

---

## [Configure a Global Device settings to automatically update MetaDefender Endpoint to the latest version](/docs/ocm/7.39.0/knowledgebase/why-is-the-exclude-cd-feature-in-opswat-client-not-working-on-on#configure-a-global-device-settings-to-automatically-update-metadefender-endpoint-to-the-latest-version)

1. Log into the **OPSWAT Central Management Console** and navigate to the **Settings>Global Settings>Device Agents** tab, then locate the **Agent** section.
2. Check the box alongside the **Allow agents to automatically update to the latest version** option.
3. Click the **Save** button in the upper right-hand corner of the screen to enable your settings.

Pro Tip:

The OPSWAT Central Management system will now ensure that all device Clients update to the latest version automatically and at regular intervals, as needed (following **Compliance Checks**), thereby enabling the **Exclude CD** function on all Clients, provided the function is enabled under the assigned **Device Policy**.

Pro Tip:

Unless the automatic updates are disabled (via the **OPSWAT Central Management Console>Settings>Global Settings>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.

If the device is offline for an extended period, the version will update as soon as the device is back online.

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

For more information on updating the Persistent and On-Demand MetaDefender Endpoint from the endpoint side, please Read This.

Support:

If you have followed the instructions above and installed the latest MetaDefender Endpoint on all of your managed devices, but find that the **Exclude CD Feature In** MetaDefender Endpoint **Is Still Not Working On Your Managed Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
