<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/troubleshooting/customize-internal-postgresql-user -->

# Customize Internal PostgreSQL User

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

In public cloud environments, or when subject to customer-specific security requirements, password complexity policies may be enforced. This guide explains how to customize the internal PostgreSQL user passwords to ensure compliance with those security requirements.

MetaDefender Core once installed, it will automatically create an internal PostgreSQL user for operation purpose, and so far that user name is auto randomized by MetaDefender Core and non adjustable (`usr_<random characters>`).

Now MetaDefender Core supports database system admin to define and change to their own PostgreSQL user instead.

That can be done in both deployment scenarios:

1. Product installation (pre-setup)
2. Product configuration (post-setup)

Notes and limits

1. Internal PG username has to be matched with Postgresql naming conventions <https://www.postgresql.org/docs/7.0/syntax525.htm>.
2. We support backup/restore credential files mechanism. In case of customizing PostgreSQL user failure, the old credential file will be restored.
3. In SharedDB mode, each MetaDefender Core instance must have a different `private_username`. Otherwise, those instances cannot be started in a parallel way.
4. Currently we do not support internal PostgreSQL user contains special characters, space, uppercase. And it cannot begin with digits (0-9). Hyphens is supported.
## [Product installation (pre-setup)](/docs/mdcore/v5.22.1/troubleshooting/customize-internal-postgresql-user#product-installation-pre-setup)

In the ignition file, there are 2 keys needed for this user setup:

- dbserver/private_username
- dbserver/private_password

Info

1. If `private_username` is not on the Postgres server, MetaDefender Core creates an internal user.
2. If `private_username` matches the user of the Postgres server. The user on the Postgres is overridden, MetaDefender Corre doesn’t create a new internal user.
## [Product configuraton (post-setup)](/docs/mdcore/v5.22.1/troubleshooting/customize-internal-postgresql-user#product-configuraton-post-setup)

Using the CLI tool bundled with MetaDefender Core to modify PostgreSQL internal user while MetaDefender Core is running:

- Windows: C:\Program Files\OPSWAT\MetaDefender Core\ometascan-custom-internal-pg-user.exe
- Linux: /usr/sbin/ometascan-custom-internal-pg-user

You can switch to other user with password optionally:

BashCopyometascan-custom-internal-pg-user [-c <PATH TO CONFIG DB>] -nu <NEW USERNAME> [-np <NEW PASSWORD>]

or you can drop the current user:

BashCopyometascan-custom-internal-pg-user [-c <PATH TO CONFIG DB>] -r

All options and arguments:

- -h\t: (--help) instruction
- -c\t: (--configuration-path) default value: HKEY_LOCAL_MACHINE\Software\OPSWAT\Metascan on Windows or /etc/ometascan/ometascan.conf on Linux
- -nu\t: (--new-username) New username must be started with usr_
- -np\t: (--new-password) new password
- -r\t: (--remove-current-user) remove your current user
