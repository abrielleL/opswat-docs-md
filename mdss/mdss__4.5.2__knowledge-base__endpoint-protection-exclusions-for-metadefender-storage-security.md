<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/endpoint-protection-exclusions-for-metadefender-storage-security -->

# Endpoint Protection Exclusions for MetaDefender Storage Security on Windows

This article lists what to exclude from an endpoint protection product (antivirus, EDR, XDR, application control) on the Windows machines that run MDSS, and why. It is vendor neutral: each item names the protection category it applies to, and you map that category to the equivalent module in your product.

MDSS is itself a file security product. It deliberately reads files that may be malicious, moves and deletes files on storage in bulk, and runs a supervised tree of processes and maintenance scripts. Each of these behaviours is something an endpoint agent is built to stop. Without exclusions the agent slows MDSS down, breaks scans and remediations, and in the worst case deletes customer files from the protected storage before MDSS can act on them.

The document has two levels. **Section 3** is the recommended rule set: a small number of generic rules that cover everything MDSS does. **Appendix A** is the complete inventory of paths, executables, scripts, services, registry keys and ports behind those rules, for security teams whose product has no wildcard or parent-process features, or whose policy requires exclusions to be enumerated one by one.

---

## 1. Symptoms of interference

Check for these before and after applying the exclusions.

| Symptom | Usual cause |
| ---- | ---- |
| Restarting MDSS on Windows takes 5 to 15 minutes. The startup log (`data\webclient\startup-log.txt`) shows two or more minutes for "Loading CA certificates", "Refreshing environment and nginx configuration" or "Applying HTTP/HTTPS configuration". | The agent inspects every PowerShell process the MDSS service launches (script control, .NET runtime instrumentation, application control). |
| `Measure-Command { powershell.exe -NoProfile -File .\mdss.ps1 -c load-ca }` takes more than 10 seconds. | Same as above. On a healthy server it completes in one to three seconds. |
| The MDSS Windows service or one of its child processes is terminated, or the web page stays on "Initializing". | Behavioural, anti-ransomware or child-process protection blocks a process in the MDSS tree. |
| Alerts about PowerShell started with `-ExecutionPolicy Bypass` by a service, or about a service process spawning `powershell.exe`, `sc.exe`, `msiexec.exe`, `psql.exe` or `nginx.exe`. | The MDSS Windows service supervising its process tree. This is expected behaviour. |
| Alerts about a new root certificate, new firewall rule, new scheduled task or changed machine environment variables. | MDSS startup and installation scripts. This is expected behaviour. |

---

## 2. Principles

- **Exclude by full path, not by file name.** Every MDSS process either lives under the installation folder or is a well-known third party runtime that MDSS ships as a private copy under that folder. The `dotnet.exe` MDSS uses is its own copy, so excluding that exact path does not exclude other .NET applications on the host.
- **A folder exclusion and a process exclusion protect different things. You need both.** A folder exclusion stops the agent from scanning the files MDSS *owns*: its libraries, logs and databases. A process exclusion stops the agent from inspecting what a process *does*, and nearly everything MDSS does happens outside the installation folder: reading customer files on shares, writing temporary copies to the temp folder, deleting and moving files in bulk, spawning PowerShell from `C:\Windows`, and compiling code in memory. Behavioural, anti-ransomware, child-process and runtime-instrumentation modules act on the process regardless of the folder it started from.
- **Prefer process exclusions over disabling a module.** Exclude the MDSS processes from on-access scanning, script control and behavioural analysis. Keep the modules enabled for everything else on the server.
- **Cover the whole process tree.** The MDSS service starts children, and those start children. Most products let you trust "a process and its descendants". Use that; it is the single most effective rule in this document. If your product cannot, exclude each executable in Appendix A.3.
- **Use the code signature where the product allows it.** OPSWAT signs every MDSS executable and library. Third party runtimes carry their own vendor signature or, for a few, no signature. Appendix A.9 explains how to enumerate the signers on the installed system.
- **Generic rules are broader than an enumerated list.** Trusting a process and its descendants trusts anything the MDSS service spawns, and a path rule trusts anything an administrator places in the folder. This is acceptable because the installation folder and the service account are already under administrator control. If your policy does not accept it, apply Appendix A instead of section 3.
- **Do not exclude the MetaDefender Core host by copying this list.** MD Core has its own requirements. This document covers only the machines running MDSS and the ONTAP Connector.
- **Verify.** Section 6 gives measurable checks.

---

## 3. Recommended exclusion rules

Everything below is relative to the installation folder, written here as `<INSTALL_DIR>`. The default is:

