<!-- source: https://www.opswat.com/docs/ocm/configuration/update-settings-core-modules -->

# MetaDefender Core modules

OPSWAT Central Management provides administrators the ability to centrally manage modules (anti-malware engines and their database) for managed OPSWAT product instances. Currently, this feature supports MetaDefender Core, MetaDefender Kiosk Linux, and MetaDefender Drive.

The Modules are accessible under **Inventory > MetaDefender Core Modules**. This list will be referred to as the module update pool in this article.

Update settings are accessible under **Settings > Server Configuration > Update Settings** tab, then select **Module Update** section.

There are 3 update modes available, determining how OPSWAT Central Management can acquire new module update packages:

- Internet
- Folder
- Manual

However, administrators can always ad-hoc update modules by manually upload them to OCM via management console regardless of the current update mode.

### [Internet](/docs/ocm/configuration/update-settings-core-modules#internet)

In Internet mode, the updater will automatically download the module updates based on the managed product instances from the OPSWAT update server. These instances should automatically request the latest updates from OPSWAT Central Management.

**Update Processing Schedule** determines when the update process should be carried out. The updater can also be configured to send an email alert if update failures persist for a certain period of time without any successes.

**Update Now:**

To trigger an update process immediately, please select **Update Now** in **Inventory > MetaDefender Core Modules**.

**Note:**

- **Update Now** only triggers the update download process. Product instances have their own scheduler settings to get update from OPSWAT Central Management.
- To have product instances immediately get the updates from OPSWAT Central Management, in the Inventory interface for the corresponding product type, select the instances that should get the update and select **Update Engine** from the **ACTIONS** dropdown menu.

### [Folder](/docs/ocm/configuration/update-settings-core-modules#folder)

In Folder mode, the OPSWAT Central Management continuously watches the configured folder and import the module updates if available from the specified folder in **Location** to the module update pool.

- **Delete files after import**: If selected, the files of imported modules are deleted from the folder set in **Location** after the import process finishes**.**

Info

From 7.29.0, UNC path format is supported when selecting a folder.

#### [Pushing modules updates to MetaDefender Core instances](/docs/ocm/configuration/update-settings-core-modules#pushing-modules-updates-to-metadefender-core-instances)

For MetaDefender Core only, OPSWAT Central Management provides a scheduled function to automatically push module updates to the managed MetaDefender Core instances.

- PUSH NOW immediately pushes the available module updates to the managed MetaDefender Core instances.
- The **Update Pause** setting allows users to set up rules that determine when the push process should not be performed.

### [Manual](/docs/ocm/configuration/update-settings-core-modules#manual)

Manual mode will disable all automatic update processes for both the module update pool and the managed MetaDefender Core instances. The administrators must manually upload the update files in the **Inventory > MetaDefender Core Modules** menu.

For MetaDefender Core, if update files should be manually uploaded but OPSWAT Central Management must still automatically deliver them to the managed MetaDefender Core instances, please use **Folder** mode.
