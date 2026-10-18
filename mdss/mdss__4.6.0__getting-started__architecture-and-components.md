<!-- source: https://www.opswat.com/docs/mdss/4.6.0/getting-started/architecture-and-components -->

# Architecture & Components

**MetaDefender Storage Security (MDSS)** is built for flexibility. It uses containers, which let you customize and adapt your development  to match your specific needs. Getting the sizing right is crucial for performance and reliability as your workload directly impacts sizing. Proper sizing ensures smooth operation. This guide will help you understand the key components and make informed decisions.

![High level architecture of MetaDefender Storage Security](https://uploads.developerhub.io/prod/k8zL/id44ghto4xwtwu81gfb8ypzoigvkq5a3x483ayj925dun995uablcq0b6stqu97f.png)

## MDSS Components

MDSS is a set of services that share the infrastructure below. Storage-type specific code (Amazon S3, Azure, Google Cloud, Box, SharePoint, SFTP, FTP, and so on) is loaded in-process by the Storages, Discovery, Remediations and Scanning services; there is no separate container per storage type. Only NFS and SMB have a dedicated sidecar service.

| Component | Role | Log folder |
| ---- | ---- | ---- |
| Web Client | The management console served by NGINX. Forwards API calls to the API Gateway | `services/webclient` |
| API Gateway | The REST API used by the web client, the public API and the OPSWAT ONTAP Connector | `mdcs_apigateway` |
| Identity Service | Users, roles, API keys and single sign-on | `mdss_identityservice` |
| Licensing Service | License activation and enforcement | `mdcs_licensingservice` |
| Job Dispatcher | Schedules scans and tracks job progress | `mdcs_jobdispatcher` |
| Storages Service | Accounts, groups and storage units, including connection tests and autodiscovery | `mdss_storagesservice` |
| Discovery Service | Enumerates the objects in each storage unit and detects changes for real-time protection | `mdss_discoveryservice` |
| Scanning Service | Downloads objects and submits them to the configured scan instance (MetaDefender Core, MetaDefender Cluster or MetaDefender Cloud) | `mdcs_scanningservice` |
| Remediations Service | Applies the remediation actions of the workflow: delete, move, copy, tag, replace with the sanitized copy | `mdss_remediationsservice` |
| Workflow Manager | Workflows, scan instances and remediation rules | `mdss_workflowmanager` |
| Notification Service | Email, webhook and RabbitMQ notifications | `mdcs_notificationservice` |
| Logging Service | Audit log, with optional forwarding to external loggers (Syslog, Kafka) | `mdcs_loggingservice` |
| NFS Service, SMB Service | Sidecars that mount NFS and SMB shares on behalf of the central services. Started only when the `nfs` or `smb` module is enabled | `mdintegrations_nfsservice`, `mdintegrations_smbservice` |
| Database migrations | One-shot jobs that upgrade the database schema at startup, then exit | `services/pgmigrations`, `services/mongomigrations` |

On Linux, the platform services (Identity, Licensing, Job Dispatcher, Logging, Scanning, Notification, Discovery, Remediations, Storages, Workflow Manager) run by default in one bundled container (`mdss_platform`). Setting `COMMON_SERVICES_ENABLED=no` runs each of them in its own container instead. The log folders are the same in both modes. On Windows, the services run as native processes managed by a single Windows service, `mdss`.

## Shared Services

MDSS depends on the following stateful services to ensure high performance and data consistency:

- **PostgreSQL (Database)** – Stores configuration, job metadata, and system state. Proper sizing ensures transactional integrity and I/O performance at scale.
- **RabbitMQ (Message Broker)** – Coordinates communication across system components. It must be horizontally scalable to handle high volumes of concurrent file scan tasks.
- **Redis (Cache)** Provides low-latency access to ephemeral data and scan results. Effective caching reduces load on other components and speeds up workflow processing.
- **MongoDB** – Present only on installations upgraded from versions that used it. New installations do not deploy it.

### Why These Services Matter:

- **Scalability** – Each service must scale independently to accommodate varying workloads.
- **Reliability** – As stateful services, downtime or data loss can impact the entire system’s operation.
- **Performance** – Throughput and responsiveness of the system depend on proper resource allocation for these services.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
