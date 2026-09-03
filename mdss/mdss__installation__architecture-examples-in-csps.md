<!-- source: https://www.opswat.com/docs/mdss/installation/architecture-examples-in-csps -->

# Architecture Examples in CSPs

This page outlines the recommended architecture for running MetaDefender Storage Security (MDSS) with any Cloud Service Provider (CSP).

We provide diagrams for AWS, Azure, and GCP, where our product is available in their respective marketplaces. However, our products are cloud-agnostic and can be deployed to any CSP.

## [**Infrastructure Options for MetaDefender Storage Security using Compute Services**](/docs/mdss/installation/architecture-examples-in-csps#infrastructure-options-for-metadefender-storage-security-using-compute-services)

The appropriate infrastructure will vary depending on the number of instances where MetaDefender Storage Security will be installed.

Options:

1. Single Instance
2. Multi-Instance with Autoscaling

### [Single Instance](/docs/mdss/installation/architecture-examples-in-csps#single-instance)

To proceed, select the tab corresponding to the CSP where you intend to deploy MetaDefender Storage Security.

AWSAzureGCP

### [Multi-Instance with Autoscaling](/docs/mdss/installation/architecture-examples-in-csps#multi-instance-with-autoscaling)

Select the tab for the CSP where you want to deploy MetaDefender Storage Security.

AWS

## [Infrastructure Options for MetaDefender Storage Security using Container Services](/docs/mdss/installation/architecture-examples-in-csps#infrastructure-options-for-metadefender-storage-security-using-container-services)

The possible infrastructure **varies** depending on the Cloud services used for hosting MetaDefender Storage Security and how the **required third-party tools** are provisioned.

Options:

1. Kubernetes Cluster with **Customer-Managed** Worker Nodes, utilizing either a Cloud PostgreSQL Service or **third-party tools as Pods**.
2. Kubernetes Cluster with **CSP-Managed** Worker Nodes, utilizing a Cloud PostgreSQL Service

### [Customer Managed Worker Nodes](/docs/mdss/installation/architecture-examples-in-csps#customer-managed-worker-nodes)

Select the **tab** for the CSP where you want to deploy MetaDefender Storage Security.

AWSAzureGCP

**EC2 Instances + AWS Document DB or** **3rd Party tools as Pod**

**Azure VM (Worker Nodes) + Azure PostgreSQL DB Service or 3rd Party tools as Pod**

**Google Compute Engines Instances (Worker Nodes) + Google Cloud SQL or 3rd Party tools as Pod**

### [**CSP-Managed** **Worker Nodes**](/docs/mdss/installation/architecture-examples-in-csps#csp-managed-worker-nodes)

Above examples include **AWS Fargate or Azure Container Apps options for computing.**

These are serverless compute engines for containers that allow you to run containerized applications without managing the underlying infrastructure.

These services run containers with certain **limitations**, such as CPU limits per instance or ephemeral storage, which may be required for some Linux packages.

Please check the **system requirements** before choosing this architecture.

IMPORTANT
We recommend deploying a database service from your Cloud Service Provider (CSP) for MetaDefender Core and MetaDefender Storage Security.
