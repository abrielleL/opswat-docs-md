<!-- source: https://www.opswat.com/docs/cm/knowledge-base/where-are-the-install-directories-for-my-opswat-central-manageme -->

# Where are the install directories for My OPSWAT Central Management v10?

> **Check Your Version:**
>
> This article applies to all OCMv10 releases deployed on Windows and Linux systems.
>
> The default locations are listed below.

## **Windows:**

**“C:\Program Files\OPSWAT\MOCM”** - Main installation directory containing the application used to generate support packages, along with other required startup components.

**“C:\Program Files\OPSWAT\MOCM\apps”** - Contains connected applications such as *MetaDefender Core* and *MetaDefender ICAP*, required for system operation and connectivity. This directory also includes the license application and built-in configuration files.

**“C:\Program Files\OPSWAT\MOCM\cm-storage”** - Folders related to connected services such as “mdcore” to hold files temporarily.

**“C:\Program Files\OPSWAT\MOCM\data-agent”** - Folders containing data related to fusion-updater, mdcore, mdfusion-vpack, opswat-gears-on-premise-fusion-files, security controls

**“C:\Program Files\OPSWAT\MOCM\erlang”** - Binaries and library files necessary for startup and functionality

**“C:\Program Files\OPSWAT\MOCM\garnet”** - Garnet and Service configuration, dll, application files necessary for startup and functionality.

**“C:\Program Files\OPSWAT\MOCM\init-data”** - Includes the `mdd_inventory`, `mem`, and `pmp_device` folders, which contain JSON files required for service functionality.

**“C:\Program Files\OPSWAT\MOCM\java”**- Java-related binaries and libraries.

**“C:\Program Files\OPSWAT\MOCM\keystore”** - Keystore for certificates and passphrases

**“C:\Program Files\OPSWAT\MOCM\mongodb-cm”** - Database related files that are necessary for functionality.

**“C:\Program Files\OPSWAT\MOCM\mongodb-tools”** - Database utility tools.

**“C:\Program Files\OPSWAT\MOCM\mongosh”** - Database binaries and scripts

**“C:\Program Files\OPSWAT\MOCM\nginx”** - Web management files and logs files for the ability to access the application on the browser

**“C:\Program Files\OPSWAT\MOCM\rabbitmq”** - RabbitMQ application files required for messaging, database operations, and logging.

**“C:\Program Files\OPSWAT\MOCM\tomcat”** - Logs for technical support along with binaries, temp, and library files that are necessary for application functionality.

**“C:\ProgramData\OPSWAT\MOCM”** - Stores log files and a required `do-not-delete.tmp` file.

## Linux:

**“/opt/mocm”** - Main installation folder containing necessary applications for startup.

**“/opt/mocm/apps”** - Directory containing connected applications such as MetaDefender Core, MetaDefender ICAP needed for these systems to run and connect, along with license application, and built-in configuration files.

**“/opt/mocm/cm-storage”** - Folders related to connected services such as “mdcore” to hold files temporarily.

**“/opt/mocm/etc”** - port configuration property file

**“/opt/mocm/jre”** - Java runtime files

**“/opt/mocm/logrotate”** - reddis and NGINX logs

**“/opt/mocm/mongosh”** - Database shell, used to connect to the database

**“/opt/mocm/nginx”** - Web management configuration files to access the console via the browser

**“opt/mocm/redis”** - Redis configuration file

**“/opt/mocm/systemd-service”** - service files that are necessary for application startup and functionality

**“/opt/mocm/archive”** - stored backup archive files for data

**“/opt/mocm/data-agent”** - Folders containing data related to fusion-updater, mdcore, mdfusion-vpack, opswat-gears-on-premise-fusion-files, security controls

**“/opt/mocm/init-data”** - directory containing mdd_inventory, mem, and pmp_device containing JSON files necessary for service functionality.

**“/opt/mocm/lib”** - directory containing the script to generate a support package, and other related script tools [change web port, enable/disable TLS, etc].

**“/opt/mocm/mongodb”** - Database related files that are necessary for functionality.

**“/opt/mocm/mongo-tools”** - Binaries and database tools

**“/opt/mocm/rabbitmq”** - rabbitmq configuration file

**“/opt/mocm/tomcat”** - Binaries, configuration files, libraries, logs, temporary, and web application files necessary for application functionality.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
