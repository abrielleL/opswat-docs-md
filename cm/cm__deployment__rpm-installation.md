<!-- source: https://www.opswat.com/docs/cm/deployment/rpm-installation -->

# RPM Installation

Before starting My OPSWAT Central Management On-premises installation, please make sure your server meets the [System Requirements](https://www.opswat.com/docs/cm/deployment/system-requirements)

1/ Open the terminal

2/ Install dependency for Linux[Red Hat Enterprise Linux] at  [Software Requirement](https://www.opswat.com/docs/cm/deployment/system-requirements#linuxred-hat-enterprise-linux)

3/ RabbitMQ Cleanup (First-Time Installation Only)

Suppose this is the **first time installing mocm** on this system, and the **RabbitMQ server** was previously started with its default configuration (not the mocm-specific configuration). In that case, you need to remove its persistent database to prevent configuration conflicts:

```bash
# 1. Stop the RabbitMQ service
sudo systemctl stop rabbitmq-server

# 2. Remove the old RabbitMQ persistent database
sudo rm -rf /var/lib/rabbitmq/mnesia/rabbit@localhost/
```

4/  Install the main RPM file:

Use the `dnf` package manager to install the main OCM file:

```bash
sudo dnf install MyOPSWATCentralManagement-10.x.x.x.rpm
```

[Replace `10.x.x.x` with your specific version number.)

5/ Start mocm services

```bash
# Reload the system daemon configuration
sudo systemctl daemon-reload
# Stop all supporting components to ensure that they are started with the latest configuration as part of mocm
sudo systemctl stop redis nginx rabbitmq-server
# Start all OCM services
sudo systemctl start mocm-all.target
```

6/ Check mocm services' status

After starting, verify the status to ensure all mocm components are running correctly:

```bash
# Check the overall OCM target status
sudo systemctl status mocm-all.target

# List the status of all individual OCM services
sudo systemctl list-units mocm-*
```

7/  Enable Auto-Start on Boot

```bash
sudo systemctl enable mocm-all.target
```

8/ Access the User Interface

Once all services are up and running, you can access the mocm setup page via your web browser:

- **URL:** `<server_ip>:9000/loading`

*(Replace **<server_ip>** with the actual IP address of your mocm server.)*

```bash
ifconfig
```

> **Info SELinux Settings**
>
> Please note that the following SELinux settings are automatically added during installation:
>
> - semanage port -a -t redis_port_t -p tcp **30000**
> - setsebool -P httpd_can_network_connect **1**
