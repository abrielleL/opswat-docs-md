<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-to-send-specific-log-entries-to-syslog-integration- -->

# How to send specific log entries to syslog integration?

This article applies to all MetaDefender ICAP version 5.0 and newer releases deployed on Windows and Linux systems.

**Introduction:**

This knowledge base article provides a way to filter specific MSGID’s and their urgency level based on the Syslog configured level.

**Details:**

There are situations where the syslog integration needs to be configured to filter the log entries shared and to leverage only specific log entries that the customer is interested in. This allows the customer to avoid sending unwanted logs to syslog integration.

For example, if we want to only view the errors in the syslog integration but at the same time, we are interested in the scan results to see if there are any infections or issues with scanning, we can configure the syslog integration using the error log level but how do we add log entries that have information log level?

By configuring the override function, we can configure specific msgid’s log level from information to error.

[INFO] 2025.05.29 10:51:27.810: (icap.communication) TCP Connection... [msgid: 3679]

After the change is implemented:

[ERROR]2025.05.29 10:53:27.857: (icap.communication) TCP Connection...[msgid: 3679]

To make the above change please follow the instructions below for each OS:

1. **Windows:**

Please open the regedit and navigate to

HKEY_LOCAL_ MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger

Create a new string value (REG_SZ) named “override” and enter all the msgid’s followed by the new log level and then add a comma to add a new value. Please see example below:

2. **Linux**

Please edit the configuration file /etc/mdicapsrv/mdicapsrv.conf in the logger section as follows:

Please navigate to the [logger] section and add the “override” entry and enter all the msgid’s followed by the new log level and then add a comma to add a new value. Please see example below:

The override option changes the log level for both syslog integration and the log information.

After the changes are made, please restart the services to implement the changes.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
