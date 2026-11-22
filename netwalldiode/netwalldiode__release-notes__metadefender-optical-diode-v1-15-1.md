<!-- source: https://www.opswat.com/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-15-1 -->

# MetaDefender Optical Diode v1.15.1

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | **Config:** 1.15.1; OD-101: 1.0.1 (Common Criteria EAL4+ certified, High Availability Not Supported) **Config:** 1.15.1; OD-102:1.0.2 , (Not EAL4+ Certified, High Availability Supported) |
| --- | --- |
| **Release Date** | October 30, 2026 |
| **Scope** | New AVEVA PI replication controls, HA status reporting, more efficient history backfill, PI Buffering support and multiple reliability fixes. |

> **Info**
>
> AVEVA PI 4.3.0 connector needs MetaDefender Optical Diode v1.15.1 to operate correctly. Please, update accordingly.

| Feature/Improvement | Details |
| --- | --- |
| AVEVA Pi Connector - Enable/Disable Pi Replication Configuration | Turns individual Pi replication configurations on/off from Blue, so a standby site can stay disabled until needed for failover. |
| AVEVA Pi Connector - HA Status PI Tag | New PI tag shows which HA node is active without opening the NetWall UI. |
| AVEVA Pi Connector - Digital Type for Control Tags | Preferred flanker and HA control tags can now be Digital, preventing invalid values. |
| AVEVA Pi Connector - HistElapsed Reported in Seconds | Blue HistElapsed is now an integer (seconds) so it can be trended in PI Vision. |
| AVEVA Pi Connector - Large Point Source Lists | Simplifies adding and managing large numbers of PI point sources. |
| AVEVA Pi Connector - Shared Point Sources | The same point source can now be used in multiple PI configurations. |
| AVEVA Pi Connector - No .bin File Required on Red (Pi2Pi) | Points are now matched by Point Name instead of PI Point Index, removing the .bin requirement on Red for Pi2Pi. |
| AVEVA Pi Connector - No Startup Wait for Schema | Pi2Pi and PI Database Replication now process snapshots and history immediately instead of waiting for the Blue schema. |
| AVEVA Pi Connector - Uninterrupted Processing During Point List Refresh | Schema and history processing now continue during a Red Point List refresh. |
| AVEVA Pi Connector - Smarter History Tracking and Backfill | Skips history already delivered via snapshots, and processes each history block only once and sends fewer queries to Red PI servers. |
| AVEVA Pi Connector - PI Buffering and Collective Support | Uses the PI Buffering System to write data to all collective members in chronological order, reducing out-of-order events on Red. |

## [Bug Fixes](/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-15-1#bug-fixes)

|  | Details |
| --- | --- |
| AVEVA Pi Connector - Automatic Backfill | Fixes History Stack overflows and “History stack size exceeded” errors on Red. |
| AVEVA Pi Connector - Memory Usage | Fixes memory growth issue after a Blue flanker restart and schema push. |
| AVEVA Pi Connector - Backfill Pacing | Fixed backfill running too quickly when no historical data exists. |
| AVEVA Pi Connector - Prepend/Append Point Names | Prefixed or suffixed points are now created on Red without restarting the Blue service. |
| AVEVA Pi Connector - Pi2Pi Flanker Installer | Windows firewall rule now uses the correct install path (C:\Program Files\OPSWAT). |
| AVEVA Pi Connector - Pi2Pi Flanker Uninstaller | Uninstall now stops svcOpswPi2PiBlue.exe correctly. |
| AVEVA Pi Connector - Missing Compression on Replicated Data | Data replicated to the destination PI server now goes through standard PI compression, so the destination archive stores same number of values as the source. |

## [Known Limitations](/docs/netwalldiode/release-notes/metadefender-optical-diode-v1-15-1#known-limitations)

MetaDefender
