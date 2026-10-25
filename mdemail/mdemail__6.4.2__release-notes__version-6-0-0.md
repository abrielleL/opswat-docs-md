<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/release-notes/version-6-0-0 -->

# Version 6.0.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Release date | Scope |
| --- | --- |
| 27th January, 2025 | Changing the database model from embedded database to database server. |

Migration from version 5.x.x not supported

Migration of data from the old embedded databases is not supported yet.

To avoid accidental over-installation, Email Gateway Security 6.0.0 installer won't run when it can detect an earlier version already installed. For details see [Installation](/docs/mdemail/6.4.2/installation/installation).

## [PostgreSQL database](/docs/mdemail/6.4.2/release-notes/version-6-0-0#postgresql-database)

With version 6.0.0, Email Gateway Security is changing its database from the embedded database [SQLite](https://www.sqlite.org) to the database server [PostgreSQL](https://www.postgresql.org).

Switching the database model is expected to help the product to scale out easily, support network based database, gain better performance, migrate high load bottleneck and provide native high availability. Email Gateway Security supports users to create a local PostgreSQL server running in the box, or allow leveraging a pre-installed remote PostgreSQL server.

High Availability

For high availability, a dedicated, preinstalled, highly available PostgreSQL database cluster is required. For details see <https://www.postgresql.org/docs/current/high-availability.html>.

### [Changes](/docs/mdemail/6.4.2/release-notes/version-6-0-0#changes)

#### [Prerequisites](/docs/mdemail/6.4.2/release-notes/version-6-0-0#prerequisites)

When using a pre-installed, remote PostgreSQL server, the database is a software dependency, and certain requirements apply.

For details please see the [Software](/docs/mdemail/6.4.2/installation/prerequisites#software) subsection in [Prerequisites](/docs/mdemail/6.4.2/installation/prerequisites).

#### [Installation](/docs/mdemail/6.4.2/release-notes/version-6-0-0#installation)

Standalone and scalable deployment

Email Gateway Security keeps supporting both standalone and scalable deployments. For details see [Standalone deployment](/docs/mdemail/6.4.2/installation/standalone-deployment) and [Scalable deployment](/docs/mdemail/6.4.2/installation/scalable-deployment) respectively.

**Database configuration**

During the installation process the administrator must choose what database type they want to use.

With the *Standalone* option, the installer will create a new, local PostgreSQL server running on the box. This option is for standalone deployments. For details see [Standalone deployment](/docs/mdemail/6.4.2/installation/standalone-deployment).

With the *External database* option, the installer will connect the Email Gateway Security instance to a pre-installed PostgreSQL server. This option is for scalable and highly available deployments. For details see [Scalable deployment](/docs/mdemail/6.4.2/installation/scalable-deployment).

For the *External database* option the connection test must pass for the installation process to continue.

For details see [Installation process](/docs/mdemail/6.4.2/installation/installation#installation-process).

**Existing earlier versions**

Email Gateway Security 6.0.0 installer will stop running when it can detect an earlier version already installed.

This way we try to protect existing 5.x.x installations from accidental over-installation as 6.0.0 can not yet migrate data from earlier versions.

#### [History database backup](/docs/mdemail/6.4.2/release-notes/version-6-0-0#history-database-backup)

With a separated, highly available database, the risk of losing email history and quarantine data can be better mitigated than with database backups. As the highly available database is now supported by Email Gateway Security, the *History database backup* functionality is no more necessary and has been removed.

For details about the history database backup in legacy versions see [https://www.opswat.com/docs/mdemail/5.7.5/operating/history-database-backup](https://www.opswat.com/docs/mdemail/5.7.4/operating/history-database-backup).

This change implies removing certain Registry entries. For details see the *Configuration changes* section below.

#### [Scalable deployment](/docs/mdemail/6.4.2/release-notes/version-6-0-0#scalable-deployment)

With the new database it has changed how Email Gateway Security instances share their database. For details see [Scalable deployment](/docs/mdemail/6.4.2/installation/scalable-deployment).

This change implies removing certain Registry entries. For details see the *Configuration changes* section below.

#### [Configuration changes](/docs/mdemail/6.4.2/release-notes/version-6-0-0#configuration-changes)

Registry root

In the registry configuration entries below */* denotes the *Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security* key.

For example */logger\logfile* stands for *Computer\HKEY LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\logger\logfile*.

**History database backup**

The following Registry entries have been removed:

1. */scheduled_db_optimization_time*
2. */internal\backup_directory*
3. */internal\enable_backup*

**Scalable deployment**

The following Registry entries have been removed:

1. */database\mode*
2. */database\server*
3. */database\port*

The following registry entries have been added:

1. */database\db_mode*
2. */database\db_port*
3. */database\db_hostname*
4. */database\dbuser name*
5. */database\max_connections*

For details see [Registry configuration](/docs/mdemail/6.4.2/configuration/registry-configuration).

### [Sharing database server with MetaDefender Core](/docs/mdemail/6.4.2/release-notes/version-6-0-0#sharing-database-server-with-metadefender-core)

As Email Gateway Security now supports using an external PostgreSQL database, it is now possible to use the PostgreSQL database of MetaDefender Core. For this scenario Email Gateway Security needs to be installed with the *External database* option and the database has to point to MetaDefender Core's database server.

For details see [Shared external database](/docs/mdemail/6.4.2/installation/scalable-deploymentf3k#shared-external-database).

### [PostgreSQL database cluster](/docs/mdemail/6.4.2/release-notes/version-6-0-0#postgresql-database-cluster)

For high availability, a dedicated, preinstalled, highly available PostgreSQL database cluster is required. For details see <https://www.postgresql.org/docs/current/high-availability.html>.
