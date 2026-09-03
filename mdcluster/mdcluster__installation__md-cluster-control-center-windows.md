<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-control-center-windows -->

# Windows

### [Overview](/docs/mdcluster/installation/md-cluster-control-center-windows#overview)

This section describes how to install and configure **MetaDefender (MD) Cluster Control Center** on **Windows** systems. After installation, administrators can use MD Cluster Control Center to manage MD Cluster services from a centralized interface.

---

### [Prerequisites](/docs/mdcluster/installation/md-cluster-control-center-windows#prerequisites)

Before installing the MD Cluster Control Center service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Windows 11 23H2+, Windows Server 2019+. |
| Privileges | Administrator privileges |
| Installation package | `md-cluster-control-center-<version>-1-x64.msi` |
| Network access | Required port is open (default port: **8892**). |
| Dependencies | MD Cluster Identity Service and PostgreSQL must be installed and reachable from the Control Center host. |
| Hardware | 4vCPU and 4GB RAM |
| Disk space | A minimum of **100 GB of available disk space** is required. |

---

### [Create the ignition file](/docs/mdcluster/installation/md-cluster-control-center-windows#create-the-ignition-file)

Create an ignition file in YAML format. This file contains the credentials and connection settings required for the service.

The file must include the following keys:

| Key | Description |
| --- | --- |
| `identity.host` | IP address or domain name of the MD Cluster Identity Service host. **Do not** use `localhost` or `127.0.0.1`. |
| `identity.port` | Port used by MD Cluster Identity Service. |
| `identity.connection_key` | A **4-64 character alphanumeric string** (`a-z`, `A-Z`, `0-9`) that matches the Identity Service connection key. |
| `database.host` | IP address or domain name of the PostgreSQL server. |
| `database.port` | Port used by PostgreSQL. |
| `database.user` | PostgreSQL user. SUPERUSER privileges are required during the initial setup. |
| `database.password` | PostgreSQL user password. |
| `secure.encryption_key` | A **32-character** plain text key containing only lowercase letters and digits. |

Example ignition file:

YamlCopydatabase:
host: "your_postgres_host_ip"
port: 5432
user: "your_postgres_username"
password: "your_postgres_admin_password"
identity:
host: "your_md_cluster_identity_service_host_ip"
port: 8891
connection_key: "1234abcd"
secure:
encryption_key: "12345678123456781234567812345678" # [a-z0-9]{32}

Save the ignition file to the following path on the target machine:

PowershellCopyC:\opswat\md_cluster_control_center.ymlInfo

The ignition file contains sensitive credentials. This file can be safely deleted any time after the installation is complete.

---

### [Install the service](/docs/mdcluster/installation/md-cluster-control-center-windows#install-the-service)

1. Copy the installer file (`.msi`) to the target machine.
2. Open **PowerShell** with **Administrator privileges**.
3. Run the following command to start the installation in **silent mode**:

PowershellCopymsiexec.exe /i <md_cluster_control_center_package>.msi /qn

---

### [Verify the service status](/docs/mdcluster/installation/md-cluster-control-center-windows#verify-the-service-status)

1. Open **PowerShell** and run the following command:

PowershellCopyGet-Service -Name md-cluster-control-center

2. Check the **Running** status in the output.
3. If the service is not running, start it manually:

PowershellCopyStart-Service -Name md-cluster-control-center

---

### [Service management](/docs/mdcluster/installation/md-cluster-control-center-windows#service-management)

| Action | Command (PowerShell) |
| --- | --- |
| Check service status | `Get-Service -Name md-cluster-control-center` |
| Start service | `Start-Service -Name md-cluster-control-center` |
| Stop service | `Stop-Service -Name md-cluster-control-center` |
| Restart service | `Restart-Service -Name md-cluster-control-center` |

---

### [Customize the service configuration](/docs/mdcluster/installation/md-cluster-control-center-windows#customize-the-service-configuration)

During installation, MD Cluster Control Center generates a configuration file at:

C:\Program Files\OPSWAT\MetaDefender Cluster Control Center\md_cluster_control_center.yml

To customize the service behavior:

1. Open the configuration file in a text editor.
2. Modify the required settings according to your environment.
3. Save the changes.
4. Restart the service to apply the new settings.

PowershellCopyRestart-Service -Name md-cluster-control-center

---

### [Directory structure](/docs/mdcluster/installation/md-cluster-control-center-windows#directory-structure)

- `C:\opswat\md_cluster_control_center.yml`: Service ignition file.
- `C:\Program Files\OPSWAT\MetaDefender Cluster Control Center\md_cluster_control_center.yml`: Service configuration file.
- `C:\Program Files\OPSWAT\MetaDefender Cluster Control Center\data\log\control-center.log`: Service log file
- `C:\Program Files\OPSWAT\MetaDefender Cluster Control Center\data\log`: Default log directory.

---

### [Log files](/docs/mdcluster/installation/md-cluster-control-center-windows#log-files)

To check the service log, open the file `C:\Program Files\OPSWAT\MetaDefender Cluster Control Center\data\log\control-center.log`.

