<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/release-notes -->

# Release Notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page New Version of Deployment Tool is required

The new version of Deployment Tool is required to deploy Kiosk Hardened Image 25.06.0

| **Version** | Kiosk Hardened Image 26.10.0 |
| --- | --- |
| **Release Date** | Oct 21, 2026 |
| **Scope** | This release updates the hardened image's applications and system components to their latest versions for improved performance, security, and compatibility. It bundles MetaDefender Kiosk 4.8.6.0639 and MetaDefender Core 5.22.1 on Windows 10 IoT Enterprise LTSC (21H2, Build 19044.7807). Enhance and support Kiosk Hardened Image Upgrade from a USB |

| Kiosk Hardened Image 26.10.0 - Oct 21, 2026 | |
| --- | --- |
| **MD KIOSK version** | 4.8.6.0639 [Release Notes](https://www.opswat.com/docs/mdkiosk/v4.8.6/release-notes) |
| **MD Core version** | 5.22.1 [Release Notes](https://www.opswat.com/docs/mdcore/v5.22.0/release-notes/release-notes) |
| **Windows OS version** | Windows 10 IoT Enterprise LTSC (21H2, Build 19044.7807) |
| **BIOS version** | - Kiosk Tower (D19U): 1.19.3 - Kiosk Tower (D18S-XE5): 1.19.3 - Kiosk Tower (D17S-XE4): 1.42.0 - Kiosk Tower (D17S-7000): 1.42.0 - Kiosk Tower (D15S-7090): 1.44.0 - Kiosk Desktop (Dell Pro 24): 1.19.1 - Kiosk Desktop (Dell 7420): 1.38.0 - Kiosk Desktop (Dell 7410): 128.0 - Kiosk Desktop (Lenovo M70a): M2SKT2EA - Kiosk Mobile/Mini (Dell Pro Rugged 12): 1.14.0 - Kiosk Mobile/Mini (Dell 7230): 1.34.0 - Kiosk Mobile (Dell 7220): 1.48.0 |
| **What's new** |  |
| Application and system update | Updated applications and system components to the latest versions (Windows 10 IoT Enterprise LTSC (21H2, Build 19044.7807), MD Kiosk 4.8.6.0639, MD Core 5.22.1) to ensure optimal performance, security, and compatibility. |
| Kiosk Hardened Image Upgrade from a USB Drive | Administrators can now select a USB drive as a hardened image upgrade source in the Kiosk Console, alongside the existing My OPSWAT (Internet) and Folder sources, so offline deployments can apply a new hardened image directly at the Kiosk. When a USB drive containing a valid image package is inserted, the Kiosk UI detects the package, runs validation checks, and prompts for the Exit Password if one is configured before copying the package locally and starting the upgrade. |
