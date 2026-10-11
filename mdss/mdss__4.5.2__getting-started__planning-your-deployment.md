<!-- source: https://www.opswat.com/docs/mdss/4.5.2/getting-started/planning-your-deployment -->

# Planning your Deployment

MetaDefender Storage Security (MDSS) offers versatile deployment options to align with your organization's specific infrastructure and security requirements. This includes support for air-gapped environments. Understanding the different deployment models will help you choose the most suitable approach.

Regardless of the deployment type, make sure you have reviewed the **recommended system requirements** for MetaDefender Storage Security.

MetaDefender Storage Security can be deployed across various platforms:

- **Physical Servers** for direct hardware installations.
- **Virtualization Platforms** compatible with popular platforms like VMware, Hyper-V, and XenServer.
- Can be deployed on **Infrastructure as a Service** from major cloud providers such as AWS, Azure, and GCP.
- Supports containerized deployments in **Kubernetes** clusters.

The Basic and Advanced Deployment types can be broadly categorized based on how the shared services (database, message broker, and cache) are managed:

## Deployments with Self-Hosted Shared Services

- Usage Cases
  - Shared services are segregated from the main MetaDefender Storage Security instance, often onto a single dedicated VM (Linux is preferred). This is suitable for allocating dedicated resources to these services. (Basic Deployment)
  - Each shared service is installed on separate instances to enhance reliability, scalability, and high availability, crucial for managing larger workloads. The key difference from the basic setup is the implementation of high availability for one or more services and potentially more advanced scalability features like database clustering (sharding) if required. (Advanced Deployment)
- High-Level Steps
  1. Prepare the system(s) by updating packages
  2. Deploy PostgreSQL (Database)
  3. Deploy RabbitMQ (Message Broker)
  4. Deploy Redis (Cache)
  5. Configure MetaDefender Storage Security to connect to these self-hosted shared services
  6. Start MetaDefender Storage Security
  7. (For advanced deployments) Implement and configure scalability and high availability for the shared services

## Deployments with Managed Shared Services

This model leverages cloud-provider-managed services for the database, message broker, and cache, reducing the operational overhead of managing these components yourself.

- Usage Scenarios
  - A single MetaDefender Storage Security instance utilizes managed cloud services for its shared components (Basic Deployment)
  - Multiple MetaDefender Storage Security instances are deployed, all connecting to the same managed cloud services. This enhances capacity, reliability, and high availability (Advanced Deployment)
- Characteristics
  - Easily deploy multiple MetaDefender Storage Security instances. Each new instance is configured to use the same managed shared services.
  - For deployments with multiple instances, a **load balancer** is recommended, especially for event-based, real-time scanning, to ensure high availability and distribute traffic.
    - Cloud - use the cloud provider's load balancing services.
    - On-Premises - manually deploy load balancers like NGINX, HAProxy, or Traefik.
  - Managed services are configured within MetaDefender Storage Security similarly to self-hosted ones, though specific terminology might vary by cloud provider.
  - Examples of Managed Services:
    - Database (PostgreSQL alternatives): Amazon RDS, Azure Database for PostgreSQL, Google Cloud SQL
    - Cache (Redis alternatives): AWS ElastiCache for Redis, Azure Cache for Redis
    - Message Broker (RabbitMQ alternatives):  AWS Amazon MQ, Azure MP Cloud AMQP and Bitnami package for RabbitMQ in Azure MP.

## Kubernetes Deployment

This approach involves deploying MetaDefender Storage Security within a Kubernetes cluster using a Helm chart.

- Prerequisites
  - An existing Kubernetes cluster (Managed Kubernetes Services like EKS, AKS, GKE are common for production, while self-managed Kubernetes offers more control but requires more maintenance).
  - For deployments using the OPSWAT-provided convenience script (`metadefenderk8s.sh`):
    - Familiarity with the chosen Cloud Service Provider (AWS or Azure)
    - An account with the CSP to create the necessary resources
    - Linux shell environment
    - Tools: Terraform, Helm, AWS-CLI (for AWS), Kubectl
- Deployment Method
  - The OPSWAT **convenience script** (`metadefenderk8s.sh`) is the simplest way to provision a Kubernetes cluster (if needed) and install MetaDefender Storage Security. It guides users through the required steps.

Choosing the right deployment type depends on your existing infrastructure, technical expertise, scalability needs, and budget.

Carefully evaluate these factors and the prerequisites for each model before proceeding with your MetaDefender Storage Security installation.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
