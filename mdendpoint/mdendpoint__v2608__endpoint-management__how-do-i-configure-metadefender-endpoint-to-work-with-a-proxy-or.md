<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-configure-metadefender-endpoint-to-work-with-a-proxy-or -->

# How do I configure MetaDefender Endpoint to work with a proxy or outbound firewall?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux or macOS systems.

## Non-Authenticated Proxies

MetaDefender Endpoint is designed to automatically detect a computer’s configured proxy and then apply the same settings.

So, no manual configuration is required for the MetaDefender Endpoint to work with a non-authenticated proxy.

## Authenticated Proxies

Authenticated proxies are not supported.

MetaDefender Endpoint will always attempt to connect directly before using a proxy, so either firewall or proxy exceptions will need to be made.

The proxy will have to be configured to exempt MetaDefender Endpoint from authenticating.

> **Pro Tip:**
>
> The following domains should be exempted from either the firewall or the proxy. Please note that all traffic is on **port 443**.
>
> - These four entries:
>   - [https://*.opswat.com/](about:blank)
>   - [https://*.opswatgears.com/](about:blank)
>   - [https://*.metadefender.com/](about:blank)
>   - [https://softwareopswat-a.akamaihd.net/](https://softwareopswat-a.akamaihd.net/)
>
> And:
>
> - This single entry:
>   - [https://opswat-gears_.__s3._amazonaws.com/](https://opswat-gears.s3.amazonaws.com/) Or …
> - The following three entries:
>   - [https://opswat-gears-cloud.s3-us-west-2.amazonaws.com/](about:blank)
>   - [https://opswat-gears-cloud-clients.s3-us-west-2.amazonaws.com/](https://opswat-gears-cloud.s3-us-west-2.amazonaws.com/)
>   - [https://opswat-gears-fetch-log.s3.amazonaws.com](https://opswat-gears-fetch-log.s3.amazonaws.com/)
>
> Please contact Support by following the instructions below.

> **Support:**
>
> For advice on how to **Exempt By User Client String** or if you have trouble with **Allowlist Domain URLs**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
