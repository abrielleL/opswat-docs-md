<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/postgresql-lost-connection-after-upgrade-on-cis-hardened-ubuntu -->

# PostgreSQL Connection Loss After Upgrade on CIS-Hardened Ubuntu

### [Overview](/docs/mdcore/v5.22.0/troubleshooting/postgresql-lost-connection-after-upgrade-on-cis-hardened-ubuntu#overview)

MetaDefender Core may lose PostgreSQL connectivity following an upgrade on Ubuntu systems with CIS (Center for Internet Security) hardening enabled.

### [Symptoms](/docs/mdcore/v5.22.0/troubleshooting/postgresql-lost-connection-after-upgrade-on-cis-hardened-ubuntu#symptoms)

- Web Console becomes inaccessible after completing a MetaDefender Core upgrade
- Error page displayed when attempting to access the Web Console

- The following error appears in the application logs:

BashCopy[ERROR ] 2025.08.14 03:20:11.504: (core.postgres) Postgres issue,
error='Starting postgres service failed',
param='Warning: Tt file, source configuration file or drop-ins of ometascan-pg.service changed on disk.
Run 'systemctl daemon-reload' to reload.
' [msgid: 4084]
### [Root Cause](/docs/mdcore/v5.22.0/troubleshooting/postgresql-lost-connection-after-upgrade-on-cis-hardened-ubuntu#root-cause)

This issue appears to be related to a systemctl behavior when CIS hardening is applied to the system. The exact cause is currently under investigation.

### [Solution](/docs/mdcore/v5.22.0/troubleshooting/postgresql-lost-connection-after-upgrade-on-cis-hardened-ubuntu#solution)

Restart the MetaDefender Core service:

BashCopy# Use systemctl
systemctl restart ometascan
# Or use service
service ometascan restart
### [Additional Notes](/docs/mdcore/v5.22.0/troubleshooting/postgresql-lost-connection-after-upgrade-on-cis-hardened-ubuntu#additional-notes)

- This issue is specific to CIS-hardened Ubuntu environments
- The service restart resolves the connectivity issue immediately
- No data loss or configuration changes are required
