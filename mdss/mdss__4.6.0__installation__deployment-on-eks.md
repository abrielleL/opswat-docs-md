<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/deployment-on-eks -->

# Deployment on EKS

This guide explains how to use the provisioning tools provided by OPSWAT to create an AWS EKS and generate all the Kubernetes components needed to run MetaDefender Core and MetaDefender Storage Security.

> **Info**
>
> In case of having the K8S cluster already created, please check the [Containerized Deployment Overview](https://www.opswat.com/docs/mdss/installation/containerized-deployment-overview)
>
> This page is purely for provisioning the EKS cluster and install the products at the same time with tools that OPSWAT has prepared.

## Deploy using Terraform

- Locally clone the [metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s) repository and go to terraform folder

```bash
git clone git@github.com:OPSWAT/metadefender-k8s.git
cd terraform/aws/
```

- Modify variables/variables.tfvars file
  - PERSISTENT_DEPLOYMENT=true -> To create K8S cluster with EC2 Worker Nodes
  - DEPLOY_FARGATE_NODES=false -> To true if wanted to create a Fargate profile
  - DEPLOY_RDS_POSTGRES_DB=true -> To create RDS instance for PostgreSQL server
  - POSTGRES_USERNAME -> if DEPLOY_RDS_POSTGRES_DB=true, set up admin database username
  - POSTGRES_PASSWORD -> if DEPLOY_RDS_POSTGRES_DB=true, set up admin database password
  - MQ_USERNAME -> if DEPLOY_RABBITMQ=true
  - MQ_PASSWORD -> if DEPLOY_RABBITMQ=true

```bash
MD_CLUSTER_NAME        = "md-k8s"
MD_CLUSTER_REGION      = "eu-central-1"
ACCESS_KEY_ID          = "<ACCESS_KEY_ID>"
SECRET_ACCESS_KEY      = "<SECRET_ACCESS_KEY>"
PERSISTENT_DEPLOYMENT  = true
DEPLOY_FARGATE_NODES   = false
DEPLOY_RDS_POSTGRES_DB = true
POSTGRES_USERNAME      = "<POSTGRES_USERNAME>"
POSTGRES_PASSWORD      = "<POSTGRES_PASSWORD>"

DEPLOY_REDIS           = true
DEPLOY_RABBITMQ        = true
MQ_PASSWORD            = "<MQ_USERNAME>"
MQ_USERNAME            = "<MQ_PASSWORD>"
```

- Run terraform init and apply. Check the resource to be created, after that enter "y"

```bash
terraform init
terraform apply
```

## MetaDefenderK8S script details

- Script path: %provisioning_script_path%
- **Programming Language:** Bash
- Installation Pre-requisites for provisioning:
  - [Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
  - [Helm](https://helm.sh/docs/intro/install/)
  - [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
  - [Kubectl ](https://kubernetes.io/docs/tasks/tools/#kubectl)
  - [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html#eksctl-install-update) (When using the lb controller script)
- AWS Credentials
  - Set in your local environment credentials the IAM user credentials under ***AWS_ACCESS_KEY_ID***& ***AWS_SECRET_ACCESS_KEY***
- MetaDefender Core License Key (Required with --mdcore parameter)
  - Set it in your local environment credentials under ***MDCORE_LICENSE_KEY***

> **Warning**
>
> As security measure do not use the root user for any deployment or operation. Follow the principle of least privilege for all access granted.

### How to run the script

```bash
./metadefenderk8s.sh provision -l AWS --mdcore --mdss
```

### **Script Parameters**

| **Parameter** | Flags | Options | Default | Description | Required/Optional |
| ---- | ---- | ---- | ---- | ---- | ---- |
| **Action** |  | - provision - install |  | Action to indicate the script if we want to provision (Create resources + install Core) or install (Install Core) | **Required** |
| **Location** | -l or --location | - AWS - Azure - GCP |  | Where is going to be the K8S cluster | **Required** |
| **MetaDefender Flag Installation** | Combination of - --mdcore - --mdss - --icap |  | -  | Install MetaDefender Core in the cluster provisioned | **Required** |
| **Image Version** | --image | - latest - [<docker-image-tag>](https://hub.docker.com/r/opswat/metadefendercore-debian/tags) | latest | MetaDefender Core image version to install | Optional |
| **Region** | --region | [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/?p=ngi&loc=2) | eu-central-1 | AWS region where all the resources will be provisioned | Optional |
| **Cluster Name** | --name | Not uppercase allowed | md-k8s | Name of the cluster that will be used for naming all the resources | Optional |
| **Number of Replicas** | --replicas | [0-9]* | 1 | Number of replicas for MetaDefender Core service | Optional |
| **Namespace** | --namespace | [A-Za-z]{1,10} |  | Namespace where MetaDefender products will be installed in the K8S Cluster | Optional Max Characters: 10 |

**Limitations using parameters**

- When using Fargate
  - the pods should be installed in the default namespace.
  - if using AWS Load Balancer controllers need a worker node to be installed in.

> **Info**
>
> The script will deploy a single Worker Node for the cluster with enough space for 1 replica of MD Core. AWS EC2 Instance size is **c5.2xlarge** **(8 vCPU & 16 GiB Memory).** Each pod would request 7 vCPU and 8 GiB Memory. To change the request to adapt each pod to the specific case go to [values.yml](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdcore/values.yaml#L153) To change the node group go to the terraform file [terraform/aws/eks_cluster_module](https://github.com/OPSWAT/metadefender-k8s/blob/58b02cbd600592b94905abea3faae21145bbe9b0/terraform/aws/eks_cluster_module/main.tf#L671)

## MetaDefender Core Flowchart Provisioning in AWS

The following flowchart represents how the provisioning script will configure the environment based on the options selected for provisioning AWS EKS.

#### Summary options to be selected

1. EKS with **EC2** or **Fargate**
2. Access to the K8S cluster. Generate **Ingress** or provide **own** access.
   1. **An Ingress** will be create per each product flag added as parameter to the script
   2. **Own Access**, you decide how to access to the cluster so it won't generate any load balancer for accessing
3. Have your **own database** or create **new database**
   1. **Own database,** will be asked if you want the script to set up the credentials and database host url for you or the script will just indicate the secrets to edit, later on by you, for connecting the MetaDefender Core with your database.
   2. Create new **DB in K8S** or **external DB** that for AWS we will provision a ***RDS instance***

![](https://uploads.developerhub.io/prod/k8zL/ry0q9sez8afgi6i4qptnzm9wdxklgc62jzh33vbambwf8916at3vptqgpxqmpxi1.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
