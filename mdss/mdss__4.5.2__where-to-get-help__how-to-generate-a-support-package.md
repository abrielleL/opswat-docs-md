<!-- source: https://www.opswat.com/docs/mdss/4.5.2/where-to-get-help/how-to-generate-a-support-package -->

# How to generate a support package

## Linux deployment

Run the following command:

```bash
sudo mdss -u support_package
```

In case of a successful generation, you should see the following message:

```powershell
Support package was exported to /etc/mdss/mdss_3.6.1.10601_support_package_2025-06-03_16-16-44.tar
```

## Windows deployment

> **PowerShell Compatibility Notice**
>
> Our product has been thoroughly tested and optimized for compatibility with **PowerShell 5.x**, which is the default Windows PowerShell version included with Windows Server 2019, 2022 and 2025.
>
> When generating a support package for troubleshooting purposes, please ensure that you use **Windows PowerShell 5.x** and not PowerShell 7 (PowerShell Core). This will make sure that all diagnostic information is correctly captured and formatted for our analysis tools.

Before you begin, please run the following command in an elevated **PowerShell** to allow the utility script (**mdss.ps1**) to be executed

```powershell
PS> Set-ExecutionPolicy RemoteSigned
```

In order to generate a support package please run the following commands in the scripts folder within the installation folder (by default *C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts*)

```powershell
PS> .\mdss.ps1 -u support_package
```

In case of a successful generation, you should see the following message:

```powershell
MetaDefender Storage Security support package was exported to C:\Program Files\OPSWAT\MetaDefender Storage Security\support_package_{date}.zip
```

## For Kubernetes Deployment

In case of issues that require further investigation by OPSWAT support, a package can be generated using the `sp.sh` script what contains pod logs, configurations and details regarding the Kubernetes deployment. In order to generate the support package, make the `sp.sh` script executable and run the following command:

[./sp.sh <NAMESPACE>](https://github.com/OPSWAT/metadefender-k8s/tree/main/troubleshooting)

Notes:

- The namespace name where the application is deployed needs to be specified as an argument, otherwise the default namespace is used.
- The script uses `kubectl` to extract the required information, make sure `kubectl` is installed and configured with the correct context.
- The script generates the support package as a zip file in the same directory where it is executed.

## Maximum  limit

The package can grow very large on systems with extensive logs. In order to prevent this, you can use the -m / --max-size argument as such:

### Linux

```bash
sudo mdss -u support_package -m 500M
sudo mdss -u support_package -m 1G
sudo mdss -u support_package -m 1.5G
```

### Windows

```bash
.\mdss.ps1 -u support_package
.\mdss.ps1 -u support_package -MaxSize 500M
.\mdss.ps1 -u support_package -MaxSize 1G
.\mdss.ps1 -u support_package -m 1.5G
```

### How the size budget is allocated internally

When -m is provided, the total budget is split into two parts:

1. Settings/host info reservation — 50MB reserved for non-log data (settings, host info, env files). Configurable via env var **RESERVED_FOR_SETTINGS**.
2. Logs budget = max_size - 50MB — everything remaining goes to logs.

The logs budget itself is then divided into:

- Container logs — each container is capped at the last 25,000 lines (configurable via **CONTAINER_LOG_LINES**)
- Script logs — always included in full (usually small)
- Service logs — whatever budget remains after container + script logs

### How service logs are collected (the two-phase approach)

**Phase 1** — Fair representation: Takes the N most recent log files from each service (default: 1 file, configurable via **MIN_FILES_PER_SERVICE**). This guarantees every service has at least some representation in the package, even if the budget is tight. **Phase 2** — Fill remaining budget: Any budget left after Phase 1 is filled with the most recently modified log files across all services, globally sorted by timestamp — most recent first.Files are never arbitrarily truncated — they are only truncated if they exceed the remaining budget, and when truncated, the last N bytes are kept (most recent content) via tail -c.

## Environment variable overrides

| Variable | Default | Description |
| ---- | ---- | ---- |
| RESERVED_FOR_SETTINGS | 50MB | Space reserved for settings/host info |
| MIN_FILES_ PER_SERVICE | 1 | Minimum files per service in Phase 1 |
| CONTAINER_LOG_LINES | 25000 | Max container log lines when -m is active |
| SERVICES_LOG_PATH | ./services_logs | Path to service log files |

> **Default limit**
>
> There is a maximum size set by default, which, if not modified it limits the support package to **2GB** on Windows and **5GB** on Linux.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
