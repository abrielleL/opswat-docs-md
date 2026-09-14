<!-- source: https://www.opswat.com/docs/mddownloader/knowledge-base/how-to-remove-an-engine-that-is-stuck-on-an-old-database-or-engi -->

# How to remove an engine that is stuck on an old database or engine version for MetaDefender Update Downloader?

Please following the steps below:

1. Navigate to Update Downloader located at [http://localhost:8028](http://localhost:8028/#/public/login)
2. Navigate to “Inventory” > “Engines” > click the trash can to the right of the engine [if able]
3. Stop the Update Downloader Service under “Services” of the OS
4. Open up the File explorer and remove the specific engine[s] package[s] from the following locations `C:\Program Files\OPSWAT\Metadefender Update Downloader\data\updates\av` `C:\Program Files\OPSWAT\Metadefender Update Downloader\data\updates\db`
5. Remove the specific engine[s] package[s] from `C:\Program Files\OPSWAT\Metadefender Update Downloader\data\update_packages`
6. Start the Update Downloader service and navigate to “Inventory” > “Engines” to hit “Update All”
7. If the engine still does not download the latest, you can rename the folder [update_packages] `C:\Program Files\OPSWAT\Metadefender Update Downloader\data\update_packages` then when getting new updates, a new folder will be created [update_packages], redownloading all the engines from our update server.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
