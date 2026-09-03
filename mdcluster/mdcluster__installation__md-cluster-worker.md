<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-worker -->

# MD Cluster Worker

### [Supported Operating Systems](/docs/mdcluster/installation/md-cluster-worker#supported-operating-systems)

| OS | Version |
| --- | --- |
| Windows | Windows 11 23H2+, Windows Server 2019+. |
| Ubuntu | Ubuntu 22.04+, Ubuntu 24.04+, Debian 12+, Rocky 9+, or RHEL 9+. |

---

### [Overview](/docs/mdcluster/installation/md-cluster-worker#overview)

This section describes how to install a **MD Cluster Worker** on a target machine by retrieving and executing an installation script from **MD Cluster Control Center**. After installation, administrators can monitor the health status of the installed worker.

---

### [Prerequisites](/docs/mdcluster/installation/md-cluster-worker#prerequisites)

| Requirement | Description |
| --- | --- |
| Privileges | **Administrator** privileges on Windows; **Root** or **sudo** access on Linux |
| Network | MD Cluster Worker must be able to communicate with MD Cluster Control Center |
| Port | Default port 8893 must be open for MD Cluster Control Center to reach |
| Dependencies | Meet [System requirements](/docs/mdcluster/installation/md-cluster-system-requirements) |

---

### [Allow Cross IP Sessions](/docs/mdcluster/installation/md-cluster-worker#allow-cross-ip-sessions)

1. Sign in to MD Cluster **Control Center** console using your administrator account.
2. From the sidebar, go to `Settings` > `Security`.
3. Toggle `Allow Cross IP Sessions`.

---

### [Retrieve the installation script](/docs/mdcluster/installation/md-cluster-worker#retrieve-the-installation-script)

1. From the sidebar, go to to `Inventory` > `Workers`.
2. Expand `Add Workers` and select `Add by script`.

3. In Worker Installation, choose the appropriate platform (Windows or Linux).
4. Enter the connection key provided by your administrator and leave the other settings as default.

Warning

Avoid using **loopback** addresses (such as localhost, 127.0.0.1, or ::1) when generating the installation script.

5. Click `Generate`.
6. Copy the generated script.

---

### [Execute the installation script](/docs/mdcluster/installation/md-cluster-worker#execute-the-installation-script)

1. Access the target machine.
2. Run the copied command:

   - On Windows: open PowerShell as Administrator, paste and run the script.
   - On Linux: open a root shell (e.g., sudo su), paste and run the script.
3. Once the installation completes, note the Worker ID displayed on the screen.

BashCopy...
[INFO] Worker registered successfully with Control Center. Worker ID: 3bfee38481ff482d8fa1b893afe79d77

---

### [Verify the installation](/docs/mdcluster/installation/md-cluster-worker#verify-the-installation)

1. Sign in to MD Cluster **Control Center** console.
2. From the sidebar, go to `Inventory` > `Workers`.
3. Confirm that the worker with the previously collected Worker ID appears with the correct version and platform.

---

### [Service management](/docs/mdcluster/installation/md-cluster-worker#service-management)

- Stop the service:

BashCopy# PowerShell on Windows
> Stop-Service md-cluster-worker
# Terminal on Linux
$ sudo systemctl --machine=md-cluster-worker@.host --user status md-cluster-worker

- Start the service:

BashCopy# PowerShell on Windows
> Start-Service md-cluster-worker
# Terminal on Linux
$ sudo systemctl --machine=md-cluster-worker@.host --user start md-cluster-worker

- Restart the service:

BashCopy# PowerShell on Windows
> Restart-Service md-cluster-worker
# Terminal on Linux
$ sudo systemctl --machine=md-cluster-worker@.host --user restart md-cluster-worker

---

### [Customize the service configuration](/docs/mdcluster/installation/md-cluster-worker#customize-the-service-configuration)

During installation, MD Cluster Worker service generates a configuration file at

- Windows: `<installation_dir>\MetaDefender Cluster Worker\md_cluster_worker.yml`
- Linux: `<installation_dir>/data/config/md_cluster_worker.yml`

To customize the service behavior:

1. Open the configuration file in a text editor.
2. Modify the required settings according to your environment.
3. Save the changes.
4. Restart the service to apply the new settings.

BashCopy# PowerShell on Windows
> Restart-Service md-cluster-worker
# Terminal on Linux
$ sudo systemctl --machine=md-cluster-worker@.host --user restart md-cluster-worker

---

### [Uninstall the service](/docs/mdcluster/installation/md-cluster-worker#uninstall-the-service)

1. Navigate to MD Cluster Worker installation directory.
2. Open PowerShell (Admin) on Windows or a sudo terminal on Linux.
3. Run command:

BashCopy# PowerShell on Windows
> & '<path_to_worker_installed>\bin\uninstall.ps1'
# Terminal on Linux
$ sudo <path_to_worker_installed>/bin/uninstall.sh

---

### [Troubleshooting](/docs/mdcluster/installation/md-cluster-worker#troubleshooting)

**CURL error 403 during installation**

Possible causes:

1. The session has expired.
2. The user does not have deployment permission.

Solutions:

1. Regenerate the installation script and run it again.
2. Use an account with the required permissions or provide an API key with deployment access.

---

### [Configuration reference](/docs/mdcluster/installation/md-cluster-worker#configuration-reference)

**Common configurations**

- `Platform` (Required)

  - Value: Windows or Linux
  - Description: The platform where the installation script will be run.
- `Connection Key` (Required)

  - Value: String
  - Description: A **4-64 character** string that contains only digits (`0-9`) and letters (`a-z`, `A-Z`) provided by system administrator.
- `Listen Host` (Optional)

  - Value: String
  - Description: The host/interface the MD Cluster Worker listens on. Default is 0.0.0.0 (all IPv4).
- `Listen Port` (Optional)

  - Value: Number
  - Description: The port number where MD Cluster Worker listens for requests. Default is 8893.

**Advanced configurations**

- `Worker added automatically during installation` (Optional)

  - Value: String
  - Description: The worker host is automatically detected from the IP address used to connect to MD Cluster Control Center. To register the worker with a DNS or domain name instead, specify the hostname here.
- `Skip SSL verification when connecting to Control Center` (Optional)

  - Value: Yes or No
  - Description: Use this option only for testing or when using self-signed certificates. For production, use a CA-signed certificate and keep SSL verification enabled.
- `Install Directory` (Optional)

  - Value: a valid directory path.
  - Description: Specifies the location where MD Cluster Worker will be installed. The default is `C:\Program Files\OPSWAT\MetaDefender Cluster Worker` on Windows and `/opt/md-cluster-worker/` on Linux.
- `API Key` (Optional)

  - Value: String
  - Description: Use an **API Key instead of** `Allow Cross IP Sessions` for authentication during installation. This is the recommended alternative when you don’t want to enable Allow Cross IP Sessions.
- `Skip dependency installation` (Optional, Linux only] :

  - Value: Yes or No
  - Description: Skip installing dependencies on Linux (e.g. when they are pre‑installed or managed by your OS image).
