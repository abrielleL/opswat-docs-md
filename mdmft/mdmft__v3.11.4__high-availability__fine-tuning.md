<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/high-availability/fine-tuning -->

# Fine tuning

Summarize Page    Connect to Cursor Connect to VS Code

The following parameters can be changed in the MetaDefender MFT HA Controller™ `appsettings.json.`

Optionally these settings can be set with the HA Configuration Tool™. See: [Settings Page](/docs/mdmft/v3.11.4/high-availability/settings-page)

| Property name | Description | Default value |
| --- | --- | --- |
| HealthCheckInterval | Node health check interval. | “00:00:01” |
| NumberOfFailedHealthChecksBeforeFailover | Number of failed health checks before failover to the other node. | 2 |
| NodeManagerClientTimeout | Request timeout for node health check, activation and deactivation. | “00:00:30” |
| ApplicationClientTimeout | Request timeout for forwarded requests to the application. | “00:02:00” |

Info

Configuration changes require service restart.
