<!-- source: https://www.opswat.com/docs/ocm/installation/on-windows -->

# On Windows

## [Using the installation wizard](/docs/ocm/installation/on-windows#using-the-installation-wizard)

The installation wizard is available for Windows installations only (.msi file).

Please follow the guidelines below:

1/ Accept the license agreement.

2/ Configure the ports that OPSWAT Central Management should use.

3/ Select the installation folder. OPSWAT Central Management will be installed into the Central folder inside the chosen folder.

Location of configuration, log and database data files

Please note that OPSWAT Central Management's configuration, log and database data files are still store in <System Drive>\ProgramData\OPSWAT\Central (default C:\ProgramData\OPSWAT\Central)

The location of these files currently cannot be changed.

4/ Confirm the installation.

5/ Installation in progress. This process may take some time.

6/ Click **Finish** to complete the installation. You can check **Launch OPSWAT Central Management** to launch the web management console immediately. If this is the first time you install OPSWAT Central Management, the [configuration wizard](/docs/ocm/quick-start/configuration-wizard) will walk you through the initial setup.

7/ After a successful installation, OPSWAT Central Management tray icon should appear and show the status of the OPSWAT Central Management server.

## [Using a command line interface](/docs/ocm/installation/on-windows#using-a-command-line-interface)

On Windows systems, it is possible to silently install the product by executing the corresponding .msi file from the command-line interface.

From the command-line interface, execute the command:

msiexec /i <.msi file> /quiet

For example:

msiexec /i C:\OPSWATCentralManagement.msi /quiet

Info

Administrator permission is required for this command.

Alternatively, to start a GUI-assisted installation process as in [Using the installation wizard](/docs/ocm/installation/on-windows#using-the-installation-wizard), execute the command:

msiexec /i <.msi file>

For example:

msiexec /i C:\OPSWATCentralManagement.msi

Windows Installer provides specific arguments for the installation/uninstallation process using a .msi file.

| Argument | Description |
| --- | --- |
| /i | Install |
| /x | Uninstall |
| /quiet | Quiet display option. The installer runs without displaying a user interface. |
| /l*v <output file path> | Log the install/uninstall process and output it to a specific filepath, for example, /l*v C:\log\log.txt |
