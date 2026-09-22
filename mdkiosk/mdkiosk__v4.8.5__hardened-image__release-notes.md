<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/hardened-image/release-notes -->

# Release Notes

The new version of Deployment Tool is required to deploy Kiosk Hardened Image 25.06.0

| **Version** | Kiosk Hardened Image 26.09.0 |
| --- | --- |
| **Release Date** | Sept 18, 2026 |
| **Scope** | This release updates the hardened image's applications and system components to their latest versions for improved performance, security, and compatibility. It bundles MetaDefender Kiosk 4.8.5.9455 and MetaDefender Core 5.22.0 on Windows 10 IoT Enterprise LTSC (21H2, Build 19044.7725). Enhance and support detect hardware-encrypted USB with USB 2.0 mode |

| Kiosk Hardened Image 26.09.0 - Sept 18, 2026 | |
| --- | --- |
| **MD KIOSK version** | 4.8.5.9455 [Release Notes](https://www.opswat.com/docs/mdkiosk/v4.8.5/release-notes) |
| **MD Core version** | 5.22.0 [Release Notes](https://www.opswat.com/docs/mdcore/v5.22.0/release-notes/release-notes) |
| **Windows OS version** | Windows 10 IoT Enterprise LTSC (21H2, Build 19044.7725) |
| **BIOS version** | - Kiosk Tower (D19U): 1.18.0 - Kiosk Tower (D18S-XE5): 1.41.0 - Kiosk Tower (D17S-XE4): 1.41.0 - Kiosk Tower (D17S-7000): 1.40.0 - Kiosk Tower (D15S-7090): 1.43.0 - Kiosk Desktop (Dell Pro 24): 1.18.0 - Kiosk Desktop (Dell 7420): 1.37.0 - Kiosk Desktop (Dell 7410): 1.27.0 - Kiosk Desktop (Lenovo M70a): M2SKT2EA - Kiosk Mobile/Mini (Dell Pro Rugged 12): 1.52.0 - Kiosk Mobile/Mini (Dell 7230): 1.33.0 - Kiosk Mobile (Dell 7220): 1.12.0 |
| **What's new** |  |
| Application and system update | Updated applications and system components to the latest versions (Windows 10 IoT Enterprise LTSC (21H2, Build 19044.7725), MD Kiosk 4.8.5.9455, MD Core 5.22.0) to ensure optimal performance, security, and compatibility. |
| Enforce OPSWAT USB hub to use USB 2.0 mode | On OPSWAT Kiosk devices, administrators can now configure the OPSWAT USB hub to use USB 2.0 mode from Configuration > Advanced > Encrypted USB, allowing hardware-encrypted USB drives to be detected reliably.  When this option is not enabled, Kiosk can still automatically detect when a hardware-encrypted USB drive fails to mount and switch to USB 2.0 mode. |
