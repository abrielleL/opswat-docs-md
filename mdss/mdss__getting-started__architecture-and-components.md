<!-- source: https://www.opswat.com/docs/mdss/getting-started/architecture-and-components -->

# Architecture & Components

**MetaDefender Storage Security (MDSS)** is built for flexibility. It uses containers, which let you customize and adapt your development to match your specific needs. Getting the sizing right is crucial for performance and reliability as your workload directly impacts sizing. Proper sizing ensures smooth operation. This guide will help you understand the key components and make informed decisions.

High level architecture of MetaDefender Storage Security

## [Shared Services](/docs/mdss/getting-started/architecture-and-components#shared-services)

MDSS depends on the following stateful services to ensure high performance and data consistency:

- **PostgreSQL (Database)** – Stores configuration, job metadata, and system state. Proper sizing ensures transactional integrity and I/O performance at scale.
- **RabbitMQ (Message Broker)** – Coordinates communication across system components. It must be horizontally scalable to handle high volumes of concurrent file scan tasks.
- **Redis (Cache)** Provides low-latency access to ephemeral data and scan results. Effective caching reduces load on other components and speeds up workflow processing.

### [Why These Services Matter:](/docs/mdss/getting-started/architecture-and-components#why-these-services-matter)

- **Scalability** – Each service must scale independently to accommodate varying workloads.
- **Reliability** – As stateful services, downtime or data loss can impact the entire system’s operation.
- **Performance** – Throughput and responsiveness of the system depend on proper resource allocation for these services.
