<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/installation/installing-from-command-line -->

# Installing from Command Line

Summarize Page    Connect to Cursor Connect to VS Code
## [Available Parameters](/docs/mdmft/v3.11.4/installation/installing-from-command-line#available-parameters)

Info

All names are case-sensitive. Mistyped or non-existent parameters will be ignored.

| Name | Description |
| --- | --- |
| /silent | Set this parameter to run the installation without user interaction, displaying any graphical user interface, or progress indicators. |
| /passive | Set this parameter to run the installation without user interaction, and displaying a graphical user interface only with a progress bar. |
| /log <log_path> | Set this parameter to change where the install exe (bundle) will write log messages. |
| /uninstall | Set this parameter to perform an uninstallation of MetaDefender Managed File Transfer™. |
| InstallFolder=<folder_path> | Set where MetaDefender Managed File Transfer™ should be installed . Default is "C:\Program Files\OPSWAT\MetaDefender Managed File Transfer" |
| DbUninstallMode=<option> | Options:   - **Keep (default)**: Database will be left where it is. This option will also requires the *UninstallExportPath* to be specified. - **TryRemove**: If database server can be reached the databases and database files will be removed |
| UninstallExportPath=<folder_path> | Set to a folder where configuration files and the encryption secret can be exported to during an uninstall. Used together with the option: *DbUninstallMode=Keep.* |
| DbInstallMode=<option> | Options:   - **CreateNew (default**): Create new empty databases. Existing MetaDefender Managed File Transfer™ databases will prevent installation. - **CreateToExisting**: Attach to an existing database and upgrade it to be compatible with the current installer. This option might require *PathToSecret* to be specified. |
| PathToSecret=<file_path> | Set the path to the file containing the encryption secret to be used for existing databases. Default filename is *secret.bin.* If there was none specify the *ConfirmNoSecret* option instead Used together with the option: *DbInstallMode=CreateToExisting* |
| AllowDbDropCreate=<value> | Set this option to *yes* or *1* to allow the installer to remove the MetaDefender Managed File Transfer™ databases (if they exist) on the target database server. Used together with the option: DbInstallMode=CreateNew |
| ConfirmNoSecret=<value> | Set this option to *yes* or *1 to* confirm *PathToSecret* is intentionally not set, because it's not used  Used together with the option: *DbInstallMode=CreateToExisting* |
| DbType=<option> | Options:   - **Sql (default**): Use SQL authentication for the database connections. - **Win**: Use Windows authentication for the the database connections by running MetaDefender Managed File Transfer™ services under this account |
| DbServer=<server_address> | Set the SQL Server address to install MetaDefender Managed File Transfer™ databases to . A non-default port can be specified. For example: 192.168.0.100,10000 |
| DbDomain=<domain> | Set the domain to be used when connecting to SQL Server with Windows Authentication. |
| DbUser=<userame> | Set the username to be used when connecting to SQL Server. |
| DbPassword=<password> | Set the password to be used when connecting to SQL Server. |
| DbBackupSchedule=<option> | Set whether database backup should be performed to ensure recovery from errors during major changes. Make sure you [backup the database manually](/docs/mdmft/v3.11.4/installation/updating-metadefender-managed-file-transfer) if you choose *never* or *skip*  Options:   - always (default): Database backup is always created before major changes - never: Database backup is never performed. This setting is remembered after installation. - skip: Database backup is never performed. After a successful installation *Always* will be set. |

Info

Avoid using the `/silent` and `/passive` parameters together, as only the last one specified will be applied.

## [Examples](/docs/mdmft/v3.11.4/installation/installing-from-command-line#examples)

### [Example 1](/docs/mdmft/v3.11.4/installation/installing-from-command-line#example-1)

Install MetaDefender Managed File Transfer™ silently to an SQL Server using SQL Server Authentication

Info

The parameters *DbType=Sql* and *DbInstallMode=CreateNew* are omitted, because these are the default values for these parameters.

cmdPowershellCopymetadefender-managed-file-transfer.exe /silent DbServer="192.168.16.100" DbUser="sa" DbPassword="password"./metadefender-managed-file-transfer.exe /silent DbServer="192.168.16.100" DbUser="sa" DbPassword="password"
### [Example 2](/docs/mdmft/v3.11.4/installation/installing-from-command-line#example-2)

Install MetaDefender Managed File Transfer™ silently to an SQL Server using *Windows Authentication*.

Info

The Windows authentication user must have "Logon as a Service" rights.

The *DbInstallMode=CreateNew parameter is* omitted, because this is the default value.

cmdPowershellCopymetadefender-managed-file-transfer.exe /silent DbType=Win DbServer="192.168.16.100" DbDomain="domain" DbUser="sa" DbPassword="password"./metadefender-managed-file-transfer.exe /silent DbType=Win DbServer="192.168.16.100" DbDomain="domain" DbUser="sa" DbPassword="password"
## [Example 3](/docs/mdmft/v3.11.4/installation/installing-from-command-line#example-3)

Install product_name creating a new database and allowing the installer to recreate the databases if they existed.

Info

The *DbType=Sql parameter is* omitted, because this is the default value.

cmdPowershellCopymetadefender-managed-file-transfer.exe /silent DbServer="192.168.16.100" DbUser="sa" DbPassword="password" DbInstallMode=CreateNew AllowDbDropCreate=yes./metadefender-managed-file-transfer.exe /silent DbServer="192.168.16.100" DbUser="sa" DbPassword="password" DbInstallMode=CreateNew AllowDbDropCreate=yes
## [Example 4](/docs/mdmft/v3.11.4/installation/installing-from-command-line#example-4)

Install MetaDefender Managed File Transfer™ silently using an existing database that utilized an encryption secret

Info

The *DbType=Sql parameter is* omitted, because this is the default value.

cmdPowershellCopymetadefender-managed-file-transfer.exe /silent DbServer="192.168.16.100" DbUser="sa" DbPassword="password" DbInstallMode=CreateToExisting PathToSecret="C:\Path\To\secret.bin"./metadefender-managed-file-transfer.exe /silent DbServer="192.168.16.100" DbUser="sa" DbPassword="password" DbInstallMode=CreateNew AllowDbDropCreate=yes
## [Example 5](/docs/mdmft/v3.11.4/installation/installing-from-command-line#example-5)

Install MetaDefender Managed File Transfer™ and skip database backups when it would be required

Info

Parameters can be specified even without the /silent option

cmdPowershellCopymetadefender-managed-file-transfer.exe DbBackupSchedule=skip./metadefender-managed-file-transfer.exe DbBackupSchedule=skip
##
