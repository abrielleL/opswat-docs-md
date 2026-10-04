<!-- source: https://www.opswat.com/docs/netwall/release-notes/release-notes-v5-15-0 -->

# Release Notes v5.15.0

| **Version** | Config: 5.15.0; USG-100: 1.0.0 (CC EAL4+ certified) |
| --- | --- |
|  | Config: 5.15.0; BSG-100: 1.0.0 (IEC-62443 certified) |
| **Release Date** | September 30, 2026 |
| **Scope** | This release delivers improvements across connectivity, file transfer, observability, and provisioning, along with multiple reliability and security updates. |

## [New Features, Improvements and Enhancements](/docs/netwall/release-notes/release-notes-v5-15-0#new-features-improvements-and-enhancements)

| Feature | Details |
| --- | --- |
| AVEVA Pi Connector | Added ability to download PI statistics as CSV**.** |
| AVEVA Pi Connector | Now supports period character [ . ] for Tag Prepend/Append naming. |
| OPC DA Auto Tag Discovery | Blue OPC DA Connector automatically discovers new tags and transfers the tags to the Red Connector without manual intervention. |
| OPC UA Certificate Expiration | Added ability to configure OPC UA certificate expiration (up to 10 years). |
| OPC UA Node Filtering | Enables OPC UA root nodes to be filtered by a List or Regular Expression. |
| Selectable UDP Source Port for Back to Back Mode | Selectable UDP Source Port for Back to Back Mode and TCP Port Selection for Back to Back Mode |
| SFTP Server Connector | Built-in SFTP Server on both BLUE and RED sides. |
| TCP Port Selection for Back to Back Mode | Added port 80/443 support for TCP streams in Back-to-Back diode mode. |
| Telemetry Connector | Sends anonymized, aggregated usage and performance data to OPSWAT to help improve product performance and reliability. Telemetry is enabled by default but can be disabled. |
| VIP for Outbound Connections | For High Availability configurations the source IP address for TCP/UDP connections is now the VIP. It maybe be necessary to update firewall entries to allow the VIP. |

## [Bug Fixes](/docs/netwall/release-notes/release-notes-v5-15-0#bug-fixes)

|  | Details |
| --- | --- |
| FTP Server Connector | Fixed FTP Server connection failure occurring after installation. |
| Licensing | Deployment IDs for license on new installs are now based on TPM and changing the hostname or IP/gateway no longer impacts the Deployment ID. |
| SMTP Connector | Fixed initial SMTP delivery errors during first-time setup. |

## [Known Limitations](/docs/netwall/release-notes/release-notes-v5-15-0#known-limitations)

N/A
