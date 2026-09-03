<!-- source: https://www.opswat.com/docs/filescan/troubleshooting/collect-logfiles -->

# Collect logfiles

If you have some issue with your system, logs can help to find out what went wrong. You can collect `webservice` , `broker` and `transform` logs automatically using a helper script.

Navigate to the `/home/sandbox/sandbox` folder where you installed the product and locate the `collect_logs.sh` script. Make sure you have the correct rights to run the script.

Warning

If you are facing an ongoing issue and you would like to restart the webservice, it is highly recommended to run `collect_logs.sh` **before restarting the webservice!**

Otherwise the logs from the currently running Docker containers would be lost.

BashCopycd /home/sandbox/sandbox
sudo ./collect_logs.sh

The script might take a few minutes to complete and it will output some information about the collected log files, for example:

BashCopyCollecting MetaDefender Sandbox log files...
- Collected 40 log files from broker
- Collected 44 log files from transform
- Collected 2 log files from nginx
- Collected 1 log files from autorestart service
- Collected 14 log files from Docker containers
Success! Logs archived in /home/sandbox/sandbox/logs-230623_134130.zip
Exit...

The output shows the path to the ZIP file that contains the collected logs. Note that the file can be large (a few hundred megabytes).

Important!

This is only available from version 1.8.0

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
