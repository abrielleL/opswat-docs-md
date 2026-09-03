<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/where-are-metadefender-core-install-directories-and-advanced-con -->

# Where are MetaDefender Core Install Directories and Advanced Configurations?

This article applies to all MetaDefender Core V5 releases deployed on Windows or Linux systems.

## [Windows](/docs/mdcore/v5.21.0/knowledge-base/where-are-metadefender-core-install-directories-and-advanced-con#windows)

By default, the following are the directories used when MetaDefender Core is installed:

| **Directory** | **Content** |
| --- | --- |
| C:\Program Files\OPSWAT\MetaDefender Core | Main installation folder where tools and support package script are found. |
| C:\Program Files\OPSWAT\MetaDefender Core ginx | Web management files and logs files for the ability to access MetaDefender core on the browser. |
| C:\Program Files\OPSWAT\MetaDefender Core\data\resources | Engine folders that store temporary files during scanning, files are deleted once the scan is complete. |
| C:\Program Files\OPSWAT\MetaDefender Core\data\updates\av  C:\Program Files\OPSWAT\MetaDefender Core\data\updates\db | Folders [av] [db] containing the engines database update packages [zip] and instruction YML file. |
| C:\Program Files\OPSWAT\MetaDefender Core\data\logs | Folder containing rotating core logs and upgrade log. |
| C:\Program Files\OPSWAT\MetaDefender Core\data\engines | Folder containing loaded engines and their necessary components to complete scanning. |
| C:\Program Files\OPSWAT\MetaDefender Core\data\enginelogs | Logs for each engine produced during scans. |
| C:\Program Files\OPSWAT\MetaDefender Core\data\pg_data | Postgres Database files and logs (only for local DB). |
| C:\Program Files\OPSWAT\MetaDefender Core\postgres | Libraires and executables for the local database. |

[Additional configuration](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#windows) located in this Registry path:

HtmlCopyComputer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan
## [Linux](/docs/mdcore/v5.21.0/knowledge-base/where-are-metadefender-core-install-directories-and-advanced-con#linux)

By default, the following are the directories used when MetaDefender Core is installed:

| **Directory** | **Directory** |
| --- | --- |
| /var/lib/ometascan | Main installation folder where tools and support package script are found. |
| /etc/ometascan  /etc/ometascan/nginx.d | Folder containing configuration files for Core and web server. |
| /var/run/ometascan | Folder containing runtime variable files for Core services. |
| /var/tmp/ometascan/resources | Engine folders that store temporary files during scanning, files are deleted once the scan is complete. |
| /var/lib/ometascan/updates/av  /var/lib/ometascan/updates/db | Folders [av] [db] containing the engines database update packages [zip] and instruction .YML file. |
| /var/log/ometascan | Folder containing rotating core logs, upgrade log, and web server logs. |
| /var/lib/ometascan/engines | Folder containing loaded engines and their necessary components to complete scanning. |
| /var/log/ometascan/enginelogs | Logs for each engine produced during scans. |
| /var/lib/ometascan/pg_data | Postgres Database files and logs (only for local DB). |
| /usr/lib/ometascan/postgres/bin  /usr/lib/ometascan/postgres/lib | Libraires and executables for the local database. |

[Additional configuration](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#linux) is located in this file:

HtmlCopy/etc/ometascan/ometascan.confSupport:

If you have followed through this article but are still unable to locate **MetaDefender Core Install Directories and Advanced Configurations**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
