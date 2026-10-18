<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/linux-installation -->

# Linux Installation

## Preliminary notes

Before you begin the installation, please ensure that the [system requirements](https://www.opswat.com/docs/mdss/getting-started/unix-deployment) are met.

If the MetaDefender Storage Security installer package dependencies are not installed on your system the installer will attempt to automatically download them over the internet.

## Acquire the package

In order to acquire the package please visit [https://www.opswat.com/solution](https://www.opswat.com/solutions)

> **Info**
>
> To limit the required resources, use the `ENABLED_MODULES` and the `DISABLED_SERVICES`  environment variables in the `customer.env` file to select which modules to install when deploying MetaDefender Storage Security, you can follow these steps:
>
> 1. Locate the `customer.env` file in your MetaDefender Storage Security deployment. This file contains environment variables used for customization.
> 2. Open the `customer.env` file in a text editor.
> 3. Add the `ENABLED_MODULES` environment variable to the file. The variable should be in the format `ENABLED_MODULES=<module_list>`, where `<module_list>` is a comma-separated list of the modules you want to enable. For example, if you want to enable modules Amazon S3, Google Cloud, and Azure Blob storage units, your `customer.env` file should include the following line: ENABLED_MODULES=azureblob,amazonsdk,googlecloud
> 4. Save the `customer.env` file.
> 5. Proceed with the deployment of MetaDefender Storage Security.
>
> Recommended Article: [How to Enable Specific Modules in the Configuration?](https://www.opswat.com/docs/mdss/knowledge-base/how-to-enable-specific-modules-in-the-configuration)

Please note that an online installation involves downloading the required `docker`  images from Docker Hub. If image pulls fail, you may have reached Docker Hub's [rate limits](https://docs.docker.com/docker-hub/usage/), especially when multiple services pull from the same IP address.

To address this, please consider one of the following solutions:

- Use `docker login` to increase your pull limit
- Implement image caching or registry proxies
- Stagger deployments to avoid concurrent pulls

## Advanced installation

We recommend that production deployments use an external database and ensure that web traffic is encrypted. For detailed information on how to configure an external database or HTTPS see advanced installation section:

- [Production Consideration Linux Deployments](https://www.opswat.com/docs/mdss/installation/linux-deployments)
- [Production Considerations Windows Deployments](https://www.opswat.com/docs/mdss/installation/windows-deployments)

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
sudo dpkg -i <name of the file>.deb
```

4. After the installation is completed, check if everything went fine

```bash
man mdss
```

or using the help menu

```bash
sudo mdss -h
```

5. Run the following command in order to initialize MetaDefender Storage Security

```bash
sudo mdss -u init
```

6. Start the service

```bash
sudo mdss -c start
```

7. Optionally, you can check the status using the following command:

```bash
sudo mdss -c status
```

8. Open a browser and navigate to the web interface [http://<server>](http://localhost:80)  to configure your deployment.

## Red Hat Enterprise Linux / CentOS / Rocky package (.rpm)

> **Info**
>
> Please note that Docker Engine is officially supported only on RHEL s390x architecture, but you may be able to install it manually following the CentOS installation steps: [https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)
>
> On Rocky Linux, it is recommended to use Podman , as Podman is officially supported by Red Hat.

> **Info**
>
> On RHEL 8, the default iptables FORWARD chain policy is set to DROP. Podman's CNI networking does not automatically add forwarding rules for external interface to bridge traffic, which will cause the web interface to be unreachable from outside the host even if the correct ports are open in the firewall or security group.

In case the FORWARD chain policy is set to DROP, here are the commands to switch it to ACCEPT:

```bash
# External → container (new connections)
iptables -I FORWARD -i eth0 -o cni-podman1 -j ACCEPT

# Container → external (return traffic for established connections)
iptables -I FORWARD -i cni-podman1 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
```

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
sudo man mdss
```

or using the help menu

```bash
sudo mdss -h
```

4. Run the following command in order to initialize MetaDefender Storage Security

```bash
sudo mdss -u init
```

*Note:* If you don’t have docker already installed, the installer will do that for you, but you will be prompted to sign out and sign back in. This is necessary because your current user needs to be added to the docker group.

5. Start the service

```bash
sudo mdss -c start
```

6. Optionally, you can check the status using the following command:

```bash
sudo mdss -c status
```

7. Open a browser and navigate to the web interface [http://<server>](http://localhost/)  to configure your deployment.
8. If you are using firewall (on CentOS8 and RHEL 8) you may need to update it’s policies:

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

## Podman Configuration

MDSS can also run using the Podman container engine instead of the default Docker one on RHEL operating systems. `Podman`, `podman-docker` and `docker-compose` need to be installed and running before installing MDSS.

```bash
# stop MDSS if is already installed
sudo mdss -c stop

# install podman, podman-docker and docker-compose
sudo yum install podman
sudo yum install podman-docker
sudo curl -SL https://github.com/docker/compose/releases/download/v2.15.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

sudo systemctl enable podman.socket
sudo systemctl start podman.socket

# to disable selinux permanetly 'SELINUX=disabled' needs to be set in the following config file
sudo vim /etc/selinux/config

# reboot machine for changes take effect
sudo reboot
```

Once the Podman and Docker components are installed, proceed with the installation of MetaDefender Storage Security (MDSS). You can skip the installation if MDSS is already installed.

After installation, MDSS must be configured to skip the default Docker engine checks. This is achieved by setting `SKIP_DOCKER_CHECKS=yes` in the `/etc/mdss/customer.env` configuration file.

```bash
# install additional MDSS dependencies (skip this if MDSS is already installed)
sudo subscription-manager repos --enable codeready-builder-for-rhel-8-$(arch)-rpms
sudo yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum install lvm2
sudo yum install wget

# install MDSS (skip this if MDSS is already installed)
sudo rpm -i mdss-x.x.x-1.noarch.rpm

# edit customer.env and add SKIP_DOCKER_CHECKS=yes
sudo vim /etc/mdss/customer.env

# start MDSS
sudo mdss -c start
```

## Configure Automatic Service Startup at Boot on RHEL and Rocky Linux with Podman

Due to a technical limitation, on **RHEL and Rocky Linux**, MDSS will not start automatically after machine restarts. To enable this option, please follow these steps:

1. Create a service file

```bash
sudo vi /etc/systemd/system/mdss.service
```

2. Paste the following content

```bash
[Unit]
    Description=MDSS Stack
    After=network-online.target
    Wants=network-online.target

    [Service]
    Type=oneshot
    RemainAfterExit=yes
    ExecStart=mdss -c start

    [Install]
    WantedBy=multi-user.target
```

3. Save and exit the file (Esc + :wq!)
4. Enable the service

```bash
sudo systemctl daemon-reload
sudo systemctl enable mdss.service
```

That's it. To confirm the changes were applied successfully, please restart your VM and then run **sudo mdss -c status** to make sure MDSS is up and running after reboot.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
