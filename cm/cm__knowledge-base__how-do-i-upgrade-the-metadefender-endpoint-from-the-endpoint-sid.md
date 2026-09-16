<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-upgrade-the-metadefender-endpoint-from-the-endpoint-sid -->

# How do I upgrade the MetaDefender Endpoint from the endpoint side?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

## Persistent MetaDefender Endpoint

For Persistent MetaDefender Endpoint, there is no need for manual upgrades from the MetaDefender Endpoint side, nor is there a method in place to do so.

Unless the automatic updates are disabled (via the **My OPSWAT Central Management** **Console>Settings>Global Settings>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.

If the device is offline for an extended period, the version will update as soon as the device is back online.

## On-Demand MetaDefender Endpoint

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

If failure to update puts an On-Demand Client endpoint in breach of a configured **My OPSWAT Central Management** **Device Policy**, the endpoint user will be notified of their **Non-Compliant** state with an on-screen banner, which will direct them to a **Remediation Page** featuring the appropriate upgrade steps.

If failure to update does not breach any configured policy, an On-Demand Client user can still manually upgrade from the endpoint side as follows:

1. Log into the [OPSWAT Portal](https://my.opswat.com/home/metadefender-endpoint) and navigate to the **Product Downloads >** **MetaDefender Endpoint**
2. Locate the appropriate **On-Demand** **MetaDefender Endpoint** package for your operating system, then click the **Download** button.

![](https://uploads.developerhub.io/prod/1yda/j878tsusfa8xdk3ci9soo40vag2abhio6fz9ed7qywk5f1z2d1t6gjgtwblmgwav.png)

![](https://uploads.developerhub.io/prod/1yda/ehuzc40vur8sjng9wuqw8yujjj510n25v80cjmeht2per7vjwezrjv2by28gyeob.png)

3. **Run** the package installer **Wizard**, and it will automatically replace your existing install with the latest On-Demand Client version.

> **Support:**
>
> If you have followed the instructions above but are **Unable To Update** **MetaDefender Endpoint** **Via Your Endpoint**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
