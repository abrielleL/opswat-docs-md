<!-- source: https://www.opswat.com/docs/supply-chain/sizing-guide/basic-deployments---system-requirements -->

# Basic deployments | System Requirements

### Minimum Hardware System Requirements

| **Hardware** | **Dedicated instance** | **Shared instance with MetaDefender Core** |
| ---- | ---- | ---- |
| CPU | 8 cores | 16 cores |
| RAM | 16 GB | 32 GB |
| Free disk space | 250 GB | 1 TB |

> **Note on System Requirements**
>
> Please be aware that the system requirements for our software are contingent upon the quantity and size of files being processed. Larger quantities or bigger files may demand more computational resources, such as memory and CPU power, for optimal performance. Ensure that you consider your anticipated workload when evaluating your system's capabilities.

## Supported Operating Systems

- CentOS 9.0+
- Red Hat Enterprise Linux 7.0+
- Debian 10.0+
- Ubuntu 18.04+
- Amazon Linux 2+

### [Installation details](https://docs.opswat.com/mdss/installation/system-requirements-for-unix-based-deployments#installation-details)

The default installation path for MetaDefender Software Supply-Chain resources is the `/etc/mdssc` folder.

The installation package will automatically install the following dependencies if they are not already present on the system:

| **Debian / Ubuntu** | **Red Hat Enterprise / CentOS** |
| ---- | ---- |
| - `curl` - `openssl` (uses the default version on the host) - `openssl` (the container uses version 3.5.5) - `ca-certificates` - `sudo` - `jq` - `iproute2` - `apt-utils` - `gnupg-agent` - `apt-transport-https` - `software-properties-common` | - `curl` - `openssl` (uses the default version on the host) - `openssl` (the container uses version 3.5.5) - `ca-certificates` - `sudo` - `jq` - `iproute` - `yum-utils` - `gnupg2` - `wget` - `device-mapper-persistent-data` - `lvm2` |

### [Installation components](https://www.opswat.com/docs/mdss/getting-started/unix-deployment#installation-components)

MetaDefender Software Supply-Chain automatically deploys the following components:

| **Name** | **Version** | **Type** |
| ---- | ---- | ---- |
| Docker Engine | system defined* | Containerization technology |
| Docker Compose | system defined* | Container orchestration |
| PostgreSQL | v17 | Database |
| RabbitMQ | v4.2.2 | Message broker |
| NGINX | `stable` | Web server |
| Redis | v8.4.0 | Data Cache (Redis compatible) |

Our system uses the existing Docker version if available. If not, it automatically downloads the latest stable version using the [docker-install](https://github.com/docker/docker-install) script.
