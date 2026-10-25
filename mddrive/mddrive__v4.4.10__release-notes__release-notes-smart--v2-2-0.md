<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/release-notes/release-notes-smart--v2-2-0 -->

# MetaDefender Drive Smart Touch v2.2.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

|  |  |
| --- | --- |
| **Released on** **Sep 08, 2026** | This release includes new features, improvements, bug fixes. |

**New Features**

- **Reset from SmartTouch:** Administrators can reset a Smart Touch back to its previous known working state from the device itself, recovering units stuck in activation loops or with a corrupted image. Refer to [Reset MetaDefender Drive Image with Smart Touch](/docs/mddrive/v4.4.10/maintenance/reset-smart-touch).

**Improvements and Bug Fixes**

- A Drive that cannot reach an update server still lists the engines it holds in System Settings, rather than reporting none.
- Starting a second scan after a reboot without reconnecting the cable no longer strips MetaDefender Drive of its engines or its OPSWAT Central Management enrollment.
- Engine transfers that stop because the wireless connection was switched off report the lost connection, so an operator reconnects and retries rather than flashing the drive again.
- When the connected network reports a time zone, syncing the clock adopts it automatically, so scan timestamps match local time without an operator selecting the zone by hand.
- Importing a certificate authority certificate for Wi-Fi follows the same full-screen prompt-and-result flow as the Kiosk and Secure Storage imports, bringing the consistency in user experience.
