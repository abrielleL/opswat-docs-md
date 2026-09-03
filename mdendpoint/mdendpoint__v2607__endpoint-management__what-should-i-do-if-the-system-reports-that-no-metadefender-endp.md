<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/what-should-i-do-if-the-system-reports-that-no-metadefender-endp -->

# What should I do if the system reports that no MetaDefender Endpoint is installed on a device?

> **Info**
>
> This article applies to the current MetaDefender IT-OT Access Console, the current MetaDefender IT-OT Access API, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

Should MetaDefender IT-OT Access report that there is no MetaDefender Endpoint installed on a device, the first step is to double check whether this is, in fact, the case.

## On Windows devices

1. Open the Windows **Start** menu.
2. Search for **MetaDefender Endpoint.**

![](https://uploads.developerhub.io/prod/1yda/besgg37f7opar7i7dxpqo7h2j1pjodvfolfn05hqg0nfy2leqllgjt5gnupxk0y3.png)

## On macOS devices

1. Go to **Finder>Applications**.
2. Search the list for **OPSWAT Gears**.

![](https://uploads.developerhub.io/prod/1yda/54yydqlc6xl97nffvmg5hfdd8cgn258gz9lel1exqit6xjumt9rx4hx5z0pnqlct.png)

## On Linux devices

1. Click the **Show Applications** icon.
2. Search for **MetaDefender Endpoint.**

![](https://uploads.developerhub.io/prod/1yda/4h8v16uw3u9142zf7l9zcs8skcm9dwcp6uz9iqguhveotb1sw2a56qqq5ifezz0b.png)

## On Android/iOS devices

1. Search for the **OPSWAT** app.

![](https://uploads.developerhub.io/prod/1yda/9cpgpkkbiqh2vji2xeqoz2i3i4nwx5zb19fvcjvkpgj2sxc23cj71pbves4teee4.png)

## All devices

If the device does not have the MetaDefender Endpoint installed:

1. Return to the associated **Remediation Page** at **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device>View Remediation Page**.
2. Click the **Download** button to download the MetaDefender Endpoint installer package.
3. **Install** the MetaDefender Endpoint.

Once you’ve installed the MetaDefender Endpoint on the device, should MetaDefender IT-OT Access still report that no MetaDefender Endpoint is installed, one of the following solutions should apply.

| Case | Solutions |
| ---- | ---- |
| You are on a mobile device | 1. On mobile devices, the system should ask you to open the **OPSWAT Mobile App** to verify your device compliance status. 2. If you do not see this prompt/link, you have likely enabled your Android Chrome browser’s **Desktop Mode**, in which case the MetaDefender IT-OT Access services will not recognize the device. 3. Disable **Desktop Mode** and try again. |
| The device has not enabled loopback for the application you are using to authenticate | 1. Check if the 3rd party vendor can retrieve the **Device ID**. Paste this link into the browser, [https://eapi.opswatgears.com:<port>/opswat/devinfo?count=10&callback=myCallback](https://eapi.opswatgears.com:%3Cport%3E/opswat/devinfo?count=10&callback=myCallback) but replace **<port>** with a port configured on your account. For example: [https://eapi.opswatgears.com:11369/opswat/devinfo?count=10&callback=myCallback](https://eapi.opswatgears.com:11369/opswat/devinfo?count=10&callback=myCallback) Ask your administrators for the port number. 1. Try to exempt the application that you are using from authenticating via the loopback restrictions by running the following command: **CheckNetIsolation LoopbackExempt -a -n=”*****<App Container or Package Family>”*** For example: *Microsoft Edge:* **CheckNetIsolation LoopbackExempt -a -n=“Microsoft.Microsoftedge_8wekyb3d8bbwe** **Microsoft”** *Microsoft Work/School Account Windows App:* **CheckNetIsolation LoopbackExempt -a -n=microsoft.aad.brokerplugin_cw5n1h2txyewy** **Note:** to unexempt, run the following command: **CheckNetIsolation LoopbackExempt -d -n=“*****<App Container or Package Family>”*** For example: *Microsoft Edge:* **CheckNetIsolation LoopbackExempt -d -n=“Microsoft.Microsoftedge_8wekyb3d8bbwe** **Microsoft”***Microsoft Work/School Account Windows App:* **CheckNetIsolation LoopbackExempt -d -n=microsoft.aad.brokerplugin_cw5n1h2txyewy** |
| MetaDefender Endpoint is reporting to a different account | 1. **Uninstall** MetaDefender Endpoint from the device. 2. Return to the remediation page at **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device>View Remediation Page** and click **Download** to download the OPSWAT Client installer. 3. **Install** the package again from your latest installer download. |
| The MetaDefender Endpoint does not support | 1. **Uninstall** MetaDefender Endpoint from the device. 2. Return to the remediation page at **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device>View Remediation Page** and click **Download** to download the MetaDefender Endpoint installer. 3. **Install** the package again from your latest installer download. |
| The MetaDefender Endpoint couldn’t connect to the MetaDefender IT-OT Access Cloud | [Read This](Read This) for detailed instructions on how to allowlist MetaDefender IT-OT Access addresses. |
| The device is leveraging a proxy service for network traffic | Add an exception for the MetaDefender IT-OT Access **eapi.opswatgears.com** to ensure that traffic to the MetaDefender Endpoint doesn’t go via the proxy. |
| DNS service cannot resolve the MetaDefender Endpoint domain | 1. Open a **Command Prompt** (Windows) or **Terminal** (macOS, Linux). 2. Type **nslookup eapi.opswatgears.com** 3. If the domain is not resolved as **127.0.0.1**, please contact your administrators to fix the DNS issue. 4. While waiting for a permanent solution from your administrators, you can add the **eapi.opswatgears.com** domain to a hosts file as a temporary workaround, by following [These Instructions](These Instructions). |
| The MetaDefender Endpoint has not fully upgraded | 1. This happens when a device has an **MetaDefender Endpoint** installed that does not support cross-domain API (OPSWAT Client releases prior to Windows **V7.6.121.0**/macOS **V10.4.147.0**) and the device has attempted to upgrade to a newer version, but the upgrade has not been successful. 2. **Uninstall** the MetaDefender Endpoint from the device. 3. Return to the remediation page at **MetaDefender IT-OT Access Console>Inventory>Devices>Relevant Device>View Remediation Page** and click **Download** to download the **MetaDefender Endpoint** installer. 4. Install the package again from your latest installer download. |
| There is a cookie and cache issue | Clean out your browser’s **Cookies** and **Cache** by following [This Guide](This Guide). |
| MetaDefender Endpoint services are not running | 1. Open Windows **Task Manager>Services** tab, and click **Open Services**. 2. Look up **OPSWAT Gears Client**. 3. Check if the status is listed as **Running**. 4. If not, please **Restart** the service. |
| None of the above | 1. **Reboot** your machine and try again. 2. If this does not solve the issue, please contact **OPSWAT Support** as instructed below. |

> **Support:**
>
> If you have followed the instructions above but **Your System Is Still Reporting That No** **MetaDefender Endpoint** **Is Installed On A Device**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
