<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/user-guide -->

# Overview

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Kiosk helps protect your network by enabling control over the flow of data into and out of your organization. It can be used as a media scanning station on your own hardware or on OPSWAT's custom-made kiosks. Media such as USB devices, DVDs, SD cards, flash drives, or floppy disks are processed by Kiosk. After the scan is complete, Kiosk generates a detailed report.

This user guide covers installing, configuring, upgrading, using, and troubleshooting MetaDefender Kiosk.

## [Key Features](/docs/mdkiosk/v4.8.6/operating/user-guide#key-features)

- Protection against zero-day attacks (MetaDefender Core integration)
- Customized data security policies
- Control over data flow
- Active Directory authentication
- Custom Authentication
- Portable Media support including floppy disks, SD cards, CDs, DVDs, encrypted USB, and more
- UI localization

  - Contains bundled language translations and the ability to manually additional languages
- Securely wipe USB drives
- Easier system hardening

---

## [User authentication](/docs/mdkiosk/v4.8.6/operating/user-guide#user-authentication)

MetaDefender Kiosk has the following authentication features:

- Active Directory authentication
- Support for [Custom Authentication Module](/docs/mdkiosk/v4.8.6/advanced-deployment/custom-authentication-module)

---

## [Peripheral media](/docs/mdkiosk/v4.8.6/operating/user-guide#peripheral-media)

MetaDefender Kiosk automatically detects multiple peripheral media insertions for the following:

Common media types:

