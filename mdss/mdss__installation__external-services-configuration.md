<!-- source: https://www.opswat.com/docs/mdss/installation/external-services-configuration -->

# External Services Configuration

While this documentation focuses on self-managed, locally deployed services for maximum control and customization, MDSS supports any compatible external services — whether self-managed on your own VMs or consumed as managed services from a Cloud Service Provider (CSP).

## Protocol Compatibility

MDSS communicates with its external stateful dependencies using **standard open-source protocols only**:

- **PostgreSQL:** standard PostgreSQL wire protocol
- **RabbitMQ:** AMQP 0-9-1 (the standard RabbitMQ protocol)
- **Redis:** standard Redis protocol (RESP)

Any service — managed or self-deployed — that exposes these standard protocols is compatible with MDSS. This is why managed services not explicitly listed in this guide (for example, managed PostgreSQL on Oracle Cloud) also work without compatibility issues. Conversely, managed services that only expose proprietary or different protocols (for example, **Azure Service Bus**, which does not implement AMQP 0-9-1 semantics compatible with RabbitMQ clients) are **not** compatible.

If your cloud provider does not offer a protocol-compatible managed service for a given component, either:

- **Self-deploy the service on a Linux VM** in your cloud environment, following the [External Components Setup](#1-external-components-setup) instructions below, or
- **Use a CSP marketplace alternative** — for example, [CloudAMQP](https://www.cloudamqp.com/) provides managed RabbitMQ available through the Azure Marketplace and Google Cloud Marketplace, and can be recommended across any CSP.

The configuration principles outlined in this guide remain the same regardless of whether you choose self-managed or cloud-managed services — simply update the connection URLs and credentials in your `customer.env` file to point to your chosen service endpoints.

## Supported Managed Services by Cloud Provider

| Component | AWS | Azure | Google Cloud |
| ---- | ---- | ---- | ---- |
| **PostgreSQL** | Amazon RDS for PostgreSQL | Azure Database for PostgreSQL | Cloud SQL for PostgreSQL |
| **RabbitMQ** | Amazon MQ for RabbitMQ | No native compatible managed service — use CloudAMQP (Azure Marketplace) or self-deploy on a Linux VM | No native compatible managed service — use CloudAMQP (Google Cloud Marketplace) or self-deploy on a Linux VM |
| **Redis** | Amazon ElastiCache for Redis | Azure Cache for Redis | Memorystore for Redis |

### PostgreSQL

#### Amazon RDS for PostgreSQL

1. In the AWS Console, create an **RDS for PostgreSQL** instance, choosing an instance class that meets the [recommended specs](#recommended-specs).
2. Deploy it in the same VPC as your MDSS hosts and configure the security group to allow inbound traffic on port `5432` from the MDSS hosts only.
3. Connect with the master user and create the `mdss` user, the `MDSS` database, and grants as described in [PostgreSQL Configuration](#postgresql-configuration) (steps 1–3).
4. Copy the instance endpoint into `POSTGRESQL_URL` in `customer.env` on the MDSS host and disable the embedded PostgreSQL container (`DISABLED_SERVICES=postgres`).

Reference: [Creating and connecting to a PostgreSQL DB instance (AWS)](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)

#### Azure Database for PostgreSQL

1. In the Azure Portal, create an **Azure Database for PostgreSQL – Flexible Server** instance sized per the [recommended specs](#recommended-specs).
2. Use private access (VNet integration) or configure firewall rules so only MDSS hosts can reach port `5432`.
3. Connect with the admin user and create the `mdss` user, the `MDSS` database, and grants as described in [PostgreSQL Configuration](#postgresql-configuration) (steps 1–3).
4. Copy the server FQDN into `POSTGRESQL_URL` in `customer.env` and disable the embedded PostgreSQL container (`DISABLED_SERVICES=postgres`).

Reference: [Create an Azure Database for PostgreSQL flexible server (Microsoft)](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/quickstart-create-server)

#### Google Cloud SQL for PostgreSQL

1. In the Google Cloud Console, create a **Cloud SQL for PostgreSQL** instance sized per the [recommended specs](#recommended-specs).
2. Enable a private IP on the VPC shared with your MDSS hosts (or use authorized networks) so only MDSS hosts can reach port `5432`.
3. Connect with the default `postgres` user and create the `mdss` user, the `MDSS` database, and grants as described in [PostgreSQL Configuration](#postgresql-configuration) (steps 1–3).
4. Copy the instance IP into `POSTGRESQL_URL` in `customer.env` and disable the embedded PostgreSQL container (`DISABLED_SERVICES=postgres`).

Reference: [Create a Cloud SQL for PostgreSQL instance (Google)](https://cloud.google.com/sql/docs/postgres/create-instance)

### RabbitMQ

#### Amazon MQ for RabbitMQ (AWS)

1. In the AWS Console, create an **Amazon MQ** broker with the **RabbitMQ** engine type, deployed in the same VPC as your MDSS hosts.
2. Configure the broker's security group to allow inbound traffic on port `5671` (AMQPS) from the MDSS hosts.
3. Create the broker admin credentials and note the AMQPS endpoint.
4. Set `RABBITMQ_URI` (using the `amqps://` scheme), `RABBITMQ_HOST`, `RABBITMQ_PORT`, `RABBITMQ_DEFAULT_USER`, and `RABBITMQ_DEFAULT_PASS` in `customer.env`, and disable the embedded RabbitMQ container (`DISABLED_SERVICES=rabbitmq`).
5. Review the broker's consumer timeout configuration — MDSS long-running scan consumers require the consumer timeout to be disabled or increased, as described in [RabbitMQ Configuration](#rabbitmq-configuration).

Reference: [Getting started with Amazon MQ for RabbitMQ (AWS)](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/getting-started-rabbitmq.html)

#### CloudAMQP (Azure and Google Cloud)

Azure and Google Cloud do not offer a native managed service compatible with the standard RabbitMQ (AMQP 0-9-1) protocol — Azure Service Bus is **not** RabbitMQ-compatible. For these providers, use **CloudAMQP** (managed RabbitMQ available via the CSP marketplaces) or self-deploy RabbitMQ on a Linux VM as described in [RabbitMQ Configuration](#rabbitmq-configuration).

1. Subscribe to CloudAMQP through the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/cloudamqp.cloudamqp) or [Google Cloud Marketplace](https://console.cloud.google.com/marketplace/details/cloudamqp-public/cloudamqp), or sign up directly at [cloudamqp.com](https://www.cloudamqp.com/).
2. Create an instance in the same cloud region as your MDSS deployment; for production, choose a dedicated plan and enable VPC peering to keep traffic private.
3. From the instance details page, copy the AMQPS URL and credentials.
4. Set `RABBITMQ_URI` (using the `amqps://` scheme, including the vhost from the CloudAMQP URL), `RABBITMQ_HOST`, `RABBITMQ_PORT`, `RABBITMQ_DEFAULT_USER`, and `RABBITMQ_DEFAULT_PASS` in `customer.env`, and disable the embedded RabbitMQ container (`DISABLED_SERVICES=rabbitmq`).
5. Disable the consumer timeout for the instance (configurable via the CloudAMQP console) as described in [RabbitMQ Configuration](#rabbitmq-configuration).

Reference: [CloudAMQP documentation](https://www.cloudamqp.com/docs/index.html)

#### Self-deployed RabbitMQ on a CSP Linux VM (any provider)

If a marketplace service is not an option, provision a Linux VM (e.g., Azure Virtual Machines, Google Compute Engine, Amazon EC2) in the same network as your MDSS hosts and follow the [RabbitMQ Configuration](#rabbitmq-configuration) instructions below.

### Redis

#### Amazon ElastiCache for Redis (AWS)

1. In the AWS Console, create an **ElastiCache for Redis** cluster in the same VPC as your MDSS hosts.
2. Configure the security group to allow inbound traffic on port `6379` from the MDSS hosts.
3. Enable authentication (Redis AUTH) and, for production, in-transit encryption (TLS).
4. Copy the primary endpoint into `CACHE_SERVICE_URI`, `CACHE_SERVICE_URL`, and `CACHE_SERVICE_PORT` in `customer.env`, and disable the embedded Redis container (`DISABLED_SERVICES=redis`).

Reference: [Getting started with Amazon ElastiCache (AWS)](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/GettingStarted.html)

#### Azure Cache for Redis

1. In the Azure Portal, create an **Azure Cache for Redis** instance in the same region as your MDSS deployment.
2. Use private endpoint / VNet integration or firewall rules so only MDSS hosts can reach the cache.
3. From **Access keys**, copy the host name, port, and access key.
4. Set `CACHE_SERVICE_URI` (host, port, and the access key as the password), `CACHE_SERVICE_URL`, and `CACHE_SERVICE_PORT` in `customer.env`, and disable the embedded Redis container (`DISABLED_SERVICES=redis`).

Reference: [Create an Azure Cache for Redis instance (Microsoft)](https://learn.microsoft.com/en-us/azure/azure-cache-for-redis/quickstart-create-redis)

#### Google Cloud Memorystore for Redis

1. In the Google Cloud Console, create a **Memorystore for Redis** instance on the VPC shared with your MDSS hosts.
2. Enable AUTH and, for production, in-transit encryption (TLS).
3. Note the instance IP address, port, and AUTH string.
4. Set `CACHE_SERVICE_URI`, `CACHE_SERVICE_URL`, and `CACHE_SERVICE_PORT` in `customer.env` accordingly, and disable the embedded Redis container (`DISABLED_SERVICES=redis`).

Reference: [Create a Memorystore for Redis instance (Google)](https://cloud.google.com/memorystore/docs/redis/create-instance-console)

## Prerequisites

- Multiple VMs in the same network for MDSS deployment
- Separate VMs or managed services for external components
- Administrative access to all systems

#### Recommended specs:

- PostgreSQL: minimum 8 CPU and 16GB of RAM for the average workload
- RabbitMQ: [RabbitMQ System Requirements](https://www.rabbitmq.com/docs/production-checklist#resource-limits)
- Redis: [Redis System Requirements](https://redis.io/docs/latest/operate/rs/installing-upgrading/install/plan-deployment/hardware-requirements/)
- MDSS VM: [General System Requirements](https://www.opswat.com/docs/mdss/getting-started/general-system-requirements)

## 1. External Components Setup

### RabbitMQ Configuration

**Installation:** Follow the [official RabbitMQ installation guide](https://www.rabbitmq.com/docs/install-debian) for your distribution.

**Configure credentials for remote access:**

```bash
sudo rabbitmqctl add_user <username> <password>
sudo rabbitmqctl set_permissions -p / <username> ".*" ".*" ".*"
sudo rabbitmqctl set_user_tags <username> administrator
```

**Enable management interface for monitoring:**

```bash
sudo rabbitmq-plugins enable rabbitmq_management
```

**Disable consumer timeout (important for long processing consumers)**

Edit RabbitMQ config:

```bash
sudo nano /etc/rabbitmq/rabbitmq.conf
```

Add:

```bash
consumer_timeout = undefined
```

**Restart RabbitMQ**

```bash
sudo systemctl restart rabbitmq-server
```

### PostgreSQL Configuration

**Installation:** Follow the [PostgreSQL installation guide](https://www.postgresql.org/download/linux/ubuntu/).

**Configure for remote access:**

1. **Create the Database User and Database**

Connect to PostgreSQL as a superuser and run:

```bash
-- Create the MDSS user (replace <your_password> with a strong password)
CREATE ROLE mdss LOGIN PASSWORD '<your_password>';

-- Create the database
CREATE DATABASE "MDSS" OWNER mdss;
```

2. ** Grant Required Permissions

**

Still connected as superuser, switch to the `MDSS` database and run:

```sql
\c "MDSS"

-- Database connection
GRANT CONNECT ON DATABASE "MDSS" TO mdss;

-- Schema permissions (required for migrations to create tables)
GRANT CREATE, USAGE ON SCHEMA public TO mdss;

-- Full privileges on existing objects
GRANT ALL PRIVILEGES ON ALL TABLES    IN SCHEMA public TO mdss;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO mdss;
GRANT ALL PRIVILEGES ON ALL FUNCTIONS IN SCHEMA public TO mdss;
GRANT ALL PRIVILEGES ON ALL PROCEDURES IN SCHEMA public TO mdss;

-- Default privileges for new objects created by migrations
ALTER DEFAULT PRIVILEGES IN SCHEMA public
    GRANT ALL PRIVILEGES ON TABLES    TO mdss;
ALTER DEFAULT PRIVILEGES IN SCHEMA public
    GRANT ALL PRIVILEGES ON SEQUENCES TO mdss;
ALTER DEFAULT PRIVILEGES IN SCHEMA public
    GRANT ALL PRIVILEGES ON FUNCTIONS TO mdss;

-- pg_catalog access (For encryption extensions if needed)
GRANT USAGE ON SCHEMA pg_catalog TO mdss;
```

3. **Enable the pgcrypto and pg_trgm Extensions**

MDSS requires the [pgcrypto ](https://www.postgresql.org/docs/current/pgcrypto.html)and[ ](https://www.postgresql.org/docs/current/pgcrypto.html)[pg_trgm](https://www.postgresql.org/docs/current/pgtrgm.html) extensions to be available in the `MDSS` database. The embedded PostgreSQL container enables them automatically, so this step applies only when you use an external or remote database.

On a self-managed server, `pgcrypto` and `pg_trgm` ship in the PostgreSQL *contrib* package. Install it if it is not already present:

```bash
# Debian / Ubuntu
sudo apt-get install postgresql-contrib

# RHEL / Rocky / Alma (replace 16 with your PostgreSQL major version)
sudo dnf install postgresql16-contrib
```

Then, still connected as a superuser, create the extensions **inside the MDSS database**:

```sql
\c "MDSS"

CREATE EXTENSION IF NOT EXISTS pgcrypto;
CREATE EXTENSION IF NOT EXISTS pg_trgm;
```

Verify that they are installed:

```sql
SELECT extname, extversion FROM pg_extension WHERE extname IN ('pgcrypto', 'pg_trgm');
```

> **Note:** On PostgreSQL 13 and later, `pgcrypto` and `pg_trgm` are trusted extensions: the `mdss` user, as owner of the `MDSS` database, can create them, and MDSS creates the ones it needs during the database migration. Creating them beforehand as a superuser is still recommended, and it is required on services that restrict extensions, such as Azure (see below).

Managed PostgreSQL services differ slightly:

- **Amazon RDS / Aurora for PostgreSQL:** run the statement as the master user. No additional configuration is required.
- **Azure Database for PostgreSQL – Flexible Server:** add `PGCRYPTO` and `PG_TRGM` to the `azure.extensions` server parameter, save, and then run the statement.
- **Google Cloud SQL for PostgreSQL:** run the statement as the default `postgres` user. No additional configuration is required.

4. **Configure postgresql.conf:**

```bash
listen_addresses = '*'

# PostgreSQL Performance Configuration
max_connections = 1000

# Memory settings for optimal database performance
shared_buffers = 16GB
work_mem = 256MB
temp_buffers = 64MB
maintenance_work_mem = 2GB
effective_cache_size = 24GB

# WAL (Write-Ahead Logging) configuration
wal_level = minimal
max_wal_senders = 0
max_replication_slots = 0
max_wal_size = 2GB
min_wal_size = 160MB
```

5. **Increase file limits in sysctl.conf:**

```yaml
fs.file-max = 50000
```

6. Update systemd service file `/usr/lib/systemd/system/postgresql.service`  to increase file limits for PostgreSQL user.
7. Restart PostgreSQL:

```bash
sudo systemctl daemon-reload && sudo systemctl restart postgresql.service
```

8. **Configure customer.env on the MDSS Host**

On the MDSS host, edit /etc/mdss/customer.env (in your MDSS installation directory) and add:

```bash
POSTGRESQL_URL=Host=<pg-host-ip>;Port=5432;Username=mdss;Password=<your_password>;Database=MDSS;Timeout=60;CommandTimeout=60
```

Replace <pg-host-ip> with the IP or hostname of your PostgreSQL server and <your_password> with the password you set in Step 1.

9. **Disable the Embedded PostgreSQL Container**

Add the following to customer.env:

```bash
DISABLED_SERVICES=postgres
```

### Redis Configuration

> **Note:** Use external Redis only when deploying MDSS services on multiple nodes. For single-node deployments, the local Redis instance provides better latency.

**Installation:** Follow the [Redis installation guide](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/install-redis-on-linux/).

**Configure password and remote access in** `/etc/redis/redis.conf`:

```yaml
requirepass your_password_here
bind 0.0.0.0
```

## 2. MDSS Configuration

### Configure External Services

Edit `customer.env` file with your external service configurations:

```yaml
# Configure external RabbitMQ
RABBITMQ_URI=amqp://mdss:mdss@<rabbitmq-host>:5672
RABBITMQ_HOST=<rabbitmq-host>
RABBITMQ_PORT=5672
RABBITMQ_DEFAULT_PASS=mdss
RABBITMQ_DEFAULT_USER=mdss

# Optional: Configure external Redis instance
CACHE_SERVICE_URI=<redis-host>:6379,user=default,password=mdss,syncTimeout=10000
CACHE_SERVICE_URL=<redis-host>
CACHE_SERVICE_PORT=6379

# Configure external database
POSTGRESQL_URL=Host=<pg-host-ip>;Port=5432;Username=mdss;Password=<your_password>;Database=MDSS;Timeout=60;CommandTimeout=60

# Disable all the local services
DISABLED_SERVICES=postgres,redis,rabbitmq

# Example performance tuning parameters for higher workloads
RABBITMQ_SCANNING_PREFETCH_COUNT=5
RABBITMQ_LOAD_BALANCER_PREFETCH_COUNT=60
RABBITMQ_NFS_DISCOVERY_PREFETCH_COUNT=60
RABBITMQ_DISCOVERY_PREFETCH_COUNT=40
DISCOVERY_THROTTLER_MAX_PENDING_FILES=10000
```

## 3. Performance Monitoring

### Monitor RabbitMQ Queues

Access the RabbitMQ management interface at `http://<rabbitmq-host>:15672` to monitor queue sizes.

**Key queue to monitor:**

- `object_ready_for_scan_queue`: Shows files waiting to be scanned

If this queue accumulates messages, consider increasing the number of scanning services.

### Prefetch Count Optimization

When running multiple scanning services, decrease the scanning prefetch count to distribute load more evenly: RABBITMQ_SCANNING_PREFETCH_COUNT=5

Adjust other prefetch counts based on your queue sizes and performance requirements.

## 5. Best Practices

1. **Resource Allocation:** Ensure adequate CPU and memory for both MDSS and external service VMs
2. **Network Latency:** Keep all components in the same network to minimize latency
3. **Monitoring:** Regularly monitor RabbitMQ queues and system resources
4. **Scaling:** Start with fewer MDSS instances and scale up based on queue monitoring
5. **Engine Selection:** Use minimal engines required for your use case to improve performance

## Troubleshooting

**Common Issues:**

- **High queue buildup:** Increase scanning service containers or optimize prefetch counts
- **External service timeouts:** Check network connectivity and service configuration
- **Resource exhaustion:** Monitor CPU/memory usage and scale resources accordingly

**Log Locations:**

- MDSS logs: `/etc/mdss/services_logs/`

This configuration enables horizontal scaling of MDSS deployments while maintaining shared state through external services, providing improved performance for high-volume scanning workloads.

## Production Considerations

### Security

**Encrypted Connections:** Always use secure connection protocols (TLS/SSL) for all communications between MDSS instances and external services. Configure RabbitMQ with AMQPS, and Redis with TLS encryption.

**Network Security:** Implement network-level security by restricting access to external services only from authorized MDSS hosts using firewalls, VPCs, or security groups. Deploy services in private subnets when possible.

**Authentication & Authorization:** Create dedicated service accounts with minimal required privileges for MDSS access.

### High Availability

Configure external services for high availability using their native clustering or replication features:

- **PostgreSQL**: Use replication to a secondary database
- **RabbitMQ:** Configure clustering with HA policies
- **Redis:** Use Redis Sentinel or Redis Cluster

For managed cloud services, enable multi-AZ deployments and automatic failover capabilities provided by your cloud provider.

### Monitoring & Alerting

Implement comprehensive monitoring for:

- Service availability and response times
- Resource utilization (CPU, memory, disk, network)
- Queue depths and processing rates
- Connection pool health
- Error rates and failed operations

Set up alerting for critical thresholds that could impact MDSS performance.

### Backup & Disaster Recovery

Establish regular backup procedures and test recovery processes for all external services. For managed services, configure automated backups with appropriate retention policies.

### Performance Optimization

- Configure connection pooling based on your concurrent load requirements
- Set appropriate resource limits and file descriptors
- Monitor and tune service-specific performance parameters
- Plan capacity based on expected MDSS throughput

### Documentation References

For detailed configuration guidance, refer to the official production documentation:

- [PostgreSQL Documentation](https://www.postgresql.org/docs/current/admin.html)
- [RabbitMQ Production Checklist](https://www.rabbitmq.com/docs/production-checklist)
- [Redis Security Guidelines](https://redis.io/docs/latest/operate/oss_and_stack/management/security/)

For managed cloud services, consult your cloud provider's best practices documentation for the specific services you're using.

# **Automated Deployment on a Dedicated Machine**

## **Supported services**

| Selector | Service | Default published port | Port override variable |
| ---- | ---- | ---- | ---- |
| `db` | PostgreSQL | 5432 | `POSTGRES_EXTERNAL_PORT` |
| `cache` | Redis | 6379 | `REDIS_EXTERNAL_PORT` |
| `queue` | RabbitMQ | 5672 | `RABBITMQ_EXTERNAL_PORT` |

Any subset can be selected — for example only `db` if Redis and RabbitMQ stay on the product machine. Port overrides are set in `/etc/mdss/customer.env` on the dedicated machine before running the command.

## **Deployment steps**

### **1. Install the MDSS package**

Install the same DEB or RPM package used for the product on the dedicated machine for external services, following the standard installation guide. Do not start the product on this machine.

### **2. Start the external services**

```bash
mdss -c start -e db,cache,queue
```

The command starts only the selected services, publishes their ports, and generates credentials for them (a Redis password and a RabbitMQ `mdss` user with a random password; the PostgreSQL password is the one already configured in `customer.env`). It then prints a settings block:

```bash
==============================================================================
 The following services are now running on this machine (10.0.20.14):
   db, cache, queue

 Add the lines below to your customer.env file (default location /etc/mdss/customer.env)
 on the machine running MetaDefender Storage Security, then run 'mdss -c restart' there:
------------------------------------------------------------------------------
DISABLED_SERVICES=postgres,redis,rabbitmq
POSTGRESQL_URL=Host=10.0.20.14;Port=5432;Username=mdss;Password=...;Database=MDSS;Timeout=60;CommandTimeout=60
CACHE_SERVICE_URI=10.0.20.14:6379,syncTimeout=10000,user=default,password=...
CACHE_SERVICE_URL=10.0.20.14
CACHE_SERVICE_PORT=6379
RABBITMQ_HOST=10.0.20.14
RABBITMQ_PORT=5672
RABBITMQ_DEFAULT_USER=mdss
RABBITMQ_DEFAULT_PASS=...
RABBITMQ_URI=amqp://mdss:...@10.0.20.14:5672
------------------------------------------------------------------------------
 A commented copy was saved in /etc/mdss/customer.env on this machine.
==============================================================================
```

Example output — addresses and passwords are generated per deployment. A commented copy of the block is kept at the end of `customer.env` on the dedicated machine, so it can be retrieved later without regenerating anything.

### **3. Apply the printed settings**

1. Append the printed block to `/etc/mdss/customer.env` on the main machine running MetaDefender Storage Security.
2. Run `mdss -c restart`.

The product now connects to the dedicated machine, and the embedded PostgreSQL, Redis, and RabbitMQ containers are no longer started there (this is what the generated `DISABLED_SERVICES` line controls).

## **Configuration variables**

| Variable | Set on | Purpose |
| ---- | ---- | ---- |
| `EXTERNAL_SERVICES_HOST` | Dedicated machine | The address written into the printed settings. Set it before running the command when the machine has several addresses and the auto-detected one is not the address the product should connect to. |
| `EXTERNAL_SERVICES_BIND_ADDRESS` | Dedicated machine | Binds the published ports to a single interface instead of all interfaces (`0.0.0.0` by default). |
| `POSTGRES_EXTERNAL_PORT`, `REDIS_EXTERNAL_PORT`, `RABBITMQ_EXTERNAL_PORT` | Dedicated machine | Override the published port of each service. |

## **Post-install operations**

After the first start, the dedicated machine remembers its role. The usual commands keep working there without repeating `-e`:

```plaintext
mdss -c status
mdss -c stop
mdss -c restart
```

Running `mdss -c start -e ...` again is safe: it re-prints the settings block using the existing credentials, so it can be used at any time to recover the values.

> **The published ports are not filtered by ufw or firewalld.** Docker publishes them at the NAT level, so they bypass host firewalls that filter the INPUT chain and are reachable from every network that can route to the machine. Restrict access to the ports from the `DOCKER-USER` iptables chain, from the network firewall, or by setting `EXTERNAL_SERVICES_BIND_ADDRESS` to a single interface.
>

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
