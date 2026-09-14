<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/upgrade-to-postgresql -->

# Upgrade Guide to PostgreSQL (MDSS v4.0.0)

## [MDSS v4.0.0 Upgrade Guide: MongoDB to PostgreSQL Migration](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#mdss-v400-upgrade-guide-mongodb-to-postgresql-migration)

## [Overview](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#overview)

Starting with MDSS version 4.0.0, PostgreSQL replaces MongoDB as the primary database backend. This guide covers the upgrade process, migration scenarios, and best practices for a seamless transition.

## [Key Changes in v4.0.0](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#key-changes-in-v400)

- **Database Backend**: PostgreSQL replaces MongoDB
- **Automatic Migration**: Data is migrated by default during upgrade
- **External Database Support**: Improved support for external PostgreSQL instances

## [Pre-Upgrade Considerations](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#pre-upgrade-considerations)

### [When Data Migration Occurs](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#when-data-migration-occurs)

Data migration happens automatically when upgrading from any MDSS version < 4.0.0 and any of the following conditions are met:

- Previous version uses internal/bundled MongoDB
- New version is configured to use external PostgreSQL
- Both previous and new versions are configured with external databases

Warning

Data migration from MongoDB to PostgreSQL takes about **2-3 hours / 1M files** in the original database. In this time MDSS is not available for operation. Other upgrade options are available below.

### [When Data Migration is Skipped](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#when-data-migration-is-skipped)

Data migration is **automatically skipped** when all the following conditions are met:

- Previous version uses external MongoDB
- New version is configured with bundled PostgreSQL deployment

Info

⚠️ Important: This prevents unintentional migration of cloud/external data to local deployments.

Data migration is also skipped after a successful installation or upgrade of MDSS v4.0.0 on the same machine so that **data is migrated only once**. This is done in order to ensure data in MDSS v4.0.0 is not overwritten by an unintentional migration from an older version.

## [Upgrade Options](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#upgrade-options)

### [Option 1: Standard Upgrade with Migration](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#option-1-standard-upgrade-with-migration)

**Recommended for**: Small to medium deployments where historical data is required.

1. **Backup your current deployment**
2. **Upgrade to v4.0.0** using your standard deployment process
3. **Monitor the migration** - duration depends on data volume

**Configuration**: No additional configuration needed for default migration.

### [Option 2: Skip Data Migration](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#option-2-skip-data-migration)

**Recommended for**: Large deployments or when historical data is not critical.

Add the following to your `customer.env` file before upgrading:

BashCopySKIP_MONGO_TO_PG=yesInfo

💡 Time Savings: For large datasets, migration can take several hours. Skipping migration provides immediate availability of the new version.

### [Option 3: Blue-Green Deployment](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#option-3-blue-green-deployment)

**Recommended for**: Production environments requiring zero downtime and maximum safety.

**Process:**

1. **Deploy v4.0.0 in parallel** to your existing environment **without starting any scans**
2. **Configure the new deployment** with the same settings as the old one
3. **Test thoroughly** without activating storage processing
4. **Stop storage processing** on the old version (while keeping it running for rollback capability)
5. **Activate storage processing** on the new v4.0.0 deployment
6. **Monitor the new deployment** for proper functionality
7. **Decommission old environment** after validation period

Benefits:

- Controlled transition of storage processing
- Easy rollback by reversing the process
- No data migration time
- Fresh start with optimized database
- Prevents duplicate storage scanning

## [External PostgreSQL Configuration](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#external-postgresql-configuration)

### [Recommended Providers](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#recommended-providers)

For production deployments, consider these managed PostgreSQL services for better performance, reliability and high availability options:

- **AWS RDS PostgreSQL**
- **Google Cloud SQL for PostgreSQL**
- **Azure Database for PostgreSQL**

### [Connection Configuration](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#connection-configuration)

To use an external PostgreSQL database, add the following to your `customer.env` file:

BashCopyPOSTGRESQL_URL=Host={your_pg_host};Port=5432;Username={your_pg_user};Password={your_pg_password};Database=MDSS

**Example configurations:**

BashCopy# AWS RDS
POSTGRESQL_URL=Host=mdss-prod.cluster-xyz.us-east-1.rds.amazonaws.com;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS
# Google Cloud SQL
POSTGRESQL_URL=Host=10.1.2.3;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS
# Self-hosted with HA
POSTGRESQL_URL=Host=postgres-cluster.internal;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS
### [Database Configuration Recommendations](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#database-configuration-recommendations)

