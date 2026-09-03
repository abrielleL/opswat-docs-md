<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package -->

[MetaDefender Core](https://www.opswat.com/docs/mdcore)Need Help?
# Which data is contains in a support package

This document describes the categories of data collected by the MetaDefender Core support package script (`ometascan-collect-support-data.bat/sh`). This package is generated on request to help OPSWAT technical support diagnose issues on a customer's system.

## [What Is Collected](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#what-is-collected)

### [1. Hardware Information](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#3-network-information)

| Data | Description |
| --- | --- |
| CPU details | Processor model, speed, core count, and other properties |
| Memory details | Physical RAM modules, capacity, and specifications |
| Disk drives | Physical disk drive model, size, and interface type |
| Logical disks | Drive letters, file system type, used/free space |

### [2. Operating System Information](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#4-installation-directory-listing)

| Data | Description |
| --- | --- |
| OS version | Windows/Linux edition, version number, build number |
| OS configuration | System locale, install date, registered organization |

### [3. Network Information](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#5-configuration-data)

| Data | Description |
| --- | --- |
| Network interfaces | IP addresses, MAC addresses, DNS servers, DHCP settings |
| Routing table | All active network routes on the machine |

### [4. Installation Directory Listing](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#6-database-information)

A recursive listing of all files and folders under the MetaDefender Core installation directory. This includes file names, sizes, and timestamps — **not** file contents.

### [5. Configuration Data](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#7-application-logs)

Common configuration: via Registry (Windows) or Configuration file (Linux)

### [6. Database Information](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#8-crash-dump-files)

| Data | Description |
| --- | --- |
| Exported database schema | A structured export of the MetaDefender Core internal database |
| PostgreSQL configuration | Configuration files (`*.conf`) from the embedded PostgreSQL instance |
| PostgreSQL data files | Non-binary configuration/settings files from the `pg_data` directory |
| PostgreSQL logs | Files related to any database upgrade operation (`pg_upgrade*`) and operational logs |

**Note:** The database export may contain scan job metadata and product configuration. It does **not** contain the actual file content of scanned files.

### [7. Application Logs](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#what-is-not-collected)

| Data | Description |
| --- | --- |
| MetaDefender Core application logs | Operational events, errors, warnings from the core service |
| Nginx web server logs of MetaDefender Core | HTTP request/error logs for the management interface |
| Engine logs (AV engine, Filetype, Deep CDR, etc) | Diagnostic output from individual anti-malware engines and other engines |
| Windows event or Syslog (Linux) | We only collect windows event or syslog belong to the application, **not all of the event/logs** |

### [8. Crash Dump Files](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#privacy-considerations)

If any of the following processes have previously crashed, their crash dump files are included:

- `ometascan.exe`
- `engineprocess.exe`
- `ocmdatatransporter.exe`

## [What Is NOT Collected](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#1-hardware-information)

- The **actual content of files** that were submitted for scanning
- **User credentials** or passwords (these are not stored in any of the collected sources)
- Data from **outside the MetaDefender Core installation directory** (except process info, network info, and OS info described above)

## [Privacy Considerations](/docs/mdcore/troubleshooting/which-data-is-contains-in-a-support-package#2-operating-system-information)

Customers who have concerns about specific data categories can use the following options before generating the package:

- Use `-enable-redact` to redact potentially sensitive values from log files.
- Use `-lite` to limit the volume of data collected (fewer logs, most recent crash dump only, no warehouse database).
- Use `-start-date` and `-end-date` to restrict log collection to a specific time window.
- Contact OPSWAT support to discuss which specific components are needed for your case before generating a full package.
