<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/java-configuration -->

# Java Configuration

From version 7.22.0, a Java Runtime Environment distribution is bundled with OPSWAT Central Management. This Java distribution will be used by default.

The instructions below allow you to specify another Java distribution for OPSWAT Central Management.

Please note that if the user-provided Java distribution fails the validity check, OPSWAT Central Management will fall back to using the bundled Java distribution instead.

The Java installation used by OPSWAT Central Management can be changed by following the below guidelines:

## [On Windows:](/docs/ocm/7.39.0/configuration/java-configuration#on-windows)

1/ Locate the file ProgramData/OPSWAT/Central/config.properties.

2/ Add or modify the **java_path** variable to the desired value. For example:

java_path=C:\Program Files\Java\jre-17

3/ Restart OPSWAT Central Management via the tray icon.

## [On Linux:](/docs/ocm/7.39.0/configuration/java-configuration#on-linux)

1/ Locate the file **/usr/lib/ocm/ocm.service**

2/ Find the **EnvironmentFile** variable, which should point to the file used to set up OPSWAT Central Management's environment variables. Open this file.

3/ Add or modify either the JRE_HOME or JAVA_HOME variables.

You should use only one variable: JRE_HOME with a Java Runtime Environment(JRE) distribution or JAVA_HOME with a Java Development Kit (JDK) distribution. For example:

JRE_HOME=/home/admin/jre-17

4/ Restart OPSWAT Central Management via the command:

systemctl restart ocm
