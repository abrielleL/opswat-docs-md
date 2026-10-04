<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/configuration/syslog-config -->

# System Log

Use the **System Log** menu to display the System Logs for the MetaDefender Optical Diode (hereinafter Optical Diode). System Log features an advanced log filtering system.

The default *System Log* pane provides a dynamic, auto-refreshing view of the local device syslog. The data displayed is presented in reverse chronological (newest first) order. Filters can be set to view specific subsets of information about events encountered by the appliance.

The initial *System Log* pane provides unfiltered events going through the appliance.

From the System Log pane, you can:

- Add filter type
- Add regex filter
- Export
- Refresh

### [Add Filter Type](/docs/netwalldiode/v1.14.0/configuration/syslog-config#add-filter-type)

You can create filtered views by selecting from a pre-defined list of available filters.

1. Open the **System Log** menu. The *System Log* pane displays.
2. Open the **Action** menu and click **Add Type Filter**. A detail pane displays.
3. Select a filter from the **Filter Type** dropdown list on the detail pane.

### [Add Regex Filter](/docs/netwalldiode/v1.14.0/configuration/syslog-config#add-regex-filter)

1. Open the **System Log** menu. The *System Log* pane displays.
2. Open the **Action** menu and click **Add Regex Filter**. A detail pane displays.
3. Click to select **Exact Match** or **Regular Expression** for searching a pattern in the log file.
4. Type an expression in the box.
5. Click the **Submit** button.

### <Export> Logs

You can export results with or without encryption. The encrypted file must have a password assigned to it and will be slightly larger than the unencrypted file. The default saved file name is *“NetWall_netwall_timestamp_syslog.gz”*

1. Open the **System Log** menu. The *System Log* pane displays.
2. Open the **Action** menu and click **Export**. A detail pane displays.
3. Click **yes** to encrypt the file or **no** to export the file without encryption.
4. Enter and confirm a password in the **Password** boxes (required for encrypted files).
5. Click the **Submit** button.

## [Syslog Message Format](/docs/netwalldiode/v1.14.0/configuration/syslog-config#syslog-message-format)

MetaDefender Optical Diode uses standard RFC 3164 syslog messaging format.

### [Syslog Format](/docs/netwalldiode/v1.14.0/configuration/syslog-config#syslog-format)

[TIMESTAMP] [HOSTNAME] PROCESS NAME [PROCESS ID]: [MESSAGE]

### [Syslog Example](/docs/netwalldiode/v1.14.0/configuration/syslog-config#syslog-example)

Jul 16 06:50:54 diode-dinrail-6041b-blue UaDiodeBlue.Main[3263]: "GetEndpoints.GetPreferredEndpoint" error="Error establishing a connection: BadNotConnected"

| Prefix Field | Sample Value |
| --- | --- |
| TIMESTAMP | Jul 16 06:50:54 |
| HOSTNAME | diode-dinrail-6041b-blue |
| PROCESS NAME | UaDiodeBlue.Main |
| PROCESS ID | 3263 |
| MESSAGE | "GetEndpoints.GetPreferredEndpoint" error="Error establishing a connection: BadNotConnected" |

MetaDefender
