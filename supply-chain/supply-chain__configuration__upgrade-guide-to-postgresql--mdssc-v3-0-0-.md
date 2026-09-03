<!-- source: https://www.opswat.com/docs/supply-chain/configuration/upgrade-guide-to-postgresql--mdssc-v3-0-0- -->

# Upgrade Guide to PostgreSQL (MDSSC v3.0.0)

### MDSSC v3.0.0 Upgrade Guide: MongoDB to PostgreSQL Migration

### Overview

Starting with MDSSC version 3.0.0, PostgreSQL replaces MongoDB as the primary database backend. This guide covers the upgrade process, migration scenarios, and the best practices for a seamless transition.

### Key Changes in v3.0.0

- **Database Backend**: PostgreSQL replaces MongoDB
- **External Database Support**: Improved support for external PostgreSQL instances

### Pre-Upgrade Considerations

> **Warning**
>
> When migrating from MongoDB to PostgreSQL, certain data types (including scans, workflows, packages, and related historical records) are not transferred and will not be available after the migration. Before proceeding, ensure that any critical information stored in the previous environment is backed up or exported according to your data-retention requirements. This behavior is expected and designed to provide a clean, optimized PostgreSQL-based system moving forward.

### Skipping Data Migration

Add the following line to your `customer.env`  file before upgrading:

```bash
SKIP_MONGO_TO_PG=yes
```

### External PostgreSQL Configuration

#### Recommended Providers

For production deployments, consider these managed PostgreSQL services for better performance, reliability and high availability options:

- **AWS RDS PostgreSQL**
- **Google Cloud SQL for PostgreSQL**
- **Azure Database for PostgreSQL**

#### Connection Configuration

To use an external PostgreSQL database, add the following to your `customer.env` file:

```bash
POSTGRESQL_URL=Host={your_pg_host};Port=5432;Username={your_pg_user};Password={your_pg_password};Database=MDSS
```

**Example configurations:**

```bash
# AWS RDS
POSTGRESQL_URL=Host=mdss-prod.cluster-xyz.us-east-1.rds.amazonaws.com;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS

# Google Cloud SQL
POSTGRESQL_URL=Host=10.1.2.3;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS

# Self-hosted with HA
POSTGRESQL_URL=Host=postgres-cluster.internal;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS
```

### Database Configuration Recommendations

#### Connection Limits

Ensure your PostgreSQL instance has adequate connection limits:

```sql
-- Recommended minimum for production
ALTER SYSTEM SET max_connections = 1000;
SELECT pg_reload_conf();
```

#### Performance Tuning

Consider these PostgreSQL settings for optimal MDSSC performance:

```sql
-- Memory settings (adjust based on your server capacity)
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
```

More details on configuring allocated resources on a PostgreSQL database can be found in the official documentation [here](https://www.postgresql.org/docs/current/runtime-config-resource.html).
