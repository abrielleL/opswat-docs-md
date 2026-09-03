<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line- -->

# How to Remove Engines from MetaDefender Core using command line?

If you encounter issues with specific scan engines in MetaDefender Core, you may need to remove them temporarily or permanently. This article provides instructions for removing scan engines from MetaDefender Core using built-in tools for both Windows and Linux systems.

## [Prerequisites](/docs/mdcore/v5.21.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line-#prerequisites)

Administrator access to the MetaDefender Core system.

- MetaDefender Core installed on Windows or Linux.
- Command-line access (Command Prompt for Windows, Terminal for Linux).

## [Removing a Scan Engine on Windows](/docs/mdcore/v5.21.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line-#removing-a-scan-engine-on-windows)

### [Steps:](/docs/mdcore/v5.21.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line-#steps)

Open Command Prompt as Administrator.

1. Navigate to the MetaDefender Core installation directory:

BashCopycd "C:\Program Files\OPSWAT\MetaDefender Core"

2. Run the following command to remove the engines:

BashCopyometascan-engine-remove.exe

3. Verify that all the engines has been removed by checking the MetaDefender Core management interface or logs.
4. Restart MetaDefender Core service to apply the changes.

## [Removing a Scan Engine on Linux](/docs/mdcore/v5.21.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line-#removing-a-scan-engine-on-linux)

### [Steps:](/docs/mdcore/v5.21.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line-#steps)

Open a Terminal session.

1. Run the following command to remove the engines:

BashCopysudo /usr/bin/ometascan-engine-remove

2. Verify that all the engines has been removed by checking the MetaDefender Core management interface or logs.
3. Restart MetaDefender Core to apply the changes:

BashCopysudo systemctl restart ometascanSupport:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
