<!-- source: https://www.opswat.com/docs/netwall/release-notes/release-notes-v5-12-1 -->

# Release Notes v5.12.1

| **Version** | Config: 5.12.1; USG-100: 1.0.0 (CC EAL4+ certified) |
| --- | --- |
|  | Config: 5.12.1; BSG-100: 1.0.0 (IEC 62443 certified) |
| **Release date** | February 6, 2026 |
| **Scope** | Bug Fixes: File Transfer History, UDP |

## [Bug fixes](/docs/netwall/release-notes/release-notes-v5-12-1#bug-fixes)

|  | Details |
| --- | --- |
| File Transfer History | Addresses issue whereby File Transfer history tables are not being created on new installations. |
| IEC104 Connector | connector now allows reuse of origin/common address for entries with the same IP/Port. |
| UDP Fragment Transmission | Addresses issue whereby large fragmented datagrams on the USG/BSG Blue Side are incorrectly transmitted on the Red Side. |

## [Known Limitations](/docs/netwall/release-notes/release-notes-v5-12-1#known-limitations)

N/A
