<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps -->

# Architecture Examples in CSPs

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This page outlines the recommended architecture for running MetaDefender ICAP Server with any Cloud Service Provider (CSP).

We provide diagrams for AWS, Azure, and GCP, where our product is available in their respective marketplaces. However, our products are cloud-agnostic and can be deployed to any CSP.

## [**Infrastructure Options for MetaDefender ICAP Server**](/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps#infrastructure-options-for-product_name)

**Using Compute Services**

The appropriate infrastructure will vary depending on the number of instances where MetaDefender ICAP Server will be installed.

Options:

1. Single Instance
2. Multi-Instance with Autoscaling

### [Single Instance](/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps#single-instance)

To proceed, select the tab corresponding to the CSP where you intend to deploy MetaDefender ICAP Server

AWSAzureGCP

### [Multi-Instance with Autoscaling](/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps#multi-instance-with-autoscaling)

Select the tab for the CSP where you want to deploy MetaDefender ICAP Server

AWSAzureGCP

Example of multiple instances in multiple regions.

## [Infrastructure Options for MetaDefender ICAP Server using Container Services](/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps#infrastructure-options-for-product_name-using-container-services)

The possible infrastructure **varies** depending on the Cloud services used for hosting MetaDefender ICAP Server and how the **required third-party tools** are provisioned.

Options:

1. Kubernetes Cluster with **Customer-Managed** Worker Nodes, utilizing either a Cloud PostgreSQL Service or **third-party tools as Pods**.
2. Kubernetes Cluster with **CSP-Managed** Worker Nodes, utilizing either a Cloud PostgreSQL Service or **third-party tools as Pods**.

## [Customer Managed Worker Nodes](/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps#customer-managed-worker-nodes)

Select the **tab** for the CSP where you want to deploy MetaDefender Storage Security.

AWSAzureGCP

## [**CSP-Managed** **Worker Nodes**](/docs/mdicap/v5.15.0/installation/architecture-examples-in-csps#csp-managed-worker-nodes)

Using above examples, include **AWS Fargate or Azure Container Apps options for computing.**

These are serverless compute engines for containers that allow you to run containerized applications without managing the underlying infrastructure.

These services run containers with certain **limitations**, such as CPU limits per instance or ephemeral storage, which may be required for some Linux packages.

Please check the **system requirements** before choosing this architecture.

Database Cloud Service

We recommend deploying a database service from your Cloud Service Provider (CSP) for MetaDefender Core and MetaDefender ICAP Server
