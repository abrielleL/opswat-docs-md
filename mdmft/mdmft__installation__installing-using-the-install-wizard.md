<!-- source: https://www.opswat.com/docs/mdmft/installation/installing-using-the-install-wizard -->

# Installing Using the Install Wizard

Summarize Page    Connect to Cursor Connect to VS Code
## [Normal Installation](/docs/mdmft/installation/installing-using-the-install-wizard#normal-installation)

Follow these steps to install MetaDefender Managed File Transfer™ using the install wizard:

1. Launch the setup: double-click on the "metadefender-managed-file-transfer.exe" file.
2. License agreement: read the License Agreement and select **"**I agree to the license terms and conditions**"** if you accept it.

3. Choose installation directory: click "Browse" to locate the desired directory and then click "OK." To install in the default directory, simply click "Install."
4. [Dependencies](/docs/mdmft/installation/dependencies) will be installed at this stage.
5. Select whether you want to do a clean installation, and click "Next"

6. Select database: on the database selection screen, choose your desired deployment model. An already installed and configured SQL Server is expected (matching the authentication mode selected) .

Info

If you are updating MetaDefender Managed File Transfer™, this dialog will be skipped, and the existing settings will be used.

Note: During an upgrade SQL Server Express LocalDb is still accepted.

Warning

Starting from version 3.9.2:

- SQL Server Express LocalDb is not supported for new installations.
- LocalDb is not bundled or installed during installation, and if LocalDb is manually uninstalled, existing LocalDb based installations will not be able to upgrade.

**Correction**: In the screenshot above "built-in" SQL Server Express is incorrectly mentioned. The installer doesn't bundle any version of SQL Server. If the SQL Server is an Express edition, the size limitation still applies.

7. If connecting to a Microsoft SQL Server database, enter the connection credentials in the window below.

Info

If you are updating MetaDefender Managed File Transfer™, this dialog will be skipped.

Info

If the server runs on a non-default port (not 1433), enter the specific port number in the "Port" field. If left blank, the default port will be used. Alternatively, the port number can be appended to the Server name in the format `<hostname>,<port>`.

Info

For Windows Authentication, provide the domain, username, and password during installation to impersonate the user, as the installer runs under the Local System account.

These credentials will not be stored in the connection string; however, the MetaDefender Managed File Transfer services will run under that user, requiring "Logon as a Service" rights.

The SQL Server account must have the "CREATE ANY DATABASE" SQL Server permission. This is required for the initial install (to create the database) and for a complete uninstall (to delete the database).

Warning

If you are upgrading MFT and [Setup Wizard - Post-Installation Configuration](/docs/mdmft/installation/post-installation-configuration) setup is not completed, the installer will halt the process. In such cases, either finish the setup or perform a clean installation

8. Click "Install" to proceed with the installation.

9. Wait for the installation to finish then click "Launch" to access the web user interface.

10. Finish [Post-Installation Setup](/docs/mdmft/installation/post-installation-configuration)

## [Clean Installation](/docs/mdmft/installation/installing-using-the-install-wizard#clean-installation)

If you encounter issues with a normal installation, perform a clean installation by selecting "yes" at the dialog below.

Warning

Running a clean installation on the selected database may result in loss of data.
