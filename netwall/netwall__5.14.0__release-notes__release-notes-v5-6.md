<!-- source: https://www.opswat.com/docs/netwall/5.14.0/release-notes/release-notes-v5-6 -->

# Release Notes v5.6.0

| **Version** | Config: 5.6.0  USG-100: 1.0.0 BSG-100: 1.0.0 |
| --- | --- |
| **Release date** | Apr 2024 |
| **Scope** | Release to include Pi new features (append support), HA Database replication and new feature to capture packages in Diagnostic section |

## [New Features, Improvements and Enhancements](/docs/netwall/5.14.0/release-notes/release-notes-v5-6#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| High Availability Support | High Availability mechanism included |
| SKU update command in CLI | New command included in the CLI to update the SKU of a device |
| User account password min length changed | User account minimum length changed to 12 chars |
| Update Dolphin ICS eXpressWare | Dolphin ICS eXpressWare updated to latest GA version: 5.21.3 |
| Update REDIS | REDIS updated to v7.2.4 |
| Support package enhancement | Support package enhaced to add the output of lspci / dmesg commands |
| PCAP support | New feature included under Diagnostic that allow the user to do a packet capture |
| PI; append tag names | Added capability to append tag names |
| GUI changes | minor GUI changes |

## [Bug fixes](/docs/netwall/5.14.0/release-notes/release-notes-v5-6#bug-fixes)

|  | Details |
| --- | --- |
| Authentication vulnerability fixed | Fixed a vulnerability that allowed a malicious actor to send a request to the web app without a valid session. It the dongle is not inserted (I.E. read only config mode) this vulnerability can not be exploited. |
| bugfixing | Several minor bugs fixed |

## [Known limitations](/docs/netwall/5.14.0/release-notes/release-notes-v5-6#known-limitations)

N/A
