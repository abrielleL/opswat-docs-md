<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-windows-defender-issues-on-metadefender-endpoint- -->

# How do I solve Windows Defender issues on MetaDefender Endpoint/My OPSWAT Central Management devices?

> **Check Your Product:**
>
> This article applies to Windows Defender, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Windows 10 or 11 systems.

The following article covers three common My OPSWAT Central Management device compliance warnings that users may encounter when running Windows Defender in conjunction with MetaDefender Endpoint

These warnings/flags are triggered by device issues and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Anti-Malware**, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/rkmkbm4ytbwzuavcz7fj0ziwz1w0qnmmv57nsjhg48d0pxhpo9gv8olczvi7dsh1.png)

## My OPSWAT Central Management Compliance Warning: Windows Defender - No Successful Scan Recently

### Windows 11

1. Open the Windows Start menu, search for Windows Security, then launch it.

![](https://uploads.developerhub.io/prod/1yda/5t30bzwi7mu8eajgzghv3xpqqgd2uqa6xy0i6xcx44edkvd6ste3v38dlm2z0vyk.png)

2. In the **Windows Security** console, click on **Virus & threat protection** in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/yd68xukrxmhum00ofpw0j912xc5p90a98vox9fitrrk1xw0tbkpwibm1m54pyu7h.png)

3. On the **Virus & threat protection** page, click **Scan options**.

