<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-track-settings-changes-in-metadefender-core -->

# How to track Settings changes in MetaDefender Core

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [Overview](/docs/mdcore/v5.22.1/knowledge-base/how-to-track-settings-changes-in-metadefender-core#overview)

This article explains how to track settings changes in MetaDefender Core.

For example: enabling **Session timeout** in Settings > Security:

## [Steps to Configure](/docs/mdcore/v5.22.1/knowledge-base/how-to-track-settings-changes-in-metadefender-core#steps-to-configure)

- Such changes can be tracked on the UI > History > [Configuration history](https://www.opswat.com/docs/mdcore/operating/dashboard#configuration-history):

- Admins can also [setup a remote syslog server](https://www.opswat.com/docs/mdcore/configuration/advanced-log-configuration#syslog-settings), and this change will show up as:

Value changed, key='/admin/config/session', parameter='absoluteSessionTimeout', old='0', new='300000', user='LOCAL/admin'
## [Verify the Change](/docs/mdcore/v5.22.1/knowledge-base/how-to-track-settings-changes-in-metadefender-core#verify-the-change)

- After setting up syslog server, make some configuration changes and observe if the syslog server records these changes.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
