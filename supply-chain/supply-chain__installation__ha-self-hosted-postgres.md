<!-- source: https://www.opswat.com/docs/supply-chain/installation/ha-self-hosted-postgres -->

# High Availability (HA) with Database Replication

## MDSSC database redundancy setup (primary + standby)

This page explains how to set up a second PostgreSQL server that can take over if the main database server fails (sometimes called a standby, replica, or disaster-recovery database).

It includes:

- how to configure the main database server (primary)
- how to set up the standby server (replica)
- how to validate replication
- how to promote the standby during an outage
- Primary (Dockerized MDSSC Postgres): `MDSSC1`
- Standby database server (replica): `MDSSC2`

Terminology used in this page:

- **Primary**: the database server that MDSSC writes to (read/write).
- **Standby/replica**: a second server that continuously copies data from the primary (read-only until promoted).
- **Failover / promotion**: switching the standby to become the new primary during an outage.

> **Security note**
>
> Store credentials in your secrets manager and export them as environment variables at runtime.

## 1) Primary host (`MDSSC1`)

### 1.1 Ensure Postgres is exposed on host port 5432

```bash
mdssc -c status
docker ps --format 'table {{.Names}}\t{{.Ports}}' | grep mdss_postgres
```

Expected ports include `0.0.0.0:5432->5432/tcp` (or equivalent host binding).

#### If port 5432 is not exposed on `0.0.0.0`

1. Edit **/etc/mdssc/docker-compose.main.yml**. Under the `postgres:` service, if there is no `ports:` section, add one. For example, immediately after `shm_size` (or before `command:`), insert:

```yaml
ports:
  - "${POSTGRES_PORT}:5432"
```

2. In **/etc/mdssc/customer.env**, set the host port (default `5432`):

```bash
POSTGRES_PORT=5432
```

3. Save the changes. You can apply them during the restart in **1.2** (recommended to only restart once).

Optional: if you want to verify the port exposure immediately before proceeding:

```bash
mdssc -c restart
```

### 1.2 Enable replication parameters on the primary

**Recommended (production):** add or merge these into `/etc/mdssc/customer.env` (they map to `wal_level`, `max_wal_senders`, and `max_replication_slots` on the Postgres process):

```bash
POSTGRES_WAL_LEVEL=replica
POSTGRES_MAX_WAL_SENDERS=10
POSTGRES_MAX_REPLICATION_SLOTS=10
```

Then restart the stack so the container picks up the new values:

```bash
mdssc -c restart
```

> **Alternative (manual ALTER SYSTEM)**
>
> If you cannot update `/etc/mdssc/customer.env`, you can set these directly in Postgres. This approach is less repeatable than environment-managed configuration.
>
> Rollback: run `ALTER SYSTEM RESET` for each parameter and restart Postgres.

```bash
docker exec -it mdss_postgres psql -U mdss -d postgres -c "ALTER SYSTEM SET wal_level = 'replica';"
docker exec -it mdss_postgres psql -U mdss -d postgres -c "ALTER SYSTEM SET max_wal_senders = '10';"
docker exec -it mdss_postgres psql -U mdss -d postgres -c "ALTER SYSTEM SET max_replication_slots = '10';"
docker restart mdss_postgres
```

### 1.3 Verify replication settings on primary

```bash
docker exec -it mdss_postgres psql -U mdss -d postgres -c "SHOW wal_level;"
docker exec -it mdss_postgres psql -U mdss -d postgres -c "SHOW max_wal_senders;"
docker exec -it mdss_postgres psql -U mdss -d postgres -c "SHOW max_replication_slots;"
```

### 1.4 Create replication user and slot

```bash
export REPL_PASSWORD='***'
docker exec -it mdss_postgres psql -U mdss -d postgres -c "CREATE ROLE replicator WITH REPLICATION LOGIN ENCRYPTED PASSWORD '${REPL_PASSWORD}';"
docker exec -it mdss_postgres psql -U mdss -d postgres -c "SELECT * FROM pg_create_physical_replication_slot('mdssc_replica1');"
```

### 1.5 Allow replica host in `pg_hba.conf`

This allows the `replicator` user to connect for replication from the replica node.

Set `REPLICA_ADDR` to one of:

- `MDSSC2` (if the primary resolves `MDSSC2` and Postgres is configured to use hostnames in `pg_hba.conf`)
- the replica IP/CIDR, for example `10.30.160.240/32`

```bash
export REPLICA_ADDR='MDSSC2'
```

```bash
docker exec -it mdss_postgres bash -lc "grep -q \"${REPLICA_ADDR}\" /var/lib/postgresql/data/pg_hba.conf || echo \"host replication replicator ${REPLICA_ADDR} scram-sha-256\" >> /var/lib/postgresql/data/pg_hba.conf"
docker exec -it mdss_postgres psql -U mdss -d postgres -c "SELECT pg_reload_conf();"
```

## 2) Replica VM (`MDSSC2`)

### 2.1 Install PostgreSQL 17

```bash
sudo apt update
sudo apt install -y postgresql-17
sudo systemctl stop postgresql
```

### 2.2 Take base backup from primary (`MDSSC1`)

> **Note**
>
> This will replace the replica data directory.

Set the replication password in your current shell (same value used when creating the `replicator` role on the primary):

