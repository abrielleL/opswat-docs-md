<!-- source: https://www.opswat.com/docs/ocm/configuration/update-client-oesis-vul -->

# MetaDefender Endpoint, OESIS, and the vulnerability database

OPSWAT Central Management provides administrators with the ability to update its MetaDefender Endpoint installers, OESIS packages, and vulnerability database, which are all components of the Device Management feature suite. The update interface is located at **Server Configuration > Update Settings > AGENT UPDATE.**

There are 3 options available for update sources:

- **Internet:** OPSWAT Central Management automatically downloads the latest updates from the OPSWAT server once they are available.
- **Folder:** OPSWAT Central Management automatically searches for updates in a folder designated by the administrators. The update files must be manually copied to this folder.
- **Manual:** Administrators manually upload the update files through the OPSWAT Central Management’s interface.

## [Internet:](/docs/ocm/configuration/update-client-oesis-vul#internet)

OPSWAT Central Management automatically downloads the latest updates from the OPSWAT server once they are available.

- **Update Processing Schedule**: The frequency of the automatic update process.
- **Update Pause (Optional):** Select a time period when updates should not be performed.

## [Folder:](/docs/ocm/configuration/update-client-oesis-vul#folder)

OPSWAT Central Management automatically searches for updates in a folder designated by the administrators. The update files must be manually copied to this folder.

- **Pick up updates from:** The folder that OPSWAT Central Management should search for the update files in.

  - **Delete files after import**: Delete the update files after the update process completes.
- **Update Schedule**: The frequency of the automatic update process.
- **Update Now:** Immediately trigger the update process

Info

From 7.29.0, UNC path format is supported when selecting a folder.

## [Manual:](/docs/ocm/configuration/update-client-oesis-vul#manual)

Administrators manually upload the update files through the OPSWAT Central Management’s interface.

The below guidelines describe how to manually update a component.

1. Select the **Upload** icon to begin the process.
2. Select the update files (usually 2 files: one .zip and one .yml) in the file browser.

3. Once the upload completes, select **Save** at the top of the page to complete the update process.
