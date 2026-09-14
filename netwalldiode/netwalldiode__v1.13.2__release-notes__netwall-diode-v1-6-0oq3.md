<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/release-notes/netwall-diode-v1-6-0oq3 -->

# MetaDefender Optical Diode v1.6.0

| **Version** | Config: 1.6.0 OD-101: 1.0.1 |
| --- | --- |
| **Release date** | Apr 2024 |
| **Scope** | Release to include HA support |

## [New Features, Improvements and Enhancements](/docs/netwalldiode/v1.13.2/release-notes/netwall-diode-v1-6-0oq3#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| High Availability Support | High Availability mechanism included. |
| PI DB enhancements | Added support for synching of security attributes |
| PI2PI | PI2PI support added |
| CLI command to change date | New command included in the CLI to change the date |
| User account password min length changed | User account minimum length changed to 12 chars |
| Update REDIS | REDIS updated to v7.2.4 |
| Support package enhancement | Support package enhaced to add the output of lspci / dmesg commands |
| PCAP support | New feature included under Diagnostic that allow the user to do a packet capture |
| PI2IP and PI DB Replication; append tag names | Added capability to append tag names |
| Redundant Fiber MIB | MIB for redundant fiber included |
| GUI changes | Minor GUI changes |
| Syslog | Syslog Liveview through a proxy supported |

## [Bug fixes](/docs/netwalldiode/v1.13.2/release-notes/netwall-diode-v1-6-0oq3#bug-fixes)

|  | Details |
| --- | --- |
| Authentication vulnerability fixed | Fixed a vulnerability that allowed a malicious actor to send a request to the web app without a valid session. It the dongle is not inserted (I.E. read only config mode) this vulnerability can not be exploited. |
| bugs | Several minor bugs fixed |

## [Known limitations](/docs/netwalldiode/v1.13.2/release-notes/netwall-diode-v1-6-0oq3#known-limitations)

N/A

MetaDefender
