<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/operating/connection-alerts -->

# Connection Alerts

The connection alerts list is accessible under **Connections** → **Connection Alerts.**

The connection alerts list contains all alerts on the devices in the system.

Each alert contains the following fields:

- Source device (device from internal network), destination device (device from internal network)/ destination host (remote host), source port, destination port, protocol, connection started time, duration, data length.
- Alert information: alert started/ended time, status, message for the detail, reason, comment, and the action.

Note: you can sort a field in ascending or descending order by clicking on its label.

A new alert will appear on the list when ***a connection*** between two devices ***violates any policies*** on the blocklist [*policy page*](https://opswat.atlassian.net/wiki/spaces/NAC3/pages/3029405033) *or* when ***Anomaly Detection is turned on***.

### [If the “On-screen alert” option is turned off](/docs/md-ot-security/v.3.4.8/operating/connection-alerts#if-the-on-screen-alert-option-is-turned-off)

An acknowledge button on each alert record will appear in the Action column to indicate that the alert has not been acknowledged yet.

When the alert has been acknowledged, the resolve button will appear and you can completely resolve that alert.

Users can acknowledge alerts in batch or all alerts by clicking on "Batch Acknowledge." Similarly, users can resolve alerts in batch or resolve all alerts by clicking on "Batch Resolve”.

## [Filter](/docs/md-ot-security/v.3.4.8/operating/connection-alerts#filter)

We support searching and filtering on the connection alerts list:

- You can ***enter the value for 1 or more fields***, and the result list and number of total records will be updated according to the value you entered.
- You can ***change the order of the fields displayed on the list*** by clicking "..." -> “Filter preference” then drag and drop the fields and arrange them in the desired order.
- You can choose to **show/hide the fields in the list** by clicking "..." -> “Filter preference” and tick/untick the box on the left of the field name
- You can ***save a custom filter*** for your convenience when you need to reuse them in the future. Enter values ​​into the fields to filter then select "..." -> "Create filter", and give a name for your filter. Every time you return, click on "..." → Your saved filter to apply it.
- You can ***update your saved custom filters*** by editing/adding values ​​to the fields and selecting "..." then "Save filter”
- You can ***delete a saved custom filter*** by selecting “…” → “X” button on the saved filter
