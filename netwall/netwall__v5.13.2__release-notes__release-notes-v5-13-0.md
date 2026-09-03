<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/release-notes/release-notes-v5-13-0 -->

# Release Notes v5.13.0

| **Version** | Config: 5.13.0; USG-100: 1.0.0 (CC EAL4+ certified) |
| --- | --- |
|  | Config: 5.13.0; BSG-100: 1.0.0 (IEC-62443 certified) |
| **Release Date** | April 1, 2026 |
| **Scope** | MD Core Integration, MQTT SparkplugB Connector, OPC DA Enhancements |

Info

AVEVA PI 4.2.1 connector needs MetaDefender USG/BSG v5.13.0 to operate correctly. Please, update accordingly.

## [New Features, Improvements and Enhancements](/docs/netwall/v5.13.2/release-notes/release-notes-v5-13-0#new-features-improvements-and-enhancements)

| Feature | Details |
| --- | --- |
| Email Logging | System logs now provides send/receive/user status for SMTP messages. |
| MD Core Integration | USG/BSG now integrates with an external instance of MetaDefender Core |
| MQTT SparkplugB Connector | SparkPlugB compliant protocol connector improves SparkPlugB integration with native message support. |
| NTP Forwarding | Supports transfer of NTP from Blue to Red. |
| OPC DA HA | High Availability failover for redundant OPC DA servers. |
| OPC DA Shallow Browsing | Resilient tag browsing for OPC DA servers that do not provide tag type or return attributes when browsing. |
| Syslog Over SSL/TLS | Supports sending syslog messages over a SSL/TLS connection. |

## [Bug Fixes](/docs/netwall/v5.13.2/release-notes/release-notes-v5-13-0#bug-fixes)

|  | Details |
| --- | --- |
| OPC UA Connector | Condition whereby connector not receiving all tags. |
| SFTP Connector | Connector not working when configured to listen on non-standard ports. |
| SFTP Connector | Inconsistent SFTP queue behavior |
| Bug Fixes | Minor Bug Fixes |

## [Known Limitations](/docs/netwall/v5.13.2/release-notes/release-notes-v5-13-0#known-limitations)

N/A
