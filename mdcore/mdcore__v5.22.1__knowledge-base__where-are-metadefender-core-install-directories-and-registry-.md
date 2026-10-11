<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/where-are-metadefender-core-install-directories-and-registry- -->

# Where are MetaDefender Core Install Directories and Registry?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

## [File Explorer:](/docs/mdcore/v5.22.1/knowledge-base/where-are-metadefender-core-install-directories-and-registry-#file-explorer)

By default, the following are the directories and use when MetaDefender Core is installed

- **“C:\Program Files\OPSWAT\MetaDefender Core”** - Main installation folder where tools and support package script are found.
- **"C:\Program Files\OPSWAT\MetaDefender Core\nginx"** - Web management files and logs files for the ability to access MetaDefender core on the browser
- **"C:\Program Files\OPSWAT\MetaDefender Core\data\resources" -** engine folders that store temporary files during scanning, files are deleted once the scan is complete
- "**C:\Program Files\OPSWAT\MetaDefender Core\data\updates**" - Folders [av] [db] containing the engines database update packages [zip] and instruction .YML file
- "**C:\Program Files\OPSWAT\MetaDefender Core\data\logs**" - Folder containing rotating core logs and upgrade log.
- "**C:\Program Files\OPSWAT\MetaDefender Core\data\engines**" - Folder containing loaded engines and their necessary components to complete scanning.
- **“C:\Program Files\OPSWAT\MetaDefender Core\data\enginelogs”** - Logs for each engine produced during scans
- **"C:\Program Files\OPSWAT\MetaDefender Core\data\pg_data"** - Postgres Database files and logs [only for local DB]
- **"C:\Program Files\OPSWAT\MetaDefender Core\postgres" -** Libraires and executables for the local database

## [Registry](/docs/mdcore/v5.22.1/knowledge-base/where-are-metadefender-core-install-directories-and-registry-#registry)

Computer\HKEY_CURRENT_USER\Software\OPSWAT\MetaDefender Core
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MetascanSupport:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
