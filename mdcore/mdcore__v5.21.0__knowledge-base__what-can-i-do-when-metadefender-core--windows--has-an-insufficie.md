<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/what-can-i-do-when-metadefender-core--windows--has-an-insufficie -->

# What can I do when MetaDefender Core (Windows) has an insufficient disk space error?

This article applies to all MetaDefender Core (Windows) versions

While using MetaDefender Core, you may occasionally encounter a **full disk space issue**, which can cause the Core service to stop functioning. MetaDefender Core includes an **Auto Retention** mechanism designed to automatically remove older entries from the database to free up space.

However, this process works in two steps:

- **Old entries are marked for deletion** based on the configured retention policy.
- **The actual deletion is triggered automatically** at a later time.

In some cases, the disk may become full **before** the deletion process is initiated. Since the deletion also requires a minimal amount of free space to execute, this can prevent the cleanup from starting.

To manually free up disk space and allow MetaDefender Core to resume normal operation, consider the following steps to remove unnecessary files or data:

1. **Manually delete/move the log folders:**

Warning:

Recommended to stop the MetaDefender Core’s services before proceeding with these steps

This method can help you free up disk space and minimize disruption to the MetaDefender Core server's operation. You can move/delete all the log folders/files located inside these locations:

- `C:\Program Files\OPSWAT\MetaDefender Core\data\logs`, **except the file “core.log”**
- `C:\Program Files\OPSWAT\MetaDefender Core\data\pg_data\log`

Info:

Moving is recommended to keep the old logs for future needs.

2. **Manually delete/move the engine folders:**

Follow this article for detailed instructions: [How do I manually clean up the MD Core engine's local folder?](/docs/mdcore/v5.21.0/knowledge-base/how-do-i-manually-clean-up-the-md-core-engine-s-local-folder-)

Warning:

Deleting MetaDefender Core Engines will require an engine update after that.

3. **Using the Windows Disk Cleanup tool:**

This method will not interfere with the MetaDefender Core installation files, but the Windows unnecessary files.

Info:

Only apply this when your install location is on the C drive.

- From Run, type `cleanmgr` then enter.
- Choose the C drive on the next pop-up.

- From the Disk Cleanup, choose Cleanup system files, confirm the C drive again.
- Select as much as possible from the list. Recommended to choose `Windows Update Cleanup`, `Previous Windows installation(s)`, `Temporary files`

Choose OK in the end to start the Windows Disk Cleanup.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/portal/support).
