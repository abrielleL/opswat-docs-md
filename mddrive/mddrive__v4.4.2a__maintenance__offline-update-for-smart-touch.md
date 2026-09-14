<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/maintenance/offline-update-for-smart-touch -->

# For Smart Touch

This article explains how to perform an **offline update** for MetaDefender Drive Smart Touch using a external USB storage device.

Engine Updates

For engines updates please follow the steps in <https://www.opswat.com/docs/mddrive/maintenance/for-metadefender-drive>

#### [Before you begin, prepare the following:](/docs/mddrive/v4.4.2a/maintenance/offline-update-for-smart-touch#before-you-begin-prepare-the-following)

- A USB storage device formatted (**NOT ENCRYPTED**] as NTFS or FAT32 with at least 500MB space free
- Download the Debian packag `.deb` package and its YAML descriptor`.yml` file.from published download URLs in My OPSWAT.

- Create the `/updates` folder on the USB drive.
- Copy the update files into the `/updates` folder.
- Safely eject the USB storage from your computer.

#### [Perform the offline update](/docs/mddrive/v4.4.2a/maintenance/offline-update-for-smart-touch#perform-the-offline-update)

- Make sure Smart Touch is powered off. If Smart Touch is currently running, shut it down gracefully from the UI or power button before proceeding.
- Insert the prepared USB storage into the USB-C port of the Smart Touch device
- Power on Smart Touch, enter PIN code
- After Smart Touch starts it will

  - automatically detect the `/updates` folder on the USB storage
  - automatically pick up the offline update package (`.deb` + `.yml`) and begin the update process.
- The update will proceed without requiring user interaction until finish. Do not power off Smart Touch or remove the USB storage during this time.
