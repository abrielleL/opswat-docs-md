<!-- source: https://www.opswat.com/docs/mdendpoint/user-guide/which-metadefender-endpoint-should-i-use- -->

# Which MetaDefender Endpoint should I use?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

The MetaDefender Endpoint is available in two unique flavors:

- **The Persistent MetaDefender Endpoint:**
  - Designed to run perpetually, following installation on the user’s device.
  - Starts running whenever the user’s system is booted up and stops only when the user shuts down.
- **The On-Demand MetaDefender Endpoint:**
  - Designed to run only when needed.
  - Must be switched on after the system boots up and switches off as soon as the Client is exited or the user shuts down/restarts the system.

> **Pro Tip**
>
> Typical uses for the **On-Demand MetaDefender Endpoint** include:
>
> - Bundling with a secure access control solution, such as VMWare UAG, NAC or SSL-VPN Host Checker for on-demand compliance checks.
> - On demand compliance and security checks on devices on which software installation is prohibited.
> - Bring your own device (BYOD) access, such as on a guest, contractor, student or employee’s personal laptop, tablet, or mobile phone.
>
> There are two versions of the **On-Demand MetaDefender Endpoint** available for **Windows** devices. When selecting the appropriate option, there are certain permissions concerns to keep in mind, namely:
>
> - One version requires user account control (UAC), while the other does not.
> - Running the non-UAC client without admin rights as, such as in the BYOD use case above, will offer a slightly degraded experience.
> - The malware deep scanning option will be limited.
> - Some applications detections will be less accurate, and BitLocker disk encryption state cannot be checked for the non-admin On-Demand Client.

In selecting the right flavor and version of the MetaDefender Endpoint for your enterprise needs, and for use through your range of managed devices, please make the most of the following feature guide, which compares the On-Demand and Persistent MetaDefender Endpoint across all platforms (Windows, macOS, Linux).

##

Configurations & Specifications

| Attributes | Windows |  | macOS |  | Linux |
| ---- | ---- | ---- | ---- | ---- | ---- |
| **Features** | **Persistent** | **On-Demand** | **Persistent** | **On-Demand** | **Persistent** |
| **Installation** | Required |  | Required |  | Required |
| **Package Format** | MSI | EXE | DMG PKG | ZIP | RPM DEB |
| **Integrations:** allow 3rd party to read device compliance status or device ID |  |  |  |  |  |
| - Registry or .plist | ✅ | ✅ | ✅ | ✅ |  |
| - Cookie | ✅ | ✅ | ✅ | ✅ |  |
| - Client Certificate | ✅ | ✅ | ✅ | ✅ |  |
| - Cross-domain API | ✅ | ✅ | ✅ | ✅ | ✅ |
| **User Interface** |  |  |  |  |  |
| - Main UI* | ✅ |  | ✅ |  | ✅ |
| - Command Line (4) | ✅ | ✅ |  | ✅ | ✅ |
| - Tray Icon | ✅ | ✅ | ✅ | ✅ | ✅ |
| - On-Demand re-check compliance status | ✅ | ✅ | ✅ | ✅ | ✅ |
| - Detailed custom guide to remediate issues | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Automatic Update** | ✅ |  | ✅ |  | ✅ |
| **Application Context** | System | User | System | User | System |
| Remote Fetch Log | ✅ |  | ✅ |  |  |
| [On-Demand Actions](On-Demand Actions) | ✅ | ✅ | ✅ |  | ✅ |
| Custom UI (5) | ✅ | ✅ | ✅ | ✅ |  |

> ***NOTE**
>
> Although there is Main UI available on MacOS & Linux platforms, some features might not be available yet

## Features

### Advanced Endpoint Protection

| **Features** | **Windows** |  | **macOS** |  | **Linux** |
| ---- | ---- | ---- | ---- | ---- | ---- |
| **Features** | **Persistent** | **On-Demand** | **Persistent** | **On-Demand** | **Persistent** |
| **Peripheral Media Protection** | ✅ |  |  |  |  |
| **Peripheral Device Control** | ✅ |  |  |  |  |
| **BadUSB Protection** | ✅ |  |  |  |  |
| **Malware Scan** | ✅ | ✅ |  |  |  |
| **Download Protection** | ✅ |  |  |  |  |
| **Advanced Malware Detection (3)** | ✅ | ✅ | ✅ |  | ✅ |
| **Managed File Transfer** | ✅ |  |  |  |  |
| **Secure Access** |  |  |  |  |  |
| - Via SDP Gateway | ✅ |  | ✅ |  | ✅ |
| - Via SAML IdP | ✅ | ✅ | ✅ | ✅ | ✅ |

