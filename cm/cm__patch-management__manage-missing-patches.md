<!-- source: https://www.opswat.com/docs/cm/patch-management/manage-missing-patches -->

# Manage Missing Patches

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

The Patches page is where you review missing OS patches, outdated third-party applications, as well as outdated drivers, firmware, and BIOS across your managed endpoints.

In the left navigation, select **Patch Management > Patches**.

It has two tabs that work the same way:

- **Operating System**: missing OS patches across all endpoints.
- **Third Party Applications**: See [Third Party Applications](/docs/cm/patch-management/patch-centric-third-party-applications) for more details.
- **Driver & Firmware**: outdated or missing drivers, BIOS, and firmware updates across supported endpoints.

The workflow below applies to both tabs.

## [**Find What Matters**](/docs/cm/patch-management/manage-missing-patches#find-what-matters)

| Goal | How to do it |
| --- | --- |
| 1. Find a specific patch or application | **Search** by patch name or KB number, or by application name |
| 2. Focus on a specific group of endpoints | Select one or more endpoint groups from the **Groups** dropdown |
| 3. Export data for reporting | Select **Export** to download the current patch list. |
| 4. Narrow your results | **Filter** by SLA Compliance, Category, Severity, Approval Status, or OS |
| 5. Review aging vulnerabilities | Set a **Timeframe** to show items that remained missing or outdated for a specific period |
| 6. Prioritize upcoming SLA due date | Set **SLA Due Date** to identify patches that are overdue or approaching their due dates |
| 7. Tailor the columns you see | Use **Display** **settings** to show or hide columns such as Severity, Release Date, or CVE count |

## [**Take Actions**](/docs/cm/patch-management/manage-missing-patches#take-actions)

1. Select the checkbox next to one or more patches. The **Actions** menu becomes available.
2. Open the **Actions** menu and choose the action that fits.

| Action | What It Means |
| --- | --- |
| Deploy Now | Starts an immediate, on-demand deployment to the affected endpoints. |
| Approve for Scheduled Deployment | Approve the patch for use in scheduled deployment. |
| Reject for Scheduled Deployment | Excludes it automatically from scheduled deployment. |
| Edit Tag (OS only) | Apply or update tags to help organize and filter patches. |

Note  After you approve or reject an item, its **Approval Status** updates in the list.

## [Investigate Patch Details](/docs/cm/patch-management/manage-missing-patches#investigate-patch-details)

To view more information about a patch, select it from the list.

The patch details page provides several tabs and section to help you assess impact and determine the appropriate action.

| Section/Tab | Details |
| --- | --- |
| Summary | View all key details about this patch |
| Vulnerabilities | Review the CVEs and security vulnerabilities fixed by the patch |
| Devices | See all endpoints that are missing this OS patch, or are running this outdated application version |
| Deployments | Review existing deployments that already target this patch |

Note From the patch detail page, you can open the **Actions** menu or choose **Deploy** to start an on-demand deployment for that specific patch.

## [Next Steps](/docs/cm/patch-management/manage-missing-patches#next-steps)

- Push an urgent fix with [On-Demand Deployment](https://www.opswat.com/docs/cm/patch-management/on-demand-deployment)
- Automate recurring patching with [Policy Deployment](/docs/cm/patch-management/policy-deployment)
- Track a specific deployment in [Monitor Deployment](/docs/cm/patch-management/monitor-deployment)
- Run pre- and post-script with [Deployment Scripts](/docs/cm/patch-management/deployment-scripts)
