<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/postgresql-fails-to-start-after-upgrade-when-ssl-is-enabled -->

# PostgreSQL fails to start after upgrade when SSL is enabled

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This issue may occur only when upgrading MetaDefender Core from a version **prior to 5.22.0 to version 5.22.0 or later**, on deployments **where SSL is enabled for the bundled PostgreSQL database**.

It can be resolved with a configuration change, and no re-installation is required.

### [Overview](/docs/mdcore/troubleshooting/postgresql-fails-to-start-after-upgrade-when-ssl-is-enabled#overview)

After upgrading MetaDefender Core from a version earlier than 5.22.0 to 5.22.0 or later, the bundled PostgreSQL service may fail to start if SSL was previously enabled for it without an `ssl_groups` setting. MetaDefender Core then cannot reach its database.

This applies only to standalone deployments that use the bundled PostgreSQL.

### [Symptoms](/docs/mdcore/troubleshooting/postgresql-fails-to-start-after-upgrade-when-ssl-is-enabled#symptoms)

- The upgrade completes and the package reports as installed, but the Web Console is not usable after the upgrade
- Sign-in requests fail with HTTP `500`, while `GET /version` still answers with the new version
- The MetaDefender Core log contains the following errors:

  [ERROR ] (core.postgres) Postgres issue, error='Starting postgres service failed', param='pg_ctl: could not start server
  Examine the log output.
  '
  [ERROR ] (core.postgres) Postgres issue, error='Failed to restart PostgreSQL under FIPS after cluster upgrade'
  [ERROR ] (common.base) Unhandled internal exception occurred in a slot, message='Failed to re-engage FIPS for the bundled PostgreSQL after cluster upgrade
- Starting PostgreSQL manually reports the following error:

  FATAL: could not set group names specified in ssl_groups: No valid groups found
  HINT: Ensure that each group name is spelled correctly and supported by the installed version of OpenSSL.

### [Root Cause](/docs/mdcore/troubleshooting/postgresql-fails-to-start-after-upgrade-when-ssl-is-enabled#root-cause)

From MetaDefender Core 5.22.0, the bundled PostgreSQL ships with a FIPS 140-3 validated OpenSSL module, and non-approved algorithms such as X25519 are not available to the database server. The PostgreSQL default for `ssl_groups` is `X25519:prime256v1`, so a PostgreSQL SSL configuration that does not set `ssl_groups` makes the service fail to start.

SSL configurations created for earlier versions do not contain `ssl_groups`. The upgrade keeps that configuration file, and PostgreSQL fails to start with it when the upgrade restarts the database.

### [Solution](/docs/mdcore/troubleshooting/postgresql-fails-to-start-after-upgrade-when-ssl-is-enabled#solution)

1. Open the PostgreSQL SSL configuration file (the file that contains `ssl = on`) in the PostgreSQL folder:

   - **Windows:** `<installation folder>/postgres/`
   - **Linux:** `/usr/lib/ometascan/postgres/`
2. Correct the setting named in the error:
   `ssl_groups`: set a FIPS-approved group
   For example:

   ssl = on
   ssl_groups = 'prime256v1'
   ssl_ciphers = 'HIGH:MEDIUM:+3DES:!aNULL'
   ssl_prefer_server_ciphers = on
   ssl_cert_file = '<absolute_path_to_cert_file>'
   ssl_key_file = '<absolute_path_to_key_file>'
   ssl_ca_file = '<absolute_path_to_root_ca_cert_file>'

3. Restart the MetaDefender Core service:

   # Use systemctl
   systemctl restart ometascan
   # Or use service
   service ometascan restart
