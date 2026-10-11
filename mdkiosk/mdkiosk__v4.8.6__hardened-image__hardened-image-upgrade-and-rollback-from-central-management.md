<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/hardened-image-upgrade-and-rollback-from-central-management -->

# Hardened Image Upgrade and Rollback from Central Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Administrators managing a fleet of Kiosks with Central Management can now upgrade and roll back the **Kiosk Hardened Image** directly from Central Management, without needing to place devices into a special management group first. You can target a single Kiosk or many at once, schedule the upgrade for a maintenance window, and roll a device back to its previous Hardened Image if needed — all from the Central Management console. This is available starting in Kiosk 4.8.3.

This is separate from upgrading and rolling back the Kiosk application itself, which is managed independently — see your Central Management documentation for application-level upgrade and rollback.

## [Prerequisites](/docs/mdkiosk/v4.8.6/hardened-image/hardened-image-upgrade-and-rollback-from-central-management#prerequisites)

- MetaDefender Kiosk **4.8.3 or later** on each device you want to manage this way.
- The Kiosk must be enrolled to Central Management.
- The device must have enough free disk space to prepare the upgrade (Kiosk checks for this automatically and reports an error if space is insufficient).
- To roll back, the device must have at least one previous successful Hardened Image upgrade.

## [Upgrading the Hardened Image from Central Management](/docs/mdkiosk/v4.8.6/hardened-image/hardened-image-upgrade-and-rollback-from-central-management#upgrading-the-hardened-image-from-central-management)

1. In Central Management, select the Kiosk device(s) you want to upgrade.
2. Create a Hardened Image upgrade job, choosing the target image version.
3. Set an **Update Preparation** window (when the device should download the upgrade package) and a **Maintenance Window** (when the device should actually perform the upgrade).
4. Save the job. During the Update Preparation window, each targeted Kiosk downloads the upgrade package in the background. At the Maintenance Window, each Kiosk performs the upgrade and restarts as needed.
5. Monitor progress and the final result (success or failure) for each device from Central Management.

While an upgrade or rollback job is running against a device, a second job cannot be started against the same device — including a rollback attempted from the Kiosk's own web console — until the first job finishes.

## [Rolling Back the Hardened Image](/docs/mdkiosk/v4.8.6/hardened-image/hardened-image-upgrade-and-rollback-from-central-management#rolling-back-the-hardened-image)

You can roll back a device to its previous Hardened Image in two ways:

- **From Central Management:** Create a rollback job against a Kiosk that has a previous successful Hardened Image upgrade. No re-download is needed — the Kiosk restores from the snapshot it created before the last upgrade.
- **From the Kiosk itself:** From the Kiosk Web Management Console, go to **Upgrades > Upgrade History** and use the rollback action on a successful Hardened Image upgrade entry.

Note

Rollback restores the device to the version it had immediately before its most recent successful Hardened Image upgrade — you cannot roll back further than one version at a time.

## [What to Expect During the Upgrade or Rollback](/docs/mdkiosk/v4.8.6/hardened-image/hardened-image-upgrade-and-rollback-from-central-management#what-to-expect-during-the-upgrade-or-rollback)

The upgrade and rollback process, restart behavior, preserved folders, post-upgrade script, and Windows account handling are the same whether the job is triggered from Central Management or locally from the Kiosk — see [Auto-Upgrade Kiosk Hardened Image](/docs/mdkiosk/v4.8.6/docs/mdkiosk/hardened-image/auto-upgrade-kiosk-hardened-image) for the full mechanics of what gets backed up and restored.

If a job fails — for example, due to insufficient disk space — the device reports the failure back to Central Management with an error, and remains on its current version. It does not restart into a partial or broken state.

Note

Central Management will not let you upgrade a device to a version that isn't newer than what's already installed, and won't let you roll back to the version the device is already running.

## [Known Limitations](/docs/mdkiosk/v4.8.6/hardened-image/hardened-image-upgrade-and-rollback-from-central-management#known-limitations)

- This capability requires Central Management with support for Kiosk Hardened Image upgrade/rollback jobs; consult your Central Management documentation for version requirements.
- Repeating an upgrade to the latest version automatically, reusing upgrade settings across jobs, and upgrading from a folder path via Central Management are not yet available — these are planned for a future release.
- General Hardened Image upgrade limitations still apply to Central-Management-triggered jobs — for example, BitLocker must be disabled on the system drive before upgrading, and only a locally-integrated MetaDefender Core is restored (a remote Core's configuration is not). See [Kiosk Image Upgrade Known Limitations](/docs/mdkiosk/v4.8.6/docs/mdkiosk/hardened-image/kiosk-image-upgrade-known-limitations) for the complete list.
