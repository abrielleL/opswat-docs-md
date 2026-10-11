<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/syslog-message-format -->

# Syslog Message Format

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Core supports to send CEF (Common Event Format) syslog message style

## [Remote Syslog](/docs/mdcore/v5.22.1/configuration/syslog-message-format#remote-syslog)

log formatCopy[Local Timestamp] [Source IP Address] [UTC Timestamp]  [Hostname] [CEF:Version|Device Vendor|Device Product|Device Version|Signature ID|Name|Severity|Extension]

For example:

log exampleCopyJun 24 14:33:18 192.168.200.223 2019-06-24T14:33:19+07:00 OPSWATPC CEF:0|OPSWAT|MSCL|4.16.0|core.network|MSCL[7548] New maximum agent count is set|2|maxAgentCount='1' msgid=665

| Prefix field | Sample value | Description |
| --- | --- | --- |
| Local timestamp | Jun 24 14:33:18 |  |
| IP address | 192.168.200.223 | Source IP address ver. 4 |
| UTC timestamp | 2019-06-24T14:33:19+07:00 |  |
| Hostname | OPSWATPC |  |
| CEF:Version | CEF:0 | Version 0 |
| Device Vendor | OPSWAT |  |
| Device Product | MSCL | MSCL = MetaDefender Core on Linux MSCW = MetaDefender Core on Windows |
| Device Version | 4.16.0 | MetaDefender Core version |
| Signature ID | core.network | For example:   - core.network: Component "network" on "Core" module - agent.engines: Component "engines" on "Node" - common.update: Component "update" on common module shared by all modules |
| Name | MSCL[7548] New maximum agent count is set | Subject of log message   - MSCL[7548] = MetaDefender Core on Linux ["ometascan" process id = 7548] - ometascan-node[455] = MetaDefender Core Node ["ometascan-node" process id = 455] |
| Severity | 2 | Log level   - **DUMP (0)**: The most verbose severity level, these entries are for debuggers only. - **DEBUG (1)**: Debuggers severity level, mostly used by support issues. - **INFO (2)**: Information from the software, such as scan results. - **WARNING (3)**: A problem occurred needs investigation and OPSWAT support must be contacted, however the product is supposed to be operational. - **ERROR (4)**: Software error happened, please contact support if the issue is persist. Software functionality may be downgraded in these cases. |
| Extension | maxAgentCount='1' msgid=665 | To learn more about msgid (message ID): [Error Message Description Table](/docs/mdcore/v5.22.1/configuration/error-message-description-table) |

## [Local Syslog](/docs/mdcore/v5.22.1/configuration/syslog-message-format#local-syslog)

log formatCopy[Local Timestamp] [Hostname] [CEF:Version|Device Vendor|Device Product|Device Version|Signature ID|Name|Severity|Extension]

For example:

log exampleCopyJun 24 14:33:18 OPSWATPC CEF:0|OPSWAT|MSCL|4.16.0|core.network|MSCL[7548] New maximum agent count is set|2|maxAgentCount='1' msgid=665

| Prefix field | Sample value | Description |
| --- | --- | --- |
| Timestamp | Jun 24 14:33:18 |  |
| Hostname | OPSWATPC |  |
| CEF:Version | CEF:0 | Version 0 |
| Device Vendor | OPSWAT |  |
| Device Product | MSCL | MSCL = MetaDefender Core on Linux MSCW = MetaDefender Core on Windows |
| Device Version | 4.16.0 | MetaDefender Core version |
| Signature ID | core.network | For example:   - core.network: Component "network" on "Core" module - agent.engines: Component "engines" on "Node" - common.update: Component "update" on common module shared by all modules |
| Name | MSCL[7548] New maximum agent count is set | Subject of log message   - MSCL[7548] = MetaDefender Core on Linux ["ometascan" process id = 7548] - ometascan-node[455] = MetaDefender Core Node ["ometascan-node" process id = 455] |
| Severity | 2 | Log level   - **DUMP (0)**: The most verbose severity level, these entries are for debuggers only. - **DEBUG (1)**: Debuggers severity level, mostly used by support issues. - **INFO (2)**: Information from the software, such as scan results. - **WARNING (3)**: A problem occurred needs investigation and OPSWAT support must be contacted, however the product is supposed to be operational. - **ERROR (4)**: Software error happened, please contact support if the issue is persist. Software functionality may be downgraded in these cases. |
| Extension | maxAgentCount='1' msgid=665 | To learn more about msgid (message ID): [Error Message Description Table](/docs/mdcore/v5.22.1/configuration/error-message-description-table) |
