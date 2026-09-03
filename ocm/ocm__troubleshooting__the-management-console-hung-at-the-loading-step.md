<!-- source: https://www.opswat.com/docs/ocm/troubleshooting/the-management-console-hung-at-the-loading-step -->

# The management console hung at the loading step

| Term | Detail |
| --- | --- |
| Problem | The management console hung at the loading step for more than 5 mins. |
| Cause | The loading page is not redirected properly due to one of the following issues   - Missing Visual C++ Redistributable Packages for Visual Studio 2013 - Java environment variable is not defined correctly |
| Troubleshooting | Refresh the page. Check the tomcat log file. The log should report certain errors. |
| Solution | - Install Visual C++ Redistributable Packages for Visual Studio 2013 - Install JRE 11 and set the JRE_HOME system environment variable to the JRE's installation path. |

If the loading step hangs for more than 5 minutes, please first try refreshing the page.

If the problem persists, please check the tomcat log file.

- On Windows, in C:\ProgramData\OPSWAT\Central\Logs, check catalina_out<timestamp>.txt and catalina_error<timestamp>.txt on Windows.
- On Linux, /var/log/ocm/catalina<timestamp>.out.

There should be some error messages.

### [Missing Visual C++ Redistributable Packages for Visual Studio 2013](/docs/ocm/troubleshooting/the-management-console-hung-at-the-loading-step#missing-visual-c-redistributable-packages-for-visual-studio-2013)

In order to fix this error, as noted in [Software Requirement](/docs/ocm/installation/recommended-system-requirements#software-requirement), please install the Visual C++ Redistributable Packages for Visual Studio 2013. Then restart OPSWAT Central Management.

### [Java environment variable is not defined correctly](/docs/ocm/troubleshooting/the-management-console-hung-at-the-loading-step#java-environment-variable-is-not-defined-correctly)

In order to fix this error, please install JRE or JDK version 11 and set either the JRE_HOME or JAVA_HOME environment variables to the correct installation path. Restart OPSWAT Central Management service for the changes to take effect. Please refer to the [Java configuration guideline](/docs/ocm/configuration/java-configuration) for more detail on setting up the environment variables.
