<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/operating/database-maintenance---metadefender-core-4-18-0 -->

# Database Maintenance | MetaDefender Core 4.18.0

Only applicable to MetaDefender Core 4.18.0 with SQLite database.

Starting with version 4.19.0, the product has changed to using PostgreSQL database. The applicable vacuum instructions could be found at MetaDefender Core 4.19.0 or above

When your scan database grows big, it might cause performance degradation (e.g. timeout on client requests).

Since MetaDefender Core 4.18.0, admin user will be notified on the UI (also in product logs) when the processing history database file size exceeds over 10 GB.

Admin user is supported to perform database maintenance including defragmentation and optimization without loss of actual scan data under **Settings > Maintenance page**. As a result, your database file size could be reduced which helps boost processing performance tremendously over usage time.

****Caution:**** Please only use this feature when your entire scanning service is at rest.

Hitting “APPLY” to apply all changes and restart MetaDefender Core service (or “REVERT” to roll back changes).

By default, only the “admin” user role can see this Maintenance page and make the changes, but you can configure to grant access to other user roles if desired.
