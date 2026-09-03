<!-- source: https://www.opswat.com/docs/supply-chain/installation/system-requirements-for-unix-based-deployments -->

# System requirements for Unix-based deployments

Supported Operating Systems

- CentOS 9.0+
- Red Hat Enterprise Linux 7.0+
- Debian 10.0+
- Ubuntu 18.04+
- Amazon Linux 2+

### System requirements

| **Hardware** | **Dedicated instance** | **Shared instance with MetaDefender Core** |
| ---- | ---- | ---- |
| CPU | 8 cores | 16 cores |
| RAM | 16 GB | 32 GB |
| Free disk space | 250 GB | 1 TB |

> **Note on System Requirements**
>
> Please be aware that the system requirements for our software are contingent upon the quantity and size of files being processed. Larger quantities or bigger files may demand more computational resources, such as memory and CPU power, for optimal performance. Ensure that you consider your anticipated workload when evaluating your system's capabilities.

### Installation details

MetaDefender Software Supply Chain default installation path is using the **/etc/mdssc** folder for storing resources. The package requires the following dependencies that are automatically installed if they don’t already exist on the system:

| **Debian / Ubuntu** | **Red Hat Enterprise / CentOS** |
| ---- | ---- |
| - curl - openssl (default version on host) - openssl (version 3.2.0 on container) - apt-transport-https - ca-certificates - gnupg-agent - software-properties-common - sudo - apt-utils - iproute2 - jq | - curl - openssl (default version on host) - openssl (version 3.2.0 on container) - yum-utils - device-mapper-persistent-data - lvm2 - ca-certificates - gnupg2 - sudo - iproute - wget - jq |

### Installation components

MetaDefender Software Supply Chain automatically deploys the following components:

| **Name** | **Version** | **Type** |
| ---- | ---- | ---- |
| Docker Engine | system defined* | Containerization technology |
| Docker-compose | system defined* | Container Orchestration |
| PostgreSQL | v17 | Database |
| RabbitMQ | v4.2.2 | Message broker |
| NGINX | *stable* | Web server |
| Redis | v8.4.0 | Data Cache  (Redis compatible) |

Our system uses the existing Docker version if available. If not, it automatically downloads the latest stable version using the [docker-install](https://github.com/docker/docker-install) script.
