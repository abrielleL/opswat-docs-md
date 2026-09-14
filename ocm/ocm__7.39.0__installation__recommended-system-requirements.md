<!-- source: https://www.opswat.com/docs/ocm/7.39.0/installation/recommended-system-requirements -->

# Recommended System Requirements

- [Operating System](/docs/ocm/7.39.0/installation/recommended-system-requirements#operating-system)
- [Minimum Hardware Requirement](/docs/ocm/7.39.0/installation/recommended-system-requirements#minimum-hardware-requirement)
- [Software Requirement](/docs/ocm/7.39.0/installation/recommended-system-requirements#software-requirement)
- [Hardware sizing](/docs/ocm/7.39.0/installation/recommended-system-requirements#hardware-sizing)
- [Directory](/docs/ocm/7.39.0/installation/recommended-system-requirements#directory)
- [Ports used](/docs/ocm/7.39.0/installation/recommended-system-requirements#ports-used)
- [Browser Requirement](/docs/ocm/7.39.0/installation/recommended-system-requirements#browser-requirement)

Your server must meet the following requirements before installing OPSWAT Central Management.

## [Operating System](/docs/ocm/7.39.0/installation/recommended-system-requirements#operating-system)

Warning

Only support 64-bit platforms.

| OS family | Supported versions |
| --- | --- |
| Microsoft Windows | 10, 11 |
| Microsoft Windows Server | 2016, 2019 and 2022   - 2016 require Windows Update to be up-to-date. |
| Red Hat Enterprise Linux | 7.7 |
| Ubuntu | 18.04  20.04, 22.04 (via [workaround](/docs/ocm/7.39.0/knowledgebase/how-to-install-opswat-central-management-on-ubuntu-20-04-and-22-)) |
| Debian | 11, 12 (via [workaround](/docs/ocm/7.39.0/knowledgebase/how-to-install-opswat-central-management-on-ubuntu-20-04-and-22-#debian-1112)) |

## [Minimum Hardware Requirement](/docs/ocm/7.39.0/installation/recommended-system-requirements#minimum-hardware-requirement)

| RAM | 16 GB |
| --- | --- |
| CPU | 1 CPU (4 cores) |
| Hard disk | 20 GB + ~500MB * [number of managed scan engines] |
| Available ports | 9000, 9026, 9005, 9009, 27017 |

## [Software Requirement](/docs/ocm/7.39.0/installation/recommended-system-requirements#software-requirement)

| Software | Version |
| --- | --- |
| PowerShell (Windows only) | Version 5.1, build 14409, revision 1018 or higher.  On Windows Server 2012, 2012 R2 and 2012, it's recommended to have Windows Update (which deliver PowerShell updates) be up-to-date.  RemoteSigned execution policy. |
| Visual C++ Redistributable Packages (Windows only) | Latest version  As of April 2025, the latest version of this software (14.42.34438.0) is available at <https://aka.ms/vs/17/release/vc_redist.x64.exe> |

## [Hardware sizing](/docs/ocm/7.39.0/installation/recommended-system-requirements#hardware-sizing)

The following table shows the configuration of the server that installs OPSWAT Central Management.

| Number of devices | Up to 5,000 | 5,000 to 20,000 | 20,000 to 40,000 |
| --- | --- | --- | --- |
| CPU | 1 CPU ( 4 cores) | 1 CPU ( 8 cores) | 1 CPU (16 cores) |
| RAM | 16 GB | 16 GB | 32 GB |
| Hard disk capacity | 60 GB + ~500MB * [number of managed scan engines] | 100 GB + ~500MB * [number of managed scan engines] | 200 GB + ~500MB * [number of managed scan engines] |

## [Directory](/docs/ocm/7.39.0/installation/recommended-system-requirements#directory)

This section contains references to directories used by OPSWAT Central Management.

**Windows:**

| Directory/folder | Default |
| --- | --- |
| Installation | C:\Program Files\OPSWAT\Central |
| Event log files | C:\Program Files\OPSWAT\ Central \tomcat\logs |
| Data backup | C:\ProgramData\OPSWAT\Central |

**Linux (Red Hat Enterprise Linux and Ubuntu):**

| Directory/folder | Default |
| --- | --- |
| Main installation folder | /opt/ocm |
| Service folder | /usr/lib/ocm |
| Event log folder | /var/log/ocm |
| Configuration/backup folder | /etc/opt/ocm |
| Database folder | /var/lib/ocm |

## [Ports used](/docs/ocm/7.39.0/installation/recommended-system-requirements#ports-used)

The table below shows the default port configuration of OPSWAT Central Management. The listed ports must be available to start OPSWAT Central Management. The ports listed under **External** should be opened for external access.

| Component / Service |  | Port | Notes |
| --- | --- | --- | --- |
| External |  |  |  |
| Central Management (Nginx) | Web Management Console | 9000 | Customizable |
| Internal |  |  |  |
| Nginx | Load balancer (internal communication) | 9026 | Customizable |
| MongoDB | Database of OPSWAT Central Management | 27017 |  |
| Redis | Caching data | 9005 |  |
| Tomcat | Webserver | 9009 |  |

To customize the ports marked as customizable, please refer to [Port Configuration](/docs/ocm/7.39.0/configuration/port-configuration).

The table below shows the default port configuration (if available) for OPSWAT Products that OPSWAT Central Management can manage.

| OPSWAT Product | Port |
| --- | --- |
| MetaDefender Core | 8008 |
| MetaDefender Kiosk | 8009 |
| MetaDefender Managed File Transfer | 8010 |
| MetaDefender ICAP | 8048 |
| MetaDefender Email Security | 8058 |
| MetaDefender Secure Storage | 80 |

## [Browser Requirement](/docs/ocm/7.39.0/installation/recommended-system-requirements#browser-requirement)

One of the following desktop browsers is required to use the web management console:

- Latest two Chrome versions
- Latest two Firefox versions
- Latest two Microsoft Edge versions

OPSWAT Central Management supports HTTPS configuration on all the aforementioned browsers. Please refer to [Secure Connection](/docs/ocm/7.39.0/configuration/enabling-https) for more details.

Mobile layouts are not supported yet.
