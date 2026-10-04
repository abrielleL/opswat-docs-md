<!-- source: https://www.opswat.com/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-15-0 -->

# MetaDefender Optical Diode v1.15.0

| **Version** | **Config:** 1.15.0; OD-101: 1.0.1 (Common Criteria EAL4+ certified, High Availability Not Supported) **Config:** 1.15.0; OD-102:1.0.2 , (Not EAL4+ Certified, High Availability Supported) |
| --- | --- |
| **Release Date** | September 30, 2026 |
| **Scope** | This release delivers improvements across connectivity, file transfer and observability, along with multiple reliability updates. |

| Feature | Details |
| --- | --- |
| AVEVA Pi Connector | Added ability to download PI statistics as CSV**.** |
| AVEVA Pi Connector | Now supports period character [ . ] for Tag Prepend/Append naming. |
| OPC DA Auto Tag Discovery | Blue OPC DA Connector automatically discovers new tags and transfers the tags to the Red Connector without manual intervention. |
| OPC UA Certificate Expiration | Added ability to configure OPC UA certificate expiration (up to 10 years). |
| OPC UA Node Filtering | Enables OPC UA root nodes to be filtered by a List or Regular Expression. |
| UDP Source Port for Back to Back Mode | Selectable UDP Source Port for Back to Back Mode. |
| SFTP Server Connector | Built-in SFTP Server on both BLUE and RED sides. |
| TCP Port Selection for Back to Back Mode | Added port 80/443 support for TCP streams in Back-to-Back diode mode. |
| Telemetry Connector | Sends anonymized, aggregated usage and performance data to OPSWAT to help improve product performance and reliability. Telemetry is enabled by default but can be disabled. |
| VIP for Outbound Connections | For High Availability configurations the source IP address for TCP/UDP connections is now the VIP. It maybe be necessary to update firewall entries to allow the VIP. |

## Bug Fixes

|  | Details |
| --- | --- |
| FTP Server Connector | Fixed FTP Server connection failure occurring after installation. |
| Licensing | Deployment IDs for license on new installs are now based on the Trusted Platform Module (TPM) and changing the hostname or IP/gateway no longer impacts the Deployment ID. |
| SMTP Connector | Fixed initial SMTP delivery errors during first-time setup. |

## Known Limitations

**Config:** 1.15.0; OD-101: 1.0.1 is Common Criterial EAL4+ certified. No High Availability support.

**Config:** 1.15.0; OD-102:1.0.2 is not Common Criterial EAL4+ certified. Supports High Availability.

MetaDefender
