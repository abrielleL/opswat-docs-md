<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-use-simplified-wf -->

# How do I use Simplified Workflow?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk releases **after version 4.7.0**, deployed on both Windows and Linux systems.

Our MetaDefender Kiosk product has a built-in Simplified workflow after a fresh install to support plug-and-play media scanning with automatic decryption and result display.

The process of Simplified Workflow is minimal as follows:

1. Kiosk will directly display the Insert Media screen
2. The Kiosk will automatically decrypt the encrypted USB using a list of preloaded passwords if any
3. The Kiosk will do the scanning and then display the end result as long as the USB is plugged
4. Once the USB is unplugged, it will show the Insert Media screen once again and wait for another USB

## [How to enable Simplified Workflow](/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-use-simplified-wf#how-to-enable-simplified-workflow)

1. Navigate to the Workflows tab and enable Simplified Workflow group.

Info:

If **Simplified Workflow** group is enabled, **Employee Workflows** and **Guest Workflows** groups are disabled automatically, and vice versa.

2. **Simplified workflow** only supports to configure [**Media Types**](https://docs.opswat.com/mdkiosk/operating/allowed-media-types), [**Processing**](https://docs.opswat.com/mdkiosk/operating/selecting-a-server-to-process-files), [**Printing**](https://docs.opswat.com/mdkiosk/operating/managing-printing-options) and [**Logging**](https://docs.opswat.com/mdkiosk/operating/managing-logging-options).

## [Usage Notes](/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-use-simplified-wf#usage-notes)

- **Simplified workflow** does not support **Retrieve Files** or other Post actions (**Allowed/Blocked** **File Handling**, **Email),** excluding **Printing** the report.
- If there are any configuration changes, manually reloading the Kiosk UI by clicking **Exit & Eject** or **Cancel** button is required to take effect.

Warning:

Simplified WF will directly display the *Insert Media* screen, which means KIOSK has already started a session. When clicking *SCAN NOW* for Self Scan, it will alert other scans are in progress.

Configure Schedule Self Scan and enable *“Allow Self Scan to cancel any currently runnning scan”* to trigger Self Scan instead.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
