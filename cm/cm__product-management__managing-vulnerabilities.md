<!-- source: https://www.opswat.com/docs/cm/product-management/managing-vulnerabilities -->

# Managing Vulnerabilities

The Vulnerabilities section in My OPSWAT Central Management allows Administrators to gather reporting on CVEs that require attention and may potentially put their devices at risk. In addition, this section is where Administrators are able to add vulnerabilities to their allowlist.

## Vulnerability Definitions and Scoring

- **CVSS 2.0 and 3.0** - OSPWAT uses the **Common Vulnerability Scoring System** (**CVSS**), it is a free and open industry standard for assessing the severity of computer system security vulnerabilities. Although the latest version, CVSSv3 has improvements compared with previous versions, it still has limitations such as it is just a static score, does not take CVE lifecycle as an input.
- **OPSWAT Score** - A dynamic score, ranging from 0 to 10, calculated based on the four parameters:
  - **CVSSv2/CVSSv3**: still be a primary input
  - **CVE Popularity**: how active the given vulnerability
  - **Compromised Risk rate:** number of infected devices/total number of devices that we have seen this vulnerability exists in. The data of risk level is coming from real life machine
  - **CVE Lifecycle**: how long the vulnerability has been reported
- **Severity** - The vulnerabilities reported in My OPSWAT Central Management are assigned a severity level. Each level is assigned to a CVE based on OPSWATs calculations.

## Filtering and Exporting

Administrators and console users are able to export and filter the vulnerability list. To filter the list, users can select **Filters** and then select vulnerability severity or allow-list status.

To export a list, users can select the **Export** button on the page. This will start a download of a CSV file with CVEs according to any filters or search values.
