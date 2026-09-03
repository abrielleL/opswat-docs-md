<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/release-notes/version3-2-1 -->

# Version 3.2.1

| **Version** | **v3.2.1** |
| --- | --- |
| **Release date** | 15 Sep 2024 |
| **Scope** | Enhance current features and add new features |

## [New Features, Improvements and Enhancements](/docs/md-ot-security/v4.0.0/release-notes/version3-2-1#new-features-improvements-and-enhancements)

|  | **Details** |
| --- | --- |
| **Detect the configuration and security status of Siemens PLC devices** | This feature enables users to scan Siemens Programmable Logic Controllers (PLCs) to detect their configuration settings and assess the security status. By conducting a comprehensive scan, it retrieves detailed information about the device’s current setup |
| **Policy: Add a new policy for firmware changes** | This feature introduces a new blocklist policy that monitors devices for firmware changes. Whenever a firmware update or modification is detected, the system automatically triggers an alert, ensuring users are promptly informed of any changes that could impact device functionality or security. This policy helps maintain control over asset integrity and reduces the risk of unauthorized or unintended firmware alterations. |
| **Upgrade vulnerabilities detection** | Upgrade the ability to detect vulnerabilities in devices. |
| **Smart asset profiling: Add PROFINET IO (DCE/RPC)** | We now support scanning PLCs using additional protocol **PROFINET IO (DCE/RPC)** to retrieve hardware and firmware information. |
| **Show detailed command statistics for protocols: S7comm, S7commplus, Profinet IO, Profinet DCP** | We now support to display detailed command statistics for protocols: S7comm, S7commplus, Profinet IO, Profinet DCP |
