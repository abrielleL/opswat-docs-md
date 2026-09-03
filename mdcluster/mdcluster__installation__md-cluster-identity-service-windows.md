<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-identity-service-windows -->

# Windows

### [Overview](/docs/mdcluster/installation/md-cluster-identity-service-windows#overview)

This section describes how to install and configure **MetaDefender (MD) Cluster Identity Service** on **Windows** system. After installation, MD Cluster Control Center can connect to MD Cluster Identity and monitor its system health.

---

### [Prerequisites](/docs/mdcluster/installation/md-cluster-identity-service-windows#prerequisites)

Before installing the MD Cluster Identity Service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Windows 11 23H2+, or Windows Server 2019+. |
| Privileges | Administrator privileges |
| Installation package | `md-cluster-identity-service-<version>-1-x64.msi` |
| Network access | Required port is open (default port: **8891**).  A minimum network bandwidth of **1 Gbps** is required. |
| Hardware | 4vCPU and 4GB RAM |
| Disk space | A minimum of **50 GB of available disk space** is required. |

---

### [Create the ignition file](/docs/mdcluster/installation/md-cluster-identity-service-windows#create-the-ignition-file)

Create an ignition file in YAML format. This file contains the credentials required for the service to connect to the system.

The file must include the following keys:

| Key | Description |
| --- | --- |
| `database.host` | IP address or domain name of the server hosting PostgreSQL. |
| `database.port` | IP address or domain name of the server hosting PostgreSQL. |
| `database.user` | PostgreSQL server user. SUPERUSER privileges are required to set up the database and extensions during the initial configuration. |
| `database.password` | PostgreSQL user password. |
| `secure.connection_key` | A **4–64 character alphanumeric string** (a–z, A–Z, 0–9) used by MD Cluster Control Center to connect to the server. |
| `secure.private_key` | The content of private key in X509 format. |
| `secure.certificate` | The content of certificate in X509 format. |

Example ignition file:

YamlCopydatabase:
host: "posgresql_host"
port: 5432
user: "postgres"
password: "admin"
secure:
connection_key: "1234abcd" # [0-9a-zA-Z]{4,64}
private_key: |
-----BEGIN PRIVATE KEY-----
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
fBrpEY1IATtPq1taBZZogRqI3rOkkPk=
-----END PRIVATE KEY-----
certificate: |
-----BEGIN CERTIFICATE-----
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
e2Hl/7M0c/lbZ4FvXgARlex2rkgS0Ka06HE=
-----END CERTIFICATE-----

Save the ignition file to the following path on the target machine:

BashCopyC:\opswat\md_cluster_identity_service.ymlInfo

The ignition file contains sensitive credentials. This file can be safely deleted any time after the installation is complete.

---

### [Install the service](/docs/mdcluster/installation/md-cluster-identity-service-windows#install-the-service)

1. Copy the installer file (`.msi` ) to the target machine.
2. Open **PowerShell** with **Administrator privileges**.
3. Run the following command to start the installation in **silent mode**:

PowershellCopymsiexec.exe /i <md_cluster_identity_service_package>.msi /qn

---

### [Verify the service status](/docs/mdcluster/installation/md-cluster-identity-service-windows#verify-the-service-status)

1. Open **PowerShell** and run the following command:

PowershellCopyGet-Service -Name md-cluster-identity-service

2. Check the **Running** Status in the output.
3. If the service is not running, start it manually:

PowershellCopyStart-Service -Name md-cluster-identity-service

---

### [Service management](/docs/mdcluster/installation/md-cluster-identity-service-windows#service-management)

| Action | Command (PowerShell) |
| --- | --- |
| Check service status | `Get-Service -Name md-cluster-identity-service` |
| Start service | `Start-Service -Name md-cluster-identity-service` |
| Stop service | `Stop-Service -Name md-cluster-identity-service` |
| Restart service | `Restart-Service -Name md-cluster-identity-service` |

---

### [Customize the service configuration](/docs/mdcluster/installation/md-cluster-identity-service-windows#customize-the-service-configuration)

During installation, MD Cluster Identity Service generates a configuration file at:

C:\Program Files\OPSWAT\MetaDefender Cluster Identity Service\md_cluster_identity_service.yml

To customize the service behavior:

1. Open the configuration file in a text editor.
2. Modify the required settings according to your environment.
3. Save the changes.
4. Restart the service to apply the new settings.

PowershellCopyRestart-Service -Name md-cluster-identity-service

---

### [Directory structure](/docs/mdcluster/installation/md-cluster-identity-service-windows#directory-structure)

