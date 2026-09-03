<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/release-notes/release-notes9ht -->

# Version 3.4.5

| **Version** | 3.4.5 |
| --- | --- |
| **Release date** | 26 July 2025 |
| **Scope** | Enhance current features and add new features. |

## [New Features, Improvements and Enhancements](/docs/md-ot-security/v4.0.0/release-notes/release-notes9ht#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| **Single Installation File for All Deployment Options** | Consolidated all deployment options (Enterprise Manager, Site Manager, Network Sensor, etc.) into a single installation file, simplifying installation and reducing operational overhead. |
| **Improved Initial Connectivity Setup** | Enhanced connection handling between Enterprise, Site Manager, and Sensor components during initial setup to streamline configuration, improve user experience and reliability. |
| **SSH Access Management (Sensor & Site Manager)** | Expanded SSH access management support to include both Network Sensor and Site Manager. Also removed the time-limited access setting, giving administrators full control over remote access configuration. |
| **Initial Setup: Enable SSH Step** | Added a dedicated step in the initial setup wizard to allow users to enable SSH access during system onboarding, improving usability and security readiness. |
| **Display Info at Asset’s Rescan Button** | Enhanced the UI to display useful information (e.g. scan status, scan port, scan OS…), giving user more visibility into the scanning of individual asset. |
| **Configure Multicast/Broadcast as distinguished values (separated from “External host” value) in Connection Policies** | Added support for defining multicast and broadcast IP/MAC addresses as distinguished values (separated from “External host” value), enhancing unauthorized connection policies. |
| **PCAP Capture in Test Network** | Enabled packet capture (PCAP) during network tests, allowing users to collect and analyze raw traffic data for troubleshooting and visibility purposes. |
| **New Industrial Protocols Supported** | Extended protocol detection capabilities with support for: **MELSEC, CC-Link IE No. IP, CC-Link TSN PTP, CC-Link TSN SLMP.** These additions improve asset discovery and monitoring for industrial environments using these specialized protocols. |
| **General Improvements** | Included various performance optimizations and bug fixes to enhance reliability and user experience. |
