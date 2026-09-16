<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/does-metadefender-core-store-original-files- -->

# Does MetaDefender Core store original files?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

MetaDefender Core does not store original files permanently.

Files are temporarily stored while waiting in the queue for processing. During processing, they are kept in a designated folder and handled by MetaDefender Core and its engines. Once processing is complete, the files are automatically removed.

### [Default Temporary Folder Locations:](/docs/mdcore/v5.22.0/knowledge-base/does-metadefender-core-store-original-files-#default-temporary-folder-locations)

- **Windows: <installation directory>\data\resources**
- **Linux:** `/var/tmp/ometascan/resources/` (MetaDefender Core creates a subfolder named `ometascan` and `ometascan/resources` in this directory.)

To change the temporary folder location, please refer to this article for more information [How can the Temp folder be changed?](/docs/mdcore/v5.22.0/knowledge-base/how-can-the-temp-folder-be-changed-)

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
