<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/database-vacuum -->

# Database Vacuum

Over time, the MDSS database accumulates index bloat and heap fragmentation as a result of deleted rows — for example, after a retention policy run or a large scan cleanup job. The `mdss -u vacuum` command provides two maintenance modes to address these issues.

## Normal mode -

```bash
sudo mdss -u vacuum
```

Rebuilds bloated indexes with no service interruption. All MDSS services remain running throughout.

**What it does:**

- Runs `VACUUM ANALYZE` on all tables — clears dead rows and updates query planner statistics
- Runs `REINDEX TABLE CONCURRENTLY` on `files`, `object_identity`, and `scan_results` — rebuilds indexes from scratch without locking reads or writes

**What you get:** Query performance is restored. Index sizes typically shrink by 55–70% after a large deletion.

**What you don't get:** Heap disk space is not reclaimed. Table file sizes on disk remain unchanged — this is expected PostgreSQL behavior. Only `VACUUM FULL` can physically rewrite and shrink the heap file.

## Full mode -

```bash
sudo mdss -u vacuum -f
```

> **Warning**
>
> The full vacuum requires a service outage

**What it does:**

1. Stops all MDSS services (`mdss stop`)
2. Runs `VACUUM FULL ANALYZE` — rewrites every table into a compact heap file; all dead-row pages are fully eliminated
3. Runs `REINDEX DATABASE` — rebuilds every index from the freshly compacted heap
4. Restarts all MDSS services (`mdss start`)

> **External PostgreSQL:** For deployments using an external PostgreSQL server, no temporary container is used. Services are still stopped before and restarted after the operation.

**What you get:** Both index bloat and heap fragmentation are resolved. Disk space is returned to the OS. Table sizes drop in proportion to the number of live rows remaining.

**What you don't get:** There is no way to run this without a service interruption. If downtime is not acceptable, run normal mode instead — query performance will be restored, but disk space will not be reclaimed until a maintenance window is available.

---

## Planning downtime for full vacuum

The duration depends primarily on the size of the PostgreSQL database on disk. Because services are stopped before the operation runs, there is no lock contention and the work proceeds at full I/O speed.

| **DB size** | Vacuum full | Service stop/start | Total downtime estimate |
| ---- | ---- | ---- | ---- |
| <1 GB | ~1 - 2 min | ~2 - 5 min | ~3 - 7 min |
| ~5 GB | ~2 - 5 min | ~2 - 5 min | ~4 - 10 min |
| ~20 GB | ~5 - 10 min | ~2 - 5 min | ~7 - 15 min |
| ~100 GB | ~30 - 40 min | ~2 - 5 min | ~35 - 45 min |
| 500 GB+ | > 3 h | ~2 - 5 min | > 3 h |

> **Info**
>
> On HDD storage, network-attached storage, or a heavily loaded host, the VACUUM FULL + REINDEX duration will be significantly longer.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
