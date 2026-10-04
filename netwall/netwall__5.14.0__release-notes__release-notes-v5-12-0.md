<!-- source: https://www.opswat.com/docs/netwall/5.14.0/release-notes/release-notes-v5-12-0 -->

# Release Notes v5.12.0

| **Version** | Config: 5.12.0; USG-100: 1.0.0 (CC EAL4+ certified) |
| --- | --- |
|  | Config: 5.12.0; BSG-100: 1.0.0 (IEC-62443 certified) |
| **Release date** | January 16, 2026 |
| **Scope** | Digital Signature, OPC UA Multi-server, UDP Multicast |

Info

AVEVA PI 4.2.1 connector needs MetaDefender Optical Diode v1.12.0 to operate correctly. Please, update accordingly.

## [New Features, Improvements and Enhancements](/docs/netwall/5.14.0/release-notes/release-notes-v5-12-0#new-features-improvements-and-enhancements)

| Feature | Details |
| --- | --- |
| Configuration via Config File | Provides the ability to do "basic" system configuration via a configuration file. Saves time when commissioning multiple devices. |
| Digital Signature and Signature Verification | For File Transfers, system can now be configured to sign outgoing files and/or verify a signature for incoming files |
| Modbus Connector | Response timeout value parameter is now configurable |
| OPC UA Multi-server Support | Now supports connecting to multiple (up to 5) OPC UA servers. Enables up to to 5 instances of the OPC UA Connector to run concurrently. Supports a 1:1 relationship between a source and destination OPC server/client. |
| OPC UA Connector | OPC Foundation / OPC UA Libraries .NETStandard updated to v1.5.375.457 |
| OPC UA Connector | .NET updated to version 8.0 |
| UDP Multicast | Now support UDP Multicast |

## [Bug Fixes](/docs/netwall/5.14.0/release-notes/release-notes-v5-12-0#bug-fixes)

|  | Details |
| --- | --- |
| Bug Fixes | Minor Bug Fixes |

## [Known Limitations](/docs/netwall/5.14.0/release-notes/release-notes-v5-12-0#known-limitations)

N/A