To check logs using Event Viewer:

1. Open **Event Viewer**.
2. Navigate to **Windows Logs > Application**.
3. Look for events related to **MD Cluster Control Center** service.

---

### [Uninstall the service](/docs/mdcluster/installation/md-cluster-control-center-windows#uninstall-the-service)

Open **PowerShell** and run the following command:

PowershellCopyUninstall-Package -Name 'MetaDefender Cluster Control Center' -Force

---

### [Troubleshooting](/docs/mdcluster/installation/md-cluster-control-center-windows#troubleshooting)

**A. Service does not start**

1. Check the service status:

PowershellCopyGet-Service -Name md-cluster-control-center

2. Review the application log and Event Viewer entries for Control Center errors.
3. Verify that the configuration file contains valid values, then restart the service.

**B. Installation fails**

Possible causes:

- Insufficient privileges.
- Missing prerequisites.
- The installer package does not match the target platform.

Solution:

- Ensure the installation command is executed with **Administrator** privileges.
- Confirm MD Cluster Identity Service and PostgreSQL are available.
- Re-download or verify the installer package if the MSI exits unexpectedly.

**C. Control Center cannot connect to Identity Service**

Possible causes:

- `identity.host` is incorrect.
- Network connectivity issues.
- Firewall restrictions.
- `identity.connection_key` does not match the value configured on MD Cluster Identity Service.

Solution:

- Verify `identity.host`, `identity.port`, and `identity.connection_key` in the ignition or configuration file.
- Ensure MD Cluster Identity Service is running and reachable from the MD Cluster Control Center host.
- Verify Windows Firewall rules allow traffic between the two services.
- Do not use `localhost` or `127.0.0.1` for `identity.host` unless both services run on the same host and the deployment explicitly supports it.

**D. Database connection fails**

Possible causes:

- PostgreSQL is not running.
- Database credentials are incorrect.
- PostgreSQL is not reachable from MD Cluster Control Center host.

Solution:

- Verify PostgreSQL service status.
- Confirm `database.host`, `database.port`, `database.user`, and `database.password` are correct.
- Ensure firewall rules allow access to PostgreSQL.

---

### [Ignition file key reference](/docs/mdcluster/installation/md-cluster-control-center-windows#ignition-file-key-reference)

- `identity.host` (**Required**)

  - Value type: string.
  - Description: IP address or domain name of the server hosting MD Cluster Identity Service. **Avoid** using `localhost` or `127.0.0.1`.
- `identity.port` (**Required**)

  - Value type: number.
  - Description: Port where MD Cluster Identity Service listens for client connections.
- `identity.connection_key` (**Required**)

  - Value type: string.
  - Description: A **4-64 character** string that contains only digits (**0-9**) and letters (**a-z, A-Z**). This value must match the connection key configured on MD Cluster Identity Service.
- `database.host` (**Required**)

  - Value type: string.
  - Description: IP address or domain name of the PostgreSQL server.
- `database.port` (**Required**)

  - Value type: number.
  - Description: Port where PostgreSQL listens for client connections.
- `database.user` (**Required**)

  - Value type: string.
  - Description: PostgreSQL user account. SUPERUSER privilege is required during the initial setup.
- `database.password` (**Required**)

  - Value type: string.
  - Description: PostgreSQL user password.
- `secure.encryption_key` (**Required**)

  - Value type: string.
  - Description: A 32-character plain text key composed only of lowercase letters (**0-9]** and digits (**0-9**).
- `rest.port` (Optional)

  - Value type: number.
  - Description: Port where MD Cluster Control Center listens for incoming connections. Default value is `8892`.
- `rest.log_path` (Optional)

  - Value type: string.
  - Description: Location where REST logs are written.
- `rest.log_level` (Optional)

  - Value type: string.
  - Description: Level of REST log messages (`dump`, `debug`, `info`, `warning`, or `error`).
- `log.streams[@].log_type` (Optional)

  - Value type: string.
  - Description: Type of log device (`file` or `syslog`).
- `log.streams[@].log_level` (Optional)

  - Value type: string.
  - Description: Level of log message (`dump`, `debug`, `info`, `warning`, or `error`).
- `log.streams[@].log_path` (Optional)

  - Value type: string.
  - Description: Location where logs are written. If `log.streams[@].log_type` is `"file"`, the value is a file path. If `log.streams[@].log_type` is `"syslog"`, the value can be `[tcp/udp]://host:port` for a remote syslog server or `"local"` for the local syslog server on supported platforms.
- `service` (optional)

  - Value type: object.
  - Description: Configures service connections that are automatically created the first time MD Cluster Control Center starts. This section can include one or more of the following service types: `cache`, `datalake`, `warehouse`, `file_storage`, and `broker`.
