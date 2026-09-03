<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/troubleshooting/open-connection-on-postgresql-server -->

# Open Connection On PostgreSQL Server

Applicable to use-case where users want to use a remote PostgreSQL server sitting on a different server from where MetaDefender ICAP Server resides.

Info

Just in case the firewall is enabled, please also make sure to configure your firewall rule properly for the connections between PostgreSQL server and MetaDefender ICAP Server.

## [Windows](/docs/mdicap/v5.14.1/troubleshooting/open-connection-on-postgresql-server#windows)

1.) Modify C:\Program Files\OPSWAT\MetaDefender ICAP Server\data\pg_data\pg_hba.conf

(**If that’s a separate PostgreSQL server then you should find it in PostgreSQL data directory instead**)

host all all 0.0.0.0/0 password

In above example, it means to accept any MetaDefender ICAP Server machine source address. Learn more at: <https://www.postgresql.org/docs/9.1/auth-pg-hba-conf.html>

2.) Create new file **C:\Program Files\OPSWAT\MetaDefender ICAP Server\postgres\postgresql.conf**

(**If that’s a separate PostgreSQL server then you can find it in PostgreSQL data directory instead**)

BashCopylisten_addresses = '*'

In above example, it means to ask PostgreSQL server to start listening for all MetaDefender ICAP Server source connections. Learn more at <https://www.postgresql.org/docs/9.1/runtime-config-connection.html>

3.) Restart **mdicapsrv-postgres** service

## [Linux](/docs/mdicap/v5.14.1/troubleshooting/open-connection-on-postgresql-server#linux)

1.) Modify **/var/lib/mdicapsrv/pg_data/pg_hba.conf**

(**If that’s a separate PostgreSQL server then you can find it in PostgreSQL data directory instead**)

BashCopyhost all all 0.0.0.0/0 password

2.) Create new file **/usr/lib/ mdicapsrv /postgres/postgresql.conf**

(**If that’s a separate PostgreSQL server then you can find it in PostgreSQL data directory instead**)

BashCopylisten_addresses = '*'

3.) Restart **mdicapsrv-postgres** service
