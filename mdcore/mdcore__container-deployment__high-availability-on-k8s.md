<!-- source: https://www.opswat.com/docs/mdcore/container-deployment/high-availability-on-k8s -->

# High Availability on K8S

## [HA solutions for Postgres](/docs/mdcore/container-deployment/high-availability-on-k8s#ha-solutions-for-postgres)

In production environments it's recommended to use a managed database service from a cloud provider, Azure, AWS and Google cloud all provide Postgres compatible SQL services. These services have built-in HA and can scale dynamically depending on the required load.

If a highly available database is required inside the k8s cluster, then there are publicly available solutions that can deploy locally. One of the most popular is the Bitnami chart for HA PostgreSQL: <https://bitnami.com/stack/postgresql-ha/helm> and can be deployed using helm:

BashCopy# Adding the Bitnami Helm repo
helm repo add bitnami https://charts.bitnami.com/bitnami
# Installing the chart with example values
helm upgrade --install postgresql-ha postgresql-ha \
--wait \
--set pgpool.authenticationMethod=scram-sha-256 \
--set postgresql.image.tag=12.12.0 \
--set postgresql.pgHbaTrustAll=true \
--set global.pgpool.adminUsername=<SET_PGPOOL_USERNAME> \
--set global.pgpool.adminPassword=<SET_PGPOOL_PASSWORD> \
--set postgresql.password=<SET_POSTGRES_PASSWORD> \
--set postgresql.postgresPassword=<SET_POSTGRES_PASSWORD> \
--set postgresql.numInitChildren=50 \
--set postgresql.maxConnections=100

In order to avoid performance bottlenecks, the following values have to be set in the PostgreSQL chart depending on the number of running MD Core pods using the same database. Example when running 3 MD Core pods:

YamlCopypostgresql:
numInitChildren: 50 # set to about the number of MD Core Pods x 16
maxConnections: 100 # set to about the value of numInitChildren plus 50

The following PGPOOL command has to be run manually the first time to add credentials to enhance authentication via PGPOOL. In case the PGPOOL k8s deployment restarts you must run the command again.

To make this setting persistent, a PV has to be mounted in `/opt/bitnami/pgpool/conf` in each Postgres pod.

BashCopy# Add user and password for internal PG user with auth method scram-sha-256
pg_enc -m -k /opt/bitnami/pgpool/conf/.pgpoolkey -f /opt/bitnami/pgpool/conf/pgpool.conf -u "<user>" "<passwd>"
## [HA deployment for MD Core](/docs/mdcore/container-deployment/high-availability-on-k8s#ha-deployment-for-md-core)

Multiple MD Core pods can be deployed by setting the `replicas`value in the`md-core` component:

YamlCopycore_components:
md-core:
replicas: 3

MD Core can also be set up with separate credentials for read/write operations. For example, the following command can be used to deploy MD core using a HA Postgres deployment as above:

BashCopyhelm install mdcore-deployment ./mdcore \
--wait \
--set db_password=<SET_POSTGRES_PASSWORD> \
--set deploy_with_core_db=false \
--set core_components.md-core.replicas=3 \
--set MDCORE_DB_HOST=<SET_POSTGRES_SERVICE_HOSTNAME> \
--set env.MDCORE_DB_PRIVATE_USERNAME=<SET_PG_USERNAME> \
--set env.MDCORE_DB_PRIVATE_PASSWORD=<SET_PG_PASSWORD>

Each MD Core pod used one activation on the given license and is automatically deactivated by the activation-manager sidecar when the pod is destroyed. It's advisable to have more activations available than the number of active pods in order to avoid activation issues when the number of pods might surge (like on a rolling update).

For redundancy, the pods can also be set to run on different nodes by using the `nodeSelector` or `nodeAffinity` Kubernetes features according to the cluster architecture.
