<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/unable-to-access-opswat-central-management-console-due-to-corrup -->

# Unable to access OPSWAT Central Management console due to corrupted web application files

| Term | Detail |
| --- | --- |
| Problem | Cannot access OPSWAT Central Management console |
| Cause | One or more web application packages were not unpacked properly during startup. |
| Troubleshooting | Accessing the dashboard at <server address>/console redirects to an error page. |
| Solution | Manually trigger the unpacking process. |

After installing OPSWAT Central Management, the web application packages may rarely fail to be unpacked properly, causing a situation where the service status is detected as running but the console cannot be accessed. This can happen if the startup processed was interrupted abruptly then restarted.

In that case, accessing the dashboard will redirect the browser to an error page, as in the image below.

In order to fix this problem, please manually trigger the unpack process by following the steps described below:

1. Stop the OPSWAT Central Management service.
2. Navigate to the web application folder:

   - On Windows systems, it is located at Program Files\OPSWAT\Central\tomcat\webapps
   - On Linux systems, it is located at /opt/ocm/tomcat/webapps
3. Delete the folders **console**, **files**, **gears**, **nac**, **o** and **scheduler.**
4. Restart the OPSWAT Central Management service.
