<!-- source: https://www.opswat.com/docs/cm/patch-management/policy-deployment -->

# Policy Deployment

Policy Deployment keeps endpoints patched automatically, on a repeating schedule, so you don't have to trigger every deployment yourself.

The process is the same for **Windows patches **and **Application updates**.

![](https://uploads.developerhub.io/prod/97qW/fsqtora9r72fjoekf5nxv3xdysckmuy7sgpe6oxsypzew1bp24jii5uk89lwhs3r.png)

## Start a Policy Deployment

1. In the left navigation, select **Patch Management > Policies**
2. Select **Create New Policy**

## Configure Policy Deployment

Note Policy deployments run on **Windows devices **only.

| Configuration | Details |
| ---- | ---- |
| Name and describe the deployment | Enter a Name, a short Description, and any Tags you want to filter by later ![](https://uploads.developerhub.io/prod/97qW/emg10uei2uu06k6av1i6ins6qv7uximzuhkfclp8fuxfgxw3hdzkslku600bs0wz.png) |
| Enable Window and Application patch policy | Use the Enable OS Patches Policy and/or Enable Application Patches Policy checkbox ![](https://uploads.developerhub.io/prod/97qW/39b5a9k6vipnlojx43ucz2nqefy2jgbn16xwtm0nz05a5382cdzeejes59mxcvmr.png) |
| Decide how often it runs | Set a Recurring Schedule. Daily, Weekly on one or more selected days, or Monthly on one or more selected days ![](https://uploads.developerhub.io/prod/97qW/5dr1qf9qpq9p3d88qr358tuhkhzw5w7a094lwaceezag3zc1q8brq1bbdy3rfwq9.png) |
| Control restart and user notifications | Configure Reboot Options (Windows) or Update Notification (Application) to reduce user disruption ![](https://uploads.developerhub.io/prod/97qW/ficzv9hn1nxrcnu09783cwnexgo9ye69lb6x617xzq8tff3l0nv2bc2byjrjti8n.png) ![](https://uploads.developerhub.io/prod/97qW/goj5q50nwk80jfvzc3vemm8lv3cgbmwsy951f9nmab54fntjpx7zv3r5jh1l5p0i.png) |
| Choose what gets installed | Use condition-based selection to automatically include patches or updates that match criteria. If you set multiple criteria, a patch only needs to match one to be included ![](https://uploads.developerhub.io/prod/97qW/x70lbdxn2euzpct1c1mbci3d07uoroy2j2p100olvdbnwwjdvct0luovfjwswe9c.png) Note* Rejected and unsupported items are automatically excluded, even if they match your selection criteria.* |
| Get notified when it's done | Add one or more email addresses under Report to receive a summary ![](https://uploads.developerhub.io/prod/97qW/rl51j2sr4r5yhvy08w3o8sam22u80qiknqy80xlcry3lpaottwockhl5o0fpje7e.png) |

## **Assign Patch Policy to Endpoint Groups**

To apply the policy, assign it to one or more endpoint groups.

- Navigate to **Inventory > Groups** and select a group.
- Open the **Settings** tab.
- In **Patch Management Policy** section, select your policy from the dropdown menu and save your changes.

The policy will be assigned to the group and will run automatically according to its schedule.

![](https://uploads.developerhub.io/prod/97qW/2mxxxcav8qtr05mtoocwkg1axpb9go6wvllokpaa1sgb5qthhlqw6jnzrrcug7fg.png)

## Next Steps

- Track a specific deployment in [Monitor Deployment](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)
- Configure point-in-time patch reports with [Custom Patch Reports](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports)
- Set real-time alerts for key patch events under [Patch Notification](https://www.opswat.com/docs/cm/patch-management/patch-notification)
- Define SLA timeframes to maintain compliance visibility via [Patch SLA](https://www.opswat.com/docs/cm/patch-management/patch-sla)
