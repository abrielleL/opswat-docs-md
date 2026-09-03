<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-recommended-setup -->

# Recommended Setup

While it is technically possible to install Redis Cache Server, RabbitMQ Message Broker, PostgreSQL Database Server, MetaDefender Cluster (MD Cluster) File Storage, and other components on the same machine, OPSWAT strongly recommends deploying them on separate servers to achieve better performance, scalability, and reliability.

### [Redis Caching Server](/docs/mdcluster/installation/md-cluster-recommended-setup#redis-caching-server)

Redis consumes a significant amount of memory during operation. To ensure optimal performance, it should be deployed on a dedicated machine with high-capacity, high-speed RAM.

### [RabbitMQ Message Broker](/docs/mdcluster/installation/md-cluster-recommended-setup#rabbitmq-message-broker)

RabbitMQ is a critical component of MD Cluster architecture. It is responsible for distributing tasks evenly across MetaDefender Core (MD Core) instances, rerouting failed tasks to healthy instances, and balancing workloads when additional Core instances are added to the environment.

Because of its central role in maintaining system stability and scalability, RabbitMQ should be hosted on a dedicated server.

### [Postgres Database Server](/docs/mdcluster/installation/md-cluster-recommended-setup#postgres-database-server)

The MD Cluster database is divided into two primary components:

- **Data Lake** stores scan results and request-related information such as `data_id`, file hashes, and metadata. Since it is shared between MD Core and MD Cluster API Gateway instances, it should be hosted on high-speed, large-capacity storage with a reliable, high-bandwidth network connection.
- **Data Warehouse** periodically collects information from Data Lake and prepares data for executive reporting. Because executive reports may need to be retained for long periods and accessed by MD Cluster Control Center, Data Warehouse should also be deployed on a server with large storage capacity.

### [MetaDefender Cluster File Storage](/docs/mdcluster/installation/md-cluster-recommended-setup#metadefender-cluster-file-storage)

MD Cluster File Storage is shared among MD Core and MD Cluster API Gateway instances. It stores submitted files from all connected instances and therefore requires substantial disk capacity.

Since all file-related traffic passes through this component, a high-speed network connection is essential. OPSWAT recommends hosting MD Cluster File Storage on Rocky Linux 9.0.

### [MetaDefender Cluster API Gateway](/docs/mdcluster/installation/md-cluster-recommended-setup#metadefender-cluster-api-gateway)

Due to operating system differences and NGINX support considerations between Windows and Linux, MD Cluster API Gateway should be deployed on a Linux server running Rocky Linux 9.0 to ensure high throughput for file scan submissions.

### [MetaDefender Core](/docs/mdcluster/installation/md-cluster-recommended-setup#metadefender-core)

One of the key strengths of MD Cluster is its support for hybrid deployments. MD Cluster API Gateway and MD Cluster File Storage can run on Linux servers, while MD Core instances can be deployed on either Windows or Linux.

This flexibility allows customers to choose the operating system that best fits their infrastructure and operational requirements.

Warning

It is recommended to deploy all MD Core instances on the same operating system, either Windows or Linux. Mixed operating system deployments are not supported.
