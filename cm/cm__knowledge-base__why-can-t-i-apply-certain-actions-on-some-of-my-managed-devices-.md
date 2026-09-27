<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-can-t-i-apply-certain-actions-on-some-of-my-managed-devices- -->

# Why can't I apply certain actions on some of my managed devices?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

Certain device actions are only available for specific MetaDefender Endpoint versions, or when certain settings are enabled via policy.

If you perform an action that is not applicable to a device or policy setting, the system will display an error message.

> **Please Note:**
>
> Listed below are the Client version and policy setting requirements for various device Actions.
>
> If a certain Action does not appear on the list, this means that the action is applicable to All Devices, without conditions.

| Action | Minimum Client Version Supported | Additional Information |
| ---- | ---- | ---- |
| **Compliance Check** - Check Applications Security | **Windows** Persistent: 7.6.254.0 On-Demand: 7.3.598.0 **MacOS** Persistent: 10.4.251.0 On-Demand: 10.5.250.0 **Linux** deb: 15.4.10.0 rpm: 15.6.7.0 |  |
| **Compliance Check** - Scan Threats | **Windows** Persistent: 7.6.254.0 On-Demand: 7.3.598.0 **MacOS** Persistent: 10.4.251.0 On-Demand: 10.5.250.0 | Under **Policy Management > Policies > Policy > Advanced Endpoint Protection > Device Scan**, ***Scan threats with a MetaDefender server*** needs to be enabled. |
| **Compliance Check** - Check For OS Updates | **Windows** Persistent: 7.6.254.0 On-Demand: 7.3.598.0 **MacOS** Persistent: 10.4.251.0 On-Demand: 10.5.250.0 |  |
| **Scan Threats** | **Windows** Persistent: 7.6.222.0 On-Demand: 7.3.598.0 **MacOS** Persistent: 10.4.214.0 On-Demand: 10.5.250.0 | Under **Policy Management > Policies > Policy >** **Advanced Endpoint Protection** **> Device Scan**, ***Scan threats with a MetaDefender server*** needs to be enabled. |
| **Fetch Log** | **Windows** Persistent: 7.6.231.0 Domain Controller: 8.0.4.0+ On-Demand: 7.3.2306.158+ **MacOS** Persistent: 10.4.225.0 On-Demand: 10.5.2306.54+ **Linux** deb: 15.4.32.0+ rpm: 15.6.31.0+ |  |
| **Ignore** |  | This action is only applicable to **Unknown** devices. |
| **Undo-Ignore** |  | This action is only applicable to **Ignored** devices. |
| **Re-Identify** | **Windows** Persistent: 7.6.71.0 **MacOS** Persistent: 10.4.123.0 **iOS** Mobile App: 2.39.1 **Android** Mobile App: 2.34 | Under **Settings > Global > Advanced**, ***Custom Information*** needs to be enabled. |
| **Delete** | **All Devices** | This action is applicable for all devices. However, the system only sends an **Uninstall** command to ***persistent*** **MetaDefender Endpoint.** |
| **Get Malware Scan Log** | **Windows** Persistent: 7.6.222.0 **MacOS** Persistent: 10.4.214.0 |  |
| **Approve** | **Windows** **MacOS** **Linux** | This action only applies to non-corporate devices that are not joined to the specified domain and appear with an **Unknown** status |
| **Reboot** | **Windows** Persistent:  7.6.2510.870+ |  |

> **Support:**
>
> If you have further queries, concerns or issues regarding **Why Certain Actions Can’t Be Applied On Some Of Your Managed Devices**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
