<!-- source: https://www.opswat.com/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services -->

# Basic Deployment with Managed Services

Instead of managing the database, cache, and message broker yourself, you let the cloud provider handle it. You focus on setting up and scaling MDSS, while the cloud takes care of the underlying infrastructure. Think of it as renting managed services instead of buying and maintaining them yourself.

This deployment builds on the basic model by using *managed cloud services* for the shared components (database, cache, message broker). This means you leverage the cloud provider's expertise to handle the infrastructure, simplifying your setup.

#### [Suitable For](/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services#suitable-for)

- Cloud-First Organizations, organizations heavily reliant on cloud infrastructure.
- Organizations Seeking Simplicity as it reduces the burden of managing infrastructure.
- Workloads up to 50,000 Files/Hour - achievable with sufficient cloud resources and MDSS and MD Core instances.

#### [Key Advantages](/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services#key-advantages)

- Cloud provider handles maintenance, monitoring, and scaling of shared services.
- Ideal for organizations already using cloud services like AWS, Azure, or Google Cloud.
- Reduces operational overhead compared to self-hosting.
- Benefits from cloud-provided features like enhanced monitoring, reporting, and proactive support.

#### [Example: Amazon AWS Integration](/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services#example-amazon-aws-integration)

- Database - use Amazon RDS.
- Cache - use Amazon ElastiCache for Redis.
- Message Broker - use Amazon MQ.

#### [Adaptable to Other Clouds](/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services#adaptable-to-other-clouds)

This approach can be adapted to Azure and Google Cloud, using their respective managed services. Please follow [this article](/docs/mdss/4.4.2/installation/types-of-deployment) for more information regarding integrating with various cloud providers.

#### [Key Points](/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services#key-points)

- You don't manage the shared services directly.
- Your primary focus is on configuring and scaling MDSS itself.
- Leverage the cloud provider's scalability for shared services.
- Benefit from the cloud provider's redundancy and reliability.

#### [Important Considerations](/docs/mdss/4.4.2/getting-started/basic-deployment-with-managed-services#important-considerations)

- Managed services have associated cloud costs, which need to be factored in.
- Requires understanding cloud service integrations and their complexity
