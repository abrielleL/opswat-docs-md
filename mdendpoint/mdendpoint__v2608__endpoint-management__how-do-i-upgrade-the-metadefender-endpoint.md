<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-upgrade-the-metadefender-endpoint -->

# How do I upgrade the MetaDefender Endpoint from the endpoint side?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

## Persistent MetaDefender Endpoint

For Persistent MetaDefender Endpoint, there is no need for manual upgrades from the MetaDefender Endpoint side, nor is there a method in place to do so.

Unless the automatic updates are disabled (via the **MetaDefender IT-OT Access** **Console>Settings>Global Settings>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.

If the device is offline for an extended period, the version will update as soon as the device is back online.

## On-Demand MetaDefender Endpoint

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

If failure to update puts an On-Demand Client endpoint in breach of a configured **MetaDefender IT-OT Access** **Device Policy**, the endpoint user will be notified of their **Non-Compliant** state with an on-screen banner, which will direct them to a **Remediation Page** featuring the appropriate upgrade steps.

If failure to update does not breach any configured policy, an On-Demand Client user can still manually upgrade from the endpoint side as follows:

1. Log into the [OPSWAT Portal](https://portalv1.opswat.com/products/endpoint-clients) and navigate to the **Products>Endpoint Clients** page (Portal V1) or **Products>Downloadable Products>Endpoint Clients** (Portal V2).
2. Locate the appropriate **On-Demand** **MetaDefender Endpoint** package for your operating system, then click the **Download** button.

![](https://uploads.developerhub.io/prod/2x2P/cx2l1c6c2twzq0ym8oj5uea6hqjrwktqyui6kdgp24ma5xwch62my793nyxwurly.png)

![](https://uploads.developerhub.io/prod/2x2P/no022hl5lpk879tud6sz1uhe8m6xso6ltxsas5uk52z9fl2pqtdb3lcuzsyf840v.png)

3. **Run** the package installer **Wizard**, and it will automatically replace your existing install with the latest On-Demand Client version.

> **Support:**
>
> If you have followed the instructions above but are **Unable To Update** **MetaDefender Endpoint** **Via Your Endpoint**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
