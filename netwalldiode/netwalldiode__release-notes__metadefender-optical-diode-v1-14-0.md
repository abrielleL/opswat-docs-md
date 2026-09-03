<!-- source: https://www.opswat.com/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-14-0 -->

# MetaDefender Optical Diode v1.14.0

| **Version** | **Config:** 1.14.0; OD-101: 1.0.1 (Common Criteria EAL4+ certified, High Availability Not Supported) **Config:** 1.14.0; OD-102:1.0.2 , (Not EAL4+ Certified, High Availability Supported) |
| --- | --- |
| **Release Date** | June 30, 2026 |
| **Scope** | File Transfer Filtering, OPC DA & OPC UA Enhancements |

Info

AVEVA PI 4.2.2 connector needs MetaDefender Optical Diode v1.14.0 to operate correctly. Please, update accordingly.

| Feature | Details |
| --- | --- |
| CPU Temp in Syslog | CPU temperature is now published via syslog. |
| Disable HTTP Port | Provides for disabling HTTP port for organizations that require disabling as per company security policy. |
| File Transfer Filtering | Allow/Block files based on File Name, Size and Type. |
| OPC DA Auto Tag Discovery | Blue OPC DA Connector automatically discovers new tags and transfers the tags to the Red Connector without manual intervention. |
| OPC DA Red Pi Interface Failover | Triggers failover of the Primary Pi OPC interface when data stops flowing so data can be received from the secondary OPC DA Red Connector. |
| OPC UA Automatic Tag Discovery | Blue OPC UA Connector automatically discovers new tags and transfers the tags to the Red Connector without manual intervention. |
| OPC UA Part 20 | Now supports OPC UA Part 20 (File Transfer) |

## [Bug Fixes](/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-14-0#bug-fixes)

|  | Details |
| --- | --- |
| AVEVA Pi Connector (v4.2.2) | Statistics frozen on initial installation. |
| HTTP Connector | Multiple HTTP Streams configured on a single port caused errors when editing the second stream. |
| OPC UA Connector | Invalid Node Error when fetching Namespace on setup. |

## [Known Limitations](/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-14-0#known-limitations)

**Config:** 1.14.0; OD-101: 1.0.1 is Common Criterial EAL4+ certified. No High Availability support.

**Config:** 1.14.0; OD-102:1.0.2 is not Common Criterial EAL4+ certified. Supports High Availability.

MetaDefender
