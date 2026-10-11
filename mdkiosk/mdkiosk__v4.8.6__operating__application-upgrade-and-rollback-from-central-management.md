<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management -->

# Application Upgrade and Rollback from Central Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [Application Upgrade and Rollback from Central Management](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#application-upgrade-and-rollback-from-central-management)

If you manage your MetaDefender Kiosk devices with Central Management, you can upgrade or roll back the Kiosk application remotely, without visiting each device — for a single Kiosk or for a whole fleet at once. Rollback lets you revert a Kiosk to the version it was running immediately before its last upgrade, reusing the installation files that are already cached on the device, so no re-download is needed. Available starting in Kiosk 4.8.2.

## [Prerequisites](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#prerequisites)

- The Kiosk must be enrolled and managed by Central Management. Standalone Kiosks that are not enrolled cannot be upgraded or rolled back remotely — use the local Kiosk Console instead.
- MetaDefender Kiosk 4.8.2 or later must be installed on the device. Rollback triggered from Central Management is not available on earlier versions.
- Rollback requires that the Kiosk has at least one successful upgrade in its history, and that the files from that upgrade are still present on the device (they are kept automatically after every successful upgrade — you don't need to do anything to prepare them).

## [Upgrading a Kiosk from Central Management](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#upgrading-a-kiosk-from-central-management)

1. In Central Management, open **Inventory**, then select **MetaDefender Kiosk**.
2. Select one or more Kiosk instances to upgrade.
3. Open the **Applications** view for the selected instances and choose **Upgrade**.
4. Select the target Kiosk version and confirm.
5. Central Management downloads the upgrade package to each targeted Kiosk (if it isn't already cached there) and then installs it.
6. Track progress for each instance from the Applications view.

## [Rolling Back a Kiosk from Central Management](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#rolling-back-a-kiosk-from-central-management)

1. In Central Management, open **Inventory**, then select **MetaDefender Kiosk**.
2. Select one or more Kiosk instances that have completed at least one successful upgrade.
3. Open the **Applications** view for the selected instances and choose **Rollback**.
4. Confirm the rollback.
5. Central Management sends the rollback command to each targeted Kiosk. No download is needed — Kiosk reverts using the files it already has from the previous upgrade.
6. Track each instance's progress from the Applications view.

When rolling back several instances at once, you can choose to roll them back **one at a time** or **all at once**, and you can turn on **stop on failure** so that if one instance fails, the remaining instances in the job are not attempted.

### [What you'll see while a job runs](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#what-youll-see-while-a-job-runs)

As an upgrade or rollback runs, Central Management shows a status for each targeted Kiosk. For a rollback, you'll see it move through:

- **Waiting for rollback** — the Kiosk has received the command and is about to start.
- **Rolling back** — the Kiosk is actively reverting to the previous version.
- **Rollback success** — the Kiosk finished and is running the previous version again.
- **Rollback failed** — the Kiosk could not complete the rollback; Central Management reports a reason (for example, that the cached files from the previous upgrade could not be found).

At the physical Kiosk, an on-screen overlay shows the same progress and clears automatically once the job finishes.

You'll receive a single notification (for example, an email, if configured) once a job reaches its final state — you won't see a "success" message followed by a contradictory "failed" message for the same job.

## [Example: Rolling back a single Kiosk after a bad upgrade](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#example-rolling-back-a-single-kiosk-after-a-bad-upgrade)

An administrator upgrades one Kiosk from Central Management and, after reviewing it, decides to revert to the previous version:

1. In **Inventory → MetaDefender Kiosk**, the administrator selects the Kiosk and chooses **Rollback** from the **Applications** view, then confirms.
2. The Kiosk reports **Waiting for rollback**, then **Rolling back**, while the on-screen overlay shows the same progress at the device.
3. The Kiosk finishes reverting, restarts its service, and reports **Rollback success**.
4. Settings that depend on the installed version — such as system hardening state and the login disclaimer text — are restored along with the previous version, so no manual reconfiguration is needed after the rollback.

Note

Rollback can only revert to the version that was installed immediately before the most recent upgrade — you can't use it to jump back multiple versions. If you need an earlier version, install it directly.

Note

Only one upgrade or rollback job can run on a given Kiosk at a time. If you start a second job on a Kiosk while one is still in progress, Central Management rejects it with an error rather than running both at once.

## [Doing This Locally Instead](/docs/mdkiosk/v4.8.6/operating/application-upgrade-and-rollback-from-central-management#doing-this-locally-instead)

You don't need Central Management to roll back a Kiosk. From the Kiosk Console, go to **Upgrades → Upgrade History**, find a successful application upgrade entry, and click its **Rollback to Previous Version** icon. This performs the same rollback directly on that device.
