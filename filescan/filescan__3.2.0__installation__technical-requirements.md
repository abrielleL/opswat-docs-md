<!-- source: https://www.opswat.com/docs/filescan/3.2.0/installation/technical-requirements -->

# Technical Requirements

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Minimum Requirements (on premise)](/docs/filescan/3.2.0/installation/technical-requirements#minimum-requirements-on-premise)

- **Ubuntu Server 22.04** LTS ("Jammy Jellyfish") or **Ubuntu Server 24.04** LTS ("Noble") or **Red Hat Enterprise Linux 9.x** or **Rocky Linux 9.x**:

  - Support for CIS-hardened **Ubuntu Server 24.04** ("Noble") machines is not yet available
  - Support for **Ubuntu Server 20.04** LTS ("Focal Fossa") was dropped with the 2.0.0 Release
  - Please download the Ubuntu ISO image from: <https://releases.ubuntu.com/noble/>

Plan for legacy OS support

OPSWAT will discontinue support for the following OS in MetaDefender Aether/Sandbox:

- **Ubuntu 22.04** from **Apr 2027**.

- 8 vCPUs (Preferably 16 vCPUs): a **CPU with AVX support is required** as the Sandbox includes MongoDB: <https://www.mongodb.com/docs/manual/administration/production-notes/#x86_64>
- 32 GB RAM (essential for scanning files *larger than 1 GB*)
- 256 GB **Free Disk Space** (SSD)_: Sandbox requires 32 GB on the first installation (subsequent upgrades will potentially consume more disk space). More information for *_multi-partition layouts**: [Low disk space](/docs/filescan/3.2.0/troubleshooting/low-disk-space)

  - Please note that the **Ubuntu server installer** will configure the main disk as an LVM group by default (2 partitions mirroring each other). For example, on a 100 GB disk you will get approx. 50 GB usable storage. This provides redundancy and better data safety, so please consider doubling your disk size. Alternatively, you can uncheck the *"Set up this disk as an LVM group"* option during the Ubuntu installation, see: <https://ubuntu.com/server/docs/install/storage>
  - *Disk space recommendation is assuming default retention settings and an average file size is assumed to be in the single digit MB range. If very large files are sent at large quantities, total disc size has to be much larger or retention settings more strict.
- Internet access is required during the installation & upgrade process, except for [Offline Installation](/docs/filescan/3.2.0/installation/offline-installation).
- The "minimized" version of Ubuntu Server is NOT suitable for **offline installations**, since it lacks some essential packages. Please select "Ubuntu Server" here:

*Note: More than 25000 scans/day requires a custom multi-server setup and needs to be scoped out with the engineering team.*

Due to the low resource requirements and cloud-native capability, the Sandbox does not require nested VMs and can be deployed and operate with its proprietary virtualization technology directly on the host system.

## [Feature availability by OS version](/docs/filescan/3.2.0/installation/technical-requirements#feature-availability-by-os-version)

| Feature/os | Ubuntu 22.04 | Ubuntu 24.04 | Red Hat 9.5 (or newer) | Rocky Linux 9.5 (or newer) |
| --- | --- | --- | --- | --- |
| Online Install | **✓** | **✓** | **✓** | **✓** |
| Online Install via Proxy | **✓** | **✓** | **✓** | **✓** |
| Offline Install | **✓** | **✓** | **✓** | **✓** |
| Install on CIS level 2 hardened system | **✓** | **X** | **✓** | **✓** |

## [Throughput / Minimum Requirements](/docs/filescan/3.2.0/installation/technical-requirements#throughput--minimum-requirements)

The following table lists explanatory system specs with a retention period of 10 days:

| Scans Per Day | Required System CPUs | Required System RAM | Required Storage per Retention Period |
| --- | --- | --- | --- |
| 1000 | 4 | 32 GB | 100 GB |
| 2500 | 4 | 32 GB | 100 GB |
| 5000 | 4 | 32 GB | 256 GB |
| 10000 | 8 | 32 GB | 512 GB |
| 25000* | 16 | 32 GB | 512 GB |

*Currently the maximum numbers of scans/day per instance

## [Minimum Cloud Requirements (AWS)](/docs/filescan/3.2.0/installation/technical-requirements#minimum-cloud-requirements-aws)

- 5000 scans/day: `r6a.xlarge`
- 10000 scans/day: `m6a.2xlarge`
- 25000 scans/day: `c6a.4xlarge`

## [Network Setup](/docs/filescan/3.2.0/installation/technical-requirements#network-setup)

It is recommended to run the product in a segregated network segment, or to operate the sandbox in a DMZ entirely.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
