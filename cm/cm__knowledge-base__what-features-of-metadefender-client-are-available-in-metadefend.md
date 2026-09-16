<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-features-of-metadefender-client-are-available-in-metadefend -->

# What features of MetaDefender Client are available in MetaDefender Endpoint?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

> **Pro Tip:**
>
> The MetaDefender Endpoint is a lightweight, unobtrusive application, designed to run on every device that is being managed by your account on either My OPSWAT Central Management or My OPSWAT.
>
> MetaDefender Endpoint delivers the device’s security status to the OPSWAT servers and, in turn, channels commands from the servers back to the device to resolve any issues.

## MetaDefender Client / MetaDefender Endpoint feature comparison:

| Feature | MetaDefender Client | MetaDefender Endpoint | Notes |
| ---- | ---- | ---- | ---- |
| **Operating System Support** | Windows | Windows macOS Linux Android iOS |  |
| **Compliance check** | Limited | Yes |  |
| **Vulnerability Assessment** |  |  |  |
| Endpoint Vulnerability | Application-based | Application-based Missing OS patch-based |  |
| File-based Vulnerability | Yes | Yes | detect vulnerabilities of scanned files |
| **Advanced Malware Detection** |  |  |  |
| Schedule a scan | No | Yes |  |
| On-demand scan | Yes | Yes |  |
| Scan option | Full scan Memory scan Custom scan Boot records | Full scan Memory scan Custom scan Boot records |  |
| Scan from CLI | Yes | Yes |  |
| **Secure Access** |  |  |  |
| IdP SAML | No | Yes |  |
| SDP | No | Yes |  |
| [NAC or SSL VPN](https://www.opswat.com/docs/cm/secure-access-solution/nac-or-ssl-vpn) | No | Yes | [Omnissa Unified Access Gateway](https://www.opswat.com/docs/cm/secure-access-solution/vmware-unified-access-gateway) |
| **Remove Unwanted App** | Yes | Yes |  |
| **Removable media protection** | Yes | Yes |  |
| Encrypted media | No | Yes [What encrypted media are supported by MetaDefender Endpoint?](https://www.opswat.com/docs/cm/knowledge-base/what-encrypted-media-are-supported-by-metadefender-endpoint-) |  |
| Support manifest file | Yes | Yes |  |
| Integrate with MetaDefender Managed File Transfer | Yes | Yes |  |
| **User Interface (UI)** | Yes | Yes |  |
| Localization | English, Hebrew, Japanese | English |  |
| Customization | No | Admins can customize text and icon. |  |
| **Administration Management** |  |  |  |
| Group Management | Yes | Yes |  |
| Deployment | managed by My OPSWAT v5 support standalone mode | managed by either My OPSWAT v7 or My OPSWAT Central Management not supported standalone mode 4 |  |

## Additional feature differences include:

- **MetaDefender Endpoint** is available in two flavors, and offers unique features for each operating system. To learn more about your options, [Read This](https://www.opswat.com/docs/cm/kb/which-opswat-client-should-i-use-).
- **MetaDefender Endpoint** shows system information and actions via a sleek tray icon and dialogs, while scan progress is shown via the tray icon menu.
- **MetaDefender Client** detects installed applications with compliance state, so administrators are not able to define security policies to assess risks on devices.

> **Pro Tip:**
>
> An alternative solution for Standalone mode is the **MetaDefender Media Validation Driver**, a lightweight tool which ensures that no media can be mounted unless it has first been processed and cleared via the MetaDefender Kiosk.
>
> For more about the **MetaDefender Media Validation Driver**, [Read This](https://docs.opswat.com/mdkiosk/operating/opswat-media-validation-agent). For more about **MetaDefender Kiosk**, [Read This](https://www.opswat.com/products/metadefender/kiosk).

> **Support:**
>
> For any queries or concerns regarding **MetaDefender Client VS MetaDefender Endpoint Features And Functionality**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
