<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/secure-image/creating-deployment-usb -->

# Creating Secure Image Deployment flash drive

Follow the steps to create a bootable flash drive containing the Kiosk Secure Image to facilitate the efficient deployment of MetaDefender Kiosk on various Kiosk hardware models

Requirements:

- A PC running Windows 7/8/8.1/10 or 11
- A USB flash drive (USB 3.0 or above) with a storage capacity of at least 32GB.
## [Step 1: Download Secure Image Deployment Wizard and Image Package](/docs/mdkiosk/v4.8.5/secure-image/creating-deployment-usb#step-1-download-secure-image-deployment-wizard-and-image-package)

1. Download the Secure Image Deployment Wizard: [**WINPEBootable.vhd**](https://installer-cdn.opswat.com/kiosk-secure-image/Deployment_Tools/WinPEBootable.vhd)
2. When licensed, you can see the **MetaDefender Kiosk Secure Image** download section inside the **MetaDefender Kiosk** download page on [MyOPSWAT Portal](https://my.opswat.com/home/metadefender-kiosk)

Download page of MetaDefender Kiosk Secure Image on My OPSWAT Portal

## [Step 2: Create bootable flash drive](/docs/mdkiosk/v4.8.5/secure-image/creating-deployment-usb#step-2-create-bootable-flash-drive)

Download [Rufus tool](https://rufus.ie/downloads/) ([version 4.5](https://installer-cdn.opswat.com/kiosk-secure-image/Deployment_Tools/rufus-4.5.exe) is recommended) to format and create bootable USB flash drive by the following steps:

1. Open Rufus and insert the USB drive.
2. Select your USB drive under "Device".
3. Click **SELECT** and select the downloaded **WINPEBootable.vhd**.
4. Click **START.**
5. The drive now has the WINPE partition for booting to the WinPE environment for deployment
6. Using Windows **Disk Management** to format the ***Unallocated space*** of the USB Driver and name it **KioskImage**. This partition will be used for storing the Secure Image package.

Note:

The USB flash drive will now be formatted, so any data on the drive will be lost.

## [Step 3: Copy Secure Image to the flash drive](/docs/mdkiosk/v4.8.5/secure-image/creating-deployment-usb#step-3-copy-secure-image-to-the-flash-drive)

1. Input the flash drive to the computer.
2. Copy the file **install.wim** which downloaded from the Step 1 to the **KioskImage** partition.

*** WINPEBootable.vhd**

- MD5: 7F4C6B37D941D073039AF291834B78C0
- SHA-1: 1F359A80C412720EE8C6B5902329B7E3AB174548
- SHA-256: C4B770AB55755575BE3C1C97107C0E8CF5D3C261F7671177C861AF5A7770E9B7
