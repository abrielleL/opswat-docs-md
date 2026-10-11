<!-- source: https://www.opswat.com/docs/cm/deployment/system-requirements -->

# System Requirements

To deploy My OPSWAT Central Management On-Premises, ensure your system meets the minimum requirements for your deployment mode.

> **Info**
>
> Only 64-bit platforms are supported.

Jump to: [MSI Installation  - Windows](https://www.opswat.com/docs/cm/deployment/system-requirements#msi-installation--windows) | [RPM Installation - Linux [RHEL]](https://www.opswat.com/docs/cm/deployment/system-requirements#rpm-installation--linux-rhel) | [Virtual Appliance[OVA]](https://www.opswat.com/docs/cm/deployment/system-requirements#virtual-appliance-ova)

## Common Requirements

These requirements apply to all deployment modes.

### Hardware

| Component | Minimum |
| ---- | ---- |
| CPU | 8 vCPUs, AVX2 support |
| Memory | 32 GB RAM |
| Storage | 500 GB SSD (see [Storage Usage Information](https://www.opswat.com/docs/cm/deployment/system-requirements#storage-usage-information) for sizing guidance) |

### Networking and Port Requirements

| Port | Protocol | Direction | Destination / Source | Purpose |
| ---- | ---- | ---- | ---- | ---- |
| 9000 | TCP | Inbound | Product instances | Communications from products to My OPSWAT Central Management |
| 443 | TCP | Outbound | [https://update.dl.opswat.com](https://update.dl.opswat.com), [https://opswat-gears-cloud.s3-us-west-2.amazonaws.com/](https://opswat-gears-cloud.s3-us-west-2.amazonaws.com/) | Product/module updates (if enabled) |
| 443 | TCP | Outbound | [https://activation.dl.opswat.com](https://activation.dl.opswat.com) | License activation (if online) |
| 443 | TCP | Outbound | Configured proxy servers | Outbound traffic via proxy (if configured) |
| `<SMTP port>` | TCP | Outbound | Configured SMTP server | Send emails (if configured) |
| `<IdP port>` | TCP | Outbound | Configured IdP servers | SSO user directory authentication (if configured) |
| 443 | TCP | Outbound | [https://metascanbucket.s3.amazonaws.com/](https://metascanbucket.s3.amazonaws.com/), [https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/), [https://s3.amazonaws.com/mem-onpremise/production/patch/](https://s3.amazonaws.com/mem-onpremise/production/patch/), [https://s3.amazonaws.com/mem-onpremise/production/vulnerability/](https://s3.amazonaws.com/mem-onpremise/production/vulnerability/) | MetaDefender Endpoint updates (if enabled) |

> **Note**
>
> - Internal ports ranging from 30000 to 30071. Conflicts within this port range can lead to improper system behavior.
> - If you route traffic through proxy servers, there's no need to set up outbound rules for other outbound connections, except the proxy connections.
> - To ensure proper communication between product instances and the My OPSWAT Central Management, the **FQDN and ports** must be allowed through your **firewall** or **proxy**.

## MSI Installation — Windows

### Operating System

| OS Family | Supported Versions |
| ---- | ---- |
| Microsoft Windows | 11 |
| Microsoft Windows Server | 2016, 2019, 2022, 2025 |

> **Info**
>
> Note: Windows Server 2016 must have all patches installed.

### Prerequisites

| Prerequisite | Required Version | Download |
| ---- | ---- | ---- |
| Visual C++ Redistributable | 14.36.32532.0+ (64-bit) | [Download](https://aka.ms/vs/17/release/vc_redist.x64.exe) |
| .NET Framework | 4.8+ (64-bit) | [Download](https://download.microsoft.com/download/f/3/a/f3a6af84-da23-40a5-8d1c-49cc10c8e76f/NDP48-x86-x64-AllOS-ENU.exe) |
| .NET Desktop Runtime | 8.0.0+ (64-bit) | [Download](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/runtime-desktop-8.0.23-windows-x64-installer) |

### Directory Paths

| Directory | Default Path |
| ---- | ---- |
| Installation, Data backup | C:\Program Files\OPSWAT\MOCM |
| Troubleshooting log files | C:\ProgramData\OPSWAT\MOCM\Logs |

## RPM Installation — Linux (RHEL)

> **Info Version Applicability**
>
> The requirements below apply to My OPSWAT Central Management **10.7.26080 and later**, where the supporting components (nginx, RabbitMQ, Valkey) are bundled with the RPM package. Their configuration and data are stored under the My OPSWAT Central Management directories, as listed in [Directory Paths](https://www.opswat.com/docs/cm/deployment/system-requirements#directory-paths-2).
>
> For **10.7.26070 and earlier**:
>
> - nginx, rabbitmq-server, redis and erlang must be installed separately before the RPM installer.
> - These components use their own system directories (`/etc/nginx`, `/usr/share/nginx`, `/etc/rabbitmq`, `/var/lib/rabbitmq`, `/etc/redis`, `/var/lib/redis`).
>
> Please refer to the documentation for version [**10.7.26070**](https://www.opswat.com/docs/cm/10.7.26070/deployment/system-requirements#rpm-installation--linux-rhel) using the version selector at the top of this page.

### Operating System

Red Hat Enterprise Linux **9.4 or later** (64-bit only).

### Required Packages

The following packages are set as the RPM package's "Requires" dependencies.

Note that when installing the main package via dnf or yum, these dependecies will be automatically installed by default if a valid upstream repository is available.

| Package | Required Minimum Version | Installation Guide |
| ---- | ---- | ---- |
| openssl | No minimum | Available via `dnf install openssl` |
| glibc | 2.34 | Available via `dnf install glibc` |
| libgcc | 11.2.1 | Available via `dnf install libgcc` |
| libstdc++ | 11.2.1 | Available via `dnf install libstdc++` |
| systemd-libs | 250 | Available via `dnf install systemd-libs` |
| zlib | 1.2.11 | Available via `dnf install zlib` |
| libcap | 2.48 | Available via `dnf install libcap` |
| libgcrypt | 1.10.0 | Available via `dnf install libgcrypt` |
| libgpg-error | 1.42 | Available via `dnf install libgpg-error` |
| libzstd | 1.5.1 | Available via `dnf install libzstd` |
| lz4-libs | 1.9.3 | Available via `dnf install lz4-libs` |
| ncurses-libs | 6.2 | Available via `dnf install ncurses-libs` |
| openssl-libs | 3.0.1 | Available via `dnf install openssl-libs` |
| xz-libs | 5.2.5 | Available via `dnf install xz-libs` |
| libxcrypt | 4.4.18 | Available via `dnf install libxcrypt` |
| pcre2 | 10.37 | Available via `dnf install pcre2` |

> **Info**
>
> Note: RPM installation requires only the packages above. No hypervisor or VMware requirement — it runs on any infrastructure (VMware, cloud VMs, bare metal, etc.).

### Directory Paths

| Directory | Default Path |
| ---- | ---- |
| Main installation folder | /opt/mocm |
| Service folder | /usr/lib/systemd/system |
| Event log folder | /var/log/mocm |
| Database folder | /var/lib/mocm |
| Config files (nginx, MongoDB, RabbitMQ) | /etc/opt/mocm |
| Nginx config | /etc/opt/mocm/nginx |
| Nginx data | /var/lib/mocm/nginx |
| RabbitMQ config | /etc/opt/mocm/rabbitmq |
| RabbitMQ data | /var/lib/mocm/rabbitmq |
| Valkey config | /etc/opt/mocm/valkey |
| Valkey data | /var/lib/mocm/valkey |

## Virtual Appliance (OVA)

> **Info**
>
> Note: VMware requirements below apply only to Virtual Appliance (OVA) deployment. They are NOT required for MSI or RPM installations.

### Hypervisor Requirements

- VMware vSphere 7.0 U3 or 8.0
- VMware Workstation Player 17

### Directory Paths

> **Info Version Applicability**
>
> The folder structure below applies to My OPSWAT Central Management **10.7.26080 and later**, where the configuration and data of the supporting components (nginx, RabbitMQ, Valkey) are stored under the My OPSWAT Central Management directories.
>
> For **10.7.26070 and earlier**, these components use their own system directories (`/etc/nginx`, `/usr/share/nginx`, `/etc/rabbitmq`, `/var/lib/rabbitmq`, `/etc/redis`, `/var/lib/redis`). Please refer to the documentation for version **10.7.26070** using the version selector at the top of this page.

| Directory | Default Path |
| ---- | ---- |
| Main installation folder | /var/opt/mocm |
| Service folder | /etc/systemd/system |
| Event log folder | /var/log/mocm |
| Database folder | /var/lib/mocm |
| Config files (nginx, MongoDB, RabbitMQ) | /etc/opt/mocm |
| Nginx config | /etc/opt/mocm/nginx |
| Nginx data | /var/lib/mocm/nginx |
| RabbitMQ config | /etc/opt/mocm/rabbitmq |
| RabbitMQ data | /var/lib/mocm/rabbitmq |
| Valkey config | /etc/opt/mocm/valkey |
| Valkey data | /var/lib/mocm/valkey |

## Sizing Guidance

My OPSWAT Central Management is sized by the **volume of reports (objects)** its enrolled instances send — mainly the total files scanned per hour across all MetaDefender Cores — plus your **data retention period**, not by the number of products. Use the minimum requirements as a baseline and scale to your expected load:

| CPU | RAM | Sustained load (objects/hr, all Cores) | Disk growth |
| ---- | ---- | ---- | ---- |
| 8 | 32 GB | ~1 million/hr (~24 million/day) | ~235 GB/month |
| 12 | 48 GB | ~3 million/hr (~72 million/day) | ~700 GB/month |
| 16 | 64 GB | ~5 million/hr (~120 million/day) | ~1,220 GB/month |

Memory saturates first as load grows; provision disk to your retention period. The disk-growth figures above were measured with *Do not store raw report data for allowed files *enabled, which significantly reduces disk usage. For product-specific disk estimates, see [Storage Usage Information](https://www.opswat.com/docs/cm/deployment/system-requirements#storage-usage-information).

> These figures are sizing guidelines based on OPSWAT performance and load testing (5 MetaDefender Core + 5 MetaDefender Kiosk, 30-day retention). Actual resource usage varies with your report volume, retention period, and environment, so use them as a starting point and validate against your own workload. For the full methodology and detailed results, see [Performance and Sizing for My OPSWAT Central Management](https://www.opswat.com/docs/cm/deployment/Performance-and-Sizing-for-My-OPSWAT-Central-Management).

## Storage Usage Information

**MetaDefender Endpoint**

On average, each MetaDefender Endpoint (MDE) sends approximately 150 MB of data to Central Management per month.

To calculate the required disk space based on your data retention policy:

**Required Disk Size** = 150 MB × *[Number of Endpoints]* × *[Data Retention Period in Months]*

For example, to manage 1,000 MetaDefender Endpoints with 1-month data retention period:

*Extra Disk Space Needed* *= 1,000 Endpoints × 0.15 GB × 1 Month =* *150 GB*

Total disk space requirement:

- 100 GB for the operating system
- 150 GB for endpoint data

Disk space needed to manage 1000 endpoints: **250 GB**

**MetaDefender Core**

The required extra disk space depends on two key factors:

1. Number of scanning engines
2. Number of managed MetaDefender Core instances & Scanning volume

**Number of scanning engines:** On average, each scanning engine requires approximately 5 GB of storage in Central Management. For example, with 20 engines, you should allocate an additional 100 GB of disk space.

**Number of managed MetaDefender Core instances & Scanning volume:** Additional disk space is required to store scanning reports generated by MetaDefender Core. As a baseline, allocate at least 100 GB for storing these reports, *with further increases based on the number of managed instances and overall scanning activity*.

- Note: On average, each file scan generates a report of approximately 10 KB. Therefore, for every 1 million scanned files, you should allocate an additional 10 GB of disk space.

For example, to manage MetaDefender Cores with 20 engines:

*Extra Disk Space Needed =* 100 GB for engine database + 100 GB for report storage = 200 GB

Total disk space requirement:

- 100 GB for the operating system
- 200 GB for engine & report data

Disk space needed to manage Cores with 20 engines & 1 million scanned files: **300 GB**

## Browser Versions Supported

Supported browsers for launching the My OPSWAT Central Management console are Chrome, Firefox, and Microsoft Edge on desktop (mobile view has not been supported yet, but in our roadmap). We recommend that you should use the most current version of the browser.

## Screen Resolution

We recommend that you use a screen resolution of 1300x768 or larger to properly display My OPSWAT Central Management console interface.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
