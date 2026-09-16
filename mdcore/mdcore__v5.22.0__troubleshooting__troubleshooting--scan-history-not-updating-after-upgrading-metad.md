<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/troubleshooting--scan-history-not-updating-after-upgrading-metad -->

# Troubleshooting: Scan history not updating after upgrading MetaDefender Core - Linux

### [Who this is for](/docs/mdcore/v5.22.0/troubleshooting/troubleshooting--scan-history-not-updating-after-upgrading-metad#who-this-is-for)

Administrators who upgraded MetaDefender Core (for example from an older release such as 5.1.7.x to a newer one such as 5.18.x) on Rocky Linux 9 using the **shared / bundle** installation, and then notice that new scans no longer appear in history (or related features that use the database fail).

### [What you might see](/docs/mdcore/v5.22.0/troubleshooting/troubleshooting--scan-history-not-updating-after-upgrading-metad#what-you-might-see)

- Scans seem to run, but results are missing from scan history.
- Logs may contain messages similar to:

  - `could not load library ".../pg_trgm.so"`
  - `invoke failed, out='QMap(("error", QVariant(QString, "ERROR: could not load library`
  - `Failed to insert new request`
  - Other database-related errors that appear right after an upgrade, without you having changed configuration on purpose.

### [Recommended fix](/docs/mdcore/v5.22.0/troubleshooting/troubleshooting--scan-history-not-updating-after-upgrading-metad#recommended-fix)

After a major upgrade, the database and application must be using the same updated components. Restart the services in this order:

1. Restart the PostgreSQL service used by MetaDefender Core (the bundled database).
2. Restart the MetaDefender Core service.

Wait until PostgreSQL has fully started before starting or restarting Core if your environment requires a strict order.

Example (systemd — names can differ on your system):

BashCopysudo systemctl restart ometascan-pg
sudo systemctl restart ometascan
