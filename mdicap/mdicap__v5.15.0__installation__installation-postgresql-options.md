<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/installation-postgresql-options -->

# PostgreSQL Database Deployment Options

View as Markdown Ask ChatGPT about this page Ask Claude about this page PostgreSQL user credentials

Unicode characters are NOT supported for "Username" and "Password"

"Password" does not accept # (hash) as starting character (e.g. #ABC)

Mapping between ICAP Version and require PostgreSQL version

| ICAP Version | bundle PostgreSQL version | Support PostgreSQL external version |
| --- | --- | --- |
| v5.15.0 | 16.14 | 14.x, 15.x, 16.x, 17.x, 18.x |
| v5.14.0 - > v5.14.1 | 16.13 | 12.x, 14.x, 15.x, 16.x, 17.x, 18.x |
| v5.13.0 | 16.13 | 12.x, 14.x, 15.x, 16.x, 17.x |
| v5.12.0 | 16.10 | 12.x, 14.x, 15.x, 16.x, 17.x |
| v5.9.0 -> v5.11.0 | 16.8 | 12.x, 14.x, 15.x, 16.x, 17.x |
| v5.9.0 | 16.8 | 12.x, 14.x, 15.x, 16.x, 17.x |
| v5.8.0 | 16.6 | 12.x, 14.x, 15.x, 16.x, 17.x |
| v5.7.0 | 16.6 | 12.x, 14.x, 15.x, 16.x, 17.x |
| v5.6.0 | 12.20 | 12.x, 14.x, 15.x |
| v5.5.1 | 12.18 | 12.x, 14.x (ICAP Linux only), 15.x (ICAP Linux only) |
| v5.5.0 | 12.18 | 12.x, 14.x (ICAP Linux only), 15.x (ICAP Linux only) |
| v5.4.0 | 12.14 | 12.x, 14.x (ICAP Linux only), 15.x (ICAP Linux only) |
| v5.3.0 | 12.14 | 12.x, 14.x (ICAP Linux only), 15.x (ICAP Linux only) |
| v5.2.1 | 12.14 | 12.x, 14.x (ICAP Linux only), 15.x (ICAP Linux only) |
| v5.2.0 | 12.14 | 12.x, 14.x (ICAP Linux only), 15.x (ICAP Linux only) |

## [1.Database Type](/docs/mdicap/v5.15.0/installation/installation-postgresql-options#1database-type)

### [1.1.Local (Bundle) PostgreSQL server](/docs/mdicap/v5.15.0/installation/installation-postgresql-options#11local-bundle-postgresql-server)

MetaDefender ICAP Server will install a new PostgreSQL server locally in the same box with the product.

### [1.2.Remote (Existing) PostgreSQL server](/docs/mdicap/v5.15.0/installation/installation-postgresql-options#12remote-existing-postgresql-server)

MetaDefender ICAP Server will connect to remote pre-installed PostgreSQL running remotely.

PostgreSQL user privilege requirements

MetaDefender ICAP Server. will need to create and use dedicated PostgreSQL users for database setup, upgrade and its own operations. Those users requires certain privileges configured on PostgreSQL server, otherwise expecting failures to occur while installing and operating MetaDefender ICAP Server.

Details: [PostgreSQL User Privilege Requirements](/docs/mdicap/v5.15.0/troubleshooting/postgresql-user-privilege-requirements)

## [2.Database Mode](/docs/mdicap/v5.15.0/installation/installation-postgresql-options#2database-mode)

### [2.1.Standalone Database Mode](/docs/mdicap/v5.15.0/installation/installation-postgresql-options#21standalone-database-mode)

Each MetaDefender ICAP Server will have owner database, the database name of each instance will be generated automatically with format: metadefender_icap_ <first 6 deployment id character with out prefix>

### [2.2.Shared Database Mode](/docs/mdicap/v5.15.0/installation/installation-postgresql-options#22shared-database-mode)

All MetaDefender ICAP Server instances can share the same external database.

That helps auto-sync all product configurations (except Single-Sign-On that requires unique settings for each MD ICAP Server), processing history, live/on-going scan result query, audit, statistics data.

Currently not supported

- Does not support to switch from shared database mode back to standalone database mode.
- Does not support to change instance_name of MetaDefender ICAP server in shared database deployment model after installation.
- Does not support to upgrade multiple MetaDefender ICAP server instances at once in shared database mode
- - Stop all MD ICAP Server instances service before performing the upgrade.
  - Upgrade each MD ICAP Server server one by one instead.
  - For each MD ICAP Server, when the upgrade finished, then you can start using that ICAP instance without waiting for the other ICAP instances’ upgrade to be done.
Requirements for shared database setup

- The central remote PostgreSQL server (for shared database) could be utilized with a built-in (native) PostgreSQL database server installed with one of the MetaDefender ICAP Server instances in the network. Or using a dedicated existing PostgreSQL database server (version 12.14 is recommended).
- Before setting up, make sure to follow steps at [Open Connection On PostgreSQL Server](/docs/mdicap/v5.15.0/troubleshooting/open-connection-on-postgresql-server) so that all MetaDefender ICAP Server instances could connect to the central remote PostgreSQL server.
- MetaDefender ICAP Server will need to create and use dedicated PostgreSQL users for database setup, upgrade and its own operations. Those users requires certain privileges configured on PostgreSQL server, otherwise expecting failures to occur while installing and operating MetaDefender ICAP Server , details: [PostgreSQL User Privilege Requirements](/docs/mdicap/v5.15.0/troubleshooting/postgresql-user-privilege-requirements)
