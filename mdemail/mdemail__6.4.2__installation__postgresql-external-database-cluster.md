<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/installation/postgresql-external-database-cluster -->

# PostgreSQL external database cluster

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [On-premises database cluster](/docs/mdemail/6.4.2/installation/postgresql-external-database-cluster#on-premises-database-cluster)

OPSWAT recommends setting up an external PosgreSQL cluster in the *streaming replication* mode as a primary and a hot standby pair.

Limitations and assumptions

The setup below assumes that PostgreSQL is installed on Windows.

The server operating system version and its bitness; and the PostgreSQL version must be identical on the primary and standby PostgreSQL instance.

Security warning

The steps below are experimental and set up a basic system only.

Further hardening and security setup is needed to have a production system.

Load balancing and failover

Depending on the use of the PostgreSQL cluster a load balancer --like Pgpool-II or HAProxy may be needed to assist with failover and other tasks.

For details see <https://www.pgpool.net> and <https://www.haproxy.org>.

To setup a primary and standby PostgreSQL instance, perform the following steps:

### [Primary server](/docs/mdemail/6.4.2/installation/postgresql-external-database-cluster#primary-server)

1. Install PostgreSQL on the primary server
2. Enable remote connection for Email Gateway Security instances

   1. Edit `C:\Program Files\PostgreSQL\14\data\postgresql.conf`
   2. Configure `listen_addresses` to listen on addresses accessible for Email Gateway Security hosts. For details see <https://www.postgresql.org/docs/14/runtime-config-connection.html>.

      1. Example: `listen_addresses = '*'`
3. Enable remote authentication for Email Gateway Security instances

   1. Edit `C:\Program Files\PostgreSQL\14\data\pg_hba.conf`
   2. Add entry to allow authentication from other hosts. For details see <https://www.postgresql.org/docs/14/auth-pg-hba-conf.html>.

      1. Example: `host all postgres 172.0.0.0/8 scram-sha-256`
4. Enable PostgreSQL port (default `5432`) through the firewall
5. Configure PostgreSQL for replication

   1. In PostgreSQL create a user for replication

      1. Example: `CREATE USER replicator WITH REPLICATION ENCRYPTED PASSWORD 'replicator';`
   2. Configure postgreSQL for streaming replication

      1. Edit `C:\Program Files\PostgreSQL\14\data\postgresql.conf`

         1. Set `wal_level = replica` .
         2. Set `archive_mode = on` .
         3. Set `archive_command` to a reasonable value.

            1. For details see <https://www.postgresql.org/docs/14/runtime-config-wal.html>.
         4. Set `wal_keep_size` to a reasonable value.
         5. Set `max_wal_senders` to a reasonable value.

            1. For details see <https://www.postgresql.org/docs/14/runtime-config-replication.html>.
         6. Example:

            1. `wal_level = replica`
            2. `max_wal_senders = 10`
            3. `wal_keep_size = 10000`
            4. `archive_mode = on`
            5. `hot_standby = on`
            6. `archive_command = 'copy "%p" "c:\\temp\\archivedir\\%f"'`
      2. Create the directory for the WAL archives

         1. Example: `mkdir C:\temp\archivedir`
      3. Enable remote authentication for replicas

         1. Edit `C:\Program Files\PostgreSQL\14\data\pg_hba.conf`
         2. Add entry to allow authentication from other hosts. Use the PostgreSQL user that was created in step 5.a. For details see <https://www.postgresql.org/docs/14/auth-pg-hba-conf.html>.

            1. Example: `host replication replicator 172.0.0.0/8 scram-sha-256`

### [Standby server](/docs/mdemail/6.4.2/installation/postgresql-external-database-cluster#standby-server)

1. Install PostgreSQL on the standby server and stop the PostgreSQL service
2. Empty the `C:\Program Files\PostgreSQL\14\data` directory

   1. Example:

      1. `cd C:\Program Files\PostgreSQL\14\data`
      2. `del *.*`
3. Take a base backup on the primary server and apply it on the standby. Use the PostgreSQL user and password that was created in step *Primary server / 5.a*.

   1. Example: `"C:\Program Files\PostgreSQL\14\bin\pg_basebackup.exe" -D "c:\Program Files\PostgreSQL\14\data" -h win11-a -p 5432 -Xs -R -P -U replicator --password`
4. Create the `C:\Program Files\PostgreSQL\14\data\standby.signal` file (should be created by the previous step)
5. Start the PostgreSQL service
6. Verify that replication works for example with adding records on the primary instance that should show up on the standby.

For details see <https://www.enterprisedb.com/blog/how-set-streaming-replication-keep-your-postgresql-database-performant-and-date>.

## [Database as a service](/docs/mdemail/6.4.2/installation/postgresql-external-database-cluster#database-as-a-service)

PostgreSQL is offered by major SaaS providers. PostgreSQL as a service can be used as the database cluster for Email Gateway Security as long as the prerequisites are fulfilled. For details see [Software prerequisites](/docs/mdemail/6.4.2/installation/prerequisites#software).

Extensions may not be available by default

For certain PostgreSQL SaaS offerings the required extensions may not be enabled.

As an example the following article details how to allow extensions in Azure PostgreSQL: <https://learn.microsoft.com/en-us/azure/postgresql/extensions/how-to-allow-extensions>.

## [Failover](/docs/mdemail/6.4.2/installation/postgresql-external-database-cluster#failover)

PostgreSQL does not provide the system software required to identify a failure on the primary and notify the standby database server. Many such tools exist and are well integrated with the operating system facilities required for successful failover, such as IP address migration.

It is possible to *manually* detect the primary server being down and switching to the standby server. After the primary server gets down the manual method requires two high level steps:

1. Promote the standby. For details see <https://www.postgresql.org/docs/14/warm-standby-failover.html>.
2. Configure each Email Gateway Security instance to connect (`db_host`*,* `db_port`) and authenticate (`db_user_name`) to the promoted server. For details see [Registry configuration](/docs/mdemail/6.4.2/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitydatabase).

The recommended way is to use *automated* tools like [Pgpool-II](https://www.pgpool.net) and [HAProxy](https://www.haproxy.org) to assist the failover.
