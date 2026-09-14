<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/discovery-fingerprinting/discovery-fingerprinting -->

# Discovery - Fingerprinting

MetaDefender OT Security provides a device discovery capability that helps users find/discover all devices connecting to the network. The device discovery agent is responsible for collecting, probing, or scanning the network to discover managed/unmanaged devices.

The device discovery agent allows users to discover:

- OT devices (PLC, HMI)
- Enterprise endpoint (SCADA, server)
- Network devices (router, switch)
- IT devices (computer, laptop, mobile, printer, camera…)

There are 2 modes for MetaDefender OT Security discovery: **Active Scanning** and **Passive Discovery**.

## [Active Scanning](/docs/md-ot-security/v.3.4.8/discovery-fingerprinting/discovery-fingerprinting#active-scanning)

The active scanning will basically discover what device is connecting to the network, and provide some basic device information as below:

IP: IPv4 address of device.

MAC: MAC address of device.

Name: Name of device (Device type + Brand)

COO: Country of Origin of NICs.

Type/Sub-type: type of device.

Status: current status of device (active/inactive).

Onboarded time of the device.

Besides that, users can enable smart active scanning and Allow scan port/OS for specific device types in the Port Scan Rules policy.

- Choose if a **scan for Hardware info** is allowed. The application only scans the hardware information of the device only 1 time
- Choose if a **scan for OS** is allowed. The interval to scan is 20 minutes. It depends on the cycle of the run, the exact time is “cycle time + interval time”
- Choose if a **scan for open ports** is allowed. The interval to scan is 5 minutes. It depends on the cycle of the run, the exact time is “cycle time + interval time”

The first time the device is onboard, the system auto-runs **Smart Asset Profiling** to scan if the option **“Use for smart active discovery“** is checked. This option can be found in **Assets → Smart Asset Profiling** → open Specific profile to see

Smart Active Scanning will provide more detailed information about the device:

- Hardware model
- Hardware version
- Hardware CPU
- Article/Part. No.
- OS - device operating system
- OS version
- OS/Firmware

Note: The function “Allow scan for hardware info”: MetaDefender OT Security will use ICS protocols to communicate with devices to ask for device information.

## [Passive Discovery](/docs/md-ot-security/v.3.4.8/discovery-fingerprinting/discovery-fingerprinting#passive-discovery)

- Open port and protocol.

Note: This is the list of opening ports the device is listening to and services are being used to communicate to the device.

Users can enable passive discovery in the Network & Discovery Settings.

In this mode, MetaDefender OT Security will listen to traffic sent from the switch to collect network data. It will continuously collect and analyze all packets in the network. Therefore, it can have information on devices and communication (protocols) among them. Depending on communicated data on the network, MetaDefender OT Security can have detailed information about the device such as IP, MAC, manufacturing vendor of the device, protocols communicated among them, and other information such as protocols, open ports, and services on the device.
