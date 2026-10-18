<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/architecture-examples-in-csps -->

# Architecture Examples in CSPs

This page outlines the recommended architecture for running MetaDefender Storage Security (MDSS) with any Cloud Service Provider (CSP).

We provide diagrams for AWS, Azure, and GCP, where our product is available in their respective marketplaces. However, our products are cloud-agnostic and can be deployed to any CSP.

## **Infrastructure Options for MetaDefender Storage Security using Compute Services**

The appropriate infrastructure will vary depending on the number of instances where MetaDefender Storage Security will be installed.

Options:

1. Single Instance
2. Multi-Instance with Autoscaling

### Single Instance

To proceed, select the tab corresponding to the CSP where you intend to deploy MetaDefender Storage Security.

**AWS**

![](https://uploads.developerhub.io/prod/k8zL/8rfxlf5kjoo806i584iusq4kachlm4qyzosx1vev4tgsceaihvgjcmmdk1eakrqr.png)

**Azure**

![](https://uploads.developerhub.io/prod/k8zL/l3njzg9sb3b1ur4x2liu5eped0j2es9bobp71cxtpjrzr3bmigcike66j1zi2wek.svg)

**GCP**

![](https://uploads.developerhub.io/prod/k8zL/gdxayoglyc3rzhw1k4zacd1wzfjjoizk369alp7xof3o70chbbxe8y4uaqovybrb.svg)

### Multi-Instance with Autoscaling

Select the tab for the CSP where you want to deploy MetaDefender Storage Security.

**AWS**

![](https://uploads.developerhub.io/prod/k8zL/i2z0enhys993l64xy3w3jwkoce0s81ikc1j7rtsv5qsus8mobn12qgvbu5pltrwu.png)

## Infrastructure Options for MetaDefender Storage Security using Container Services

The possible infrastructure **varies** depending on the Cloud services used for hosting MetaDefender Storage Security and how the **required third-party tools** are provisioned.

Options:

1. Kubernetes Cluster with **Customer-Managed** Worker Nodes, utilizing either a Cloud PostgreSQL Service or **third-party tools as Pods**.
2. Kubernetes Cluster with **CSP-Managed** Worker Nodes, utilizing a Cloud PostgreSQL Service

### Customer Managed Worker Nodes

Select the **tab** for the CSP where you want to deploy MetaDefender Storage Security.

**AWS**

**EC2 Instances + AWS Document DB or** **3rd Party tools as Pod**

![](https://uploads.developerhub.io/prod/k8zL/vtce4s1sfkdfcu78temzdqrkypqlt7qy21uaylmwayctzw7zzhd7qmyqx83gzk52.svg)

**Azure**

**Azure VM (Worker Nodes) + Azure PostgreSQL DB Service or 3rd Party tools as Pod**

![](https://uploads.developerhub.io/prod/k8zL/h8dd8l6fawzvhvxtnlcfuaq91t0l496mcsbqi96c9ynytdi9mn2wves17j4dakno.svg)

**GCP**

**Google Compute Engines Instances (Worker Nodes) + Google Cloud SQL or 3rd Party tools as Pod**

![](https://uploads.developerhub.io/prod/k8zL/6luqqq5dyfnpk9qow4efiddi202ixk40ecsdv1274fidwnuvc1nzbltmctyrmlvt.svg)

### **CSP-Managed** **Worker Nodes**

Above examples include **AWS Fargate or Azure Container Apps options for computing.**

These are serverless compute engines for containers that allow you to run containerized applications without managing the underlying infrastructure.

These services run containers with certain **limitations**, such as CPU limits per instance or ephemeral storage, which may be required for some Linux packages.

Please check the **system requirements** before choosing this architecture.

> **IMPORTANT
>
> We recommend deploying a database service from your Cloud Service Provider (CSP) for MetaDefender Core and MetaDefender Storage Security.**

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
