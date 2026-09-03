<!-- source: https://www.opswat.com/docs/mdss/getting-started/windows-deployment -->

# Windows deployment

## [Supported Operating Systems](/docs/mdss/getting-started/windows-deployment#supported-operating-systems)

| **OS** | **Version** | **Architecture** |
| --- | --- | --- |
| Windows Server | 2019, 2022, 2025 (latest) | 64-bit |

Operating System Requirements and Licensing Considerations

Microsoft's licensing terms prohibit the use of Windows Desktop operating systems in server environments. As a result, MetaDefender Storage Security is not compatible with Windows Desktop editions.

For organizations concerned about Windows Server licensing costs, we recommend deploying on Unix-based systems instead. Unix platforms deliver enterprise-level reliability and performance without additional licensing fees.

## [Port Requirements](/docs/mdss/getting-started/windows-deployment#port-requirements)

The following ports must be available for our services to listen on.

Please ensure that no other services are using these ports before starting the installation. NGINX port can be customized during the [installation process](/docs/mdss/installation/windows-installation).

For the MDSS Windows deployment, every port in the below table is **TCP**, and the rule you need is an **inbound "Allow" rule** for each so the components can talk to each other and clients can reach the services. Open these before installing:

| Component | Port |
| --- | --- |
| PostgreSQL | 5432 |
| RabbitMQ | 5672 |
| NGINX | 80 (and 443 if SSL enabled) |
| API Gateway | 8005 |
| Licensing Service | 5001 |
| SMB Service | 6002, 6003, 6004, 6005, 6006, 7002, 7003, 7004, 7005, 7006 |
| SFTP Service | 5003 |
| NFS Service | 5004 |

## [Installation components](/docs/mdss/getting-started/windows-deployment#installation-components)

MetaDefender Storage Security automatically deploys the following components:

| Name | Version | Type |
| --- | --- | --- |
| PostgreSQL | v17.0 | Database |
| RabbitMQ | v4.3.0 | Message Broker |
| NGINX | v1.29.2 | Web Server |
| Garnet | v1.1.8 | Data Cache (Redis compatible) |
