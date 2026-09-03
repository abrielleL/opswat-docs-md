<!-- source: https://www.opswat.com/docs/mdmediafirewall/troubleshooting/troubleshooting -->

# Troubleshooting

## [Support Package](/docs/mdmediafirewall/troubleshooting/troubleshooting#support-package)

A support package contains essential information regarding the Media Firewall system’s operation. For any issues encountered with the Media Firewall, please generate a support package and provide it when reaching out to Customer Support.

**Creating the package**

1. Prepare a USB with a folder named `Gather OPSWAT support package` at the root directory
2. Insert the USB into the rear `USB-A` port when not running a scan

   1. The support package can only be generated after [Setup Mode](https://docs.opswat.com/mdmediafirewall/setup/getting-started#setup-mode) is complete
3. Wait at least 5 minutes or (if your USB has an activity light) wait until the USB activity light stops flashing
4. Unplug the USB

Successful package creation will generate 2 files in the `Gather OPSWAT support package` directory:

- `UF3-SupportPackage` - the full support package
- `UF3-SupportPackage.sha256` - hash of the support package to ensure completeness

If any file is missing or the hash does not match the package, reattempt the process again until successful.

Warning

It is recommended that the USB used to retrieve a support package be formatted to anything other than FAT32.

In rare cases, a support package may grow larger than 4GB and may result in failure to obtain the package due to exceeding the file size limitation of FAT32.

---

## [Factory Reset](/docs/mdmediafirewall/troubleshooting/troubleshooting#factory-reset)

To re-configure the MMF (certificate, network connection, management connection, etc...) it will need to be reset to a factory state:

1. Power on the MMF

   1. The unit will start the [Power on sequence](https://docs.opswat.com/mdmediafirewall/operating#power-on-sequence)
2. During the phase where each media indicator cycles a WHITE display, hold down the `RESET` button on the back of the unit
3. When the power indicator begins to flash RED, continue to hold down the `RESET` button for **~8 seconds**

   1. the power indicator will actively flash RED while it is resetting
4. When complete, the power indicator will show a solid RED light
5. A power cycle will allow the MMF to start back into Setup Mode

Warning

Factory resetting the system will remove the existing configuration settings & certificate and the internal hard drive will be wiped

---

## [LED State Guide](/docs/mdmediafirewall/troubleshooting/troubleshooting#led-state-guide)

The LED lights on the Media Firewall convey specific information respective to the functionality performed.

The tables below outline the different meanings.

### [General](/docs/mdmediafirewall/troubleshooting/troubleshooting#general)

| States | Meaning | Additional Info |
| --- | --- | --- |
| Solid | Final Result |  |
| Active flash | Activity | Momentary on/off flashing |
| Long flash + 1 quick flash | Warning | Always ORANGE |
| Long flash + 2 quick flashes | Error | Always RED |

### [Power indicator](/docs/mdmediafirewall/troubleshooting/troubleshooting#power-indicator)

| States | Meaning |
| --- | --- |
| Solid WHITE | MMF is powering on |
| Solid GREEN | MMF is powered on and ready |
| Active flash GREEN | MMF is internally accessing files |
| Active flash RED | MMF is unusable - system issue. Unit will attempt to auto-restart back into a working state. |

### [Media indicator](/docs/mdmediafirewall/troubleshooting/troubleshooting#media-indicator)

| States | Meaning |
| --- | --- |
| Active flash CYAN | Scan in progress - green will result on completion or Writing files to the media is in progress |
| Active flash ORANGE | Scan in progress - orange will result on completion |
| Active flash RED | Scan in progress - red will result on completion |
|  |  |
| Solid GREEN | Scan finished - all files are allowed |
| Long flash + 1 quick flash ORANGE | Scan finished - some files are blocked/concealed |
| Long flash + 2 quick flashes RED | Scan finished - media error during scan |
|  |  |
| Alternating BLUE & CYAN among all indicators | Update in progress |
| Alternating ORANGE & CYAN among all indicators | Update package is of a lesser or same version - update will not be performed |

### [Setup Mode](/docs/mdmediafirewall/troubleshooting/troubleshooting#setup-mode)

| Indicators | Status | Meaning |
| --- | --- | --- |
| Power indicator | Solid GREEN | MMF is powered on and ready |
| USB A indicator | Active flash RED | Certificate is invalid or missing |
| Compact Flash indicator | *blank* | No configuration issues detected |
|  | Active flash RED | Settings in `config.ini` are invalid |
| All other media indicators | *blank* | No configuration issues detected |
|  | All solid GREEN | MMF is configured correctly and requires to turn the unit off & on to be fully operational |

### [Alert Mode](/docs/mdmediafirewall/troubleshooting/troubleshooting#alert-mode)

Info

When `Port Alarm Protection` is enabled

| Indicators | Status | Meaning |
| --- | --- | --- |
| All indicators | Active flash RED | The MMF has been disconnected from the Host. Restore the connection to allow the MMF to be operational. |

---

## [Host System Power Negotiation over USB-C Port](/docs/mdmediafirewall/troubleshooting/troubleshooting#host-system-power-negotiation-over-usb-c-port)

The Host System cannot power on the MetaDefender Media Firewall over USB-C. When a `USB-C to USB-C` cable connects the Host System to the MetaDefender Media Firewall, the Host System will negotiate the power draw demanded by the MetaDefender Media Firewall. A message will appear on the Host System to inform the user that there is no sufficient power over USB-C to run the MetaDefender Media Firewall exclusively. Dismiss this message and rely on the 12VDC power supply provided within the kit.

USB device might need more power

This message does not appear when the Host System connects to the MetaDefender Media Firewall using the `USB-C to USB-A` cable supplied within the kit.

---

## [USB Hub support](/docs/mdmediafirewall/troubleshooting/troubleshooting#usb-hub-support)

#### [USB Hub connection to Host](/docs/mdmediafirewall/troubleshooting/troubleshooting#usb-hub-connection-to-host)

It is highly recommended to connect Media Firewall directly to a Host system for optimal security and performance.

If the Media Firewall is connected to a Host via a hub or adapter, it is not guaranteed to work as expected.

| Hub tested | Supported |
| --- | --- |
| Apple USB-C Multiport Adapter | ✔️ |
| Dell DA20 | ❌ |
| Lention USB C Hub (CB-C31) | ✔️ |

Info

Table is not comprehensive - provides insight into known USB hubs encountered

#### [USB Hub connection to Media Firewall](/docs/mdmediafirewall/troubleshooting/troubleshooting#usb-hub-connection-to-media-firewall)

It is expected for media to be connected directly into the Media Firewall.

Connecting a hub to any of the media ports is not supported.
