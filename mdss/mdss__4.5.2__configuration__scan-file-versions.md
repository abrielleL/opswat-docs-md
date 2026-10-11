<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/scan-file-versions -->

# Scan File Versions

### Overview

The File Version Scanning remediation capability enables MDSS to locate and examine **every version of a file** that exists during scanning operations. This functionality helps users more effectively pinpoint problematic or restricted file versions.

### Requirements

File versioning must be activated on your SharePoint On-Premises environment before utilizing this feature. The scanning process cannot identify and report on multiple file versions without versioning being enabled.

> **Compatible Storage Systems/Storage Unit**
>
> SharePoint On-Premises

### Configuration

1. Navigate to **Workflows** from the left-side navigation menu.
2. Select the workflow you want to configure scan file versions.
3. Click the **Other Remediations** node.
4. In the modal window that opens, toggle the **Scan File Versions** option.
5. Click **Save Changes** to apply the changes.

![](https://uploads.developerhub.io/prod/k8zL/yuzafmiqwfnuqv9gdd5vme5bocjd5kx4hf0a93w0q5g7hmfkshhf6eufdzxf5884.png)

## Use Case

This remediation type is particularly useful when:

- Multiple versions of the same file may exist across different environments.
- You need to ensure that all versions comply with security and compliance requirements.
- You want quick visibility into which versions are safe and which are blocked.

## Reporting

During or after a scan with **Scan File Versions** enabled, the report provides additional insights:

- **New Column – File Versioning**: A dedicated column displays the number of detected versions for each file and indicates if any of those versions are blocked.

![](https://uploads.developerhub.io/prod/k8zL/fvbeopjx56vnryrjsfp8xms8v64bluho4pxge7fmiiwrzczoiwtx1x8t6q9bmkm7.png)

- **Filtering**: The report includes a filter to show only files that contain blocked versions.

![](https://uploads.developerhub.io/prod/k8zL/ls4koewj82uam7aaorisofe8tek98yjzvya6aas9gd17pzpdjspifzow5xwfip5g.png)

- **Individual File Report**: Within a file’s detailed report, a new column lists all discovered versions. Clicking on a version displays its scan result.

![](https://uploads.developerhub.io/prod/k8zL/kvdg1dgtgfzh4agnr8014ee6dnydmmea3x36tlgtezq9qnep4n6sqi05vsjwk4dg.png)

![](https://uploads.developerhub.io/prod/k8zL/18nc60ms999esowv23rq2qdd46cwa5mes6jw5isp489i4r8x0qkylrjayo00hqzx.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
