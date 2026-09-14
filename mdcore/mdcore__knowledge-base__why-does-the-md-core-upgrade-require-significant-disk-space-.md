<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space- -->

# Why Does the MD Core Upgrade Require Significant Disk Space?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

When upgrading OPSWAT MetaDefender Core (MD Core) to a **much newer version**, some users encounter an **“Insufficient Disk Space”** error — even if the MD Core installation only appears to use a modest amount of disk space (e.g., 40 GB).

However, during the upgrade, the process may report requiring **well over 150 GB** of available disk space.

## [Why Major Upgrades Need More Space](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#why-major-upgrades-need-more-space)

Upgrading to a significantly newer version of MD Core can involve major architectural and database changes. These types of upgrades may:

- Temporarily duplicate data for migration or backup

  - *Ensure that available disk space is larger than the Core database size to accommodate this duplication.*
- Extract and stage large upgrade packages
- Create fallback points in case the upgrade needs to be rolled back

As a result, the upgrade process needs additional **temporary disk space**, far more than what Metade Core typically uses during daily operations.

## [Before You Retry the Upgrade](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#before-you-retry-the-upgrade)

If you’ve already experienced a failed upgrade due to disk space limitations, we recommend gathering some details to help us investigate the issue and provide tailored guidance.

Here’s what would help:

- **System Specifications** Overview of your total disk space and current available space on all drives
- **Installation Folder Usage** Go to your MD Core installation folder → right-click → *Properties* → take a screenshot
- **Data Folder Usage** Inside the installation folder, locate the `data` folder → right-click → *Properties* → take a screenshot
- **Upgrade Log File** If you have the upgrade log that mentioned the disk space requirement, please share it with your support case
- **Support Package** Generating a support package from the MD Core system can help us understand exactly what happened during the failed upgrade

Note:

If you're already working with OPSWAT Support, please attach this information to your existing case so we can assist you more effectively.

## [What You Can Do If Disk Space Is Limited](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#what-you-can-do-if-disk-space-is-limited)

If disk space is the main barrier, here are several ways to work around it:

#### [1. Reduce Existing Data Usage](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#1-reduce-existing-data-usage)

Free up space used by accumulated scan data and logs:

- [How to manage Disk Space Usage in pg_data\base directory in MetaDefender Core for Windows?](/docs/mdcore/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta)

#### [2. Adjust Data Retention Settings](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#2-adjust-data-retention-settings)

Reduce how long MD Core retains data:

- [What can I do when MetaDefender Core (Windows) has an insufficient disk space error?](/docs/mdcore/knowledge-base/what-can-i-do-when-metadefender-core--windows--has-an-insufficie)

#### [3. Move Temp and Quarantine Folders to Another Drive](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#3-move-temp-and-quarantine-folders-to-another-drive)

Use a drive with more free space:

- [How can the Temp folder be changed?](/docs/mdcore/knowledge-base/how-can-the-temp-folder-be-changed-)

#### [4. Fresh Installation on a New Machine](/docs/mdcore/knowledge-base/why-does-the-md-core-upgrade-require-significant-disk-space-#4-fresh-installation-on-a-new-machine)

Install the newer version of MD Core on a machine with sufficient space, then migrate your configurations and data.

Support:

If you continue to experience issue with the upgrade and have followed the instructions above, [**please create a support case or chat with our support engineer for further assistance.**](https://my.opswat.com/portal/support)
