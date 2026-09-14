<!-- source: https://www.opswat.com/docs/ocm/7.39.0/integrations/metadefender-core-module -->

# MetaDefender Core Module

Administrators can leverage OPSWAT Central Management to centralize management of modules for MetaDefender instances . OPSWAT Central Management downloads, stores, and distributes update packages to connected MetaDefender Core, Drive and MetaDefender Kiosk Linux instances.

OPSWAT Central Management's pool of update packages for MetaDefender Core modules is located at **Inventory** > **MetaDefender Core Modules** .

Info

When updating its own module pool, OPSWAT Central Management only updates the modules registered with the product instances connected at the time that the update process triggers.

The module update pool has 3 update modes: Internet mode, Folder mode, and Manual mode. Please refer to [MetaDefender Core module update](/docs/ocm/7.39.0/configuration/update-settings) for more detail on how to configure the module updater.

Administrators can determine what modules should be updated by the update process by using the **ENABLED** toggle-button.

Administrators can also update individual modules by manually uploading the update packages. Select **UPLOAD** **PACKAGES** to bring up the module upload dialog then choose the update packages (.zip format) along with their corresponding descriptor files (.yml format) and select **UPLOAD.** Please note that this function is not available in Internet mode.

In Internet mode, administrators can select **UPDATE NOW** to manually trigger an update for the module update pool.

In Folder mode, update packages placed in the designated folder will be automatically added to the module update pool.

For both Internet and Folder modes, administrators can set a schedule for the update process at **Settings > Update Settings > Module Update.** Please refer to [MetaDefender Core module update](/docs/ocm/7.39.0/configuration/update-settings) for more detail on how to configure the schedule.

Once the update process complete, the update packages are ready for distribution to product instances.

For more information on how updates are distributed to MetaDefender Core instances, please refer to [Delivering module updates to MetaDefender Core instances](/docs/ocm/7.39.0/integrations/metadefender-core-module/delivering-module-updates-to-metadefender-core-instances).

Warning

To utilize the module updater, the MetaDefender Core instances must have their **Source** setting set to **Internet** in the **Update Settings** menu in the MetaDefender Core management console.

Warning

Modules that have been unused for more than 7 days (such as having been removed from the managed product instances) will be removed from OPSWAT Central Management.
