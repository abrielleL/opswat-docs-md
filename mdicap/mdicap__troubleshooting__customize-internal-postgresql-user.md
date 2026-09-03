<!-- source: https://www.opswat.com/docs/mdicap/troubleshooting/customize-internal-postgresql-user -->

# Customize Internal PostgreSQL User

MetaDefender ICAP Server once installed, it will automatically create an internal PostgreSQL user for operation purpose, and so far that user name is auto randomized by MetaDefender ICAP Server and non adjustable (`usr_<random characters>`).

Now MetaDefender ICAP Server supports database system admin to define and change to their own PostgreSQL user instead.

That can be done in both deployment scenarios:

1. Product installation (pre-setup)
2. Product configuration (post-setup)

Notes and limits

1. Internal PG username has to be matched with Postgresql naming conventions <https://www.postgresql.org/docs/12/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS>
2. We support backup/restore credential files mechanism. In case of customizing PostgreSQL user failure, the old credential file will be restored.
3. Currently we do not support internal PostgreSQL user contains backslash(), double quotes (“), it cannot begin with digits (0-9) and length must be less than 64 bytes
## [Product installation (pre-setup)](https://docs.opswat.com/mdcore/troubleshooting/customize-internal-postgresql-user#product-installation-pre-setup)

In the ignition file, there are 2 keys needed for this user setup:

- dbserver/private_username
- dbserver/private_password

Info

1. If `private_username` is not on the Postgres server, MetaDefender ICAP Server creates an internal user.
2. If `private_username` matches the user of the Postgres server. The user on the Postgres is overridden, MetaDefender ICAP Server doesn’t create a new internal user.
## [Product configuration (post-setup)](https://docs.opswat.com/mdcore/troubleshooting/customize-internal-postgresql-user#product-configuraton-post-setup)

Using the CLI tool bundled with MetaDefender ICAP Server to modify PostgreSQL internal user while MetaDefender ICAP Server is running:

- Windows: C:\Program Files\OPSWAT\Metadefender ICAP Server\mdicapsrv-custom-internal-pg-user.exe
- Linux: /usr/sbin/mdicapsrv-custom-internal-pg-user

You can switch to other user with password optionally:

BashCopymdicapsrv-custom-internal-pg-user [-c <PATH TO CONFIG DB>] -nu <NEW USERNAME> [-np <NEW PASSWORD>]

or you can drop the current user

BashCopymdicapsrv-custom-internal-pg-user [-c <PATH TO CONFIG DB>] -r

All options and arguments:

- -h\t: (--help) instruction
- -c\t: (--configuration-path) default value: HKEY_LOCAL_MACHINE\Software\OPSWAT\Metadefender ICAP Server on Windows or /etc/mdicapsrv/mdicapsrv.conf on Linux
- -nu\t: (--new-username) New username must be started with usr_
- -np\t: (--new-password) new password
- -r\t: (--remove-current-user) remove your current user
