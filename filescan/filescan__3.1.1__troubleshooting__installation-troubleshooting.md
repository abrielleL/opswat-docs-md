<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/installation-troubleshooting -->

# Installation troubleshooting

In case any issues arise after installation please check the logs. The most important places where logs are shown are accessed with the the following commands (try to look for lines beginning with [ERROR]):

BashCopysudo service sandbox status
sblog
sblog --broker
sudo docker logs webservice
## [Webservice is unavailable / under maintenance](/docs/filescan/3.1.1/troubleshooting/installation-troubleshooting#webservice-is-unavailable--under-maintenance)

This may happen from time to time, if there is an issue with unhealthy docker containers. Please restart Sandbox using the helper scripts:

BashCopysudo /home/sandbox/sandbox/stop_sandbox.sh
sudo /home/sandbox/sandbox/start_sandbox.sh
# Or use the system service (does not produce output)
sudo service sandbox restart
## ["Unfortunately, the application server "app*" is not reachable"](/docs/filescan/3.1.1/troubleshooting/installation-troubleshooting#unfortunately-the-application-server-app-is-not-reachable)

The issue is that the analyzer app (transform) is unable to start up or it is not accessible by the broker.

It is recommended to stop and restart the sandbox service. Then wait a minute or so until the connection is established between broker and transform. If the issue persists after several minutes, please check deeper into logs.

BashCopysudo /home/sandbox/sandbox/stop_sandbox.sh
sudo /home/sandbox/sandbox/start_sandbox.sh
sblog --broker
## [General issues related to file permissions](/docs/filescan/3.1.1/troubleshooting/installation-troubleshooting#general-issues-related-to-file-permissions)

Please investigate whether the folder mentioned in the error message is owned by the `sandbox` user.

This can be done using the `ls -la <path>` command. In case it is not owned by that user, recursively own it with the following command:

BashCopycd <parent path>
chown -R sandbox:sandbox <folder name>
## [Issues related to the APT package manager](/docs/filescan/3.1.1/troubleshooting/installation-troubleshooting#issues-related-to-the-apt-package-manager)

When the installer fails to install a required package via APT, you might see a similar error message indicating that the package manager is locked by another process that is running in the background:

BashCopyReading package lists...
E: Could not get lock /var/lib/dpkg/lock-frontend. It is held by process 18943 (apt-get)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend),is another process using it?
[FATAL] Failed to install XYZ package
OR:
[FATAL] Failed to prepare apt for docker installation

In this case, it is recommended to wait a few minutes while that other process finishes and releases the lock.

Feel free to check the status of that background process using `top` , `htop` or any similar utility.

If the process PID is also displayed in the error message (e.g. 18943 above), then the following command shows the status of the given process:

BashCopysudo ps aux | grep 18943
OR
sudo ps aux | grep apt

Please restart the Sandbox installation after the background process is completed.

If that does not help, please reboot the system and try again!

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
