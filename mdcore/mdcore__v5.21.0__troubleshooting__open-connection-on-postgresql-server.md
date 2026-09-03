<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/open-connection-on-postgresql-server -->

# Open Connection On PostgreSQL Server

Applicable to use cases where users want to use a PostgreSQL server sitting on a different server from where MetaDefender Core resides.

Info

Just in case the firewall is enabled, please also make sure to configure your firewall rule properly for the connections between PostgreSQL server and MetaDefender Core.

Info

The guide here assumes we are using an SSL connection with PostgreSQL. With a non-SSL connection, please use host instead of hostssl

## [Windows](/docs/mdcore/v5.21.0/troubleshooting/open-connection-on-postgresql-server#windows)

1.) Modify **C:\Program Files\OPSWAT\MetaDefender Core\data\pg_data\pg_hba.conf**

(**If that’s a separate PostgreSQL server, then you should find it in the PostgreSQL data directory instead**)

hostssl all all 0.0.0.0/0 scram-sha-256

In the above example, it means to accept any MetaDefender Core machine source address. Learn more at: <https://www.postgresql.org/docs/9.1/auth-pg-hba-conf.html>

2.) Create a new file **C:\Program Files\OPSWAT\MetaDefender Core\postgres\postgresql.conf**

(**If that’s a separate PostgreSQL server, then you can find it in the PostgreSQL data directory instead**)

listen_addresses = '*'

In the above example, it means to ask the PostgreSQL server to start listening for all MetaDefender Core source connections. Learn more at <https://www.postgresql.org/docs/9.1/runtime-config-connection.html>

3.) Restart **ometascan-postgres** service

## [Linux](/docs/mdcore/v5.21.0/troubleshooting/open-connection-on-postgresql-server#linux)

1.) Modify **/var/lib/ometascan/pg_data/pg_hba.conf**

(**If that’s a separate PostgreSQL server, then you can find it in the PostgreSQL data directory instead**)

hostssl all all 0.0.0.0/0 scram-sha-256

2.) Create a new file **/usr/lib/ometascan/postgres/postgresql.conf**

(**If that’s a separate PostgreSQL server, then you can find it in the PostgreSQL data directory instead**)

listen_addresses = '*'

3.) Restart **ometascan-postgres** service
