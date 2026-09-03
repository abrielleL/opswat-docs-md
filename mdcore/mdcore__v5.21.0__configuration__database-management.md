<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/database-management -->

# Database Management

Starting MetaDefender Core 4.20.1, we have supported users to update PostgreSQL server information.

It could be done via either MetaDefender Core management console or separate CLI tool.

- [MetaDefender Core management console](/docs/mdcore/v5.21.0/configuration/database-management#metadefender-core-management-console)
- [CLI tool (ometascan-change-db-credentials)](/docs/mdcore/v5.21.0/configuration/database-management#cli-tool-ometascan-change-db-credentials)

## [MetaDefender Core management console](/docs/mdcore/v5.21.0/configuration/database-management#metadefender-core-management-console)

Navigate to Settings → Network

You are required to setup PIN code first before changing the database information.

Info

- Local (Bult-in) PostgreSQL database setup: Only admin user credentials option displayed on the UI and allowed for modification.
- Remote PostgreSQL database setup: Both admin user credentials and database information (IP address and port) options displayed on the UI and allowed for modification.
## [CLI tool (ometascan-change-db-credentials)](/docs/mdcore/v5.21.0/configuration/database-management#cli-tool-ometascan-change-db-credentials)

The tool could be used when you somehow lost the PostgreSQL database connection and could not access to the MetaDefender Core management console UI.

The tool could be located at:

- Windows: <MetaDefender Core installation folder>\ometascan-change-db-credentials.exe
- Linux: /usr/sbin/ometascan-change-db-credentials

Info

The CLI tool requires admin/root privilege to run.

Make sure to stop following services yourself before running the tool (by doing so, you also confirm all active scanning activities are stopped so this modification will not impact to your production scanning service)

- MetaDefender Core (ometascan)
- MetaDefender Core PostgreSQL (Windows: ometascan-postgresql, Linux: ometascan-pg)

Upon the tool finsihed, you may need to double check to start those services back if not running.

CLI tool parameters:

ometascan-change-db-credentials.exe -h
 
Usage: ometascan-change-db-credentials.exe [options]
MetaDefender Core Change DB Credentials.
 
Options:
-?, -h, --help Displays this help.
-s, --skppassword Only change database credentials at Core side, do not
change user password at PostgreSQL server

By default, this CLI tool will help change the PostgreSQL database admin credentials on both MetaDefender Core and PostgreSQL server sides. If you do not want to change the password on PostgreSQL server side, make sure you will use “-s” parameter.

Info

- Local (Bult-in) PostgreSQL database setup: Only admin user credentials option displayed and allowed for modification.
- Remote PostgreSQL database setup: Both admin user credentials and database information (IP address and port) options displayed and allowed for modification.
