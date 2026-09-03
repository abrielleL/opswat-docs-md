<!-- source: https://www.opswat.com/docs/mdndr/installation-guide/technical-requirements -->

# Technical Requirements

## [**Minimum requirements [on-premise]**](/docs/mdndr/installation-guide/technical-requirements#minimum-requirements-on-premise)

**1Gb virtual sensor specifications**

- **Ubuntu Server 22.04** LTS ("Jammy Jellyfish"), **Ubuntu Server 24.04** LTS ("Noble"), **Red Hat Enterprise Linux 9.x**, or **Rocky Linux 9.x**:

  - CIS-hardened **Ubuntu Server 24.04** ("Noble") machines do not yet have support.
  - OPSWAT dropped support for **Ubuntu Server 20.04** LTS ("Focal Fossa") with the 2.0.0 Release.
  - Download the Ubuntu ISO image from <https://releases.ubuntu.com/jammy/>.
- 32 vCPUs
- 128GB RAM (essential for analysis at 1Gbps networks)
- Two NICs (One management interface; One capture interface)
- 3.2 TB **Free Disc Space** (SSD)*:

  - By default, the **Ubuntu server installer** configures the main disk as an LVM group. It uses 2 mirrored partitions. For example, a 100 GB disk gives approximately 50 GB usable storage. This gives redundancy and better data safety. Thus, consider a disk with twice the required size. As an alternative, clear the *"Set up this disk as an LVM group"* option during the Ubuntu installation. See <https://ubuntu.com/server/docs/install/storage>.
  - *The disc space recommendation assumes default retention settings and an average file size in the single digit MB range. If the sensor sends many very large files, use a much larger disk. As an alternative, use stricter retention settings.
- Internet access is necessary during the installation & upgrade process.

## [Example hardware setup](/docs/mdndr/installation-guide/technical-requirements#example-hardware-setup)

- **CPU:** Intel Xeon 6 Performance 6730P 2.5G, 32C/64T, 24GT/s, 330M Cache, Turbo, (250W) DDR5-6400, OEM XL
- **RAM**: 128 GB (4 × 32 GB DDR5-6400 ECC RDIMM)
- **Storage**: 3.2TB Useable RAID10 4x 1.6TB Data Center NVMe Mixed Use AG Drive U2 with carrier
- **Power Supply**: Dual, Fully Redundant(1+1), Hot-Plug MHS Power Supply,800W MM (100-240Vac]

*Note: this example system lets the sensor process traffic at 1Gbps with default retention periods.*
