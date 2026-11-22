<!-- source: https://www.opswat.com/docs/supply-chain/installation/version-upgrade-notes -->

# Version Upgrade Notes

### Overview

Some versions of MDSSC change how a feature works or need an action from you after the upgrade. This page lists those changes for each version.

Read the notes for every version between your current version and the version you upgrade to. For the upgrade procedure, see [Upgrading from a previous version](https://www.opswat.com/docs/supply-chain/installation/upgrading-from-a-previous-version).

---

## Upgrading to 4.3 and later

### Key Changes in v4.3.0

- **Platform services**: MDSSC runs on a new version of the MetaDefender platform services, with an automatic database migration
- **Cross Domain Administrator privilege**: only a Cross Domain Administrator configures Cross Domain Transfer
- **High-Side Receive Key**: the High Side accepts transfers only with this key

### Platform services update

In 4.3, MDSSC runs on a new version of the MetaDefender platform services. The upgrade changes the database and the containers. Read these notes before you upgrade from 4.2 or earlier.

**Before the upgrade**

- The upgrade does not create a backup. Take a snapshot of the server, or back up the database, before you install the new package. For the database backup, see [AWS RDS with PostgreSQL](https://www.opswat.com/docs/supply-chain/configuration/database-procedures).
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

### Cross Domain Administrator privilege

In 4.3, only a Cross Domain Administrator configures Cross Domain Transfer. The upgrade gives the **Cross Domain Administrator** privilege to every enabled local Administrator, once. SSO users do not get it.

After the upgrade, open the **Users** page and check who holds the privilege. Revoke it from the Administrators who do not need it. For details, see [User Roles](https://www.opswat.com/docs/supply-chain/configuration/user-roles#cross-domain-administrator-privilege).

### High-Side Receive Key

In 4.3, the High Side accepts transfers only with the **High-Side Receive Key**. The Low Side **Authorization Token** no longer works.

> **Warning**
>
> Transfers fail after the upgrade until you complete the steps below.

1. Upgrade both the High Side and the Low Side.
2. On the High Side, sign in as a Cross Domain Administrator.
3. In **Settings** > **Cross Domain Transfer**, next to **High-Side Receive Key**, click **Create**. Copy the key.
4. On the Low Side, paste the key in **High-Side Receive Key** and click **Save**.

For details, see [Cross Domain Transfer](https://www.opswat.com/docs/supply-chain/configuration/cross-domain-transfer#high-side-receive-key).

---

## Upgrading to 4.2 and later

### Key Changes in v4.2.0

- **Cross Domain Transfer**: the import scan is set on each connection mapping
- **API keys**: each user has one API key

### Cross Domain Transfer import scan settings

In 4.2, the High Side sets the import scan on each connection mapping, not in High Side Setup. The upgrade copies your 4.1 settings to each mapping:

- **Scan Before Import** keeps its 4.1 value. If it was never set, it is on after the upgrade.
- **Workflow** keeps the 4.1 scan workflow. If none was set, the mapping uses the **Default Workflow**.

The 4.1 **Maximum Allowed Severity** and **Block transfer if secrets are found** settings are removed. To block vulnerabilities and secrets, set the **Blocked File Definition** of the mapping's workflow.

After the upgrade, open each mapping on the High Side and check its import scan settings. For details, see [Cross Domain Transfer](https://www.opswat.com/docs/supply-chain/configuration/cross-domain-transfer#mapping-the-transfer).

### API keys

In 4.2, each user has one API key. Existing API keys continue to work after the upgrade. When a user saves a new API key, MDSSC deletes that user's other keys.

After you save a new API key, update every place that uses the old key:

- the webhooks in your service providers
- the **Authorization Token** in the Low Side setup of Cross Domain Transfer

For details, see [Configuring an API Key](https://www.opswat.com/docs/supply-chain/configuration/configuring-an-api-key).

---

## Upgrading to 4.1 and later

### Key Changes in v4.1.0

- **Cross Domain Transfer Activity Log**: uses a real-time connection that needs `ALLOWED_ORIGINS` behind a TLS-terminating load balancer

### Load balancer configuration

> **Warning**
>
> When upgrading from 4.0.x behind a TLS-terminating load balancer, set [ALLOWED_ORIGINS](https://www.opswat.com/docs/supply-chain/configuration/custom-configuration#allowed-origins). Otherwise, the Cross Domain Transfer Activity Log stops loading.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
