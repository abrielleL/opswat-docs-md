<!-- source: https://www.opswat.com/docs/supply-chain/sizing-guide/managed-services-configuration-in-aws -->

# Managed Services configuration in AWS

Software Supply Chain comes bundled with 3rd party services that can be replaced with AWS managed equivalents. Below are the steps on how to configure each of the AWS services in MDSSC.

## PostgreSQL -> Amazon RDS

> **Related**
>
> See [AWS RDS with PostgreSQL](https://www.opswat.com/docs/supply-chain/configuration/database-procedures) for full deployment and connection instructions.

- TLS can be disabled in the cluster parameter group, otherwise the RDS tls certificate will need to be loaded in MDSSC using the `/etc/mdssc/ca_certificates` directory

### [Connection Configuration](https://www.opswat.com/docs/mdss/configuration/upgrade-to-postgresql#connection-configuration)

After creating a DocumentDB instance in AWS, its connection string can be added in the MDSSC configuration file `/etc/mdssc/customer.env` as it appears in the “Connect“ section:

```bash
POSTGRESQL_URL=Host={your_pg_host};Port=5432;Username={your_pg_user};Password={your_pg_password};Database=MDSS
```

**Example configurations:**

```bash
# AWS RDS
POSTGRESQL_URL=Host=mdssc-prod.cluster-xyz.us-east-1.rds.amazonaws.com;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS

# Google Cloud SQL
POSTGRESQL_URL=Host=10.1.2.3;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS

# Self-hosted with HA
POSTGRESQL_URL=Host=postgres-cluster.internal;Port=5432;Username=mdss;Password=SecurePassword123;Database=MDSS
```

### [Database Configuration Recommendations](https://www.opswat.com/docs/mdss/configuration/upgrade-to-postgresql#database-configuration-recommendations)

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

More details on configuring allocated resources on a PostgreSQL database can be found in their official documentation [here](https://www.postgresql.org/docs/current/runtime-config-resource.html).

## Redis -> Amazon ElastiCache

After creating a new Redis cache in Amazon ElastiCache, its `Configuration endpoint` can be added in the MDSSC configuration file `/etc/mdssc/.env` as it appears in the “Cluster details“ section:

```bash
CACHE_SERVICE_URI=<redis_hostname>.cache.amazonaws.com:6379
CACHE_SERVICE_URL=<redis_hostname>.cache.amazonaws.com
CACHE_SERVICE_PORT=6379
```

`CACHE_SERVICE_URL` and `CACHE_SERVICE_PORT` also need to be configured for MDSSC to check connectivity to the service before starting up.

## RabbitMQ -> Amazon MQ

After creating a new Amazon MQ instance, its `Endpoint` can be added in the MDSSC configuration file `/etc/mdssc/.env` as it appears in the “Connections“ section:

```bash
RABBITMQ_URI=amqps://<username>:<password>@<amazon_mq_hostname>.amazonaws.com:5671
RABBITMQ_HOST=<amazon_mq_hostname>.amazonaws.com:5671
RABBITMQ_PORT=5671
```

`RABBITMQ_HOST` and `RABBITMQ_PORT` also need to be configured for MDSSC to check connectivity to the service before starting up.

> **Info**
>
> Due to the limits  AmazonMQ puts on the number of consumers per open channel, we recommend decreasing the consumer numbers used for AmazonMQ.

To decrease the number of consumers used and comply with the AmazonMQ limits, the environment variables `RABBITMQ_CONSUMER_MULTIPLIER` and `RABBITMQ_RPC_CONSUMER_MULTIPLIER` can be used with a value lower  than the default of 10.
