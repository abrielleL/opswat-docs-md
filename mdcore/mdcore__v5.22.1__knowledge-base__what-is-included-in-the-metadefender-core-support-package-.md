<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package- -->

# What is Included in the MetaDefender Core Support Package?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

When troubleshooting issues with MetaDefender Core, OPSWAT support may request a support package. Here’s a support article, [“How to Create Support Package With Web Console,”](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-with-web-console#advanced) that explains how to generate a support package. You can choose either an Advanced or Lightweight support package depending on the level of information you would like to collect for analysis.

## [1. Config Folder](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#1-config-folder)

The `config` folder contains configuration details of the MetaDefender Core server. These configurations define various settings and operational parameters. More details on the MetaDefender Core configuration can be found [here](/docs/mdcore/v5.22.1/configuration/metadefender-configuration).

## [2. Crashdump Folder](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#2-crashdump-folder)

The `crashdump` folder includes memory dumps generated when MetaDefender Core crashes. These dumps provide insights into system failures and help in debugging crash-related issues.

## [3. Database Folder](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#3-database-folder)

The `database` folder consists of:

- Logs from the PostgreSQL server used by MetaDefender Core.
- A PostgreSQL database dump, which captures the state of the database for further analysis.

## [4. Enginelogs Folder](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#4-enginelogs-folder)

The `enginelogs` folder contains logs for all the engines integrated into MetaDefender Core. These logs are useful for identifying engine-specific issues or performance-related concerns.

## [5. Log Folder](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#5-log-folder)

The `log` folder contains:

- The primary log files of MetaDefender Core.
- Logs related to the Nginx engine, which may be useful for identifying network or proxy-related issues.
- Starting from MetaDefender Core **v5.17.0**, you can also export **Windows Event Logs** from the Log section. These logs are useful when troubleshooting application crashes.

## [6. Process Folder](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#6-process-folder)

The `process` folder includes details about the active MetaDefender Core processes. This information helps in diagnosing issues related to system performance and resource utilization.

## [7. files.info](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#7-filesinfo)

The `files.info` file lists the contents of the MetaDefender Core installation directory. This file helps in verifying the integrity of installed files and identifying missing or modified components.

## [8. hw.info](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#8-hwinfo)

The `hw.info` file provides hardware details of the system running MetaDefender Core. This information is useful for ensuring that the server meets the recommended hardware specifications.

## [9. network.info](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#9-networkinfo)

The `network.info` file contains network-related details of the MetaDefender Core server. This information is essential for diagnosing connectivity issues.

## [10. os.info](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#10-osinfo)

The `os.info` file includes details about the operating system on which MetaDefender Core is running. This data helps in identifying OS-related compatibility or configuration issues.

## [Conclusion](/docs/mdcore/v5.22.1/knowledge-base/what-is-included-in-the-metadefender-core-support-package-#conclusion)

The MetaDefender Core support package is a crucial resource for diagnosing and troubleshooting issues. When providing this package to OPSWAT support, ensure that all relevant folders and files are included to facilitate efficient issue resolution.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
