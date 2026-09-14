<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-resolve-metadefender-core-service-start-up-failures-on-ip -->

# How to Resolve MetaDefender Core Service Start-up Failures on IPv6-Disabled Linux Systems?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Linux systems.

**Issue**: MetaDefender Core services fail to initialize on Linux systems that lack IPv6 support. Symptoms include unresponsive services and an inaccessible MetaDefender Core dashboard.

**Cause**: The underlying web server (typically Nginx) attempts to access both IPv4 and IPv6 addresses when the 'restaddress' configuration in the 'ometascan.conf' file is set to '*'. If the Linux system lacks IPv6 support or an IPv6 IP address, Nginx fails to start. The error messages in the 'ometascan.log' and 'nginx-ometascan.log' logs reflect this failure.

Here are the associated log entries indicating such errors:

ometascan.logCopy[ERROR ] 2023.07.12 07:48:01.781: (common.base) Error in Metadefender Core service, shutdown.., error='REST frontend stopped, exitCode: '1'' [msgid: 131]
[INFO ] 2023.07.12 07:48:01.813: (core.postgres) Postgres info, info='systemctl stop ometascan-pg', param='' [msgid: 4085]
[ERROR ] 2023.07.12 07:48:01.932: (common.base) Exception has been caught, message='REST frontend stopped, exitCode: '1'' [msgid: 833]nginx-ometascan.logCopy2023/07/12 07:49:07 [emerg] 9677#0: socket() [::]:8008 failed (97: Address family not supported by protocol)

Solution:

1. Open a terminal or SSH into your Linux system.
2. Go to the directory where the MetaDefender Core configuration file is located (/etc/ometascan/ometascan.conf).
3. Open the 'ometascan.conf' file with a text editor (e.g., vi or nano).
4. Find the line that specifies the 'restaddress' configuration (it is usually set to 'restaddress=*').
5. Change the 'restaddress' line to 'restaddress=0.0.0.0'. This action forces the MetaDefender Core services to listen on any IPv4 address set up on the server.
6. Save the changes to the 'ometascan.conf' file and close the text editor.
7. Restart the MetaDefender Core services to apply the configuration changes using the command: 'sudo systemctl restart ometascan'.
8. Confirm the successful operation of the MetaDefender Core services by checking their status with the command: 'sudo systemctl status ometascan'.

By altering the 'restaddress' line to '0.0.0.0' in the 'ometascan.conf' file, the MetaDefender Core services are set to listen on any available IPv4 address on the server. This action ensures that the services can start successfully even on Linux systems without IPv6 support.

If the issue persists or if you have further concerns, please refer to the MetaDefender Core documentation or reach out to OPSWAT support for assistance.

Support:

To contact us, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
