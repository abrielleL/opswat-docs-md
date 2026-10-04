<!-- source: https://www.opswat.com/docs/cm/patch-management/custom-patch-reports -->

# Custom Patch Reports

Administrators can create custom Patch Reports to share patching progress with stakeholders, prove compliance, and track remediation outcomes across operating systems, third-party apps, and deployment jobs.

- [Create a Report](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports#create-a-report)
- [Preview a Report](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports#preview-a-report)
- [Report Details](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports#report-details)
- [Report Structure](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports#report-structure)

To view and manage your reports, navigate to **Patch Management > Reports**.

![](https://uploads.developerhub.io/prod/97qW/2g3t58lbvqc6byzg843gcha9dgnxfmn9pkq5ssrmqm5huoz3fje71u90tmta9zce.png)

## Create a Report

1. From the Reports list, select** Create Report**.
2. Fill in the configuration fields, then select **Preview** to review the output or **Save** to store the report.

| Configurations | Details |
| ---- | ---- |
| Report Name ![](https://uploads.developerhub.io/prod/97qW/8946k0mh8xdym80w2gfyc132batmrc7k3ai85z39xh1a2ozr7f5w314tu54ky54c.png) | Enter a clear, recognizable name that appears in the report list, header, and email subject |
| Generating Schedule ![](https://uploads.developerhub.io/prod/97qW/ouktkv4y8t3i0nokpqqrb3u647a04n8uxthr3pyke85k4azb7umds5tzne0sy7e9.png) | Choose how often the report runs |
| Time Frame Note* Time Frame configuration is only available on ****Patch Deployment**** reports. * ![](https://uploads.developerhub.io/prod/97qW/dgegxjq39p59a1iyr3djuqd3h0k9jfed7j3nk1ipde9gl0loonude4pl9bwte1gk.png) | Define the reporting window |
| Groups ![](https://uploads.developerhub.io/prod/97qW/gdfxfozjf0rh38kbz3fg0d7l2aufv1zl4kg7dcdthbl25fckvtmfgbvbofixu3oq.png) | Select the device groups to include in the report. |
| Report Type ![](https://uploads.developerhub.io/prod/97qW/2hw252eal7zyomkhnve3jcm6k6m7q34zp0wgcfyftytp3mng2xegsp2pkyrjrn2n.png) | Select the focus of the report. This determines the metrics, charts, and details included in the output |
| Detail Report Hierarchy - **Group by Devices**: Lists each device with its associated patches, applications, or deployment jobs - **Group by Patches**: Lists each patch with the affected devices (available for Operating System and Patch Deployment type only) - **Group by Applications**: Lists each application with the affected devices (available for Third-party Application only) ![](https://uploads.developerhub.io/prod/97qW/64yn0hwke4zauiopwvo0in425vhidx3atd9actodpxgovj6y4m2ynom3tg4gtmse.png) | Define how detailed data is organized in the report, based on the selected report type |
| Report Scope Filters Note *The available filters depend on the selected Report Type.* ![](https://uploads.developerhub.io/prod/97qW/ufohnsnzeiwk90ryfpm4iugl10bemt5zyselhpq69na9skqp0uw3ji4gsoguoj9o.png) | Refine the data set with one or more scope filters.  |
| Share Report by Email Note* You can update the recipients anytime by editing the report configuration from the Reports List page.* - Tick **Summary** to include the high-level summary section in the report (available for PDF format only) - Tick **Detailed Report** to include the per-device, per-patch, or per-job detail section ![](https://uploads.developerhub.io/prod/97qW/0qar40ucy3msanzo5nztpa6qq2fpzx7yvralndhcsausrz1xtrhbtr0g5vqtem5f.png) | Enable this option to automatically email the report to selected recipients each time it runs. |

## **Preview a Report**

After completing the required fields, select **Preview** to see a sample version of the report. Click the **X** symbol to close the preview.

Note* The preview is a sample for reference only and does not reflect actual generated data. The full HTML report is created only after you ****Save**** the configuration.*

![Select **Preview** to see a sample report](https://uploads.developerhub.io/prod/97qW/uqru1m7axauak17oenv8bkp1d54gti4une05w0hfqli1ne0jetfg36h920fn7mq6.png)

## Report Details

From the Reports List, select a report or choose **View details** to open its detail page. This page serves as the central hub for running, editing, and managing generated copies of a report.

| Report Section | What It Shows |
| ---- | ---- |
| Summary | Shows the report configuration ![](https://uploads.developerhub.io/prod/97qW/e8m28axgtqzra4f5gl3hpnzoa9sqzrdxa4z7d8582w27512hr5cywfjpfrcaxlkf.png) |
| Generated Reports List | Lists each generated copy of the report ![](https://uploads.developerhub.io/prod/97qW/8858ryar2jj0fu2iivhmtvufdtnztobz7rt4tztnmzmc94irjmxrpwlerdifz664.png) |
| Export a Report | Select **Export as** from three-dot menu. ![](https://uploads.developerhub.io/prod/97qW/elhgxtetckz27wm84oomrwooqgerzt2bl5lz3vk5q0ehhwi219ejwnbsgi3grtxs.png) |

## Report Structure

Every generated report follows the same three-part layout, regardless of type:

### **Cover Page**

The cover identifies the report and its scope at a glance:

- The report title, a one-line description
- Generated, Schedule, Group, Time Frame, Device, Device Status, Patch, and Patch Status.
- Job Status, and Deployment Type (only for Patch Deployment report type).
- A Confidential notice marks the report for internal use only.

![](https://uploads.developerhub.io/prod/97qW/vhoz8ndsntkupcshszk8k61use1m2ymmhsdsf84uoqcrj8ntrqel8qg1j4ta3tnk.png)

**Summary**

![](https://uploads.developerhub.io/prod/97qW/2jvo2opt4xalivd0whqgbyobul9eqsvuyuiv2lnabe6224tvb2uawqpdab1i54sk.png)

| Report Type | Shown Info |
| ---- | ---- |
| Operating System | - **Device Summary**: Devices with Critical Missing Patches, Missing Patches, Deployment Issues - **OS Patches Summary**: Total missing patches, critical patches, pending approval - **Missing Patches by Severity**: A breakdown of missing patches by severity levels (Critical, High, Medium, Low, and Unknown). - **Critical Patch Age Distribution**: Critical patches based on how long they have been missing (from under 7 days up to 90+ days). |
| Third-Party Application | - **Device Summary**: Devices with Critical CVEs, needing updates, deployment issues - **Application Summary**: Total critical vulnerabilities, applications affected by known CVEs, and patches pending approval. - **Application by Severity**: Grouping applications by their highest active CVE severity level. - **Application Vulnerabilities Trend**: Tracking cumulative CVE exposure across installed application versions. |
| Patch Deployment | - **Job Summary**: Total jobs, executed jobs, total devices targeted, and overall success rate. - **Device Install Outcomes**: Displaying results such as Completed, Install Failed, Incomplete, Partially Installed, Pending Reboot, and Unreachable. - **Deployment History**: Showing completed jobs over time, helping identify activity peaks and high-failure periods. |

### **Detailed Report**

Includes the full dataset, organized based on the selected Detail Report Hierarchy.

![](https://uploads.developerhub.io/prod/97qW/fkgbfehen8bai2z33yafc3y3ze3787aik3iszgwfjae7uc3dfnf8a1bpvbn6usud.png)

- **Operating System**: Detailed Report can be grouped by **Devices** or by **Patches**.
- **Third-Party Application**: Detailed Report can be grouped by **Devices** or by **Applications**.
- **Patch Deployment**: Detailed Report can be grouped by **Devices** or by **Patches**.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