- USB devices
- Encrypted USB devices (refer to [supported encrypted USB device list](https://www.opswat.com/docs/mdkiosk/operating/user-guide#encrypted-usb-devices))
- CDs/DVDs/Blu-ray
- Card readers
- SD cards
- Floppy disks

Other media types:

- CF Card
- MS Pro Duo
- XDCAM drive (refer to [How to scan XDCAM Drive in Kiosk? - MetaDefender Kiosk Windows](https://www.opswat.com/docs/mdkiosk/knowledge-base/how-to-scan-xdcam-drive-in-kiosk-))

Info

Not all USB devices are currently supported. If you have a specific device you need supported, please contact OPSWAT support.

---

## [Encrypted USB devices](/docs/mdkiosk/v4.8.6/operating/user-guide#encrypted-usb-devices)

MetaDefender Kiosk can unlock encrypted USB devices with a given password and process its contents. Kiosk supports the following encrypted USB devices:

| Device | Software Version | Firmware Version | Scanning | Wipe | File Handling | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Apricorn Aegis Secure Key |  |  | ✔️ | ✔️ | ✔️ |  |
| Aegis Padlock 3 | A25-3PL128-XXXX |  | ✔️ | ✔️ | ✔️ |  |
| Apricorn Aegis Fortress |  |  | ✔️ | ✔️ | ✔️ |  |
| Apricorn Aegis Bio |  |  | ✔️ | ✔️ | ✔️ |  |
| Avira-Iron-Drive I | InfoPure - 3.201812 |  | ✔️ | ❌ | ✔️ |  |
| Biocryptodisk-ISPX |  |  | ✔️ |  |  |  |
| Buffalo RUF2-HSCT | PASSWORD - 2.67 |  | ✔️ | ✔️ | ✔️ |  |
| Buffalo RUF3-HSL | OPEN_HS - 2.68 |  | ✔️ | ✔️ | ✔️ | Not supported as copy -to destination with all encrypted scan source devices, except **SanDisk Cruzer Enterprise FIPS Edition** and **Bitlocker USBs**. |
| Datalocker DL4 FE | 6.8.2.0 | 3.0.8 | ✔️ | ✔️ | ✔️ | End user is required to press 'LOCK and DISCONNECT' on the device screen to safely eject the device |
| DataLocker H350 | 6.8.1.0 | 1.1.1 | ✔️ | ✔️ | ✔️ |  |
| DataLocker Sentry K350 |  |  | ✔️ | ✔️ | ✔️ |  |
| DataLocker Sentry 3 FIPS | 6.8.1.0 | 3.05 | ✔️ | ✔️ | ✔️ |  |
| DataLocker Sentry ONE | 6.8.1.0 | 03.05 | ✔️ | ✔️ | ✔️ | Versions managed with SafeConsole are also supported |
| DataLocker Sentry ONE Managed | 6.6.0.0 | 03.05 | ✔️ | ✔️ | ✔️ |  |
| DataLocker Sentry 3.0 | 4.8.1 |  | ✔️ | ✔️ | ✔️ |  |
| DataLocker Sentry 5 FIPS (Managed) | 6.7.0.0 |  | ✔️ | ✔️ | ✔️ |  |
| ELECOM MF-PUVT | 1.0.0.452 |  | ✔️ | ✔️ | ✔️ |  |
| ELECOM MF-ENU3A | 1.0.0.269 |  | ✔️ | ✔️ | ✔️ |  |
| Greenhouse PicoDrive Secure GH-UF3SRxG |  |  | ✔️ | ✔️ | ✔️ | Does not support Copy&Go and Copy to 2nd Greenhouse PicoDrive USB |
| Integral Courier FIPS 197 | 1.0.3.1 |  | ✔️ |  |  |  |
| Kingston DataTraveler Vault Privacy | 1.06 |  | ✔️ | ✔️ | ✔️ |  |
| Kingston DataTraveler Vault Privacy 3.0 - (DTVP30) | 3.0.1.1 |  | ✔️ | ✔️ | ✔️ |  |
| Kingston DataTraveler Vault Privacy 3.0 - (DTVP30M-R) | 4.8.2.1 |  | ✔️ | ✔️ | ✔️ |  |
| Kingston DataTraveler Locker+ G3 | 3.0.0.3 | 1.03 | ✔️ | ✔️ | ✔️ |  |
| Kingston IronKey D250 | 3.4.3.0 |  | ✔️ | ✔️ | ✔️ |  |
| Kingston IronKey D300 | 3.4.3.0 |  | ✔️ | ✔️ | ✔️ |  |
| Kingston IronKey D300S | 3.4.3.0 |  | ✔️ | ✔️ | ✔️ | Re-enter the password when the use of an incorrect password has not been supported yet. |
| Kingston IronKey D500S | 3.4.3.0 |  | ✔️ | ✔️ | ✔️ |  |
| Kingston IronKey S1000 | 6.7.0.0 |  | ✔️ | ✔️ | ✔️ |  |
| Ivanti encrypted devices |  |  | ✔️ | ❌ | ✔️ | Support decrypt USB devices encrypted via Ivanti Device Control |
| Kanguru Defender Elite 30 |  |  | ✔️ | ✔️ | ✔️ |  |
| Kanguru Defender Elite 200 | 4.0.8.1 |  | ✔️ | ✔️ | ✔️ |  |
| Kanguru Defender Elite 300 |  |  | ✔️ | ✔️ | ✔️ |  |
| Kanguru Defender 2000 | 5.1.6.8 |  | ✔️ | ✔️ | ✔️ |  |
| Kanguru Defender 3000 | 5.6.8.0 |  | ✔️ | ✔️ | ✔️ |  |
| McAfee Complete Data Protection | 4.3.0.224 |  | ✔️ | ❌ |  | McAfee File and Removable Media Protection client is installed on the system that MetaDefender Kiosk is installed. |
| Trellix File and Removable Media Protection  *As of December 30, 2022, McAfee File and Removable Media Protection is now known as Trellix File and Removable Media Protection (Trellix FRP)* | 5.4.3.170 - 5.4.4 - 5.6.0 |  | ✔️ | ❌ | ✔️ | Trellix File and Removable Media Protection client is installed on the system that MetaDefender Kiosk is installed. Details can be referred to at [How to encrypt a USB with Trellix and use it with a Kiosk (formerly McAfee)](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-encrypt-a-usb-with-trellix--formerly-mcafee--and-scan-wit) |
| Microsoft BitLocker |  |  | ✔️ | ❌ | ✔️ | Supports BitLocker To Go using passwords. MetaDefender Kiosk does not support BitLocker encryption using key files, smart cards, or VHD (Virtual Hard Drive) BitLocker encryptions. |
| SanDisk Cruzer Enterprise FIPS Edition | 2.5 SDK 1.2.10.12 | 6.615 | ✔️ |  |  |  |
| SanDisk Cruzer Contour U3 based USB | 4.08 U3 Launchpad - 1,6,1,1 |  | ✔️ |  |  |  |
| SDMS MkIII AES Duoulock | 1.0.0.8 | 1.21 | ✔️ | ✔️ | ✔️ |  |
| USB Flash Security | 4.1.12.17 |  | ✔️ |  |  |  |
| Viasat Freedom 600 | 4.1.14 |  | ✔️ | ✔️ | ✔️ | The Eclypt Management Application (`ema-ui.exe`) must be installed on the system in order to unlock the device. |
| WD My Passport |  |  | ✔️ | ✔️ | ✔️ | Utility-enabled encrypted hard devices |
| Viasat Freedom 100 | 4.1.14 |  | ✔️ | ✔️ | ✔️ | The Eclypt Management Application (`ema-ui.exe`) must be installed on the system in order to unlock the device. |

Warning

Encrypted devices are not supported by OPSWAT Media Validation Agent (OMVA)

---

## [Media handling](/docs/mdkiosk/v4.8.6/operating/user-guide#media-handling)

MetaDefender Kiosk's media handling features include the following:

- Can process drives with multiple partitions
- Can process full or partial media
- Can wipe/format USB drives
- Supports integration with MetaDefender Managed File Transfer for uploading files for processing or uploading/downloading processed files
- USB device soft eject
- CD/DVD eject

---

## [Processing files](/docs/mdkiosk/v4.8.6/operating/user-guide#processing-files)

MetaDefender Kiosk uses MetaDefender Core to process files. MetaDefender Core has the following processing features:

- Scanning with multiple anti-malware engines
- Data sanitization
- Application vulnerability detection
- Heuristics for zero-day threats
- Archive extraction
- File type verification
- Workflow engines

---

## [Processing session results](/docs/mdkiosk/v4.8.6/operating/user-guide#processing-session-results)

After processing media, MetaDefender Kiosk allows you to view detailed logs and print results.

---

## [Customizable interface](/docs/mdkiosk/v4.8.6/operating/user-guide#customizable-interface)

The MetaDefender Kiosk user interface includes multiple display languages:

- English
- Arabic
- Hebrew
- Korean
- Vietnamese
- German
- Japanese
- Spanish
- French

With the additional support of customizing the bundled languages or adding other languages.

On-screen keyboards are also supported for all of these languages.

Refer to [UI Localization / Customization - MetaDefender Kiosk Windows](https://www.opswat.com/docs/mdkiosk/advanced-deployment/ui-localization---customization#edit-a-language)

---

## [System hardening](/docs/mdkiosk/v4.8.6/operating/user-guide#system-hardening)

MetaDefender Kiosk comes with a variety of system hardening features for additional security:

- Disables autorun of inserted media
- Users can only exit by pressing `ALT+S` and if Kiosk is configured to require a password to exit, entering the exit password
- User interface blocks direct access to the underlying system and unnecessary keystrokes
- Runs automatically on system startup

### [Defending against BadUSB devices](/docs/mdkiosk/v4.8.6/operating/user-guide#defending-against-badusb-devices)

A range of BadUSB devices, including well-known ones like RubberDucky and BashBunny, mimic standard USB flash storage devices in appearance. Beneath that facade, they present a USB keyboard (or network adapter) interface when connected to a host system, and use it to execute keystroke sequences that launch processes, open a shell, or change system settings.

Starting in Kiosk 4.8.0, you can turn on **Bad USB Detection** to actively identify and isolate these devices the moment they're plugged in, instead of only suppressing their keystrokes in the background.

**To turn on Bad USB Detection:**

1. In the Kiosk Management Console, go to **Settings > System Hardening**.
2. Turn on **Bad USB Detection**.
3. Click **Save Updates**.

Bad USB Detection is off by default, so existing Kiosk deployments are not affected until an administrator turns it on.

**What happens when a suspicious device is detected**

When a connected USB device presents an interface other than storage — such as a keyboard or a network adapter — Kiosk isolates that interface right away and shows a warning on screen naming the device and what it appears to be, so the person at the Kiosk knows a device has been blocked and why.

- **If the device looks like a keyboard**, a short numeric code appears on screen. Entering that code on the on-screen keypad allows the keyboard to work for the rest of that session.
- **For other device types** (for example, a network or Bluetooth adapter), a simple confirmation prompt is shown instead of a code.

Unblocking a device this way only applies while it stays plugged in — unplugging and reconnecting the same device triggers the check again.

**Permanently blocking a device**

From the warning screen, an administrator can choose to permanently block a specific device instead of allowing it. Once blocked, that same device is ignored automatically on future connections, with no warning shown. To clear this list and start over, go to **Settings > System Hardening**, turn on **Bad USB Detection** if it isn't already on, and click **Reset Blocked USB List**.

Note

Bad USB Detection only affects devices that present a non-storage interface (like a keyboard or network adapter). Ordinary USB storage devices continue to be scanned normally — this feature doesn't change how Kiosk handles legitimate storage media.
