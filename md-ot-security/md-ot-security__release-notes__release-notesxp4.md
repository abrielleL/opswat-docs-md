<!-- source: https://www.opswat.com/docs/md-ot-security/release-notes/release-notesxp4 -->

# Version 3.6.0

| **Version** | 3.6.0 |
| --- | --- |
| **Release date** | 22 December 2025 |
| **Scope** | Enhance current features and add new features. |

## [New Features, Improvements, and Enhancements](/docs/md-ot-security/release-notes/release-notesxp4#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| **Physical (network topology) network map** | Visualize network topology for better network management, asset visibility, and administrative reporting |
| **Report Builder** | Support any of the reporting requirements through a powerful report design and generation tool with a combination of programmable, AI-enhanced data retrieval and flexible data presentation.  A set of ready-to-use report templates for different compliance standards is provided. |
| **Manage Login Session** | Implemented automatic session timeout that logs out users after a fixed period of time (even if active), enhancing security by preventing unauthorized access from long-lived sessions. |
| **Integration with ServiceNow** | Seamless integration with ServiceNow via Service Graph Connector and Vulnerability Response for improved CMDB workflow and vulnerability management. |
| **Batch delete for inactive devices** | Added support for bulk deletion of inactive devices, both manually and via scheduled automated cleanup rules, streamlining device management and improving database performance. |
| **Batch update devices** | Enabled bulk editing and updating of asset information, reducing manual effort and ensuring data consistency across large environments. |
| **Allow to set Policies by Subnet (CIDR)** | Enabled the ability to configure asset policies and connection policies using CIDR notation (e.g., 192.168.1.0/24), allowing administrators to apply policies to entire network segments instead of individual IP addresses, simplifying policy management for large-scale deployments. |
| **Display Ask AI feature to the sensor** | Added the AI-powered “Ask AI” feature on a sensor. |
| **Allow to customize alerts for BYOD and locally administered devices** | Allow users to define specific alert rules for BYOD (Bring Your Own Device) and locally administered assets to reduce false positives and focus on relevant security events. |
| **Support for opening a local web on the AIO installation** | Added support for accessing the MetaDefender OT Security web interface directly on AIO installations. This is especially useful for demo and PoC systems that need to open the web UI locally on the AIO device without additional network configuration. |
| **Adjust Device Type and Subtype** | We refined how device **Type** and **Subtype** are defined and displayed in the system. This update ensures device classification is more accurate and consistent across discovery, inventory, and policy-related views |
| **General Improvements** | Included various UI improvements, performance optimizations, and bug fixes to enhance performance, reliabilit,y and user experience. |
