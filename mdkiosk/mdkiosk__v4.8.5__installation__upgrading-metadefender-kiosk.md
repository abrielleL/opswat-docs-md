<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/installation/upgrading-metadefender-kiosk -->

# Upgrading MetaDefender Kiosk

As of Kiosk 4.5.5, upgrading no longer requires uninstallation of an existing version. The installer can now be ran with a Kiosk already installed.

Upgrade from Kiosk 4.6.0

As a critical issue with login via AD authentication, Kiosk 4.6.0 was removed and unable to be upgraded in place. To upgrade to the latest version from the Kiosk 4.6.0, the following actions should be followed:

1. Remove the `Log` folder in the installation directory
2. Generate a support package from the Management Console
3. Uninstall Kiosk 4.6.0
4. Install the latest version
5. Configure Kiosk from the beginning. The support package from step `2` can be utilized to verify any missed settings or contact OPSWAT Support for more details.
## [Automatic Application Upgrade](/docs/mdkiosk/v4.8.5/installation/upgrading-metadefender-kiosk#automatic-application-upgrade)

In addition to running the installer manually, MetaDefender Kiosk can check for and install application upgrades automatically, without visiting the device.

1. From the Kiosk Console, navigate to **Upgrades**, then select the **Kiosk Application Upgrade** tab.
2. Turn on **Enable Kiosk application upgrade**.
3. Under **Upgrade source**, choose where the upgrade package comes from:

   - **My.OPSWAT.com (Internet)** — the Kiosk checks for and downloads new versions automatically.
   - **Folder** — specify a local or network folder path containing the upgrade package; useful for kiosks without internet access.
4. Under **Set schedule**, choose how often the Kiosk checks for and installs upgrades: **None** (manual only), **Daily**, **Weekly**, **Monthly**, or a **Specific time** (a one-time date and time).
5. Optionally, select **Automatically reboot if required after upgrading** so the device restarts on its own if the upgrade needs a full system restart to complete.
6. Select **Save Updates**.

Note

While an upgrade is installing, the Kiosk displays a full-screen progress overlay in place of the normal scanning screen so the device can't be used or interrupted mid-upgrade. The Kiosk automatically returns to normal operation on the new version once the upgrade finishes.

## [Rolling Back an Application Upgrade](/docs/mdkiosk/v4.8.5/installation/upgrading-metadefender-kiosk#rolling-back-an-application-upgrade)

If a newer version needs to be reverted, MetaDefender Kiosk keeps the previous version's files so a rollback doesn't require downloading anything again:

1. From the Kiosk Console, navigate to **Upgrades**, then select the **Upgrade History** tab.
2. Find the successful **Kiosk Application Upgrade** entry you want to revert.
3. Select the **Rollback to Previous Version** icon on that row.

For fleets managed through Central Management, an upgrade or rollback can also be triggered and monitored centrally instead of configuring each device individually — see [Application Upgrade and Rollback from Central Management](https://www.opswat.com/docs/mdkiosk/operating/application-upgrade-and-rollback-from-central-management).

Note

Rollback is only available to the version immediately before the current one — you can't roll back multiple versions at once. If a newly-installed version fails to start correctly, the Kiosk is designed to automatically revert to the last working version on its own.

Upgrade to a new version of Kiosk by running its installer using one of the following methods:

1. [Wizard](/docs/mdkiosk/v4.8.5/installation/installing-metadefender-kiosk-using-the-install-wizard)
2. [Command Line](/docs/mdkiosk/v4.8.5/installation/installing-metadefender-kiosk-from-the-command-line)

Installing Kiosk without uninstalling the previous version helps all configurations, workflow settings, and session history retained.

On manual uninstallation, session history will be lost and not retained after the installation of a new version.

Warning

Upgrading from an old version (4.3.X) might cause the Management Console to be inaccessible. A system restart should make it work.
