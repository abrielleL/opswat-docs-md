<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/failed-to-remote-install-opswat-products -->

# Failed to remote install OPSWAT Products

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Term | Detail |
| --- | --- |
| Problem | Failed to remote install OPSWAT Products |
| Cause | OPSWAT Central Management was unable to open a SSH connection. The target machine did not satisfy the system requirements of the OPSWAT Product that was being installed. |
| Troubleshooting | Check log in gears_product_service.log file. Look for the newest version of the message **"Testing connection to <target machine>".** |
| Solution | Ensure that the target machine has enabled OpenSSH server and can satisfy the system requirements of the OPSWAT Product. |

After starting the remote installation, the new OPSWAT Product's entry in the corresponding management page shows the **Disconnected** status.

Please check the file gears_product_service.log in the folder "C:\Program Files\OPSWAT\Central\tomcat\logs".

Look for the section that starts with **"Testing connection to <target machine>"** to find the remote installation's error message. If the log includes the line **"Install failed"**, a possible cause is that the target machine did not satisfy the OPSWAT Product's system requirements. Please ensure that the target machine does meet the system requirements and try again.

If the log has one or more error messages **"ExitStatus: 1"** instead of **"ExitStatus: 0"**, it is possible that OpenSSH server has not been enabled correctly on the target machine. Please refer to [Remote Install OPSWAT Products](/docs/ocm/7.39.0/operating/remote-install-opswat-products) to correct its configuration.
