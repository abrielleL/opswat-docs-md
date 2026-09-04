<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/asset-alert -->

# Asset Alerts

The asset alerts list tab is accessible under **Assets** → **Alerts.**

The asset alerts list contains records of alerts on assets in the system.

Each alert contains:

- Basic information of that asset such as Name, IP, MAC, Criticality, Type, Sub-type.
- Alerting information such as Alert Started, Alert Ended, Alert Criticality, Message, Reason, Alert Status.
- Detailed asset information such as operating system, Manufacturer, Country of Origin (COO), Site, and which asset belongs to Purdue Models.
- Also, the status of the asset in the system such as Onboarded Time, Current Status, Asset ID, and Agent that detected that asset is shown.

Note: you can sort a field in ascending or descending order by clicking on its name.

### [A new alert will appear on the list when:](/docs/md-ot-security/v.3.4.0/operating/asset-alert#a-new-alert-will-appear-on-the-list-when)

- MetaDefender OT Security turns on **Anomaly Detection** and a ***strange asset*** (not in allowlist) connects/plugs into the system.

*Note: You can add an asset to the allowlist by resolving its alert by choosing the option “Anticipated” while turning on anomaly detection or switching to Discovery mode and letting that asset be discovered automatically by* MetaDefender OT Security_._

- An asset is ***active*** but ***makes no communication*** in a ***certain period***

*Note: You can set a time threshold for the asset not to communicate in*

- An asset is ***active*** and ***communicates*** with other assets ***on disallowed port(s)***

*Note: You can specify which ports all assets can communicate on in the asset type Setting. You can also set for a specific asset in asset policies.*

- An asset is ***active*** and ***makes communication*** with other assets ***with disallowed protocol(s)***

*Note: You can specify which protocols all assets of that type can communicate within the asset type Setting. You can also set for a specific asset in asset policies.*

- An asset is ***inactive*** for a ***certain period***
- An asset violates a block list policies.

*Note: You can set a threshold for how long an asset can be inactive before alerting. You can also set for a specific asset in asset policies.*

If the option “On-screen alert” in *Alert settings* is disabled, a “Acknowledge” button will appear on each alert record for you to acknowledge when tapping on.

### [If the “On-screen alert” option is turned off,](/docs/md-ot-security/v.3.4.0/operating/asset-alert#if-the-on-screen-alert-option-is-turned-off)

An acknowledge button on each alert record will appear in the Acknowledgment column to indicate that the alert has not been acknowledged yet.

When the alert has been acknowledged, the resolve button will appear and you can completely resolve that alert.

Users can acknowledge alerts in batch or all alerts by clicking on "Batch Acknowledge." Similarly, users can resolve alerts in batch or resolve all alerts by clicking on "Batch Resolve.

## [Filter](/docs/md-ot-security/v.3.4.0/operating/asset-alert#filter)

We support searching and filtering on the asset alerts list:

- You can ***enter the value for 1 or more fields***, and the result list and number of total records will be updated according to the value(s) you entered.
- You can ***change the order of the fields displayed on the list*** by clicking "..." -> “Filter preference” then drag and drop the fields and arrange them in the desired order.
- You can choose to **show/hide the fields in the list** by clicking "..." -> “Filter preference” and tick/untick the box on the left of the field name. If you choose more than 10 fields to be displayed on the list, a horizontal scroll bar will appear, just scroll it to the right to see more fields.
- You can ***save a custom filter*** for your convenience when you need to reuse them in the future. Enter values ​​into the fields to filter then select "..." -> "Create filter", and give a name for your filter. Every time you come back, click on "..." → Your saved filter to apply it.
- You can ***update your saved custom filters*** by editing/adding values ​​to the fields and selecting "..." then "Save filter”
- You can ***delete a saved custom filter*** by selecting “…” → “X” button on the saved filter
