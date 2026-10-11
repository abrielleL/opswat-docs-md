<!-- source: https://www.opswat.com/docs/md-ot-security/release-notes/release-notes48v -->

# Version 3.4.4

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| **Version** | 3.4.4 |
| --- | --- |
| **Release date** | 01 July 2025 |
| **Scope** | Enhance current features and add new features. |

## [New Features, Improvements and Enhancements](/docs/md-ot-security/release-notes/release-notes48v#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| **Batch delete assets** | Allow removal of related information (connections, alerts, etc.) |
| **Handle of connectivity between Components when their IP changes.** | Network Sensors can now manually reconnect to the Site Manager, and Site Manager can reconnect to Enterprise Manager when their IP changes, ensuring stable communication in dynamic network environments. |
| **Check and report network interfaces of Sensor (Passive, Active NICs).** | Added the ability to test the network connectivity of passive and active NICs on Sensors, helping users validate and troubleshoot interface configurations more easily. |
| **Provide APIs: Get Vulnerabilities of Assets and Patching** | Introduced a new API to retrieve the list of vulnerabilities associated with specific assets, enabling integration with external systems for risk monitoring and compliance.  Provided a Patching API to support integration with external patch management workflows or platforms, streamlining the remediation process for identified vulnerabilities. |
| **Enhance passive asset discovery of devices behind a router** | The system now automatically detects and displays devices located behind routers during passive discovery. This enhancement improves asset visibility in networks, especially in complex industrial environments. |
| **Enhance passive asset discovery of industrial devices based on Siemens proprietary protocols** | Added protocol-based detection for industrial devices using S7comm and Siemens devices using S7commPlus, providing deeper insight into OT assets |
| **General Improvements** | Includes various performance optimizations and bug fixes to enhance reliability and user experience. |
