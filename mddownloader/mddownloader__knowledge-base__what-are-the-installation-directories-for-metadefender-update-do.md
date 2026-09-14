<!-- source: https://www.opswat.com/docs/mddownloader/knowledge-base/what-are-the-installation-directories-for-metadefender-update-do -->

# What are the installation directories for MetaDefender Update Downloader?

This article applies to all MetaDefender Update Downloader releases deployed on Windows and Linux systems.

Below lists the default installation directories for Windows and Linux

## [Windows](/docs/mddownloader/knowledge-base/what-are-the-installation-directories-for-metadefender-update-do#windows)

| **Location** | **Path** | **Description** |
| --- | --- | --- |
| Registry | 1. Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadownloader 2. Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadownloader\globa 3. Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadownloader\logger | 1. String: “Installation Folder” path 2. Strings: “restaddress” and “restport” 3. String: “wineventlog_level” |
| File Explorer | 1. C:\Program Files\OPSWAT\Metadefender Update Downloader 2. C:\Program Files\OPSWAT\Metadefender Update Downloader\data 3. C:\Program Files\OPSWAT\Metadefender Update Downloader\nginx 4. C:\Program Files\OPSWAT\Metadefender Update Downloader\sqldrivers 5. C:\Program Files\OPSWAT\Metadefender Update Downloader\tls | 1. Main installation path containing files and sub directories for application functionality. 2. Directories: update_packages, updates. Where the metascan engine and database packages are stored locally. Files: auditlog.sqlite, config.db.sqlite, config.db.sqlite.key 3. Website functionality files and directories. HTML, resource. 4. Database required dll files 5. TLS required file for HTTPS connection. |

## [Linux](/docs/mddownloader/knowledge-base/what-are-the-installation-directories-for-metadefender-update-do#linux)

| **Directory Path** | **Description** |
| --- | --- |
| /etc/default/ometadownloader | Environment variables for proxy |
| /etc/init.d/ometadownloader | Script for ometadownloader service start |
| /etc/logrotate.d/ometadownloader | How often logs rotate for ometadownloader.log and nginx-ometadownloader.log |
| /etc/ometadownloader/ometadownloader.conf | Configuration file for rest port, and log directories |
| /usr/bin | Script for collecting support package: ometadownloader-collect-support-data.sh  Script for watchdog: ometadownloader-watchdog.sh |
| /usr/lib/ometadownloader | Library files  Directories: lib, resources, plugins [SQL database, drivers, TLS] |
| /usr/lib/systemd/system | Ometadownloader.service |
| /usr/sbin | Directories: ometadownloader, ometadownloader-strip-configdb, ometadownloader-upgrade-db |
| /usr/share/doc/ometadownloader/copyright | Copyright file |
| /usr/share/man/man1 | Ometadownloader.1.gz |
| /usr/share/ometadownloader | Ometadownloader.conf - Global configuration for rest port and rest address. Log configuration on where to store log files |
| /var/lib/ometadownloader | Auditlog.sqlite, config.db.sqlite  Directories: html, update_packages, updates. Where core engine update database and engine packages store locally. |
| /var/lib/ometadownloader/html | HTML, CSS for website funtionality |
| /var/log/ometadownloader | ometadownloader.log  Log file for troubleshooting |

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
