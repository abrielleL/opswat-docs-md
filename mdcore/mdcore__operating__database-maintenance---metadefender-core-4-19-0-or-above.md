<!-- source: https://www.opswat.com/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above -->

# Database Maintenance | MetaDefender Core 4.19.0 or above

This tool and instructions are only applicable to MetaDefender Core 4.19.0 or above that leverages PostgreSQL database.

PostgreSQL database could be more bulky over time with high scanning traffic. Even manually removing scan history or leaving it to data retention to clean up old records, it will not immediately remove actual data in the PostgreSQL database which is fully controlled by PostgreSQL.

The tool which is bundled with MetaDefender Core installation is to analyze database and vacuum database effectively, and simplify IT administration.

- Windows: `<MetaDefender Core installation folder>\ometascan-vacuum-db.exe`
- Linux: `/usr/sbin/ometascan-vacuum-db`

Warning

Even though it is not required to stop MetaDefender Core service while running, but still recommended to run the vacuum tool when the scanning service is at rest, or not in peak hours to avoid scanning performance impact.

## [How-to run instructions](/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above#how-to-run-instructions)

### [Windows](/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above#windows)

1. Open cmd as Administrator
2. Navigate to MetaDefender Core installation folder (e.g. `C:\Program Files\OPSWAT\MetaDefender Core` )
3. Call: ometascan-vacuum-db.exe with no arguments.
4. Upon done, expected to have a new database analysis and vacuum outcome package auto generated in the same folder with format: `analyze_and``_cleanup_database``<timestamp>.zip`

### [Linux](/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above#linux)

1. Run as superuser privileges: `sudo export LD_LIBRARY_PATH=/usr/lib/ometascan`
2. Run as superuser privileges: `sudo /usr/sbin/ometascan-vacuum-db`
3. Upon done, expected to have a new database analysis and vacuum outcome package auto generated in `/usr/lib/ometascan/` with format: `/usr/lib/ometascan/analyze_and_cleanup_database_<timestamp>.tar.gz`

### [Kubernetes](/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above#kubernetes)

To run the vacuum in a containerized environment, use this command:

kubectl exec <pod-name> -c <container_name> -n <namespace> -- "/opt/ometascan/usr/sbin/ometascan-vacuum-db"

Example command and output:

$ kubectl exec md-core-9d96d7cb8-g5dhg -c md-core -n <namespace> -- "/opt/ometascan/usr/sbin/ometascan-vacuum-db"
Running vacuum with config file: /opt/ometascan/core_data/ometascan.conf
Postgres info: Temp directory: , /opt/ometascan/core_data/tmp
Postgres info: Current hba config version = 3, expected = 3,
Postgres info: Postgres private user is not defined,
Postgres info: Database name, metadefender_core
Postgres info: Postgres private password is not defined,
Postgres info: Generating private password for the first time, metadefender_core
Postgres info: The service and the config are mismatched, re-config the service..., /opt/ometascan/core_data/var/lib/ometascan/pg_data
Postgres info: PG_DATA path in dat file = /opt/ometascan/core_data/var/lib/ometascan/pg_data,
Postgres info: PG_DATA path in conf file = /opt/ometascan/core_data/var/lib/ometascan/pg_data,
Postgres info: Saving /opt/ometascan/core_data/tmp/ometascan/ometascan-pg.service,
Postgres info: Opened /opt/ometascan/core_data/tmp/ometascan/ometascan-pg.service,
Postgres info: Replacing ometascan-pg.service...,
Postgres info: Restart services...,
Postgres info: Saving /opt/ometascan/core_data/tmp/ometascan/ometascan-pg.init,
Postgres info: Replacing /etc/init.d/ometascan-pg,
Postgres info: Checking for database upgrade,
Postgres info: Upgrade database status: 0,
Postgres service init done
Creating connection with: postgres-core
Creating connection done
Created out dir: /opt/ometascan/core_data/analyze_and_cleanup_database
Working dir: /opt/ometascan/usr/lib/ometascan/postgres
Running vacuum DONE
## [What’s inside the generated package?](/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above#whats-inside-the-generated-package)

Including database object size analysis before and after running vacuum, the vacuum result and log, the new database size after vacuum. That helps us analyze and determine how effective the vacuum performs against that database, and investigate if any issue occurs.
