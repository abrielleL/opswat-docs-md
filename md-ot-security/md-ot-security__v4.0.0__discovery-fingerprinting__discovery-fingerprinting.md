<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting -->

# Discovery - Fingerprinting

MetaDefender OT Security provides a device discovery capability that helps users find all devices connecting to the network. The discovery agent collects, probes, and analyzes traffic to discover both managed and unmanaged devices.

Discoverable device categories:

- OT devices (PLC, HMI)
- Enterprise endpoints (SCADA, server)
- Network devices (router, switch)
- IT devices (computer, laptop, mobile, printer, camera)

There are two discovery modes: **Active Scanning** and **Passive Discovery**. Both are configured per network interface in **Network Sensor Configuration → Network Settings → Scan Setup**.

## [Active Scanning](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#active-scanning)

Active scanning probes the network using nmap to discover connected devices and collect device information. It is enabled and configured per interface in the sensor's Network Settings wizard.

### [Configuration — Scan Setup (per interface)](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#configuration--scan-setup-per-interface)

For each network interface card (NIC) the **Scan Setup** panel exposes the following active scanning controls:

| Setting | Description |
| --- | --- |
| **Using for Active Discovery** | Master toggle. Enables nmap-based active probing on this interface. |
| **Active Scanning Scope** | IPv4 CIDR subnet to probe (e.g. 192.168.1.0/24). If blank, defaults to the interface's detected subnet. |
| **Auto run Smart Profiling** | Automatically runs Smart Asset Profiling once when a device is first discovered. Uses ICS protocols (S7comm, Modbus, CIP, BACnet, etc.) to query hardware details from the device. |
| **Auto run Mass Discovery** | Continuously scans all IPs in the configured scope, performing host discovery, OS fingerprinting, and open-port scanning on each cycle. |

### [Scan Intervals and Rules](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#scan-intervals-and-rules)

| Scan Type | Default Interval | Notes |
| --- | --- | --- |
| Port scan | 5 minutes | Only runs for device types with *Allow scan port* enabled in Port Scan Rules |
| OS detection | 20 minutes | OT devices (Purdue model OT level: PLC, HMI) are excluded to avoid disrupting industrial protocols |
| Smart Profiling | Once (on first discovery) | Uses ICS protocols; only runs if *Auto run Smart Profiling* is enabled |
| Mass Discovery | 60 seconds | Scans all IPs in the configured scope |

### [Port Scan Rules Policy](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#port-scan-rules-policy)

Port and OS scanning respect the **Asset Type** policy. For each device type/sub-type you can configure:

- Whether a **scan for Hardware info** is allowed — the sensor queries ICS protocols once to collect hardware details.
- Whether an **OS scan** is allowed — interval is 20 minutes from end of previous cycle.
- Whether **Ports scan** is allowed — interval is 5 minutes from end of previous cycle.

Device types not covered by a rule are included by default, allowing the sensor to classify unknown devices on first contact.

### [Smart Asset Profiling](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#smart-asset-profiling)

When *Auto run Smart Profiling* is enabled, the sensor automatically runs a profiling pass the first time each device is onboarded. It uses OT/ICS protocol queries to request identity information directly from the device.

Additional fields collected by Smart Profiling:

- Hardware model
- Hardware version
- Hardware CPU
- Article / Part No.
- OS and OS version
- Firmware version

**Note:** Smart Asset Profiling sends ICS protocol packets directly to the target device. Ensure the device type policy allows it before enabling in environments with sensitive OT equipment.

## [How Auto Run Mass Discovery Uses the Scanning Scope](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#how-auto-run-mass-discovery-uses-the-scanning-scope)

When **Auto Run Mass Discovery** is enabled, the sensor continuously scans devices it has already found — it does not blindly ping every IP address in the range looking for brand-new hosts. Think of it as: the sensor keeps a list of known devices, and the Scanning Scope tells it which ones to actively probe each cycle.

### [Which IP range gets scanned](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#which-ip-range-gets-scanned)

The sensor uses one of two ranges per interface:

- **Active Scanning Scope** — what you typed in the field (e.g., `192.168.1.0/24`). This takes priority if set.
- **Default** — the interface's own subnet, auto-detected when the NIC was first configured. This kicks in when the scope field is left blank, so the sensor works out of the box without extra setup.

### [What you can enter in the Scanning Scope field](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#what-you-can-enter-in-the-scanning-scope-field)

| Format | Example |
| --- | --- |
| Subnet (CIDR) | 192.168.1.0/24 192.168.1.0/24 |
| No filter | Leave blank — all known devices are candidates regardless of IP |

You can add multiple entries. Overlapping ranges (e.g., a /24 and a /28 that sit inside it) are not allowed — the sensor will flag this as a configuration error when you save.

### [Which devices actually get scanned](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#which-devices-actually-get-scanned)

Even if a device's IP falls inside the configured range, it will be skipped if:

- **The interface is disabled.** No scans run on a turned-off interface.
- **It's an OT device** (PLC, HMI, or similar industrial equipment). These are always excluded — sending OS-detection probes to live industrial equipment can disrupt operations.
- **It has already been scanned this cycle.** Each device is scanned once per cycle, then marked as done until the next cycle begins.
- **Its device type policy blocks scanning.** The Asset Type policy controls, per device type, whether OS and port scanning is allowed. Unknown device types are included by default so the sensor can classify them.
- **It has no IP address recorded yet.** Devices seen only at Layer 2 (MAC only, no IP) are skipped.

## [Passive Discovery](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#passive-discovery)

Passive discovery listens to network traffic without sending any probes. Enable it per interface via the **Using for Passive Monitoring/Discovery** toggle in Scan Setup.

In passive mode, MetaDefender OT Security uses Zeek to continuously capture and analyze all packets on the monitored interface. No traffic is injected into the network.

### [Collected Information](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#collected-information)

- IP and MAC addresses
- Manufacturing vendor (from MAC OUI database)
- Active protocols and services
- Open ports the device is listening on
- **Layer 2 protocols**: ARP, LLDP, GOOSE, EtherCAT, Profinet DCP, CDP, SV, and more
- **Layer 3 protocols**: Modbus, S7comm, MMS, DNP3, DNS, HTTP, and more

**Note:** Open ports listed under Passive Discovery are ports the device is *actively communicating on* — not a port scan result. They reflect observed traffic, not a complete port inventory.

### [Passive Scanning Settings](/docs/md-ot-security/v4.0.0/discovery-fingerprinting/discovery-fingerprinting#passive-scanning-settings)

Click **Passive Scanning Settings** on any enabled interface to configure:

- **Included / Excluded network ranges** — restrict which subnets are analyzed
- **Layer 2 visibility** — toggle Layer 2 protocol analysis (ARP, LLDP, etc.)
- **Standard BPF filters** — pre-built packet filters (exclude broadcast, multicast, etc.)
- **Advanced BPF filters** — custom BPF expression for fine-grained capture control
- **Zeek open-connection write interval** — how frequently partially open connections are flushed to storage
