<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/gke-cluster-deployment -->

# GKE Cluster

This guide explains how to use the [provisioning script](https://github.com/OPSWAT/metadefender-k8s/blob/main/metadefenderk8s.sh) provided by OPSWAT to create an GCP GKE and generate all the Kubernetes components needed to run MetaDefender Core.

### MetaDefenderK8S script details

- **GitHub Project** [OPSWAT/metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s) --> **Script path:** [./metadefenderk8s.sh](https://github.com/OPSWAT/metadefender-k8s/blob/main/metadefenderk8s.sh)
- **Programming Language:** Bash
- Installation **Pre-requisites** for provisioning:

  - [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
  - [Helm](https://helm.sh/docs/intro/install/)
  - [gcloud cli](https://cloud.google.com/sdk/docs/install)
  - [Kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)

    - [kubectl plugin "gke-gcloud-auth-plugin"](https://cloud.google.com/blog/products/containers-kubernetes/kubectl-auth-changes-in-gke) (Since GKE 1.6)
- **GCP Credentials**

  - The Cloud SQL Admin API is enabled. (Optional, enabled when Cloud SQL database is going to be used)
  - Download the credentials for the service account, it should have the following permissions

    - Editor
    - Compute Network Admin
  - Set in your environment variable the path to the JSON key with the credentials for the service account to use

    - **GCP_JSON_CREDENTIALS_PATH**
- MetaDefender **Core License Key** (Required with --mdcore parameter)

  - Set it in your local environment credentials under ***MDCORE_LICENSE_KEY***

#### **How to run script**

Only MD CoreMD Core + MDSSMD Core + ICAPCopy./metadefenderk8s.sh provision -l GCP --mdcore --project_id <PROJECT_ID>./metadefenderk8s.sh provision -l GCP --mdcore --mdss./metadefenderk8s.sh provision -l GCP --mdcore --icapInfo

The script will deploy a single Worker Node for the cluster with enough space for 1 replica of MD Core. GCP compute size is **e2-standard-8** **(8 vCPU & 32 GB Memory).** Each pod would need a minimum of 4 vCPU and 8 GB Memory. To change the request to adapt each pod to the specific case go to [values.yml](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdcore/values.yaml#L153) To change the size of the node pool for having more MD Core replicas or install additional MetaDefender products go to terraform file [terraform/gcloud/main.tf](https://github.com/OPSWAT/metadefender-k8s/blob/main/terraform/azure/main.tf#L106)

#### Script Parameters

| **Parameter** | Flags | Options | Default | Description | Required/Optional |
| --- | --- | --- | --- | --- | --- |
| **Action** |  | - provision - install |  | Action to indicate the script if we want to provision (Create resources + install Core) or install (Install Core) | **Required** |
| **Location** | -l or --location | - AWS - Azure - GCP |  | Where is going to be the K8S cluster | **Required** |
| **MetaDefender Flag Installation** | Combination of   - --mdcore - --mdss - --icap |  |  | Install MetaDefender Core in the cluster provisioned | **Required** |
| **Project ID** | --project_id |  |  | GCP project where the resources will be created | **Required** |
| **Image Version** | --image | latest 5.0.1 | latest | MetaDefender Core image version to install | Optional |
| **Region** | --region | [GCP Regions](https://cloud.google.com/compute/docs/regions-zones) | us-central1 | AWS region where all the resources will be provisioned | Optional |
| **Cluster Name** | --name | Not uppercase allowed | md-k8s | Name of the cluster that will be used for naming all the resources | Optional |
| **Number of Replicas** | --replicas | [0-9]* | 1 | Number of replicas for MetaDefender Core service | Optional |
| **Namespace** | --namespace | [A-Za-z]{1,10} |  | Namespace where MetaDefender products will be installed in the K8S Cluster | Optional Max Characters: 10 |

### Connection to Cloud SQL Database from GKE

### MetaDefender Core Flowchart Provisioning in GCP

The following flowchart represents how the provisioning script will configure the environment based on the options selected for provisioning GCP GKE.

#### Summary options to be selected

1. Access to the K8S cluster. Generate **Ingress** or provide **own** access.

   1. **An Ingress** and an internal load balancer will be created per each product flag added as parameter to the script
   2. **Own Access**, you decide how to access to the cluster so it won't generate any ingress but will still create the internal load balancer for the product service deployed
2. Have your **own database** or create **new database**

   1. **Own database,** will be asked if you want the script to set up the credentials and database host url for you or the script will just indicate the secrets to edit, later on by you, for connecting the MetaDefender Core with your database.
   2. Create new **DB in K8S** or **external DB** that for GCP we will provision a **Cloud SQL Server**

      1. **If external, indicate how to connect to it, by private connection or SQL Proxy pod**

GKE Autopilot Deployment

For having GKE of type Autopilot it is needed to change AUTOPILOT_GKE variable to true from terraform.tfvars. Database has to be external (Cloud SQL)
