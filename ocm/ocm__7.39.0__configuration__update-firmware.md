<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/update-firmware -->

# Firmware for MetaDefender Products

OPSWAT Central Management provides administrators the ability to centrally manage firmware updates for managed instances. This feature currently supports only MetaDefender Kiosk Linux and MetaDefender Drive.

OPSWAT Central Management serves as an update server and hosts firmware update packages. Managed MetaDefender Kiosk Linux and MetaDefender Drive instances automatically check for the latest packages hosted by OPSWAT Central Management and perform upgrades if available.

Update settings are accessible under **Settings > Server Configuration > Update Settings** tab**,** then select the **KIOSK LINUX PACKAGE UPDATE** and **METADEFENDER DRIVE PACKAGE UPDATE** section.

There are 3 update modes available, determining how OPSWAT Central Management can acquire new update packages:

- **Internet:** OPSWAT Central Management automatically downloads updates from the OPSWAT servers once they are available.
- **Folder:** OPSWAT Central Management automatically searches for updates in a designated folder. Update packages must be manually copied to that folder.
- **Manual:** Administrators manually upload an update package to the OPSWAT Central Management. This mode is set by default.

### [Internet](/docs/ocm/7.39.0/configuration/update-firmware#internet)

In Internet mode, OPSWAT Central Management automatically checks for updates from the OPSWAT servers. The frequency of this automatic check is configured in the setting "**Update Processing Schedule"**.

As of OPSWAT Central Management version 7.19.0, release notes for firmware updates are available for MetaDefender Drive. They are viewable in the OPSWAT Central Management console at **<Server URL>/console/drive/update/release-note.html**

- **Update Processing Schedule**: The frequency of the automatic update process.

### [Folder](/docs/ocm/7.39.0/configuration/update-firmware#folder)

In Folder mode, OPSWAT Central Management searches for updates from a folder configured in the setting **Pick up updates from.** OPSWAT Central Management watches this folder for modification. Whenever new firmware update files for the supported product types are added to this folder, OPSWAT Central Management picks them up, performs validation and finally updates the firmware packages hosted for the corresponding product types.

Administrators can set OPSWAT Central Management to automatically delete the update files in the selected folder after the update process completes successfully via the setting **Delete files after import.**

- **Pick up updates from:** The folder that OPSWAT Central Management should search for the update files in.

  - **Delete files after import**: Delete the update files after the update process completes.

Info

From 7.29.0, UNC path format is supported when selecting a folder.

### [Manual](/docs/ocm/7.39.0/configuration/update-firmware#manual)

By choosing the Manual mode, administrators need to update a new firmware package manually to OCM whenever there is a new version available.

Here are steps to upload a new firmware package to OCM:

1. Select the **Upload** icon.
2. Select the update files (usually 2 files: one archive file and one .yml) in the file browser, then click Open
3. Once the files are uploaded successfully, click **Save** at the top of the page and confirm your PIN to complete the update process.
