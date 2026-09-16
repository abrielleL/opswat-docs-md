<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core -->

# Product Upgrading

Simply run installer file, details could be found at [Installation](/docs/mdcore/v5.22.0/installation/installing-metadefender-core).

For command-line-mode upgrading (e.g. on **Linux**), just run the command line to install the new version of the product.

## [Recommendation for MetaDefender Core upgrade](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#recommendation-for-metadefender-core-upgrade)

Our goal is to help you execute the product upgrade continuously, efficiently, and correctly.

### [PostgreSQL service upgrade](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#postgresql-service-upgrade)

- **Bundled PostgreSQL Service**: If you are using the bundled PostgreSQL server included in the installer, the PostgreSQL service will be automatically upgraded to the newer version (if available). No additional action is required for this process.
- **Remote PostgreSQL Service**: For remote PostgreSQL servers, customers are responsible for managing and upgrading the service independently. Upgrading MetaDefender Core does not update the remote PostgreSQL service.

### [Before MetaDefender Core upgrade](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#before-metadefender-core-upgrade)

Prepare a proper disaster recovery plan (DRP) including some common practices:

- Backup, or take a snapshot of your current working MetaDefender Core server.

  - This is to help quickly rollback for any upgrade failure might cause later for any reason.
- Optionally backup your PostgreSQL database, especially when using remote shared database mode.

  - Reference: <https://www.postgresql.org/docs/current/backup.html>
  - Please do it after stopping all linked MetaDefender Core instances to avoid potential data collision.
- Lastly, if backing up entire server is not feasible, then at least export MetaDefender Core configuration package [Import/Export configuration](/docs/mdcore/v5.22.0/operating/import-export-configuration) just in case you'll need to start off a new server with current MetaDefender Core configuration to keep the scanning service running without any impact.

On the PostgreSQL server, double check server resource to ensure sufficient RAM memory and disk space to be preserved for the upgrade process.

- 8GB RAM available at least during the upgrade.
- Disk availability is greater than MetaDefender Core database size.

### [While doing the upgrade](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#while-doing-the-upgrade)

Applicable for shared database deployment:

- Stop all MetaDefender Core instances' scanning service before performing the upgrade.
- Upgrade one (1) MetaDefender Core instance at a time.
- Proceed to upgrade MetaDefender Core instance where the bundle local PostgreSQL server is used for shared database setup.
- Otherwise is using remote PostgreSQL then the upgrade order does not matter.

***For large size database, mostly for scan history, expecting long time to be spent on the upgrade process.***

The product supports an option to skip data migration for scan history to expedite the process drastically and mitigate any failure risk. You can manually backup all data from your PostgreSQL server for offline usage if any.

Check "Skip upgrade scan data" to enable this feature while doing the upgrade.

or add following key in the ignition file:

[internal]
skip_upgrade_scan_data = 0Info

You might notice this option during the upgrade process

"Do not clean up installation folder when uninstalling"

This option is designed for advanced users who need to preserve the installation directory after product removal. It provides control over whether the installer removes the entire installation folder during uninstallation (via msiexec)

- **Standard Users**: **If you are performing a typical uninstallation through the wizard interface, you can safely ignore this option**. The default behavior (cleaning up the installation folder) is appropriate for most use cases.
- **Advanced Users**: Select this option if you:

  - Need to preserve custom files or configurations stored in the installation directory
  - Plan to reinstall the product and want to retain certain files
  - Are performing administrative tasks that require keeping the installation structure intact

### [Rollback](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#rollback)

MetaDefender Core provides automatic rollback protection during the installation phase, but **rollback is not possible after a successful execution of the installer package**. For this reason, **we strongly recommend backing up your server before performing any upgrade**.

#### [Automatic Rollback During Installation](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#automatic-rollback-during-installation)

If an issue occurs during the installation process, the installer will automatically rollback changes:

**Windows (WIX Installer)**

- The WIX installer automatically handles rollback if errors occur during the installation wizard
- Common scenarios that trigger rollback:

  - Insufficient permissions
  - Missing required third-party libraries
  - Installation file corruption

**Linux (Package Managers)**

- **Debian-based systems (APT/dpkg)**: The package manager automatically rolls back if the `.deb` package installation fails
- **RHEL-based systems (YUM/RPM)**: The package manager automatically rolls back if the `.rpm` package installation fails

In all cases, the installer or package manager handles the rollback process automatically—no user intervention is required.

#### [Post-Installation Rollback Limitations](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#post-installation-rollback-limitations)

Once the package has been extracted and installed successfully, **automatic rollback is no longer available**. At this point:

- You cannot use the installer or package manager to revert to the previous version
- The only recovery option is to restore from a backup

Best Practices

To ensure you can recover from upgrade issues:

1. **Always back up your server** before starting the upgrade process
2. **Test the upgrade** in a non-production environment first
3. **Verify system requirements** (disk space, permissions, dependencies) before upgrading
4. **Plan for downtime** to allow for backup creation and testing after upgrade
### [Troubleshooting](/docs/mdcore/v5.22.0/installation/upgrading-metadefender-core#troubleshooting)

If the upgrade process ever runs into an error:

- Double check your network and services, applicable to remote PostgreSQL server.
- Optionally configure MetaDefender Core to skip migrating scan history.

  - Windows

    - Open Windows registry, and navigate to HKLM\Software\OPSWAT\Metascan
    - Add a new key `internal/skip_upgrade_scan_data` with value = 1
  - Linux

    - Open MetaDefender Core configuration file `/etc/ometascan/ometascan.conf`
    - Add new key into the file

      - [internal]
      - skip_upgrade_scan_data=1
  - Note: This key will be auto removed upon the upgrade finishes.
  - Then restart MetaDefender Core service to retry the upgrade.

    - Might retry this a few times until the upgrade is done.

Just in case the upgrade process still fails, please contact OPSWAT support with the support package - [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-) This will help us analyze the root cause and figure out an optimal solution for your system failure.
