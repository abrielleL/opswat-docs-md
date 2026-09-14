<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/maintenance/offline-update-for-metadefender-drive-toolkit -->

# For MetaDefender Drive Toolkit

## [Offline Engines Update for MetaDefender Drive Toolkit](/docs/mddrive/v4.4.2a/maintenance/offline-update-for-metadefender-drive-toolkit#offline-engines-update-for-metadefender-drive-toolkit)

To update the scanning engines using a MetaDefender Drive Toolkit in an isolated environment, you can download the engine definitions using OPSWAT Update Downloader and add them to the MetaDefender Drive Toolkit:

1. Download the MetaDefender Drive engine package files from Update Downloader.
2. Open the MetaDefender Drive Toolkit folder and locate the *engines* subfolder.
3. Copy and extract the engine packages downloaded from the Update Downloader into the *engines* folder.
4. Restart your system and boot from the MetaDefender Drive to install the engine updates.

## [Offline MetaDefender Drive Version Update for MetaDefender Drive Toolkit](/docs/mddrive/v4.4.2a/maintenance/offline-update-for-metadefender-drive-toolkit#offline-metadefender-drive-version-update-for-metadefender-drive-toolkit)

**Step 1:** Download USB/LCD image and yml from URLs

- <https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/mdd-dd.tgz>
- [https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/mdd-dd.ym](https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/mdd-dd.yml)

**Step 2:** Extract file ***.tgz** of corresponding image, then you will see **mdd-pkg.dd**

**Step 3:** Open MetaDefender Drive Toolkit folder and locate the ***current*** subfolder, then clean up all existed image in this subfolder

**Step 4:** Copy **mdd-pkg.dd** and its **mdd-dd.yml** that downloaded ad extracted from step 1,2 to *current* subfolder for **USB image only** and *nvme* subfolder for **LCD image only**

- After extracting, the folder structure should be looking like this

******Note:*** *please make sure mdd-dd.yml and mdd-pkg.dd belongs to USB or LCD*