```bash
export REPL_PASSWORD='***'
sudo -u postgres rm -rf /var/lib/postgresql/17/main/*
sudo -u postgres PGPASSWORD="${REPL_PASSWORD}" pg_basebackup \
  -h MDSSC1 \
  -p 5432 \
  -U replicator \
  -D /var/lib/postgresql/17/main \
  -Fp -Xs -P -R \
  -S mdssc_replica1
```

### 2.3 Required recovery fix (must match primary limits)

If startup fails with `insufficient parameter settings` and `max_connections ... lower setting than on the primary`, run:

```bash
sudo pg_ctlcluster 17 main stop || true
sudo -u postgres bash -c "cat >> /var/lib/postgresql/17/main/postgresql.auto.conf <<'EOF'
max_connections = 1000
max_worker_processes = 8
max_locks_per_transaction = 64
max_prepared_transactions = 0
hot_standby = on
EOF"
sudo rm -f /var/lib/postgresql/17/main/postmaster.pid
sudo chown -R postgres:postgres /var/lib/postgresql/17/main
sudo chmod 700 /var/lib/postgresql/17/main
sudo pg_ctlcluster 17 main start
```

## 3) Check everything is working

### 3.1 Replica checks (`MDSSC2`)

```bash
pg_lsclusters
sudo -u postgres psql -h 127.0.0.1 -p 5432 -U mdss -d MDSS -c "SELECT pg_is_in_recovery();"
```

Expected:

- cluster status includes `online,recovery`

### 3.2 Primary check (`MDSSC1`)

```bash
docker exec -it mdss_postgres psql -U mdss -d postgres -c "SELECT client_addr, state, sync_state FROM pg_stat_replication;"
```

Expected:

- a row exists for the replica connection
- `state = streaming`
- `sync_state = async`

## 4) Known warnings (observed during validation)

- `database "MDSS" has a collation version mismatch` can appear on the replica and does not block replication startup in this setup.
- `role "postgres" does not exist` may appear in service checks because this deployment uses `mdss` as the primary database role.

## 5) Switch over to the standby during an outage (manual)

Promote replica:

```bash
sudo -u postgres psql -h 127.0.0.1 -p 5432 -U mdss -d MDSS -c "SELECT pg_promote(wait_seconds => 60);"
```

After promotion, update the application DB host (`POSTGRESQL_URL Host=...`) to the promoted node (or use a VIP/HA proxy for cleaner failover).

## 6) Two MDSSC app servers sharing one resilient PostgreSQL database

Use this when you run **two MDSSC application nodes** (or two full stacks) and want both to use the **same** external PostgreSQL setup that can survive a database server failure (for example: primary + standby, or a managed/failover PostgreSQL service).

### 6.1 Align with OPSWAT external PostgreSQL

Configure MetaDefender Software Supply Chain to use an external database per OPSWAT:

- [Advanced installation for Unix-based deployments - external PostgreSQL](https://www.opswat.com/docs/supply-chain/installation/advanced-installation-for-unix-based-deployments#how-to-setup-an-external-postgresql-in-metadefender-software-supply-chain)

That covers product-specific settings for pointing MDSSC at a non-bundled Postgres. This page only adds how to wire two MDSSC nodes to one resilient PostgreSQL setup.

### 6.2 One writer for both nodes

MDSSC expects a **single read/write** database. With primary + standby replication:

- **Both** MDSSC instances must use the **same** connection target that resolves to the **current primary** (the only node that accepts writes).
- Do **not** point the second MDSSC instance at the standby/replica for normal operation

In practice, the host in `POSTGRESQL_URL` should be one of:

- The primary server’s IP or DNS name (steady state).
- A **virtual IP (VIP)**, **managed DNS name**, or **HA proxy / connection pooler** (PgBouncer, HAProxy) that always routes to the **primary**, including after failover.

### 6.3 Environment on each MDSSC node

On **both** nodes, set the same application database URL in **/etc/mdssc/customer.env** (production). The entry looks like:

```bash
POSTGRESQL_URL=Host=<primary_or_vip>;Port=5432;Username=mdss;Password=<password>;Database=MDSS
```

Replace `<primary_or_vip>` with the hostname or IP that reaches the write primary from **each** MDSSC host. Use identical values on node 1 and node 2 unless you deliberately split traffic (not typical for this stack).

### 6.4 PostgreSQL access from both application hosts

On the Postgres primary (and any node that accepts app connections, if you route through a proxy), ensure `pg_hba.conf` allows the MDSSC database user from **both** MDSSC server IPs, for example:

```plaintext
host MDSS mdss <mdssc_node_1_ip>/32 scram-sha-256
host MDSS mdss <mdssc_node_2_ip>/32 scram-sha-256
```

Reload PostgreSQL configuration after changes (`SELECT pg_reload_conf();` or service reload).

### 6.5 Failover and both MDSSC instances

After **manual** promotion of a standby (see the manual failover section above) or after **automatic** failover (for example Patroni, repmgr), every MDSSC instance must still reach the **new** primary:

- If you use a **VIP/DNS/proxy** that moves with the primary, `POSTGRESQL_URL` in `/etc/mdssc/customer.env` may stay unchanged on both nodes.
- If you use **fixed IPs**, update `POSTGRESQL_URL` in `/etc/mdssc/customer.env` on **both** MDSSC nodes to the new primary host (or redeploy with the updated secret/config store), then restart using your standard procedure (for example `mdssc -c restart` where appropriate).

Until all MDSSC instances point at the writable primary, one node may hit read-only errors or stale routing after failover.
