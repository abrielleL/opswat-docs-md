<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/quarantine-manager-command-line-interface -->

# Quarantine Manager Command Line Interface

View as Markdown Ask ChatGPT about this page Ask Claude about this page

You can use the MetaDefender Kiosk Quarantine Manager CLI (omsQMCLI.exe) to browse and manage quarantines. The size of the MetaDefender Kiosk quarantine is limited to 100 MB.

Warning

The MetaDefender Kiosk Quarantine Manager CLI must be executed with administrator privilege.

## [Help](/docs/mdkiosk/v4.8.6/advanced-deployment/quarantine-manager-command-line-interface#help)

Syntax: help

This function prints the available command line options.

## [Quarantine file](/docs/mdkiosk/v4.8.6/advanced-deployment/quarantine-manager-command-line-interface#quarantine-file)

Syntax: quarantine <file path> <threat name>

This command adds the specified file to the quarantine database under the given threat name.

## [Delete file](/docs/mdkiosk/v4.8.6/advanced-deployment/quarantine-manager-command-line-interface#delete-file)

Syntax: delete <file path>

This command permanently deletes a file which has been quarantined.

**Note:** Disk space will be reused without returning to the OS.

## [Restore file](/docs/mdkiosk/v4.8.6/advanced-deployment/quarantine-manager-command-line-interface#restore-file)

Syntax: restore <quarantine ID> [target directory]

This command restores a quarantined file back to the original location. If a file already exists with the same name, a number will be appended to the file name. You can override the location the file is to be restored to by specifying the target directory.

## [Browse quarantine](/docs/mdkiosk/v4.8.6/advanced-deployment/quarantine-manager-command-line-interface#browse-quarantine)

Syntax: list [<minimum number of quarantines to display>]

This command lists quarantined files.
