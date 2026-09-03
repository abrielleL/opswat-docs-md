<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-do-i-upgrade-the-opswat-client-from-the-endpoint-side- -->

# How do I upgrade the MetaDefender Endpoint from the endpoint side?

This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

## [Persistent MetaDefender Endpoint](/docs/ocm/knowledgebase/how-do-i-upgrade-the-opswat-client-from-the-endpoint-side-#persistent-metadefender-endpoint)

For Persistent MetaDefender Endpoint, there is no need for manual upgrades from the Client side, nor is there a method in place to do so.

Unless the automatic updates are disabled (via the **OPSWAT Central Management Console>Settings>Global Settings>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.

If the device is offline for an extended period, the version will update as soon as the device is back online.

---

## [On-Demand MetaDefender Endpoint](/docs/ocm/knowledgebase/how-do-i-upgrade-the-opswat-client-from-the-endpoint-side-#on-demand-metadefender-endpoint)

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

If failure to update puts an On-Demand Client endpoint in breach of a configured **OPSWAT Central Management Device Policy**, the endpoint user will be notified of their **Non-Compliant** state with an on-screen banner, which will direct them to a **Remediation Page** featuring the appropriate upgrade steps.

If failure to update does not breach any configured policy, an On-Demand Client user can still manually upgrade from the endpoint side as follows:

1. Log into the MyOPSWAT and navigate to Products>Downloadable Products>Endpoint Clients
2. Locate the appropriate **On-Demand** **MetaDefender Endpoint** package for your operating system, then click the **Download** button.

3. **Run** the package installer **Wizard**, and it will automatically replace your existing install with the latest On-Demand Client version.

Support:

For further queries, concerns or issues regarding **How do I upgrade the** **MetaDefender Endpoint** **from the endpoint side?**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
