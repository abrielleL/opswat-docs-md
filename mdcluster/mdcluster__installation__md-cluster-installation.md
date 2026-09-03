<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-installation -->

# Installation

### [Overview](/docs/mdcluster/installation/md-cluster-installation#overview)

This section describes how to install and set up **MetaDefender Cluster** (MD Cluster), a distributed system composed of multiple services, including:

- Redis
- RabbitMQ
- PostgreSQL
- MetaDefender Cluster File Storage (MD Cluster File Storage)
- MetaDefender Cluster Identity (MD Cluster Identity)
- MetaDefender Cluster Control Center (MD Cluster Control Center)
- MetaDefender Cluster Worker (MD Cluster Worker)

MD Cluster can be deployed on **virtual machines** or **physical servers**. After installation, all services are connected to **MD Cluster Control Center**, where licensing is activated and system health is monitored.

---

### [Architecture Overview](/docs/mdcluster/installation/md-cluster-installation#architecture-overview)

MD Cluster consists of the following components:

| Component | Default port | Description |
| --- | --- | --- |
| Redis | 6379 | Caching and fast data access |
| RabbitMQ | 5672 | Message broker |
| PostgreSQL | 5432 | Persistent data storage |
| MD Cluster File Storage | 8890 | File storage service |
| MD Cluster Identity Service | 8891 | Authentication and authorization service |
| MD Cluster Control Center | 8892 | Central control and management |
| MD Cluster Worker | 8893 | Instance lifecycle management |

Info

All other services must be connected to MD Cluster Control Center for the system to function correctly.

---

### [Prerequisites](/docs/mdcluster/installation/md-cluster-installation#prerequisites)

Ensure the following requirements are met before starting the installation.

| Requirement | Description |
| --- | --- |
| Deployment type | Virtual machines or physical servers. |
| Privileges | **Administrator** privileges on Windows; **Root** or **sudo** access on Linux |
| Network | All nodes must be able to communicate with each other |
| Port | Required ports for Redis, RabbitMQ, PostgreSQL, and MD Cluster services must be open |
| Time synchronization | NTP must be configured across all nodes |
| Resources | Adequate CPU, RAM, and disk for each service |

Info

Ensure that firewall rules allow communication between all services (Redis, RabbitMQ, PostgreSQL, and MD Cluster services).

---

### [Installation procedure](/docs/mdcluster/installation/md-cluster-installation#installation-procedure)

#### [Step 1: Install infrastructure services](/docs/mdcluster/installation/md-cluster-installation#step-1-install-infrastructure-services)

Install the required third-party services on designated nodes.

1. Install Redis on [Windows](/docs/mdcluster/installation/md-cluster-redis-windows), [Linux](/docs/mdcluster/installation/md-cluster-redis-linux), or [Air-gapped](/docs/mdcluster/installation/md-cluster-redis-airgapped).
2. Install RabbitMQ on [Windows](/docs/mdcluster/installation/md-cluster-rabbitmq-windows), [Linux](/docs/mdcluster/installation/md-cluster-rabbitmq-linux), or [Air-gapped](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped).
3. Install PostgreSQL on [Windows](/docs/mdcluster/installation/md-cluster-postgresql-windows), [Linux](/docs/mdcluster/installation/md-cluster-postgresql-linux), or [Air-gapped](/docs/mdcluster/installation/md-cluster-postgresql-airgapped).

Success

Ensure all services are installed and running before proceeding to the next step.

---

#### [Step 2: Install and setup core MD Cluster services](/docs/mdcluster/installation/md-cluster-installation#step-2-install-and-setup-core-md-cluster-services)

1. Install MD Cluster File Storage on [Windows](/docs/mdcluster/installation/md-cluster-file-storage-windows) or [Linux](/docs/mdcluster/installation/md-cluster-file-storage-linux).
2. Install MD Cluster Identity Service on [Windows](/docs/mdcluster/installation/md-cluster-identity-service-windows) or [Linux](/docs/mdcluster/installation/md-cluster-identity-service-linux).
3. Install MD Cluster Control Center on [Windows](/docs/mdcluster/installation/md-cluster-control-center-windows) or [Linux](/docs/mdcluster/installation/md-cluster-control-center-linux).
4. Setup [Data Lake and Warehouse](/docs/mdcluster/installation/md-cluster-lake-warehouse).

