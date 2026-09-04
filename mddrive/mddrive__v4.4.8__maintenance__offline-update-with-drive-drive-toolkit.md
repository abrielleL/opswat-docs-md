<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/maintenance/offline-update-with-drive-drive-toolkit -->

# Update Engines and Drive Image Offline Using Drive Toolkit

This article explains how to use MetaDefender Drive Toolkit in an isolated environment to update the scanning engines and the MetaDefender Drive image. Both procedures use packages that were downloaded on an internet-connected system and transferred into the isolated environment.

Before you begin, make sure you have downloaded the MetaDefender Drive engine packages using MetaDefender Update Downloader. See [Update MetaDefender Drive Offline](https://www.opswat.com/docs/mddrive/maintenance/update-engines-in-airgap) for setup instructions.

## [Update the Scanning Engines Offline](/docs/mddrive/v4.4.8/maintenance/offline-update-with-drive-drive-toolkit#update-the-scanning-engines-offline)

To update the scanning engines using MetaDefender Drive Toolkit in an isolated environment:

1. Download the MetaDefender Drive engine package files from Update Downloader.
2. Transfer the packages to the system running MetaDefender Drive Toolkit.
3. Open the MetaDefender Drive Toolkit folder and locate the *engines* subfolder.
4. Copy and extract the engine packages into the *engines* folder.

The updated engine definitions will be applied to MetaDefender Drive the next time you run an update from Drive Toolkit.

## [Update the MetaDefender Drive Image Offline](/docs/mddrive/v4.4.8/maintenance/offline-update-with-drive-drive-toolkit#update-the-metadefender-drive-image-offline)

To update the MetaDefender Drive version using Drive Toolkit in an isolated environment:

1. On a system with internet access, download the image and its YAML descriptor from the following URLs:

- <https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/mdd-dd.tgz>
- <https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/mdd-dd.yml>

2. Extract the *.tgz* file. After extracting, you will see the image file **mdd-pkg.dd**.
3. Transfer **mdd-pkg.dd** and **mdd-dd.yml** to the system running MetaDefender Drive Toolkit.
4. Open the MetaDefender Drive Toolkit folder and locate the *current* sub-folder, then delete all existing image files in this sub-folder.
5. Copy **mdd-pkg.dd**, **mdd-dd.yml** and **partition-layout-info** into the *current* sub-folder.

After copying, the folder structure should look like this:
