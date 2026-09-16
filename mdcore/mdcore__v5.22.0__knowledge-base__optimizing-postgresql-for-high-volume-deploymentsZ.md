<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ -->

# Optimizing PostgreSQL for High-Volume Deployments

This article applies to all MetaDefender Core releases deployed on Windows and Linux.

> ## [Overview](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#overview)
>
> In high-volume MetaDefender Core environments (heavy ICAP traffic, archive scanning, large file uploads, workflow processing), the default bundled PostgreSQL configuration is often the bottleneck.

## [Symptoms of an Untuned Database](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#symptoms-of-an-untuned-database)

- High CPU usage on the Database process.
- Slow file processing and "stuttering" in the Dashboard.
- Database locks or timeouts.
- Excessive disk I/O is causing system lag.

This guide explains how to tune the bundled PostgreSQL instance for high-volume deployments on Windows and Linux.

## [Prerequisites](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#prerequisites)

⚠️ Prerequisite: Before applying changes, take a Backup of your database or ensure you have a snapshot of the VM.

## [Tuning Strategy (Read This First)](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#tuning-strategy-read-this-first)

Do **not** blindly copy the examples below. You must adjust values based on your server's **Total RAM**.

### [Memory Allocation Guidelines](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#memory-allocation-guidelines)

Use this table to determine the correct values for your server size.

|  | **shared_buffers (25%)** | **effective_cache_size (75%)** | **maintenance_work_mem** | **max_wal_size** |
| --- | --- | --- | --- | --- |
| **16 GB** | 4GB | 12GB | 1GB | 4GB |
| **32 GB** | 8GB | 24GB | 2GB | 8GB |
| **64 GB** | 16GB | 48GB | 2GB | 16GB |
| **128 GB** | 32GB | 96GB | 4GB | 32GB |

## [PostgreSQL Tuning on Windows](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#postgresql-tuning-on-windows)

### [A. Locate the Correct Configuration File](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#a-locate-the-correct-configuration-file)

MetaDefender Core uses an override mechanism. You must edit the file in the installation directory, not the data directory.

- **File Path:** `<Installation Directory>\\OPSWAT\\MetaDefender Core\\postgres\\postgresql.conf`
- **Default Example:** `C:\\Program Files\\OPSWAT\\MetaDefender Core\\postgres\\postgresql.conf`

**Note:** If this file does not exist, create it. Settings in this file override the defaults in pg_data.

### [B. Apply Configuration [This configuration is tuned for a 64GB RAM Server]](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#b-apply-configuration-this-configuration-is-tuned-for-a-64gb-ram-server)

Open the `postgresql.conf` file (Run Notepad as Administrator) and add/append the following block. (Values below are optimised for a **64GB RAM server**. Adjust based on the table above.)

# -- Memory Settings (Adjust based on RAM Table) --
shared_buffers = 16GB
effective_cache_size = 48GB
work_mem = 64MB
maintenance_work_mem = 2GB
# -- Connection & Write Tuning --
max_connections = 100
wal_buffers = 16MB
max_wal_size = 16GB # Crucial for high-volume writes
min_wal_size = 4GB
checkpoint_completion_target = 0.9
# -- SSD Optimizations (If using SSD/NVMe) --
random_page_cost = 1.1 # Default is 4.0 (for spinning disks)
effective_io_concurrency = 200
# -- Autovacuum Tuning (Prevent Bloat) --
autovacuum = on
autovacuum_max_workers = 5

**IMPORTANT**: Please note that the number of workers is totally dependent on the customer’s instance **CPU** size.

**IMPORTANT**: The **random_page_cost** and **effective_io_concurrency** values are only applicable to the **SSD** disk.

### [C. Restart Service](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#c-restart-service)

Restarting the MetaDefender Core service automatically restarts the bundled PostgreSQL.

1. Press `Win + R`, type `services.msc`.
2. Locate `MetaDefender Core`.
3. Right-click > `Restart`.

## [PostgreSQL Tuning on Linux](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#postgresql-tuning-on-linux)

### [A. Locate the Correct Configuration File](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#a-locate-the-correct-configuration-file)

Create or edit the override configuration file.

- **Edit:** `/usr/lib/ometascan/postgres/postgresql.conf`

⚠️ **Do NOT modify:** `/var/lib/ometascan/pg_data/postgresql.conf` (This file is reset on upgrades/restarts).

### [B. Apply Configuration [This configuration is tuned for a 64GB RAM Server]](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#b-apply-configuration-this-configuration-is-tuned-for-a-64gb-ram-server)

Use a text editor to add the configuration block. (Values below are optimised for a **64GB RAM server**. Adjust based on the table above.)

sudo nano /usr/lib/ometascan/postgres/postgresql.conf

**Paste the following:**

# -- Memory Settings --
shared_buffers = 16GB
effective_cache_size = 48GB
work_mem = 64MB
maintenance_work_mem = 2GB
# -- Write Ahead Log (WAL) --
wal_buffers = 16MB
max_wal_size = 16GB
min_wal_size = 4GB
checkpoint_completion_target = 0.9
# -- Connections --
max_connections = 100
# -- Autovacuum --
autovacuum = on
autovacuum_max_workers = 5

**IMPORTANT**: Please note that the number of workers is totally dependent on the customer’s instance **CPU** size.

### [C. Restart Service](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#c-restart-service)

Restart the MetaDefender Core service to apply changes.

sudo systemctl restart ometascan
## [Verification](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#verification)

After restarting, you must confirm that the database actually loaded your new settings.

**Method:** Log in to the database (or use the SQL tool in the Core dashboard if available) and run:

SELECT name, setting, unit, source
FROM pg_settings
WHERE name IN ('shared_buffers', 'max_connections', 'max_wal_size', 'work_mem');

- **Check:** The `setting` column should match your new values.
- **Check:** The `source` column should say `configuration file` (indicating it read your override).

## [Monitoring & Troubleshooting](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#monitoring--troubleshooting)

### [Essential Monitoring Queries](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#essential-monitoring-queries)

1. **Check Active Connections** Ensure you aren't hitting the `max_connections` limit.

SELECT count(*) as active_connections FROM pg_stat_activity;

2. **Check for Slow Queries** Identify what is slowing down the system.

SELECT pid,
now() - query_start AS duration,
state,
query
FROM pg_stat_activity
WHERE state != 'idle'
ORDER BY duration DESC;

3. **Check Database Size**

- For a standalone DB

SELECT pg_size_pretty(pg_database_size('metadefender_core')) as db_size;

- For shared DB

SELECT pg_size_pretty(pg_database_size('metadefender_core_xxx')) as db_size;
### [When to Scale Up (Externalize Database)](/docs/mdcore/v5.22.0/knowledge-base/optimizing-postgresql-for-high-volume-deploymentsZ#when-to-scale-up-externalize-database)

If tuning PostgreSQL is insufficient, you should move to a **Dedicated PostgreSQL Server**.

**Indicators you need a dedicated DB server:**

- **CPU:** The `postgres` process consistently consumes > 40% of total system CPU (starving the Scanning engines).
- **Disk I/O:** Disk queue length is high, causing scan timeouts.
- **Database Size:** DB exceeds 500GB.
- **Architecture:** You are running multiple MetaDefender Core nodes and need a central repository.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
