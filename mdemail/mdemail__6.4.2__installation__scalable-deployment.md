<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/installation/scalable-deployment -->

# Scalable deployment

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/installation/scalable-deployment#overview)

In a scalable deployment Email Gateway Security instances work on a shared database.

Eliminate single point of failure

The shared database can be a single point of failure in a scalable deployment. The solution is to set up a PostgreSQL database cluster that provides high availability for the database. For details see <https://www.postgresql.org/docs/current/high-availability.html>.

The database runs either on one of the the Email Gateway Security instances

or as a separate database server

All (the other) instances connect to the shared database.

For details about scalable deployment see [Scalable deployment operation](/docs/mdemail/6.4.2/operating/scalable-deployment-operation).

## [Installation](/docs/mdemail/6.4.2/installation/scalable-deployment#installation)

### [Shared database on an Email Gateway Security instance](/docs/mdemail/6.4.2/installation/scalable-deployment#shared-database-on-an-email-gateway-security-instance)

PostgreSQL restricted to localhost

By default, Email Gateway Security installed in the *Standalone* mode will restrict its PostgreSQL database to be accessible from localhost only.

PostgreSQL need to be configured specifically to allow connections from remote hosts. For details see below.

Embedded database performance

The embedded PostgreSQL database is primarily designed for testing and low-volume deployments, and is not recommended for heavy load environments.

For reliable and secure operation, a robust external PostgreSQL database cluster solution is recommended.

1. When the shared database is intended to be on one of the Email Gateway Security instances, install this instance first.

   1. In the *Choose Database Setup Type* dialog select the *Standalone* option and complete the setup of the first instance.

2. For all other instances in the *Choose Database Setup Type* dialog select the *External database* option.
3. In the database properties dialog set the *Address* and *Port* of the first instance and provide the database *Username* and *Password* set for the first instance.

4. Configure PostgreSQL to accept connections from other hosts

   1. In `<installation directory>\data\pg_data\postgresql.conf` (default `C:\Program Files\OPSWAT\MetaDefender Email Security\data\pg_data\postgresql.conf`) configure `listen_addresses` to listen on addresses accessible for other hosts. For details see <https://www.postgresql.org/docs/14/runtime-config-connection.html>.

      1. Example: `listen_addresses = '*'`
   2. In `<installation directory>\data\pg_data\pg_hba.conf` (default `C:\Program Files\OPSWAT\MetaDefender Email Security\data\pg_data\pg_hba.conf`) add entry to allow authentication from other hosts. For details see <https://www.postgresql.org/docs/14/auth-pg-hba-conf.html>.

      1. Example: `host all postgres 172.0.0.0/8 scram-sha-256`
   3. Allow PostgreSQL port (default 5433) through the firewall.
   4. Restart PostgreSQL

      1. Example:

         1. `net stop postgresql-x64-14`
         2. `net start postgresql-x64-14`

### [Shared external database](/docs/mdemail/6.4.2/installation/scalable-deployment#shared-external-database)

1. The shared database must be up and running before the first Email Gateway Security instance is about to be installed.
2. For all instances in the *Choose Database Setup Type* dialog select the *External database* option.

3. In the database properties dialog set the *Address* and *Port* of the shared external database server and provide the shared database *Username* and *Password*.
