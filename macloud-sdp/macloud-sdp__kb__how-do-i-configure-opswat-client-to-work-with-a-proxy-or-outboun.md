<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-configure-opswat-client-to-work-with-a-proxy-or-outboun -->

# How do I configure MetaDefender Endpoint to work with a proxy or outbound firewall?

This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux or macOS systems.

## [Non-Authenticated Proxies](/docs/macloud-sdp/kb/how-do-i-configure-opswat-client-to-work-with-a-proxy-or-outboun#non-authenticated-proxies)

MetaDefender Endpoint is designed to automatically detect a computer’s configured proxy and then apply the same settings.

So, no manual configuration is required for the MetaDefender Endpoint to work with a non-authenticated proxy.

## [Authenticated Proxies](/docs/macloud-sdp/kb/how-do-i-configure-opswat-client-to-work-with-a-proxy-or-outboun#authenticated-proxies)

Authenticated proxies are not supported.

MetaDefender Endpoint will always attempt to connect directly before using a proxy, so either firewall or proxy exceptions will need to be made.

The proxy will have to be configured to exempt MetaDefender Endpoint from authenticating.

Pro Tip:

The following domains should be exempted from either the firewall or the proxy. Please note that all traffic is on **port 443**.

- These four entries:

  - [https://*.opswat.com/](/docs/macloud-sdp)
  - [https://*.opswatgears.com/](/docs/macloud-sdp)
  - [https://*.metadefender.com/](/docs/macloud-sdp)
  - <https://softwareopswat-a.akamaihd.net/>

And:

- This single entry:

  - [https://opswat-gears_.__s3._amazonaws.com/](https://opswat-gears.s3.amazonaws.com/) Or …
- The following three entries:

  - [https://opswat-gears-cloud.s3-us-west-2.amazonaws.com/](/docs/macloud-sdp)
  - [https://opswat-gears-cloud-clients.s3-us-west-2.amazonaws.com/](https://opswat-gears-cloud.s3-us-west-2.amazonaws.com/)
  - <https://opswat-gears-fetch-log.s3.amazonaws.com>

Please contact Support by following the instructions below.

Support:

For advice on how to **Exempt By User Client String** or if you have trouble with **Allowlist Domain URLs**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