- `service.cache` (optional) — Redis cache service

  - Value type: object.
  - Description: Defines one or more Redis cache service connections.
  - `service.cache.connections[@].display_name` (Required)

    - Value type: string.
    - Description: The display name of the connection. The value must not be empty.
  - `service.cache.connections[@].host` (Required)

    - Value type: string.
    - Description: The hostname or IP address of the Redis server.
  - `service.cache.connections[@].port` (Required)

    - Value type: number.
    - Description: The port used by the Redis server. A valid value ranges from **1** to **65535**.
  - `service.cache.connections[@].user` (optional)

    - Value type: string.
    - Description: The Redis username.
  - `service.cache.connections[@].password` (optional)

    - Value type: string.
    - Description: The Redis password.
  - `service.cache.connections[@].secure` (optional)

    - Value type: boolean.
    - Description: Enables a TLS connection to the Redis server. Defaults to false. When enabled, port must be the Redis TLS port.
  - `service.cache.connections[@].ssl_verify` (optional)

    - Value type: boolean.
    - Description: Verifies the Redis server's certificate. Defaults to true. Only applies when secure is enabled.
  - `service.cache.connections[@].ca_cert` (optional)

    - Value type: string.
    - Description: The path to the CA certificate file, read on the Control Center host. If empty, the system trust store is used.
- `service.datalake` (optional)

  - Value type: object.
  - Description: Defines one or more PostgreSQL Data Lake service connections.
  - `service.datalake.connections[@].display_name` (Required)

    - Value type: string.
    - Description: The display name of the connection. The value must not be empty.
  - `service.datalake.connections[@].host` (Required)

    - Value type: string.
    - Description: The hostname or IP address of the PostgreSQL server.
  - `service.datalake.connections[@].port` (Required)

    - Value type: number.
    - Description: The port used by the PostgreSQL server. A valid value ranges from **1** to **65535**.
  - `service.datalake.connections[@].user` (Required)

    - Value type: string.
    - Description: The PostgreSQL username.
  - `service.datalake.connections[@].password` (Required)

    - Value type: string.
    - Description: The password for the PostgreSQL user.
- `service.warehouse` (optional) — PostgreSQL warehouse service

  - Value type: object.
  - Description: Defines one or more PostgreSQL Warehouse service connections.
  - `service.warehouse.connections[@].display_name` (Required)

    - Value type: string.
    - Description: The display name of the connection. The value must not be empty.
  - `service.warehouse.connections[@].host` (Required)

    - Value type: string.
    - Description: The hostname or IP address of the PostgreSQL server.
  - `service.warehouse.connections[@].port` (Required)

    - Value type: number.
    - Description: The port used by the PostgreSQL server. A valid value ranges from **1** to **65535**.
  - `service.warehouse.connections[@].user` (Required)

    - Value type: string.
    - Description: The PostgreSQL username.
  - `service.warehouse.connections[@].password` (Required)

    - Value type: string.
    - Description: The password for the PostgreSQL user.
- `service.file_storage` (optional)

  - Value type: object.
  - Description: Defines one or more File Storage service connections.
  - `service.file_storage.connections[@].display_name` (Required)

    - Value type: string.
    - Description: The display name of the connection. The value must not be empty.
  - `service.file_storage.connections[@].host` (Required)

    - Value type: string.
    - Description: The hostname or IP address of the File Storage server.
  - `service.file_storage.connections[@].port` (Required)

    - Value type: number.
    - Description: The port used by the File Storage server. A valid value ranges from **1** to **65535**.
  - `service.file_storage.connections[@].connection_key` (Required)

    - Value type: string.
    - Description: The connection key used to authenticate with the File Storage service.
- `service.broker` (optional)

  - Value type: object.
  - Description: Defines one or more RabbitMQ broker service connections.
  - `service.broker.connections[@].display_name` (Required)

    - Value type: string.
    - Description: The display name of the connection. The value must not be empty.
  - `service.broker.connections[@].host` (Required)

    - Value type: string.
    - Description: The hostname or IP address of the RabbitMQ server.
  - `service.broker.connections[@].port` (Required)

    - Value type: number.
    - Description: The port used by the RabbitMQ server. A valid value ranges from **1** to **65535**.
  - `service.broker.connections[@].user` (Required)

    - Value type: string.
    - Description: The RabbitMQ username.
  - `service.broker.connections[@].password` (Required)

    - Value type: string.
    - Description: The password for the RabbitMQ user.
  - `service.broker.connections[@].secure` (Optional)

    - Value type: boolean.
    - Description: Enables a TLS connection to the RabbitMQ server. Defaults to false. When enabled, port must be the broker's TLS port.
  - `service.broker.connections[@].ssl_verify` (Optional)

    - Value type: boolean.
    - Description: Verifies the RabbitMQ server's certificate. Defaults to true. Only applies when secure is enabled.
  - `service.broker.connections[@].ca_cert` (Optional)

    - Value type: string.
    - Description: The path to the CA certificate file, read on the Control Center host. If empty, the system trust store is used.
- `access.allowed_directories` (optional)

  - Value type: array of strings.
  - Description: Specifies up to **16** local directories from which MD Cluster Control Center is permitted to read certificate files. Only files located in the configured directories or their subdirectories are allowed. Each directory must exist when MD Cluster Control Center starts. If any configured directory is invalid or cannot be resolved, MD Cluster Control Center fails to start.
