<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre -->

# Database dead-tuple alert: what it means and how to tune PostgreSQL autovacuum

## [Dead tuples (what they are)](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#dead-tuples-what-they-are)

In PostgreSQL, each row in a table is stored as a tuple. When a row is updated or deleted, PostgreSQL does not immediately remove the old copy from disk. The old version becomes obsolete and is referred to as a dead tuple (also called “dead rows”). Dead tuples remain until PostgreSQL runs VACUUM, which reclaims that space and keeps the database efficient.

If dead tuples accumulate, tables grow larger than necessary, queries and maintenance can take longer, and the database may use more disk I/O and storage than required.

### [How this relates to MetaDefender Core](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#how-this-relates-to-metadefender-core)

During normal operation, MetaDefender Core creates, updates, and deletes database records as files are submitted and processed (for example, as scan state and results change over the lifecycle of a submission). Over time, this routine activity produces dead tuples in the same way any busy application database does.

Dead tuples are expected in a working system; the important part is that regular maintenance (autovacuum/VACUUM) keeps them under control so performance and storage use stay healthy.

## [When the system sends an email notification](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#when-the-system-sends-an-email-notification)

Please check more details about email notification for dead tuples: [Email Notification](/docs/mdcore/v5.22.0/configuration/email-notification)

The database monitoring feature sends an email when the estimated number of dead tuples exceeds a configured threshold (for example, 200,000).

> Note: Thresholds, intervals, and severity may vary if your deployment uses non-default configuration. Use your administrator-defined settings as the source of truth.

---

### [Bundled PostgreSQL compared with remote PostgreSQL](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#bundled-postgresql-compared-with-remote-postgresql)

Whether you use the bundled PostgreSQL included with MetaDefender Core or a remote (external) self-managed PostgreSQL instance affects how often you are likely to see this alert.

- Bundled PostgreSQL: **The database is delivered with settings intended to keep dead tuples under control. In typical deployments, this alert is uncommon.**
- Remote PostgreSQL: Maintenance behavior depends on your organization’s PostgreSQL configuration. If autovacuum is disabled, delayed, or tuned to run only at higher dead tuples levels than your alert threshold, you may see more frequent or recurring notifications until the database is tuned appropriately.

---

### [Bundled PostgreSQL (default installation)](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#bundled-postgresql-default-installation)

When MetaDefender Core is installed with the bundled PostgreSQL database:

- Autovacuum is enabled by default, so PostgreSQL can reclaim dead tuples automatically during normal operation.
- The bundled configuration is aligned so that autovacuum is expected to address dead tuples before they reach typical alert thresholds (for example, autovacuum may begin cleanup around 100,000 dead tuples while an alert might be configured around 200,000—exact values depend on your environment).

Expected outcome: Dead tuples are routinely reclaimed, so the dead tuples count usually does not reach the email alert threshold. **As a result, administrators rarely receive this email on a correctly operating bundled database.**

### [Remote PostgreSQL (external / self-managed)](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#remote-postgresql-external--self-managed)

If MetaDefender Core uses a remote PostgreSQL instance that your organization hosts and maintains, **autovacuum behavior is determined by your database configuration**, not by the MetaDefender Core application alone.

Misalignment between your alert threshold (for example, 200,000 dead tuples) and your PostgreSQL maintenance settings can cause repeated or intermittent email notifications.

---

### [Conditions that commonly lead to frequent alerts](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#conditions-that-commonly-lead-to-frequent-alerts)

The examples below assume an email alert threshold around 200,000 dead tuples (your environment may differ).

| Scenario | What happens | Typical impact |
| --- | --- | --- |
| Autovacuum is **disabled** | Dead tuples are not reclaimed automatically | Dead tuple counts can rise steadily; you may receive alerts on each evaluation cycle, subject to the 24-hour cooldown between emails |
| Autovacuum thresholds are higher than the alert threshold | Vacuum runs only after dead tuples exceed the database’s configured trigger | The alert can trigger before autovacuum begins cleanup, which may produce recurring notifications until settings are aligned |
| Autovacuum is enabled but runs too slowly or too infrequently for workload | Dead tuples accumulate between successful vacuum cycles | Counts may sporadically cross the alert threshold during busy periods |

---

### [Recommended action for remote PostgreSQL administrators](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#recommended-action-for-remote-postgresql-administrators)

Work with your database administrator to ensure PostgreSQL autovacuum is enabled and tuned so that routine cleanup begins before dead tuples reach your MetaDefender Core alert threshold.

A practical approach is to align autovacuum settings with the bundled PostgreSQL defaults supplied with MetaDefender Core (or your organization’s approved baseline). This typically reduces unnecessary dead tuples growth and helps prevent routine alert emails caused by maintenance lag.

> Note: PostgreSQL tuning should consider server CPU, memory, disk performance, and database workload. Apply changes through your standard change-management process, validate in a non-production environment when possible, and reload/restart PostgreSQL according to your configuration method (`ALTER SYSTEM` + `pg_reload_conf()`, or equivalent).

| **auto vacuum metrics** | **value** |
| --- | --- |
| `autovacuum` | true |
| `autovacuum_vacuum_threshold` | 100000 |
| `autovacuum_vacuum_scale_factor` | 0 |

### [Guidance on the recommended settings](/docs/mdcore/v5.22.0/troubleshooting/database-dead-tuple-alert--what-it-means-and-how-to-tune-postgre#guidance-on-the-recommended-settings)

The settings described in this guide are intended to encourage PostgreSQL to run autovacuum before dead tuples reach levels that commonly trigger MetaDefender Core alerts (for example, by using a lower autovacuum trigger than a typical 200,000 dead-tuple alert threshold, such as a 100,000-tuple-oriented baseline when paired with appropriate scale factors).

**These values are recommendations, not a universal standard**. You should tune PostgreSQL to match your hardware capacity, workload patterns, maintenance windows, and organizational policies.

What matters most

- Autovacuum must remain enabled for routine dead tuples cleanup.
- Autovacuum vacuum thresholds and scale factors should be set to reasonable values for your database size and activity so cleanup runs predictably and before dead tuples accumulate to the point where they affect performance or generate frequent monitoring alerts.

If you are unsure, validate changes in a non-production environment first, then monitor dead tuples trends, autovacuum activity, and system resource usage after deployment.
