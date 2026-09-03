<!-- source: https://www.opswat.com/docs/mdcluster/trouble-shooting/open-connection-on-pg-server -->

# Open Connection On PostgreSQL Server

Just in case the firewall is enabled, please also ensure that you configure your firewall rules properly for the connections between PostgreSQL server and the services of MetaDefender Cluster, which include MetaDefender Core services.

Info

The guide here assumes we are using an SSL connection with PostgreSQL. With a non-SSL connection, please use `host` instead.

### [Windows](/docs/mdcluster/trouble-shooting/open-connection-on-pg-server#windows)

1. Locate and modify `pg_hba.conf` configuration file within the PostgreSQL data directory. For example**:** `C:\Program Files\PostgreSQL\16\data\pg_hba.conf`.

pg_hba.confCopyhostssl all all 0.0.0.0/0 scram-sha-256

In the above example, all source addresses from MetaDefender Cluster and MetaDefender Core services are permitted. Refer [here](https://www.postgresql.org/docs/9.1/auth-pg-hba-conf.html) for more details.

2. Locate and modify `postgresql.conf` configuration file within the PostgreSQL data directory. For example: `C:\Program Files\PostgreSQL\<version>\data\postgresql.conf`.

postgresql.confCopylisten_addresses = '*'

The configuration above directs PostgreSQL server to permit incoming connections from all sources associated with MetaDefender Cluster and MetaDefender Core services**.** Learn more from [here](https://www.postgresql.org/docs/9.1/runtime-config-connection.html).

### [Linux](/docs/mdcluster/trouble-shooting/open-connection-on-pg-server#linux)

1. Locate and modify the `pg_hba.conf` configuration file within the PostgreSQL data directory. For example**:** `/var/lib/pgsql/<version>/data/pg_hba.conf`.

pg_hba.confCopyhostssl all all 0.0.0.0/0 scram-sha-256

In the above example, all source addresses from MetaDefender Cluster and MetaDefender Core services are permitted. Refer [here](https://www.postgresql.org/docs/9.1/auth-pg-hba-conf.html) for more details.

2. Locate and modify the `postgresql.conf` configuration file within the PostgreSQL data directory. For example: `/var/lib/pgsql/<version>/data/postgresql.conf`.

postgresql.confCopylisten_addresses = '*'

The configuration above directs PostgreSQL server to permit incoming connections from all sources associated with MetaDefender Cluster and MetaDefender Core services**.** Learn more from [here](https://www.postgresql.org/docs/9.1/runtime-config-connection.html).
