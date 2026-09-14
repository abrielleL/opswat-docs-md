<!-- source: https://www.opswat.com/docs/mdemail/installation/tuning-high-volume-postgresql-deployments -->

# Tuning high-volume PostgreSQL deployments

MetaDefender Email Gateway Security stores email history, quarantine data, statistics, and the email content itself in PostgreSQL. On high-volume deployments, the database server becomes the component that determines overall mail throughput: every stage of the processing pipeline (history recording, content storage, quarantine, reporting) issues database operations, so a saturated database slows down or stalls mail flow itself, not just the management UI.

A default PostgreSQL installation is tuned for small databases and light workloads. This page describes how to recognize a database-bound deployment and which PostgreSQL settings to change.

PostgreSQL version

Always use a PostgreSQL version listed in the [system requirements](/docs/mdemail/installation/prerequisites#3rd-party-frameworks-or-components) for your Email Gateway Security release. Apply configuration changes in a maintenance window and verify them afterwards — several settings below require a service restart.

## [When this page applies to you](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#when-this-page-applies-to-you)

Consider your deployment high-volume if it matches some of these characteristics:

| Characteristic | Typical values |
| --- | --- |
| Mail volume | 50,000–100,000+ emails per business day; sustained peaks of 5,000–7,000 emails/hour |
| Traffic pattern | Strong business-hours profile: volume ramps 5–10× within one hour in the morning |
| Email history size | Millions of email records (1–10M+); classification rows typically 2–3× the email count; quarantine in the hundreds of thousands to millions |
| Database size | Several hundred GB to multiple TB, depending on daily volume and retention |
| Database write volume | Tens of GB of WAL per hour during business hours |
| Topology | External PostgreSQL server, possibly shared with MetaDefender Core databases |

## [Symptoms of an undersized or default-configured database](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#symptoms-of-an-undersized-or-default-configured-database)

You are likely database-bound if you observe any of the following:

- Emails accumulate in **Pending** state during business hours and drain outside them; an Email Gateway Security service restart does not help.
- The **Email History** or **Quarantine** pages time out, load extremely slowly or only load when filters are applied.
- The Email Gateway Security log contains `Failed to acquire Pool Object, because none is available`, `Email history query failed`, or filestore read/write errors during busy hours.
- The PostgreSQL log contains repeated `checkpoints are occurring too frequently` hints.
- Queries spill large amounts of temporary files to disk: `pg_stat_database.temp_bytes` grows quickly, or (with `log_temp_files` enabled) the PostgreSQL log shows frequent large temporary-file entries — a sign that `work_mem` is too small for the workload. If `temp_file_limit` is set on your server, the same condition surfaces as `ERROR: temporary file size exceeds temp_file_limit` in the PostgreSQL log, with the affected query cancelled.
- MetaDefender Core instances sharing the same database server return HTTP 503 to scan requests during the same periods.

On default settings, business-hours load can produce a self-reinforcing write amplification: once the WAL volume exceeds `max_wal_size` (default 2 GB) faster than the checkpoint interval, PostgreSQL checkpoints every 30–60 seconds, and each checkpoint forces full-page images for every touched page. In our load tests this roughly **quadrupled** the write cost at identical mail volume — enough to saturate the disk and stall both Email Gateway Security and a co-hosted MetaDefender Core database. Removing the amplification (first row group below) is the highest-impact change.

## [Recommended settings](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#recommended-settings)

All values assume a dedicated database server. Percentages refer to the database server's physical RAM — check it before applying. Example absolute values are given for a 64 GB server.

### [Checkpoints and WAL — highest impact](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#checkpoints-and-wal--highest-impact)

| Setting | PostgreSQL default | Recommended | Restart? | Why |
| --- | --- | --- | --- | --- |
| `max_wal_size` | 2GB | **32–64GB** | No (reload) | Prevents WAL-triggered checkpoints under load. At tens of GB of WAL per hour, 2 GB forces a checkpoint every 30–60 s. Requires matching free space on the WAL volume (See `pg_wal` below for details). |
| `checkpoint_timeout` | 5min | **15–30min** | No | Fewer checkpoints → fewer full-page re-images → several times less WAL at identical mail volume. |
| `wal_compression` | off | **zstd** (or `lz4`) | No | Compresses full-page images — typically 50–70% WAL reduction on this workload profile, at low CPU cost. |
| `min_wal_size` | 80MB–512MB | **4GB** | No | Keeps recycled WAL segments between traffic bursts, avoiding file create/delete churn. |
| `checkpoint_completion_target` | 0.9 | keep 0.9 | — | Already appropriate. |

Potentially longer recovery

Raising `checkpoint_timeout` and `max_wal_size` increases the amount of WAL PostgreSQL must replay after a crash or unclean shutdown — recovery can take several minutes instead of seconds before the database accepts connections again (and mail flow resumes). Choose values that keep the worst-case recovery time acceptable for your availability requirements.

### [Memory](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#memory)

| Setting | PostgreSQL default | Recommended | Restart? | Why |
| --- | --- | --- | --- | --- |
| `shared_buffers` | 128MB | **25% of RAM** (e.g. 16GB) | Yes | The default forces constant page eviction and re-reads against a large database. |
| `effective_cache_size` | 4GB | **~70% of RAM** (e.g. 45GB) | No | Planner hint; too low makes PostgreSQL choose unnecessarily pessimistic plans. |
| `work_mem` | 4MB | **32–64MB** | No | 4 MB makes even mid-size sorts and hash joins spill to temporary files on disk. Do not set much higher globally — the limit applies per sort/hash operation per backend. |
| `maintenance_work_mem` | 64MB | **1–2GB** | No | Vacuum and index builds on multi-hundred-GB tables are severely slowed at 64 MB (repeated index passes). |
| `autovacuum_work_mem` | -1 | **1GB** | No | Bounds the same for autovacuum workers. |

### [Autovacuum — keep large tables healthy](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#autovacuum--keep-large-tables-healthy)

With default thresholds (`autovacuum_vacuum_scale_factor = 0.2`), a multi-million-row history table is only vacuumed after 20% of it is dead — rare, enormous vacuum runs that then compete with production traffic for hours. Prefer frequent small vacuums:

| Setting | PostgreSQL default | Recommended | Restart? |
| --- | --- | --- | --- |
| `autovacuum_max_workers` | 3 | 4–6 | Yes |
| `autovacuum_vacuum_cost_limit` | 200 (via `vacuum_cost_limit`) | 1000–2000 | No |
| `log_autovacuum_min_duration` | off | 0 (log all runs) | No |

Additionally, set per-table thresholds on the large Email Gateway Security tables so they receive small, frequent vacuums:

ALTER TABLE mdemailsecurity.filestore_files SET (
autovacuum_vacuum_scale_factor = 0.01,
autovacuum_vacuum_insert_scale_factor = 0.02,
autovacuum_analyze_scale_factor = 0.02);
-- repeat for:
-- mdemailsecurity.emailhistorydb_emails
-- mdemailsecurity.emailhistorydb_email_classifications
-- mdemailsecurity.emailhistorydb_emails_quarantined

If the deployment has been running on defaults for a long time, schedule a one-time `VACUUM (VERBOSE)` of these tables in an off-hours window to clear accumulated dead rows first.

### [Guard rails — contain runaway queries and stuck sessions](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#guard-rails--contain-runaway-queries-and-stuck-sessions)

Set these per database rather than globally, so maintenance operations are not affected:

ALTER DATABASE mdemailsecurity SET statement_timeout = '120s';
ALTER DATABASE mdemailsecurity SET lock_timeout = '15s';
ALTER DATABASE mdemailsecurity SET idle_in_transaction_session_timeout = '5min';

`temp_file_limit` (default: unlimited) caps how much temporary file space a single process may use and is a reasonable safety net (e.g. `2GB`). Two cautions:

- The limit is **per process**: a query using parallel workers can consume a multiple of the limit before being cancelled.
- Mind the unit when changing it. The value accepts `kB`, `MB` and `GB` suffixes — a typo such as `2000kB` instead of `2000MB` makes practically every reporting query and index build fail with `temporary file size exceeds temp_file_limit`.

### [Observability — cheap settings that make the next incident diagnosable](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#observability--cheap-settings-that-make-the-next-incident-diagnosable)

| Setting | Recommended | Effect |
| --- | --- | --- |
| `log_lock_waits` | on | Logs any session waiting on a lock longer than `deadlock_timeout` (1 s), including the blocker. |
| `log_temp_files` | 102400 (100 MB) | Logs every large temporary-file spill together with the query that caused it. |
| `log_min_duration_statement` | 5000–30000 (ms) | Logs slow statements. |
| `track_io_timing` | on | Adds real I/O timings to `pg_stat_statements`. |
| `shared_preload_libraries` | pg_stat_statements | Per-query statistics; on PostgreSQL 15+ includes `wal_bytes` for write attribution (see below). |

To see which database and which queries generate the write load:

SELECT d.datname,
pg_size_pretty(sum(s.wal_bytes)) AS wal_written,
sum(s.calls) AS calls
FROM pg_stat_statements s
JOIN pg_database d ON d.oid = s.dbid
GROUP BY d.datname
ORDER BY sum(s.wal_bytes) DESC;

Reset the statistics at the start of a business day (`SELECT pg_stat_statements_reset();`) and snapshot them at the end for a clean measurement window.

## [What not to change](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#what-not-to-change)

- `full_page_writes` — leave **on**. Disabling it also removes checkpoint write amplification, but risks unrecoverable corruption after a crash unless the storage guarantees atomic 8 kB writes. Use `wal_compression` and a larger `max_wal_size` instead.
- `synchronous_commit` — leave **on** unless you can accept losing the most recent commits on a crash.
- `fsync` — never disable.

## [Beyond postgresql.conf](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#beyond-postgresqlconf)

These architectural measures matter as much as the configuration settings:

- **Do not share one PostgreSQL instance between Email Gateway Security and MetaDefender Core** at high volume. Both products are write-heavy; on a shared instance they saturate the same disk and connection pool, and degrade together. Use separate instances — ideally separate servers.
- **Place** `pg_wal` **on a separate physical disk** from the data files. Every commit waits on a WAL flush; on a shared disk, checkpoint bursts and temporary-file spills inflate commit latency for every transaction.
- **Size retention to storage.** Email history and quarantine retention multiplied by daily volume determines the database size; long retention at a high daily volume quickly produces a multi-TB database. Smaller tables mean faster queries, faster vacuum, and faster backups.
- **Watch connection counts.** `max_connections` (default 100) is shared by all Email Gateway Security instances, MetaDefender Core instances, and tools. Post-restart reconnection storms can exhaust it; a connection pooler in front of high-churn clients removes both the storm risk and the per-connection process overhead (significant on Windows).
- **Verify disk headroom** after tuning: during business hours, disk write latency and queue length (Windows Performance Monitor, or `iostat` on Linux) should stay well below saturation. The tuning above reduces the write volume several-fold, but the underlying disk still has to carry the remainder.

## [Quick verification checklist](/docs/mdemail/installation/tuning-high-volume-postgresql-deployments#quick-verification-checklist)

After applying the changes, during a normal business day:

1. PostgreSQL log contains **no** `checkpoints are occurring too frequently` hints; checkpoints are timed (`checkpoint starting: time`), not WAL-triggered.
2. No `temporary file size exceeds temp_file_limit` errors; `log_temp_files` shows no unexpectedly large spills.
3. `SELECT * FROM pg_stat_database WHERE datname = 'mdemailsecurity';` shows `temp_bytes` growing slowly or not at all.
4. Emails do not accumulate in Pending state at peak hour; Email History and Quarantine pages load without filters.
5. Autovacuum log lines show regular short runs on the large tables instead of rare multi-hour ones.
