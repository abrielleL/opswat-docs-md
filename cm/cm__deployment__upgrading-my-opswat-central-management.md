<!-- source: https://www.opswat.com/docs/cm/deployment/upgrading-my-opswat-central-management -->

# Upgrading My OPSWAT Central Management

> **Info**
>
> If you installed My OPSWAT Central Management version 10.2.2509 or earlier, use Option 1. If you installed version 10.2.2510 or later, use Option 2.

### Option 1: Upgrade to version 10.2.2510

To upgrade to a newer version of My OPSWAT Central Management, please first [Uninstall My OPSWAT Central Management](https://www.opswat.com/docs/cm/deployment/uninstall-my-opswat-central-management). Then, follow the steps in the appropriate installation guide to reinstall the product using the new package.

- **Windows Installation Guide:** [MSI Installation - Standalone mode](https://www.opswat.com/docs/cm/deployment/msi-installation)
- **Linux[Red Hat Enterprise Linux] Installation Guide:**  [RPM Installation](https://www.opswat.com/docs/cm/deployment/rpm-installation)

**Note:** All existing My OPSWAT Central Management configuration and data will be kept during this process.

> **Info**
>
> Uninstalling My OPSWAT Central Management will not cause any data or settings loss including files, configuration, and license. If you want to perform a clean uninstall and reinstall, please refer to [Clean uninstall of OPSWAT Central Management.](https://www.opswat.com/docs/cm/deployment/uninstall-my-opswat-central-management)

### Option 2: Upgrade to version 10.3.2511 or later

#### Windows

If you are installing version 10.2.2510 or later, My OPSWAT Central Management supports in-place upgrades. You do not need to uninstall the previous version before installing the new one:

• Download the latest My OPSWAT Central Management installer.

• Run the installer on the system where the current version is installed.

• Follow the on-screen instructions to complete the upgrade.

• Verify that all services are running correctly.

#### **Linux[Red Hat Enterprise Linux]**

My OPSWAT Central Management [RPM] supports in-place upgrades. You do not need to uninstall the previous version before installing the new one:

• Download the latest My OPSWAT Central Management installer.

• Run the installer on the system where the current version is installed.

```bash
# Upgrade MOCM installation
sudo dnf install MyOPSWATCentralManagement-10.x.x.x.rpm
# Reload the system daemon configuration
sudo systemctl daemon-reload
# Stop all supporting components to ensure that they are started with the latest configuration as part of mocm
sudo systemctl stop redis nginx rabbitmq-server
# Start all OCM services
sudo systemctl start mocm-all.target
# Check the overall OCM target status
sudo systemctl status mocm-all.target
# List the status of all individual OCM services
sudo systemctl list-units mocm-*
```

• Once all services are up and running, you can access the mocm setup page via your web browser:

- **URL:** `<server_ip>:9000/loading`

*(Replace <server_ip> with the actual IP address of your mocm server.)*
