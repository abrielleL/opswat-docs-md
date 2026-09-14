<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/maintenance/offline-update-for-metadefender-drive -->

# For MetaDefender Drive

## [Offline Engine Updates for MetaDefender Drive](/docs/mddrive/v4.4.2a/maintenance/offline-update-for-metadefender-drive#offline-engine-updates-for-metadefender-drive)

If you don't have access to MetaDefender Drive Toolkit, follow these steps to add the downloaded engine definition packages directly to MetaDefender Drive:

1. Download the MetaDefender Drive engine package files from Update Downloader.
2. Open the NTFS partition MetaDefender Drive and extract the *.zip* files into the */update/defs/* folder. Make sure to place each *engine.yml* and *engine.zip* file is in the root of */update/defs/*.
3. Delete any files with extensions other than *.zip* or *.yml*.
4. Restart your system and boot from the MetaDefender Drive to install the engine updates.

Engine Updates

After following the steps above, the engine definitions will **only be copied** to MetaDefender Drive. The engines will be fully installed and initiated with the next boot.

__

.
