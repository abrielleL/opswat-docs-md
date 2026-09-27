<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/troubleshooting/remediate-no-metadefender-endpoint-is-installed -->

# What should I do if the system reports that no MetaDefender Endpoint is installed on a device?

> **Info**
>
> This article applies to My OPSWAT Central Management, all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems, the current MetaDefender IT Access Console, the current MetaDefender IT Access API.

Should My OPSWAT Central Management or MetaDefender IT Access report that there is no MetaDefender Endpoint installed on a device, the first step is to double check whether this is, in fact, the case.

## [On Windows devices](https://www.opswat.com/docs/macloud-sdp/kb/no-agent-installed-remediation-instruction#on-windows-devices)

1. Open the Windows **Start** menu.
2. Search for **MetaDefender Endpoint.**

![](https://uploads.developerhub.io/prod/2x2P/5ie8uzk6m7l2e4n906yw9uugu0flaid30785glxtu7gpyz630pyklna6o0nlohld.png)

## [On macOS devices](https://www.opswat.com/docs/macloud-sdp/kb/no-agent-installed-remediation-instruction#on-macos-devices)

1. Go to **Finder>Applications**.
2. Search the list for **OPSWAT Gears**.

![](https://uploads.developerhub.io/prod/2x2P/o1eh3nswf48a2iaydx9zoggx1epp0su56vzp4cy3zu491ktg6447mfaqb18fjdz5.png)

## [On Linux devices](https://www.opswat.com/docs/macloud-sdp/kb/no-agent-installed-remediation-instruction#on-linux-devices)

1. Click the **Show Applications** icon.
2. Search for **MetaDefender Endpoint.**

![](https://uploads.developerhub.io/prod/2x2P/vqubod2zjkjvr5xh0bqf1p2gbbq28zeawf8bih1vycqnfy8dkz7wnvgas0f59env.png)

## [On Android/iOS devices](https://www.opswat.com/docs/macloud-sdp/kb/no-agent-installed-remediation-instruction#on-androidios-devices)

1. Search for the **OPSWAT** app.

![](https://uploads.developerhub.io/prod/2x2P/e32zanxmxvbjva875bkyuoncwzbmtvf8yep7pmocva2bc8t7ymxkmogkuqonphun.png)

## [All devices](https://www.opswat.com/docs/macloud-sdp/kb/no-agent-installed-remediation-instruction#all-devices)

If the device does not have the MetaDefender Endpoint installed:

1. Return to the associated **Remediation Page** at **My OPSWAT Central Management** or **MetaDefender IT Access Console>Inventory>Devices>Relevant Device>View Remediation Page**.
2. Click the **Download** button to download the MetaDefender Endpoint installer package.
3. **Install** the MetaDefender Endpoint.

Once you’ve installed the MetaDefender Endpoint on the device, should My OPSWAT Central Management or MetaDefender IT Access still report that no MetaDefender Endpoint is installed, one of the following solutions should apply.

| **Case** | **Solution** |
| ---- | ---- |
| You are on a mobile device | 1. On mobile devices, the system should ask you to open the **OPSWAT Mobile App** to verify your device compliance status. 2. If you do not see this prompt/link, you have likely enabled your Android Chrome browser’s **Desktop Mode**, in which case the MetaDefender IT Access services will not recognize the device. 3. Disable **Desktop Mode** and try again. |
| The device has not enabled loopback for the application you are using to authenticate | 1. Check if the 3rd party vendor can retrieve the **Device ID**. Paste this link into the browser, [https://eapi.opswatgears.com:<port>/opswat/devinfo?count=10&callback=myCallback](https://eapi.opswatgears.comport/) but replace **<port>** with a port configured on your account. For example: [https://eapi.opswatgears.com:11369/opswat/devinfo?count=10&callback=myCallback](https://eapi.opswatgears.com:11369/opswat/devinfo?count=10&callback=myCallback) Ask your administrators for the port number. 2. Try to exempt the application that you are using from authenticating via the loopback restrictions by running the following command: **CheckNetIsolation LoopbackExempt -a -n=”*****<App Container or Package Family>”*** For example: *Microsoft Edge:* **CheckNetIsolation LoopbackExempt -a -n=“Microsoft.Microsoftedge_8wekyb3d8bbwe** **Microsoft”** *Microsoft Work/School Account Windows App:* **CheckNetIsolation LoopbackExempt -a -n=microsoft.aad.brokerplugin_cw5n1h2txyewy** **Note:** to unexempt, run the following command: **CheckNetIsolation LoopbackExempt -d -n=“*****<App Container or Package Family>”*** For example: *Microsoft Edge:* **CheckNetIsolation LoopbackExempt -d -n=“Microsoft.Microsoftedge_8wekyb3d8bbwe** **Microsoft”***Microsoft Work/School Account Windows App:* **CheckNetIsolation LoopbackExempt -d -n=microsoft.aad.brokerplugin_cw5n1h2txyewy** |
| MetaDefender Endpoint is reporting to a different account | 1. **Uninstall** MetaDefender Endpoint from the device. 2. Return to the remediation page at **MetaDefender IT Access Console>Inventory>Devices>Relevant Device>View Remediation Page** and click **Download** to download the OPSWAT Client installer. 3. **Install** the package again from your latest installer download. |
| The MetaDefender Endpoint does not support | 1. **Uninstall** MetaDefender Endpoint from the device. 2. Return to the remediation page at **MetaDefender IT Access Console>Inventory>Devices>Relevant Device>View Remediation Page** and click **Download** to download the MetaDefender Endpoint installer. 3. **Install** the package again from your latest installer download. |
| The MetaDefender Endpoint couldn’t connect to the My OPSWAT Central Management / MetaDefender IT Access Cloud | [Read This](https://www.opswat.com/docs/mdendpoint/kb/how-do-i-configure-opswat-client-to-work-with-a-proxy-or-outboun) for detailed instructions on how to allowlist MetaDefender IT Access addresses. |
| The device is leveraging a proxy service for network traffic | Add an exception for the MetaDefender IT Access **eapi.opswatgears.com** to ensure that traffic to the MetaDefender Endpoint doesn’t go via the proxy. ![](https://uploads.developerhub.io/prod/2x2P/44172boxe97yaq5f6uhske6cse3vyihhu5pg82gqcoqnjvf6712azs28453esu8j.png) |
| DNS service cannot resolve the MetaDefender Endpoint domain | 1. Open a **Command Prompt** (Windows) or **Terminal** (macOS, Linux). 2. Type **nslookup eapi.opswatgears.com** 3. If the domain is not resolved as **127.0.0.1**, please contact your administrators to fix the DNS issue. 4. While waiting for a permanent solution from your administrators, you can add the **eapi.opswatgears.com** domain to a hosts file as a temporary workaround, by following [These Instructions](https://www.opswat.com/docs/mdendpoint/kb/devices-could-not-resolve-cross-domain-api-url). |
| The MetaDefender Endpoint has not fully upgraded | 1. This happens when a device has an **MetaDefender Endpoint** installed that does not support cross-domain API (OPSWAT Client releases prior to Windows **V7.6.121.0**/macOS **V10.4.147.0**) and the device has attempted to upgrade to a newer version, but the upgrade has not been successful. 2. **Uninstall** the MetaDefender Endpoint from the device. 3. Return to the remediation page at **MetaDefender IT Access Console>Inventory>Devices>Relevant Device>View Remediation Page** and click **Download** to download the **MetaDefender Endpoint** installer. 4. Install the package again from your latest installer download. |
| There is a cookie and cache issue | Clean out your browser’s **Cookies** and **Cache** by following [This Guide](https://support.google.com/accounts/answer/32050?co=GENIE.Platform%3DDesktop&hl=en&oco=0). |
| MetaDefender Endpoint services are not running | 1. Open Windows **Task Manager>Services** tab, and click **Open Services**. 2. Look up **OPSWAT Gears Client**. 3. Check if the status is listed as **Running**. 4. If not, please **Restart** the service. |
| None of the above | 1. **Reboot** your machine and try again. 2. If this does not solve the issue, please contact **OPSWAT Support** as instructed below. |

> **Support**
>
> If you have followed the instructions above but **Your System Is Still Reporting That No** **MetaDefender Endpoint** **Is Installed On A Device**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
