<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/manual-upgrade-of-kiosk-hardened-image -->

# Manual Upgrade of Kiosk Hardened Image

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Kiosk Hardened Image can be manually upgraded by downloading the appropriate upgrade package and providing the path to the folder containing it. Once the path is set, you can either click "Upgrade Now" or wait for the scheduled upgrade time. Kiosk will use the provided package to perform the upgrade.

## [Instruction](/docs/mdkiosk/v4.8.6/hardened-image/manual-upgrade-of-kiosk-hardened-image#instruction)

1. Identify the Kiosk Model

   - Login to Kiosk Console, Navigate to **Settings** > **About**.
   - Here you will find the **Kiosk Hardware Model** (e.g Dell 7230). This ensures you download the correct upgrade package.
2. Download the Upgrade Package

   - Based on your Kiosk model, download the corresponding **.zip and .yml files** (find the download links from the table below)
3. Prepare the upgrade folder

   - Create a folder on the Kiosk device or a shared network location.
   - Copy both the **.zip and .yml files** into this folder.
4. Provide the upgrade package path in the Kiosk Folder Upgrade option

   - Navigate to **Upgrades**, open the **Kiosk Hardened Image Upgrade** tab, and enable **Auto upgrade**
   - Select **Folder** option, set the **Folder path** to the folder containing the upgrade files. Click Save Updates
5. Trigger the Upgrade

   - Click **Upgrade Now** to start the upgrade immediately
   - Or set **upgrade schedule** for the upgrade

Using Networked shared folder for the upgrade

If a network folder is used as Upgrade option, please ensure the Windows account used to log in to the Kiosk system has the necessary permissions to access the network resource.

For example, If Kiosk uses a domain account for Windows logon, this account must have access to the assigned network folder.

## [Kiosk Hardened Image offline package](/docs/mdkiosk/v4.8.6/hardened-image/manual-upgrade-of-kiosk-hardened-image#kiosk-hardened-image-offline-package)

**Current version:** 26.10.0

| Model | Device | Upgrade Package |
| --- | --- | --- |
| Kiosk Desktop | Dell Pro 24, Dell 7420, Dell 7410, Lenovo M70a | - [kiosk-dell-desktop-hardened-image-pkg.zip](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-desktop/kiosk-dell-desktop/kiosk-dell-desktop-hardened-image-pkg.zip) - [kiosk-dell-desktop-hardened-image-pkg.yml](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-desktop/kiosk-dell-desktop/kiosk-dell-desktop-hardened-image-pkg.yml) |
| Kiosk Mobile/ Mini | Dell Pro Rugged 12, Dell 7230, Dell 7220 | - [k2100-dell-mobile-hardened-image-pkg.zip](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-mobile/kiosk-dell-mobile/kiosk-dell-mobile-hardened-image-pkg.zip) - [k2100-dell-mobile-hardened-image-pkg.yml](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-mobile/kiosk-dell-mobile/kiosk-dell-mobile-hardened-image-pkg.yml) |
| Kiosk Tower | D19U, D18S (XE5), D17S (XE4), D17S (7000) | - [kiosk-dell-tower-hardened-image-pkg.zip](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-tower/kiosk-dell-tower/kiosk-dell-tower-hardened-image-pkg.zip) - [kiosk-dell-tower-hardened-image-pkg.yml](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-tower/kiosk-dell-tower/kiosk-dell-tower-hardened-image-pkg.yml) |
|  | D15S (7090) (From an old Kiosk Hardened Image version) | [Kiosk Tower D15s (7090) - zip](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-tower/k3001-dell-d15s/k3001-dell-d15s-hardened-image-pkg.zip)  [Kiosk Tower D15s (7090) - yml](https://installer-cdn.opswat.com/kiosk-hardened-image/official-releases/26.10.0/kiosk-tower/k3001-dell-d15s/k3001-dell-d15s-hardened-image-pkg.yml) |
