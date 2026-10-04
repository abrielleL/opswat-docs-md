<!-- source: https://www.opswat.com/docs/supply-chain/installation/offline-installation -->

# Linux Offline Installation

This guide provides step-by-step instructions for installing MetaDefender Software Supply Chain and its dependencies on machines with limited or no internet connectivity.

A machine with internet access is required to download the dependencies manually and transfer them to the offline machine.

## [Installing Binary Packages](https://www.opswat.com/docs/mdss/installation/linux-offline-installation#installing-binary-packages)

You will need to download and install the binary packages(found in [Installation details](https://www.opswat.com/docs/supply-chain/installation/system-requirements-for-unix-based-deployments#installation-details)) for your respective operating system:

#### Debian/Ubuntu

```bash
curl, openssl, sudo, apt-utils, ca-certificates, jq, gnupg-agent, iproute2, apt-transport-https,  software-properties-common
```

#### RedHat/CentOS

```bash
curl, openssl, sudo, apt-utils, ca-certificates, jq, gnupg-agent, iproute2, apt-transport-https,  software-properties-common
```

> **Info**
>
> **Note:** For detailed instructions, refer to the guide for [Debian/Ubuntu](https://help.ubuntu.com/community/InstallingSoftware) or [CentOS/RHEL](https://stackoverflow.com/questions/40382412/install-packages-without-internet-red-hat)

## Installing Docker and Docker Compose

To be able to install the dependencies offline, you need a machine connected to the internet to download the required packages. Later, the packages will be copied to the offline machine.

To download the dependencies, follow the official guide for [Docker Engine](https://docs.docker.com/engine/install/binaries/) and [Docker Compose](https://docs.docker.com/compose/install/)

The compose plugin for docker can be installed only manually when in an offline environment using the following commands (also available in the official instructions in the link above):

```bash
mkdir -p /usr/local/lib/docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.28.0/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose

sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
```

> **Warning**
>
> For RedHat based operating systems:
>
> Since RedHat officially supports Podman as a container engine, skip Docker installation and follow our guide on [Podman Configuration](https://www.opswat.com/docs/mdss/installation/linux-installation#podman-configuration).

## Installing MetaDefender Software Supply Chain package

After the prerequisites above have been set up, you can run the MetaDefender Software Supply Chain  installer to setup the compose files and the mdssc command line.

#### Debian/Ubuntu

```bash
sudo dpkg -i <name of the file>.deb || sudo apt-get install -f
```

#### RedHat/CentOS

```bash
sudo yum install -y <name of the file>.rpm
```

## Loading Docker Images

In offline environments, all required Docker images must be downloaded on an internet-connected machine and transferred to the target system. For RHEL installations, the offline toolkit is the recommended method. Use the manual pull and export method below for other operating systems.

#### Recommended: Load images using the offline toolkit (RHEL only)

For RHEL installations, download the 4.1.0 offline or portable toolkit and its corresponding checksum from My OPSWAT -> [Product Downloads](https://my.opswat.com/home/metadefender-software-supply-chain). Download the files on an internet-connected machine and transfer them to the offline machine.

Extract the offline toolkit and load the images:

```bash
tar -xzf mdssc-offline-4.1.0.tar.gz
cd mdssc-offline-4.1.0
sudo ./mdssc.sh -u load_images
```

#### Manual method: Pull and export images

#### Required Images

MetaDefender Software Supply Chain requires:

- MDSSC service images
- OPSWAT platform services
- Third-party infrastructure images (database, cache, messaging)

All images are versioned per release.

Use the following placeholders:

- `<MDSSC_VERSION>` — e.g. `4.1.0`
- `<PLATFORM_VERSION>` — e.g. `platform-2.x`

#### Step 1: Pull Images (Online Machine)

```bash
docker pull docker.io/opswat/mdssc_api:4.1.0
docker pull docker.io/opswat/mdssc_frontend:4.1.0
docker pull docker.io/opswat/mdssc_binaries:4.1.0
docker pull docker.io/opswat/mdssc_sourcecode:4.1.0
docker pull docker.io/opswat/mdssc_containers:4.1.0
docker pull docker.io/opswat/mdssc_notifications:4.1.0
docker pull docker.io/opswat/mdssc_processing:4.1.0
docker pull docker.io/opswat/mdssc_pgmigrations:4.1.0

docker pull docker.io/library/postgres:17
docker pull docker.io/library/rabbitmq:4.2.2-alpine
docker pull docker.io/library/redis:8.4.0-alpine

docker pull docker.io/opswat/mdcloudservices_commonservices:platform-2.5.1
docker pull docker.io/opswat/mdcloudservices_mdplatform:platform-2.5.1
docker pull docker.io/opswat/mdcloudservices_licensing:platform-2.5.1
docker pull docker.io/opswat/mdcloudservices_identityservice:platform-2.5.1
```

> **Info**
>
> Can be tried on the offline machine also with the Docker whitelist: [Allowlist | Docker Docs](https://docs.docker.com/desktop/setup/allow-list/)

#### Step 2: Export Images

```bash
docker save \
  opswat/mdssc_api:<MDSSC_VERSION> \
  opswat/mdssc_frontend:<MDSSC_VERSION> \
  opswat/mdssc_binaries:<MDSSC_VERSION> \
  opswat/mdssc_sourcecode:<MDSSC_VERSION> \
  opswat/mdssc_containers:<MDSSC_VERSION> \
  opswat/mdssc_notifications:<MDSSC_VERSION> \
  opswat/mdssc_processing:<MDSSC_VERSION> \
  opswat/mdssc_mongomigrations:<MDSSC_VERSION> \
  opswat/mdssc_pgmigrations:<MDSSC_VERSION> \
  opswat/mdcloudservices_commonservices:<PLATFORM_VERSION> \
  opswat/mdcloudservices_licensing:<PLATFORM_VERSION> \
  mongo:<MONGO_VERSION> \
  postgres:<POSTGRES_VERSION> \
  redis:<REDIS_VERSION> \
  rabbitmq:<RABBITMQ_VERSION> \
  -o mdssc.tar
```

#### Step 3: Load Images (Offline Machine)

```bash
docker load -i mdssc.tar
# Check result
docker image ls
```

## [Podman Configuration](https://www.opswat.com/docs/mdss/installation/linux-installation#podman-configuration)

MDSSC can also run using the Podman container engine instead of the default Docker one on RHEL operating systems. `Podman`, `podman-docker` and `docker-compose` need to be installed and running before installing MDSSC.

After the installation is complete, MDSSC needs to be configured to skip the checks for the default Docker engine. This is done by setting `SKIP_DOCKER_CHECKS=yes` in the `/etc/mdssc/customer.env` file. The following commands can be used to install Podman and MDSSC on RHEL.

```bash
# install podman, podman-docker and docker-compose
sudo yum install podman
sudo yum install podman-docker
sudo curl -SL https://github.com/docker/compose/releases/download/v2.15.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

sudo systemctl enable podman.socket
sudo systemctl start podman.socket

# disable SELinux temporarily
setenforce 0
# to disable selinux permanetly 'SELINUX=disabled' needs to be set in the following config file
sudo vim /etc/selinux/config

# install additional MDSSC dependencies
sudo subscription-manager repos --enable codeready-builder-for-rhel-8-$(arch)-rpms
sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum install lvm2
sudo yum install wget

# install MDSSC
sudo rpm -i mdssc-x.x.x.noarch.rpm

# edit customer.env and add SKIP_DOCKER_CHECKS=yes
sudo vim /etc/mdssc/customer.env

# start MDSSC
sudo mdssc -c start
```

## Starting  MetaDefender Software Supply Chain

Finally, MDSSC can be started using the regular startup command:

```bash
sudo mdssc -c start
```

## Next Steps

Once the MetaDefender Software Supply Chain services are running, a few additional steps are required before the system is fully operational:

1. **Activate your license** You must upload and apply a valid license to enable functionality. For details, see offline license activation section from [License Page](https://www.opswat.com/docs/supply-chain/configuration/license).
2. **Configure a Scan Pool** At least one scan instance is required to analyze source code, containers or artifacts. For details, see [Scan Pools](https://www.opswat.com/docs/supply-chain/configuration/scan-pools).

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
