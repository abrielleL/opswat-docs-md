<!-- source: https://www.opswat.com/docs/cm/patch-management/monitor-deployment -->

# Monitor Deployment

The **Jobs** page is the central place to monitor and manage all patch deployments across your environment, including On-Demand, Policy, and Ring deployments for both OS patches and application updates.

In the left navigation, select **Patch Management > Jobs**.

![](https://uploads.developerhub.io/prod/97qW/cmvz66ko8vi0ih31trl4edxp91b2au1pp8irkvva9xlmg7df4fycabaiu8xlpm0w.png)

## **Find What You Need**

![](https://uploads.developerhub.io/prod/97qW/f232qhfbg7qjtiucy4oae5neag2kzpbwphid1i965txuv71ttoi7labufqn0y3yl.png)

| Goal | Details |
| ---- | ---- |
| Open the right deployment tabs | Deployments are organized into three tabs:  1. **Running**: Deployments currently in progress 2. **Schedule**: Deployments scheduled  to run in the future 3. **History**: Completed deployments |
| Identify deployment type and patch type | Look for the badges and label associated with each deployment to identify their deployment type and patch type |
| Narrow the list to specific deployment or patch types | Open the Filter panel and filter by available criteria. Multiple filters can be combined |

### Actions

Select the three-dot menu next to the deployment and choose an action.

| Actions | What It Does |
| ---- | ---- |
| Stop | Stops a deployment that is currently running ![](https://uploads.developerhub.io/prod/97qW/qpen1n4tdvrjck63w9a0trn34x1yz25m5ws3dbgykunc3pcp8dsqnjccyooolu0x.png) |
| Clone & Delete *(only for deployments that have not started)* | Creates a copy of a deployment or removes a deployment before it starts ![](https://uploads.developerhub.io/prod/97qW/h9kkt5ypunapme68qyutrk9v5asv7ygaoeg67i4e3cmmuqpclgm7n70vl18v7xyu.png) |
| Skip *(only for Policy deployment)* | Skips the next scheduled occurrence ![](https://uploads.developerhub.io/prod/97qW/vx43lctpka5p5fjzwl99cj9g7rdtcjgyqs76mdzlu2a5j2h54vkh9539x9bn4rnd.png) Note* Skipping a policy occurrence affects only the next scheduled run. Future runs remain unchanged.* |
| Start *(only for ring deployments configured One Time — Manual Start schedule)* | Starts a deployment manually |
| Create Deployment | Start a new on-demand or ring deployment right from this page ![](https://uploads.developerhub.io/prod/97qW/fbj08boy5u08upbc87ya1zgsu56k7nsanpztggtha8a8ws9kxpk8fjbs2q3a9s6e.png) |

## Monitor Deployments

Select a deployment to open its details page.

The deployment details page includes the following sections:

| Section/Tab | Details |
| ---- | ---- |
| Summary ![](https://uploads.developerhub.io/prod/97qW/gca20x3hxd78gvbvnarkxcoi6vdo1qxwyo3mkd4gy0qgn2ev6m3q8svuqeqt6nst.png) | Overall deployment status |
| By Patch ![](https://uploads.developerhub.io/prod/97qW/69rlvwerufvs49qtxqmspta1hyco0q27ie0i53ll1jnro166m2sx284kqypmbn4n.png) | Track patch-level status (OS) |
| By Application ![](https://uploads.developerhub.io/prod/97qW/i1h0io5ruuw8328pzkqh6hadmyldx3blttpwc5fhajut7mfdqazbwrjgligczht7.png) | Track application-level status |
| By Device ![](https://uploads.developerhub.io/prod/97qW/smi1c4kxviadolouf9wx1ytg0xndlu93c17rjmfqwwpjdne73snefpb4myno30i1.png) | Track device-level status |
| Log ![](https://uploads.developerhub.io/prod/97qW/8pvevbyc3lkj7v8xxeeqbir6r4j4qwtw3jjw69ooxxclny3g1fu3z8tnvatrsmob.png) | A complete, timestamped audit trail of deployment activity |
| Ring Tabs (only available for ring deployments) ![](https://uploads.developerhub.io/prod/97qW/38kal9s6caslndmokbdn0es1wdp4ser0m4ks6aavvkxkv1tpup8hlj9li9qq3wl2.png) | See total progress and deployment health across every ring or results for an individual ring |
| Scripts ![](https://uploads.developerhub.io/prod/97qW/vwltpqkm9888gr88rhcy8gckh0ihgzi53kgv4oixd3yw13j5c4ocjt5c5lgcla7j.png) | Track pre- and post-script execution status across target devices and download attached script files Refer to [Deployment Scripts](https://www.opswat.com/docs/cm/patch-management/deployment-scripts) for details |

## Review Deployment History

Open the **History** tab to review completed deployments.

![](https://uploads.developerhub.io/prod/97qW/u3iefuuh40xp03s67ju4cc1msvjvp4xhtlounc08dycdv1cyip3rzr5ur2c75twl.png)

You can:

- Use Search to find a specific job by name
- Use Filter panel to filter by Type (On-Demand, Policy, or Ring) and Patch Type (OS or Application)
- Select a deployment to view its full details
- Select the download icon for its execution report

## Related Resources

- [Missing Patches: ](https://www.opswat.com/docs/cm/patch-management/manage-missing-patches)Find and act on missing patches and outdated application across your environment
- [Patch Dashboard](https://www.opswat.com/docs/cm/patch-management/patch-dashboard): Get a single-pane view of your environment's patch posture
- [Custom Patch Reports](https://www.opswat.com/docs/cm/patch-management/custom-patch-reports): Configure point-in-time patch reports

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
