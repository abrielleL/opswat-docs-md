<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/operating/asset-list -->

# Asset List

The list of devices is accessible via **Assets → Asset List**.

Currently, asset data is also cached in the **Enterprise Manager** to improve performance and ensure essential asset information is readily available to users.

The **Asset List** contains detailed information about all devices in the system.

*(Image could not be embedded — see Confluence)*

Each row contains the following fields:

- **Basic Information:** This includes the device's name, IP address, MAC address, criticality, type, subtype, brand, OS, and exposure score.
- **Detailed Information:** This includes the product model, hardware/CPU, hardware version, part number, and OS version.
- **Device Status:** This shows the device's status within the system, including its onboarded time, current status, asset label, and the agent that detected it or its device learning time status.

**Note:** You can sort any field in ascending or descending order by clicking on its name.

You can perform actions on a device directly from the list of devices. These actions include learning options, editing device information, deleting the device, and cloning the device. To access these options, tap the "..." icon to the left of each device's record.

For more details, please refer to the **Device Manipulation** section.

*(Image could not be embedded — see Confluence)*

*(Image could not be embedded — see Confluence)*

## [Filter](/docs/md-ot-security/v4.0.0/operating/asset-list#filter)

We support searching and filtering on the list of devices:

*(Image could not be embedded — see Confluence)*

- You can ***enter a value for 1 or more fields***, and the result list and number of total records will be updated according to the value(s) you entered.

| **Index** | **Field** | **Data type** | **Type of input ** | **Support multi-input** | **Note** |
| --- | --- | --- | --- | --- | --- |
| 1 | Name | Text | Input text | No |  |
| 2 | Type | Text | Select from the drop-down list | Yes |  |
| 3 | Sub-type | Text | Select from the drop-down list | No |  |
| 4 | Vendor/Brand | Text | Select from the drop-down list | No |  |
| 5 | Product/Model | Number | Input a number | No |  |
| 6 | Hardware/CPU | Text&Number | Input a number and text | No |  |
| 7 | Hardware version | Text&Number | Input a number and text | No |  |
| 8 | Article/Part No. | Text&Number | Input a number and text | No |  |
| 9 | Operating System | Text&Number | Select from the drop-down list | No |  |
| 10 | OS Version | Text&Number | Input a number and text | No |  |
| 11 | IP | Number | Input number in IP address format (e.g. 192.168.1.102), IP netmask format (e.g.192.168.1.0/24) | No |  |
| 12 | MAC | Text&Number | Input number and text in MAC address format (e.g. A1:B2:C3:D4:E5:F6), | No |  |
| 13 | Origin of NIC | Text | Select from the drop-down list | No |  |
| 14 | Purdue Model Level | Number | Select from the drop-down list | Yes |  |
| 15 | Criticality of Asset | Text | Select from the drop-down list | No |  |
| 16 | Exposure score | Number | 0 to 100 | No |  |
| 17 | Onboarded | Date time | Select from the pop-up calendar and clock | No |  |
| 18 | Status | Text | Select from the drop-down list | No |  |
| 19 | Site | Text | Select from the drop-down list | No |  |
| 20 | Asset Label | Text | Input text | No |  |
| 21 | Agent | Text | Select from the drop-down list | No |  |
| 22 | Learning status | Icon | Learning/Completed | No |  |
| 23 | Host Name | Text | Input text | No |  |
| 24 | System Description | Text | Input text | No |  |
| 25 | Protected By | Text | Input text | No |  |
| 26 | Product Lifecycle Status | Text | Input text | No |  |

- You **can change the order of the fields displayed on the list** by clicking "..." -> **Filter Preference**, then dragging and dropping the fields into your desired order.

*(Image could not be embedded — see Confluence)*

- You can **show or hide fields in the list** by clicking '...' -> **Filter Preference** and **checking/unchecking** the box to the left of the field name.
- You can **save a custom filter** for future use. To create one, first enter values into the desired fields to apply your filter. Then, select "..." -> **Save filter as** and give your filter a name. To apply a saved filter later, simply click "..." and select your saved filter's name.

*(Image could not be embedded — see Confluence)*

- You can update your saved custom filters by **editing or adding values** to the fields, then selecting "..." and choosing **Save filter**.
- You can delete a saved custom filter by selecting "..." and then clicking the "**X**" button next to the saved filter.

**Note:**

- When selecting a Purdue model, any previously chosen Type that is incompatible with the selected model will be discarded, requiring you to choose a new Type.
- When selecting a Type, any previously chosen Subtype that is incompatible with the selected type will be discarded, requiring you to choose a new Subtype.
