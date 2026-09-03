<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture -->

# AKS Cluster

The possible infrastructure vary depending on how the PostgreSQL database is provisioned

Options:

1. Azure AKS with VMs + Azure PostgreSQL
2. Azure AKS with VMs + PostgreSQL Pod

We offer a provisioning script that depending on the selection, we automatically provision the cluster for you and install the K8S components needed for MD Core service. See [AKS Cluster Deployment](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-provision)

#### [MetaDefender PostgreSQL database details](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#metadefender-postgresql-database-details)

#### [**Recommendations**](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#recommendations)

For running MD Core in a Kubernetes cluster we recommend to use, for production environments, an external database service for PostgreSQL. In case of **Azure** it is **Azure PostgreSQL** which the script will deploy and configure to be accessible from the cluster.

For non-production environments or for stateless use cases, we offer the option of installing the database within the cluster using a standard PostgreSQL image.

### [Azure VMs + Azure PostgreSQL / PostgreSQL Pod Diagram](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#azure-vms--azure--postgresql--postgresql-pod-diagram)

### [Resources Inventory](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#resources-inventory)

#### [***Networking***](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#networking)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Azure Virtual Network | <resource-group-name>-vnet |  |
| Azure Subnet | <resource-group-name>-aks-subnet |  |
| Azure Subnet | <resource-group-name>-db-subnet |  |
| Azure Private DNS Zone | <postgres_db_account_name>.postgres.database.azure.com |  |
| Azure Private DNS Zone Virtual Network Link | <postgres__db__account_name>.com |  |

#### [***Monitoring***](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#monitoring)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Azure Log Analytics WorkSpace | <log_analytics_workspace_name> | Workspace for analyzing the AKS Service |
| Azure Log Analytics Solution | ContainerInsights | Solution for gathering metrics of containers |

#### [***Compute***](/docs/mdcore/v5.21.0/cloud-deployment/aks-cluster-architecture#compute)

| Service Type | Resource Name | Description | Option |
| --- | --- | --- | --- |
| Azure AKS | <cluster_name> | Azure Kubernetes Service Cluster | All |
| Azure ProstgreSQL Flexible Server | postgresql-<postgres_db_account_name> | PostgreSQL Server for MetaDefender Core | Option with Azure PostgreSQL |
| Azure ProstgreSQL Flexible Server Configuration | azure.extensions | Configuration for installing PG_TRGM,DBLINK,BTREE_GIN_ | Option with Azure PostgreSQL |

Info

The script will deploy a single Worker Node for the cluster with enough space for 1 replica of MD Core. Azure VM size is **Standard_F8s_v2 (8 vCPU & 16 GiB Memory).** Each pod would need a minimum of 4 vCPU and 8 GiB Memory. To change the request to adapt each pod to the specific case go to [values.yml](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdcore/values.yaml#L153) To change the size of the node pool go to terraform file [terraform/azure/main.tf](https://github.com/OPSWAT/metadefender-k8s/blob/main/terraform/azure/main.tf#L106)
