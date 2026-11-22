<!-- source: https://www.opswat.com/docs/mdmft/v3.11.6/installation/uninstalling-metadefender-managed-file-transfer -->

# Uninstalling MetaDefender Managed File Transfer

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## Uninstalling Using the Install Wizard

1. Go to Start → Control Panel → Uninstall a program
2. Select whether to do a complete uninstallation. If you select no, a normal uninstallation will take place

#### Keeping the database

When you choose this option the installer will preserve uploaded files stored in the installation directory, settings and the database for future installations.

This uninstallation mode is suitable for:

- Preserving database for compliance reasons, or when it's unclear if MetaDefender Managed File Transfer™ will be used in the future
- Repair installation
- Removing an MFT node from an MFT cluster

Warning

Exporting settings is highly encouraged, otherwise reconnecting a new installation to the database may not be possible.

Uninstallation with keeping the database

Selecting a config backup folder for uninstall

#### Removing the database

When you choose this option the installer will remove all data created by MetaDefender Managed File Transfer™ including the database and uploaded files stored in the installation directory.

Warning

If the database server couldn't be reached at the time of uninstallation, it needs to be manually removed.

Uninstallation with database removal

## Uninstall From Command Line

For a complete list of command line parameters see [Installing from Command Line](/installation/installing-from-command-line)

### Keeping the database

cmdPowershellCopymetadefender-managed-file-transfer.exe /silent /uninstall DbUninstallMode=Keep UninstallExportPath=C:\MFT\ExportPath./metadefender-managed-file-transfer.exe /silent /uninstall DbUninstallMode=Keep UninstallExportPath=C:\MFT\ExportPath
### Complete uninstallation

cmdPowershellCopymetadefender-managed-file-transfer.exe /silent /uninstall DbUninstallMode=TryRemove./metadefender-managed-file-transfer.exe /silent /uninstall DbUninstallMode=TryRemove
