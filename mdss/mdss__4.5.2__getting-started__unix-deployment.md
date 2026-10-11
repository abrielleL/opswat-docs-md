<!-- source: https://www.opswat.com/docs/mdss/4.5.2/getting-started/unix-deployment -->

# Unix deployment

## Supported Operating Systems

| **Distribution** | **Supported versions** | Architecture |
| ---- | ---- | ---- |
| CentOS Stream | 9-x, 10-x (latest) | x86_64 (64-bit) |
| Red Hat Enterprise Linux **(podman only)** | 7.x, 8.x, 9.x (latest) | x86_64 (64-bit) |
| Rocky Linux **(podman only)** | 9.x, 10.x (latest) | x86_64 (64-bit) |
| Debian | 10.x, 11.x, 12.x (latest) | x86_64 (64-bit) |
| Ubuntu | 18.x, 19.x, 20.x, 21.x, 22.x, 23.x, 24.x (latest) | x86_64 (64-bit) |
| Amazon Linux | 2 | x86_64 (64-bit) |

## Installation details

The default installation path for MetaDefender Storage Security resources is the `/etc/mdss` folder.

The installation package will automatically install the following dependencies if they are not already present on the system:

| **Debian / Ubuntu** | **Red Hat Enterprise / CentOS** |
| ---- | ---- |
| - `curl` - `openssl` (uses the default version on the host) - `openssl` (the container uses version 3.2.0) - `ca-certificates` - `sudo` - `jq` - `iproute2` - `apt-utils` - `gnupg-agent` - `apt-transport-https` - `software-properties-common` | - `curl` - `openssl` (uses the default version on the host) - `openssl` (the container uses version 3.2.0) - `ca-certificates` - `sudo` - `jq` - `iproute` - `yum-utils` - `gnupg2` - `wget` - `device-mapper-persistent-data` - `lvm2` |

## Installation components

MetaDefender Storage Security automatically deploys the following components:

| **Name** | **Version** | **Type** |
| ---- | ---- | ---- |
| Docker Engine | system defined* | Containerization technology |
| Docker Compose | system defined* | Container orchestration |
| PostgreSQL | v17.0 | Database |
| RabbitMQ | v4.3.0 | Message broker |
| NGINX | v1.29.2 | Web server |
| Redis | v8.6.0-alpine | Data Cache |

Our system uses the existing Docker version if available. If not, it automatically downloads the latest stable version using the [docker-install](https://github.com/docker/docker-install)  script.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
