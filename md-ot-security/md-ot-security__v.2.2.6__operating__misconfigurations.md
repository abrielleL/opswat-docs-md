<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/misconfigurations -->

# Misconfigurations

## [**The misconfigurations tab is accessible under** **Assets -> Misconfigurations.**](/docs/md-ot-security/v.2.2.6/operating/misconfigurations#the-misconfigurations-tab-is-accessible-under-assets---misconfigurations)

This page contains misconfiguration ports of all devices in the system.

Each record contains:

- Basic information of that device such as Name, IP, MAC, Criticality, Type, Sub-type.
- The port that is opening with protocol and state information, last seen open and close.

Note: you can sort a field in ascending or descending order by clicking on the its name.

## [Filter](/docs/md-ot-security/v.2.2.6/operating/misconfigurations#filter)

We support searching and filtering on the device misconfigurations list:

- You can *enter value for one or more fields*, and the result list and number of total records will be updated according to the value(s) you entered.

| **Index** | **Field** | **Data type** | **Type of input** | **Support multi-input** | **Note** |
| --- | --- | --- | --- | --- | --- |
| 1 | Name | Text | Input text | No |  |
| 2 | IP | Number | Input number in IP address format (e.g. 192.168.1.102), IP netmask format (e.g.192.168.1.0/24) | No |  |
| 3 | MAC | Text & Number | Input number and text in MAC address format (e.g. A1:B2:C3:D4:E5:F6), | No |  |
| 4 | Type | Text | Select from drop-down list | Yes |  |
| 5 | Sub-type | Text | Select from drop-down list | No |  |
| 6 | Port | Number | Input text | No |  |
| 7 | Protocol | Text | Input text | No |  |
| 8 | State | Text | Select from drop-down list | No |  |
| 9 | Last seen open | Date time | Select from pop-up calendar and clock | No |  |
| 10 | Last seen close | Date time | Select from pop-up calendar and clock | No |  |

We support searching and filtering on the misconfigurations list:

- You can *enter value for 1 or more fields*, and the result list and number of total records will be updated according to the value(s) you entered.
- You can *change the order of the fields displaying on the list* by clicking "..." -> “Filter preference” then drag and drop the fields and arrange them in the desired order.
- You can choose to **show/hide the fields in the list** by clicking "..." -> “Filter preference” and tick/untick the box on the left of field name. If you choose more than 10 fields to be displayed on the list, an horizontal scroll bar will appear, just scroll it to the right to see more fields.
- You can *save a custom filter* for your convenience when you need to reuse them in the future. Enter values ​​into the fields to filter then select "..." -> "Create filter", give a name for your filter. Every time you come back, click on "..." → Your saved filter to apply it.
- You can *update your saved custom filters* by editing/adding values ​​to the fields and selecting "..." then "Save filter”
- You can *delete a saved custom filter* by selecting “…” → “X” button on saved filter