```plaintext
C:\Program Files\OPSWAT\MetaDefender Storage Security
```

The installer lets the customer pick another drive or folder, so always confirm the real path. It is stored in the registry value `InstallDir` under `HKLM\SOFTWARE\OPSWAT\MetaDefender Storage Security`.

### 3.1 Folders

Exclude from on-access (real-time) scanning, scheduled scanning and behavioural file monitoring:

1. `<INSTALL_DIR>\` (the whole tree). Binaries, configuration, databases, message store, logs, scripts and the support package working folder. Appendix A.1 describes each subfolder.
2. `C:\ProgramData\OPSWAT\`. Contains the upgrade state file and, in its `mdss\smb-mounts` subfolder, one directory symbolic link per protected SMB share pointing at `\\server\share`. **Critical:** anything the agent does under `smb-mounts` happens on the customer's storage. Scanning there scans the whole share through the MDSS server, and quarantining there deletes the customer's file. The location is configurable through `SMBSERVICE_MOUNT_DIRECTORY`; exclude the configured value if it was changed.
3. `C:\ProgramData\OPSWAT-ONTAP-Connector\`, when the ONTAP Connector is installed on this host (section 4).
4. The temp folder of the account the `mdss` service runs as. MDSS writes temporary copies of files being uploaded during remediation, and of some downloads, there. These copies can be the original, possibly malicious, file that a workflow is moving to quarantine; if the agent removes them the remediation fails. For `LocalSystem` this is `C:\Windows\Temp` (or `C:\Windows\SystemTemp` on recent Windows Server builds). For a custom service account it is `C:\Users\<account>\AppData\Local\Temp`. If a temp exclusion is too broad for your policy, the process rules in 3.2 achieve the same result.
5. `%APPDATA%\OPSWAT\MetaDefender Storage Security\backup\` of the account that runs the installer. Used only during upgrades to back up and restore `customer.env`, the nginx and RabbitMQ configuration and the TLS certificate files.

### 3.2 Processes

Exclude from on-access scanning, network file scanning, behavioural analysis, anti-ransomware, exploit and memory protection, and .NET or process instrumentation (CLR profilers, startup hooks, `APPDOMAIN_MANAGER_*` injection):

1. **<INSTALL_DIR>\services\opswat.mdss.windows.service\opswat.mdss.windows.service.exe and all its descendants.** This is the `mdss` Windows service. It starts and supervises every other MDSS process, so trusting its descendants covers the private .NET runtime (`services\dotnet\dotnet.exe`, 12 to 40 instances hosting the microservices), nginx, the Garnet cache, the SMB sidecar, and every `powershell.exe`, `sc.exe`, `icacls.exe`, `psql.exe`, `nginx.exe`, `node.exe` and `msiexec.exe` it launches at start-up.
2. **Any executable under <INSTALL_DIR>\services\** (wildcard `<INSTALL_DIR>\services\**\*.exe`). This catches the two components that are not descendants of the supervisor because they run as their own Windows services (PostgreSQL under `mdss_postgresql`, RabbitMQ and Erlang under `mdss_rabbitmq`), plus tools an administrator runs by hand (`pg_dump.exe`, `opswat.mdss.reencryption.cli.exe`).
3. **C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe**, when installed on this host.

Rule 1 also covers the SMB sidecar reading customer files through `C:\ProgramData\OPSWAT\mdss\smb-mounts` and the remediation temp copies from 3.1, so the "scan network files" and temp folder concerns are closed from the process side as well. The per-executable inventory, signers and listening ports are in Appendix A.3 and A.4.

### 3.3 Scripts

Under script control / PowerShell protection, allow any `.ps1` file under `<INSTALL_DIR>\scripts\` when it is started by the `mdss` service (rule 3.2.1), by `msiexec.exe` during install or upgrade, or by an administrator from an elevated prompt. They are Windows PowerShell 5.1 scripts launched with `-ExecutionPolicy Bypass -NoProfile -NonInteractive -File`, so do not rely on script signing or execution policy. Appendix A.5 describes what each script does, which is useful when explaining an alert.

### 3.4 Services, scheduled task, firewall rules and registry

Allow the installer and the processes in 3.2 to create, change and delete:

- Windows services whose name starts with `mdss` (`mdss`, `mdss_postgresql`, `mdss_rabbitmq`, legacy `mdss_mongodb`) and `opswat-ontap-connector`.
- The scheduled task `MDSS_InstallSharePointComponents` (SharePoint On-Premises module only).
- Windows Firewall inbound rules whose display name starts with `MetaDefender Storage Security:`.
- Registry keys under `HKLM\SOFTWARE\OPSWAT`, `HKLM\SOFTWARE\Ericsson\Erlang\ErlSrv`, `HKLM\SYSTEM\CurrentControlSet\Services\mdss*`, the machine environment key `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment`, the machine Trusted Root certificate store, and (ONTAP Connector only) `HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs`.

Details are in Appendix A.2 and A.6.

### 3.5 Network

- **Inbound**: 80 and 443 (configurable through `WEB_PORT`, `WEB_PORT_SSL`). MDSS console, REST API, storage webhooks and ONTAP Connector traffic, all through nginx.
- **Loopback**: every MDSS component talks to the others on 127.0.0.1. Do not filter loopback traffic for the processes in 3.2. The port list is in Appendix A.7.
- **Outbound**, grouped by purpose:
  - Scan engines: MetaDefender Core instances (HTTP or HTTPS, default port 8008) and `api.metadefender.com:443` when MetaDefender Cloud is used.
  - OPSWAT services: `activation.dl.opswat.com:443` for license activation; `mdss-telemetry.metadefender.com:4317` only when `ENABLE_TELEMETRY=yes`.
  - Protected storages: SMB 445, NFS 2049 and 111, SFTP 22, FTP 21 plus passive ports, and 443 to the cloud storage endpoints (Amazon S3, Azure, Google Cloud, Alibaba, Oracle, Box, Microsoft Graph, SharePoint).
  - Infrastructure the customer configured: domain controllers or LDAP servers (389, 636, 3268, 3269) for directory synchronisation, the SMTP server, webhook targets and an external RabbitMQ for notifications.

### 3.6 Behaviours to whitelist

These are normal for MDSS and produce detections in most products. Excluding the processes in 3.2 from the behavioural, anti-ransomware and child-process modules handles all of them; the list is here so the security team can recognise the alerts.

1. **Bulk file operations on network shares.** Remediation workflows delete, move, copy, rename and overwrite many files per minute. Anti-ransomware heuristics (mass delete, mass rename, canary file access, "encryption-like" writes when a file is replaced with its sanitized version) fire on this.
2. **Reading, and temporarily copying, malicious files.** MDSS downloads infected files to send them to MetaDefender Core and, depending on the workflow, writes a temporary copy before moving them to quarantine.
3. **Symbolic links to UNC paths.** The SMB sidecar creates directory symbolic links under `C:\ProgramData\OPSWAT\mdss\smb-mounts` pointing at `\\server\share`, using `WNetAddConnection2` and `CreateSymbolicLink`. It requires the "Create symbolic links" privilege. Agents that scan through reparse points scan, and may quarantine on, the customer's storage.
4. **A service spawning PowerShell and management tools.** At every start the `mdss` service runs `powershell.exe -ExecutionPolicy Bypass`, which spawns further PowerShell, `sc.exe`, `icacls.exe`, `nginx.exe`, `psql.exe`, `node.exe` and `msiexec.exe`, registers other services and changes their logon account.
5. **Start-up changes to the machine.** At every start MDSS imports CA certificates into the Trusted Root store, rewrites about 200 machine environment variables and broadcasts `WM_SETTINGCHANGE`; the installer adds firewall rules and a scheduled task. When an administrator generates a support package, MDSS runs `systeminfo`, `route print` and `ipconfig /all` and creates large archives.

Two further points explain latency rather than alerts: the service host is a single-file .NET application that loads its assemblies from inside its own image, and all .NET services JIT-compile code at run time, so memory scanning and instrumentation add latency to every one of the 12 to 40 `dotnet.exe` processes; and the supervisor polls every 10 seconds and restarts any exited child, so a blocked process becomes a restart loop.

### 3.7 Application control (allow-listing)

When application control is in enforcing mode:

1. Publisher rule for **OPSWAT, Inc.** (all MDSS executables and libraries, the ONTAP Connector).
2. Publisher rule for **Microsoft Corporation** (the private .NET runtime, Garnet, PowerShell, `msiexec.exe`, `sc.exe`, `icacls.exe`).
3. Path rule allowing everything under **<INSTALL_DIR>\**, including scripts, SQL and JavaScript files. This covers the third party runtimes (PostgreSQL, Erlang, RabbitMQ, Python, Node.js, MongoDB) whatever their signer, and `nginx.exe`, which is unsigned in 4.5.x. The folder is writable only by administrators, which is what makes a path rule acceptable here.

If your policy requires publisher rules for every file, use the enumeration command in Appendix A.9 to list the signers present on the installed system, and hash rules for the unsigned files it reports.

The `mdss` service performs its own integrity check: it refuses to start any MDSS binary that is not signed by OPSWAT and any third party runtime executable that is not signed at all. Do not let the endpoint agent modify, wrap or re-sign these files.

---

## 4. OPSWAT ONTAP Connector (NetApp ONTAP)

The connector is a separate Windows service, usually on its own Windows host next to the NetApp Antivirus Connector (`ontapavc` service). It is installed to `C:\ProgramData\OPSWAT-ONTAP-Connector\` by MDSS or manually.

- **Service**: `opswat-ontap-connector`, executable `C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe`, signed by OPSWAT.
- **Files**: `config.ini` (rewritten as storages change, via `config.ini.tmp`), `data.json`, `logs\*.log`, `OPSWAT-ONTAP-Connector.exe.bak` after an upgrade.
- **Named pipes**: `\pipe\ntapvsrq` (receives scan requests from the NetApp AV Connector) and `\pipe\ntapvscp` (registers and returns verdicts). RPC over `ncacn_np` to 127.0.0.1.
- **Registry**: writes `data-lif::<host>` values under `HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs`.
- **Network**: outbound HTTP or HTTPS to the MDSS web port (80 or 443) for `/api/webhook/realtime`, `/api/file/*`, `/api/account`, `/api/health`. SMB (445) to the ONTAP shares.
- **Behaviour**: reads every file that a user opens or modifies on the protected ONTAP shares, through `\\?\UNC\...` paths, and posts it to MDSS. These files may be malicious. Optionally writes the `Zone.Identifier` alternate data stream on files (`ZoneIdentifierFiles` setting).

Exclude the installation folder, the process, and its UNC file reads from on-access scanning. If the agent scans network files opened by this process it scans, and may quarantine on, the ONTAP volume before MDSS returns a verdict, and it doubles the latency of every file open for every ONTAP user.

---

## 5. What to keep enabled

- Everything on the operating system outside the paths and processes above. MDSS does not need the agent disabled.
- On-access scanning of files that administrators copy onto the MDSS server themselves (downloads, installers, browser).
- Network protection for destinations that are not in section 3.5.
- Logging of the MDSS behaviours in section 3.6 in audit-only mode, if the security team wants visibility. Only the blocking and quarantine actions need to be excluded.

---

## 6. Verification

Run these after configuring the exclusions.

1. PowerShell start-up time, as administrator. Expect well under one second for the first command and one to three seconds for the second.

   ```powershell
   Measure-Command { powershell.exe -NoProfile -NonInteractive -Command exit }
   cd "<INSTALL_DIR>\scripts"
   Measure-Command { powershell.exe -NoProfile -File .\mdss.ps1 -c load-ca }
   ```
2. Restart MDSS and read the step timings.

   ```powershell
   .\mdss.ps1 -c restart
   Get-Content "<INSTALL_DIR>\data\webclient\startup-log.txt"
   ```

   Every step except database migrations should complete within seconds. The whole restart should take two to four minutes on a healthy server.
3. Confirm every process is up.

   ```powershell
   .\mdss.ps1 -c status
   Get-Service mdss, mdss_postgresql, mdss_rabbitmq
   ```
4. Check the agent's own console for detections that reference the paths in 3.1, the processes in 3.2 or the behaviours in 3.6. Any remaining detection means an exclusion is missing or is by file name where a full path is required.
5. Run a scan on a storage with a known-safe test file and, if the customer uses remediation, a workflow that moves a file to quarantine. Confirm in the MDSS audit log that both complete, and confirm on the storage that no file was removed by anything other than MDSS.

---

## 7. Quick reference

| Protection category | Rule |
| ---- | ---- |
| On-access / real-time file scanning | Folders in 3.1. |
| Network file scanning | Processes in 3.2, in particular the `mdss` service tree and the ONTAP Connector. |
| Script control / PowerShell protection | `<INSTALL_DIR>\scripts\*.ps1` with parent `mdss` service, `msiexec.exe` or an elevated administrator (3.3). |
| Executable and library examination, reputation lookups | Processes in 3.2; publisher OPSWAT, Inc. |
| Child-process / process-tree protection | `opswat.mdss.windows.service.exe` and its descendants (3.2 rule 1). |
| Behavioural, anti-ransomware, exploit and memory protection | Processes in 3.2. |
| .NET / runtime instrumentation | Processes in 3.2, including `powershell.exe` started by them. |
| Tamper, persistence, registry and certificate store monitoring | Services, task, firewall rules and registry keys in 3.4. |
| Host firewall / network protection | Ports and destinations in 3.5. |
| Application control | Two publisher rules and one path rule in 3.7. |

---

## Appendix A. Detailed inventory

Use this appendix when your product has no wildcard or parent-process trust feature, or when policy requires each exclusion to be enumerated. It contains every item the rules in section 3 stand for.

### A.1 Installation folder layout

- `services\`: one subfolder per MDSS microservice with its `.dll` files and its `logs\` folder, plus the private .NET runtime (`services\dotnet`), Garnet cache (`services\garnet`), nginx (`services\opswat.mdcs.webclient`), PostgreSQL (`services\postgres`), RabbitMQ (`services\rabbitmq`), Erlang (`services\erlang`), the SMB sidecar (`services\opswat.mdss.smb.service`), the Windows service host (`services\opswat.mdss.windows.service`), legacy Python (`services\python`) and legacy MongoDB (`services\mongo`). Hundreds of executables and libraries are loaded at every start, and the log files are written continuously.
- `data\`: PostgreSQL data files (`data\postgres`), the RabbitMQ message store (`data\rabbitmq\rabbit@localhost-mnesia`), the web client files (`data\webclient`) and legacy MongoDB data (`data\mongo`). Database files are rewritten constantly; scanning them causes latency and lock conflicts.
- `logs\`: PostgreSQL, RabbitMQ, migration and installation logs.
- `config\`: `.env`, `customer.env`, nginx configuration and TLS certificates (`config\nginx\certificates`), RabbitMQ, PostgreSQL and Garnet configuration. Rewritten at every start by the maintenance scripts.
- `scripts\`: the PowerShell maintenance scripts listed in A.5.
- `dependencies\`: compressed third party runtimes extracted during install and upgrade.
- `Utils\`: SQL migration scripts and installer prerequisites (SharePoint client components MSI, Visual C++ runtime).
- `ca_certificates\`: customer supplied CA certificates imported into the Windows trust store at every start.
- `tmp\` and `<INSTALL_DIR>\*.zip`: working folder and output of the support package, log export, settings export and database export commands.

Outside the installation folder: `C:\ProgramData\OPSWAT\mdss_upgrade_service_account.txt` (upgrade state), `C:\ProgramData\OPSWAT\mdss\smb-mounts\` (SMB mount symlinks, see 3.1), `C:\ProgramData\OPSWAT-ONTAP-Connector\` (section 4), `%APPDATA%\OPSWAT\MetaDefender Storage Security\backup\` (installer configuration backup), and the service account's temp folder (see 3.1).

### A.2 Windows services, scheduled task and firewall rules

- **mdss** (MetaDefender Storage Security): `<INSTALL_DIR>\services\opswat.mdss.windows.service\opswat.mdss.windows.service.exe`. The supervisor. Starts and monitors every other MDSS process. Runs as `LocalSystem` by default; the customer may change it to a domain or gMSA account.
- **mdss_postgresql** (MDSS PostgreSQL): `<INSTALL_DIR>\services\postgres\bin\pg_ctl.exe`, which runs `postgres.exe`. Registered with `pg_ctl register`, reconfigured with `sc.exe config` and `sc.exe failure`.
- **mdss_rabbitmq** (RabbitMQ): `<INSTALL_DIR>\services\erlang\erts-*\bin\erlsrv.exe`, which runs `erl.exe`. Registered with `rabbitmq-service.bat install`. Also writes `HKLM\SOFTWARE\Ericsson\Erlang\ErlSrv\1.1\MDSS_RabbitMQ`.
- **mdss_mongodb** (MDSS MongoDB): `<INSTALL_DIR>\services\mongo\mongod.exe`. Legacy. Present only on systems upgraded from MDSS 3.x, stopped and set to Manual once the data migration to PostgreSQL has completed.
- **opswat-ontap-connector** (OPSWAT ONTAP Connector): `C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe`. Only when the NetApp ONTAP integration is used.
- Scheduled task **MDSS_InstallSharePointComponents**: runs `powershell.exe -ExecutionPolicy Bypass -WindowStyle Hidden -NoProfile -File "<INSTALL_DIR>\scripts\install-sharepoint-components.ps1"` once at system startup as `SYSTEM`. Present only when the SharePoint On-Premises module is enabled.
- Windows Firewall inbound rules named **MetaDefender Storage Security: Allow inbound traffic <NAME> - <PORT>** for the licensing, NFS and SMB sidecar ports.

### A.3 Executables

**Process tree.** `services.exe` starts `opswat.mdss.windows.service.exe`. That process starts `powershell.exe` for the startup orchestration, which in turn starts more `powershell.exe` instances, `nginx.exe -s reload`, `psql.exe`, `node.exe` and `msiexec.exe`. After orchestration it starts and keeps alive every process below, restarting any that exits.

- **<INSTALL_DIR>\services\opswat.mdss.windows.service\opswat.mdss.windows.service.exe** (signed by OPSWAT). The `mdss` service, started by the Service Control Manager. Self-contained single-file .NET application: it loads its managed assemblies from inside its own executable image rather than from separate `.dll` files on disk, which some agents flag as in-memory loading. Validates the code signature of every MDSS binary before starting it.
- **<INSTALL_DIR>\services\dotnet\dotnet.exe** (signed by Microsoft). The private .NET runtime. Every MDSS microservice runs as this executable with the service `.dll` as its first argument, so expect 12 to 40 concurrent instances. Exclude by this exact path; do not exclude every `dotnet.exe` on the host. The hosted services are listed in A.4.
- **<INSTALL_DIR>\services\opswat.mdss.smb.service\opswat.mdss.smb.service.exe** (signed by OPSWAT). SMB sidecar. Authenticates to SMB servers, creates directory symbolic links under `C:\ProgramData\OPSWAT\mdss\smb-mounts`, reads and writes files on the shares. Listens on 127.0.0.1:6002 and 127.0.0.1:7002.
- **<INSTALL_DIR>\services\opswat.mdcs.webclient\nginx.exe** (unsigned in 4.5.x). Web server for the MDSS console and reverse proxy for the API. Runs as a master process plus one worker. Listens on ports 80 and 443 (configurable).
- **<INSTALL_DIR>\services\garnet\GarnetServer.exe** (signed by Microsoft). Redis-compatible cache. Listens on 127.0.0.1:6379. Writes log files to its own folder.
- **<INSTALL_DIR>\services\postgres\bin\postgres.exe, pg_ctl.exe, psql.exe, pg_dump.exe, pg_restore.exe, pg_isready.exe, initdb.exe** (PostgreSQL vendor build). Database server and its tools, run by the `mdss_postgresql` service and by the maintenance scripts. `postgres.exe` forks one backend per connection. Listens on 127.0.0.1:5432.
- **<INSTALL_DIR>\services\erlang\erts-*\bin\erlsrv.exe, erl.exe, epmd.exe, inet_gethost.exe** and **<INSTALL_DIR>\services\rabbitmq\sbin\rabbitmq-service.bat, rabbitmqctl.bat** (Erlang and RabbitMQ vendor builds, may be unsigned). Message broker, run by the `mdss_rabbitmq` service and by the maintenance scripts. Listens on 127.0.0.1:5672, 15672, 25672 and 4369.
- **C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe** (signed by Microsoft). Windows PowerShell 5.1 running the scripts in A.5, started by the `mdss` service, the installer and administrators. Launched with `-ExecutionPolicy Bypass -NoProfile -NonInteractive -File`.
- **C:\Windows\System32\msiexec.exe** (signed by Microsoft). Installs `<INSTALL_DIR>\Utils\prerequisites\sharepointclientcomponents.msi` when the SharePoint On-Premises module is enabled, and the MDSS MSI itself.
- **C:\Windows\System32\sc.exe, icacls.exe, systeminfo.exe, route.exe, ipconfig.exe** (signed by Microsoft). Run by the maintenance scripts for service configuration, permission changes on `customer.env`, and host information collected into the support package.
- **<INSTALL_DIR>\services\python\python.exe** (Python Software Foundation). Legacy SMB sidecar (`server.py`), five processes on ports 6002 to 6006 and 7002 to 7006. Only when `USE_OPSWAT_SMB_SERVICE=false`.
- **<INSTALL_DIR>\services\mongo\mongod.exe, mongosh.exe** and **<INSTALL_DIR>\services\opswat.mdcs.mongomigrations\node.exe** (MongoDB Inc., Node.js). Legacy database and its migration tooling. Only on systems upgraded from MDSS 3.x, until the migration to PostgreSQL has completed.
- **<INSTALL_DIR>\services\opswat.mdss.reencryption.cli\opswat.mdss.reencryption.cli.exe** (signed by OPSWAT). Command line tool for re-encrypting stored credentials, run by administrators.
- **C:\ProgramData\OPSWAT-ONTAP-Connector\OPSWAT-ONTAP-Connector.exe** (signed by OPSWAT). See section 4.

### A.4 Microservices hosted by `dotnet.exe`

If your product filters on the command line rather than the process path, allow `dotnet.exe` when its argument is one of these files. Paths are under `<INSTALL_DIR>\services\`, and each runs with its own folder as the working directory.

- Licensing: `opswat.mdcs.license.service\opswat.mdcs.license.service.dll`, listens on 127.0.0.1:5001 (gRPC).
- API Gateway: `opswat.mdcs.api.gateway\opswat.mdcs.api.gateway.dll`, listens on 127.0.0.1:8005 and 8006.
- Identity: `opswat.mdss.identity.service\opswat.mdss.identity.service.dll`, listens on 127.0.0.1:7001.
- Logging: `opswat.mdcs.logging.service\opswat.mdcs.logging.service.dll`.
- Job Dispatcher: `opswat.mdcs.job.dispatcher\opswat.mdcs.job.dispatcher.dll`.
- Notification: `opswat.mdcs.notification.service\opswat.mdcs.notification.service.dll`.
- Scanning: `opswat.mdcs.scanning.service\opswat.mdcs.scanning.service.dll`, 1 to 30 instances (`WINDOWS_SCANNING_SERVICE_INSTANCES`).
- Discovery: `opswat.mdss.discovery.service\opswat.mdss.discovery.service.dll`.
- Remediations: `opswat.mdss.remediations.service\opswat.mdss.remediations.service.dll`.
- Storages: `opswat.mdss.storages.service\opswat.mdss.storages.service.dll`.
- Workflow Manager: `opswat.mdss.workflowmanager.service\opswat.mdss.workflowmanager.service.dll`.
- NFS sidecar (NFS module only): `opswat.mdss.nfs.service\opswat.mdss.nfs.service.dll`, listens on 127.0.0.1:5004.

The Discovery, Storages and Remediations services load the storage provider libraries (Amazon S3, Azure, Google Cloud, Box, SharePoint, SFTP, FTP and others) in-process from their own folders. The Scanning service additionally loads provider libraries from a `providers` folder and verifies their Authenticode signature with Windows before loading them. An agent that blocks or delays library loading, or that strips or alters signatures, prevents these services from starting.

### A.5 PowerShell scripts

All scripts live in `<INSTALL_DIR>\scripts\`. They are Windows PowerShell 5.1 scripts, so they run on the .NET Framework; agents that hook the .NET Framework through the `APPDOMAIN_MANAGER_ASM` and `APPDOMAIN_MANAGER_TYPE` machine environment variables inspect every one of these processes and can add minutes to each. The installer additionally sets the process execution policy to `Unrestricted` when it runs `init.ps1` in-process.

- **startup-orchestration.ps1**, started by the `mdss` service at every start. Orchestrates everything below: clears the RabbitMQ queue store, imports CA certificates, validates JSON files, refreshes configuration, regenerates the web client `env-config.js`, applies HTTP or HTTPS configuration, syncs about 200 environment variables to Machine scope, reloads nginx, installs SharePoint components, runs database migrations.
- **mdss.ps1**, started by the orchestration (`-c load-ca`, `-u enable_https`, `-u disable_https`) and by administrators (`-c start/stop/restart/status`, `-u support_package`, `-u export_db`, and others). Main maintenance entry point. `load-ca` writes each certificate to a temporary `.crt` file and imports it into `Cert:\LocalMachine\Root`. `support_package` runs `systeminfo`, `route print`, `ipconfig /all`, collects logs and compresses them. `export_db` runs `pg_dump.exe`.
- **init.ps1**, started by the installer (in-process, inside `msiexec.exe`) and by the orchestration (`-setenv`). Installation and environment setup. Writes machine environment variables, broadcasts `WM_SETTINGCHANGE`, creates firewall rules and the SharePoint scheduled task.
- **dependencies.ps1**, started by the installer and by the orchestration (`-refresh`). Extracts and registers PostgreSQL, RabbitMQ, Erlang, nginx, Garnet, .NET, Python and MongoDB. Registers Windows services with `sc.exe`, `pg_ctl.exe`, `rabbitmq-service.bat` and `mongod.exe --install`. Regenerates nginx and PostgreSQL configuration. Updates the ONTAP Connector binary in place.
- **migrations_postgres.ps1, migrations.ps1, migrations_mongo_to_postgres.ps1**, started by the orchestration. Database schema and data migrations using `psql.exe` and, on upgraded systems, `node.exe`.
- **install-sharepoint-components.ps1**, started by the orchestration and by the scheduled task. Runs `msiexec.exe` to install the SharePoint client components MSI.
- **mdss-service-logon.ps1, write-customer-env.ps1, InstallationStatus.ps1, monitor-installation.ps1, mdss-resp-client.ps1**, started by the installer and by the other scripts. Restore the service logon account after upgrade (`sc.exe config`, `icacls`), write `customer.env`, report installer progress, talk to the Garnet cache.

### A.6 Registry keys

- **HKLM\SOFTWARE\OPSWAT\MetaDefender Storage Security**, written by the installer: `InstallDir` and installation state.
- **HKLM\SYSTEM\CurrentControlSet\Services\mdss, mdss_postgresql, mdss_rabbitmq, mdss_mongodb, opswat-ontap-connector**, written by the installer and the scripts: service definitions, recovery options, logon account.
- **HKLM\SOFTWARE\Ericsson\Erlang\ErlSrv\1.1\MDSS_RabbitMQ**, written by the RabbitMQ service registration: Erlang service parameters.
- **HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment**, written by `init.ps1 -setenv` and the orchestration: about 200 MDSS-related machine environment variables (ports, connection strings, feature flags, `DOTNET_ROOT`, `ERLANG_HOME`, `RABBITMQ_*`). Rewritten at every service start.
- **HKLM\SOFTWARE\Microsoft\SystemCertificates\ROOT\Certificates**, written by `mdss.ps1 -c load-ca`: customer CA certificates from `<INSTALL_DIR>\ca_certificates` imported into the machine Trusted Root store.
- **HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs**, written by the ONTAP Connector: one `data-lif::<host>` value per protected NetApp SVM.

### A.7 Loopback ports

Bound to 127.0.0.1 unless the customer changed the listening IP.

- 8005, 8006: API Gateway.
- 5001: Licensing (gRPC).
- 7001: Identity.
- 6002, 7002: SMB sidecar (gRPC and health). Legacy Python sidecar: 6002 to 6006 and 7002 to 7006.
- 5004: NFS sidecar.
- 5432: PostgreSQL.
- 5672, 15672, 25672, 4369: RabbitMQ, management, Erlang distribution, port mapper.
- 6379: Garnet cache.
- 27017, 27778: legacy MongoDB and its migration tool.

### A.8 .NET and process instrumentation

Some agents inject a component into every .NET process, either through the `APPDOMAIN_MANAGER_ASM` / `APPDOMAIN_MANAGER_TYPE` machine environment variables (affects Windows PowerShell 5.1 and other .NET Framework processes such as the MSI custom actions) or through a CLR profiler or startup hook (affects the .NET 10 services hosted by `dotnet.exe`). Exclude from this instrumentation:

- `powershell.exe` when its parent is `opswat.mdss.windows.service.exe`, `msiexec.exe` or another `powershell.exe` from the MDSS tree, or when the script path is under `<INSTALL_DIR>\scripts\`.
- `<INSTALL_DIR>\services\dotnet\dotnet.exe`
- `<INSTALL_DIR>\services\opswat.mdss.windows.service\opswat.mdss.windows.service.exe`
- `<INSTALL_DIR>\services\opswat.mdss.smb.service\opswat.mdss.smb.service.exe`
- `<INSTALL_DIR>\services\garnet\GarnetServer.exe`

The startup timing in `data\webclient\startup-log.txt` is the fastest way to confirm this exclusion works: the three script-heavy steps ("Loading CA certificates", "Refreshing environment and nginx configuration", "Applying HTTP/HTTPS configuration") should each take a few seconds.

### A.9 Code signers

- **Publisher OPSWAT, Inc.**: `opswat.mdss.windows.service.exe`, `opswat.mdss.smb.service.exe`, `OPSWAT-ONTAP-Connector.exe`, `opswat.mdss.reencryption.cli.exe`, every `opswat.*.dll`.
- **Publisher Microsoft Corporation**: `dotnet.exe` and the .NET runtime libraries under `services\dotnet`, `GarnetServer.exe`, `powershell.exe`, `msiexec.exe`, `sc.exe`, `icacls.exe`.
- **Publishers of the third party runtimes** (PostgreSQL build vendor, Erlang/OTP, RabbitMQ, Python Software Foundation, Node.js, MongoDB Inc.): the corresponding runtimes under `services\`.
- **Unsigned**: `services\opswat.mdcs.webclient\nginx.exe` in 4.5.x, and possibly some third party runtime files. Use path or hash rules for these.

Enumerate the real signers on the installed system before writing publisher rules, because third party runtime versions change between MDSS releases:

```powershell
Get-ChildItem "<INSTALL_DIR>\services" -Recurse -Include *.exe,*.dll |
  Get-AuthenticodeSignature |
  Group-Object { if ($_.SignerCertificate) { $_.SignerCertificate.Subject } else { "UNSIGNED" } } |
  Select-Object Count, Name | Sort-Object Count -Descending
```

Application control must also allow the PowerShell scripts in `<INSTALL_DIR>\scripts\` and the SQL and JavaScript files in `<INSTALL_DIR>\Utils\` and `<INSTALL_DIR>\services\opswat.mdcs.mongomigrations\`.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
