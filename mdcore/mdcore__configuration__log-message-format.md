<!-- source: https://www.opswat.com/docs/mdcore/configuration/log-message-format -->

# Log Message Format

## [Format](/docs/mdcore/configuration/log-message-format#format)

In the log, each line represents a log message sent by the server or node. Depending on the log file, the format of the line is as follows:

log formatCopy[LEVEL] TIMESTAMP (COMPONENT) MESSAGE [msgid: MESSAGE ID]

Example:

log exampleCopy[INFO] 2019.07.02 05:25:27.115: (core.workflow) Processing finished, node=':1076', user='LOCAL/admin', workflow_id='lms::workflow::WorkflowExecutor(0x214b02a8f60)', dataId='702a2230dd0d44de9bd773bccfe472a9', fileName='TermUtil.class', sha256sum='07aca175cc8a9f40819a47f6b5f809404bae8d31cf16e70d0a182c413ab39c98', blocked='false', blocked_reason='', overallResult='No Threat Detected', threatFoundCount='0', embeddedObjectsWithThreat='0', totalResultCount='3', threatDetectedBy='', threatName='', ruleName='File process', source='::1' [msgid: 82]

Where the different values are:

- **LEVEL** : the severity of the message
- **TIMESTAMP** : The date value when the log entry was sent
- **COMPONENT** : which component sent the entry
- **MESSAGE** : the verbose string of the entry's message
- **MESSAGE ID** : the unique ID of this log entry - Learn more at [Error Message Description Table](/docs/mdcore/configuration/error-message-description-table)

## [Severity levels of log entries](/docs/mdcore/configuration/log-message-format#severity-levels-of-log-entries)

Depending on the reason for the log entry, there are different types of severity levels.

Based on the configuration, the following levels are possible:

- **DEBUG** : Debuggers severity level, mostly used by support issues.
- **INFO** : Information from the software, such as scan results.
- **Extended INFO:** Like `INFO` level but having more information about every (engine) stage
- **WARNING** : An unexpected event occurred; however, the product is supposed to be operational.
- **ERROR** : Software error happened, please contact support if the issue persists. Software functionality may be downgraded in these cases.

Log Levels recommendation

- In most cases, the **INFO** log level is sufficient for general system monitoring and troubleshooting. It provides the essential information needed to observe normal operations without generating excessive log data.
- The **Extended INFO** log level is useful when users need detailed traceability of each processing stage within the engine. This level records additional events, such as which engine step a file is currently being processed at. Please note that enabling **Extended INFO** will increase log volume and file size compared to the standard **INFO** level.
- The **DEBUG** log level should only be enabled when investigating issues or under the guidance of OPSWAT Support. Once enabled, users can collect the logs and provide them to OPSWAT for analysis. This level produces a significant amount of log data, which can increase storage usage and negatively impact system performance. Therefore, it is **not recommended for regular production use**.
