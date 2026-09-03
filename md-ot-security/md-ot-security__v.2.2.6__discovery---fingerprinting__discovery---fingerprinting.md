<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/discovery---fingerprinting/discovery---fingerprinting -->

# Discovery - Fingerprinting

MetaDefender OT Security provides a device discovery capability that helps users find/discover all devices connecting to the network. The device discovery agent is responsible for collecting, probing, or scanning the network to discover managed/unmanaged devices.

The device discovery agent allows users to discover:

- OT devices (PLC, HMI)
- Enterprise endpoint (SCADA, server)
- Network devices (router, switch)
- IT devices (computer, laptop, mobile, printer, camera…)

There are 3 modes for MetaDefender OT Security discovery: basic active, smart active scanning and passive discovery. These settings can be configured at SETTINGS-> Network & Discovery Settings.

## [Active Scanning](/docs/md-ot-security/v.2.2.6/discovery---fingerprinting/discovery---fingerprinting#active-scanning)

The active scanning will basically discover what device is connecting to the network. The active scanning will provide some basic device information as below:

IP: IPv4 address of device.

MAC: MAC address of device.

Name: Name of device (Device type + Brand)

COC: Country of Origin of NICs.

Type/Sub-type: type of device.

Status: current status of device (active/inactive).

Onboarded time of the device.

## [Smart Active Scanning](/docs/md-ot-security/v.2.2.6/discovery---fingerprinting/discovery---fingerprinting#smart-active-scanning)

User can enable smart active scanning for specific device type in the Device Type setting.

Smart active scanning will provide more detailed information about the device:

- Hardware model
- Hardware version
- Hardware CPU
- OS - device operating system
- OS version

Note: The function “Allow scan for hardware info”: MetaDefender OT Security will use ICS protocols to communicate with devices to ask for device information.

- Open port and protocol.

Note: This is the list of opening ports the device is listening and services are being used to communicate to the device.

Note: This is the list of opening port that device is listening and services is being used to communicate to device.

## [Passive Discovery](/docs/md-ot-security/v.2.2.6/discovery---fingerprinting/discovery---fingerprinting#passive-discovery)

Users can enable passive discovery in the Network & Discovery Settings.

In this mode, MetaDefender OT Security will listen to traffic sent from the switch to collect network data. It will continuously collect and analyze all packets in the network. Therefore, it can have information on devices and communication (protocols) among them. Depending on communicated data on the network, MetaDefender OT Security can have detailed information about the device such as:

- Hardware model
- Hardware version
- Hardware CPU
- OS version

and other information such as protocols, open ports and services on the device.
