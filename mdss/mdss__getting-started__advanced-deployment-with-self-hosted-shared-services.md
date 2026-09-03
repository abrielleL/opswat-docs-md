<!-- source: https://www.opswat.com/docs/mdss/getting-started/advanced-deployment-with-self-hosted-shared-services -->

# Advanced Deployment with Self-Hosted Shared Services

This deployment is for high-performance needs, using multiple MDSS and MD Core instances and self-hosted shared services (database, cache, message broker). It's significantly more complex than the basic setups but offers superior performance and reliability.

This setup is like building a powerful engine. You're running multiple MDSS and MD Cores and managing the database, cache, and communication hub yourself. This gives you high performance, but it's also more complex to set up and maintain.

#### [Suitable For](/docs/mdss/getting-started/advanced-deployment-with-self-hosted-shared-services#suitable-for)

- High-Throughput Environments, organizations processing large volumes of files.
- Organizations with Strong IT Infrastructure as it requires in-house expertise to manage the complexity.

#### [Key Components & Their Roles](/docs/mdss/getting-started/advanced-deployment-with-self-hosted-shared-services#key-components--their-roles)

- Multiple MDSS Core Instances - allows parallel processing for higher throughput.
- PostgreSQL (Database) - stores data.
- Redis (Cache) - speeds up data access.
- RabbitMQ (Message Broker) - manages communication between components.

#### [Key Points](/docs/mdss/getting-started/advanced-deployment-with-self-hosted-shared-services#key-points)

- Requires more planning and technical expertise.
- Can handle up to 100,000 files per hour with sufficient resources.
- You are responsible for installing, configuring, and maintaining all components.
- Allows scaling through multiple MDSS Core instances and shared services.
- Achieved through database replication and careful configuration.

#### [Important Considerations](/docs/mdss/getting-started/advanced-deployment-with-self-hosted-shared-services#important-considerations)

- Requires significant hardware resources for all components.
- Effective monitoring is essential due to the increased complexity.
- While better than basic setups, careful planning is needed to avoid single points of failure.
- Our testing showed 2 MDSS instances with 4 MDSS Core instances yielded substantial performance improvements.
- Once all services are deployed and ready to be used, please follow [Installation Methods](/docs/mdss/installation/installation-methods) to connect MDSS to them.
