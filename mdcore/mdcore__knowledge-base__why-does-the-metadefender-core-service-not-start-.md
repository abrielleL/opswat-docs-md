<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-the-metadefender-core-service-not-start- -->

# Why does the MetaDefender Core service not start?

This article applies to all MetaDefender Core version 5.0 and newer releases deployed on Windows and Linux systems.

**MetaDefender Core Service Fails to Start (Windows & Linux)**

If the MetaDefender Core service fails to start, it may be due to a variety of system or configuration-related issues. This article outlines common causes and troubleshooting steps for both **Windows** and **Linux** environments.

🚦 **Symptoms**

- MetaDefender Core does not start after installation or reboot.
- The service is visible but stuck in a "Starting" or "Stopped" state.
- Log files show initialization errors.
- The web UI is unreachable on the configured port.

🛠️ **Troubleshooting Steps**

1. ✅ **Check Service Status**

**Windows:**

- Open **Services (services.msc)**.
- Locate **MetaDefender Core**.
- Right-click → **Start** (or Restart).
- If the service does not start, check the **Windows Event Viewer** and the logs located at: C:\Program Files\OPSWAT\MetaDefender Core\data\logs\Core.log

**Linux**:

- Run the following command:

sudo systemctl status ometascan

- Check logs using:

sudo journalctl -u ometascan

tail /var/log/ometascan/ometascan.log

2. **Configuration issues**

**Registry Issues (Windows)**

If the Windows registry was manually edited or configured incorrectly, the service may fail to start.

**Resolution**:

- Whenever changing the configuration in the registry, please make sure that the key names and the values are according to the documentation found in the link below: [MetaDefender Configuration](/docs/mdcore/configuration/metadefender-configuration#windows)
- Any typos or wrong configuration may prevent the service start
- If edits were made, restore from backup or compare the registry under:

HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan

- Ensure values such as InstallationFolder, loglevel, and other critical keys are valid.
- Check for any typo’s in the keys names or values
- Be careful for Keys dependencies, such as when syslog is configured, syslog_level is also required, or when nginx_logfile is configured, nginx_log_rotation is also required.
- The rest port is configured on a free port. If the port is in use by a different application, the service might fail as well.

**Configuration (Linux)**

If the MetaDefender Core configuration was manually edited or configured incorrectly, the service may fail to start. The configuration file for the server is located in /etc/ometascan/ometascan.conf

**Resolution**:

- Whenever changing the configuration in the ometascan.conf, please make sure that the names and the values are according to the documentation found in the link below: [MetaDefender Configuration](/docs/mdcore/configuration/metadefender-configuration#linux)
- Any typos or wrong configuration may prevent the service to start
- If edits were made, restore from backup or compare the configuration file ometascan.conf
- Check for any typo’s in the names or values
- Be careful for Keys dependencies, such as when syslog is configured, syslog_level is also required, or when nginx_logfile is configured, nginx_log_rotation is also required.
- The rest port is configured on a free port. If the port is in use by a different application, the service might fail as well.

3. 🔐 **SSL Certificate or Key Issues**

MetaDefender Core may be configured to use SSL. If the certificate or private key path is invalid or the files are missing, the service will not start.

**Common errors:**

- File not found
- Permission denied
- Invalid certificate format

⚠️ For production deployments, ensure the certificate is valid and trusted.

**Solution:**

**For Windows:**

Please navigate to the MetaDefender Core installation folder, by default: C:\Program Files\OPSWAT\MetaDefender Core and run the ometascan-reset-ssl-conf.exe tool **as Administrator** to disable the SSL configuration.

**For Linux:**

Please run the script /usr/sbin/ometascan-reset-ssl-conf **with root privileges**

Once done, please try starting the service again.

4. 🗂️ **Temporary Folder Not Accessible**

MetaDefender Core relies on a configured temporary folder for file processing. If this directory is misconfigured or inaccessible, the service will fail.

**Error message:**

[ERROR ] <timestamp>: (common.base) Error in Service, shutdown.., error='Extension setting up failed: extension: 'ekm', **rc: '-612'**, error: ''' [msgid: 8]

**Default paths:**

- **Windows**: C:\Program Files\OPSWAT\MetaDefender Core\data\resources\
- **Linux**: /var/tmp/ometascan/resources

**Solution**

**Windows**:

First of all, please check the mentioned at point 2 regarding the current path for the Resources folder. If no entry is configured, then the default location will be in the MetaDefender Core installation Folder\data\resources

Please check the folder permissions:

System group should have full permissions.

If the permissions are not configured as above, please configure the correct permissions and then try starting the service once again.

**Linux**:

First of all, please check the correct path configured at point 2 for the temporary folder. By default, this will be in the path /var/tmp/ometascan/resources and the permissions should be assigned to user metascan with the permissions mentioned below:

If the permissions are different, please use the commands below to set the correct permissions:

sudo chmod 755 /var/tmp/ometascan/resources

sudo chown metascan:metascan /var/tmp/ometascan/resources

5. **IPv6 is Disabled on the Linux System**

In some Linux systems, IPv6 maybe disabled or not supported, in which case startup will fail. The workaround is to force MetaDefender Core service to use IPv4.

For more details on this issue, please refer to [How to Resolve MetaDefender Core Service Start-up Failures on IPv6-Disabled Linux Systems?](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-resolve-metadefender-core-service-start-up-failures-on-ip)

📬 **Contacting Support**

If you are unable to resolve the issue, please collect the following information:

- Please create a support package using the steps provided in the below links:

  - [How to Create Support Package With Web Console](/docs/mdcore/troubleshooting/how-to-create-support-package-with-web-console)
  - [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
