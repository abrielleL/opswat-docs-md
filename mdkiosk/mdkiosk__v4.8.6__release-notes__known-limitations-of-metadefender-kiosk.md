<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk -->

# Known Limitations

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Handling Multiple Devices](/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk#handling-multiple-devices)

MetaDefender Kiosk does not allow multiple devices to be processed at the same time.

Each device must be inserted independently.

---

## [Non-Windows Partitions](/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk#non-windows-partitions)

Wiping non-Windows partitions is not currently supported.

While non-Windows partitions are generally supported for USBs and other media, they are not supported within a VMDK file.

---

## [USB Hubs](/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk#usb-hubs)

If a USB hub with multiple USB drives is inserted into a MetaDefender Kiosk system for processing, Kiosk will only scan the first device reported to Windows.

This is not guaranteed to be the same device each time the USB hub is inserted.

OPSWAT does not recommend connecting drives to MetaDefender Kiosk through a USB hub.

---

## [Private or encrypted partitions](/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk#private-or-encrypted-partitions)

If a device has a private, or encrypted partition, MetaDefender Kiosk may not be able to read it. Encrypted drives can be scanned as described in [Unlocking Encrypted Devices](/docs/mdkiosk/v4.8.6/operating/unlocking-encrypted-devices). Non-primary encrypted partitions can be blocked in the MetaDefender Kiosk Management Console. If a drive does not have any readable partitions, you can use MetaDefender Kiosk’s wipe functionality to clean the drive and ensure that there are no hidden partitions. Refer to the Advanced Options section of [Configuring Global Kiosk Settings](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-global-kiosk-settings) for additional information.

---

## [User Account Control](/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk#user-account-control)

If UAC is not disabled, MetaDefender Kiosk's watchdog functionality may not work as expected.

---

## [Other Known Issues](/docs/mdkiosk/v4.8.6/release-notes/known-limitations-of-metadefender-kiosk#other-known-issues)

- Kiosk is expected to be operated on a local, physical system. Operating the Kiosk in a remote desktop session is not supported.
- All external USB drives, such as SD card readers, floppy disk drives, and CD ROM drives, must be inserted before MetaDefender Kiosk is started.
- Kingston encrypted devices have issues unlocking when used as a copy-to device with source media that is non-Kingston encrypted.
- For certain encrypted devices (e.g. Kanguru, Ironkey and Kingston), unlocking may fail even with the correct password if a user interacts with the Kiosk UI during the process of unlocking.
