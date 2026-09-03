<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-manually-clean-up-the-md-core-engine-s-local-folder- -->

# How do I manually clean up the MD Core engine's local folder?

This article applies to all MetaDefender Core versions.

Warning:

We recommend taking these steps when MetaDefender Core is out of service, since deleting the engine folder will stop the current processing.

Internet access is required. In an air-gap environment, please prepare an offline engine package before applying this.

In some cases, MetaDefender Core keeps the engine folders after updating to a newer version, which can cause engine update issues and increase the disk space MetaDefender Core uses over time. Below is how to manually delete the engine folders.

1. Stop MetaDefender Core services
2. Browse and delete folders inside these installation locations (by default):

- C:\Progam Files\OPSWAT\MetaDefender Core\data\engines
- C:\Progam Files\OPSWAT\MetaDefender Core\data\resources
- C:\Progam Files\OPSWAT\MetaDefender Core\data\updates\av
- C:\Progam Files\OPSWAT\MetaDefender Core\data\updates\db\

3. Delete the file "C:\Program Files\OPSWAT\MetaDefender Core\data\updates\metadescriptor"
4. Start the MetaDefender Core services again and manually click the button “Update All” to update the engine

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/portal/support).
