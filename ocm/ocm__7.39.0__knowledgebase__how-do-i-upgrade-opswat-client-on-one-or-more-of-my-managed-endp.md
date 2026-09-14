<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/how-do-i-upgrade-opswat-client-on-one-or-more-of-my-managed-endp -->

# How do I upgrade MetaDefender Endpoint on one or more of my managed endpoints via the OPSWAT Central Management Console?

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

There is no way to force an upgrade on managed endpoints via the **OPSWAT Central Management Console**. I.e. there is no way to manually upgrade endpoint Clients via the **OPSWAT Central Management Console**.

However, provided automatic updates are enabled via the instructions below, the **Persistent** MetaDefender Endpoint will update automatically on all endpoints as new versions are released.

If a device is offline for an extended period, the version will update as soon as the device is back online.

Please Note:

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

For more information on updating the Persistent and On-Demand MetaDefender Endpoint from the endpoint side, please [Read This](https://docs.opswat.com/ocm/knowledgebase/how-do-i-upgrade-the-opswat-client-from-the-endpoint-side-).

To configure auto-updates on all Persistent Client devices from the OPSWAT Central Management Console, please follow the instructions below.

1. Log into the **OPSWAT Central Management Console** and navigate to the **Settings>Global Settings>Device Agents** tab, then locate the **Agent** section.
2. Check the box alongside the **Allow agents to automatically update to the latest version** option.
3. Click the **Save** button in the upper right-hand corner of the screen to enable your settings.

Pro Tip:

The OPSWAT Central Management system will now ensure that all device Clients update to the latest version automatically and at regular intervals (i.e. following **Compliance Checks**), as needed.

Support:

For further queries, concerns or issues regarding **How do I upgrade** **MetaDefender Endpoint** **on one or more of my managed endpoints via the OPSWAT Central Management Console?**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
