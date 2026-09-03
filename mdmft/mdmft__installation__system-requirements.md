<!-- source: https://www.opswat.com/docs/mdmft/installation/system-requirements -->

# System Requirements

Summarize Page    Connect to Cursor Connect to VS Code
## [Hardware Requirements](/docs/mdmft/installation/system-requirements#hardware-requirements)

|  | Minimum | Recommended |
| --- | --- | --- |
| CPU | 4 cores | 16 cores |
| RAM | 8 GB | 32 GB |
| Free Disk  Space | Sufficient  to temporarily hold at least double the size of the file you wish to process.  For instance, to process a 1 TB file, ensure at least 2.1 TB of free space is available. Once processing is complete, the space will be restored. |  |
| DB CPU | 4 Cores | 8 Cores |
| DB RAM | 8 GB | 16 GB |
| DB storage | Determined by log retention policies (default: 90 days). Unlikely to exceed 1 GB.  Examples:   - 160 MB initial size (clean install) - +64 MB / 4000 users - +64 MB / 3000 files   Note: files themselves are not stored in the database. |  |

## [Operation System Requirements](/docs/mdmft/installation/system-requirements#operation-system-requirements)

- Microsoft Windows Server 2019 / 2022 / 2025
- Architecture: 64-bit only

Unsupported Operating Systems

