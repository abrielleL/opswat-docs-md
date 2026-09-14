<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/advanced-usages/update-engines-in-airgapped-environment -->

# Update Engines In Air-Gapped Environment

In addition to MetaDefender Drive Toolkit as a tool to manage provision MetaDefender Drive and with features to updates Drives' engines. However, if in your network there is an OPSWAT Update Downloader set up and running, you can take the advantages of it to update Drive's engines in isolated environment.

## [Offline Download and Install Update Downloader for Air-gapped environment](/docs/mddrive/v4.4.2a/advanced-usages/update-engines-in-airgapped-environment#offline-download-and-install-update-downloader-for-air-gapped-environment)

- This guidance is written with an assumption that in your organization's network there is already an Update Downloader instance up and running. If it is not a case, please to: <https://docs.opswat.com/mddownloader>
- Once installed please follow the instructions in <https://docs.opswat.com/mddownloader/operating/products#add-a-new-product-on-update-downloader> to add new product (in our case is MetaDefender Drive)
- Then follow instructions in <https://docs.opswat.com/mddownloader/operating/download-all-update-packages> to download the updated **engines package**

## [Offline Update Engines for MetaDefender Drive Toolkit](/docs/mddrive/v4.4.2a/advanced-usages/update-engines-in-airgapped-environment#offline-update-engines-for-metadefender-drive-toolkit)

- Navigate to the folder where you extract and run MetaDefender Drive Toolkit.
- There you'll find a sub folder names "engines"
- Extract the **engines package** you get from Update Downloader into this "engines" folder
- Now your MetaDefender Drive Toolkit is ready to hydrate your Drives with new engines

## [Offline Update Engines for MetaDefender Drive](/docs/mddrive/v4.4.2a/advanced-usages/update-engines-in-airgapped-environment#offline-update-engines-for-metadefender-drive)

This to be done only when you don't have MetaDefender Drive Toolkit and want to keep the engines of MetaDefender Drive up to date

- Download the appropriate .zip from Update Downloader for MetaDefender Drive
- Extract this .zip into /update/defs/ folder on the NTFS partition MetaDefender Drive. Make sure to place each engine.yml and engine.zip file is in the root of /update/defs/. Delete any files that are not .zip or .yml

NOTE

After the following the steps above, the engines will **only be copied** successfully to your MetaDefender Drives. They will be installed to your MetaDefender Drive with the next boot. Until the next boot, your Drive won't be ready to perform any scans until the downloaded engines are installed successfully.
