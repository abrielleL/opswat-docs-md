<!-- source: https://www.opswat.com/docs/mdendpoint/user-guide/what-features-of-metadefender-client-are-available-in-metadefend -->

# What features of MetaDefender Endpoint are available per management platform?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

> **Pro Tip:**
>
> The MetaDefender Endpoint is a lightweight, unobtrusive application, designed to run on every device that is being managed by your account on either MetaDefender IT-OT Access or OPSWAT Central Management v7 (OCM).
>
> MetaDefender Endpoint delivers the device’s security status to the OPSWAT servers and, in turn, channels commands from the servers back to the device to resolve any issues.

## [MetaDefender Client / MetaDefender Endpoint feature comparison:](https://docs.opswat.com/macloud-sdp/kb/what-features-of-metadefender-client-are-available-in-opswat-cli#metadefender-client--metadefender-endpoint-feature-comparison)

| Feature | Standalone | OCM v7 Managed | MDITOT Managed | Notes |
| ---- | ---- | ---- | ---- | ---- |
| **Operating System Support** | Windows | Windows | Windows MacOS Linux Android iOS | Mobile device support compliance check only. |
| **Compliance check** |  | Limited | Yes |  |
| **Vulnerability Assessment** |  |  |  |  |
| Endpoint Vulnerability |  | Application-based | Application-based Missing OS patch-based | Support for Windows and MacOS |
| File-based Vulnerability |  | Yes | Yes | Detect vulnerabilities of scanned files. Support for Windows and MacOS. |
| **Advanced Malware Detection** |  |  |  |  |
| Schedule a scan |  | No | Yes |  |
| On-demand scan |  | Yes | Yes |  |
| Scan option |  | Full scan Memory scan Custom scan Boot records | Full scan Memory scan Custom scan Boot records |  |
| Scan from CLI |  | Yes | Yes | Windows support only |
| **Secure Access** |  |  |  |  |
| IdP SAML |  | No | Yes |  |
| SDP |  | No | Yes |  |
| [3rd party solutions](https://docs.opswat.com/macloud-sdp/integrations) |  | No | Yes | [VMware Unified Access Gateway and Horizon Client](https://docs.opswat.com/macloud-sdp/integrations/vmware-unified-access-gateway) |
| **Remove Unwanted App** |  | Yes | Yes |  |
| **Removable Media Protection** |  | Yes | Yes | Windows support only |
| Device control | Yes | Yes | Yes | Include BadUSB and HID protection |
| Encrypted media |  | No | Yes | [What encrypted media are supported by MetaDefender Endpoint?](https://docs.opswat.com/macloud-sdp/kb/what-encrypted-media-are-supported-by-opswat-client-) |
| Removable media validation | Yes | Yes | Yes |  |
| Integrate with MetaDefender Transfer Guard |  | Yes | Yes |  |
| Secure files download |  | No | Yes | Windows support only. Google Chrome, WhatsApp |
| On-Access file scan |  | No | Yes | Windows support only |
| **User Interface (UI)** |  | Windows | Windows, MacOS and Linux Debian support | -  |
| Localization |  | English, Hebrew, Japanese | English |  |
| Customization |  | No | Admins can customize text and icon |  |
| Tray icon notification |  | Yes | Yes |  |
| **Administration Management** |  |  |  |  |
| Group Management |  | Yes | Yes |  |
| Deployment |  | managed by My OPSWAT v5 support standalone mode | managed by either OPSWAT Central Management v7 (OCM) or MetaDefender IT-OT Access not supported standalone mode |  |

## [Additional feature included:](https://docs.opswat.com/macloud-sdp/kb/what-features-of-metadefender-client-are-available-in-opswat-cli#additional-feature-differences-include)

- **MetaDefender Endpoint** is available in two flavors, and offers unique features for each operating system. To learn more about your options, [Read This](https://docs.opswat.com/macloud-sdp/kb/which-opswat-client-should-i-use-).
- **MetaDefender Endpoint** shows system information and actions via a sleek tray icon and dialogs, while scan progress is shown via the tray icon menu.

> **Pro Tip:**
>
> An alternative solution for Standalone mode is the **OPSWAT Media Validation Agent**, a lightweight tool which ensures that no media can be mounted unless it has first been processed and cleared via the MetaDefender Kiosk.
>
> For more about the **OPSWAT Media Validation Agent**, [Read This](https://docs.opswat.com/mdkiosk/operating/opswat-media-validation-agent). For more about **MetaDefender Kiosk**, [Read This](https://www.opswat.com/products/metadefender/kiosk).

> **Support:**
>
> For any queries or concerns regarding **MetaDefender Endpoint Features And Functionality**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
