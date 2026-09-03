<!-- source: https://www.opswat.com/docs/mdmft/high-availability/troubleshooting -->

# Troubleshooting

Summarize Page    Connect to Cursor Connect to VS Code
### [All controls are disabled](/docs/mdmft/high-availability/troubleshooting#all-controls-are-disabled)

This occurs when `localpeer.json` is missing or has no valid API key. Only the close button remains functional. Fix the file and relaunch.

### [Node or peer shows "Unreachable" on Dashboard](/docs/mdmft/high-availability/troubleshooting#node-or-peer-shows-unreachable-on-dashboard)

The health check endpoint could not be reached. Check that:

- The node/peer is running and accessible from this machine.
- The URL is correct (verify on the Nodes or Cluster page).
- Firewall rules allow the connection.

### [Save button stays disabled](/docs/mdmft/high-availability/troubleshooting#save-button-stays-disabled)

The **Save** button is only enabled when there are unsaved changes. Modify any field to enable it.

### [Validation error: "Must be a valid positive TimeSpan"](/docs/mdmft/high-availability/troubleshooting#validation-error-must-be-a-valid-positive-timespan)

TimeSpan fields require the `HH:mm:ss` format. Examples:

- 1 second: `00:00:01`
- 30 seconds: `00:00:30`
- 2 minutes: `00:02:00`
- 1 hour: `01:00:00`

### [Cluster settings disappear after saving](/docs/mdmft/high-availability/troubleshooting#cluster-settings-disappear-after-saving)

This is expected behavior when only the self peer exists. In standalone mode, the `ClusterSettings` and `Kestrel.Endpoints.Raft` sections are intentionally removed from `appsettings.json` to keep the configuration clean.

### [Unmanaged JSON sections are being modified](/docs/mdmft/high-availability/troubleshooting#unmanaged-json-sections-are-being-modified)

The tool preserves all JSON sections it does not manage. If you notice unwanted changes, ensure you are using the tool (not a text editor) for all edits, and that `appsettings.json` is well-formed JSON before loading.
