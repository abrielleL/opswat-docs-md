<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/how-to-read-the-metadefender-core-log- -->

# How to Read the Metadefender Core Log?

The log files are plain text files that can be opened with any text editor.

## [Files](/docs/mdcore/v5.22.0/troubleshooting/how-to-read-the-metadefender-core-log-#files)

Under Linux the server and nodes generate separate log files under **/var/log/ometascan**. The **ometascan.log** file (if present) belongs to MetaDefender Core server.

Under Windows there is no default logging into file unless otherwise specified. For details see [MetaDefender Configuration](/docs/mdcore/v5.22.0/configuration/metadefender-configuration).

## [Format](/docs/mdcore/v5.22.0/troubleshooting/how-to-read-the-metadefender-core-log-#format)

In the log, each line represents a log message sent by the server or node. Depending on the log file, the format of the line is as follows:

[LEVEL] TIMESTAMP (COMPONENT) MESSAGE [msgid: MESSAGE ID]

Example:

[INFO ] 2015.08.19 09:40:27.941: (core.workflow) Scan finished, dataId='c35a190681944380a52efb9ef32ef509', overallResult='No Threat Detected', totalResultCount='5', infectedResultCount='0' [msgid: 82]

Where the different values are:

- **LEVEL** : the severity of the message
- **TIMESTAMP** : The date value when the log entry was sent
- **COMPONENT** : which component sent the entry
- **MESSAGE** : the verbose string of the entry's message
- **MESSAGE ID** : the unique ID of this log entry

## [Severity levels of log entries](/docs/mdcore/v5.22.0/troubleshooting/how-to-read-the-metadefender-core-log-#severity-levels-of-log-entries)

Depending on the reason for the log entry, there are different types of severity levels.

Based on the configuration, the following levels are possible:

- **DEBUG** : Debuggers severity level, mostly used by support issues.
- **INFO** : Information from the software, such as scan results.
- **WARNING** : A problem occurred needs investigation and OPSWAT support must be contacted, however the product is supposed to be operational.
- **ERROR** : Software error happened, please contact support if the issue is persist. Software functionality may be downgraded in these cases.
