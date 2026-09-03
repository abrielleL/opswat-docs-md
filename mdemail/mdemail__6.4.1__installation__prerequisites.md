<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/installation/prerequisites -->

# Prerequisites

## Minimum hardware

Scalable Deployment

When Email Gateway Security is deployed in the scalable mode, then the minimum hardware requirements apply to each of the primary instance and all secondary instances.

For details about the shared database see [Scalable deployment](/installation/scalable-deployment), [Scalable deployment related registry configuration](/configuration/scalable-deployment-related-registry-configuration) and [Scalable deployment operation](/operating/scalable-deployment-operation).

| **CPU** | **RAM** | **SSD** | **NIC** |
| --- | --- | --- | --- |
| 4 Cores | 4 GB DDR4 | 16 GB | 1 GbE |

Space details

Please note that this hard disk space is only enough for installing MetaDefender Email Gateway Security and for very limited operation.

Quarantine and permanently failing emails (especially with large attachments) may consume huge disk volumes.

Storage performance concerns

For performance reasons it is not recommended to use HDD instead of SSD.

## Networking

### Ports

The following ports must be accessible for the product to work properly:

| **Direction** | **Service** | **Default Port** |
| --- | --- | --- |
| Inbound | SMTP service | 10025 |
| Inbound | Web Management Console and REST interface | 8058 |
| Outbound | MetaDefender Core (in case of being integrated to MetaDefender Core; for details see [Server profiles](/configuration/server-profiles)) | 8008 |
| Outbound | MetaDefender Managed File Transfer (optional; in case of being integrated to MetaDefender MFT; for details see [Server profiles](/configuration/server-profiles)) | 8010 |
| Outbound | SMTP destinations | 25 or 487 |
| Inbound / Outbound | Shared database for *Scalable Deployment* | 8060 |

Scalable Deployment

When Email Gateway Security is deployed in the scalable mode, then the shared database port must be available inbound on the primary instance, and outbound on all the secondary instances.

For details about the shared database see [Scalable deployment](/installation/scalable-deployment), [Scalable deployment related registry configuration](/configuration/scalable-deployment-related-registry-configuration) and [Scalable deployment operation](/operating/scalable-deployment-operation).

For details how to change port values see [Configuration/Registry configuration](/configuration/registry-configuration) and [Configuration/Settings](/configuration/settings).

### External services

The following services and URLs must be accessible to the product for it to work properly

| **Service** | **Client** | **Notes** |
| --- | --- | --- |
| <https://update.dl.opswat.com/> | Email Gateway Security | Upgrade service for processing engine (anti-malware, CDR, etc.) updates. |
| <https://metadefender.opswat.com> | Email end client (e.g. Outlook, Thunderbird, etc.) | For the proactive anti-phishing time-of-click analysis feature. |
| [https://metadefender.opswat.com](https://metadefender.opswat.com/) | Email Gateway Security | Multiscanning, Deep CDR and Proactive DLP services in case of being integrated to MetaDefender Cloud. For details see [Server profiles](/configuration/server-profiles). |
| [*.nimbus.bitdefender.net](https://nimbus.bitdefender.net) | Email Gateway Security | Only in case if anti-spam feature is licensed. |

#### Proxy settings

Anti-spam and anti-phishing

The anti-spam and anti-phishing filters use a cloud based service to look up patterns. To set up proxy for the anti-spam and anti-phishing cloud service use the antispam_proxy_ip and antispam_proxy_port Registry tunables. For details see [Registry configuration](/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securityinternalhttpsdocsopswatcommdemailconfigurationhkey_local_machinesoftwareopswatmetadefender-email-securityinternal).

## Software

### Operating system

| **Distribution** | **Version** | **Bitness** |
| --- | --- | --- |
| Microsoft Windows | 10 / 11 | 64 bit |
| Microsoft Windows Server | 2019 / 2022 | 64 bit |

### Supported browsers

One of the following desktop browsers is required to use the Web Management Console:

- Latest Google Chrome version
- Latest Mozilla Firefox version
- Latest Microsoft Edge version

### 3rd party frameworks or components

| **Name** | **Version** | **Notes** |
| --- | --- | --- |
| **Microsoft .NET Framework** | 4.5 or newer | Required |
| **Microsoft .NET 10** | 10.0.9 | Required |
| **PostgreSQL** | 14.11 or newer | Only applicable for deployments with *External database.* For details see [Installation](/installation/installation). |
| **pgcrypto** | Must come with the external database | Only applicable for deployments with *External database.* For details see [Installation](/installation/installation). |
| **pg_trgm** | Must come with the external database | Only applicable for deployments with *External database.* For details see [Installation](/installation/installation). |

### Local anti-virus

OPSWAT recommends to disable the real-time protection of anti-malware products on the servers that host Email Gateway Security.

If the corporate policy does not allow to disable the real-time anti-virus product, exception rules need to be added.

Exclude installation folder

To implement the exception rule, the OPSWAT installation folder (`C:\Program Files\OPSWAT` by default) must be excluded from the relevant anti-malware product’s real-time protection.

## Directories

This section contains references to directories used by Email Gateway Security.

In further sections of this user guide the *directory reference* is used instead of the actual directory to refer to locations on the system disk.

Everything, except logs, is placed under the installation folder.

| **Directory reference** | **Directory path** |
| --- | --- |
| Installation folder | C:\Program Files\OPSWAT\Metadefender Email Security |
| Event log files | C:\Windows\System32\WinEvt\Logs |

## Recommended MetaDefender Core and engine versions

| **Component** |  | **Recommended version** |
| --- | --- | --- |
| MetaDefender Core |  | Latest |
| FileType | engine | Latest |
| FileType | database | Latest |
| Archive | engine | Latest |
| Archive | database | Latest |
| Yara | engine | Latest |
| Yara | database | Latest |
| Deep CDR | engine | Latest |
| Deep CDR | database | Latest |
| Proactive DLP | engine | Latest |
| Proactive DLP | database | Latest |
| Threat Intelligence | database | Latest |
| Threat Intelligence | database | Latest |
| File-Based Vulnerability Assessment | engine | Latest |
| File-Based Vulnerability Assessment | database | Latest |
| Sandbox | engine | Latest |
| Sandbox | database | Latest |