### Vulnerability & Patch Management

| Features | Windows |  | Macintosh |  | Linux v4 |
| ---- | ---- | ---- | ---- | ---- | ---- |
|  | **Persistent** | **On-Demand (1)** | **Persistent** | **On-Demand** | **Persistent** |
| Vulnerabilities And Exposures | ✅ | ✅ | ✅ | ✅ | ✅ |
| Patch Management | ✅ | ✅ | ✅ | ✅ |  |

### Device Compliance

| Features | Windows |  | Macintosh |  | Linux v4 |
| ---- | ---- | ---- | ---- | ---- | ---- |
|  | **Persistent** | **On-Demand (1)** | **Persistent** | **On-Demand** | **Persistent** |
| Anti-Malware | ✅ | ✅ | ✅ | ✅ | ✅ |
| Encryption | ✅ | ✅ | ✅ | ✅ | ✅ |
| User Authentication | ✅ | ✅ | ✅ | ✅ | ✅ |
| Antiphishing | ✅ | ✅ | ✅ | ✅ | ✅ |
| Backup | ✅ | ✅ | ✅ | ✅ |  |
| Firewall | ✅ | ✅ | ✅ | ✅ | ✅ |
| Hard Drive | ✅ | ✅ |  |  |  |
| Operating System | ✅ | ✅ | ✅ | ✅ | ✅ |
| Custom Check | ✅ | ✅ | ✅ | ✅ | ✅ |

### AppRemoval

MetaDefender Endpoint can detect unwanted applications and remove/stop applications without user intervention – including password-protected or corrupted/incomplete installations. Currently, we also support many categories such as: Peer-to-Peer, Data Loss Prevention and many categories under Deep compliance.

| Features | Windows Persistent | Windows **On-Demand (1)** |
| ---- | ---- | ---- |
| Cloud Storage | ✅ | ✅ |
| Developer Tool | ✅ | ✅ |
| Media Player | ✅ | ✅ |
| Uninstaller | ✅ | ✅ |
| Toolbar | ✅ | ✅ |
| Chat/IM | ✅ | ✅ |
| Cleaner / Optimizer | ✅ | ✅ |
| VPN Client | ✅ | ✅ |
| Remote Control | ✅ | ✅ |
| Unclassified PUA | ✅ | ✅ |

### Mobile

| Features | iOS | Android | Chrome OS |
| ---- | ---- | ---- | ---- |
| Screen lock and passcode | ✅ | ✅ |  |
| Detect if the device is rooted or jailbroken |  | ✅ | ✅ |
| Internal storage encryption state | ✅ | ✅ | ✅ |
| Operating System detection | ✅ | ✅ | ✅ |
| Threat Detection (Installed Apps) |  | ✅ |  |

> **Feature Guide Key:**
>
> **(1)** The Windows **On-Demand MetaDefender Endpoint** cannot perform certain compliance checks due to admin-permission requirements when the Client is running.
>
> **(2)** The MetaDefender Endpoint is no longer supports these checks on macOS. If an administrator enables these checks in a Security Policy, the checks will fail on the following OS versions:
>
> - Detect lock screen timeout on macOS 10.13+
> - Detect hard disk free space on macOS 10.14+
>
> **(3)** If the MetaDefender Endpoint runs without admin rights, it cannot scan processes that run only with admin/system rights, or files that are protected by admin permission.
>
> **(4)** MetaDefender Endpoint supports some CLI (command line interface) input, to allow administrators to customize how the Client runs or performs on-demand actions:
>
> - By default, once the **On-Demand MetaDefender Endpoint** is running, it will keep running until it is closed or the system is restarted. However, this can be customized via command line options. For more information, [Read This](https://www.opswat.com/configuration---management/on-demand-client-cli).
> - The **Persistent MetaDefender Endpoint** offers a utility too that allows users to scan folders/files with a MetaDefender server. To learn more, [Read This](https://www.opswat.com/configuration---management/scan-files-folder-cli).
>
> **(5)** The MetaDefender Endpoint offers the option for a customized tray icon and text on the client UI (including the tray-icon menu, notifications, and more):
>
> - This feature is only available for Enterprise customers.
> - To receive a user interface rebranding package, and for the steps necessary to enable this feature, please contact OPSWAT Support, and [Read This](https://www.opswat.com/kb/how-do-i-change-text-on-opswat-client-ui-).

> **Support:**
>
> For further queries or concerns regarding the **MetaDefender Endpoint and Its Suitability for Your Enterprise**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
