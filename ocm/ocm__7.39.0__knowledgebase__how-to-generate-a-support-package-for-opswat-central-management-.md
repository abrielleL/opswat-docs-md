<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/how-to-generate-a-support-package-for-opswat-central-management- -->

# How to generate a support package for OPSWAT Central Management?

This article applies to all OPSWAT Central Management V7.25.0+ releases deployed on Windows or Linux systems.

A support package is a collection of log and configuration files which are used by the OPSWAT Support team when troubleshooting OPSWAT Central Management Issues.

A support package can be generated in either Windows or Linux systems, by following the relevant instructions below.

## [Windows](/docs/ocm/7.39.0/knowledgebase/how-to-generate-a-support-package-for-opswat-central-management-#windows)

1. Navigate to the **OPSWAT Central Management Installation Folder** (for example, **C:\Program Files\OPSWAT\Central**).

2. Double click on **generateSupportPackage.exe** or, if preferred, you can execute it in a **Command Prompt**.

3. The package will be generated in the format of **ocmSupport_<timestamp>.zip**, inside the installation folder, to be copied and forwarded to **OPSWAT Support**.

In cases where the support package generator is also unable to function properly, please follow the below instructions to manually collect the log files

1. Locate OPSWAT Central Management installation folder (default C:\Program Files\OPSWAT) and the System Drive (default C:)
2. Collect the following folders/files

   - <installation folder>\Central\nginx\conf folder
   - <installation folder>\Central\nginx\logs folder
   - <installation folder>\Central\tomcat\logs folder
   - <System Drive>\ProgramData\OPSWAT\Central\Logs folder
   - <System Drive>\ProgramData\OPSWAT\Central*.properties (all .properties files)
   - <System Drive>\ProgramData\OPSWAT\Central*.log (all .log files)

## [Linux - Red Hat Enterprise /Ubuntu](/docs/ocm/7.39.0/knowledgebase/how-to-generate-a-support-package-for-opswat-central-management-#linux---red-hat-enterprise-ubuntu)

1. Open a **Terminal** and navigate to **/usr/lib/ocm**.
2. Execute **generateSupportPackage.sh,** with Root privileges or, if needed, grant execute permission via chmod.
3. The package will be generated in the format of **ocmSupport_<timestamp.tar.gz**, inside the **/opt/ocm** folder.

In cases where the support package generator is also unable to function properly, please manually collect the following folders and files:

- /opt/ocm/nginx/conf folder
- /opt/ocm/nginx/logs folder
- /opt/ocm/tomcat/logs folder
- /etc/opt/ocm folder
- /var/log/ocm folder
- /usr/lib/ocm/set-port.sh file

Support:

After generating your package, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via the form method, uploading your OCM logs as prompted.

Warning

Depending on the total size of the OPSWAT Central Management server's log files. it may take a long time for the support package generation process to complete.
