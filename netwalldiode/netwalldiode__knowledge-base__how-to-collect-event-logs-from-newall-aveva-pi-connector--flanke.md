<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/how-to-collect-event-logs-from-newall-aveva-pi-connector--flanke -->

# How to collect Event logs from Newall AVEVA PI Connector (Flankers)?

This article applies to all AVEVA PI Connector versions

> Typically, the Netwall AVEVA PI Connector services forward their event logs directly to the Netwall. These logs can usually be accessed via the Netwall syslog or included in a support package.

However, in some cases, the logs available on the Netwall may not contain sufficient detail for troubleshooting. In such situations, we may need to collect logs directly from the servers where the Netwall AVEVA PI Connector services are running. These servers are referred to as **flankers**:

- **Red flanker** → associated with the Red Netwall
- **Blue flanker** → associated with the Blue Netwall

### [Steps to Export Event Logs](/docs/netwalldiode/knowledge-base/how-to-collect-event-logs-from-newall-aveva-pi-connector--flanke#steps-to-export-event-logs)

1. Log in to the appropriate flanker server.
2. Open **Event Viewer**.
3. Navigate to the following path:

   - **Blue flanker:**`Applications and Services Logs → OpswPiBlueLog`

- **Red flanker:**`Applications and Services Logs → OpswPiRedLog`

4. Select the relevant log.
5. In the right-hand pane, click “Save All Events As…”
6. Choose a file name and save the log file.
7. Share the exported file with us for further analysis.

- By default, Windows stores approximately **50,000 events** per log.
- If needed, the log size can be increased on the flanker servers using PowerShell:: [Limit-EventLog (Microsoft.PowerShell.Management) - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/limit-eventlog?view=powershell-5.1)
Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
