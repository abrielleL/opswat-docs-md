<!-- source: https://www.opswat.com/docs/supply-chain/installation/upgrading-from-a-previous-version -->

# Upgrading from a previous version

## [Upgrading from a previous version on Unix-based deployments](https://docs.opswat.com/mdss/installation/upgrading-from-a-previous-version#upgrading-from-a-previous-version-on-unix-based-deployments)

### Preliminary notes

Upgrading is usually a two-step process:

1. upgrade the *mdssc* package by installing the newer package
2. upgrade the existing code by downloading new images

### Notes for upgrading to 4.1 and later

When upgrading from 4.0.x behind a TLS-terminating load balancer, set [ALLOWED_ORIGINS](https://www.opswat.com/docs/supply-chain/configuration/custom-configuration#allowed-origins). Otherwise, the Cross Domain Transfer Activity Log stops loading.

### Notes for upgrading to 4.2 and later

#### Cross Domain Transfer import scan settings

In 4.2, the High Side sets the import scan on each connection mapping, not in High Side Setup. The upgrade copies your 4.1 settings to each mapping:

- **Scan Before Import** keeps its 4.1 value. If it was never set, it is on after the upgrade.
- **Workflow** keeps the 4.1 scan workflow. If none was set, the mapping uses the **Default Workflow**.

The 4.1 **Maximum Allowed Severity** and **Block transfer if secrets are found** settings are removed. To block vulnerabilities and secrets, set the **Blocked File Definition** of the mapping's workflow.

After the upgrade, open each mapping on the High Side and check its import scan settings. For details, see [Cross Domain Transfer](https://www.opswat.com/docs/supply-chain/configuration/cross-domain-transfer#mapping-the-transfer).

#### API keys

In 4.2, each user has one API key. Existing API keys continue to work after the upgrade. When a user saves a new API key, MDSSC deletes that user's other keys.

After you save a new API key, update every place that uses the old key:

- the webhooks in your service providers
- the **Authorization Token** in the Low Side setup of Cross Domain Transfer

For details, see [Configuring an API Key](https://www.opswat.com/docs/supply-chain/configuration/configuring-an-api-key).

### Notes for upgrading to 4.3 and later

#### Cross Domain Administrator privilege

In 4.3, only a Cross Domain Administrator configures Cross Domain Transfer. The upgrade gives the **Cross Domain Administrator** privilege to every enabled local Administrator, once. SSO users do not get it.

After the upgrade, open the **Users** page and check who holds the privilege. Revoke it from the Administrators who do not need it. For details, see [User Roles](https://www.opswat.com/docs/supply-chain/configuration/user-roles#cross-domain-administrator-privilege).

#### High-Side Receive Key

In 4.3, the High Side accepts transfers only with the **High-Side Receive Key**. The Low Side **Authorization Token** no longer works. Transfers fail after the upgrade until you complete these steps:

1. Upgrade both the High Side and the Low Side.
2. On the High Side, sign in as a Cross Domain Administrator.
3. In **Settings** > **Cross Domain Transfer**, next to **High-Side Receive Key**, click **Create**. Copy the key.
4. On the Low Side, paste the key in **High-Side Receive Key** and click **Save**.

For details, see [Cross Domain Transfer](https://www.opswat.com/docs/supply-chain/configuration/cross-domain-transfer#high-side-receive-key).

#### Platform services update

In 4.3, MDSSC runs on a new version of the MetaDefender platform services. The upgrade changes the database and the containers. Read these notes before you upgrade from 4.2 or earlier.

**Before the upgrade**

- The upgrade does not create a backup. Take a snapshot of the server, or back up the database, before you install the new package. For the database backup, see Database procedures.
- Upgrade when no job is active. The upgrade stops all services, and running scans do not continue.

**Database migration**

- The database migration runs automatically when the services start after the upgrade. No command is necessary.
- The migration copies your connections, workflows, scheduled scans and settings.
- The migration does not copy the reports of scans made before the upgrade, unless you enable it. To copy them, add `MDSSC_MIGRATE_LEGACY_SCANS=true` to `/etc/mdssc/customer.env` before you run `sudo mdssc -u update`. The copy needs PostgreSQL 16 or later. The copy time increases with the number of scans.

**Expected downtime**

- The web interface and the API are not available during the upgrade. The package installation stops the services. They start again when you run `sudo mdssc -u update`.
- The downtime depends on the image download speed and on the size of the database. The services are available again when `sudo mdssc -c status` shows them as running and the web interface opens.

**Containers and configuration**

- The platform services now run in one container, `mdss_platform`. The upgrade removes the containers that are not used anymore. Update your container monitoring, if you have one.
- In `customer.env`, the upgrade renames `MDSS_VERSION` to `PLATFORM_VERSION` and `MDSS_REPO` to `PLATFORM_REPO`.
- If your `customer.env` sets `MDSSC_CONTAINER_TMP_MIN_FREE_MB` or `MDSSC_CONTAINER_TMP_WAIT_MAX_MINUTES`, rename them to `MDSSC_TMP_MIN_FREE_MB` and `MDSSC_TMP_WAIT_MAX_MINUTES`. MDSSC does not read the old names.

**Rollback**

- MDSSC has no downgrade command, and the database migration cannot be reversed.
- To go back to the previous version, restore the snapshot or the backup that you made before the upgrade.

### Update from the web interface

From 4.3, you can update MDSSC from **Settings** > **Product Update**. The update downloads the new package, installs it and restarts MDSSC.

> To upgrade from 4.2 or earlier to 4.3, use the installer package procedure below. The update from the web interface is available after you install 4.3.

The update from the web interface has these requirements:

- MDSSC is installed from the .deb or .rpm package. On other deployments, the page shows **Automatic updates are not available for this deployment.**
- The MDSSC server has internet access.

The **Product Version** card shows the **Installed Version**, the **Internet Access** status and the time of the last check. Click **Check now** to look for new versions:

![](https://uploads.developerhub.io/prod/jdK6/enry5fcpub34hrlfokxitswq227hiel2ek1wu5xmhe9quqeyuopznrfzu1v42jrs.png)

When a newer version exists, the page shows **New version available** and the **Available Updates** table. The table shows the version, the release date, the package size and the type of each update: Patch, Minor or Major.

To update MDSSC:

1. Open **Settings** > **Product Update**.
2. Optional: in **Available Updates**, click the preview button of a version to read what is new.
3. Click the update button of the version. To install the newest version, click **Update to <version>** in the banner.
4. Read the confirmation and click **Update Now**.

During the update:

- MDSSC restarts and all sessions disconnect.
- Running jobs are interrupted. They resume after the restart.
- The update typically takes a few minutes. The **Updating** page reconnects automatically. When it shows **Updated to version <version>**, click **Back to MDSSC**.

If the page shows **This is taking longer than expected**, check the service status on the server with `sudo mdssc -c status`.

The update does not create a backup. Back up the database before you update.

### Acquire the installer package

In order to acquire the new package please visit My OPSWAT -> [Product Downloads](https://my.opswat.com/home/metadefender-software-supply-chain)

### Debian / Ubuntu package (.deb)

1. Update your packages

```bash
sudo apt-get update
```

2. Move to the folder containing the installer and install it

```bash
sudo dpkg -i <name of the file>.deb || sudo apt-get install -f
```

3. Start the service

```bash
sudo mdssc -u update
```

4. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

5. Open a browser and navigate to the web interface: http://<server> to configure your deployment

### Red Hat Enterprise Linux / CentOS package (.rpm)

1. Update your packages

```bash
sudo yum -y update
```

2. Move to the folder containing the installer and install it

```bash
sudo yum upgrade <name of the file>.rpm
```

> **Warning**
>
> If `yum` fails with `Cannot download repomd.xml`, run the upgrade with all repositories disabled:
>
> ```bash
> sudo yum upgrade -y --disablerepo="*" ./mdssc-<version>.noarch.rpm
> ```

3. Start the service

```bash
sudo mdssc -u update
```

4. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

5. Open a browser and navigate to the web interface: http://<server> to configure your deployment

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
