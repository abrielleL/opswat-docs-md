<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-upgrade-to-metadefender-icap-server-5-2-0-or-newer- -->

# How to upgrade to MetaDefender ICAP Server 5.2.0 or newer?

Starting with ICAP version 5.2.0 we have a new Database Management System (PostgreSQL) to replace SQLite.

Database Migration will be happened when you install MetaDefender ICAP Server v5.2.0 or newer on a host which has already installed older MD ICAP Server version.

Two options for migration:

1. Do not migrate ICAP history (only migrate workflow rules, setting, user management,..)
2. Migrate all database(include ICAP history)

The upgrade process may take a long time depending on the size of the ICAP history database.

Please note that if you try to use the Use your existing PostgreSQL server option you will be asked for credentials and will receive an *Invalid credential* error message.

More details about upgrading to MetaDefender ICAP Server 5.2.0 or newer can be found here: auto$

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
