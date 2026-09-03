<!-- source: https://www.opswat.com/docs/mdmediafirewall/setup/overview -->

# Overview

OPSWAT’s MetaDefender Media Firewall works in conjunction with MetaDefender Kiosk acting as a simple, plug-and-play firewall appliance to secure host systems from the threats of removable media-borne cyberattacks. The Media Firewall ensures file contents of inserted portable media are inspected, audited, and approved prior to use.

## [Key Features](/docs/mdmediafirewall/setup/overview#key-features)

- Plug and Play appliance that requires no software installation on SCADA/HMI host system
- Automatically blocks unprocessed or compromised files
- Locally managed using a Host system without Ethernet or remotely managed over Ethernet with [My OPSWAT](https://my.opswat.com)
- Works with MetaDefender Kiosk to validate a manifest of audited files via a public key site certificate that can be programmed onto the appliance prior to operation
- Compliance: NERC CIP, ISA 62443, NIST 800-53, NIST 800-82, and ISO 27001

---

## [Technical Specifications](/docs/mdmediafirewall/setup/overview#technical-specifications)

### [Front Panel](/docs/mdmediafirewall/setup/overview#front-panel)

Ports from Left to Right of the unit:

- Power LED indicator
- USB 3.0 Type-A
- USB 3.0 Type-C
- SD card slot
- Micro SD card slot
- Compact Flash card slot

### [Back Panel](/docs/mdmediafirewall/setup/overview#back-panel)

- `RESET` - for factory resetting the unit or warm reboot
- Power button
- `PWR` - 12V DC or 24 VDC jack
- `USB-A` - USB 3.0 Type-A (for management using a Wi-Fi Dongle)
- `COMP` - USB 3.0 Type-C (connect to the Host system)
- `MGMT` - RJ45 1GbE LAN (for management over a wired network)

  - Some models may come with two additional ethernet ports (`ENET-1` & `ENET-2`). These are reserved for future use. Network connection can only be utilized on the port labeled `MGMT`.
- Kensington Security Slot - for securing the unit to a location with a Kensington lock

### [Host System Requirements](/docs/mdmediafirewall/setup/overview#host-system-requirements)

- OS: Windows, Linux, Mac
- USB Type-A (1.0 or greater)
- Support exFAT file system

### [Supported File Systems](/docs/mdmediafirewall/setup/overview#supported-file-systems)

- FAT
- exFAT
- NTFS
- ext2/3/4

### [Additional Details](/docs/mdmediafirewall/setup/overview#additional-details)

| Category | Value |
| --- | --- |
| Maximum file size | 104GB |
| Operating temperature | -5 to 40 Celsius / 23 to 104 Fahrenheit |
| Accessories included | - 12VDC 36W power supply - AC power cord (USA) - 6' USB cable Type-C to Type-A for host system connection - 6' RJ45 Cat 6 ethernet cable for remote management |
