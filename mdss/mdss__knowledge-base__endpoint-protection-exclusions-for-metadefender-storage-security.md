<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/endpoint-protection-exclusions-for-metadefender-storage-security -->

# Endpoint Protection Exclusions for MetaDefender Storage Security running on Windows

> **Applies to:** MetaDefender Storage Security (MDSS) **4.6.x or later**, Windows Basic Deployment, and the OPSWAT ONTAP Connector. Linux and Kubernetes deployments are out of scope.

This article lists what to exclude from an endpoint protection product (antivirus, EDR, XDR, application control) on the Windows machines that run MDSS, and why. It is vendor neutral: each item names the protection category it applies to; map that category to the matching module in your product.

MDSS is itself a file security product. It reads files that may be malicious, deletes and moves files on storage in bulk, and runs a supervised tree of processes and PowerShell scripts. An endpoint agent is built to stop exactly these behaviours. Without exclusions it slows MDSS down, breaks scans and remediations, and in the worst case deletes customer files from the protected storage before MDSS acts on them.

**Section 3** is the recommended rule set: a few generic rules that cover everything MDSS does. **Appendix A** is the full inventory behind those rules, for products without wildcard or parent-process features, or for policies that require every exclusion to be enumerated.

---

## 1. Symptoms of interference

| Symptom | Usual cause |
| ---- | ---- |
| Restarting MDSS takes 5 to 15 minutes. `data\webclient\startup-log.txt` shows minutes spent in "Loading CA certificates", "Refreshing environment and nginx configuration" or "Applying HTTP/HTTPS configuration". | The agent inspects every PowerShell process the MDSS service starts (script control, .NET instrumentation, application control). |
| `powershell.exe -NoProfile -File .\mdss.ps1 -c load-ca` takes more than 10 seconds (healthy: 1 to 3). | Same as above. If the exclusions do not fix it, Windows is waiting on blocked revocation checks for the signed scripts; see [Slow 'mdss.ps1' commands on Windows](https://www.opswat.com/docs/mdss/4.6.1/knowledge-base/slow--mdss-ps1--commands-on-windows). |
| The `mdss` service or one of its child processes is terminated, or the console stays on "Initializing". | Behavioural, anti-ransomware or child-process protection blocks a process in the MDSS tree. |
| Alerts about a service starting `powershell.exe -ExecutionPolicy Bypass`, `sc.exe`, `icacls.exe`, `msiexec.exe`, `psql.exe` or `nginx.exe`, or about a new root certificate, firewall rule, scheduled task or changed machine environment variables. | The `mdss` service supervising its process tree, and its start-up scripts. Expected behaviour. |

---

## 2. Principles

- **Exclude by full path, not by file name.** Every MDSS process lives under the installation folder or is a private copy of a runtime under it. Excluding the MDSS `dotnet.exe` by path does not exclude other .NET applications on the host.
- **Use folder and process exclusions together.** A folder exclusion protects the files MDSS *owns*. A process exclusion protects what MDSS *does*, and most of that happens outside the installation folder: reading files on shares, writing temp copies, bulk deletes and moves, spawning PowerShell from `C:\Windows`.
- **Trust the process tree.** "A process and its descendants" for the `mdss` service is the single most effective rule in this document. If your product lacks it, exclude each executable in A.3.
- **Prefer process exclusions over disabling a module**, and use the OPSWAT, Inc. code signature where the product allows it (A.7).
- **Do not copy this list to the MetaDefender Core host.** MD Core has its own requirements.

---

## 3. Recommended exclusion rules

`<INSTALL_DIR>` is the installation folder, by default `C:\Program Files\OPSWAT\MetaDefender Storage Security`. The installer lets the customer choose another drive or folder; the real path is in the registry value `InstallDir` under `HKLM\SOFTWARE\OPSWAT\MetaDefender Storage Security`.

### 3.1 Folders

Exclude from on-access (real-time) scanning, scheduled scanning and behavioural file monitoring:

1. **<INSTALL_DIR>\**, the whole tree (A.1).
2. **C:\ProgramData\OPSWAT\**: upgrade state files and, under `mdss\smb-mounts`, one directory symbolic link per mounted SMB share pointing at `\\server\share`. **Critical:** anything the agent does under `smb-mounts` happens on the customer's storage. Scanning there scans the whole share through the MDSS server; quarantining there deletes the customer's file. The location is set by `SMBSERVICE_MOUNT_DIRECTORY`; exclude the configured value if it was changed.
3. **C:\ProgramData\OPSWAT-ONTAP-Connector\**, plus the folder named by `LogPath` in its `config.ini` if one is set, when the ONTAP Connector runs on this host (section 4).
4. **The temp folder of the account the mdss service runs as**: `C:\Windows\Temp` (or `C:\Windows\SystemTemp` on current Windows Server builds) for `LocalSystem`, `C:\Users\<account>\AppData\Local\Temp` for a custom account. MDSS writes temporary copies of the files it uploads during remediation there. They can be the original, possibly malicious, file a workflow is moving to quarantine; if the agent removes them the remediation fails. If this is too broad for your policy, the process rules in 3.2 give the same result.

### 3.2 Processes

Exclude from on-access scanning, network file scanning, behavioural analysis, anti-ransomware, exploit and memory protection, and .NET or process instrumentation (CLR profilers, startup hooks, `APPDOMAIN_MANAGER_*` injection):

1. **<INSTALL_DIR>\services\opswat.mdss.windows.service\opswat.mdss.windows.service.exe and all its descendants.** This is the `mdss` Windows service. It starts and supervises every other MDSS process: the private .NET runtime (`services\dotnet\dotnet.exe`, 12 or more instances hosting the microservices), nginx, the Garnet cache, the SMB sidecar, and every `powershell.exe`, `sc.exe`, `icacls.exe`, `psql.exe`, `nginx.exe`, `node.exe` and `msiexec.exe` it launches at start-up.
2. **Any executable under <INSTALL_DIR>\services\** (`<INSTALL_DIR>\services\**\*.exe`). Covers the two components that run as their own Windows services rather than under the supervisor (PostgreSQL as `mdss_postgresql`, RabbitMQ and Erlang as `mdss_rabbitmq`) and the tools administrators run by hand (`pg_dump.exe`, `opswat.mdss.reencryption.cli.exe`).
3. **C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe**, when installed on this host.

Rule 1 also covers the SMB sidecar reading customer files through `smb-mounts` and the remediation temp copies. Every service is a .NET 10 application that compiles code at run time, so memory scanning and instrumentation add latency to each process, and the supervisor restarts any child that exits (it polls every 10 seconds), so a blocked process becomes a restart loop. Executables, signers and ports: A.3 and A.4.

### 3.3 Scripts

Under script control, PowerShell protection and .NET Framework instrumentation, allow every `.ps1` file in `<INSTALL_DIR>\scripts\`, and the `powershell.exe` that runs it, when started by the `mdss` service (rule 3.2.1), by `msiexec.exe` during install, upgrade or uninstall, or by an administrator from an elevated prompt. They are Windows PowerShell 5.1 scripts signed by OPSWAT, Inc. and launched with `-ExecutionPolicy Bypass … -File`, so key the rule on publisher or path, not on the execution policy. The installer additionally runs inline PowerShell commands (`powershell.exe -Command`), VBScript custom actions inside `msiexec.exe` (the UAC relaunch, WMI queries of ports, processes and services) and `cmd.exe /c net stop … sc delete …`. A.5 lists what each script does.

### 3.4 Services, scheduled task, firewall rules and registry

Allow the installer and the processes in 3.2 to create, change and delete:

- Windows services `mdss`, `mdss_postgresql`, `mdss_rabbitmq`, legacy `mdss_mongodb`, and `opswat-ontap-connector`.
- The scheduled task `MDSS_InstallSharePointComponents` (SharePoint On-Premises module only).
- Windows Firewall inbound rules whose display name starts with `MetaDefender Storage Security:`.
- Registry keys under `HKLM\SOFTWARE\OPSWAT`, `HKLM\SOFTWARE\Ericsson\Erlang\ErlSrv`, `HKLM\SYSTEM\CurrentControlSet\Services\mdss*` and `…\Services\opswat-ontap-connector`, the machine environment key `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment`, the machine Trusted Root and Personal certificate stores, and (ONTAP Connector only) `HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs`.

Details: A.2 and A.6.

### 3.5 Network

- **Inbound:** 80 and 443 (`WEB_PORT`, `WEB_PORT_SSL`): console, REST API, storage webhooks and ONTAP Connector traffic, all through nginx.
- **Loopback:** all MDSS components talk to each other on 127.0.0.1. Do not filter loopback traffic for the processes in 3.2 (ports in A.4).
- **Outbound:**
  - Scan engines: MetaDefender Core (HTTP or HTTPS, default port 8008); `api.metadefender.com:443` when MetaDefender Cloud is used.
  - OPSWAT: `activation.dl.opswat.com:443` for license activation and, only when `ENABLE_TELEMETRY=yes`, for telemetry (OTLP over HTTPS). The previous telemetry endpoint `mdss-telemetry.metadefender.com:4317` is used only when configured explicitly.
  - Protected storages: SMB 445; NFS 2049 and 111; SFTP 22; FTP 21 plus passive ports; 443 to the cloud storage endpoints (Amazon S3, Azure, Google Cloud, Alibaba, Oracle, Box, Microsoft Graph, SharePoint).
  - Customer infrastructure: domain controllers or LDAP servers (389, 636, 3268, 3269), the SMTP server, webhook targets, and an external PostgreSQL or RabbitMQ when configured.

### 3.6 Behaviours to recognise

These are normal for MDSS. Excluding the processes in 3.2 from the behavioural, anti-ransomware and child-process modules handles all of them; the list helps the security team recognise the alerts.

1. **Bulk file operations on network shares.** Remediation workflows delete, move, copy, rename and overwrite many files per minute, which triggers mass-delete, mass-rename, canary-file and "encryption-like write" heuristics.
2. **Reading, and temporarily copying, malicious files** before they are sent to MetaDefender Core or moved to quarantine.
3. **Symbolic links to UNC paths.** The SMB sidecar maps shares with `WNetAddConnection2` and creates directory symbolic links under `smb-mounts` with `CreateSymbolicLink`, on demand, removing them after 300 seconds idle. Agents that follow reparse points scan, and may quarantine on, the customer's storage.
4. **A service spawning PowerShell and management tools.** At every start the `mdss` service runs `powershell.exe -ExecutionPolicy Bypass`, which spawns more PowerShell, `sc.exe`, `icacls.exe`, `nginx.exe`, `psql.exe`, `node.exe` and `msiexec.exe`, registers services and changes their logon account.
5. **Start-up and installer changes to the machine.** Every start imports CA certificates into the Trusted Root store, rewrites about 300 machine environment variables and broadcasts `WM_SETTINGCHANGE`. The installer relaunches itself elevated through UAC, queries WMI, adds firewall rules and a scheduled task, and writes state files to `C:\ProgramData\OPSWAT`. A support package runs `systeminfo`, `route print` and `ipconfig /all` and creates large archives under `<INSTALL_DIR>`.

### 3.7 Application control (allow-listing)

1. Publisher rule for **OPSWAT, Inc.**: all MDSS executables, libraries and PowerShell scripts, and the ONTAP Connector.
2. Publisher rule for **Microsoft Corporation**: the private .NET runtime, Garnet, PowerShell, `msiexec.exe`, `sc.exe`, `icacls.exe`.
3. Path rule for everything under **<INSTALL_DIR>\**, including SQL and JavaScript files. Covers the third-party runtimes (PostgreSQL, Erlang, RabbitMQ, Python, Node.js, MongoDB) whatever their signer, and `nginx.exe`, which is not signed by OPSWAT in 4.6.x. The folder is writable only by administrators, which is what makes a path rule acceptable.

If policy requires publisher rules for every file, enumerate the signers with the command in A.7 and add hash rules for the unsigned files it reports. The `mdss` service performs its own integrity check: it refuses to start an MDSS binary that is not signed by OPSWAT, or a runtime executable (`dotnet.exe`, `GarnetServer.exe`, `python.exe`) that carries no signature. Do not let the agent modify, wrap or re-sign these files.

---

## 4. OPSWAT ONTAP Connector (NetApp ONTAP)

A separate Windows service, usually on its own host next to the NetApp Antivirus Connector (`ontapavc`). Installed to `C:\ProgramData\OPSWAT-ONTAP-Connector\` by MDSS or manually; the MDSS installer updates and removes it together with MDSS.

- **Service:** `opswat-ontap-connector`, executable `OPSWAT-ONTAP-Connector.exe`, signed by OPSWAT.
- **Files:** `config.ini` (rewritten through `config.ini.tmp` whenever the set of protected storages changes), `data.json`, `logs\YYYYMMDD.log` and `YYYYMMDD_HHMMSS.log` (or the configured `LogPath`). On uninstall, `config.ini` is backed up to `C:\ProgramData\OPSWAT\ontap-connector-config.ini.bak`.
- **Named pipes:** `\pipe\ntapvsrq` (scan requests from the NetApp AV Connector) and `\pipe\ntapvscp` (registration and verdicts), RPC over `ncacn_np` to 127.0.0.1.
- **Registry:** writes and deletes `data-lif::<host>` values under `HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs`, creating the key if it is missing. Since 4.6.0 this runs automatically every 15 seconds (`StorageSyncIntervalInSeconds`), not only at installation.
- **Network:** HTTP or HTTPS to the MDSS web port (80 or 443) for `/api/webhook/realtime`, `/api/file/*`, `/api/health` and `/api/account` (polled every 15 seconds). SMB 445 to the ONTAP shares.
- **Behaviour:** reads every file a user opens or modifies on the protected shares through `\\?\UNC\…` paths and posts it to MDSS. These files may be malicious. Optionally writes the `Zone.Identifier` alternate data stream (`ZoneIdentifierFiles`).

Exclude the folder, the process and its UNC file reads from on-access scanning. An agent that scans the network files this process opens scans, and may quarantine on, the ONTAP volume before MDSS returns a verdict, and it doubles the latency of every file open for every ONTAP user.

---

## 5. What to keep enabled

- Everything outside the paths and processes above. MDSS does not need the agent disabled.
- On-access scanning of files that administrators copy onto the server themselves, and network protection for destinations not listed in 3.5.
- Audit-only logging of the behaviours in 3.6, if the security team wants visibility. Only blocking and quarantine actions need to be excluded.

---

## 6. Verification

1. PowerShell start-up time, as administrator. Expect well under one second for the first command and one to three seconds for the second.

   ```powershell
   Measure-Command { powershell.exe -NoProfile -NonInteractive -Command exit }
   cd "<INSTALL_DIR>\scripts"
   Measure-Command { powershell.exe -NoProfile -File .\mdss.ps1 -c load-ca }
   ```
2. Restart MDSS, read the step timings and confirm every process and service is up. Every step except database migrations should finish within seconds; a healthy restart takes two to four minutes.

   ```powershell
   .\mdss.ps1 -c restart
   Get-Content "<INSTALL_DIR>\data\webclient\startup-log.txt"
   .\mdss.ps1 -c status
   Get-Service mdss, mdss_postgresql, mdss_rabbitmq
   ```
3. Check the agent console for detections referencing the paths in 3.1, the processes in 3.2 or the behaviours in 3.6. Any remaining detection means an exclusion is missing, or is by file name where a full path is required.
4. Scan a storage that holds a known-safe test file and, if remediation is used, run a workflow that moves a file to quarantine. Confirm in the MDSS audit log that both complete, and on the storage that nothing other than MDSS removed a file.

---

## Appendix A. Detailed inventory

Use this appendix when your product has no wildcard or parent-process trust feature, or when policy requires each exclusion to be enumerated.

### A.1 Installation folder layout

| Folder | Contents |
| ---- | ---- |
| `services\` | One folder per microservice (its `.dll` files and a `logs\` folder), the private .NET runtime (`dotnet`), Garnet (`garnet`), nginx (`opswat.mdcs.webclient`), PostgreSQL (`postgres`), RabbitMQ (`rabbitmq`), Erlang (`erlang`), the SMB sidecar (`opswat.mdss.smb.service`), the service host (`opswat.mdss.windows.service`), legacy Python (`python`) and MongoDB (`mongo`). The Scanning service keeps its storage providers in a `providers` subfolder. Hundreds of files load at every start; logs are written continuously. |
| `data\` | PostgreSQL data, the RabbitMQ message store, the web client files and start-up log (`data\webclient`), legacy MongoDB data. Rewritten constantly; scanning causes latency and lock conflicts. |
| `logs\` | PostgreSQL, RabbitMQ, migration and installation logs. |
| `config\` | `.env`, `customer.env`, nginx configuration and TLS certificates (`config\nginx\certificates`), RabbitMQ, PostgreSQL and cache configuration. Rewritten at every start. |
| `scripts\` | The PowerShell scripts in A.5. |
| `dependencies\` | Compressed runtimes extracted during install and upgrade. |
| `Utils\` | SQL migration scripts and installer prerequisites (SharePoint client components MSI, Visual C++ runtime). |
| `ca_certificates\` | Customer CA certificates imported into the Windows trust store at every start. |
| `tmp\`, `<INSTALL_DIR>\*.zip` | Working folder and output of the support package, log, settings and database exports; staging folder for ONTAP Connector updates. |

Outside the installation folder: `C:\ProgramData\OPSWAT\` (`mdss_upgrade_customer.env` and `mdss_upgrade_service_account.txt` during upgrades, `ontap-connector-config.ini.bak`, `mdss\smb-mounts\`), `C:\ProgramData\OPSWAT-ONTAP-Connector\`, the service account's temp folder (3.1), and `%TEMP%\MetaDefenderStorageSecurity-Setup-<timestamp>.log` of the administrator who ran the installer.

### A.2 Windows services, scheduled task and firewall rules

| Item | Executable or definition | Notes |
| ---- | ---- | ---- |
| Service `mdss` | `<INSTALL_DIR>\services\opswat.mdss.windows.service\opswat.mdss.windows.service.exe` | The supervisor. `LocalSystem` by default; a custom domain or gMSA account is preserved across upgrades. |
| Service `mdss_postgresql` | `<INSTALL_DIR>\services\postgres\bin\pg_ctl.exe`, runs `postgres.exe` | Registered with `pg_ctl register`, reconfigured with `sc.exe config` and `sc.exe failure`. |
| Service `mdss_rabbitmq` | `<INSTALL_DIR>\services\erlang\erts-*\bin\erlsrv.exe`, runs `erl.exe` | Registered with `rabbitmq-service.bat install`; writes `HKLM\SOFTWARE\Ericsson\Erlang\ErlSrv\1.1\MDSS_RabbitMQ`. |
| Service `mdss_mongodb` | `<INSTALL_DIR>\services\mongo\mongod.exe` | Legacy. Only on systems upgraded from MDSS 3.x; stopped after the migration to PostgreSQL. |
| Service `opswat-ontap-connector` | `C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe` | NetApp ONTAP integration only. |
| Scheduled task `MDSS_InstallSharePointComponents` | `powershell.exe -ExecutionPolicy Bypass -WindowStyle Hidden -NoProfile -File "<INSTALL_DIR>\scripts\install-sharepoint-components.ps1"`, at system start-up as `SYSTEM` | SharePoint On-Premises module only. |
| Firewall rules `MetaDefender Storage Security: Allow inbound traffic <NAME> - <PORT>` | Inbound TCP | Licensing port, NFS sidecar port, the five SMB sidecar ports. |

### A.3 Executables

`services.exe` starts `opswat.mdss.windows.service.exe`, which starts `powershell.exe` for the start-up orchestration; that starts more `powershell.exe` instances, `nginx.exe -s reload`, `psql.exe`, `node.exe` and `msiexec.exe`. After orchestration the service starts and keeps alive every process below, restarting any that exits.

| Executable (under `<INSTALL_DIR>\services\` unless stated) | Signer | Role and ports |
| ---- | ---- | ---- |
| `opswat.mdss.windows.service\opswat.mdss.windows.service.exe` | OPSWAT | The `mdss` service. Single-file .NET application that loads its assemblies from its own image (some agents flag this as in-memory loading); validates the signature of every MDSS binary before starting it. |
| `dotnet\dotnet.exe` | Microsoft | Private .NET 10 runtime: one instance per service in A.4, plus one per scanning instance (`WINDOWS_SCANNING_SERVICE_INSTANCES`, 1 to 30). Exclude by this exact path only. |
| `opswat.mdss.smb.service\opswat.mdss.smb.service.exe` | OPSWAT | SMB sidecar: authenticates to shares, creates the `smb-mounts` links, reads and writes files on the shares. 127.0.0.1:6002 (gRPC), 7002 (health). |
| `opswat.mdcs.webclient\nginx.exe` | not OPSWAT | Console web server and API reverse proxy, one master and one worker. Ports 80 and 443. |
| `garnet\GarnetServer.exe` | Microsoft | Redis-compatible cache. 127.0.0.1:6379. |
| `postgres\bin\postgres.exe`, `pg_ctl.exe`, `psql.exe`, `pg_dump.exe`, `pg_restore.exe`, `pg_isready.exe`, `initdb.exe` | PostgreSQL build vendor | Database and tools; one backend process per connection. 127.0.0.1:5432. |
| `erlang\erts-*\bin\erlsrv.exe`, `erl.exe`, `epmd.exe`, `inet_gethost.exe`; `rabbitmq\sbin\rabbitmq-service.bat`, `rabbitmqctl.bat` | Erlang / RabbitMQ vendors, may be unsigned | Message broker. 127.0.0.1:5672, 15672, 25672, 4369. |
| `opswat.mdss.reencryption.cli\opswat.mdss.reencryption.cli.exe` | OPSWAT | Re-encrypts stored credentials; run by administrators. |
| `python\python.exe` | Python Software Foundation | Legacy SMB sidecar (`server.py`, five processes on 6002 to 6006 and 7002 to 7006), only when `USE_OPSWAT_SMB_SERVICE=false`. |
| `mongo\mongod.exe`, `mongosh.exe`; `opswat.mdcs.mongomigrations\node.exe` | MongoDB Inc., Node.js | Legacy database and migration tooling, only on systems upgraded from MDSS 3.x. |
| `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe` | Microsoft | Runs the scripts in A.5 and the installer's inline commands, with `-ExecutionPolicy Bypass`. |
| `C:\Windows\System32\msiexec.exe`, `sc.exe`, `icacls.exe`, `cmd.exe`, `net.exe`, `systeminfo.exe`, `route.exe`, `ipconfig.exe` | Microsoft | Installer and scripts: SharePoint client components MSI, service configuration and cleanup, permissions on `customer.env`, host information for the support package. |
| `C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe` | OPSWAT | Section 4. |

### A.4 Microservices hosted by `dotnet.exe`, and loopback ports

If your product filters on the command line rather than the process path, allow `dotnet.exe` when its argument is one of these files (paths under `<INSTALL_DIR>\services\`; each service runs with its own folder as the working directory). Ports are bound to 127.0.0.1 unless the customer changed the listening IP.

| Service | Command-line argument | Loopback port |
| ---- | ---- | ---- |
| Licensing | `opswat.mdcs.license.service\opswat.mdcs.license.service.dll` | 5001 (gRPC) |
| API Gateway | `opswat.mdcs.api.gateway\opswat.mdcs.api.gateway.dll` | 8005, 8006 |
| Identity | `opswat.mdss.identity.service\opswat.mdss.identity.service.dll` | 7001 |
| Logging | `opswat.mdcs.logging.service\opswat.mdcs.logging.service.dll` | – |
| Job Dispatcher | `opswat.mdcs.job.dispatcher\opswat.mdcs.job.dispatcher.dll` | – |
| Notification | `opswat.mdcs.notification.service\opswat.mdcs.notification.service.dll` | – |
| Scanning (1 to 30 instances) | `opswat.mdcs.scanning.service\opswat.mdcs.scanning.service.dll` | – |
| Discovery | `opswat.mdss.discovery.service\opswat.mdss.discovery.service.dll` | – |
| Remediations | `opswat.mdss.remediations.service\opswat.mdss.remediations.service.dll` | – |
| Storages | `opswat.mdss.storages.service\opswat.mdss.storages.service.dll` | – |
| Workflow Manager | `opswat.mdss.workflowmanager.service\opswat.mdss.workflowmanager.service.dll` | – |
| NFS sidecar (NFS module only) | `opswat.mdss.nfs.service\opswat.mdss.nfs.service.dll` | 5004 |

Other loopback ports: 6002 and 7002 SMB sidecar (legacy Python sidecar: 6002 to 6006 and 7002 to 7006); 5432 PostgreSQL; 5672, 15672, 25672 and 4369 RabbitMQ, its management interface, Erlang distribution and port mapper; 6379 Garnet cache; 27017 and 27778 legacy MongoDB and its migration tool.

All storage providers (Amazon S3, Azure, Google Cloud, Alibaba, Oracle, Box, Microsoft Graph, SharePoint, SFTP, FTP, SMB and NFS) are libraries loaded in-process by the Discovery, Storages, Remediations and Scanning services; there are no per-provider processes. The Scanning service verifies the Authenticode signature of its providers with Windows before loading them. An agent that blocks or delays library loading, or that strips or alters signatures, prevents these services from starting.

### A.5 PowerShell scripts

All scripts live in `<INSTALL_DIR>\scripts\`, are signed by OPSWAT, Inc., and run on Windows PowerShell 5.1 (.NET Framework). Agents that hook the .NET Framework through the `APPDOMAIN_MANAGER_ASM` and `APPDOMAIN_MANAGER_TYPE` machine environment variables inspect every one of these processes and can add minutes to each.

| Script | Started by | Purpose |
| ---- | ---- | ---- |
| `startup-orchestration.ps1` | The `mdss` service, at every start | Clears the RabbitMQ queue store, imports CA certificates, refreshes configuration and the web client `env-config.js`, applies HTTP or HTTPS, syncs the environment variables to Machine scope, reloads nginx, installs SharePoint components, runs database migrations. |
| `mdss.ps1` | The orchestration (`-c load-ca`, `-u enable_https`, `-u disable_https`) and administrators (`-c start/stop/restart/status`, `-u support_package`, `-u export_db`, others) | `load-ca` writes each certificate to a temp `.crt` file and imports it into `Cert:\LocalMachine\Root`; `support_package` runs `systeminfo`, `route print` and `ipconfig /all` and compresses logs; `export_db` runs `pg_dump.exe`. |
| `init.ps1` | The installer; the orchestration (`-setenv`) | Writes machine environment variables, broadcasts `WM_SETTINGCHANGE`, checks ports, creates firewall rules and the SharePoint scheduled task; `-uninstall` reverses it. |
| `dependencies.ps1` | The installer; the orchestration (`-refresh`) | Extracts and registers PostgreSQL, RabbitMQ, Erlang, nginx, Garnet, .NET, Python and MongoDB (`sc.exe`, `pg_ctl.exe`, `rabbitmq-service.bat`, `mongod.exe --install`); regenerates nginx and PostgreSQL configuration; updates or removes the ONTAP Connector. |
| `migrations_postgres.ps1`, `migrations.ps1`, `migrations_mongo_to_postgres.ps1` | The orchestration | Database migrations with `psql.exe` and, on upgraded systems, `node.exe`. |
| `install-sharepoint-components.ps1` | The orchestration; the scheduled task | Runs `msiexec.exe` to install the SharePoint client components MSI. |
| `mdss-service-logon.ps1`, `write-customer-env.ps1`, `InstallationStatus.ps1`, `monitor-installation.ps1`, `mdss-resp-client.ps1` | The installer; the other scripts | Restore the service logon account after an upgrade (`sc.exe config`, `icacls`), write `customer.env`, report installer progress, talk to the Garnet cache. |

### A.6 Registry keys

- `HKLM\SOFTWARE\OPSWAT\MetaDefender Storage Security`: `InstallDir` and installation state, written by the installer and read back on upgrade.
- `HKLM\SYSTEM\CurrentControlSet\Services\mdss`, `mdss_postgresql`, `mdss_rabbitmq`, `mdss_mongodb`, `opswat-ontap-connector`: service definitions, recovery options and logon account, written by the installer and the scripts.
- `HKLM\SOFTWARE\Ericsson\Erlang\ErlSrv\1.1\MDSS_RabbitMQ`: written by the RabbitMQ service registration.
- `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment`: about 300 MDSS machine environment variables (ports, connection strings, feature flags, `DOTNET_ROOT`, `ERLANG_HOME`, `RABBITMQ_*`), rewritten at every service start.
- `HKLM\SOFTWARE\Microsoft\SystemCertificates\ROOT\Certificates`: customer CA certificates imported by `mdss.ps1 -c load-ca`. `enable_https` also uses the machine Personal (`My`) store temporarily.
- `HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs`: one `data-lif::<host>` value per protected NetApp SVM, maintained automatically by the ONTAP Connector.

### A.7 Code signers

- **OPSWAT, Inc.:** `opswat.mdss.windows.service.exe`, `opswat.mdss.smb.service.exe`, `opswat.mdss.reencryption.cli.exe`, `OPSWAT-ONTAP-Connector.exe`, every `opswat.*.dll`, every `.ps1` in `<INSTALL_DIR>\scripts\`, and the installer itself.
- **Microsoft Corporation:** `dotnet.exe` and the .NET runtime libraries under `services\dotnet`, `GarnetServer.exe`, `powershell.exe`, `msiexec.exe`, `sc.exe`, `icacls.exe`.
- **Third-party runtime vendors** (PostgreSQL build vendor, Erlang/OTP, RabbitMQ, Python Software Foundation, Node.js, MongoDB Inc.): the corresponding runtimes under `services\`.
- **Not signed by OPSWAT:** `services\opswat.mdcs.webclient\nginx.exe`, and possibly some third-party runtime files. Use path or hash rules for these.

Enumerate the real signers on the installed system before writing publisher rules, because third-party runtime versions change between MDSS releases:

```powershell
Get-ChildItem "<INSTALL_DIR>\services" -Recurse -Include *.exe,*.dll |
  Get-AuthenticodeSignature |
  Group-Object { if ($_.SignerCertificate) { $_.SignerCertificate.Subject } else { "UNSIGNED" } } |
  Select-Object Count, Name | Sort-Object Count -Descending
```

Application control must also allow the PowerShell scripts in `<INSTALL_DIR>\scripts\` and the SQL and JavaScript files in `<INSTALL_DIR>\Utils\` and `<INSTALL_DIR>\services\opswat.mdcs.mongomigrations\`.

---

## Appendix B. Changes since the 4.5.x article

If you applied the 4.5.x version of this list, update these items:

- **SFTP sidecar removed.** `opswat.mdss.sftp.service`, its loopback port 5003 and its firewall rule no longer exist. SFTP, FTP and all cloud providers run in-process inside the Discovery, Storages, Remediations and Scanning services.
- **Telemetry endpoint.** Telemetry goes to `activation.dl.opswat.com:443` by default; `mdss-telemetry.metadefender.com:4317` is used only when configured explicitly.
- **Installer behaviour.** The installer relaunches itself elevated through UAC, checks ports through WMI, runs inline PowerShell commands, and keeps upgrade state in `C:\ProgramData\OPSWAT` instead of `%APPDATA%\OPSWAT\MetaDefender Storage Security\backup\`. It also updates and uninstalls the ONTAP Connector.
- **ONTAP Connector synchronisation.** The connector polls `/api/account` every 15 seconds and rewrites `config.ini` and the `data-lif` registry values on its own. Its log folder is configurable (`LogPath`).
- **Signed scripts.** The PowerShell scripts carry an OPSWAT, Inc. Authenticode signature, so publisher-based script rules are possible. Blocked revocation checks for that signature are a separate cause of slow start-up (section 1).
- **Environment variables.** The machine environment holds about 300 MDSS variables, up from about 200.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
