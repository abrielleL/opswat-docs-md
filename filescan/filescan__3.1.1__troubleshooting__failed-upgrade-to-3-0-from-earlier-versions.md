<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/failed-upgrade-to-3-0-from-earlier-versions -->

# Failed upgrade to 3.0 from earlier versions

**Upgrading directly** from versions prior to 2.5.0 to 3.0.0 is **not supported**. Skipping version 2.5.x may result in a successful installation, but Sandbox will become inoperable. Consequences include:

- Scan tasks may fail with unexpected errors.
- Transform may fail to start due to a SQL error.

**Recommended Upgrade Path:** First upgrade to **2.5.1**, then proceed to **3.0.0**.

## [How to troubleshoot](/docs/filescan/3.1.1/troubleshooting/failed-upgrade-to-3-0-from-earlier-versions#how-to-troubleshoot)

The recommended and safest solution is to **follow the supported upgrade path** and run the installers in the correct order.

**If version 2.5.x was skipped and the system is already in a broken state**, the issue can be mitigated by following the steps below.

#### [1. Stop the Sandbox service](/docs/filescan/3.1.1/troubleshooting/failed-upgrade-to-3-0-from-earlier-versions#1-stop-the-sandbox-service)

Stop the Sandbox service before making any changes.

Stop SandboxCopysudo service sandbox stop

---

#### [2. Remove old update files](/docs/filescan/3.1.1/troubleshooting/failed-upgrade-to-3-0-from-earlier-versions#2-remove-old-update-files)

Remove leftover update and database files that prevent Sandbox from starting correctly.

Remove leftover filesCopysudo rm -rf /data/db/sandbox/transform/sqlite
sudo rm -rf /home/sandbox/sandbox/transform/storage/update

---

#### [3. Re-run the 3.0.0 installer](/docs/filescan/3.1.1/troubleshooting/failed-upgrade-to-3-0-from-earlier-versions#3-re-run-the-300-installer)

After the cleanup is complete, run the **3.0.0 installer again** as you normally would.

Once the installation finishes, the Sandbox services should start correctly, and file scanning should be restored.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
