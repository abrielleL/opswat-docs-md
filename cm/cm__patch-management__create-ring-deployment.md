<!-- source: https://www.opswat.com/docs/cm/patch-management/create-ring-deployment -->

# Create Ring Deployment

Set up a reusable deployment configuration, then stage its rollout into rings in the steps that follow.

![](https://uploads.developerhub.io/prod/97qW/br6id2aew6kejdyqc8ya513j7hxt58bpfb9io6sc44v121tkq75zafqv6p3oefo1.png)

## Create Ring Deployment

1. In the left navigation, select **Patch Management > Jobs**
2. Select **Create Deployment**, then choose **Ring **from the dropdown
3. In the dialog, choose what to deploy:
   1. For Windows Patches
   2. For Application Patches

![](https://uploads.developerhub.io/prod/97qW/3odgg1t35l8vg3uwlextmq2ofqdto0nhan4t69j14p0eu0qwoj88jiypq1dsq8tr.png)

## Configure Ring Deployment

| Configuration | Details |
| ---- | ---- |
| Name and describe the deployment | Enter a Name, a short Description, and any Tags you want to filter by later ![](https://uploads.developerhub.io/prod/97qW/s5724xwzoa1rqqsb6w0ogx4eocuv2f1r0puqq0ugtww0hpbejb1ce3q7bds6h8op.png) |
| Choose what gets installed | Use condition-based selection to automatically include updates that match criteria, or pick Specific Patches / Specific Applications manually Note* Rejected and unsupported items are automatically excluded, even if they match your selection criteria* ![](https://uploads.developerhub.io/prod/97qW/elttqiu4z08wsd66i4bdcv63fq1mzwd494a575a6shrhwo7nvabuej79e43rh9xf.png) |
| Set how often the deployment runs | Set the Date and Start time. Add an End time if you want it to stop automatically. Refer to [Ring Schedule ](https://www.opswat.com/docs/cm/patch-management/how-ring-deployment-works#ring-schedule-)to understand how it works ![](https://uploads.developerhub.io/prod/97qW/wqgh51ie3aihj3od1nh9dk6ookdo83uev3zqbu7yr0tcx005em0ap0kgiohj4p4v.png) Note * If no end time is specified, the deployment is marked complete only once every endpoint finishes and reports back to My OPSWAT Central Management. Offline endpoints during the window are marked Unreachable.* |
| Control when deployments can occur | Configure a Maintenance Window to limit deployments to approved times. Refer to [Maintenance Window](https://www.opswat.com/docs/cm/patch-management/how-ring-deployment-works#maintenance-window) to understand how it works ![](https://uploads.developerhub.io/prod/97qW/zdk3oqp0vr4f6e39bd844tvsnbvnl6b49tdtaynwmc0gzs06cin1zkrgecw6g4v4.png) |
| Stage your rollout across rings | Configure deployment rings under Targets for Ring Deployment. Refer to [Targets for Ring Deployment](https://www.opswat.com/docs/cm/patch-management/how-ring-deployment-works#targets-for-ring-deployment)[ ](https://www.opswat.com/docs/cm/patch-management/how-ring-deployment-works#what-is-auto-promote-and-manual-promote)to understand how they work Note* You can configure up to ****10 rings**** per deployment. At least one ring is required before saving.* ![](https://uploads.developerhub.io/prod/97qW/k9hzzajwcfbawd9lhroh4hd68ewm38br54xshdom2yrzu3352jgcv60rwfbn3axx.png) |
| Control restart and user notifications | Configure Reboot Options (Windows) or Update Notification (Application) to reduce user disruption ![](https://uploads.developerhub.io/prod/97qW/ficzv9hn1nxrcnu09783cwnexgo9ye69lb6x617xzq8tff3l0nv2bc2byjrjti8n.png) ![](https://uploads.developerhub.io/prod/97qW/goj5q50nwk80jfvzc3vemm8lv3cgbmwsy951f9nmab54fntjpx7zv3r5jh1l5p0i.png) |
| Get notified when it's done | Add one or more email addresses under Report to receive a summary ![](https://uploads.developerhub.io/prod/97qW/rl51j2sr4r5yhvy08w3o8sam22u80qiknqy80xlcry3lpaottwockhl5o0fpje7e.png) |

## Next Steps

- Track a specific deployment in [Monitor Deployment](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)
- Configure point-in-time patch reports with [Custom Patch Reports](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports)
- Set real-time alerts for key patch events under [Patch Notification](https://www.opswat.com/docs/cm/patch-management/patch-notification)
- Define SLA timeframes to maintain compliance visibility via [Patch SLA](https://www.opswat.com/docs/cm/patch-management/patch-sla)