![](https://uploads.developerhub.io/prod/1yda/33wirjieevgytdf5nrcjbol9v2hvg5cn0ciatws7ucah7t6s5szok7tw3pfo6wvp.png)

4. On the **Scan options** page, select the **Full scan** option, then click **Scan now**.

![](https://uploads.developerhub.io/prod/1yda/epik2mr12lw8latjubv8st0al8fwii8vpap4kyoz877kzgrxelconisaimdxfd81.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/jwgrw7qs4mscw9smuvmygidbye5llslpuegvcnnhhh3mkjhxrq1mkjkc7nsx1a4m.png)

6. Once the app is running, right-click on the Client tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/uzxw7yhzfz81kyu94y6syomp36gyqf6y1vilcmmgdcop7gexgqianf4fe4ybkjeh.png)

### Windows 10

1. Open the Windows **Start** menu, search for **Windows Defender**, then launch it.

![](https://uploads.developerhub.io/prod/1yda/ow9dqziso2nhek2ld36p0i8rxqig0fwgstxcw1zoo1mmgmfz78w6keb6fg5u8g81.png)

2. In the **Windows Defender** console, click on **Virus & threat protection** in the main panel, or in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/wj0cm1t9ob64nmbe6lhxm38fikqn08lsi1nxksr7bqpmdtsdxa2k57oxixis6pqr.png)

3. On the **Virus & threat protection** page, click **Advanced scan**

![](https://uploads.developerhub.io/prod/1yda/2a02ruxct4lx0rhwgu3jutmw2h7gcud32hhqmh1r1d2vze0f9j30ojznslljd258.png)

4. On the **Advanced scans** page, select the **Full scan** option, then click **Scan now**.

![](https://uploads.developerhub.io/prod/1yda/31f2u6jdupem8ey1zjmqezybkpa48f35zad94qb5d4kt7cihc4idyilu3467u4d1.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/ovdav71xu5umcmcv3lwbpxqmg1fxooxadjhkw6663lwrwy9ylz4u0j1st0dkr6qn.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/9yrsolbvkdz0uj7nf39pyqxphh8dqfj6lk80xhtidxdsnhkns3i4322003koqwak.png)

## My OPSWAT Central Management Compliance Warning: Windows Defender - Real Time Protection Disabled

### Windows 11

1. Open the Windows **Start** menu, search for **Windows Security**, then launch it.

![](https://uploads.developerhub.io/prod/1yda/ikkwbwd969bl0prjm28gvw8vwn7ni44em4vl0vs1vd5ie79g8v6faze0kyugo4cj.png)

2. In the **Windows Security** console, click on **Virus & threat protection** in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/x4tb9vyq16l5z35lmma6kd1tnutcib6jj3tmramw05debiczirlsspufowxjh1ib.png)

3. On the **Virus & threat protection** page, click **Manage settings**.

![](https://uploads.developerhub.io/prod/1yda/vj5ro70nnuwehkmnia2lsxwdwpu81w9okkcq21atnonaixhf6kio65g2a3txody2.png)

4. On the **Virus & threat protection settings** page, enable **Real-time protection**.

![](https://uploads.developerhub.io/prod/1yda/gc9hm8bz76m5duwr2o3dmbmeauu8z5k0ootvsju3674jccp5pqi0utjngr8xsfr6.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/q0ffigizdtk61kbb3iddpb43q7jqclzqc3ahv5wf8spv1d2tsrwqo979kg3ctvo9.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/bmtfh97f6z2hkq59cmcbikvs3p8pwzeq7b3yxlsizwtof4zoxnu4ohetn4ylistq.png)

### Windows 10

1. Open the Windows **Start** menu, search for **Windows Defender**, then launch it.

![](https://uploads.developerhub.io/prod/1yda/v0vmz3fd64eg1biwpwkvwfmdkac76txu9ljx51rxzi4kgf8icxx55ho87ukst4ge.png)

2. In the **Windows Defender** console, click on **Virus & threat protection** in the main panel, or in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/0deadlxvb6caqy014uvx7fp4mburgoqb70fnz8ou5yp3ai56p2n08otppaf0k3gt.png)

3. On the **Virus & threat protection** page, click on **Virus & threat protection settings**.

![](https://uploads.developerhub.io/prod/1yda/bhgqb1rsxoil39djyzny8mmkpplxzs9gtkbjzbjqe6m67zs2s9jmkabqysa0buww.png)

4. On the **Virus & threat protection settings** page, enable **Real-time protection**.

![](https://uploads.developerhub.io/prod/1yda/o2b9zv9p4thtixnf7j656rjhferzqmgtti0a9968shzg5n62eztn7mk3t2dt1mxi.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/98kjhyhdxz3s4sukeh9p1f3rjglueb7oi5o4ckguwkwsittkmlcycklpsmdxbrc2.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/1pz1ju4s126jx70bd80is41zb1rrs9a0yus4kku175s2yc8ejh0gswzso3qbkgq9.png)

## My OPSWAT Central Management Compliance Warning: Windows Defender - Virus Definition Out Of Date

### Windows 11

1. Open the Windows **Start** menu, search for **Windows Security**, then launch it.

![](https://uploads.developerhub.io/prod/1yda/jq90a62dkaerxp0f6yi9h0d9ppira3grs9acnxuqiqowi4mki95n93wf7iqtkr4y.png)

2. In the **Windows Security** console, click on **Virus & threat protection** in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/b398didwgkuffh0w4u5ijprje9mek3jg0s3jprbd3i2ywqio3udiktiekgsqb6is.png)

3. On the **Virus & threat protection** page, click **Protection updates**.

![](https://uploads.developerhub.io/prod/1yda/hslo32m25s26i7mwmuep2zrlczpdifgkjnpmb1r6jpbq665xxq6iehtm4sx239ut.png)

4. On the **Virus & threat protection updates** page, click **Check for updates**.

![](https://uploads.developerhub.io/prod/1yda/osdxd52m46t7seb5lzsauo3dwnr1bl8r2vt6o3o0b91pgcb66kkyks06xbat490u.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/83zxjx3kszss57bnmc0v1ix0tfczmcit7tz7m86s4qgc0c8on5w7ug78zvyze7w4.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/l9cv3llx6azn77z7961y5wjwx2k3e3v7mxtopk8adroasbagu99l8gyb3dc97z9z.png)

### Windows 10

1. Open the Windows **Start** menu, search for **Windows Defender**, then launch it.

![](https://uploads.developerhub.io/prod/1yda/l9ip4v2x942n5a0xll51e9l2jsq814ypntcf3kz5uqluiw3tyzzwqqcivorf1kaf.png)

2. In the **Windows Defender** console, click on **Virus & threat protection** in the main panel, or in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/1yda/hjdp29z4pbboh53xu7kv0ar7prl2uyuzanasjxtg8t0feyxfaswlvb2zg70koxnr.png)

3. On the **Virus & threat protection** page, click on **Protection updates**.

![](https://uploads.developerhub.io/prod/1yda/tu8r6bsuqieulbdrkq2vdd9ykrwoc96uzsssa9p9llt45tujou7kshqe7mdnjk20.png)

4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **My OPSWAT Central Management**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/1yda/admi5ft85c6rwf8pm968wqrbhcjmfdpoppq4cvi85jzetdpawymk1ecre3cbnpjz.png)

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please Note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the My OPSWAT Central Management servers again.

![](https://uploads.developerhub.io/prod/1yda/lesqjwhnwnsmipqulz0kgydhfgpcy4j0hb9fnkpczhvgywe9lbni6gynooi5806u.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Windows Defender Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
