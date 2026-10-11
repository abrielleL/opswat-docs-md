<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements -->

# Kiosk System Requirements

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Hardware requirements](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#hardware-requirements)

**MetaDefender Kiosk System Requirements**

When MetaDefender Kiosk is installed on a **separate system** from MetaDefender Core, the following specifications are required:

- **Processor:** Quad-core or higher
- **Memory:** Minimum 4 GB RAM
- **Storage:** At least 10 GB available hard drive space
- **Operating System:** 64-bit architecture version

If MetaDefender Kiosk and Core are installed on the **same system**, please refer to the MetaDefender Core user guide for detailed system requirements.

## [Software requirements](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#software-requirements)

### [Supported File Systems](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#supported-file-systems)

- Windows: FAT12/FAT16/FAT32, exFAT, NTFS
- Linux: Ext2/3/4, Btrfs, XFS*
- macOS: HFS Plus, HFSX, APFS
- Optical media: UDF

* XFS volumes are supported only when created using the legacy 32-bit timestamp format. XFS volumes created with the newer 64-bit ("Y2038-safe") timestamp format — the default on most current Linux distributions — are not detected.

**Not supported:** overlayfs, Minix, F2FS, CramFS, UFS, RomFS, VxFS, QNX4, and QNX6 file systems are not currently supported for scanning.

### [Operating System](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#operating-system)

- 64-bit architecture required
- **Windows:**

  - Windows 10, minimum version 2004 (build 19041) or higher
  - Windows 11, minimum version 21H2 (build 22000) or higher
- Windows Installer 4.5 or higher

### [Dependencies](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#dependencies)

- **OPSWAT MetaDefender Core:** Required for multi-scanning capabilities. Can be installed on the same or a separate system. Refer to the MetaDefender Core user guide for specific requirements.

**Note:** Maintaining the operating system with the latest updates is strongly recommended.

---

## [Security requirements](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#security-requirements)

The system administrators are required to make a Kiosk machine more secure by following these actions:

1. Set a BIOS password
2. Enable TPM and Secure Boot in the Windows system
3. Turn on BitLocker encryption (Note that Kiosk Hardened Image Update currently does not support BitLocker enabled device)

Kiosk is expected to be operated on a local, physical system. Operating a Kiosk in a remote desktop session is not supported. It is recommended to disable RDP access to the kiosk system if it is not required for your deployment environment.

---

## [Installed third party components](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#installed-third-party-components)

The following third party components are installed as part of the MetaDefender Kiosk installation process. These components may be shared with other applications.

All of these are required by MetaDefender Kiosk. Uninstalling them may result in unexpected behavior of other applications.

| Component | Details |
| --- | --- |
| Microsoft Visual C++ redistributable | - Microsoft Visual C++ 2015-2022 Redistributable - x64 |
| Microsoft .NET Runtime | - Microsoft .NET Runtime 8.0 or above |
| Paragon Software (optional) | - APFS for Windows by Paragon Software - HFS+ for Windows by Paragon Software - Linux File Systems for Windows by Paragon Software |

.NET Runtime version 9 is recommended

The support for .NET 8.0 is scheduled to end in November 2026, It is recommended to upgrade to .NET 9.0 when possible.

MetaDefender Core and Engine Requirements

MetaDefender Core and its related engines maintain their own system requirements. Please review the Core requirements page before deployment - [Recommended System Configuration - MetaDefender Core](https://www.opswat.com/docs/mdcore/installation/recommended-system-configuration)

---

## [Installed services](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#installed-services)

The following list are services that MetaDefender Kiosk depends on for operating.

| **Product Services** | Additional Information |
| --- | --- |
| MetadefenderSVC |  |
| ometascan, ometascan-node, ometascan-postgresql (Core v4.19+) | If Core is installed locally to Kiosk |
| **Third Party Services** |  |
| ParagonAPFSMounter | If *APFS for Windows by Paragon Software* is installed |
| apmwinsrv | If *HFS+ for Windows by Paragon Software* is installed |
| ParagonLinuxFSMounter | If *Linux File Systems for Windows by Paragon Software* is installed |
| **Windows Services** |  |
| Winmgmt | This service has dependencies on other Windows services |

---

## [Required available ports](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#required-available-ports)

The following ports need to be available for the machine MetaDefender Kiosk is installed on.

| Component/service | Port |
| --- | --- |
| MetaDefender Kiosk Web Console | 8009 |
| MongoDB | 27019 |

---

## [Application directories and registry key](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#application-directories-and-registry-key)

#### [Installation location](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#installation-location)

Installation directory can be configured. Default location is `C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client`.

#### [Application directory](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#application-directory)

The `%ProgramData%\OPSWAT` directory is used for storing MetaDefender Kiosk application data.

#### [Registry key](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#registry-key)

`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\OPSWAT` is the registry key for all OPSWAT products.

---

## [Real Time Protection \ Antivirus exclusion requirements](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#real-time-protection--antivirus-exclusion-requirements)

Real Time Protection (RTP) from any 3rd party software may adversely affect Kiosk operation as it will likely interfere with Kiosk's handling of media. It is recommended to either fully disable RTP or create exclusions to allow Kiosk to function and scan media without any interruptions.

### [Disabling Real Time Protection (RTP)](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#disabling-real-time-protection-rtp)

If setting up hardware not provided by OPSWAT, or your license key is not including Windows Defender as a part or MultiScan engine, ensure that Windows Defender Real Time Protection is disabled:

- Under `Virus & threat protection settings` disable `Tamper Protection`
- Under `Local Group Policy Editor`: *Computer Configuration* > *Administrative Templates* > *Windows Components* > *Microsoft Defender Antivirus* > *Real-time Protection* → *Turn off real-time protection* to `Enabled`
- Apply and reboot the system

### [Directories exclusion settings if RTP must be on](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#directories-exclusion-settings-if-rtp-must-be-on)

If your policy does not allow for RTP to be disabled, it is necessary to exclude these directories:

- Kiosk installation folder

  - `C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client`
- Kiosk application data folders

  - `C:\ProgramData\OPSWAT`
  - C:\Users<username>\AppData\Local\OPSWAT\Metadefender Kiosk
  - C:\Users<username>\AppData\Roaming\metadefender-kiosk
  - C:\Users<username>\AppData\Roaming\metadefender-kiosk-electron
- Paragon software folder

  - C:\Program Files (x86)\Paragon Software
- any known drive letters media will be mounted to when inserted

For Core, please refer to this [knowledge base article on RTP exclusions](https://docs.opswat.com/mdcore/knowledge-base/how-do-i-disable-real-time-protection-of-my-anti-malware-softwar).

Info

These steps may need to be redone after a Windows update since it may cause the Windows Defender settings to be reset.

---

## [Programs not removed during uninstall](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#programs-not-removed-during-uninstall)

The Microsoft redistributables are not removed when MetaDefender Kiosk is uninstalled.

---

## [Related Links](/docs/mdkiosk/v4.8.6/installation/kiosk-system-requirements#related-links)

- [Allowed Media Types](https://www.opswat.com/docs/mdkiosk/operating/allowed-media-types)
