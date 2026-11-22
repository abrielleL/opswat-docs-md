<!-- source: https://www.opswat.com/docs/mddrive/release-notes/release-notes-smart-touch -->

# MetaDefender Drive Smart Touch v2.4.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

|  |  |
| --- | --- |
| **Released on** **Nov 10, 2026** | This release includes new features, improvements, bug fixes. |

**New Features**

- **Remote wipe and lock:** Administrators can erase all Secure File Storage data or lock a lost Smart Touch device from Central Management, and the lock holds until the correct code is entered. Refer to [Wipe Data and Lock a Lost Drive with Smart Touch from Central Management](/configuration/wipe-and-lock-smart-touch-remotely-from-cm).
- **Smart Touch preferences from Central Management:** Administrators manage all Smart Touch preferences from OPSWAT Central Management, not only certificates, so settings stay consistent across every enrolled drive without visiting each device.

**Improvements and Bug Fixes**

- **Quarantine restore audit:** Restore actions recorded on the drive are forwarded to Central Management by Smart Touch on the next sync, keeping the audit trail complete when the drive was offline.
- **In-Session configuration sync:** Smart Touch re-applies OPSWAT Central Management's In-Session settings after each host session ends, so operator configuration does not drift from what Central Management prescribes between sessions.
