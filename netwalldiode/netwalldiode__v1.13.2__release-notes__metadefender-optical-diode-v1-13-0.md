<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/release-notes/metadefender-optical-diode-v1-13-0 -->

# MetaDefender Optical Diode v1.13.0

| **Version** | **Config:** 1.13.0; OD-101: 1.0.1 (Common Criteria EAL4+ certified, High Availability Not Supported) **Config:** 1.13.0; OD-102:1.0.2 , (Not EAL4+ Certified, High Availability Supported) |
| --- | --- |
| **Release Date** | April 1, 2026 |
| **Scope** | MQTT SparkPlugB Connector, NTP Forwarding, OPC DA Enhancements |

Info

AVEVA PI 4.2.1 connector needs MetaDefender Optical Diode v1.13.0 to operate correctly. Please, update accordingly.

## [Cryptographic posture improvements on TLS configuration](/docs/netwalldiode/v1.13.2/release-notes/metadefender-optical-diode-v1-13-0#cryptographic-posture-improvements-on-tls-configuration)

| Feature | Details |
| --- | --- |
| Email Logging | System log now provides send/receive/user status for SMTP messages. |
| MQTT SparkplugB Connector | SparkPlugB compliant protocol connector improves SparkPlugB integration with native messaging support. |
| MQTT Bandwidth Throttle | Bitrate throttle optimizes MQTT data flow across the Optical Diode. |
| NTP Forwarding | Supports transfer of NTP from Blue to Red. |
| OPC DA HA | High Availability failover for redundant OPC DA servers. |
| OPC DA Shallow Browsing | Resilient tag browsing for OPC Da servers that do not provide tag type or return attributes when browsing. |
| Syslog over SSL/TLS | Transfer of syslog messages over a SSL/TLS connection. |

## [Bug Fixes](/docs/netwalldiode/v1.13.2/release-notes/metadefender-optical-diode-v1-13-0#bug-fixes)

|  | Details |
| --- | --- |
| OPC UA Connector | Condition whereby connector not receiving all tags. |
| SFTP Connector | Connector not working when configured to listen on non-standard ports. |
| SFTP Connector | Inconsistent SFTP queue behavior. |
| Bug Fixes | Minor bug fixes |

## [Known Limitations](/docs/netwalldiode/v1.13.2/release-notes/metadefender-optical-diode-v1-13-0#known-limitations)

**Config:** 1.13.0; OD-101: 1.0.1 is Common Criterial EAL4+ certified. No High Availability support.

**Config:** 1.13.0; OD-102:1.0.2 is not Common Criterial EAL4+ certified. Supports High Availability.

MetaDefender
