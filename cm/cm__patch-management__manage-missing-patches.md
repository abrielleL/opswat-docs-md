<!-- source: https://www.opswat.com/docs/cm/patch-management/manage-missing-patches -->

# Manage Missing Patches and Outdated Applications

 The Patches page is where you review missing OS patches and outdated third-party applications detected across your managed endpoints.,

In the left navigation, select **Patch Management > Patches**.

It has two tabs that work the same way:

- **Operating System**: missing OS patches across all endpoints.
- **Third Party Applications**: installed applications running an outdated version.

The workflow below applies to both tabs.

![](https://uploads.developerhub.io/prod/97qW/xytgmoo7b59lj7t7sdbtu4rhmi8kmktmu8yr2rxis18fp9q6awx3qmmzls0v8uje.png)

## **Find What Matters**

![](https://uploads.developerhub.io/prod/97qW/mfoh5yfewbjmi64zpqu4395dz24cwbx5gsnd6e7zoeutr9afxj282r9dndg0c1ha.png)

| Goal | How to do it |
| ---- | ---- |
| 1. Find a specific patch or application | **Search **by patch name or KB number, or by application name |
| 2. Focus on a specific group of endpoints | Select one or more endpoint groups from the** Groups **dropdown |
| 3. Export data for reporting | Select** Export** to download the current patch list. |
| 4. Narrow your results | **Filter **by SLA Compliance, Category, Severity, Approval Status, or OS |
| 5. Review aging vulnerabilities | Set a** Timeframe** to show items that remained missing or outdated for a specific period |
| 6. Prioritize upcoming SLA due date | Set **SLA Due Date** to identify patches that are overdue or approaching their due dates |
| 7. Tailor the columns you see | Use** Display** **settings** to show or hide columns such as Severity, Release Date, or CVE count |

## **Take Actions**

1. Select the checkbox next to one or more patches. The** Actions** menu becomes available.
2. Open the** Actions** menu and choose the action that fits.

![](https://uploads.developerhub.io/prod/97qW/xi8x9mqu4wzeh87bomup13q6cuz4asmoh1os3zdp3x1bzk5331njf819ig3zweei.png)

| Action | What It Means |
| ---- | ---- |
| Deploy Now | Starts an immediate, on-demand deployment to the affected endpoints. |
| Approve for Scheduled Deployment | Approve the patch for use in scheduled deployment. |
| Reject for Scheduled Deployment | Excludes it automatically from scheduled deployment.  |
| Edit Tag (OS only) | Apply or update tags to help organize and filter patches. |

Note  After you approve or reject an item, its** Approval Status **updates in the list.

## Investigate Patch Details

To view more information about a patch, select it from the list.

The patch details page provides several tabs and section to help you assess impact and determine the appropriate action.

| Section/Tab | Details |
| ---- | ---- |
| Summary ![](https://uploads.developerhub.io/prod/97qW/odzhcjjq65v22s14zljypxb82c0mcfodt8e79oc2wxxk2ugpnl4wzg8en8cf0rik.png) | View all key details about this patch |
| Vulnerabilities ![](https://uploads.developerhub.io/prod/97qW/5sqky4kive6iglc6tkihn577v4tmh5fw3ki6nifof7vb21qet6vfd40jf853x6c9.png) | Review the CVEs and security vulnerabilities fixed by the patch |
| Devices ![](https://uploads.developerhub.io/prod/97qW/64lik7hwtuww893lzwlq1s43psjpc5n11sxunlux31gop2nwfv5mxgj8lq2af8cq.png) | See all endpoints that are missing this OS patch, or are running this outdated application version |
| Deployments ![](https://uploads.developerhub.io/prod/97qW/bhhodou3usnwunymb9oxth49zzp6yt5ah4qyxjgvqr305685nzil4u3ads308qq2.png) | Review existing deployments that already target this patch |

Note From the patch detail page, you can open the **Actions **menu or choose** Deploy** to start an on-demand deployment for that specific patch.

![](https://uploads.developerhub.io/prod/97qW/lyplgdvo5k123gr2qm5lucf5jsweil1vis0txuyds4kh02a9ddl7r8pclfhe7k7h.png)

## Next Steps

- Push an urgent fix with [On-Demand Deployment](https://www.opswat.com/docs/cm/patch-management/on-demand-deployment)
- Automate recurring patching with [Policy Deployment](https://www.opswat.com/docs/cm/patch-management/policy-deployment)
- Track a specific deployment in [Monitor Deployment](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)
