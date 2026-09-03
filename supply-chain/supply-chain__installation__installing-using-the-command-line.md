<!-- source: https://www.opswat.com/docs/supply-chain/installation/installing-using-the-command-line -->

# Linux Installation

## Preliminary notes

Before you begin the installation, please ensure that the [System requirements](https://www.opswat.com/docs/supply-chain/installation/system-requirements) are met and that [docker engine](https://docs.docker.com/engine/install/ubuntu/)  is already installed on the system..

If the MetaDefender Software Supply Chain installer package dependencies are not installed on your system the installer will attempt to automatically download them over the internet.

## Acquire the package

In order to acquire the package please visit My OPSWAT -> [Product Downloads](https://my.opswat.com/home/metadefender-software-supply-chain)

## Advanced installation

We recommend that production deployments use an external database and ensure that web traffic is encrypted. For detailed information on how to configure an external database or HTTPS see advanced installation section - [Advanced installation for Unix-based deployments](https://www.opswat.com/docs/supply-chain/installation/advanced-installation-for-unix-based-deployments).

## Debian / Ubuntu package (.deb)

1. Update your packages

```bash
sudo apt update
```

2. Install the necessary package dependencies

```bash
sudo apt install jq curl gnupg-agent software-properties-common
```

3. Move to the folder containing the installer and install it

```bash
sudo dpkg -i <name of the file>.deb || sudo apt-get install -f
```

4. After the installation is completed, check if everything went fine

```bash
man mdssc
```

or using the help menu

```bash
sudo mdssc -h
```

5. Run the following command in order to initialize MetaDefender Software Supply Chain

```bash
sudo mdssc -u init
```

6. Start the service

```bash
sudo mdssc -c start
```

7. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

8. Open a browser and navigate to the web interface: http://<server> to configure your deployment.

## Red Hat Enterprise Linux / CentOS package (.rpm)

> **Info**
>
> Please note that Docker Engine is officially supported only on RHEL s390x architecture, but you may be able to install it manually following the CentOS installation steps: [https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)
>
> On Rocky Linux, it is recommended to use Podman, as Podman is officially supported by Red Hat.

1. Update your packages

```bash
sudo yum -y update
```

2. Move to the folder containing the installer and install it

```bash
sudo yum install -y <name of the file>.rpm
```

3. After the installation is completed, check if everything went fine

```bash
sudo man mdssc
```

or using the help menu

```bash
sudo mdssc -h
```

4. Run the following command in order to initialize MetaDefender Software Supply Chain

```bash
sudo mdssc -u init
```

*Note:* If you don’t have docker already installed, the installer will do that for you, but you will be prompted to sign out and sign back in. This is necessary because your current user needs to be added to the docker group.

5. Start the service

```bash
sudo mdssc -c start
```

6. Optionally, you can check the status using the following command:

```bash
sudo mdssc -c status
```

7. Open a browser and navigate to the web interface: http://<server> to configure your deployment.
8. If you are using firewall (on CentOS8 and  RHEL 8) you may need to update it's policies:

```bash
# Check what interface docker is using, e.g. 'docker0'
ip link show
 
# Check available firewalld zones, e.g. 'public'
sudo firewall-cmd --get-active-zones
 
# Check what zone the docker interface it bound to, most likely 'no zone' yet
sudo firewall-cmd --get-zone-of-interface=docker0
 
# So add the 'docker0' interface to the 'public' zone. Changes will be visible only after firewalld reload
sudo nmcli connection modify docker0 connection.zone public
 
# Masquerading allows for docker ingress and egress (this is the juicy bit)
sudo firewall-cmd --zone=public --add-masquerade --permanent
# Optional open required incomming ports (wasn't required in my tests)
# sudo firewall-cmd --zone=public --add-port=443/tcp
# Reload firewalld
sudo firewall-cmd --reload
# Reload dockerd
sudo systemctl restart docker
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

## Next Steps

Once the MetaDefender Software Supply Chain services are running, a few additional steps are required before the system is fully operational:

1. **Activate your license** You must upload and apply a valid license to enable functionality. For details, see [License Page](https://www.opswat.com/docs/supply-chain/configuration/license).
2. **Configure a Scan Pool** At least one scan instance is required to analyze source code, containers or artifacts. For details, see [Scan Pools](https://www.opswat.com/docs/supply-chain/configuration/scan-pools).
