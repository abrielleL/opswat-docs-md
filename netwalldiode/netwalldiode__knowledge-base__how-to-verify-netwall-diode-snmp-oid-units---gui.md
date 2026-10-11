<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui -->

# How to verify NetWall Diode SNMP OID Units & GUI

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [**Overview**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#overview)

This article documents the units returned by NetWall Diode SNMP OIDs for RAM and Disk monitoring, and how to verify these values using the NetWall web GUI.

> All OID values have been validated against a live NetWall Diode and match the GUI exactly.

## [**OID Unit Reference**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#oid-unit-reference)

#### [**RAM OIDs**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#ram-oids)

| OID | OID Path | Unit | Source |
| --- | --- | --- | --- |
| `meminfo-memtotal` | .1.3.6.1.4.1.61422.500.50 | kB (kilobytes) | `/proc/meminfo` → MemTotal |
| `meminfo-memfree` | .1.3.6.1.4.1.61422.500.51 | kB (kilobytes) | `/proc/meminfo` → MemFree |
| `meminfo-buffers` | .1.3.6.1.4.1.61422.500.52 | kB (kilobytes) | `/proc/meminfo` → Buffers |
| `meminfo-cached` | .1.3.6.1.4.1.61422.500.53 | kB (kilobytes) | `/proc/meminfo` → Cached |
| `meminfo-basispointsused` | .1.3.6.1.4.1.61422.500.54 | Basis points (÷100 = %) | Calculated |

#### [**Disk OIDs**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#disk-oids)

| OID | OID Path | Unit | Source |
| --- | --- | --- | --- |

| OID | OID Path | Unit | Source |
| --- | --- | --- | --- |
| `fs-persist-blocks` | .1.3.6.1.4.1.61422.500.60.1 | 1K-blocks | Persistent partition |
| `fs-persist-pct` | .1.3.6.1.4.1.61422.500.60.4 | Percentage (0–100) | Persistent partition usage |
| `fs-tmp-blocks` | .1.3.6.1.4.1.61422.500.60.9 | 1K-blocks | /tmp (tmpfs) partition |
| `fs-tmp-pct` | .1.3.6.1.4.1.61422.500.60.12 | Percentage (0–100) | /tmp partition usage |

> > **Important note on** `-pct` OIDs: The MIB DESCRIPTION states these are *"expressed in basis points (percentage times 100)"*, however testing has confirmed that the device **returns plain percentage (0–100)**, not basis points (0–10000). For example, 54% disk usage returns `54`, not `5400`.

## [**MIB Definitions (from OPSWAT-NETWALL-BLUE-MIB v1.11)**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#mib-definitions-from-opswat-netwall-blue-mib-v111)

#### [**RAM Section**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#ram-section)

meminfo-memtotal OBJECT-TYPE
SYNTAX INTEGER
MAX-ACCESS read-only
STATUS current
DESCRIPTION "total memory on-device"
::= { netwall-blue 50 }
meminfo-memfree OBJECT-TYPE
SYNTAX INTEGER
MAX-ACCESS read-only
STATUS current
DESCRIPTION "memory free on-device"
::= { netwall-blue 51 }
meminfo-buffers OBJECT-TYPE
SYNTAX INTEGER
MAX-ACCESS read-only
STATUS current
DESCRIPTION "memory buffers on-device"
::= { netwall-blue 52 }
meminfo-cached OBJECT-TYPE
SYNTAX INTEGER
MAX-ACCESS read-only
STATUS current
DESCRIPTION "memory allocated to cache on-device"
::= { netwall-blue 53 }
meminfo-basispointsused OBJECT-TYPE
SYNTAX INTEGER
MAX-ACCESS read-only
STATUS current
DESCRIPTION "memory usage in basis points"
::= { netwall-blue 54 }
#### [**Disk Section**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#disk-section)

fs-persist-blocks OBJECT-TYPE
SYNTAX Counter64
MAX-ACCESS read-only
STATUS current
DESCRIPTION "The number of persist-file-system blocks on the system."
::= { system-resources 1 }
fs-persist-pct OBJECT-TYPE
SYNTAX Counter64
MAX-ACCESS read-only
STATUS current
DESCRIPTION "The number of usable persist-file-system blocks on the system,
expressed in basis points (percentage times 100)."
::= { system-resources 4 }
fs-tmp-blocks OBJECT-TYPE
SYNTAX Counter64
MAX-ACCESS read-only
STATUS current
DESCRIPTION "The number of working-file-system blocks on the system."
::= { system-resources 9 }
fs-tmp-pct OBJECT-TYPE
SYNTAX Counter64
MAX-ACCESS read-only
STATUS current
DESCRIPTION "The number of usable working-file-system blocks on the system,
expressed in basis points (percentage times 100)."
::= { system-resources 12 }

---

## [**GUI Verification**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#gui-verification)

To compare SNMP values against actual system performance, navigate to the NetWall web console:

#### [**1. Disk Usage —** `Advanced > Statistics > File System Usage`](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#1-disk-usage--advanced--statistics--file-system-usage)

| Filesystem | Mount | 1K-blocks | Used | Available | Use% |
| --- | --- | --- | --- | --- | --- |
| `/dev/nvme0n1p2` | `/run/live/persistence/nvme0n1p2` | 1,898,640 | 1,018,912 | 869,728 | 54% |
| `tmpfs` | `/tmp` | 2,097,152 | 893,232 | 1,203,920 | 43% |

**Expected SNMP values:**

- `fs-persist-blocks` → **1898640**
- `fs-persist-pct` → **54**
- `fs-tmp-blocks` → **2097152**
- `fs-tmp-pct` → **43**

#### [**2. System Counters —** `Advanced > Statistics > System Counters`](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#2-system-counters--advanced--statistics--system-counters)

Displays the same counter values exposed via SNMP. Compare directly — no conversion needed.

#### [**3. Processes —** `Advanced > Statistics > Processes`](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#3-processes--advanced--statistics--processes)

Shows per-process CPU/memory usage (VSS and RSS in kB). Helpful for understanding what consumes memory.

---

## [**Quick Conversion Reference**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#quick-conversion-reference)

| To convert... | Do this |
| --- | --- |
| kB → GB | Divide by 1,048,576 |
| 1K-blocks → GB | Divide by 1,048,576 |
| Basis points → percentage (meminfo only) | Divide by 100 |

---

## [**Known Discrepancy**](/docs/netwalldiode/knowledge-base/how-to-verify-netwall-diode-snmp-oid-units---gui#known-discrepancy)

| Item | MIB Documentation Says | Actual Device Behavior |
| --- | --- | --- |
| `fs-persist-pct` | Basis points (0–10000) | **Plain percentage (0–100)** |
| `fs-tmp-pct` | Basis points (0–10000) | **Plain percentage (0–100)** |

This has been confirmed by customer testing (July 2026, Diode OD-102).

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

MetaDefender
