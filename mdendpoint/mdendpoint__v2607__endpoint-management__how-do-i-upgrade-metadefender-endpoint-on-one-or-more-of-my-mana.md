<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-upgrade-metadefender-endpoint-on-one-or-more-of-my-mana -->

# How do I upgrade MetaDefender Endpoint on one or more of my managed endpoints via the OPSWAT Central Management Console?

> **Check Your Product:**
>
> This article applies to all My OPSWAT V7.5.0+ releases deployed on Windows or Linux systems, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

There is no way to force an upgrade on managed endpoints via the **My OPSWAT Console**. I.e. there is no way to manually upgrade endpoint Clients via the **My OPSWAT Console**.

However, provided automatic updates are enabled via the instructions below, the **Persistent** MetaDefender Endpoint will update automatically on all endpoints as new versions are released.

If a device is offline for an extended period, the version will update as soon as the device is back online.

> **Please note:**
>
> The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.
>
> For more information on updating the Persistent and On-Demand MetaDefender Endpoint from the endpoint side, please [Read This](https://docs.opswat.com/ocm/knowledgebase/how-do-i-upgrade-the-opswat-client-from-the-endpoint-side-).

To configure auto-updates on all Persistent Client devices from the My OPSWAT Console, please follow the instructions below.

1. Log into the **My OPSWAT Console** and navigate to the **Settings>Global Settings>Device Agents** tab, then locate the **Agent** section.
2. Check the box alongside the **Allow agents to automatically update to the latest version** option.
3. Click the **Save** button in the upper right-hand corner of the screen to enable your settings.

> **Pro Tip:**
>
> The My OPSWAT system will now ensure that all device Clients update to the latest version automatically and at regular intervals (i.e. following **Compliance Checks**), as needed.

> **Support:**
>
> For further queries, concerns or issues regarding **How do I upgrade** **MetaDefender Endpoint** **on one or more of my managed endpoints via the My OPSWAT Console?**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
