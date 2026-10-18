<!-- source: https://www.opswat.com/docs/mdss/installation/upgrade-procedures -->

# Upgrade MDSS

> **Warning**
>
> Before proceeding with the upgrade process, it's highly recommended that a backup is performed of the original deployment in order for recovery purposes.
>
> The contents of the `customer.env` file (contains credentials and custom settings) and the PostgreSQL database files (contain all MDSS data) are critical in order to prevent any data loss.

## Upgrading is typically a two-step process:

1. Upgrade the **mdss** package by installing the newer version.
2. Update the codebase by downloading and applying new container images.

> **NOTE**
>
> > The behavior of the update process depends on the current version:
>
> - **Before v3.5.3:** Can only upgrade to v3.5.3
> - **From v3.5.3:** Can upgrade to version **v3.6.0** for database validation
> - **From v3.6.0**: Can upgrade to the latest compatible version
>
> > ⚠️ MDSS v3.6.0+ requires **MongoDB 6.0 or higher**
> >
> > ⚠️ MDSS v4.0.0+ requires **PostgreSQL 16.0 or higher**

## **Upgrading to version 4.0.0 or newer**

Starting with version 4.0.0 of MDSS the database will be migrated from MongoDB to PostgreSQL. Please follow the [Upgrade Guide to PostgreSQL](https://www.opswat.com/docs/mdss/configuration/upgrade-to-postgresql) to ensure the upgrade completes successfully and all data is migrated.

> ## **Unix-Based Systems**
>
> ### Step 1: Download the Installer
>
> Visit [My OPSWAT](https://my.opswat.com/)  to download the latest `.deb` or `.rpm` package.

> **Warning**
>
> > If you have overridden `ENABLED_MODULES` in `/etc/mdss/customer.env`, review the list before upgrading. Module names must match the ones in `/etc/mdss/.env` of the new version: `onedrive` was renamed to `graph` in 4.0.0 (OneDrive and SharePoint Online), and newer modules such as `mft`, `ftp` and `oraclesdk` are only enabled if they are in your list. Names are case-sensitive and must be separated by commas without spaces.
>
> > Starting with 4.6.0, unknown module names are ignored and the corresponding integrations are not available after the upgrade. Versions 4.0.0 to 4.5.2 stop instead with an error such as `open /etc/mdss/docker-compose.onedrive.yml: no such file or directory`. If you do not need a custom list, remove the line so the default from `.env` applies.

> **Offline Deployments**
>
> In case of an offline deployment, the offline steps need to be followed: [Offline Upgrade](https://www.opswat.com/docs/mdss/installation/upgrade-procedures#offline-upgrade)

### Debian / Ubuntu package (.deb)

1. Update your packages

```plaintext
sudo apt-get update
```

2. Move to the folder containing the installer and install it

```plaintext
sudo dpkg -i <name of the file>.deb || sudo apt-get install -f
```

3. Start the service

```plaintext
sudo mdss -u update
```

4. Optionally, you can check the status using the following command:

```plaintext
sudo mdss -c status
```

5. Open a browser and navigate to the web interface: **http://<server>** to configure your deployment.

### Red Hat Enterprise Linux / CentOS package (.rpm)

1. Update your packages

```plaintext
sudo yum -y update
```

2. Move to the folder containing the installer and install it

```plaintext
sudo yum upgrade <name of the file>.rpm
```

3. Start the service

```plaintext
sudo mdss -u update
```

4. Optionally, you can check the status using the following command:

```plaintext
sudo mdss -c status
```

5. Open a browser and navigate to the web interface: http://<server> to configure your deployment.

### Offline Upgrade

> **Warning**
>
> The following steps only apply when MDSS is installed using the official installer (.deb/.rpm). For any other deployment methods like when using the portable package, bundled binaries or the helm chart, then you should consider a clean deployment and migrating the original data if necessary.

> **Info**
>
> Instructions to be followed for upgrading after installing the product using the [Installing Offline on Linux documentation](https://www.opswat.com/docs/mdss/installation/linux-offline-installation)

1. Download the latest MetaDefender Storage Security **Installation Package** from [My OPSWAT](https://my.opswat.com/) portal.
2. Download the latest MetaDefender Storage Security **Offline Docker Tool Kit** from [My OPSWAT](https://my.opswat.com/) portal.

![](https://uploads.developerhub.io/prod/k8zL/qwml1ldy3elam56dn33845sbaaz6wpjjunybsrcikbvkvfggyeftekl6qfmpvtf5.png)

3. Stop the service

```bash
sudo mdss -c stop
```

4. Run the installation script

```bash
sudo dpkg -i <name of the file>.deb
```

```bash
sudo yum install -y <name of the file>.rpm
```

5. Extract deployment.zip folder and load the container images

```bash
unzip deployment.zip -d <extracting_path>/
cd <extracting_path>/
sudo docker load -i ./mdss.tar
```

6. Start the service

```bash
sudo mdss -c start
```

## Upgrading from a previous version on Windows-based deployments

### Upgrading from v3.4.0 or newer

To upgrade from a previous version, running the new installer is enough. The installer will walk you through the [Windows Installation Wizard Section](https://www.opswat.com/docs/mdss/installation/windows-installation)

### Upgrading from v3.3.4 or earlier to v3.4.0 or newer

Upgrading to v.3.4.0 from an older version requires a special procedure due to major architectural changes. If a clean install with configuration import is not possible, please see the steps below.

**Caution: This operation modifies a live database. Errors may cause irreversible data loss. Proceed with caution and ensure adequate backups. We advise on performing this operation only if absolutely necessary.**

All commands should be run in a PowerShell terminal.

1. Update MDSS to the latest version

```powershell
.\mdss.ps1 -u update
```

2. Edit the following file: C:\Program Files\OPSWAT\MetaDefender Storage Security\docker\docker-compose.main.linux.yml
3. Under the mongodb container modify the image to use version 6.0. It should look like this:

```yaml
version: '3'
services:
    mongodb:
        platform: linux/amd64
        image: "mongo:6.0"
        volumes:
            - mongo_db:/data/db
```

4. Repeat procedure for  C:\Program Files\OPSWAT\MetaDefender Storage Security\docker\docker-compose.main.all.linux.yml
5. Run the upgrade command from the installation directory (C:\Program Files\OPSWAT\MetaDefender Storage Security\docker):

```powershell
.\mdss.ps1 -u upgrade_db
```

Depending on your DB size, this operation may take more than 30 minutes

6. After upgrade is finished, export the DB

```powershell
.\mdss.ps1 -u export_db
```

7. Copy the exported DB archive to a different location, e.g.: C:\temp
8. In that different location, extract the archive

```powershell
tar -xf .\db_{timestamp}.tar
```

9. Compress the files in a zip format

```powershell
Compress-Archive .\dump\  db_{timestamp}.zip
```

10. Uninstall MetaDefender Storage Security 3.3.4 as documented [Uninstall](https://www.opswat.com/docs/mdss/installation/uninstall).
11. Run the latest installer for MetaDefender Storage Security as documented [Installation Methods](https://www.opswat.com/docs/mdss/installation/installation-methods)
12. Run the stop command from the installation directory (C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts)

```powershell
.\mdss.ps1 -c stop
```

13. Copy the .zip file you created earlier (db__{timestamp}_.zip) to the installation directory (by default, (C:\Program Files\OPSWAT\MetaDefender Storage Security)
14. Import the DB

```powershell
.\mdss.ps1 -u import_db
```

15. Run the start command:

```powershell
.\mdss.ps1 -c start
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
