<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-system-requirements -->

# System requirements

This page describes the software dependencies and recommended system requirements for deploying MetaDefender Cluster (MD Cluster) components on supported Windows and Linux platforms. Review these requirements before installation to ensure your environment is properly prepared for a stable and supported deployment.

## [Windows](/docs/mdcluster/installation/md-cluster-system-requirements#windows)

### [PostgreSQL](/docs/mdcluster/installation/md-cluster-system-requirements#postgresql)

- **Supported version:** 16.9 or later
- **System requirements:**

  - 8 CPU cores
  - 16 GB RAM
  - 5 Gbps network bandwidth
  - 1 TB SSD or NVMe storage

Info

For a deployment with 5 MD Core instances, each running 8 AV engines, approximately 4 GB of disk space is needed to store 1 million objects.

---

### [RabbitMQ](/docs/mdcluster/installation/md-cluster-system-requirements#rabbitmq)

- **Supported version:** 4.2 or later
- **Dependencies:**

  - 64-bit Erlang/OTP. Please refer to [the link](https://www.rabbitmq.com/docs/which-erlang#compatibility-matrix) for the Erlang-RabbitMQ compatibility matrix.
- **System requirements:**

  - 4 CPU cores
  - 8 GB RAM
  - 1 Gbps network bandwidth
  - 100 GB storage

---

### [MD Cluster File Storage](/docs/mdcluster/installation/md-cluster-system-requirements#md-cluster-file-storage)

- **Supported version:** 2.6.0
- **Dependencies:**

  - [Microsoft Visual C++ Redistributable 2019](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  - Version 14.29.30139.0 or later
- **Recommended system requirements:**

  - 8 CPU cores
  - 8 GB RAM
  - 5 Gbps network bandwidth
  - 1 TB SSD or NVMe storage

Info

The available storage volume should be at least twice the total size of files submitted to the MD Cluster API Gateway at the same time.

If CDR or DLP engines are installed on MD Core instances, the required file storage volume should be doubled.

---

### [MD Cluster Control Center](/docs/mdcluster/installation/md-cluster-system-requirements#md-cluster-control-center)

- **Supported version:** 2.6.0
- **Dependencies:**

  - [Microsoft Visual C++ Redistributable 2019](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  - Version 14.29.30139.0 or later
- **Recommended system requirements:**

  - 4 CPU cores
  - 4 GB RAM
  - 1 Gbps network bandwidth
  - 100 GB storage

---

### [MD Cluster Identity Service](/docs/mdcluster/installation/md-cluster-system-requirements#md-cluster-identity-service)

- **Supported version:** 2.6.0
- **Dependencies:**

  - [Microsoft Visual C++ Redistributable 2019](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  - Version 14.29.30139.0 or later
- **Recommended system requirements:**

  - 4 CPU cores
  - 4 GB RAM
  - 1 Gbps network bandwidth
  - 50 GB storage

---

### [Worker hosting MD Cluster API Gateway](/docs/mdcluster/installation/md-cluster-system-requirements#worker-hosting-md-cluster-api-gateway)

- **Supported version:** 2.6.0
- **Dependencies:**

  - [Microsoft Visual C++ Redistributable 2019](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  - Version 14.29.30139.0 or later
- **Recommended system requirements:**

  - 8 CPU cores
  - 16 GB RAM
  - 5 Gbps network bandwidth
  - 50 GB storage

---

### [Worker hosting MD Core](/docs/mdcluster/installation/md-cluster-system-requirements#worker-hosting-md-core)

- **Supported version:** 2.6.0
- **Dependencies:**

  - [Microsoft Visual C++ Redistributable 2019](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  - Version 14.29.30139.0 or later
- **Recommended system requirements:**

  - Refer [here](https://www.opswat.com/docs/mdcore/installation/recommended-system-configuration#windows-supported-operating-systems) for detailed requirements

---

### [Notes](/docs/mdcluster/installation/md-cluster-system-requirements#notes)

- MetaDefender Cluster requires **WMIC** to be enabled. Run the following command in Command Prompt as Administrator:

PowershellCopyDISM /Online /Add-Capability /CapabilityName:WMIC

---

## [Debian / Ubuntu / Red Hat / Rocky](/docs/mdcluster/installation/md-cluster-system-requirements#debian--ubuntu--red-hat--rocky)

### [PostgreSQL](/docs/mdcluster/installation/md-cluster-system-requirements#postgresql)

- **Supported version:** 16.9 or later
- **System requirements:**

  - 8 CPU cores
  - 16 GB RAM
  - 5 Gbps network bandwidth
  - 1 TB SSD or NVMe storage

Info

For a deployment with 5 MD Core instances, each running 8 AV engines, approximately 4 GB of disk space is needed to store 1 million objects.

---

### [Redis](/docs/mdcluster/installation/md-cluster-system-requirements#redis)

- **Supported version:** 7.2 or later
- **System requirements:**

  - 2 CPU cores
  - 32 GB RAM
  - 5 Gbps network bandwidth
  - 20 GB storage

---

### [RabbitMQ](/docs/mdcluster/installation/md-cluster-system-requirements#rabbitmq)

- **Supported version:** 4.2 or later
- **Dependencies:**

  - 64-bit Erlang/OTP. Please refer to [the link](https://www.rabbitmq.com/docs/which-erlang#compatibility-matrix) for the Erlang-RabbitMQ compatibility matrix.
- **System requirements:**

  - 4 CPU cores
  - 8 GB RAM
  - 1 Gbps network bandwidth
  - 100 GB storage

---

### [MD Cluster File Storage](/docs/mdcluster/installation/md-cluster-system-requirements#md-cluster-file-storage)

- **Supported version:** 2.6.0
- **Required packages/tools:**

  - uuid
  - tar
  - lsb_release
- **Recommended system requirements:**

  - 8 CPU cores
  - 8 GB RAM
  - 5 Gbps network bandwidth
  - 1 TB SSD or NVMe storage

Info

The available storage volume should be at least twice the total size of files submitted to the MD Cluster API Gateway at the same time.

If CDR or DLP engines are installed on MD Core instances, the required file storage volume should be doubled.

---

### [MD Cluster Control Center](/docs/mdcluster/installation/md-cluster-system-requirements#md-cluster-control-center)

- **Supported version:** 2.6.0
- **Required packages/tools:**

  - uuid
  - tar
  - lsb_release
- **Recommended system requirements:**

  - 4 CPU cores
  - 4 GB RAM
  - 1 Gbps network bandwidth
  - 100 GB storage

---

### [MD Cluster Identity Service](/docs/mdcluster/installation/md-cluster-system-requirements#md-cluster-identity-service)

- **Supported version:** 2.6.0
- **Required packages/tools:**

  - uuid
  - tar
  - lsb_release
- **Recommended system requirements:**

  - 4 CPU cores
  - 4 GB RAM
  - 1 Gbps network bandwidth
  - 50 GB storage

---

### [Worker hosting MD Cluster API Gateway](/docs/mdcluster/installation/md-cluster-system-requirements#worker-hosting-md-cluster-api-gateway)

- **Supported version:** 2.6.0
- **Required packages/tools:**

  - uuid
  - tar
  - lsb_release
  - jq
  - curl
- **Recommended system requirements:**

  - 4 CPU cores
  - 8 GB RAM
  - 5 Gbps network bandwidth
  - 50 GB storage

---

### [Worker hosting MD Core](/docs/mdcluster/installation/md-cluster-system-requirements#worker-hosting-md-core)

- **Supported version:** 2.6.0
- **Required packages/tools:**

  - uuid
  - tar
  - lsb_release
  - jq
  - curl
- **Recommended system requirements:**

  - Refer [here](https://www.opswat.com/docs/mdcore/installation/recommended-system-configuration#linux-supported-operating-systems) for detailed requirements

---

### [Notes](/docs/mdcluster/installation/md-cluster-system-requirements#notes)

- MD Cluster requires `uuid`, `tar`, `curl` , `jq` to be installed. Run the following command in Terminal to install them:

BashCopy# Debian/Ubuntu
sudo apt install -y uuid curl jq tar
# Red Hat/Rocky
sudo dnf install -y libuuid curl jq tar

- MD Cluster requires `lsb_release` on Rocky Linux. Run the following commands in Terminal to install it:

BashCopysudo dnf install -y yum-utils
sudo dnf config-manager --set-enabled devel
sudo dnf update -y
sudo dnf install -y redhat-lsb-core
