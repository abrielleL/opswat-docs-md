<!-- source: https://www.opswat.com/docs/mdemail/operating/cef-syslog-message-format -->

# CEF log message format

MetaDefender Email Gateway Security supports sending log messages in CEF (Common Event Format) to local or remote syslog servers.

Common Event Format (CEF) is an extensible, text-based format designed to support multiple device types by offering the most relevant information. Message syntaxes are reduced to work with ESM normalization. CEF specifically defines a syntax for log records containing a standard header and a variable extension, formatted as key-value pairs.

CEF is a text-based log format developed by ArcSight™ and used by HP ArcSight™ products. It uses syslog as transport. The full format includes a syslog header or "prefix", a CEF "header", and a CEF "extension". The extension contains a list of key-value pairs. Standard key names are provided, and user-defined extensions can be used for additional key names. In some cases, the CEF format is used with the syslog header omitted.

[Syslog prefix] CEF:Version|Device Vendor|Device Product|Device Version|Device Event Class ID|Name|Severity|[Extension]

The following example shows a message received locally.

Jan 23 12:10:16 UTC egs-001 CEF:0|OPSWAT|MDEMAIL|5.7.4|email.workflow|Sending email|2|OMSemailId=681464 OMSuri=smtp://192.168.0.17:25 OMSrecipients=QList("karoly.arnhoffer@opswat.com") OMSuseTls=false OMSforceTls=false OMSmsgid=2407

The syslog prefix is in the following structure in the example:

[Timestamp] [Host]

The syslog prefix value is:

Jan 23 12:10:16 UTC egs-001

While the extension for the above example was:

OMSemailId=681464 OMSuri=smtp://192.168.0.17:25 OMSrecipients=QList("karoly.arnhoffer@opswat.com") OMSuseTls=false OMSforceTls=false OMSmsgid=2407

The following example shows the message received by a remote log server. Please note the additional syslog prefix added to the original local syslog prefix by the receiving syslog server.

127.0.0.1 55090 system Debug 0 0 -02-03T17:31:15Z LE11-D6100 CEF:0|OPSWAT|MDEMAIL|5.7.5|common.workflow|Executing Workflow|1|OMSworkflow_id=lms::workflow::WorkflowExecutor(0x2063ba5d1d0) OMSname=:/workflows/instanceprocesssampling.workflow OMSmsgid=360
## [Header field definitions](/docs/mdemail/operating/cef-syslog-message-format#header-field-definitions)

| Header | Email Gateway Security values | Examples |
| --- | --- | --- |
| CEF Version | *CEF:0* |  |
| Severity | - **DUMP (***0***)**: The most verbose severity level, these entries are for debuggers only. - **DEBUG (***1***)**: Debuggers severity level, mostly used by support issues. - **INFO (***2***)**: Information from the software, such as scan results. - **WARNING (***3***)**: A problem occurred needs investigation and OPSWAT support must be contacted, however the product is supposed to be operational. - **ERROR (***4***)**: Software error happened, please contact support if the issue is persist. Software functionality may be downgraded in these cases. |  |
| Device Event Class ID | Source module of the message | *common.workflow* |
| Device Product | *MDEMAIL* |  |
| Device Vendor | *OPSWAT* |  |
| Device Version | Email Gateway Security product version | *5.7.5* |
| Name | Log message | *Executing Workflow* |

## [Extension field](/docs/mdemail/operating/cef-syslog-message-format#extension-field)

The Extension field contains a collection of key-value pairs in the structure *key*=*value*. An event can contain any number of key-value pairs in any order, separated by spaces (" ").

The extension provides additional details about the event covered by the message.

SOC level message parameters

As of release 6.4.2, SOC-level log messages also carry their message parameters as key-value pairs in the extension field. In earlier versions, SOC-level messages embedded these parameters only in the Name field text, leaving the extension without them.

OMSemailId=681464 OMSuri=smtp://192.168.0.17:25 OMSrecipients=QList("karoly.arnhoffer@opswat.com") OMSuseTls=false OMSforceTls=false OMSmsgid=2407

For further details about CEF see <https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/pdfdoc/cef-implementation-standard/cef-implementation-standard.pdf>.
