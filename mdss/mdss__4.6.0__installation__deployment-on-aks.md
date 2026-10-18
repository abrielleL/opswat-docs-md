<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/deployment-on-aks -->

# Deployment on AKS

This guide explains how to use the provisioning tools provided by OPSWAT to create an Azure AKS and generate all the Kubernetes components needed to run MetaDefender Core and MetaDefender Storage Security.

> **Info**
>
> In case of having the K8S cluster already created, please check the [Containerized Deployment Overview](https://www.opswat.com/docs/mdss/installation/containerized-deployment-overview)
>
> This page is purely for provisioning the AKS cluster and install the products at the same time with tools that OPSWAT has prepared.

## Deploy using Terraform

- Locally clone the [metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s) repository and go to terraform folder

```bash
git clone git@github.com:OPSWAT/metadefender-k8s.git#OPTIONAL, IT CAN BE SET UP WITH ENV VARIABLES
cd terraform/azure/
```

- Modify variables/variables.tfvars file
  - PERSISTENT_DEPLOYMENT=true -> To create K8S cluster with EC2 Worker Nodes
  - DEPLOY_FARGATE_NODES=false -> To true if wanted to create a Fargate profile
  - DEPLOY_RDS_POSTGRES_DB=true -> To create RDS instance for PostgreSQL server
  - POSTGRES_USERNAME -> if DEPLOY_RDS_POSTGRES_DB=true, set up admin database username
  - POSTGRES_PASSWORD -> if DEPLOY_RDS_POSTGRES_DB=true, set up admin database password`

```bash
aks_service_principal_app_id = "" #OPTIONAL, IT CAN BE SET UP WITH ENV VARIABLES
aks_service_principal_client_secret = "" #OPTIONAL, IT CAN BE SET UP WITH ENV VARIABLES
aks_service_principal_object_id = "" #OPTIONAL, IT CAN BE SET UP WITH ENV VARIABLES

postgres_admin = ""
postgres_password = ""
```

- Run terraform init and apply. Check the resource to be created, after that enter "y"

```bash
terraform init
terraform apply

# IF Variables are not setup you can use this command
terraform apply \
  -var="aks_service_principal_app_id=$ARM_CLIENT_ID" \
  -var="aks_service_principal_client_secret=$ARM_CLIENT_SECRET"
```

### MetaDefenderK8S Script Details

- **GitHub Project** [metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s) --> **Script path**: [./metadefenderk8s.sh](https://github.com/OPSWAT/metadefender-k8s/blob/main/metadefenderk8s.sh)
- **Programming Language:** Bash
- Installation **Pre-requisites** for provisioning:
  - [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
  - [Helm](https://helm.sh/docs/intro/install/)
  - [AZ CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
  - [Kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- **Azure Credentials**
  - Set in your local environment variables the credentials of the IAM user under
    - **ARM_CLIENT_ID**
    - **ARM_CLIENT_SECRET**
    - **ARM_SUBSCRIPTION_ID**
    - **ARM_TENANT_ID**
  - ssh public key to used to access the cluster with kubectl. Default (~/.ssh/id_rsa.pub). Change from [here](https://github.com/OPSWAT/metadefender-k8s/blob/main/terraform/azure/variables.tf#L54)
  - az login before running the script for the step of downloading the kubeconfig file for you
- MetaDefender **Core License Key** (Required with --mdcore parameter)
  - Set it in your local environment variables the credentials under ***MDCORE_LICENSE_KEY***

#### How to run the script

```bash
./metadefenderk8s.sh provision -l Azure --mdcore
```

```bash
./metadefenderk8s.sh provision -l Azure --mdcore --mdss
```

```bash
./metadefenderk8s.sh provision -l Azure --mdcore --icap
```

> **Info**
>
> The script will deploy a single Worker Node for the cluster with enough space for 1 replica of MD Core. Azure VM size is **Standard_F8s_v2 (8 vCPU & 16 GiB Memory).** Each pod would need a minimum of 4 vCPU and 8 GiB Memory. To change the request to adapt each pod to the specific case go to [values.yml](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdcore/values.yaml#L153) To change the size of the node pool for having more MD Core replicas or install additional MetaDefender products go to terraform file [terraform/azure/main.tf](https://github.com/OPSWAT/metadefender-k8s/blob/main/terraform/azure/main.tf#L106)

#### Script Parameters

| **Parameter** | Flags | Options | Default | Description | Required/Optional |
| ---- | ---- | ---- | ---- | ---- | ---- |
| **Action** |  | - provision - install |  | Action to indicate the script if we want to provision (Create resources + install Core) or install (Install Core) | **Required** |
| **Location** | -l or --location | - AWS - Azure - GCP |  | Where is going to be the K8S cluster | **Required** |
| **MetaDefender Flag Installation** | Combination of - --mdcore - --mdss - --icap |  | -  | Install MetaDefender Core in the cluster provisioned | **Required** |
| **Image Version** | --image | latest 5.0.1 | latest | MetaDefender Core image version to install | Optional |
| **Region** | --region | [Azure Regions](https://azure.microsoft.com/en-us/explore/global-infrastructure/geographies/#overview) | centralus | AWS region where all the resources will be provisioned | Optional |
| **Cluster Name** | --name |  | md-k8s | Name of the cluster that will be used for naming all the resources | Optional |
| **Number of Replicas** | --replicas | [0-9]* | 1 | Number of replicas for MetaDefender Core service | Optional |
| **Namespace** | --namespace | [A-Za-z]{1,10} |  | Namespace where MetaDefender products will be installed in the K8S Cluster | Optional Max Characters: 10 |

### MetaDefender Core Flowchart Provisioning in Azure

The following flowchart represents how the provisioning script will configure the environment based on the options selected for provisioning Azure AKS.

#### Summary options to be selected

1. Access to the K8S cluster. Generate **Ingress** or provide **own** access.
   1. **An Ingress** and an internal load balancer will be created per each product flag added as parameter to the script
   2. **Own Access**, you decide how to access to the cluster so it won't generate any ingress but will still create the internal load balancer for the product service deployed
2. Have your **own database** or create **new database**
   1. **Own database,** will be asked if you want the script to set up the credentials and database host url for you or the script will just indicate the secrets to edit, later on by you, for connecting the MetaDefender Core with your database.
   2. Create new **DB in K8S** or **external DB** that for Azure we will provision a **Azure** ***PostgreSQL Flexible Server***_ **** ___ _ ******._

![](https://uploads.developerhub.io/prod/k8zL/8t8tpvik0wadwsdac919h2ssmezp4zld2n477gx81q31q9qx8bmc37yb0yo9gze3.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
