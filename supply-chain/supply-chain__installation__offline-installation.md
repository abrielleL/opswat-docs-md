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
sudo yum install -y --disablerepo="*" ./<name of the file>.rpm
```

`--disablerepo="*"` is required on an offline machine. Otherwise, yum tries to refresh repository metadata and fails before installing the local file.

## Pulling the  Docker Images

In offline environments, all required Docker images must be pulled on an internet-connected machine and transferred to the target system.

#### Required Images

MetaDefender Software Supply Chain requires:

- MDSSC service images
- OPSWAT platform services
- Third-party infrastructure images (database, cache, messaging)

All images are versioned per release.

Use the following placeholders:

- `<MDSSC_VERSION>` — e.g. `4.0.0`
- `<PLATFORM_VERSION>` — e.g. `platform-2.x`

#### Step 1: Pull Images (Online Machine)

```bash
docker pull docker.io/opswat/mdssc_api:4.0.0
docker pull docker.io/opswat/mdssc_frontend:4.0.0
docker pull docker.io/opswat/mdssc_binaries:4.0.0
docker pull docker.io/opswat/mdssc_sourcecode:4.0.0
docker pull docker.io/opswat/mdssc_containers:4.0.0
docker pull docker.io/opswat/mdssc_notifications:4.0.0
docker pull docker.io/opswat/mdssc_pgmigrations:4.0.0

docker pull docker.io/library/postgres:17
docker pull docker.io/library/rabbitmq:4.2.4-alpine
docker pull docker.io/library/redis:8.6.0-alpine

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
  opswat/mdssc_pgmigrations:<MDSSC_VERSION> \
  opswat/mdcloudservices_commonservices:<PLATFORM_VERSION> \
  opswat/mdcloudservices_mdplatform:<PLATFORM_VERSION> \
  opswat/mdcloudservices_identityservice:<PLATFORM_VERSION> \
  opswat/mdcloudservices_licensing:<PLATFORM_VERSION> \
  postgres:<POSTGRES_VERSION> \
  rabbitmq:<RABBITMQ_VERSION> \
  redis:<REDIS_VERSION> \
  -o mdssc.tar
```

The version placeholders for 4.0.4 are: `<MDSSC_VERSION>` = `4.0.4`, `<PLATFORM_VERSION>` = `platform-2.5.1`, `<POSTGRES_VERSION>` = `17`, `<RABBITMQ_VERSION>` = `4.2.4-alpine`, and `<REDIS_VERSION>` = `8.6.0-alpine`.

#### Step 3: Load Images (Offline Machine)

```bash
docker load -i mdssc.tar
# Check result
docker image ls
```

#### Alternative: Offline Toolkit

Download the offline toolkit and the RPM or DEB package for the same version on an internet-connected machine, then transfer both files to the offline machine. The RPM is available on the My.OPSWAT portal or at `https://metascanbucket.s3.amazonaws.com/Metadefender/MetaDefender_Software_Supply_Chain/<VERSION>/mdssc-<VERSION>.noarch.rpm`.

```bash
curl -O https://metascanbucket.s3.amazonaws.com/Metadefender/MetaDefender_Software_Supply_Chain_Offline/<VERSION>/mdssc-offline-<VERSION>.tar.gz
curl -O https://metascanbucket.s3.amazonaws.com/Metadefender/MetaDefender_Software_Supply_Chain_Offline/<VERSION>/mdssc-offline-<VERSION>.tar.gz.sha256
sha256sum -c mdssc-offline-<VERSION>.tar.gz.sha256

tar -xzf mdssc-offline-<VERSION>.tar.gz
cd mdssc-offline-<VERSION>
sudo ./mdssc.sh -u load_images
```

## [Podman Configuration](https://www.opswat.com/docs/mdss/installation/linux-installation#podman-configuration)

MDSSC can also run using the Podman container engine instead of the default Docker one on RHEL operating systems. `Podman`, `podman-docker` and `docker-compose` need to be installed and running before installing MDSSC.

After the installation is complete, MDSSC needs to be configured to skip the checks for the default Docker engine. This is done by setting `SKIP_DOCKER_CHECKS=yes` in the `/etc/mdssc/customer.env` file. The following commands can be used to install Podman and MDSSC on RHEL.

> **Note**
>
> The SELinux step below applies to Podman deployments only. With Docker, SELinux can remain in Enforcing mode.

```bash
# install podman, podman-docker and docker-compose
sudo yum install podman
sudo yum install podman-docker
sudo curl -SL https://github.com/docker/compose/releases/download/v2.15.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

sudo systemctl enable podman.socket
sudo systemctl start podman.socket

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

## Verify the installation

```bash
sudo mdssc -c status
sudo mdssc -v
sudo docker ps
```

Expect about 14 running containers and the version you installed. The web interface answers on `https://<server IP>` when HTTPS is enabled.

## Next Steps

Once the MetaDefender Software Supply Chain services are running, a few additional steps are required before the system is fully operational:

1. **Activate your license** You must upload and apply a valid license to enable functionality. For details, see offline license activation section from [License Page](https://www.opswat.com/docs/supply-chain/configuration/license).
2. **Configure a Scan Pool** At least one scan instance is required to analyze source code, containers or artifacts. For details, see [Scan Pools](https://www.opswat.com/docs/supply-chain/configuration/scan-pools).
