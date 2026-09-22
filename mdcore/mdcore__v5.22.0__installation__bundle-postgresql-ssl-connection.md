<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/bundle-postgresql-ssl-connection -->

# Enabling SSL Connections for PostgreSQL via ignition file

## [Overview](/docs/mdcore/v5.22.0/installation/bundle-postgresql-ssl-connection#overview)

Starting with MetaDefender Core version 5.16.0, users can optionally enable SSL connections for the bundled PostgreSQL database during installation using the ignition file. This feature enhances security by encrypting data transmissions between the application and the database.

Key Considerations

- This feature applies exclusively to the bundled PostgreSQL database.
- It is available only for automated deployments via the ignition file.
- **Enabling the SSL connection has overhead and might impact the performance in general.**
- It does not apply during upgrades of MetaDefender Core.
- SSL connections can be disabled by customers at any time post-installation.
- This configuration is not supported in Docker environments.
## [Setting Up SSL Connections](/docs/mdcore/v5.22.0/installation/bundle-postgresql-ssl-connection#setting-up-ssl-connections)

Enabling SSL is an optional step performed during the installation of MetaDefender Core using the ignition file. In addition to preparing the ignition file, you must create a configuration file named `postgres_ssl.conf` in the following fixed location:

- **Windows:** `C:\opswat\postgres_ssl.conf`
- **Linux:** `/etc/opswat/postgres_ssl.conf`

The file must be placed exactly in this path for the installation process to detect and apply the settings.

### [Contents of the Configuration File](/docs/mdcore/v5.22.0/installation/bundle-postgresql-ssl-connection#contents-of-the-configuration-file)

The `postgres_ssl.conf` file should contain the following PostgreSQL SSL parameters. Replace the placeholders with the absolute paths to your certificate, key, and CA files:

BashCopyssl = on
ssl_groups = 'prime256v1'
ssl_ciphers = 'HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers = on
ssl_cert_file = '<absolute_path_to_cert_file>'
ssl_key_file = '<absolute_path_to_key_file>'
ssl_ca_file = '<absolute_path_to_root_ca_cert_file>'

For example, in Linux

BashCopyssl = on
ssl_groups = 'prime256v1'
ssl_ciphers = 'HIGH:MEDIUM:+3DES:!aNULL'
ssl_prefer_server_ciphers = on
ssl_cert_file = '/etc/tmp_cert/server.crt'
ssl_key_file = '/etc/tmp_cert/server.key'
ssl_ca_file = '/etc/tmp_cert/root.crt'

**FIPS 140-3 Compliant Configuration from MetaDefender Core 5.22.0**

From MetaDefender Core 5.22.0, the bundled PostgreSQL ships with a FIPS 140-3 validated OpenSSL module. On these versions, non-approved algorithms such as X25519 are unavailable to the database server regardless of configuration.

Please note that the PostgreSQL [default](https://www.postgresql.org/docs/18/runtime-config-connection.html) for `ssl_groups` is `X25519:prime256v1`, which is not supported on these deployments. Specify only approved groups in `postgres_ssl.conf` - if the configuration references an algorithm the module does not provide, the PostgreSQL service fails to start. This applies only to standalone deployments using the bundled PostgreSQL.

Users can store the cert/key files in any place, but please make sure that the cert/key files have the right permissions, so MetaDefender Core can copy them to the right location. For example, in Linux, the files need to have **read permission** for other users. Users can use this command in Linux to set the permissions

BashCopychmod 555 -R /path/to/store/cert_files/
# For example
chmod 555 -R /etc/tmp_cert/Additional Notes

During installation, the specified certificate file (server.crt), key file (server.key), and root CA file (root.crt) will be automatically copied to the PostgreSQL data directory:

- Windows: `<installation folder>/data/pg_data`
- Linux: `/var/lib/ometascan/pg_data`

Once the installation is complete and verified, you may safely delete the original files from their source locations if they are no longer needed.

## [How to disable bundled PostgreSQL SSL connection](/docs/mdcore/v5.22.0/installation/bundle-postgresql-ssl-connection#how-to-disable-bundled-postgresql-ssl-connection)

1. Go to `postgres` folder and remove the file `postgres_ssl.conf`

   1. Windows: `<installation folder>/postgres/postgres_ssl.conf`
   2. Linux: `/usr/lib/ometascan/postgres/postgres_ssl.conf`
2. Go to pg_data folder, remove the file `pg_hba.conf` then rename `pg_hba_bk.conf` to `pg_hba.conf`
3. Restart the MetaDefender Core PostgreSQL service.
