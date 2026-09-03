<!-- source: https://www.opswat.com/docs/md-ot-security/operating/asset-alert -->

# Asset Alerts

The asset alerts list tab is accessible under **Assets** → **Asset Alerts.**

The asset alerts list contains records of alerts on assets in the system.

*(Image could not be embedded — see Confluence)*

Each alert provides comprehensive details, including:

- Basic Asset Information: Such as Name, Type, Sub-type, and IP address.
- Alerting Information: Including Alert Started (timestamp), Alert Ended (timestamp), Alert Criticality, Message, Reason, and Alert Status.
- Detailed Asset Information: Such as Operating System (OS), Manufacturer, Country of Origin (COO), Site, and its associated Purdue Model.
- Asset System Status: Such as Onboarded Time, Current Status, Asset ID, and the Agent that detected the asset.

Note: You can sort any field in ascending or descending order by clicking its name.

### [A new alert will appear on the list when:](/docs/md-ot-security/operating/asset-alert#a-new-alert-will-appear-on-the-list-when)

- MetaDefender OT Security turns on **Anomaly Detection,** and a ***strange asset*** (not in the allowlist) connects/plugs into the system.

*Note: You can add an asset to the allowlist by resolving its alert by choosing the option “Anticipated” while turning on anomaly detection or switching to Discovery mode and letting that asset be discovered automatically by* MetaDefender OT Security_._

- An asset is ***active*** but ***makes no communication*** in a ***certain period***

*Note: You can set a time threshold for the asset not to communicate in*

- An asset is ***active*** and ***communicates*** with other assets ***on disallowed port(s)***

*Note: You can specify which ports all assets can communicate on in the asset type settings. You can also set for a specific asset in asset policies.*

- An asset is ***active*** and ***communicates*** with other assets ***with disallowed protocol(s)***

*Note: You can specify which protocols all assets of that type can communicate within the asset type Setting. You can also set a specific asset in asset policies.*

- An asset is ***inactive*** for a ***certain period***
- An asset violates a block list policy.

*Note: You can set a threshold for how long an asset can be inactive before alerting. You can also set a specific asset in asset policies.*

If the option “On-screen alert” in *Alert settings* is disabled, a “Acknowledge” button will appear on each alert record for you to acknowledge when tapping on it.

### [If the “On-screen alert” option is turned off,](/docs/md-ot-security/operating/asset-alert#if-the-on-screen-alert-option-is-turned-off)

An acknowledge button on each alert record will appear in the Acknowledgment column to indicate that the alert has not been acknowledged yet.

When the alert has been acknowledged, the resolve button will appear, and you can completely resolve that alert.

Users can acknowledge alerts in batch or all alerts by clicking on "Batch Acknowledge." Similarly, users can resolve alerts in batch or resolve all alerts by clicking on "Batch Resolve.

*(Image could not be embedded — see Confluence)*

*(Image could not be embedded — see Confluence)*

## [Filter](/docs/md-ot-security/operating/asset-alert#filter)

We support searching and filtering on the asset alerts list:

- You can ***enter the value for 1 or more fields***, and the result list and number of total records will be updated according to the value(s) you entered.

| **Index ** | **Field ** | **Data type** | **Type of input** | **Support multi-input** | **Note** |
| --- | --- | --- | --- | --- | --- |
| 1 | Name | Text | Input text | No |  |
| 2 | IP | Number | Input number in IP address format (e.g. 192.168.1.102), IP netmask format (e.g.192.168.1.0/24) | No |  |
| 3 | Level | Text | Select from the drop-down list | No |  |
| 4 | MAC | Text & Number | Input number and text in MAC address format (e.g. A1:B2:C3:D4:E5:F6), | No |  |
| 5 | Type | Text | Select from the drop-down list | Yes |  |
| 6 | Sub-type | Text | Select from the drop-down list | No |  |
| 7 | Started | Date | Select from the pop-up calendar and clock | No |  |
| 8 | Acknowledged Time | Date | Select from the pop-up calendar and clock | No |  |
| 9 | Criticality of Asset | Text | Select from the drop-down list | No |  |
| 10 | Message | Text | Input text | No |  |
| 11 | Reason | Text | Input text | No |  |
| 12 | Status | Text | Select from the drop-down list | No |  |
| 13 | OS | Text | Select from the drop-down list | No |  |
| 14 | Brand | Text | Select from the drop-down list | No |  |
| 15 | Origin of NIC | Text | Select from the drop-down list | No |  |
| 16 | Purdue Model Level | Number | Select from the drop-down list | Yes |  |
| 17 | Site | Text | Select from the drop-down list | No |  |
| 18 | Onboarded | Date time | Select from the pop-up calendar and clock | No |  |
| 19 | Asset Label | Text | Input text | No |  |
| 20 | Agent | Text | Select from the drop-down list | No |  |

- You can **change the order of the fields displayed on the list** by clicking "..." -> "**Filter Preference**." Then, **drag and drop** the fields to arrange them in your desired order.
- You can **show or hide** **fields in the list** by clicking "..." -> "**Filter Preference**" and **checking/unchecking** the box to the left of each field name. If you select more than 10 fields to be displayed, a horizontal scrollbar will appear. Simply scroll to the right to view the additional fields.
- You can **save a custom filter** for easy reuse. To create one, first enter values into the fields you want to filter by. Then, select "..." -> "Create filter" and give your filter a name. To apply your saved filter later, simply click "..." and select its name.
- You can **update your saved custom filters** by editing or adding values to the fields. Then, select "..." and choose "**Save Filter**."
- You can **delete a saved custom filter** by selecting "..." and then clicking the "**X**" button next to the saved filter.
