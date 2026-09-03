<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/installation/installation -->

# Installation

To upgrade the product from a previous -supported- product *release* to the current release (e.g. from 6.0.0 to 6.1.0), simply run the installer of the current release. The installation process will take care of upgrading the product and migrating all data.

To upgrade from an earlier product *version* to the current release (e.g. form 5.7.6 to 6.1.0), a migration process may need to be performed. For details see [Migration](/installation/migration).

Migration from version 5

Migration of data from the old embedded databases of version 5 is supported from release 6.1.0.

For details see [Migration From MetaDefender Email Gateway Security v5](/installation/migration#from-metadefender-email-gateway-security-v5).

## Overview

The following steps are needed to be executed to install MetaDefender Email Gateway Security

1. Download the package of your choice from the [My OPSWAT portal](https://my.opswat.com/)
2. Install the package on your computer
3. Open a web browser and point to: (`<server name or IP>` is the DNS name or IP address of your test server)
4. Follow the steps in [Wizard](/installation/wizard)

## Installation process

As usual with Windows installers, you may click through the installer steps to install the product.

Following are the detailed installation steps for MetaDefender Email Gateway Security:

1. Welcome message

2. License agreement

3. Setup type. The difference between *Simple* and *Custom* is that *Custom* allows you to select the installation folder. For both you may specify later the *REST address* and *REST port* (see step 5).

4. Installation folder

5. Server properties. This is the merge point for *Simple* and *Custom* setup types (see step 3). Specify the *REST address* and *REST port*:

   - *REST address*: the IP address on which the server is listening. If set to `0.0.0.0` then the server will listening on all available interfaces.
   - *REST port*: the TCP port on which the server is listening on the configured interface(s).
   - Exchange plugin installation:

     - *Microsoft Exchange Server (2013/2016) mode* (enabled only when Exchange is installed on the machine): Enable this to install MetaDefender Email Gateway Security's Exchange plugin. This option is only available if Microsoft Exchange Server is present in the system.

6. Database type.

   1. Standalone: this option creates a new, local PostgreSQL database for standalone deployments. This database may be reused later in other Email Gateway Security instances to share database. Details of the new local PostgreSQL installation need to be provided in the dialog.
   2. External database: this option will connect to an other, already existing PostgreSQL database for scalable or highly available deployments (that may be a dedicated database to share database among Email Gateway Security instances or that might have been already created with the Standalone option for an other Email Gateway Security instance to share database). Details of the existing PostgreSQL installation need to be provided in the dialog. To verify that the database server is accessible and that the process will be able to create the necessary database tables, the connection test must pass before the installation process can continue.

Port may already be taken

The default database port 5433 in case of a standalone deployment may already be taken by a running PostgreSQL instance (e.g. an other OPSWAT product's standalone database).

This situation can lead to a broken installation. To avoid that, the target database port availability must be checked prior to the installation.

Database password characters

Any printable ASCII characters (any characters between ASCII 33 (`!` exclamation mark) - ASCII 126 (`~` tilde)) are allowed as database password characters except ASCII 59 (`;` semicolon).

Password policy

No policy is enforced on database password complexity and length. Following industrial best practices is recommended.

7. Installation progress. This is the merge point of *Standalone* and *External database* database setup types.

9. Finish installation. After finishing the installation MetaDefender Email Gateway Security is up and running. You may access the Web Management Console for further configuration with pointing your browser to <http://localhost:8058/> or click the MetaDefender Email Gateway Security shortcut on the desktop.

## Uninstallation

Data and settings left behind

At uninstallation, Email Gateway Security leaves data files and database connection properties behind to make it possible to re-install the product and preserve its email data.

To clean up this data, manually remove the `InstallationFolder` (see [Registry configuration](/configuration/registry-configuration); default `C:\Program Files\OPSWAT\MetaDefender Email Security`) and the `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security` Registry key after uninstalling the product.

### Re-installation

Deployment mode kept

At re-installation without cleaning up the data and the Registry, Email Gateway Security will allow installation in the same deployment it previously was before the uninstallation (standalone with local database exclusive or scalable with remote database).

#### Clean re-installation

**Overview**

In certain cases (e.g.: upgrading to a newer release candidate, downgrading to a previous version or changing between local and remote database deployment mode) a clean re-installation of the product is required.

Loss of data

In case of a clean re-installation, data from the previous installation is lost.

For a clean re-installation:

1. Uninstall the previous version.
2. Delete installation directory.
3. Clean-up Windows registry.
4. Install the current version.

**Details**

*Uninstall the previous version*

| Step | Description | Details |
| --- | --- | --- |
| 1 | > Control Panel > Programs > Uninstall a program |  |
| 2 | In Programs and Features, find *MetaDefender Email Security*. Right click and select *Uninstall*. |  |
| 3 | Follow the steps of the installer |  |

*Delete the installation directory*

| Step | Description | Details |
| --- | --- | --- |
| 1 | Delete the directory and its contents where MetaDefender Email Security is installed. | The installation directory is stored in the `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\InstallationFolder` Registry value.  The default is `C:\Program Files\OPSWAT\MetaDefender Email Security`. |

Delete blocked

Deleting the installation directory may be blocked by running applications that hold or use files that are included in the installation directory.

A common example of this issue is `emailrelay.exe`, which is not stopped by the uninstallation process.

Please lookup `emailrelay.exe` in the task manager and stop it manually. After this, try deleting the folder again.

*Clean-up the Registry*

| Step | Description | Details |
| --- | --- | --- |
| 1 | Start the Registry Editor:  > regedit |  |
| 2 | Navigate to the following key: `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MetaDefender Email Security` |  |
| 3 | Delete the MetaDefender`Email Security` key and all of its subkeys |  |
| 4 | Confirm deletion |  |

*Install the current product version*

Follow the steps in the *Installation process* above.