- `C:\opswat\md_cluster_file_storage.yml`: Service Ignition file.
- `C:\Program Files\OPSWAT\MetaDefender Cluster Identity Service\md_cluster_file_storage.yml`: Service configuration file.
- `C:\Program Files\OPSWAT\MetaDefender Cluster Identity Service\data\log\identity-service.log` : Service log file.
- `C:\Program Files\OPSWAT\MetaDefender Cluster Identity Service\data\storage`: Default storage directory.
- `C:\Program Files\OPSWAT\MetaDefender Cluster Identity Service\data\log` Default log directory.

---

### [Log files](/docs/mdcluster/installation/md-cluster-identity-service-windows#log-files)

To check the service log, open the file `C:\Program Files\OPSWAT\MetaDefender Cluster Identity Service\data\log\identity-service.log`.

To check logs using Event Viewer:

1. Open **Event Viewer**.
2. Navigate to **Windows Logs > Application**.
3. Look for events related to **MD Cluster Identiy** **Service.**

---

### [Uninstall the service](/docs/mdcluster/installation/md-cluster-identity-service-windows#uninstall-the-service)

Open **PowerShell** and run the following command:

PowershellCopyUninstall-Package -Name 'MetaDefender Cluster Identity Service' -Force

---

### [Troubleshooting](/docs/mdcluster/installation/md-cluster-identity-service-windows#troubleshooting)

**A. Service is not running**

1. Check the service status

PowershellCopyGet-Service -Name md-cluster-identity-service

2. Start the service if it is not running:

PowershellCopyStart-Service -Name md-cluster-identity-service

**B. Installation fails**

Possible causes

- Insufficient privileges.
- Missing dependencies.

Solution

- Ensure the installation command is executed with **Administrator** privileges.
- Ensure dependencies are installed.

**C. MD Cluster Control Center cannot connect to MD Cluster Identity Service.**

Possible causes

- Network connectivity issues.
- Firewall restrictions.

Solution

- Ensure MD Cluster Control Center has network connectivity to MD Cluster Identity Service.
- Verify that firewall rules allow **inbound** and **outbound** connections.

---

### [Ignition file key reference](/docs/mdcluster/installation/md-cluster-identity-service-windows#ignition-file-key-reference)

- `secure.connection_key` (**Required**)

  - Value type: string.
  - Description: Use a **4–64 character string** that contains only numbers (0–9) and letters (a–z, A–Z). This string is used by clients to connect to the server. Set this value as the `identity.connection_key` in the MD Cluster Control Center configuration file.
- `secure.private_key` (**Required**)

  - Value type: string.
  - Description: The content of private key in X509 format.
- `secure.certificate` (**Required**)

  - Value type: string.
  - Description: The content of certificate in X509 format.
- `database.host` (**Required**)

  - Value type: string.
  - Description: IP address or domain name of the server hosting PostgreSQL.
- `database.port` (**Required**)

  - Value type: string.
  - Description: Port where the PostgreSQL server listens for client connections.
- `database.user` (**Required**)

  - Value type: string.
  - Description: PostgreSQL server user. SUPERUSER privileges are required to set up the database and extensions during the initial configuration.
- `database.password` (**Required**)

  - Value type: string.
  - Description: PostgreSQL user password.
- `rest.host` [optional)

  - Value type: string.
  - Description: IP address (V4/V6) or host where the server resides on. Default value is **'*'***.* Notes: `'*'` allows the service to accept connections from all network interfaces. To bind the service to a specific interface, specify its IP address or domain name. For example, to listen on all IPv4 interfaces, set the host to `0.0.0.0`.
- `rest.port` [optional)

  - Value type: number.
  - Description: The port where the server resides on. Default value is `8891`.
- `log.streams[@].log_type` [optional)

  - Value type: string.
  - Description: Type of log device (`file`, or `syslog`)
- `log.streams[@].log_level` [optional)

  - Value type: string.
  - Description: Level of log message (`dump`, `debug`, `info`, `warning`, or `error`).
- `log.streams[@].log_path` [optional)

  - Value type: string.
  - Description: Location where logs are written. If `log.streams[@].log_type` is `"file"` then `log.streams[@].log_path` is the path to a file on file system where logs are written. If `log.streams[@].log_type` is `"syslog"` then

    - `log.streams[@].log_path` can be `[tcp/udp]://host:port` where host:port is the host and port to a remote syslog server that supports TCP or UDP protocol.
    - `log.streams[@].log_path` can be `"local"` to write log to local syslog server (Linux only).
- `user.name` [optional)

  - Value type: string.
  - Description: Username for the initial administrator account.
- `user.password` [optional)

  - Value type: string.
  - Description: Password for the initial administrator account.
- `user.email` [optional)

  - Value type: string.
  - Description: Email address for the initial administrator account.
- `user.apikey` [optional)

  - Value type: string.
  - Description: API key for the initial administrator account.
