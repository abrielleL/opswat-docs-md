<!-- source: https://www.opswat.com/docs/mdtransferguard/release-notes/metadefender-diode-x-v1-10-0-2-5-0 -->

# MetaDefender Diode X v1.10.0/2.5.0

| **Version** | **Config:** 1.10.0; OD-101: 1.0.1 (Common Criterial EAL4+, No High Availability Support).**Config:** 2.5.0; OD-102: 1.0.2 (No EAL4+, High Availability Supported) |
| --- | --- |
| **Release Date** | June 30, 2026 |
| **Scope** | File Transfer Filtering |

Info

Please, note that the process to update from 1.8.X to 2.4.0 is different than the normal process explained in the Updates section. Contact customer support to update to version 2.4.0.

## [New Features, Improvements and Enhancements](/docs/mdtransferguard/release-notes/metadefender-diode-x-v1-10-0-2-5-0#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| CPU Temp in Syslog | CPU temperature is now published via syslog. |
| Disable HTTP Port | Provides for disabling HTTP port for organizations that require disabling as per company security policy. |
| File Transfer Filtering | Allow/Block files based on File Name, Size and Type. |

## [Bug Fixes](/docs/mdtransferguard/release-notes/metadefender-diode-x-v1-10-0-2-5-0#bug-fixes)

|  | Details |
| --- | --- |
| HTTP Connector | Multiple HTTP Streams configured on a single port caused errors when editing the second stream. |
| Support Package | Addressed issue whereby support packages where not able to be generated using Diode X versions 2.4.0 & 2.4.1 |

## [Note](/docs/mdtransferguard/release-notes/metadefender-diode-x-v1-10-0-2-5-0#note)

Diode X has been upgraded to support MD Core version 5.17.1. Upgrading to MD Core v5.17.1 requires a system software rebuild. Customers wishing to upgrade should contact customer support for software access and technical support. <https://www.opswat.com/support/contact-support>
