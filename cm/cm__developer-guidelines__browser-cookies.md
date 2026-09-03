<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/browser-cookies -->

# Browser Cookies

Because the cookies store non-volatile information (License_Key and Device_ *ID*), the cookies are given a far-future expiration date. Unlike the registry and p-list APIs, My OPSWAT Central Management does not provide policy compliance information in the cookie itself. The intention is for the cookie to be used for identifying the device and securely calling the oAuth APIs to fetch device compliance status.

The injection works only for Windows devices. If the persistent MetaDefender Endpoint is uninstalled, the cookies will be removed with it. If the on-demand  MetaDefender Endpoint is stopped, the cookies will be deleted as the agent shuts down.

Because of XSS protections, cookies are not visible from one domain to another. For this reason, the My OPSWAT Central Management provides a form to specify the domains that require cookie injection.

![](https://uploads.developerhub.io/prod/97qW/kiywehd7ibe4bgfbwembrf0jdrbz2gsrcx2osn7bi9ku7grw8g3ag91d5s9jayos.png)

## Cookie Format

Whenever a cookie injection is scheduled, actually two separate cookies are injected. This allows for either secure or insecure integration types. Format of the two cookies:

| Cookie Name | Device_ID | License_Key |
| ---- | ---- | ---- |
| Content | {Unique Device ID} | {license key} |

Each cookie is also set as follows:

| Host | {hostname configured on your My OPSWAT Central Management account} |  |
| ---- | ---- | ---- |
| Path | / |  |
| Send For | Any connection type |  |
| Expires | Far-future |  |
| Type | Persistent |  |

![](https://uploads.developerhub.io/prod/97qW/zk9rnn18nk32ie69oqkxzhcus4eianortuxgu7p4gf7h7ycup9smo46tba47g2le.png)

![](https://uploads.developerhub.io/prod/97qW/e4yzucnigx4jdjcloanfqqctsidqbcbsf4oj2dkwi2wu4ueszg8uf01hoz9f7j83.png)

**Cookie: License_Key**

The License_Key cookie provides the account license key to which the My OPSWAT Central Management account is associated.

**Cookie: Device_ID**

The Device_ID cookie is provided so the web service can access the richest and most secure information directly from the My OPSWAT Central Management. My OPSWAT Central Management offers [oAuth APIs](https://www.opswat.com/docs/cm/developer-guidelines/how-to-work-with-apis) to get device information. These APIs require either a MAC address or a Device_ID. Since most web services (without the use of Java) cannot query the device’s MAC address, the Device_ ID is made available in this cookie.

**Notes**

- Because the cookies are cleaned-up when  MetaDefender Endpoint is uninstalled (persistent) or stopped (on-demand), the presence of the cookie can be used as an indicator that  MetaDefender Endpoint is running on the endpoint. This is not deterministic though as special cases can arise where  MetaDefender Endpoint is stopped or removed without the cookies being cleaned up, and vice-e-versa a user may delete their cookies without removing  MetaDefender Endpoint (though in this case  MetaDefender Endpoint will try to recreate the cookies from time to time). Cookie injection is automatic as long as  MetaDefender Endpoint is running on the endpoint. It is not configurable.
- The cookie is injected into all detected and supported browsers on the endpoint. Even if one fails, the remaining browsers will still be tried.
- This cookie injection has little to no impact on system resources (CPU, memory, disk IO, etc.)

## Supported browsers

As of November 10th, 2016, the cookie integration is only supported on Windows 7+

| Browser | Persistent agent | On-demand agent with admin | On-demand agent with non-admin |
| ---- | ---- | ---- | ---- |
| Chrome 34+ (ID: 41) | Yes | Yes | Yes |
| Firefox 28+ (ID: 46) | Yes | Yes | Yes |
| Internet Explorer 8+ | No | Yes | Partial |

**Notes:**

- The cookie couldn't be injected if there is at least 1 instance of chrome.exe running
- On Firefox, you need to set baseDomain different with Hostname. If not, the cookie will not be injected
- MetaDefender Endpoint can inject cookie to IE database but IE couldn't transmit the cookie to servers if IE runs protected mode.
- Windows On-demand MetaDefender Endpoint is available with and without UAC. When using the non-UAC version as a user without local administrator rights, the cookie injection will not work with Internet Explorer
