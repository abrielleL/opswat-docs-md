<!-- source: https://www.opswat.com/docs/md-ot-security/operating/vulnerabilities -->

# Vulnerabilities

The device alerts list tab is accessible under **Assets** → **Vulnerabilities.**

This page displays **CVE violations** for all devices in the system.

Each record contains:

- **Source** — where the CVE definition came from: **CISA** (CISA Known Exploited Vulnerabilities catalog) or **System** (the built-in vulnerability database).
- Basic information of that device, such as Device Name, IPv4, Type, Sub-type.
- CVE information: CVE code, **Status** (Unpatched, Patched, Potential), **Category** (Open, Closed), Last Detected Time, Last Patched Time, and **Confidence Score**.
- Vulnerability score: common vulnerability scoring system and severity score. The color will be changed based on the score level. (low/medium/high)
- **Asset Status** — whether the affected device is still active/inventoried.

Note: Some of the CVEs may not have a CVSS v3 score.

Every column is sortable — click a column header to toggle ascending/descending order.

## [CVE document](/docs/md-ot-security/operating/vulnerabilities#cve-document)

Users can click the **Document** button at the end of each row to open detailed documentation for a specific CVE code. We support multiple document versions, allowing users to select the suitable version for their environment.

**Note:** If no document has been acquired for that CVE yet, the viewer shows "Document is not available" with a link to the **Vulnerability Definitions** tab, where documents can be acquired online or uploaded manually. The neighboring **Vulnerability Supplemental Documents** tab manages vendor-specific supplemental documents the same way.

## [View Detail](/docs/md-ot-security/operating/vulnerabilities#view-detail)

Click the **View Detail** (info) button at the end of a row to open the CVE detail popup. It shows:

- **CVSS Version 3.X** / **CVSS Version 2.0** tabs — only the version(s) NVD actually published for that CVE are available.
- **NVD CVSS** score and severity, the CVSS **Vector** string, and **Last Detected Time**.
- The CVE description.
- A **Recommendation** section with remediation guidance. For a **CISA**-sourced CVE this section is marked with a **CISA** badge; for a **System**-sourced CVE it is labeled **System Recommendation** instead, with no CISA badge, and may list guidance per affected vendor product.

## [Updating vulnerability status](/docs/md-ot-security/operating/vulnerabilities#updating-vulnerability-status)

Click the **Edit** (pencil) button on a row to update a single vulnerability, or select one or more rows with the row checkboxes and click **Batch Update** (top-right of the table) to update them all at once. Both open the same **Update Vulnerability** form:

- **Category** — Open or Closed.
- **Status** — Unpatched, Patched, or Potential.
- **Reason** — free-text note explaining the change; required before **Save** becomes enabled.

Saving shows a confirmation toast and records the change in that CVE's History (see below).

## [History](/docs/md-ot-security/operating/vulnerabilities#history)

Click the **History** (clock) button on a row to see the audit trail of Status/Category changes for that device's CVE: **CVE Code**, **Status** (from → to), **Category** (from → to), **Updated By**, **Updated At**, and **Reason**. The list can be quick-searched by CVE Code or by Reason, and shows "No data to show" if the vulnerability has never been manually updated.

## [Filter](/docs/md-ot-security/operating/vulnerabilities#filter)

We support searching and filtering on the device vulnerabilities list:

- You can ***enter a value for one or more fields***, and the result list and number of total records will be updated according to the value(s) you entered.

| **Index ** | **Field ** | **Data type** | **Type of input** | **Support multi-input** | **Note** |
| --- | --- | --- | --- | --- | --- |
| 1 | Name | Text | Input text | No |  |
| 2 | IP | Number | Input number in IP address format (e.g. 192.168.1.102), IP netmask format (e.g.192.168.1.0/24) | No |  |
| 3 | CVE Code | Text & Number | Input number and text in CVE code (e.g. CVE-2017-12741) | No |  |
| 4 | Type | Text | Select from drop-down list | Yes |  |
| 5 | Sub-type | Text | Select from drop-down list | No |  |
| 6 | NVD CVSS v2 | Float Number | Input range from-to | No |  |
| 7 | NVD CVSS v3 | Float Number | Input range from-to | No |  |
| 8 | OPSWAT CVSS | Float Number | Input range from-to | No |  |
| 9 | Last seen open | Date time | Select from pop-up calendar and clock | No |  |
| 10 | Last seen close | Date time | Select from pop-up calendar and clock | No |  |

We support searching and filtering on the vulnerabilities list:

- You can ***enter a value for 1 or more fields***, and the result list and number of total records will be updated according to the value(s) you entered.
- You can **change the order of the fields displayed on the list** by clicking "..." and selecting "Filter Preference." Then, drag and drop the fields to arrange them in your desired order.
- You can **show or hide fields in the list** by clicking "..." -> "Filter Preference" and checking/unchecking the box to the left of each field name. If you select more than 10 fields to display, a horizontal scrollbar will appear. Simply scroll to the right to see more fields.
- You can **save custom filters** for easy reuse. To create one, enter values into the fields you want to filter by, then select "..." -> "Create filter," and name your filter. To apply a saved filter later, simply click "..." and select its name.
- You can **update your saved custom filters** by editing or adding values to the fields. Then, select "..." and choose "Save Filter."
- You can **delete a saved custom filter** by selecting "..." and then clicking the "**X**" button next to the saved filter.
