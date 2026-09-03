<!-- source: https://www.opswat.com/docs/mdss/4.4.2/installation/upgrade-procedures -->

# Upgrade MDSS

Before proceeding with the upgrade process, it's highly recommended that a backup is performed of the original deployment in order for recovery purposes.

The contents of the `customer.env` file (contains credentials and custom settings) and the PostgreSQL database files (contain all MDSS data) are critical in order to prevent any data loss.

## [Upgrading is typically a two-step process:](/docs/mdss/4.4.2/installation/upgrade-procedures#upgrading-is-typically-a-two-step-process)

1. Upgrade the **mdss** package by installing the newer version.
2. Update the codebase by downloading and applying new container images.

NOTE
> The behavior of the update process depends on the current version:

- **Before v3.5.3:** Can only upgrade to v3.5.3
- **From v3.5.3:** Can upgrade to version **v3.6.0** for database validation
- **From v3.6.0**: Can upgrade to the latest compatible version

> ⚠️ MDSS v3.6.0+ requires **MongoDB 6.0 or higher**
>
> ⚠️ MDSS v4.0.0+ requires **PostgreSQL 16.0 or higher**

## [**Upgrading to version 4.0.0 or newer**](/docs/mdss/4.4.2/installation/upgrade-procedures#upgrading-to-version-400-or-newer)

Starting with version 4.0.0 of MDSS the database will be migrated from MongoDB to PostgreSQL. Please follow the [Upgrade Guide to PostgreSQL](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql) to ensure the upgrade completes successfully and all data is migrated.

> ## [**Unix-Based Systems**](/docs/mdss/4.4.2/installation/upgrade-procedures#unix-based-systems)
>
> ### [Step 1: Download the Installer](/docs/mdss/4.4.2/installation/upgrade-procedures#step-1-download-the-installer)
>
> Visit [My OPSWAT](https://my.opswat.com/) to download the latest `.deb` or `.rpm` package.

Offline Deployments

In case of an offline deployment, the offline steps need to be followed: [Offline Upgrade](/docs/mdss/4.4.2/installation/upgrade-procedures#offline-upgrade)

### [Debian / Ubuntu package (.deb)](/docs/mdss/4.4.2/installation/upgrade-procedures#debian--ubuntu-package-deb)

1. Update your packages

sudo apt-get update

2. Move to the folder containing the installer and install it

sudo dpkg -i <name of the file>.deb || sudo apt-get install -f

3. Start the service

sudo mdss -u update

4. Optionally, you can check the status using the following command:

sudo mdss -c status

5. Open a browser and navigate to the web interface: **http://<server>** to configure your deployment.

### [Red Hat Enterprise Linux / CentOS package (.rpm)](/docs/mdss/4.4.2/installation/upgrade-procedures#red-hat-enterprise-linux--centos-package-rpm)

1. Update your packages

sudo yum -y update

2. Move to the folder containing the installer and install it

sudo yum upgrade <name of the file>.rpm

3. Start the service

sudo mdss -u update

4. Optionally, you can check the status using the following command:

sudo mdss -c status

5. Open a browser and navigate to the web interface: http://<server> to configure your deployment.

### [Offline Upgrade](/docs/mdss/4.4.2/installation/upgrade-procedures#offline-upgrade)

Warning

The following steps only apply when MDSS is installed using the official installer (.deb/.rpm). For any other deployment methods like when using the portable package, bundled binaries or the helm chart, then you should consider a clean deployment and migrating the original data if necessary.

Info

Instructions to be followed for upgrading after installing the product using the [Installing Offline on Linux documentation](https://www.opswat.com/docs/mdss/installation/installing-offline-on-linux)

1. Download the latest MetaDefender Storage Security **Installation Package** from [My OPSWAT](https://my.opswat.com/) portal.
2. Download the latest MetaDefender Storage Security **Offline Docker Tool Kit** from [My OPSWAT](https://my.opswat.com/) portal.

3. Stop the service

BashCopysudo mdss -c stop

4. Run the installation script

Ubuntu/DebianRedHat/CentOSCopysudo dpkg -i <name of the file>.debsudo yum install -y <name of the file>.rpm

5. Extract deployment.zip folder and load the container images

BashCopyunzip deployment.zip -d <extracting_path>/
cd <extracting_path>/
sudo docker load -i ./mdcs.tar

6. Start the service

BashCopysudo mdss -c start
## [Upgrading from a previous version on Windows-based deployments](/docs/mdss/4.4.2/installation/upgrade-procedures#upgrading-from-a-previous-version-on-windows-based-deployments)

### [Upgrading from v3.4.0 or newer](/docs/mdss/4.4.2/installation/upgrade-procedures#upgrading-from-v340-or-newer)

To upgrade from a previous version, running the new installer is enough. The installer will walk you through the [Windows Installation Wizard Section](/docs/mdss/4.4.2/installation/windows-installation)

### [Upgrading from v3.3.4 or earlier to v3.4.0 or newer](/docs/mdss/4.4.2/installation/upgrade-procedures#upgrading-from-v334-or-earlier-to-v340-or-newer)

Upgrading to v.3.4.0 from an older version requires a special procedure due to major architectural changes. If a clean install with configuration import is not possible, please see the steps below.

**Caution: This operation modifies a live database. Errors may cause irreversible data loss. Proceed with caution and ensure adequate backups. We advise on performing this operation only if absolutely necessary.**

All commands should be run in a PowerShell terminal.

1. Update MDSS to the latest version

PowershellCopy.\mdss.ps1 -u update

2. Edit the following file: C:\Program Files\OPSWAT\MetaDefender Storage Security\docker\docker-compose.main.linux.yml
3. Under the mongodb container modify the image to use version 6.0. It should look like this:

YamlCopyversion: '3'
services:
mongodb:
platform: linux/amd64
image: "mongo:6.0"
volumes:
- mongo_db:/data/db

4. Repeat procedure for C:\Program Files\OPSWAT\MetaDefender Storage Security\docker\docker-compose.main.all.linux.yml
5. Run the upgrade command from the installation directory (C:\Program Files\OPSWAT\MetaDefender Storage Security\docker):

PowershellCopy.\mdss.ps1 -u upgrade_db

Depending on your DB size, this operation may take more than 30 minutes

6. After upgrade is finished, export the DB

PowershellCopy.\mdss.ps1 -u export_db

7. Copy the exported DB archive to a different location, e.g.: C:\temp
8. In that different location, extract the archive

PowershellCopytar -xf .\db_{timestamp}.tar

9. Compress the files in a zip format

PowershellCopyCompress-Archive .\dump\ db_{timestamp}.zip

10. Uninstall MetaDefender Storage Security 3.3.4 as documented [Uninstall](/docs/mdss/4.4.2/installation/uninstall).
11. Run the latest installer for MetaDefender Storage Security as documented [Installation Methods](/docs/mdss/4.4.2/installation/installation-methods)
12. Run the stop command from the installation directory (C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts)

PowershellCopy.\mdss.ps1 -c stop

13. Copy the .zip file you created earlier (db__{timestamp}_.zip) to the installation directory (by default, (C:\Program Files\OPSWAT\MetaDefender Storage Security)
14. Import the DB

PowershellCopy.\mdss.ps1 -u import_db

15. Run the start command:

PowershellCopy.\mdss.ps1 -c start
