<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/release-notes/version3-3-0 -->

# Release Notes

| **Version** | 3.3.0 |
| --- | --- |
| **Release date** | 17 Dec 2024 |
| **Scope** | Enhance current features and add new features |

## [New Features, Improvements and Enhancements](/docs/md-ot-security/v.3.4.0/release-notes/version3-3-0#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| **Auto Software Update** | Easy ways to update MD OT Security to new versions |
| **Signature-based network threat detection (Suricata integration)** | Integration with Suricata to enhance network threat detection through signature-based analysis, allowing for more effective and proactive identification of network threats. |
| **Multi Languages** | Added support for German language (DE) |
| **Enhance discovered information of an asset** | 1. **Host Name**: Displays the hostname of the device. 2. **System Description**: Provides a brief description of the device's system. 3. **Product Lifecycle Status**: Indicates the product lifecycle status as provided by the vendor. |
| **Integration with MD Industrial Firewall for protection of PLCs** | Manage MetaDefender Industrial Firewall to protect PLCs |
| **PCAP analysis: log details** | Enhanced PCAP analysis with detailed logging, providing users with granular insights into network packet data for improved diagnostics and incident response |
| **Offline updates (Update database CVE)** | Added support for offline updates to the CVE database, allow continuous vulnerability updates even in environments without internet access. |
| **Backup** | Introduced a backup feature to safeguard configuration data and provide resilience against data loss, supporting uninterrupted operations. |
| **Auto probing for asset details (Smart Asset Profiling)** | Supported auto probing of asset details using Smart Asset Profiling. |
| **Enhanced Passive Scanning: LLDP, ARP** |  |
| **REST API for Asset’s data** | Developed REST API endpoints for asset management, enabling automated integration with other systems and customizable asset workflows. |
| **Set names for rules from defined policies** |  |
| **Smart asset profiling: Add SNMP** | Supported scanning devices using additional protocol **SNMP** to retrieve hardware and firmware information. |
| **Compliance CIP report** | Added a Compliance CIP reporting feature to streamline regulatory compliance tracking and provide auditors with clear, standardized reporting. |
| **Bundle sensor and site server are on one computer** | Supported site and sensor can be installed and run on one machine. |
| **View assets of all sensors at the Site manager and Enterprise manager** | Cached assets data at Enterprise Manager for improvement of performance and availability essential asset info to users |
| **Network Diagnosis** | Supported:   1. **Ping Test**: Verify network connectivity and measure latency. 2. **Trace Route**: Identify the path and pinpoint issues in data transmission. 3. **Telnet**: Test port connectivity and troubleshoot remote services. |
