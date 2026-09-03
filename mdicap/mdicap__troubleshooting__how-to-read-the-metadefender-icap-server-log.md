<!-- source: https://www.opswat.com/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log -->

# How to read the MetaDefender ICAP Server log

- [Linux](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#linux)

  - [Files](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#files)
  - [Format](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#format)
  - [Severity levels of log entries](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#severity-levels-of-log-entries)
- [Windows](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#windows)

## [Linux](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#linux)

The log files are plain text files that can be opened with any text editor.

## [Files](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#files)

The MetaDefender ICAP Server generates a log file under **/var/log/mdicapsrv** named mdicapsrv.log.

## [Format](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#format)

In the log, each line represents a log message sent by the server. Depending on the log file, the format of the line is as follows:

[LEVEL] TIMESTAMP (COMPONENT) MESSAGE [msgid: MESSAGE ID]

Example:

[INFO ] 2016.02.09 08:41:37.099: (common.update) Package successfully downloaded, packageDir='/tmp/downloader-data/updates/db/clamav_1_linux_2OMCap' [msgid: 671

Where the different values are:

- **LEVEL** : the severity of the message
- **TIMESTAMP** : The date value when the log entry was sent
- **COMPONENT** : which component sent the entry
- **MESSAGE** : the verbose string of the entry's message
- **MESSAGE** **ID** : the unique ID of this log entry

## [Severity levels of log entries](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#severity-levels-of-log-entries)

Depending on the reason for the log entry, there are different types of severity levels.

Based on the configuration, the following levels are possible:

- **DUMP** : The most verbose severity level, these entries are for debuggers only.
- **DEBUG** : Debuggers severity level, mostly used by support issues.
- **INFO** : Information from the software, such as scan results.
- **WARNING** : A problem occurred needs investigation and OPSWAT support must be contacted, however the product is supposed to be operational.
- **ERROR** : Software error happened, please contact support if the issue is persist. Software functionality may be downgraded in these cases.

## [Windows](/docs/mdicap/troubleshooting/how-to-read-the-metadefender-icap-server-log#windows)

On Windows systems logging is done via Event Log.

MetaDefender ICAP Server logs can be found under Windows Logs / Application and are labelled with *Metadefender ICAP* source.
