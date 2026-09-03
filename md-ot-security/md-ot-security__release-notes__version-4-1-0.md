<!-- source: https://www.opswat.com/docs/md-ot-security/release-notes/version-4-1-0 -->

# Version 4.1.0

| **Version** | v4.1.0 |
| --- | --- |
| **Release date** | 7/31/2026 |
| **Scope** | Enhance current features and add new features |

## [**New Features, Improvements and Enhancements**](/docs/md-ot-security/release-notes/version-4-1-0#new-features-improvements-and-enhancements)

| **Feature** | **Description** |
| --- | --- |
| **Alert Category Dashboard** | Introduced a centralized alert dashboard with category-based filtering and severity distribution, making it easier to review and prioritize alerts at a glance. |
| **Alert Categorization & Consolidation** | Alerts are now categorized by type and consolidated where possible, reducing noise and helping operators focus on actionable issues. |
| **Unacknowledged Alert Counts** | Asset Alerts, Connection Alerts, and Suricata Alerts now show counts of unacknowledged alerts only, giving a clearer view of open items. |
| **Improved Risk Score & Recommendations** | Enhanced risk scoring to factor in asset criticality and CVE severity, with updated recommendations to support better prioritization and reporting. |
| **Report Builder Charts** | Added chart-based visualizations to Report Builder, making executive and operational reports easier to digest. |
| **SSO Authentication** | Added Single Sign-On support (including Okta OIDC and SAML), enabling enterprise identity providers for web console login. |
| **My OPSWAT Asset Visibility Integration** | Integrated with My OPSWAT to enrich OT asset data and pull visibility information from across the OPSWAT stack. |
| **MD Endpoint Vulnerability Detection** | Improved CVE detection by integrating MetaDefender Endpoint for Windows as an additional vulnerability source, with periodic sync and on-demand refresh. |
| **Schneider PLC Passive Fingerprinting** | Added passive fingerprinting support for Schneider Electric PLCs (M221, M241, M251, M262, M238, M258) to improve device identification. |
| **Extended Protocol Support** | Added support for NetBIOS, SSDP, CIFS, HART IP, and mDNS to improve network discovery and protocol visibility. |
| **PCAP Capture for Live Traffic** | Added the ability to capture PCAP files from live traffic for forensic analysis and troubleshooting. |
| **PCAP Capture for Events** | Added the ability to capture PCAP context when an alert or event occurs, helping operators understand the environment at the time of detection. |
| **Data Archiving** | Introduced configurable data archiving by time or storage utilization, with manual or scheduled execution and downloadable archive files. |
| **Scanning Performance Prioritization** | Added user options to optimize and prioritize scanning resources for different network environments. |
| **Processing Performance Optimizations** | Improved backend performance for high-traffic deployments, including retention job optimization, persistent enterprise-to-site communication, batch job reliability, and worker health monitoring. |
| **Web Console Initial Setup via Default IP** | Enabled initial configuration through the web console using default component IPs (Enterprise 10.10.10.102, Site 10.10.10.101, Sensor 10.10.10.100), simplifying deployment and re-provisioning. |
| **One-Way Communication Only** | Removed bi-directional communication settings across Enterprise, Site, and Sensor; the setup wizard now supports one-way communication only. |
| **System Upgrade Improvements** | Redesigned upgrade workflows with separate Transfer and Install steps, pre-upgrade health checks, per-component readiness validation, local web upgrade support, and retry APIs for package download and installation. |
| **Offline Upgrade Streaming Upload** | Improved offline upgrade package upload with streaming to reduce client memory usage during large package transfers. |
| **Disk Encryption Option** | Added an optional disk encryption setting for security-conscious deployments. |
| **MD IFW + MD OTS Sensor Integration** | Delivered an integrated deployment of MetaDefender Industrial Firewall and MD OTS Network Sensor on a single appliance for constrained environments. |
| **Ask AI — Gemma 4 Upgrade** | Upgraded the Ask AI base language model to Gemma 4 for improved assistance quality. |
| **Security Enhancements** | Addressed findings from penetration testing and other security hardening work across components. |
| **General Improvements** | Includes various UI improvements, performance optimizations, and bug fixes to enhance reliability and user experience. |
