<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/kubernetes -->

# Kubernetes

This guide provides installation and operating instructions for running **MetaDefender Cluster** on Kubernetes.

## [**Supported Kubernetes versions**](/docs/mdcluster/container-deployment/kubernetes#supported-kubernetes-versions)

| Version | Notes |
| --- | --- |
| 1.31.x | Fully supported and validated. |
| Earlier versions | Not validated. The chart uses only stable APIs (`apps/v1`, `v1`), but no testing is performed below 1.31. |

## [**Guide structure**](/docs/mdcluster/container-deployment/kubernetes#guide-structure)

Start with Quick start for a first deployment. The other pages are reference material and can be read in any order once the cluster is running.

| **Page** | **What it covers** |
| --- | --- |
| [Quick start](/docs/mdcluster/container-deployment/quick-start) | Prerequisites and the step-by-step install |
| [Kubernetes components](/docs/mdcluster/container-deployment/kubernetes-components) | The workloads and images the chart creates, service discovery, the shared ConfigMap and Secret, and the pod security model |
| [Enable HTTPs](/docs/mdcluster/container-deployment/enable-https) | Serving HTTPS from MetaDefender Cluster Control Center and MetaDefender Cluster API Gateway |
| [Resource requirements](/docs/mdcluster/container-deployment/resource-requirements) | CPU, memory and ephemeral storage sizing |
| [Scaling](/docs/mdcluster/container-deployment/scaling) | Adding and removing MetaDefender Cluster Workers and MetaDefender Cluster File Storage replicas |
| [Upgrade](/docs/mdcluster/container-deployment/upgrade) | Upgrading the core services and the deployed instances |
| [High Availability](/docs/mdcluster/configurations/md-cluster-high-availability) | Clustered PostgreSQL, RabbitMQ and Redis, and multiple MetaDefender Cluster File Storage replicas |
| [Troubleshooting](/docs/mdcluster/container-deployment/troubleshooting) | Symptoms, checks and log collection |