---

#### [Step 3: Connect services to Control Center](/docs/mdcluster/installation/md-cluster-installation#step-3-connect-services-to-control-center)

After installation, register all infrastructure services and MD Cluster File Storage to Control Center.

1. Sign in to MD Cluster **Control Center** console using your administrator account.
2. From the sidebar, go to `Inventory` > `Services`.
3. Follow the [instructions](/docs/mdcluster/operating/md-cluster-operating-services) to add the services.
4. Verify connectivity to

   1. PostgreSQL (including DataLake and Data Warehouse)
   2. File Storage
   3. RabbitMQ
   4. Redis

---

#### [Step 4: Install and register MD Cluster Worker](/docs/mdcluster/installation/md-cluster-installation#step-4-install-and-register-md-cluster-worker)

1. Follow the [instructions](/docs/mdcluster/installation/md-cluster-worker) to obtain the installation script.
2. Access each target machine and run the script.
3. Sign in to MD Cluster **Control Center** console.
4. From the sidebar, go to `Inventory` > `Workers`.
5. Verify that the installed workers are showing as `Available`.

---

#### [Step 5: Submit execution installers](/docs/mdcluster/installation/md-cluster-installation#step-5-submit-execution-installers)

Execution installers are deployable units managed by MD Cluster Worker, responsible for executing defined processing tasks within the system’s main flow. These installers are:

- MetaDefender Core (MD Core)
- MetaDefender Cluster API Gateway (MD Cluster API Gateway)
- MetaDefender Cluster Callback Service (MD Cluster Callback Service)

Typical steps:

1. Sign in to MD Cluster Control Center console using your administrator account.
2. From the sidebar, go to `Inventory` > `Installers`.
3. Follow the [instructions](/docs/mdcluster/operating/md-cluster-operating-installer) to upload the installers.

Info

While MD Core and MD Cluster API Gateway are **essential** to the main flow, MD Cluster Callback Service is **optional** and only needed when scan results are delivered via webhooks.

---

#### [Step 6: Deploy execution instances](/docs/mdcluster/installation/md-cluster-installation#step-6-deploy-execution-instances)

1. Sign in to MD Cluster Control Center console.
2. From the sidebar, go to `Inventory` > `Workers`.
3. Ensure that MD Cluster Workers are showing as `Available`.

4. Follow the [instructions](/docs/mdcluster/operating/operating-workers#deploy-instances) to deploy execution instances.
5. Verify that all instances are successfully deployed.

Info

At least one instance of **MD Cluster API gateway** and **MD Core** must be deployed on MD Cluster Workers for the system to function fully.

---

#### [Step 7: Activate license](/docs/mdcluster/installation/md-cluster-installation#step-7-activate-license)

1. Sign in to MD Cluster **Control Center** console.
2. From the sidebar, go to `Inventory` > License
3. Follow the [instructions](/docs/mdcluster/operating/md-cluster-operating-licenses) to activate the product according to your license type.
4. Confirm activation.

---

#### [Step 8: Verify system activity](/docs/mdcluster/installation/md-cluster-installation#step-8-verify-system-activity)

After licensing, verify system status.

1. Sign in to the MD Cluster **Control Center** console.
2. Submit a file for scanning from the Control Center.

Submitting files from the Control Center is intended only to verify that the system is working correctly. For actual scanning workloads, submit files through the API Gateway using [POST – Analyze File (Asynchronous Mode).](/docs/mdcluster/api-gateway#fileanalysispost)

3. Go to `History` > `Processing` and confirm that the files has been processed.

---

### [Log files](/docs/mdcluster/installation/md-cluster-installation#log-files)

| Platform | Service | Log location |
| --- | --- | --- |
| Windows | MD Cluster Control Center | `C:\Program Files\OPSWAT\MetaDefender Cluster Control Center\data\log\control-center.log` |
| Linux | MD Cluster Control Center | `var/log/md-cluster-control-center/control-center.log` |
