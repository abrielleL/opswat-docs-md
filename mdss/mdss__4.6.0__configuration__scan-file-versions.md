<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/scan-file-versions -->

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

![](https://uploads.developerhub.io/prod/k8zL/hucaoslsobdvd7phnkj7v00pq2ahik5nt4ermzivp1tuwshdxjhw2ru8hywiw3am.png)

## Use Case

This remediation type is particularly useful when:

- Multiple versions of the same file may exist across different environments.
- You need to ensure that all versions comply with security and compliance requirements.
- You want quick visibility into which versions are safe and which are blocked.

## Reporting

During or after a scan with **Scan File Versions** enabled, the report provides additional insights:

- **New Column – File Versioning**: A dedicated column displays the number of detected versions for each file and indicates if any of those versions are blocked.

![](https://uploads.developerhub.io/prod/k8zL/vbvevdaepcv1ewnhs5se921bi79fhr6zosictdzjvtirukl8iltetj3hxxoh51zi.png)

- **Filtering**: The report includes a filter to show only files that contain blocked versions.

![](https://uploads.developerhub.io/prod/k8zL/pok3jjtjb0qzxzed66qas8w9jvwrs9qybmdcq0ic78g0punjok4y4kjrz61yzegj.png)

- **Individual File Report**: Within a file’s detailed report, a new column lists all discovered versions. Clicking on a version displays its scan result.

![](https://uploads.developerhub.io/prod/k8zL/4phmtdcijlk7g378qf25l7pedl6ttsiffpkg75ryeeffurk5qoe8tlzcarrqwcy9.png)

![](https://uploads.developerhub.io/prod/k8zL/f86jsn5a0mhnggbzpte50soeet5c9ccs63me8z8zjt0ntiabot0fza9x38smm1z5.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
