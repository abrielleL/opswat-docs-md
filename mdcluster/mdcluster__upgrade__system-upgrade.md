<!-- source: https://www.opswat.com/docs/mdcluster/upgrade/system-upgrade -->

# System Upgrade

Upgrading MetaDefender Cluster (MD Cluster) requires careful planning because not all services affect the system in the same way.

Some components can be upgraded while file scanning continues normally, while others are critical infrastructure services that affect authentication, queue management, metadata handling, and file availability across the entire cluster.

To reduce operational risk, the upgrade procedure is divided into two stages:

| Stage | Description | Downtime Impact |
| --- | --- | --- |
| **Live Upgrade** | Upgrades application-level services while the cluster continues processing files | Minimal or no disruption |
| **Critical Service Upgrade** | Upgrades shared infrastructure services that the cluster depends on | Maintenance window required |

---

## [Before You Begin](/docs/mdcluster/upgrade/system-upgrade#before-you-begin)

Before starting the upgrade:

- Verify backups are available for:

  - PostgreSQL
  - MD Cluster File Storage
- Confirm all cluster nodes are healthy
- Review available disk space and system resources
- Notify users about potential service interruptions
- Schedule a maintenance window for Stage 2 upgrades

For production deployments, OPSWAT strongly recommends validating the upgrade procedure in a staging environment first.

---

## [Why the Upgrade Is Split Into Two Stages](/docs/mdcluster/upgrade/system-upgrade#why-the-upgrade-is-split-into-two-stages)

MD Cluster includes both application services and shared infrastructure services. Application services can typically be upgraded with minimal impact to running scans. Critical infrastructure services are different.

Services such as:

- PostgreSQL
- Redis
- File Storage
- Identity Service

are shared dependencies used throughout the cluster. These services support:

- Authentication and authorization
- Queue coordination
- Metadata storage
- Workflow synchronization
- File access and retrieval
- Internal service communication

Because these components affect the entire cluster, they require additional care and should only be upgraded during a planned maintenance window.

---

## [Stage 1 — Live Upgrade](/docs/mdcluster/upgrade/system-upgrade#stage-1--live-upgrade)

This stage upgrades services that can be updated while file scanning continues.

Although some management functionality may be temporarily unavailable, active file processing is not interrupted.

Services included:

- MD Cluster Identity Service
- MD Cluster Control Center
- MD Cluster Worker
- MD Core
- MD Cluster API Gateway
- MD Cluster Callback Service

---

### [1. Upgrade MD Cluster Identity Service](/docs/mdcluster/upgrade/system-upgrade#1-upgrade-md-cluster-identity-service)

The MD Cluster Identity Service controls authentication and API authorization throughout the cluster.

**Expected Impact:**

- API authentication becomes temporarily unavailable.
- New authenticated requests cannot be submitted.
- Existing running scans continue processing.

**Upgrade Procedure:**

