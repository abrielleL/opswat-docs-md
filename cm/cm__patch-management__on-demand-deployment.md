<!-- source: https://www.opswat.com/docs/cm/patch-management/on-demand-deployment -->

# On-Demand Deployment

On-demand deployment pushes specific OS patches or application updates to targeted endpoints immediately. Use it for urgent security fixes, critical vulnerabilities, or targeted updates.

The process is the same for OS or third-party application.

![](https://uploads.developerhub.io/prod/97qW/qex8do4cfpwcaflblh8h627usdwv6fab2xeycbmoatl13mxrjjnry8d465ks2by6.png)

## Start On-Demand Deployment

1. In the left navigation, select **Patch Management > Jobs**
2. Select **Create On-Demand Deployment**
3. In the dialog, choose what to deploy:
   1. For Windows Patches
   2. For Application Patches

![](https://uploads.developerhub.io/prod/97qW/sidnzk94cm3ue4cp4s22jt8dknb18v3j78pvvbfoi0th846cn8fkes29edbj2dki.png)

## Configure On-Demand Deployment

Note On-demand deployments run on **Windows devices **only.

| Configuration | Details |
| ---- | ---- |
| Name and describe the deployment | Enter a Name, a short Description, and any Tags you want to filter by later ![](https://uploads.developerhub.io/prod/97qW/emg10uei2uu06k6av1i6ins6qv7uximzuhkfclp8fuxfgxw3hdzkslku600bs0wz.png) |
| Schedule when deployment runs | Set the Date and Start time. Add an End time if you want it to stop automatically ![](https://uploads.developerhub.io/prod/97qW/as4f3163hdeb89vakefoa6lsrgfog5rj3pohrmwk66r7kh4yrctce0z42j9odqu1.png) Note * If no end time is specified, the deployment is marked complete only once every endpoint finishes and reports back to My OPSWAT Central Management. Offline endpoints during the window are marked Unreachable.* |
| Control restart and user notifications | Configure Reboot Options (Windows) or Update Notification (Application) to reduce user disruption ![](https://uploads.developerhub.io/prod/97qW/ficzv9hn1nxrcnu09783cwnexgo9ye69lb6x617xzq8tff3l0nv2bc2byjrjti8n.png) ![](https://uploads.developerhub.io/prod/97qW/goj5q50nwk80jfvzc3vemm8lv3cgbmwsy951f9nmab54fntjpx7zv3r5jh1l5p0i.png) |
| Choose which endpoints get the update | Select All Devices, Specific Groups, or Specific Devices ![](https://uploads.developerhub.io/prod/97qW/a68gitpkxcy77xiw78rrfdocc3t8s3f1ev1ypvv6fhkzq5fmddsx4i9icmbnf0t0.png) |
| Choose what gets installed | Use condition-based selection to automatically include updates that match criteria, or pick Specific Patches / Specific Applications manually ![](https://uploads.developerhub.io/prod/97qW/h81wmwm41vazbgw7vc7ukyy3cej4p9z3mear1zm0rgf47bfzry4y1dvwz9r2x1lg.png) Note* Rejected and unsupported items are automatically excluded, even if they match your selection criteria.* |
| Get notified when it's done | Add one or more email addresses under Report to receive a summary ![](https://uploads.developerhub.io/prod/97qW/rl51j2sr4r5yhvy08w3o8sam22u80qiknqy80xlcry3lpaottwockhl5o0fpje7e.png) |

## Next Steps

- Track a specific deployment in [Monitor Deployment](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)
- Configure point-in-time patch reports with [Custom Patch Reports](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports)
- Set real-time alerts for key patch events under [Patch Notification](https://www.opswat.com/docs/cm/patch-management/patch-notification)
- Define SLA timeframes to maintain compliance visibility via [Patch SLA](https://www.opswat.com/docs/cm/patch-management/patch-sla)
