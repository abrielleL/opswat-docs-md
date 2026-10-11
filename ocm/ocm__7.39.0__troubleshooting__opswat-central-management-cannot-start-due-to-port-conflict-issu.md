<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/opswat-central-management-cannot-start-due-to-port-conflict-issu -->

# OPSWAT Central Management cannot start due to port conflict issues

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Term | Detail |
| --- | --- |
| Problem | OPSWAT Central Management cannot start due to port conflict issues |
| Cause | One or more ports used by OPSWAT Central Management are already in use. |
| Troubleshooting | (On Windows) The tray icon reports a port conflict issues via notification Port conflict is reported in log files |
| Solution | Close the program occupying the conflicted ports Change the ports OPSWAT Central Management uses |

As of version 7.10, by default, OPSWAT Central Management requires ports 9000, 9005, 9009m 9026, and 27017 to be available.

On Windows, the tray icon can show a notification reporting possible port conflict issues when starting OPSWAT Central Management.

On all supported operating systems, port conflict issues are also reported in log files.

- Windows: ProgramData\OPSWAT/Central\Logs\powershell_out.txt
- Linux: /var/log/ocm/ocn_<current date>.log

One solution is to ensure that programs occupying the aforementioned ports are closed when starting OPSWAT Central Management.

A second solution is to change the ports OPSWAT Central Management uses as a workaround. Each port requires changing two configuration files. The first file is the main configuration which coordinates the services.

- On Windows, this file is located at ProgramData\OPSWAT\Central\config.properties.
- On Linux, this file is located at /usr/lib/ocm/set-port.sh.

The content should be similar to the below example:

tomcat_port=9009
mongo_port=27017
memcached_port=9005
nginx_port=9000
up_port=9026

Edit the port number as needed to solve the port conflicts.

The second configuration file to edit is listed below for each port.

**Tomcat port (9009 by default):**

- On Windows: Program Files\OPSWAT\Central\tomcat\conf\server.xml
- On Linux: /opt/ocm/tomcat/conf/server.xml

Find the configuration entry containing the current port used by Tomcat and edit it to match the main configuration file.

<Connector port="9009" protocol="HTTP/1.1"
connectionTimeout="20000" maxThreads="250" compression="on" URIEncoding="UTF-8"
redirectPort="9443" sendReasonPhrase="true"/>

**Mongodb port (27017 by default):**

- On Windows: ProgramData\OPSWAT\Central\mongod.conf
- On Linux: /opt/ocm/mongo/mongod.conf

Find the configuration entry containing the current port used by Mongodb and edit it to match the main configuration file.

net:
port: 27017

**Nginx port (9000)** Port 9000 is already supported to be configurable prior to version 7.10. [Please follow the guide here.](/docs/ocm/7.39.0/configuration/port-configuration)

**Up port (9026 by default):**

- On Windows: Program Files\OPSWAT\Central\nginx\conf\nginx.conf
- On Linux: /opt/ocm/nginx/conf/nginx.conf

Find the configuration entry containing the current port used to determine OPSWAT Central Management's status and edit it to match the main configuration file.

server {
listen 9026;Warning

Except for nginx port, port changes do not carry over across reinstallation/upgrade.
