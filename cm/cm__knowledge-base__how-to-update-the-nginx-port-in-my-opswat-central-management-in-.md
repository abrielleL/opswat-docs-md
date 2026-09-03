<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-update-the-nginx-port-in-my-opswat-central-management-in- -->

# How to update the NGINX port in My OPSWAT Central Management in Linux?

## Overview

This article explains how to change the web management interface port (nginx port) used by My OPSWAT Central Management (OCM v10) on Linux systems.
By default, the NGINX web interface listens on port 9000.

> > For a full list of ports used by OPSWAT Central Management, refer to the official documentation:
> > [Ports used by My OPSWAT Central Management](https://www.opswat.com/docs/cm/deployment/system-requirements#networking-and-port-requirements)

## Prerequisites

- Access to the Linux system running OPSWAT Central Management (RHEL or Ubuntu)
- Sudo or root privileges

## Steps to update the Web Management Interface Port on Red Hat Enterprise Linux/Ubuntu

1. Stop OPSWAT Central Management and NGINX Services

Before changing the port, stop the relevant services to avoid conflicts:

```bash
systemctl stop mocm-all.target
systemctl stop mocm-nginx # for RPM package
systemctl stop nginx # for OVA appliance
```

2. Edit the Port Configuration File

Open the configuration file `/etc/opt/mocm/port-config.properties` in a text editor:

Locate the line NGINX_PORT=9000 and change it to your desired port (8018), for example:

```bash
NGINX_PORT=8018
```

Save and exit the file.

3. Apply the Port Change

Run the following script to apply the new NGINX port configuration:

```bash
/opt/mocm/lib/nginx-port-change.sh
```

Output: Setting nginx port to [new port]

4. Restart OPSWAT Central Management and NGINX

After applying the changes, restart the services:

```bash
systemctl restart mocm-all.target
systemctl restart mocm-nginx # for RPM package
systemctl restart nginx # for OVA appliance
```

> Warning: After changing the web management console port, you will also need to update the Server URL setting to reflect the new address.

> Support:
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
