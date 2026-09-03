<!-- source: https://www.opswat.com/docs/cm/deployment/rpm-installation-for-bundled-dependencies -->

# RPM Installation for Bundled Dependencies

Before starting My OPSWAT Central Management On-premises installation, please make sure your server meets the [System Requirements](https://www.opswat.com/docs/cm/deployment/system-requirements)

1/ Open the terminal

2/ For air gap system, install dependencies for Linux[Red Hat Enterprise Linux] at  [Software Requirement](https://www.opswat.com/docs/cm/deployment/system-requirements#linuxred-hat-enterprise-linux)

Note that if a valid upstream repository is available, these dependencies will be automatically installed with the main package.

3/  Install the main RPM file:

Use the `dnf` package manager to install the main OCM file:

```bash
sudo dnf install MyOPSWATCentralManagement-10.x.x.x.rpm
```

[Replace `10.x.x.x` with your specific version number.)

4/ Start mocm services

```bash
# Reload the system daemon configuration
sudo systemctl daemon-reload
# Start all OCM services
sudo systemctl start mocm-all.target
```

5/ Check mocm services' status

After starting, verify the status to ensure all mocm components are running correctly:

```bash
# Check the overall OCM target status
sudo systemctl status mocm-all.target

# List the status of all individual OCM services
sudo systemctl list-units mocm-*
```

6/  Enable Auto-Start on Boot

```bash
sudo systemctl enable mocm-all.target
```

7/ Access the User Interface

Once all services are up and running, you can access the mocm setup page via your web browser:

- **URL:** `<server_ip>:9000/loading`

*(Replace <server_ip> with the actual IP address of your mocm server.)*

```bash
ifconfig
```

> **Info SELinux Settings**
>
> Please note that the following SELinux settings are automatically added during installation:
>
> - semanage port -a -t redis_port_t -p tcp **30000**
> - setsebool -P httpd_can_network_connect **1**
> - setsebool -P nis_enabled 1
