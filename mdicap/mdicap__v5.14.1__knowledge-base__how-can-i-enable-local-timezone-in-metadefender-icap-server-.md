<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-can-i-enable-local-timezone-in-metadefender-icap-server- -->

# How can I Enable Local Timezone in MetaDefender ICAP Server?

#### [Using Local Timezone in MetaDefender ICAP Server Logs](/docs/mdicap/v5.14.1/knowledge-base/how-can-i-enable-local-timezone-in-metadefender-icap-server-#using-local-timezone-in-metadefender-icap-server-logs)

To configure the MetaDefender ICAP Server to use the server's local timezone for syslog messages, you need to adjust the registry settings on your Windows system. Follow the steps below.

#### [Steps to Enable Local Timezone in Syslog Logs](/docs/mdicap/v5.14.1/knowledge-base/how-can-i-enable-local-timezone-in-metadefender-icap-server-#steps-to-enable-local-timezone-in-syslog-logs)

1. Open the Windows Registry Editor:

   - Press Win + R, type regedit, and press Enter.
2. Navigate to the Logger Configuration Key:

   - Go to: HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP-Server\Logger
3. Modify or Create the `local_timezone` Value:

   - If the `local_timezone` entry exists, double-click it and set its value to `true`.
   - If it doesn't exist:

     - Right-click in the right pane, select New > String Value.
     - Name it `local_timezone`.
     - Double-click the new entry and set its value to `true`.
4. Restart the ICAP Server Service:

   - Open the Services console (services.msc).
   - Locate MetaDefender ICAP Server.
   - Right-click and select Restart.

After completing these steps, the ICAP Server will log syslog messages using the server's local timezone.

**For more details, refer to the official documentation:** [**HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger**](/docs/mdicap/v5.14.1/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverlogger)