1. Download the MD Cluster Identity Service installer package from [My OPSWAT](https://my.opswat.com/portal/home/metadefender-cluster).
2. Run the appropriate command for your operating system.

BashCopy# Windows
> msiexec.exe /i <md_cluster_identity_package>.msi /qn
# Debian/Ubuntu
$ sudo dpkg -i <md_cluster_identity_package> || sudo apt install -f
# Rocky/RHEL
$ sudo dnf install <md_cluster_identity_package> -y

3. Verify the service status.

BashCopy# Windows - PowerShell
> Get-Service md-cluster-identity-service
# Debian/Ubuntu/Rocky/RHEL
$ sudo systemctl status md-cluster-identity-service

---

### [2. Upgrade MD Cluster Control Center](/docs/mdcluster/upgrade/system-upgrade#2-upgrade-md-cluster-control-center)

The MD Cluster Control Center upgrade only affects the management interface.

**Expected Impact:**

- The web console may be temporarily unavailable.
- File scanning and processing continue normally.

**Upgrade Procedure:**

1. Download the MD Cluster Control Center installer package from [My OPSWAT](https://my.opswat.com/portal/home/metadefender-cluster).
2. Run the appropriate command for your operating system.

BashCopy# Windows
msiexec.exe /i <md_cluster_control_center_package>.msi /qn
# Debian/Ubuntu
sudo dpkg -i <md_cluster_control_center_package> || sudo apt install -f
# Rocky/RHEL
sudo dnf install <md_cluster_control_center_package> -y

3. Verify the service status.

BashCopy# Windows PowerShell
Get-Service md-cluster-control-center
# Linux
sudo systemctl status md-cluster-control-center

---

### [3. Upgrade MD Cluster Worker](/docs/mdcluster/upgrade/system-upgrade#3-upgrade-md-cluster-worker)

MD Cluster Worker can be upgraded without interrupting active file scans.

**Expected Impact:**

The following worker-related features may be temporarily unavailable during the upgrade:

- System Health
- System Activity
- Workflow Synchronization
- Support Package generation
- Automated deployment operations

**Upgrade Procedure:**

1. Sign in to MD Cluster Control Center console using your administrator account.
2. Go to `Inventory`> `Workers` .
3. In the notification banner, click `Upgrade Now`, then confirm the upgrade action.
4. Monitor the upgrade progress and verify that all Workers are running the same latest version.

See [Upgrade Workers](/docs/mdcluster/operating/operating-workers#upgrade-workers) for more details.

---

### [4. Upgrade Execution Instances](/docs/mdcluster/upgrade/system-upgrade#4-upgrade-execution-instances)

This step includes upgrading:

- MD Core
- MD Cluster API Gateway
- MD Cluster Callback Service

**Expected Impact:**

- MD Core instances can be upgraded gradually using a rolling upgrade.
- Single-instance MD Cluster API Gateway or Callback Service deployments may experience a brief interruption.

**Upgrade Procedure:**

1. Download the [MD Core](https://my.opswat.com/portal/home/metadefender-core), [MD Cluster API Gateway](https://my.opswat.com/portal/home/metadefender-cluster) or [MD Cluster Callback Service](https://my.opswat.com/portal/home/metadefender-cluster) installer packages from My OPSWAT.
2. Sign in to the Control Center console using your administrator account.
3. Navigate to `Inventory`>`Installers`.
4. Click `Upload Package` and upload the installer packages. For detailed upload instructions, see [here](/docs/mdcluster/operating/md-cluster-operating-installer).
5. Go to `Inventory`>`Workers`.
6. Expand `Deploy Workers` and select `Upgrade`.
7. Select the appropriate version of MD Core or MD Cluster API Gateway or MD Cluster Callback Service, then click `Upgrade` to start the process. See [Upgrade Instances](/docs/mdcluster/operating/operating-workers#upgrade-instances) for more information.

---

## [Stage 2 — Critical Infrastructure Upgrade](/docs/mdcluster/upgrade/system-upgrade#stage-2--critical-infrastructure-upgrade)

This stage upgrades services that the entire cluster depends on.

These services must be upgraded carefully because interruptions can affect cluster-wide functionality, including authentication, queue processing, metadata operations, and file availability.

A maintenance window is required before continuing.

The following services are considered critical infrastructure components within MD Cluster:

| Service | Purpose |
| --- | --- |
| PostgreSQL | Stores cluster configuration, operational state, processing result and executive data |
| RabbitMQ | Coordinate tasks between components |
| Redis | Handles caching, and internal coordination |
| MD Cluster File Storage | Stores files, scan artifacts, and deployment packages |

---

### [Before Upgrading](/docs/mdcluster/upgrade/system-upgrade#before-upgrading)

We recommend completing the following checks before proceeding:

- Stop submitting new scan requests
- Allow all in-progress scans to complete
- Confirm the cluster is idle
- Ensure PostgreSQL, RabbitMQ, Redis, and MD Cluster File Storage are healthy before proceeding

Info

Interrupting critical infrastructure services while scans are still processing may lead to failed requests, incomplete workflows, temporary data inconsistency, or service interruptions across the cluster.

---

### [1. Verify That Processing Has Completed](/docs/mdcluster/upgrade/system-upgrade#1-verify-that-processing-has-completed)

Before starting Stage 2:

1. Log in to the Control Center web console.
2. Navigate to `Dashboard` > `Processing History` .
3. Filter requests by **In-Progress.**

4. Wait until all requests are completed.

Warning

Only continue after the cluster is no longer processing files.

---

### [2. Upgrade MD Cluster File Storage](/docs/mdcluster/upgrade/system-upgrade#2-upgrade-md-cluster-file-storage)

MD Cluster File Storage is one of the most critical services in MD Cluster.

Most cluster operations depend on MD Cluster File Storage, including:

- File scanning
- File retrieval
- Module distribution
- Instance deployment

Because of this dependency, MD Cluster File Storage should always be upgraded last.

**Expected Impact**

- File processing may become temporarily unavailable
- Scan operations may pause
- Internal services depending on shared storage may be interrupted

**Upgrade Procedure**

1. Download the MD Cluster File Storage installer package from [My OPSWAT](https://my.opswat.com/portal/home/metadefender-cluster).
2. Run the appropriate command for your operating system.

BashCopy# Windows
msiexec.exe /i <md_cluster_file_storage_package>.msi /qn
# Debian/Ubuntu
sudo dpkg -i <md_cluster_file_storage_package> || sudo apt install -f
# Rocky/RHEL
sudo dnf install <md_cluster_file_storage_package> -y

3. Verify the service status.

BashCopy# Windows PowerShell
Get-Service md-cluster-file-storage
# Linux
sudo systemctl status md-cluster-file-storage
### [3. Upgrade Lake and Warehouse](/docs/mdcluster/upgrade/system-upgrade#3-upgrade-lake-and-warehouse)

1. On the machine hosting MD Cluster **Control Center**, navigate to the folder:

BashCopy# Windows
cd 'C:\Program Files\OPSWAT\MetaDefender Cluster Control Center'
# Linux
cd /usr/sbin

2. Run the following command to upgrade **Data Lake**:

BashCopymd-cluster-dbready --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --target=lake

3. Run the following command to upgrade **Data Warehouse**:

BashCopymd-cluster-dbready --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --lake-host=<lake-postgres-host> --lake-port=<lake-postgres-port> --lake-user=<lake-postgres-user> --lake-password=<lake-postgres-password> --target=warehouseInfo

If the Data Lake and Data Warehouse are hosted on the same PostgreSQL instance, a combined setup command can be used:

`md-cluster-dbready --host=<postgres-host> --port=<postgres-port> --user=<postgres-user> --password=<postgres-password> --target=lake,warehouse`

---

## [After the Upgrade](/docs/mdcluster/upgrade/system-upgrade#after-the-upgrade)

After completing all upgrade stages:

- Verify all services are healthy
- Confirm workers reconnect successfully
- Run test scan requests
- Validate API accessibility
- Review cluster logs for warnings or migration failures

---

## [Best Practices](/docs/mdcluster/upgrade/system-upgrade#best-practices)

- Perform upgrades during low-traffic periods
- Always back up PostgreSQL, Redis, RabbitMQ and MD Cluster File Storage before maintenance
- Avoid leaving the cluster in a mixed-version state
- Upgrade critical infrastructure services carefully and sequentially
- Monitor cluster health throughout the upgrade process

Info

Critical infrastructure services are foundational to cluster stability. Careful planning and controlled upgrades help prevent extended outages and operational inconsistencies.
