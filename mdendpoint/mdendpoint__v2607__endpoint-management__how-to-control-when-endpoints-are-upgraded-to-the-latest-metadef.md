<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-to-control-when-endpoints-are-upgraded-to-the-latest-metadef -->

# How to control when endpoints are upgraded to the latest MetaDefender Endpoint?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint and SDK releases deployed on Windows and macOS systems.

Many MetaDefender Endpoint and SDK customers prefer to phase the application of updates across their managed endpoints.

> **Pro Tips:**
>
> By using an *update control group*, where a certain group of endpoint user groups serve as early adopters of the most recent releases, OPSWAT customers can gain familiarity with new releases in a controlled and specific user environment.

To enable phasing or controlling of Client or SDK updates across your managed endpoints, please follow the instructions below.

1. Go to your MetaDefender IT-OT Access Console and navigate to Settings>Global>Device Agents>Agent and uncheck the Automatic Update boxes, as indicated in the screenshots below.

![](https://uploads.developerhub.io/prod/2x2P/qbg0j85te0x1y8t285yhh4offmgd33fz3kdzko13ngjpn8o3su56mn8jwnblyc2d.png)

![](https://uploads.developerhub.io/prod/2x2P/fhcktd2j07hzv7mopd8aav7si5yt7f78fqthp1gxvi3cqylfuswxi1ap2g9be7zq.png)

2. Click **Save** to apply your settings.
3. Next, to enable auto-updates/upgrades for one or more select groups from the **MetaDefender IT-OT Access Console**, go to **Inventory>Device Groups**.
4. Click on the relevant group, then access the **Settings** tab for that group.
5. Toggle the Agent switch to access update settings for that group, then check the boxes to Automatically update to the specific version, as indicated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/vvb0zrxi23tg6mgxp7lzyyhxbogl1ypgm5rzcccxaymdhhfum77jlbh0a1p4azci.png)

6. Allow the devices in the control group to run with the client for 24 hours or until you are confident that the new Client and SDK versions operate stably in your user environment.
7. Then, you can re-enable global auto-updates/upgrades via the **MetaDefender IT-OT Access Console** by navigating back to the **Global>Device Agents>Agent** settings and checking the auto-update boxes mentioned in step one above.
8. One sufficient time has passed to apply updates across all of your managed endpoints, you can once again disable the global auto-update/upgrade settings.

> **Please Note:**
>
> OPSWAT plans to include enhanced auto-update features in future, so that administrators interested in phasing or controlling updates will no longer need to repeat this process for each update cycle.

> **Support:**
>
> If you have further queries or concerns regarding **Phasing Or Controlling Endpoint Updates, And Enabling Update Groups For** **MetaDefender Endpoint** **and SDK**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
