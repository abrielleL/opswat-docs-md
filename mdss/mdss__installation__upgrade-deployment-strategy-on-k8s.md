<!-- source: https://www.opswat.com/docs/mdss/installation/upgrade-deployment-strategy-on-k8s -->

# Upgrade/Deployment Strategy on K8S

The helm upgrade command can be used to upgrade the mdss services using the latest helm chart:

BashCopyhelm upgrade my_mdss <path_to_chart>
### [General recommendations](/docs/mdss/installation/upgrade-deployment-strategy-on-k8s#general-recommendations)

Before performing any upgrade, review the following best practices:

- **Back up the database**: Always take a full backup of your PostgreSQL database before upgrading. For in-cluster deployments this means snapshotting the persistent volume; for externally managed databases use the provider's native backup/snapshot mechanism. Keep the backup until the new version has been validated in production.
- **Read the release notes**: Check for any breaking changes or required configuration updates in the target release before upgrading.
- **Blue-green deployment**: For production environments where rollback safety is critical, consider a blue-green upgrade strategy:

  1. Clone your existing PostgreSQL database to a separate instance (e.g. a snapshot-restored replica or a managed DB clone).
  2. Deploy the new chart version into a separate namespace (e.g. `mdss-green`), pointing it at the cloned database:`helm install my_mdss_green path_to_new_chart --namespace mdss-green --set POSTGRESQL_URL="connection_string_to_cloned_db"`
  3. Validate functionality of the new deployment against the cloned data without affecting production traffic.
  4. Switch ingress or DNS to the new namespace once satisfied.
  5. If issues arise, revert by routing traffic back to the original namespace — the original database remains untouched.
  6. Decommission the old deployment and cloned database after a suitable validation period.

### [Database upgrades](/docs/mdss/installation/upgrade-deployment-strategy-on-k8s#database-upgrades)

**This step is not required when using an external, managed database**

The helm chart is configured by default to use the latest compatible version of PostgreSQL. Before upgrading an existing deployment with a persistent in-cluster database, make sure the database version matches the version required by the corresponding release:

- MDSS (latest) - PostgreSQL 17

#### [Upgrading from MongoDB (versions prior to v4.0.0)](/docs/mdss/installation/upgrade-deployment-strategy-on-k8s#upgrading-from-mongodb-versions-prior-to-v400)

Starting with MDSS v4.0.0, PostgreSQL replaces MongoDB as the primary database backend. If upgrading from an older MongoDB-based deployment, follow the official [Upgrade Guide to PostgreSQL](https://www.opswat.com/docs/mdss/configuration/upgrade-to-postgresql#upgrade-options) which covers three upgrade options:

- **Option 1 – Standard upgrade with migration**: Recommended for small to medium deployments where historical data is required. Data is migrated automatically; no extra configuration needed. Note that migration takes approximately 2–3 hours per 1 million files.
- **Option 2 – Skip data migration**: Recommended for large deployments or when historical data is not critical. The chart sets `SKIP_MONGO_TO_PG: "yes"` by default, so migration is skipped unless explicitly removed from the values. This provides immediate availability of the new version without waiting for data migration.
- **Option 3 – Blue-green deployment**: Recommended for production environments requiring zero downtime. Deploy v4.0.0 in parallel, test it, then cut over storage processing with easy rollback capability.

#### [Schema migrations](/docs/mdss/installation/upgrade-deployment-strategy-on-k8s#schema-migrations)

Database schema migrations are handled automatically by the `pgmigrations` pod, which runs as an init step before any other MDSS containers start up. No manual migration steps are required — ensure the `pgmigrations` pod completes successfully before troubleshooting other service startup issues.

#### [Upgrading with an externally managed database](/docs/mdss/installation/upgrade-deployment-strategy-on-k8s#upgrading-with-an-externally-managed-database)

When using an external (managed) database, the database itself holds all persistent state. In this case it is **strongly recommended to perform a clean reinstall** rather than a rolling upgrade, to avoid schema or configuration conflicts:

BashCopyhelm delete my_mdss
helm install my_mdss <path_to_chart>

The following components are non-persistent and can be updated to the latest compatible version by setting the respective image tag:

- RabbitMQ: `rabbitmq:4.1.0-alpine`
- Redis Cache: `redis:7.4.1-alpine`

## [Operational Notes](/docs/mdss/installation/upgrade-deployment-strategy-on-k8s#operational-notes)

The entire deployment can be customized by overwriting the chart's default configuration values. Here are a few point to look out for when changing these values:

- By default, a PostgreSQL 17 database is deployed alongside the MDSS deployment
- In a production environment it's recommended to use an external service for the database and set `deploy_with_mdss_db` to false in order to not deploy an in-cluster database
- When using an external database, prefer a clean reinstall (`helm delete` / `helm install`) over `helm upgrade`, since the database holds all persistent state and a clean install avoids potential schema or configuration conflicts
