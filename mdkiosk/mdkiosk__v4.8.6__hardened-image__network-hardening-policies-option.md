<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/network-hardening-policies-option -->

# Network Hardening Policies Option

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Purpose](/docs/mdkiosk/v4.8.6/hardened-image/network-hardening-policies-option#purpose)

This article document shows how to enable “Network Hardening Policies Option” for MetaDefender Kiosk during system configuration and what changes will be applied.

## [Solution](/docs/mdkiosk/v4.8.6/hardened-image/network-hardening-policies-option#solution)

To set up “Network Hardening Policies Option” in MD Kiosk, please read through the following guidance for step-by-step instructions.

**Step 1.** Access Kiosk WebMC, navigate to Settings, select System Hardening

**Step 2.** Enable Network Hardening Policies, then click Save Setting. A prompt will appear requesting a system restart.

**Step 3:** Restart the machine to apply the setting.

## [System changes when the option is enabled](/docs/mdkiosk/v4.8.6/hardened-image/network-hardening-policies-option#system-changes-when-the-option-is-enabled)

When the **Network Hardening Policies** option is enabled, certain network-related services will be disabled to enhance system security. As a result, some Kiosk functionalities that rely on these services may be limited or unavailable. Below is a list of affected features

| Feature | Use case | Network Hardening Policies is disabled | Network Hardening Policies is enabled |
| --- | --- | --- | --- |
| Activation | Activate license online | ✔️ | ❌ |
| Engine Update | Update scanning engine online | ✔️ | ❌ |
| File processing with the local Core | Process files with the local MD Core | ✔️ | ✔️ |
| File processing with the remote Core | Process files with the remote MD Core | ✔️ | ❌ |
| Active Directory | Login to Kiosk with Active Directory accounts | ✔️ | ❌ |
| Encrypted USBs | Process files on encrypted USBs | ✔️ | ✔️ |
| USBs with multiple partitions | Process files in media multiple partitions | ✔️ | ✔️ |
| Virtual disks (VHD, VMDK, TIB) | Process files on virtual disk (VHD, VMDK, TIB) | ✔️ | ✔️ |
| Phone, CD, DVD, Blue-ray, Floppy Disk | Process files on different media types (Phone/CD/DVD/Blu-ray/Floppy Disk) | ✔️ | ✔️ |
| MFT Integration | Process, send and retrieve files with MFT | ✔️ | ❌ |
| Shared folder | Copy files and save session logs to a shared folder | ✔️ | ❌ |
| Secure connections (HTTPS) | Enable Secure Connections (HTTPS) | ✔️ | ✔️ |
| Watchdog | Watchdog to monitor the system behavior | ✔️ | ✔️ |
| Email notification | Send email notification for the scan completion | ✔️ | ❌ |
| Syslog | Integrate with syslog server | ✔️ | ❌ |
| System hardening | Enable other Kiosk system hardening options | ✔️ | ✔️ (except for RDP feature) |
| Windows Firewall | Turn on/off Windows Firewall service | ✔️ | ❌ (Firewall service is disabled) |
| Network and IP Address | Configure Kiosk's IP address | ✔️ | ❌ |
| Export/import Kiosk configurations | Export or import Kiosk configuration files | ✔️ | ✔️ |
| Kiosk Hardened Image Upgrade | Upgrade Kiosk Hardened Image online or via Folder | ✔️ | ❌ |

Following network-related services will be disabled:

| Service | Default Status | When Network Hardening Policies is enabled |
| --- | --- | --- |
| AJRouter | Manual | Disabled |
| ALG | Manual | Disabled |
| BFE | Automatic | Disabled |
| BITS | Manual | Disabled |
| CDPSvc | Manual | Disabled |
| cloudidsvc | Manual | Disabled |
| CscService | Manual | Disabled |
| Dhcp | Automatic | Disabled |
| Dnscache | Automatic | Disabled |
| DoSvc | Manual | Disabled |
| dot3svc | Manual | Disabled |
| DsSvc | Manual | Disabled |
| DusmSvc | Manual | Disabled |
| Eaphost | Manual | Disabled |
| edgeupdate | Automatic | Disabled |
| edgeupdatem | Manual | Disabled |
| fdPHost | Manual | Disabled |
| FDResPub | Manual | Disabled |
| IKEEXT | Manual | Disabled |
| InstallService | Manual | Disabled |
| Intel(R) Capability Licensing Service TCP IP Interface | Manual | Disabled |
| iphlpsvc | Automatic | Disabled |
| IpxlatCfgSvc | Manual | Disabled |
| McpManagementService | Manual | Disabled |
| MicrosoftEdgeElevationService | Manual | Disabled |
| MSDTC | Manual | Disabled |
| NcaSvc | Manual | Disabled |
| NcbService | Manual | Disabled |
| NcdAutoSetup | Manual | Disabled |
| Netlogon | Manual | Disabled |
| Netman | Manual | Disabled |
| netprofm | Manual | Disabled |
| NetSetupSvc | Manual | Disabled |
| NgcCtnrSvc | Manual | Disabled |
| NgcSvc | Manual | Disabled |
| NlaSvc | Automatic | Disabled |
| nsi | Automatic | Disabled |
| PeerDistSvc | Manual | Disabled |
| PolicyAgent | Manual | Disabled |
| PrintNotify | Manual | Disabled |
| QWAVE | Manual | Disabled |
| RasMan | Automatic | Disabled |
| SharedRealitySvc | Manual | Disabled |
| shpamsvc | Manual | Disabled |
| SmsRouter | Manual | Disabled |
| SNMPTRAP | Manual | Disabled |
| SstpSvc | Manual | Disabled |
| TrkWks | Manual | Disabled |
| W32Time | Manual | Disabled |
| Wcmsvc | Automatic | Disabled |
| wcncsvc | Manual | Disabled |
| WebClient | Manual | Disabled |
| WEPHOSTSVC | Manual | Disabled |
| WFDSConMgrSvc | Manual | Disabled |
| WinHttpAutoProxySvc | Manual | Disabled |
| WlanSvc | Automatic | Disabled |
| wlpasvc | Manual | Disabled |
| WManSvc | Manual | Disabled |
| workfolderssvc | Manual | Disabled |
| WPDBusEnum | Manual | Disabled |
| WwanSvc | Manual | Disabled |
