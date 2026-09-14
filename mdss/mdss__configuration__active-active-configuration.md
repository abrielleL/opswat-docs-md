<!-- source: https://www.opswat.com/docs/mdss/configuration/active-active-configuration -->

# Active-Active configuration

This guide explains how to configure an active-active deployment of MDSS where multiple instances can use the same shared external services for improved performance and scalability.

## [Overview](/docs/mdss/configuration/active-active-configuration#overview)

In an active-active deployment, multiple MDSS instances work together using shared external components (RabbitMQ, PostgreSql, and Redis) to distribute workload, add redundancy and improve throughput. This configuration is particularly useful when handling large volumes of files.

## [Active-Active Configuration Behavior](/docs/mdss/configuration/active-active-configuration#active-active-configuration-behavior)

In an active-active configuration, file processing operations are distributed dynamically across available instances:

- **File Discovery** - any available MDSS instance can detect and identify files requiring processing
- **File Scanning** - any available MDSS instance can perform the security scanning operation
- **Remediation** - any available MDSS instance can execute the remediation actions

#### [**Key Points**](/docs/mdss/configuration/active-active-configuration#key-points)

- Operations may be handled by different instances (distributed processing) or by the same instance (consolidated processing)
- The actual distribution depends on which instance processes the message first
- This design ensures optimal load balancing and high availability across your deployment

This approach maximizes system efficiency while maintaining consistent security coverage regardless of which specific instances handle each operation.

## [External Services Deployment Options](/docs/mdss/configuration/active-active-configuration#external-services-deployment-options)

External services are required for this type of deployment, a deployment and configuration guide is available here: [External Services Configuration](/docs/mdss/installation/external-services-configuration)
