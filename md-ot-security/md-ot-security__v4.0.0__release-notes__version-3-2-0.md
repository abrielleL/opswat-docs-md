<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/release-notes/version-3-2-0 -->

# Version 3.2.0

| **Version** | **v3.2.0** |
| --- | --- |
| **Release date** | 05 Sep 2024 |
| **Scope** | Enhance current features and add new features |

## [New Features, Improvements and Enhancements](/docs/md-ot-security/v4.0.0/release-notes/version-3-2-0#new-features-improvements-and-enhancements)

|  | **Details** |
| --- | --- |
| **Integration with HPE Aruba Networking ClearPass Policy Manager** | The integration allows the sync of asset information to HPE Aruba Networking ClearPass Policy Manager. MetaDefender OT Security supports three types of sync:   1. **Periodic Sync:** MetaDefender OT Security can sync data with ClearPass Policy Manager at specified intervals. 2. **Automatic Sync:** Custom-trigger sync based on conditions:     1. Detection of changes in asset properties of certain types.    2. Detection of changes in asset exposure scores within or outside defined ranges. 3. **Manual Sync:** Sync at any time the user wants. |
| **Enable configuring NTP server** | This feature allows users to configure a Network Time Protocol (NTP) server within the system. By enabling this configuration, users can synchronize the system's time between components (Enterprise Manager, Site Manager and Sensor) |
| **Allow adding custom fields** | This feature allows users to add more custom fields to an asset. |
| **Smart asset profiling: Add GE-SRTP** | In addition to the existing smart asset profiling features (BACnet/IP profile, B&R profile, EtherNet/IP profile, Modbus-TCP profile, S7COMM profile, ABB Profile, Mitsubishi profile), we now support scanning PLCs using additional protocol **GE-SRTP** to retrieve hardware and firmware information. |
| **Support more protocols (GE-SRTP)** | The SRTP protocol from Emerson (General Electric) |
| **Syslog: Support RFC3164, RFC 5424, CEF format** | This feature provides comprehensive support for various Syslog message formats, including RFC3164, RFC5424, and Common Event Format (CEF). By supporting these widely-used formats, the system ensures seamless integration with various logging and monitoring tools, enhancing the ability to collect, analyze, and manage log data from different sources. |
