<!-- source: https://www.opswat.com/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s- -->

# Cloud Deployment with Kubernetes (k8s)

This is our recommended option for maximum scalability, high availability, and handling large volumes of data. It uses Kubernetes to automate deployment, scaling, and management of MDSS in a cloud environment.

Kubernetes is like an automated control system for your cloud deployment. It lets you scale MDSS easily, ensures it stays running, and optimizes resource usage. If you need high performance and availability, this is the way to go.

#### [Suitable For](/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s-#suitable-for)

- Organizations handling massive amounts of data.
- Organizations Prioritizing High Availability, needing minimal downtime.
- Cloud-Savvy Teams familiar with Kubernetes.

#### [Why Use Kubernetes?](/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s-#why-use-kubernetes)

- Dynamically adjust resources based on workload.
- Distributes MDSS across multiple nodes to minimize downtime.
- Optimize resource allocation for each component.
- Kubernetes handles load balancing, autoscaling, and more.

#### [Key Components & Cloud Integration](/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s-#key-components--cloud-integration)

- Kubernetes (k8s) orchestrates the deployment.
- Managed Cloud Services for database, cache, message broker (e.g., AWS EKS, Azure AKS, Google GKE).

#### [Examples](/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s-#examples)

- For AWS - use Amazon RDS, Amazon ElastiCache, Amazon MQ
- Users of Azure or Google Cloud can adapt this model to employ their respective managed services with Azure Kubernetes Service (AKS) or Google Kubernetes Engine (GKE). For detailed guidance on integrating with various cloud providers, please follow:

  - [Azure AKS](https://learn.microsoft.com/en-us/azure/aks/)
  - [Azure Database for PostgreSQL](https://azure.microsoft.com/en-us/products/postgresql)
  - [Azure Cache for Redis](https://learn.microsoft.com/en-us/azure/azure-cache-for-redis/)
  - [Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine/docs)

#### [Key Points](/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s-#key-points)

- Kubernetes automates many deployment tasks.
- Easily scale up or down as needed.
- Kubernetes ensures high availability.
- Integrates with cloud monitoring, reporting, etc.

#### [Important Considerations](/docs/mdss/getting-started/cloud-deployment-with-kubernetes--k8s-#important-considerations)

- Requires understanding Kubernetes concepts.
- You need a Kubernetes cluster set up before deploying MDSS.
- MDSS is deployed using a Helm chart available on GitHub.
