<!-- source: https://www.opswat.com/docs/supply-chain/sizing-guide/sizing-guide -->

# Sizing Guide

## Overview

**MetaDefender Software Supply Chain (MDSSC)** is developed with container technology, offering various ways to organize these networked services to suit your specific requirements. When deploying MDSSC, it's essential to assess the anticipated workload and operational needs. This evaluation will guide you in selecting a deployment strategy that aligns with your performance and reliability criteria.

## Deployment Options

The table below provides a summary of the various options available for deployment.

---

|  | Small scale deployments | Medium scale deployments | Large scale  deployments |
| ---- | ---- | ---- | ---- |
|  | **Basic deployment** | **Cloud deployment with Kubernetes (k8s)** | **Cloud deployment with Kubernetes (k8s)** |
|  | *Suitable for small and predictable workloads* | Suitable for small workloads, offers some flexibility | *Ideal for large workloads, handles daily peaks, cost optimized* |
| **Scalability** | NO | YES | YES |
| **High Availability** | NO | NO | YES |
| **Auto-Scale Ready** | NO | YES | YES |
| **Data / hour** | **5 GB** | **27 GB** | *Tailored for each customer* |
| (data / day) | (115 GB) | (635 GB) |  |
| **Files / hour** | **30,500** | **440,000** | *Tailored for each customer* |
| (files / day) | (732,000) | (10,500,000) |  |
| **Recommended MD Core Resources** | 8CPU 16GB memory | 16CPU 32GB memory | *Tailored for each customer* |
| **Recommended MDSSC Resources** | 8CPU 16GB memory | 16CPU 32GB memory | *Tailored for each customer* |
|  |  |  |  |
| **Recommended  Nodes** | 2 | 1x 32vCPU, 64GB memory | *Tailored for each customer* |

## Basic deployment

For basic deployments, two machines are used:

- **VM 1:** Runs `MetaDefender Core`
- **VM 2:** Runs `MetaDefender Software Supply Chain`

`MDSSC` is installed on a Linux machine following the standard installation procedure: [Linux Installation](https://www.opswat.com/docs/supply-chain/installation/installing-using-the-command-line)

## Cloud deployment with Kubernetes (k8s)

This deployment type is our recommended option when scalability, high availability, or handling a high volume of files is a priority. Kubernetes offers the flexibility to scale from a small setup, designed to manage a moderate volume of files with minimal resources, to a large-scale deployment ensuring high availability across multiple nodes without interruptions. Moreover, scaling can be dynamically adjusted based on workload or other metrics, and each component can be individually scaled to optimize resource allocation tailored to specific needs.

For this setup, we advise using managed services for the shared components such as the database, cache, and message broker. For instance, if you plan to deploy MetaDefender Software Supply Chain on AWS EKS, using Amazon RDS for your database service, Amazon ElastiCache as your cache, and Amazon MQ as your message broker will simplify the workload and bring additional benefits such as enhanced monitoring, reporting, and maintenance, along with proactive support—including billing and continuous improvements from your cloud provider.

Users of Azure or Google Cloud can adapt this model to employ their respective managed services with Azure Kubernetes Service (AKS) or Google Kubernetes Engine (GKE). For detailed guidance on integrating with various cloud providers, please follow:

- [Kubernetes Deployment](https://www.opswat.com/docs/supply-chain/sizing-guide/kubernetes-deployment)
- [Managed Services configuration in AWS](https://www.opswat.com/docs/supply-chain/sizing-guide/managed-services-configuration-in-aws)

Before deploying Storage Security, a Kubernetes cluster must be provisioned and prepared. This preparation includes setting up load balancing, autoscaling, ensuring persistent storage if required, and establishing connectivity to external services. Once these prerequisites are addressed, you can proceed to deploy MDSSC using our Helm chart available on GitHub - [GitHub - OPSWAT/metadefender-k8s: Run MetaDefender in Kubernetes using Terraform and Helm Chart](https://github.com/OPSWAT/metadefender-k8s) . For more detailed instructions on how to deploy and configure the product in a generic Kubernetes cluster, please refer to [Kubernetes Deployment](https://www.opswat.com/docs/supply-chain/sizing-guide/kubernetes-deployment).

## Rate Limiting

When integrating with various platforms, it's essential to be aware of their API rate limits to ensure optimal performance and avoid disruptions. Below is a summary of the API rate limits for several popular platforms.

> **Warning**
>
> **Please note that these are not the official documentation of the limits**; for the most accurate and up-to-date information, refer to the respective platform's official documentation.

---

### **GitHub**

- **Unauthenticated Requests**: 60 requests per hour per IP address.
- **Authenticated Requests**: 5,000 requests per hour per user.
- **GitHub Apps**:
  - **Installation Access Tokens**: 5,000 requests per hour per installation.
  - **For GitHub Enterprise Cloud Organizations**: 15,000 requests per hour per installation.

[docs.github.com](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api?utm_source=chatgpt.com&apiVersion=2022-11-28#primary-rate-limit-for-github-app-installations)

---

### **GitLab**

- **Unauthenticated traffic**: 500 requests per minute per IP address.
- **Authenticated Users**: 2,000 requests per minute.

[docs.gitlab.com](https://docs.gitlab.com/ee/user/gitlab_com/index.html#gitlabcom-specific-rate-limits)

---

### **Bitbucket**

- **Authenticated Requests**: 1,000 requests per hour per user.
- **Unauthenticated Requests**: Unauthenticated requests are subject to stricter rate limits and are discouraged.

[support.atlassian.com](https://support.atlassian.com/bitbucket-cloud/docs/api-request-limits/)

---

### **Azure DevOps**

- Might depend on the subscription plan. For more details, check the link below.

[learn.microsoft.com](https://learn.microsoft.com/en-us/azure/devops/integrate/concepts/rate-limits?view=azure-devops)

---

### **Docker Hub**

- **Anonymous Users**: 10 image pulls per hour per IP address.
- **Authenticated Free Users**: 40 image pulls per hour.
- **Pro and Team Subscribers**: Unlimited pulls.

[docs.docker.com](https://docs.docker.com/docker-hub/usage/)

---

**Important**: API rate limits are subject to change. Always refer to the official documentation of each platform for the most current information.
