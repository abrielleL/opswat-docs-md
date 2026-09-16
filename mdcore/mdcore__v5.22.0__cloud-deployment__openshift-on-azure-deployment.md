<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/openshift-on-azure-deployment -->

# Provisioning OpenShift on your CSP

## [Requirements](/docs/mdcore/v5.22.0/cloud-deployment/openshift-on-azure-deployment#requirements)

Most cloud service providers (CSP) have options for managed deployments of RedHat OpenShift without the need to manually provision and configure VMs. The available resources for the nodes of such a deployment that are intended for MD Core should still follow the recommended system requirements from [here](https://docs.opswat.com/mdcore/installation/recommended-system-configuration#linux-recommended-system-configuration) depending on the expected load and desired performance per node.

The MD Core helm chart used for deployment already has a default request for 7 CPUs and 7 GB of memory and a limit of 8 CPUs and 8 GB of memory, these values can be changed at installation depending on the provisioned resources available.

The PostgreSQL database can be provisioned separately as a managed service (recommended) or as part of the same MD Core deployment on the cluster, in which case the Cluster needs additional resources depending on the expected demand ([PostgreSQL requirements](https://www.commandprompt.com/blog/postgresql_mininum_requirements/)). All major CSPs have managed database solutions compatible with PostgreSQL clients like MD Core.

## [Database Options](/docs/mdcore/v5.22.0/cloud-deployment/openshift-on-azure-deployment#database-options)

**Option 1.** Provisioning a database managed by the cloud provider:

- Microsoft Azure Database for PostgreSQL: <https://learn.microsoft.com/en-us/azure/postgresql/single-server/quickstart-create-server-database-portal>
- Amazon RDS: <https://aws.amazon.com/getting-started/hands-on/create-connect-postgresql-db/>
- Google Cloud SQL: <https://cloud.google.com/sql/docs/postgres/connect-instance-cloud-shell>

**Option 2.** Using an OpenShift operator for PostgreSQL. There are several publicly available operators for HA deployments of PostgreSQL, this type of deployment allows running the database inside the same cluster as MD Core. A persistent volume using managed storage from the cloud provider is preferred for reliability.

Example deployment:<https://portworx.com/blog/run-ha-postgresql-red-hat-openshift/>

**Option 3**. Using the MD Core helm chart. By default, the helm chart also deploys a single PostgreSQL instance alongside MD Core and configures MD Core to use this database. This option is intended mostly for testing and demonstration.

## [Provisioning OpenShift](/docs/mdcore/v5.22.0/cloud-deployment/openshift-on-azure-deployment#provisioning-openshift)

- AWS: [https://docs.openshift.com/rosa/rosa_getting_ started/rosa-quickstart-guide-ui.html](https://docs.openshift.com/rosa/rosa_getting_started/rosa-quickstart-guide-ui.html)
- Azure: <https://learn.microsoft.com/en-us/azure/openshift/tutorial-create-cluster>
- Google Cloud: <https://docs.openshift.com/container-platform/4.10/installing/installing_gcp/installing-gcp-default.html>

After the cluster is provisioned, the MD Core helm chart can be installed: <https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdcore-README.md>
