<!-- source: https://www.opswat.com/docs/mdicap/getting-started/general-system-requirements -->

# General System Requirements

## [Operating System Requirements](/docs/mdicap/getting-started/general-system-requirements#operating-system-requirements)

- Red Hat Enterprise Linux8.x, 9.x
- Rocky Linux 9
- Debian 11.x, 12.x
- Ubuntu 22.04, 24.04
- Windows 11
- Microsoft Windows Server 2019, 2022, 2025 or newer (64 bit)

Plan for legacy OS support

OPSWAT will discontinue support for the following OS versions in MetaDefender ICAP Server:

- Debian 11 since **July** **2026**.
- Ubuntu 22.04 since **Apr 2027**.
## [Hardware Requirements](/docs/mdicap/getting-started/general-system-requirements#hardware-requirements)

| Hardware | MetaDefender ICAP Server Dedicated | MetaDefender ICAP + MetaDefender Core |
| --- | --- | --- |
| CPU | Min 4 CPU |  |
| RAM | Min. 2 GB |  |
| Disk Space | 2 GB + (Max size per scan request * [number of scan request in parallels ]) |  |

Disk Performance

For performance reasons it is NOT recommended to use a HDD in place of an SSD.

Shared server

If MetaDefender Core or any other system is installed on the same physical machine as MetaDefender ICAP Server then the additional systems' hardware requirements need also be taken into consideration.

## [Other software requirements](/docs/mdicap/getting-started/general-system-requirements#other-software-requirements)

### [**MetaDefender Core Version Compatibility Matrix**](/docs/mdicap/getting-started/general-system-requirements#metadefender-core-version-compatibility-matrix)

| MetaDefender ICAP Server | MetaDefender Core |
| --- | --- |
| 4.0.0 | 4.7.0+ |
| 4.1.0 | 4.8.0+ |
| 4.2.0+ | 4.8.2+ |

The following scan engines must be active:

| Scan engine | Version |
| --- | --- |
| Data sanitization | 5.0.2-6+ |
| At least one of the available anti-malware engines | N/A |

**[Linux] Third Party Dependencies**

|  |  |
| --- | --- |
| FileType engine | Rocky Linux 8.x 9.x/Red Hat 8.x 9.x: libnsl |

**Security rules**

Under **Policy > Security rules** on Core, security rules – that are used by MetaDefender ICAP Server's security rules: ** **

Enable Visibility of scan result (recommended):

| Role | Visibility |
| --- | --- |
| Everybody | FULL DETAILS |

Info

Without this visibility ICAP Server can still work, but certain details may not be visible within the UI.

**Browser Requirements**

One of the following desktop browsers is suggested to view the MetaDefender ICAP Server's UI:

- Chrome
- Firefox
- Safari
- Microsoft Edge

Info

Chrome, Firefox, Safari and Edge browsers are tested with the latest available version at the time of release. Microsoft IE is no longer supported (replaced by Microsoft Edge).

Mobile layouts are not supported.

**Additional installation of Windows services**

| Name | Service Name | Optional |
| --- | --- | --- |
| MetaDefender ICAP Server | mdicapsrv | REQUIRED |

**Ports that must be available**
