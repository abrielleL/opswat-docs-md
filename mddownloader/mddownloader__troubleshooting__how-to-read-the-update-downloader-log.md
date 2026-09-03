<!-- source: https://www.opswat.com/docs/mddownloader/troubleshooting/how-to-read-the-update-downloader-log -->

# How to read the Update Downloader log

The log files are plain text files that can be opened with any text editor.

## [Files](/docs/mddownloader/troubleshooting/how-to-read-the-update-downloader-log#files)

The Update Downloader generates a log file under **/var/log/ometadownloader** named ometadownloader.log.

## [Format](/docs/mddownloader/troubleshooting/how-to-read-the-update-downloader-log#format)

In the log, each line represents a log message sent by the server or agent. Depending on the log file, the format of the line is as follows:

log formatCopy[LEVEL] TIMESTAMP (COMPONENT) MESSAGE [msgid: MESSAGE ID]

Example:

log exampleCopy[INFO ] 2016.02.09 08:41:37.099: (common.update) Package successfully downloaded, packageDir='/tmp/downloader-data/updates/db/clamav_1_linux_2OMCap' [msgid: 671

Where the different values are:

- **LEVEL** : the severity of the message
- **TIMESTAMP** : The date value when the log entry was sent
- **COMPONENT** : which component sent the entry
- **MESSAGE** : the verbose string of the entry's message
- **MESSAGE ID** : the unique ID of this log entry

## [Severity levels of log entries](/docs/mddownloader/troubleshooting/how-to-read-the-update-downloader-log#severity-levels-of-log-entries)

Depending on the reason for the log entry, there are different types of severity levels.

Based on the configuration, the following levels are possible:

- **DUMP** : The most verbose severity level, these entries are for debuggers only.
- **DEBUG** : Debuggers severity level, mostly used by support issues.
- **INFO** : Information from the software, such as scan results.
- **WARNING** : A problem occurred needs investigation and OPSWAT support must be contacted, however the product is supposed to be operational.
- **ERROR** : Software error happened, please contact support if the issue is persist. Software functionality may be downgraded in these cases.
