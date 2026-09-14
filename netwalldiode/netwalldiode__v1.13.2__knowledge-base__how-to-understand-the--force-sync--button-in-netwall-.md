<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/knowledge-base/how-to-understand-the--force-sync--button-in-netwall- -->

# How to Understand the "Force Sync" Button in NetWall?

This article applies to all Blue sides of Optical Diodes, MetaDefender Security Gateway (USG and BSG) and Transfer Guards.

The BLUE side maintains a record of previously transferred files. This prevents duplicate transmissions and ensures efficient use of bandwidth and resources. Once a file is sent from BLUE to RED, BLUE considers that file “sent” and will not re-send it unless certain actions are taken.

Importantly, the BLUE node has no awareness of file deletions on the RED side, as RED cannot communicate status or state changes back to BLUE. Therefore, if a file is removed from RED, BLUE has no way of knowing and will not attempt to re-send it.

**How does Force Sync work?**

When the users click Force Sync, it clears the internal record of previously sent files. This forces the system to treat all files in the folder as new and reprocess them for transfer.

Note that the Force Sync button becomes visible when the 'Delete Files on Share after Transfer' option is disabled.

**Not using Force Sync when transferring the same file?**

If the users prefer not to use Force Sync but still want the file to be re-sent, they can simply rename the file before uploading it again. A new filename shall prompt BLUE to process and send the file as a new item.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
