<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/troubleshooting/how-to-create-support-package -->

# Creating Support Packages

Summarize Page    Connect to Cursor Connect to VS Code

To ensure optimal support from OPSWAT®, you can create a support package from the MetaDefender Managed File Transfer™ user interface. This package includes essential information about the operating system and OPSWAT® software installed on the machine.

### [Generating the Package via Command Line Interface (CLI)](/docs/mdmft/v3.11.4/troubleshooting/how-to-create-support-package#generating-the-package-via-command-line-interface-cli)

You can also generate the support package using the GenerateSupportFiles command line tool located in the product's installation directory. Default path: "*C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\GenerateSupportFiles.exe."*

Refer to the examples below for usage instructions.

Info

The CLI tool can be run even if MetaDefender Managed File Transfer™ services or the database server are not running. However, without the database server, the support package will lack key information.

#### [Command Line Parameters](/docs/mdmft/v3.11.4/troubleshooting/how-to-create-support-package#command-line-parameters)

| Parameter | Description |
| --- | --- |
| --OutputFolder | (Required) Move the support package to this folder after creation |
| --IncludeDbDump | Include a backup of the database in the support package. Including a database dump can significantly increase the size of the resulting archive |
| --IncludeTelemetry | Include telemetry data in the support package |
| --Password | Create a password-protected support package with this password |

#### [Examples](/docs/mdmft/v3.11.4/troubleshooting/how-to-create-support-package#examples)

**Example 1: Create a support package to a specified folder**

cmdCopy"C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\GenerateSupportFiles.exe" --OutputFolder C:\Temp

*Output*

Generating support package. Please wait...
Support archive created at C:\Temp\metadefender-managed-file-transfer_20250523_102520_UTC02.00.zip
Press ENTER to exit...

**Example 2: Create a support package with Telemetry**

cmdCopy"C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\GenerateSupportFiles.exe" --OutputFolder C:\Temp --IncludeTelemetry

**Example 3: Create a support package with DbBackup**

PowershellCopy"C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\GenerateSupportFiles.exe" --OutputFolder C:\Temp --IncludeDbBackup
### [Generating the Package Through the User Interface (UI)](/docs/mdmft/v3.11.4/troubleshooting/how-to-create-support-package#generating-the-package-through-the-user-interface-ui)

Administrator privileges are required.

To generate a support package from the web interface:

1. In the top-right corner of the screen, open the User Info menu.

2. Click "Contact Support"
3. Enter a password to-protect the archive
4. (Optional) Check "Include database dump" if you want to include a database dump. Note: including a database dump can significantly increase the size of the package.
5. Click "Export packages" to download the package

### [Content of the Support Package](/docs/mdmft/v3.11.4/troubleshooting/how-to-create-support-package#content-of-the-support-package)

The support package contains the following elements:

- Config

  - MetaDefender Managed File Transfer™ service configuration files
  - nginx configuration files
- DbDebug

  - Database statistics
- Environment

  - System information
  - Network information
- EventLog

  - Windows event logs (errors only)
- Localization

  - Default localizations
  - Custom localizations
- Logs

  - MetaDefender Managed File Transfer™ service log files
  - MetaDefender Managed File Transfer™ tool log files
- MsiInstallLog

  - MSI installation logs for MetaDefender Managed File Transfer™
  - MSI installation logs for installed dependencies
- InstallLog

  - MetaDefender Managed File Transfer™ install log files
- Registry

  - Registry keys relevant for product_name
- Services

  - File version info for MetaDefender Managed File Transfer™ files
- Storage

  - Local MetaDefender Managed File Transfer™ file storage metrics
- Telemetry (Optional)

  - Telemetry data
- DbBackup (Optional)

  - Database backup
