<!-- source: https://www.opswat.com/docs/netwall/release-notes/release-notes-v5-14-0 -->

# Release Notes v5.14.0

| **Version** | Config: 5.14.0; USG-100: 1.0.0 (CC EAL4+ certified) |
| --- | --- |
|  | Config: 5.14.0; BSG-100: 1.0.0 (IEC-62443 certified) |
| **Release Date** | June 30, 2026 |
| **Scope** | File Transfer Filtering, OPC DA & OPC UA Enhancements |

Info

AVEVA PI 4.2.2 connector needs MetaDefender USG/BSG v5.14.0 to operate correctly. Please, update accordingly.

## [New Features, Improvements and Enhancements](/docs/netwall/release-notes/release-notes-v5-14-0#new-features-improvements-and-enhancements)

| Feature | Details |
| --- | --- |
| CPU Temp in Syslog | CPU temperature is now published via syslog. |
| Disable HTTP Port | Provides for disabling HTTP port for organizations that require disabling as per company security policy. |
| OPC DA Auto Tag Discovery | Blue OPC DA Connector automatically discovers new tags and transfers the tags to the Red Connector without manual intervention. |
| OPC DA Red Pi Interface Failover | Triggers failover of the Primary Pi OPC interface when data stops flowing so data can be received from the secondary OPC DA Red Connector. |
| OPC DA Shallow Browsing | Resilient tag browsing for OPC DA servers that do not provide tag type or return attributes when browsing. |
| OPC UA Automatic Tag Discovery | Blue OPC UA Connector automatically discovers new tags and transfers the tags to the Red Connector without manual intervention. |
| OPC UA Part 20 | Now supports OPC UA Part 20 (File Transfer) |

## [Bug Fixes](/docs/netwall/release-notes/release-notes-v5-14-0#bug-fixes)

|  | Details |
| --- | --- |
| AVEVA Pi Connector | Statistics frozen on initial installation. |
| HTTP Connector | Multiple HTTP Streams configured on a single port caused errors when editing the second stream. |
| OPC UA Connector | Invalid Node Error when fetching Namespace on setup. |

## [Known Limitations](/docs/netwall/release-notes/release-notes-v5-14-0#known-limitations)

N/A
