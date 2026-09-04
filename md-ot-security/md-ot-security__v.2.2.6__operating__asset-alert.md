<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/asset-alert -->

# Asset Alert

The asset alerts list tab is accessible under **Assets -> Alerts**.

The asset alerts list contains records of alerts on assets in the system.

Each alert contains:

- Basic information of that asset such as Name, IP, MAC, Criticality, Type, Sub-type.
- Alerting information such as Alert Started, Alert Ended, Alert Criticality, Message, Reason, Alert Status.
- Detailed asset information such as operating system, Manufacturer, Country of Origin (COO), Site, which asset belongs to Purdue Models.
- Also, the status of the asset in the system such as Onboarded Time, Current Status, Asset ID, Agent that detected that asset is shown.

Note: you can sort a field in ascending or descending order by clicking on its name.

### [A new alert will appear on the list when:](/docs/md-ot-security/v.2.2.6/operating/asset-alert#a-new-alert-will-appear-on-the-list-when)

- MetaDefender OT Security turns on **Anomaly Detection** and a *strange* *asset* (not in allowlist) connect/plug in to the system.

*Note: You can add a* *asset* *to allowlist by either resolve its alert by choosing option “Anticipated” while turning on anomaly detection or switch to Discovery mode and let that* *asset* *discovered automatically by* MetaDefender OT Security_._

- A asset is *active* but *make no communication* in a *certain period of time*

*Note: You can set a time threshold for the* *asset* *not to communicate in*

- A asset is *active* and *communicate* with other assets *on disallowed port(s)*

*Note: You can specify which ports that all* *assets* *can communicate on in A__sset* *type Setting. You can also set for a specific* *asset* *in A__sset* *policies.*

- A asset is *active* and *make communication* with other assets *with disallowed protocol(s)*

*Note: You can specify which protocols that all* *assets* *of that type can communicate with in Asset* *Type Setting. You can also set for a specific* *asset* *in A__sset* *policies.*

- A asset is *inactive* in a *certain period of time*
- A asset violates a block list policies.

*Note: You can set a threshold for how long a* *asset* *can be inactive before alerting. You can also set for a specific* *asset* *in A__sset* *policies.*

If option “On-screen alert” in *Alert settings* is disabled, a “Acknowledge” button will show up on each alert record for you to acknowledge when tapping on.

### [If “On-screen alert” option is turned off,](/docs/md-ot-security/v.2.2.6/operating/asset-alert#if-on-screen-alert-option-is-turned-off)

An acknowledge button will appear in the Acknowledgment column on each alert record to indicate that the alert has not been acknowledged yet.

When the alert has been acknowledged, the resolve button will appear, and you can completely resolve that alert.

## [Filter](/docs/md-ot-security/v.2.2.6/operating/asset-alert#filter)

We support searching and filtering on the asset alerts list:

- You can *enter value for 1 or more fields*, and the result list and number of total records will be updated according to the value(s) you entered.

| **Index** | **Field** | **Data type** | **Type of input** | **Support multi-input** | **Note** |
| --- | --- | --- | --- | --- | --- |
| 1 | Name | Text | Input text | No |  |
| 2 | IP | Number | Input number in IP address format (e.g. 192.168.1.102), IP netmask format (e.g.192.168.1.0/24) | No |  |
| 3 | Level | Text | Select from drop-down list | No |  |
| 4 | MAC | Text & Number | Input number and text in MAC address format (e.g. A1:B2:C3:D4:E5:F6), | No |  |
| 5 | Type | Text | Select from drop-down list | Yes |  |
| 6 | Sub-type | Text | Select from drop-down list | No |  |
| 7 | Started | Date | Select from pop-up calendar and clock | No |  |
| 8 | Acknowledged Time | Date | Select from pop-up calendar and clock | No |  |
| 9 | Criticality of Asset | Text | Select from drop-down list | No |  |
| 10 | Message | Text | Input text | No |  |
| 11 | Reason | Text | Input text | No |  |
| 12 | Status | Text | Select from drop-down list | No |  |
| 13 | OS | Text | Select from drop-down list | No |  |
| 14 | Brand | Text | Select from drop-down list | No |  |
| 15 | Origin of NIC | Text | Select from drop-down list | No |  |
| 16 | Purdue Model Level | Number | Select from drop-down list | Yes |  |
| 17 | Site | Text | Select from drop-down list | No |  |
| 18 | Onboarded | Date time | Select from pop-up calendar and clock | No |  |
| 19 | Asset Label | Text | Input text | No |  |
| 20 | Agent | Text | Select from drop-down list | No |  |

- You can *change the order of the fields displaying on the list* by clicking "..." -> “Filter preference” then drag and drop the fields and arrange them in the desired order.
- You can choose to **show/hide the fields in the list** by clicking "..." -> “Filter preference” and tick/untick the box on the left of field name. If you choose more than 10 fields to be displayed on the list, a horizontal scroll bar will appear, just scroll it to the right to see more fields.
- You can *save a custom filter* for your convenience when you need to reuse them in the future. Enter values ​​into the fields to filter then select "..." -> "Create filter", give a name for your filter. Every time you come back, click on "..." → Your saved filter to apply it.
- You can *update your saved custom filters* by editing/adding values ​​to the fields and selecting "..." then "Save filter”
- You can *delete a saved custom filter* by selecting “…” → “X” button on saved filter
