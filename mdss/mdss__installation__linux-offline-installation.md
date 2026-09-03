<!-- source: https://www.opswat.com/docs/mdss/installation/linux-offline-installation -->

# Linux Offline Installation

This guide provides detailed instructions for installing MetaDefender Storage Security and its dependencies on machines with limited or no internet connectivity. A machine connected to the internet will be needed to download the dependencies manually and copy them to the offline machine.

## [Installing Binary Packages](/docs/mdss/installation/linux-offline-installation#installing-binary-packages)

You will need to download and install the following binary packages for your respective operating system:

#### [Debian/Ubuntu](/docs/mdss/installation/linux-offline-installation#debianubuntu)

Debian packagesCopycurl, openssl, sudo, apt-utils, ca-certificates, jq, gnupg-agent, iproute2, apt-transport-https, software-properties-common
#### [RedHat/CentOS](/docs/mdss/installation/linux-offline-installation#redhatcentos)

CentOS packagesCopycurl, openssl, sudo, yum-utils, ca-certificates, jq, gnupg2, iproute, lvm2, wget, device-mapper-persistent-dataInfo

**Note:** For detailed instructions, refer to the guide for [Debian/Ubuntu](https://help.ubuntu.com/community/InstallingSoftware) or [CentOS/RHEL](https://stackoverflow.com/questions/40382412/install-packages-without-internet-red-hat)

## [Option 1: Using installers](/docs/mdss/installation/linux-offline-installation#option-1-using-installers)

This option uses the the official installation methods for docker and docker-compose to create an offline docker environment where the MDSS installer from the MyOPSWAT portal can be used to deploy MDSS containers. If for some reason this method cannot be used on the target deployment machine then skip to **Option 2** below.

#### [Installing Docker and Docker Compose](/docs/mdss/installation/linux-offline-installation#installing-docker-and-docker-compose)

To be able to install the dependencies offline, you need a machine connected to the internet to download the required packages. Later, the packages will be copied to the offline machine.

To download the dependencies, follow the official guide for [Docker Engine](https://docs.docker.com/engine/install/binaries/) and [Docker Compose](https://docs.docker.com/compose/install/)

The compose plugin for docker can be installed only manually when in an offline environment using the following commands (also available in the official instructions in the link above):

BashCopymkdir -p /usr/local/lib/docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.28.0/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
#### [Installing MetaDefender Storage Security package](/docs/mdss/installation/linux-offline-installation#installing-metadefender-storage-security-package)

After the prerequisites above have been set up, you can run the MetaDefender Storage Security installer to setup the compose files and the mdss command line.

#### [Debian/Ubuntu](/docs/mdss/installation/linux-offline-installation#debianubuntu)

BashCopysudo dpkg -i <name of the file>.deb || sudo apt-get install -f
#### [RedHat/CentOS](/docs/mdss/installation/linux-offline-installation#redhatcentos)

BashCopysudo yum install -y <name of the file>.rpm
#### [Loading Docker images](/docs/mdss/installation/linux-offline-installation#loading-docker-images)

**MetaDefender Storage Security** is composed of several Docker images that need to be pulled from an online repository. For offline installations, these images are available on the MyOPSWAT portal under **MetaDefender Storage Security** in the **MetaDefender Storage Security Offline Docker Toolkit** section:

Next, you need to extract the `mdss.tar` archive and transfer it to the offline machine. Once the file is on the offline machine, use the following command to load the Docker images:

BashCopydocker load -i <archive_path>\mdss.tar
#### [Starting MetaDefender Storage Security](/docs/mdss/installation/linux-offline-installation#starting-metadefender-storage-security)

Finally, MDSS can be started using the regular startup command:

BashCopysudo mdss -c start
## [Option 2: using bundled binaries](/docs/mdss/installation/linux-offline-installation#option-2-using-bundled-binaries)

Using this method you will only need to download the same MetaDefender Storage Security Offline Docker Toolkit as above without needing to pre-install docker and docker-compose or use the MDSS installer. It's still recommended to have all prerequisites installed before continuing.

#### [Download and extract the offline toolkit](/docs/mdss/installation/linux-offline-installation#download-and-extract-the-offline-toolkit)

The offline toolkit is available on the **MyOPSWAT** portal under **MetaDefender Storage Security** in the **MetaDefender Storage Security Offline Docker Toolkit** section. The package needs to be extracted to the desired path on the target offline machine and the following steps should all be performed from the same path where the package is extracted on the offline machine.

#### [Load docker images](/docs/mdss/installation/linux-offline-installation#load-docker-images)

To load the MDSS docker images run the following command from the same path where the offline package is extracted:

BashCopysudo ./mdss.sh -u load_images
#### [Starting MetaDefender Storage Security](/docs/mdss/installation/linux-offline-installation#starting-metadefender-storage-security)

Finally, MDSS can be started using the regular startup command but specifying the local path to the `mdss.sh` script from the offline package:

BashCopysudo ./mdss.sh -c start

Using this method, all mdss commands (start, stop etc.) will need to be executed from the same path where the package is extracted.

### [Updating MetaDefender Storage Security Offline](/docs/mdss/installation/linux-offline-installation#updating-metadefender-storage-security-offline)

Info

To update MetaDefender Storage Security while in offline mode the same steps can be followed but with the latest installer and offline package, detailed instructions are outlined in the [Offline Update Guide](https://www.opswat.com/docs/mdss/installation/upgrading-from-a-previous-version#offline-upgradeding-from-a-previous-version#offline-upgrade)
