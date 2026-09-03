<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine -->

# Migrate MetaDefender Core from one machine to another machine

### [Environment: Windows - Standalone mode - Local (Bundle) PostgreSQL server](/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine#environment-windows---standalone-mode---local-bundle-postgresql-server)

### [Goal: Move as much as possible (the data) from one machine to another machine](/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine#goal-move-as-much-as-possible-the-data-from-one-machine-to-another-machine)

- PG database data
- Log files
- Sanitized/DLP processed files
- Quarantine files
- etc

### [Some aspects need to be checked before and after the upgrade](/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine#some-aspects-need-to-be-checked-before-and-after-the-upgrade)

- Registry
- Sanitized/DLP/Quarantine path
- Custom directory
- Custom log directory
- External scanner/ Post-action configuration file paths
- Certificated paths
- SSL PostgreSQL: certificate path
- Configure HTTPS via ssl.conf file
- Sanitized/DLP/Quarantined files: can be downloaded
- Custom local folder for module updates
- Try to restart MetaDefender Core service

## [Steps by steps](/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine#steps-by-steps)

Let's call the old (current server) Server A and the new server will be Server B

Have tested with MetaDefender Core 5.6.0

#### [I. Server A](/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine#i-server-a)

1. Stop MetaDefender Core service)and make sure MetaDefender Core is successfully stopped.
2. If you have any custom configuration on the registry (custom log file, custom temp dir etc): you need to export the registry config (if not please ignore this step):

   1. Open the registry editor, go `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan`
   2. Export the registry config

3. Compress MetaDefender Core’s installation directory to a zip file named *MetaDefender Core.zip*

- For example: Compress whole folder `c:\Program Files\OPSWAT\MetaDefender Core\`

4. You also might need to compress/backup the data (if have any) in the custom folder:

Info

If you do not have any custom configured path, please ignore this step

- Custom log files folder
- Custom quarantine folder
- Custom sanitized files folder
- etc

#### [II. Server B](/docs/mdcore/troubleshooting/migrate-metadefender-core-from-one-machine-to-another-machine#ii-server-b)

1. Install MetaDefender Core with the same version and same installation path as MetaDefender Core A.
2. Stop MetaDefender Core service and make sure MetaDefender Core is successfully stopped.
3. Import registry that is exported from Server A (Step I.2).
4. Remove the MetaDefender Core's installation directory: `rd /s /q "C:\Program Files\OPSWAT\MetaDefender Core"`
5. Copy and extract the zip package of MetaDefender Core A (*MetaDefender Core.zip*) to *the new* MetaDefender Core’s installation path (default is `C:\Program Files\OPSWAT`)
6. Copy/move the backup files (which were backup at step I.4) to the desired location.
7. Start MetaDefender Core service, login, and activate the license.
