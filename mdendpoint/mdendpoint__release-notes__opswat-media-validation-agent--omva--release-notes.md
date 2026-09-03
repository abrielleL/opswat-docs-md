<!-- source: https://www.opswat.com/docs/mdendpoint/release-notes/opswat-media-validation-agent--omva--release-notes -->

# OPSWAT Media Validation Agent (OMVA) Release Notes

### Version 2.0.21

**Windows 7 and Above:** 2.0.21.374

**Release date:** August 12, 2026

Enhancements

- Supports OS-level ejection, allowing users to eject peripheral media device during active validation

---

**Windows 7 and Above:** 2.0.21.368

**Release date:** July 14, 2026

Bug fixes

- **Safe Removal of USB Devices:** Fixed an issue where removable storage media (USB drives) could not be safely ejected while OMVA is installed. Ejecting now works from both File Explorer and the system tray ("Safely Remove Hardware"), for validated as well as blocked devices, without requiring administrator privileges.

**Known Limitations**

- CD/DVD Ejection: Optical media (CD/DVD) cannot be ejected from File Explorer. To remove a disc, please use the physical eject button on the CD/DVD drive.
- During the validation process, users cannot perform the Eject action until validation is complete.

---

### Version 2.0.20

**Windows 7 and Above:** **2.0.20**

**Release date:** June 26, 2026

Enhancements

- Improved verification for USB devices that contain folders with multi-byte names (e.g. Japanese, Chinese, Korean, emoji, or accented characters).

### Version 2.0.19

**Windows 7 and Above:** **2.0.19 | Windows 7 SP1 without SHA256:** **2.0.19**

**Release date:** November 19, 2025

Enhancements

- **Allow Virtual-Mounted ISO Drives:** Introduced capability to allow mounting ISO drives that have been validated.

---

### Version 2.0.18

**Windows 7 and Above:** **2.0.18.343 | Windows 7 SP1 without SHA256:** **2.0.18.343**

**Release date:** October 24, 2025

Enhancements

- **Admin-Defined Trusted Devices:** Enable administrators with greater flexibility to define trusted internal peripheral devices and selectively allow or block their use based on security policies

---

### Version 2.0.17

**Windows 7 and Above:** **2.0.17.339 | Windows 7 SP1 without SHA256: 2.0.16.340**

**Release date:** September 17, 2025

Enhancements

- **Reduced Memory Consumption:** Optimized workflows and mechanisms to reduce memory usage during agent runtime.

---

### Version 2.0.16

**Windows 7 and Above: 2.0.16.335 | Support Windows 7 SP1 without SHA256: 2.0.16.336**

**Release date:** August 20, 2025

Enhancements

- Support validating manifest files in General.OPSWAT folder for XDCAM device

---

### Version 2.0.15

**Release date:** July 16, 2025

Enhancements

- **Integrity Checking Tooltip:** OPSWAT Media Validation Agent now displays the status of file integrity checking in the tray icon tooltip when hovering, giving users clear, continuous visibility until the device check is fully complete.

---

### Archived Release Notes

**Release date:** June 18, 2025

- **Support for Always-Connected USB drives:** OPSWAT Media Validation Agent (OMVA) now automatically validates all plugged USB drives after system reboots, ensuring seamless continuity for users.

**Release date:** May 21, 2025

- Support the Windows 7 SP1 without installing KBs

**Release date:** February 21, 2025

Bug fixes:

- The tray icon no longer shows the image after the machine restarts.
- USB drive validation fails when the agent detects multiple simultaneous insert events, occurring only when users restart the machine or connect a USB device with multiple partitions.
