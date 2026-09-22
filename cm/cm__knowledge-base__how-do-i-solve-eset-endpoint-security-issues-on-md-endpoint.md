<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-eset-endpoint-security-issues-on-md-endpoint -->

# How do I solve ESET Endpoint Security issues on MetaDefender Endpoint devices?

> **Check Your Product:**
>
> This article applies to ESET Endpoint Security for Windows, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

The following article covers three common My OPSWAT Central Management device compliance warnings that users may encounter when running ESET Endpoint Security in conjunction with MetaDefender Endpoint.

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Anti-Malware**.

Please follow the relevant instructions below.

## My OPSWAT Central Management Compliance Warning: ESET Endpoint Security - No Successful Scan Recently

1. Launch **ESET Endpoint Security** for Windows.

![](https://uploads.developerhub.io/prod/1yda/ky41dbxrdf6oozo8m1am4q87lcgpbhyig9j2mlt1fkrhfpyvb8weu5ushwwse8qh.png)

2. Click **Computer scan** in the left-hand navigation bar.
3. On the **Computer scan** page, click on **Custom scan**.

![](https://uploads.developerhub.io/prod/1yda/oepcu8niqlgom2ni2y9ksf5ot1ma2djyzeq17gwmkplkbwpn3c3omwca1pvljinb.png)

4. From the **Custom scan** pop-up window, select **Local drives**, then click the **Scan** button, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/ko1an87w891zinck4o6hw5arhjuavwsh6v2uglq7qkoglxz22sljc0yo9u720p1k.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/dim5e1y6wgmg6667wf3cmcfhpw4kt9ew7k4k3gevu5gomiw2va1zizvb58va4m17.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/tpzjocpkef63hfkp9e56hxrp3b018r02827f31zyhs38t6mtwz1ktrqcdtgksqeu.png)

## My OPSWAT Central Management Compliance Warning: ESET Endpoint Security - Realtime Protection Disabled

1. Launch **ESET Endpoint Security** for Windows.

![](https://uploads.developerhub.io/prod/1yda/npeojx52h0uhlwc9ag1tovx3g51s323zo7y5llmx1t9w8eokeapleg8pntoxx4e2.png)

2. Click **Setup** in the left-hand navigation bar.

![](https://uploads.developerhub.io/prod/1yda/794zuf2w61nkxjiz66rubbi1cwj2h6c8nyw4h83pbs9zki4hqaxovkni19t4dh5a.png)

3. On the **Setup** page, click **Real-time file system protection** to enable it.

![](https://uploads.developerhub.io/prod/1yda/kshq3ucovaz6n6azshxu93nxpown38n33kd5w6k4fo0kox7t11thvvimlxwgmzjd.png)

4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/lpmkkvah9srasdrfhbhdx6aiamlxlxwgtcjjx6uigv1mo5idi1joohhicmgnx030.png)

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/fa3nkrx0cwyk14zw7pejwhf4kwl89027xlg73xu7g9b83g1t9376583ek35qseyk.png)

## My OPSWAT Central Management Compliance Warning: ESET Endpoint Security - Virus Definition Out Of Date

1. Launch **ESET Endpoint Security** for Windows.

![](https://uploads.developerhub.io/prod/1yda/79ysocaame9eib5y55uxpb94cknvsnh3lurcwswy8ctbihbstzdwq7ebrsd9i2bm.png)

2. Click **Update** in the left-hand navigation bar.

![](https://uploads.developerhub.io/prod/1yda/7mcwgszktrl9tv0p54w8nuiu3gjsmoxdo1e501uhf6zahyz3p53x8umcebvfyxmi.png)

3. On the **Update** page, click on **Update virus signature database**.

![](https://uploads.developerhub.io/prod/1yda/t8wdvutryap5fbb3syb1737r7t66xhagj129cm3gig2dlrcvf2sonztn9sbxjuf0.png)

4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management** and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/ag867mfxel9insxylyrah2uju6r10wcez97u2dnghvph4u5bn14rb5hfm0dm910f.png)

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/jdt4iwxdrfkskvdtmapf0gldvwx5apingjxmxvcpakiiw1s1j6p76k145r049thn.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience ESET Endpoint Security Issues On Your** **MetaDefender Endpoint/MetaDefender IT Access** **Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
