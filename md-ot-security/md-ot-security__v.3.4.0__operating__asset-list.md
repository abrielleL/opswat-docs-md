<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/asset-list -->

# Asset List

The list of devices is accessible under **Investigate --> Assets → Asset List.**

Currently, we also cached assets data at Enterprise Manager for improvement of performance and availability essential asset info to users

The list of assets contains all assets information in the system.

Each row contains these following fields:

- Basic information of that device such as Name, IP, MAC, Criticality of Asset, Type, Sub-type, Vendor/Brand, OS, Origin of NIC and exposure score.
- Detailed information such as product model, hardware/CPU, hardware version, part No., OS version.
- Also, the status of the device in the system such as Onboarded Time, Current Status, Asset Label, Agent that detected that device is shown or device learning time status.

Note: you can sort a field in ascending or descending order by clicking on its name.

You can perform actions on a device while on a list of devices such as edit its details, delete the device, clone the device by tapping "..." on each device's record and select Edit/Delete/Clone. For more detail, refer to “Device Manipulation”.

## [Filter](/docs/md-ot-security/v.3.4.0/operating/asset-list#filter)

We support searching and filtering on the list of devices:

- You can ***enter value for 1 or more fields***, and the result list and number of total records will be updated according to the value(s) you entered.

| **Index** | **Field** | **Data type** | **Type of input** | **Support multi-input** | **Note** |
| --- | --- | --- | --- | --- | --- |
| 1 | Name | Text | Input text | No |  |
| 2 | Type | Text | Select from drop-down list | Yes |  |
| 3 | Sub-type | Text | Select from drop-down list | No |  |
| 4 | Vendor/Brand | Text | Select from drop-down list | No |  |
| 5 | Product/Model | Number | Input number | No |  |
| 6 | Hardware/CPU | Text&Number | Input number and text | No |  |
| 7 | Hardware version | Text&Number | Input number and text | No |  |
| 8 | Article/Part No. | Text&Number | Input number and text | No |  |
| 9 | Operating System | Text&Number | Select from drop-down list | No |  |
| 10 | OS Version | Text&Number | Input number and text | No |  |
| 11 | IP | Number | Input number in IP address format (e.g. 192.168.1.102), IP netmask format (e.g.192.168.1.0/24) | No |  |
| 12 | MAC | Text&Number | Input number and text in MAC address format (e.g. A1:B2:C3:D4:E5:F6), | No |  |
| 13 | Origin of NIC | Text | Select from drop-down list | No |  |
| 14 | Purdue Model Level | Number | Select from drop-down list | Yes |  |
| 15 | Criticality of Asset | Text | Select from drop-down list | No |  |
| 16 | Exposure score | Number | 0 to 100 | No |  |
| 17 | Onboarded | Date time | Select from pop-up calendar and clock | No |  |
| 18 | Status | Text | Select from drop-down list | No |  |
| 19 | Site | Text | Select from drop-down list | No |  |
| 20 | Asset Label | Text | Input text | No |  |
| 21 | Agent | Text | Select from drop-down list | No |  |
| 22 | Learning status | Icon | Learning/Completed | No |  |
| 23 | Host Name | Text | Input text | No |  |
| 24 | System Description | Text | Input text | No |  |
| 25 | Protected By | Text | Input text | No |  |
| 26 | Product Lifecycle Status | Text | Input text | No |  |

- You can *change the order of the fields displaying on the list* by clicking "..." -> “Filter preference” then drag and drop the fields and arrange them in the desired order.
- You can choose to **show/hide the fields in the list** by clicking "..." -> “Filter preference” and tick/untick the box on the left of field name.
- You can *save a custom filter* for your convenience when you need to reuse them in the future. Enter values ​​into the fields to filter then select "..." -> "Create filter", give a name for your filter. Every time you come back, click on "..." → Your saved filter to apply it.
- You can *update your saved custom filters* by editing/adding values ​​to the fields and selecting "..." then "Save filter”.
- You can *delete a saved custom filter* by selecting “…” → “X” button on saved filter.

Note: When you select a type first then select a purdue model, if the selected type is not included in selected purdue model, the type will be discarded, you will need to choose another type.

Note: When you select a sub-type first then select a type, if the selected sub-type is not included in selected type, the sub-type will be discarded, you will need to choose another sub-type.