Based on [Microsoft License Terms](https://www.microsoft.com/en-us/useterms), Windows Desktop is not allowed to be used as a server, therefore, MetaDefender Managed File Transfer™ does not support the following:

- Windows 10 (22H2)
- Windows 10 (IoT Enterprise LTSB/LTSC editions 1607, 1809, 21H2)
- Windows 11 [all editions)
- all other Desktop editions that have reached end of support from Microsoft
Info

MetaDefender Managed File Transfer™ has been tested and works as expected on CIS-hardened images. This ensures compliance with the CIS standard for security and configuration

Software Requirements

- [Windows Installer 5.0 or higher](/docs/mdmft/installation/system-requirements#additional-installation-of-third-party-frameworkscomponents)
- [Additional frameworks/components](/docs/mdmft/installation/system-requirements#additional-installation-of-third-party-frameworkscomponents)

## [Minimum Supported Browsers](/docs/mdmft/installation/system-requirements#minimum-supported-browsers)

- Chrome 67 or later
- Microsoft Edge last two major version
- Safari last two major version
- Firefox 68 or later

## [Additional Installation of Third-Party Frameworks/Components](/docs/mdmft/installation/system-requirements#additional-installation-of-third-party-frameworkscomponents)

MetaDefender Managed File Transfer automatically installs the following frameworks/components which should not be removed:

Warning

For MetaDefender Managed File Transfer™ version **3.9.2** Microsoft Visual C++ 2015-2019 redistributable needs to be manually installed if:

- This is the first time MetaDefender Managed File Transfer™ is installed on the host machine
- and the operating system doesn't have it installed already. For example with Windows Server editions.

| Name | Details |
| --- | --- |
| .NET Framework | [Microsoft .NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48), |
| Microsoft Visual C++ 2015-2019 redistributable | [Microsoft Visual C++ Redistributable 2015-2019](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0) |
| .NET Runtime | [.NET 8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) |
| ASP.NET Runtime | [ASP.NET Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/7.0) |

## [Database](/docs/mdmft/installation/system-requirements#database)

Before installing MetaDefender Managed File Transfer, you must first set up a Microsoft SQL Server database. The table below lists the supported Microsoft SQL Server editions (including Express):

| Name | Editions | Supported |
| --- | --- | --- |
| SQL Server 2016 | All | Yes |
| SQL Server 2017 | All | Yes |
| SQL Server 2019 | All | Yes |
| SQL Server 2022 | All | Yes |
| SQL Server 2025 | All | Yes |

Warning

The SQL Server instance must have **Force Encryption** enabled (`ForceEncryption = Yes`) to ensure all client-server communication is encrypted via TLS.

Info

The **Force** ***Strict*** **Encryption** option in SQL Server is not compatible with MFT. If this setting is enabled, MFT will be unable to establish a connection to the database.

### [Permissions](/docs/mdmft/installation/system-requirements#permissions)

During installation, MetaDefender® MFT creates two databases: `sft_data` and `sft_conn`. To allow database creation, the SQL Server account used for installation must have the `CREATE ANY DATABASE` permission. For more details on SQL Server database permissions, see [Microsoft’s documentation](https://learn.microsoft.com/en-us/sql/relational-databases/security/permissions-database-engine?view=sql-server-ver17#sql-server-permissions).

After installation, MetaDefender® MFT should run using a SQL Server login that is the owner of both databases—that is, the account must have the `db_owner` role on `sft_data` and `sft_conn`. You can learn more about the `db_owner` role in [Microsoft’s documentation](https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-ver16#fixed-database-roles).

Info

`db_owner` role is required to operate MetaDefender® MFT because there are features which require database level operations.

For example MetaDefender® MFT initiates database backups for operations including encryption key rotation and product version upgrades.

Info

Windows Authentication (Integrated Security) is supported, and the service account should have "Logon as Service" rights.

Info

Azure SQL Managed Instance can serve as the database for MetaDefender Managed File Transfer™. However, network speed and the physical distance between MetaDefender® MFT and the database instance can result in slower response times for MetaDefender® MFT

### [About SQL Server Express LocalDb](/docs/mdmft/installation/system-requirements#about-sql-server-express-localdb)

Starting from version 3.9.2:

- LocalDb can't be selected for a new installation
- SQL Server Express LocalDb is not bundled or installed by MetaDefender Managed File Transfer™ installer
- Existing deployments using LocalDb may upgrade to a newer version as long as the version being upgraded to supports LocalDb.

Warning

Microsoft SQL Server 2019 Express LocalDb is primarily designed for testing and development purposes and is not recommended for production environments.

Using this database in a production setting can result in data loss and significant performance issues, especially under high load.

For reliable and secure operation, we recommend using a more robust database solution. We strongly advise against deploying this backend in live production systems.

Info

For information about how to migrate from Microsoft SQL Server 2019 Express LocalDB, refer to our [documentation](/docs/mdmft/knowledge-base/sql-server-express-localdb-migration).

## [Web Server Configuration](/docs/mdmft/installation/system-requirements#web-server-configuration)

MetaDefender Managed File Transfer uses NGINX as the embedded HTTP(S) and reverse proxy server. The web server is embedded in the application and is not shared with other processes running on the machine. After uninstalling MetaDefender Managed File Transfer, all NGINX processes will be stopped, and the program will be physically removed from the hard drive.

On startup, the web server will listen on the configured HTTP(S) port or on the default HTTP port (8010 if free) in case of a clean install.

Info

From versions 1.3.7 onwards, REST API calls should be made to the Web UI port because TLS/SSL connections are no longer supported and the REST API service connection is thus unsecured. NGINX acts as a TLS/SSL termination proxy for the REST API service.

## [Port Usage](/docs/mdmft/installation/system-requirements#port-usage)

MetaDefender Managed File Transfer requires two free ports to run.

| Service name | Port | Firewall Rule |
| --- | --- | --- |
| MetaDefender Managed File Transfer Web UI | 8010 | Needed |
| MetaDefender Managed File Transfer REST API | 8000 | Not needed;  Internal usage only |
| MetaDefender Managed File Transfer Next | 8001 | Not needed; Internal usage only |

## [Whitelisting Requirements](/docs/mdmft/installation/system-requirements#whitelisting-requirements)

- To access the user interface externally, open port 8010 (default).
- Whitelist any processes running from the MetaDefender Managed File Transfer install directory. Exclude the folder from any real-time protection.
- Exclude the file storage (permanent and temporary) or the installation folder from real-time protection.
- The service account should have "Logon as Service" rights to:

  - Start, stop, and interact with services without requiring interactive logon privileges.
  - Log on and run scheduled or automatically executed batch jobs.
  - Connect to the database using Windows Authentication.

## [Recommended deployment setups](/docs/mdmft/installation/system-requirements#recommended-deployment-setups)

When planning where to install MetaDefender Managed File Transfer™ and the supporting SQL Server instance, consider the expected scale of your deployment:

#### [Small environments](/docs/mdmft/installation/system-requirements#small-environments)

For small teams, lab, or testing environments it's acceptable to run a collocated SQL Server (for example SQL Server Express) on the same host or VM as MetaDefender Managed File Transfer™ . This keeps deployment and management simple and reduces resource needs.

Note

Use this setup only when load is light and you understand the limitations of SQL Server Express.

#### [Medium & Large production environments](/docs/mdmft/installation/system-requirements#medium--large-production-environments)

For medium and large environments we strongly recommend running SQL Server on a separate VM or physical server with dedicated, fast (SSD) storage. The SQL Server workload for MetaDefender Managed File Transfer™ is often heavy on RAM and disk I/O; these two resources have the largest impact on real-world performance.

- Adding many CPU cores alone does not linearly improve SQL performance and can sometimes exacerbate contention (locks and context switching). Prioritize generous RAM and high I/O throughput (low latency, high IOPS) over simply increasing core counts.
- We recommend that an experienced database administrator be responsible for sizing, deploying, and maintaining the SQL Server instance used by MetaDefender Managed File Transfer™ . Common operational tasks include backups, statistics updates, monitoring for long-running queries, and tuning tempdb. In our experience, maintenance of the SQL Server instance can often prevent downtime, avoiding disruptions to production.
- Ensure an adequately sized, low-latency network link between the MetaDefender Managed File Transfer™ server and the SQL Server instance. Network latency and bandwidth between MetaDefender Managed File Transfer™, the database, and your clients directly affect end-user performance.
- Other OPSWAT products (for example, MetaDefender Core™ and its own database) should live on separate VMs or hosts. Collocating multiple product databases or services on the same host increases IO and memory contention and can mask the true source of performance issues.

Additional operational tips

- Monitor database metrics (memory utilization, disk queue length/latency, waits, and transaction log growth) and tune retention/cleanup settings to control growth.
- Use regular backups and test restores; ensure the service account used by MetaDefender Managed File Transfer™ has the required permissions and that SQL Server maintenance windows are coordinated with your MetaDefender Managed File Transfer™ support plan.
- By default, MetaDefender Managed File Transfer™ sets its databases to use [Simple Backup](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql).