#### [Connection Limits](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#connection-limits)

Ensure your PostgreSQL instance has adequate connection limits:

SqlCopy-- Recommended minimum for production
ALTER SYSTEM SET max_connections = 1000;
SELECT pg_reload_conf();
#### [Performance Tuning](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#performance-tuning)

Consider these PostgreSQL settings for optimal MDSS performance:

SqlCopy-- Memory settings (adjust based on your server capacity)
ALTER SYSTEM SET shared_buffers = '8GB'; -- for best performance set to about 1/4 of total available memory
ALTER SYSTEM SET effective_cache_size = '16GB'; -- for best performance set to about 1/2 of total available memory
ALTER SYSTEM SET work_mem = '256MB';
ALTER SYSTEM SET temp_buffers = '64MB';
ALTER SYSTEM SET maintenance_work_mem = '2GB';
-- WAL (Write-Ahead Logging) configuration
ALTER SYSTEM SET wal_level = 'minimal';
ALTER SYSTEM SET max_wal_senders = 0;
ALTER SYSTEM SET max_replication_slots = 0;
ALTER SYSTEM SET max_wal_size = '2GB';
ALTER SYSTEM SET min_wal_size = '160MB';
-- Connection and logging
ALTER SYSTEM SET log_statement = 'none';
ALTER SYSTEM SET log_min_duration_statement = 1000;

More details on configuring allocated resources on a PostgreSQL database can be found in their official documentation [here](https://www.postgresql.org/docs/current/runtime-config-resource.html).

## [What Gets Migrated](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#what-gets-migrated)

- User accounts and permissions
- Configuration settings
- Historical data and logs
- Custom configurations
- Dashboards and reports
- Storages

Warning

**Special attention** on Real Time Processing, Storage Remediations and Scan Configurations migration.

The idea of Workflow is the result of merging Scan Configuration and Storage remediations. To not lose any remediations from storage, a Workflow shall be created starting from Default Scan Configuration and appending the Storage Remediations.

Remediation of DeepCdr with encrypt original will be migrated to Keep Allowed and Keep Blocked for the original file

The existent Scan Configuration will be migrated with only Keep Allowed and Keep Blocked remediations which are the defaults.

Real Time Processing shall be migrated using the new Workflow created from that specific storage

## [Troubleshooting](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#troubleshooting)

**Connection Issues**

BashCopy# Verify PostgreSQL connectivity
psql -h your-host -p 5432 -U mdss -d MDSS -c "SELECT version();"
### [Rollback Procedure on Linux](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#rollback-procedure-on-linux)

If you need to rollback after upgrade:

1. **Set** in `customer.env`: `ENV_IMAGE_TAG=stable3.6.1`
2. **Run the update command: sudo mdss -u update**
3. **Verify connectivity** to your original MongoDB database
4. **Confirm functionality** and data integrity

In order to perform the rollback on an offline deployment you need to (re)deploy the docker offline toolkit for version 3.6.1.

### [Rollback Procedure on Windows](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#rollback-procedure-on-windows)

If you need to rollback on a Windows deployment:

1. Stop MDSS
2. Backup the MongoDB data folder: `C:\Program Files\OPSWAT\MetaDefender Storage Security\data\mongo` - preferably before upgrading to v4.0.0 but this folder should be kept even after an upgrade
3. Uninstall MDSS 4.0.0
4. Install MDSS 3.6.1
5. Stop MDSS (after the installation is complete it start automatically)
6. Replace the MongoDB data folder with the previously created backup.
7. Start MDSS

### [Running the data migration manually](/docs/mdss/4.4.2/configuration/upgrade-to-postgresql#running-the-data-migration-manually)

In order to migrate the data from an older MongoDB database and overwrite any existing data in the new PostgreSQL database:

1. Clear the **SKIP_MONGO_TO_PG** variable from the `.env` and `customer.env` files and from the system environment variables (Windows only)
2. Delete the PostgreSQL data docker volume `mdss_postgres_data` (Linux only): `docker volume rm`mdss_postgres_data``
3. Restart MDSS v4.0.0

Info

💡 Notes:

- The migration process doesn't modify your original MongoDB database, so rollback is straightforward by reverting to the previous MDSS version.
- Modifications performed after the upgrade will not be kept after the rollback.
- Rollback is only supported to version 3.6.1.
Warning

The only backup of the original MongoDB database is in the original docker volume called **mdss_*****mongo***_**db. Uninstalling MDSS or performing any cleanup operations will delete this volume permanetly.**__
