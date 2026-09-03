<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/how-do-i-solve-windows-defender-issues-on-metadefender-endpoint- -->

# How do I solve Windows Defender issues on MetaDefender Endpoint/MetaDefender IT-OT Access devices?

> **Check Your Product:**
>
> This article applies to Windows Defender, the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows 10 or 11 systems.

The following article covers three common MetaDefender IT-OT Access device compliance warnings that users may encounter when running Windows Defender in conjunction with MetaDefender IT-OT Access/MetaDefender Endpoint

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Anti-Malware**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/uz2hfrr7pdwi7dvd2k1fsg1ssbtnv69nby8vnmtc7sd1225qbwuovo7g602fpovt.png)

## MetaDefender IT-OT Access Compliance Warning: Windows Defender - No Successful Scan Recently

### Windows 11

1. Open the Windows Start menu, search for Windows Security, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/qdu2jnkp81vftk997wtxy2pebsoa89n4y8gnwz9zwuu6p7u1u0lcc0gw2myuzbdl.png)

2. In the **Windows Security** console, click on **Virus & threat protection** in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/2x2P/kcvlv1wy49rnaead2wg6siznnwb57lrqql2cfcb55e5fn5s8zuz5qd3vbkx2mraw.png)

3. On the **Virus & threat protection** page, click **Scan options**.

![](https://uploads.developerhub.io/prod/2x2P/3nujdi42g740jeaygd88frl1qzp4mkb2c2p1w82b2nbqitwp174yckrlpohde7wf.png)

4. On the **Scan options** page, select the **Full scan** option, then click **Scan now**.

![](https://uploads.developerhub.io/prod/2x2P/mkyr18q5b6ggdug2xfkyesdw3x6034hzny9fozij526qrzkl3914l46aru5wooe8.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/nzyspwbdjy3toyt6127japziiokyq31rlj0p7x2jnsopy9wsvn2ewfeetculio3u.png)

6. Once the app is running, right-click on the Client tray icon and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/a79zgxatky9noovomo8yn33x0nxs5y8wkerv2yzs61uypx5bzxdp669ibom5lwkv.png)

### Windows 10

1. Open the Windows **Start** menu, search for **Windows Defender**, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/xzfpe223tzqoo2a4fwjljzvqz2fgdqwjwjz0wx1y972byv3cczyzdtxslt5vkdqp.png)

2. In the **Windows Defender** console, click on **Virus & threat protection** in the main panel, or in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/2x2P/65gwt9s49jigbxstdd3epz50zvs8i8o08ssb0nmk0nm4blvzcx7nrxco7wz3hfpi.png)

3. On the **Virus & threat protection** page, click **Advanced scan**

![](https://uploads.developerhub.io/prod/2x2P/u0hweval8ppgg7f2kzwis0e6nioze08hd6dxaiuyg9br5b2njjcgfji7pavyufjh.png)

4. On the **Advanced scans** page, select the **Full scan** option, then click **Scan now**.

![](https://uploads.developerhub.io/prod/2x2P/hb1zqu7j6wrxbn3tda0g3cnbn9o3inun21tdefswtjzwqsjp3lk0iaguxdez821l.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/bbmfkhw2zokm7s4orouqdxi1cgn0ne5honid93ae826dg9yvtwgott7ugtqgeeii.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/yexgbcwrsrj93fercx4dcruibvvhffc8xx0g3sstxm5g9b6a7lgh19sf733btt9x.png)

## MetaDefender IT-OT Access Compliance Warning: Windows Defender - Real Time Protection Disabled

### Windows 11

1. Open the Windows **Start** menu, search for **Windows Security**, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/o3ou0v0x84trsz0m9yudgswqx5eoxaq6d8cxp5tt8sqq6j4lu44g7140e9dchniv.png)

2. In the **Windows Security** console, click on **Virus & threat protection** in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/2x2P/uq3511ha822s2564yahrwkbmueuxrr7r5afhs0nb6mchsgc1fimdjsb5wd02jmye.png)

3. On the **Virus & threat protection** page, click **Manage settings**.

![](https://uploads.developerhub.io/prod/2x2P/mcvl070q3ey7ki8csdup8owysebwtpy7173uq7kbrvuu5vnh5m5tb3lu2leoqv4y.png)

4. On the **Virus & threat protection settings** page, enable **Real-time protection**.

![](https://uploads.developerhub.io/prod/2x2P/c03upd7pmjt5qai9m9lr0g6eo1kbi0mljd604q3f28youqrxf5csbxdnxo0kk27x.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/se0z8nmeo7f391ukjxagiwt3li8sn9ewsfpdwghmn024zaf42pf0b2a2oh0956jh.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/u30og04xdubl7kaxg41x49nvichuj8vkoinu3tvf06f85pwpws8gc6hjuhj8d8s4.png)

### Windows 10

1. Open the Windows **Start** menu, search for **Windows Defender**, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/52c5d2ot14xh3hly5tvr86oc8d80n9idnug9p48fu7vvcy4up9b8l2js1ayopdof.png)

2. In the **Windows Defender** console, click on **Virus & threat protection** in the main panel, or in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/2x2P/rjwqf5sxole8rulmv4ga1z5gc4s3pqkgdduyukktpmr6rcqhx9b2sreca4dh2or7.png)

3. On the **Virus & threat protection** page, click on **Virus & threat protection settings**.

![](https://uploads.developerhub.io/prod/2x2P/qqjn7dn2xfsykcgs5hxb2q6i3yz3ebdiiqfu221wemi2g98k8199qxn3dz3lrmub.png)

4. On the **Virus & threat protection settings** page, enable **Real-time protection**.

![](https://uploads.developerhub.io/prod/2x2P/u1m9ac2ze6r5qhpq8l93x222z8x4hd3nytoosq4hg42km54j9j81k9a8qj2bxn60.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/6k9bivdxkxuqyjtqtotlwd6nlwia37at2kbf5oaa8hovegv2htrcrj1b9n0sr21z.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/v2s4yi9lqz7ccvia39h68lbkx1zqkgaqk7a6u20u5i3l4xog6y9oxc29vldwyn5o.png)

## MetaDefender IT-OT Access Compliance Warning: Windows Defender - Virus Definition Out Of Date

### Windows 11

1. Open the Windows **Start** menu, search for **Windows Security**, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/463x82qu4njkvojh03kt7az2pbdz82xt9do8o3sw2xh9o55zwn2i885d5cpedg2q.png)

2. In the **Windows Security** console, click on **Virus & threat protection** in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/2x2P/7iupux3uvmxf5nksv9ytsa7abv3ik3d1uev4qvt0v5yebg3lt7d2733l918cewsd.png)

3. On the **Virus & threat protection** page, click **Protection updates**.

![](https://uploads.developerhub.io/prod/2x2P/sn18xbt2uxmfceaqi4s7u9qm53vbf6mhgxrn0q5oq79bgql48nuiximr8b3z1a8f.png)

4. On the **Virus & threat protection updates** page, click **Check for updates**.

![](https://uploads.developerhub.io/prod/2x2P/p892lj4rqe78issflip9o777sazqj53mr9miex1wqiw68ll4fw2zr85wz6eyothe.png)

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/sm0icj3gl6i98ey2akoerddenw5dvvqbuui8z8ix3r254yb35j6v8qqhe16bi0f6.png)

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/00egpt52cw1p62fzgqnf8qa5huqakcwzi9sh70iqzftamko3028yepoae4otyn9q.png)

### Windows 10

1. Open the Windows **Start** menu, search for **Windows Defender**, then launch it.

![](https://uploads.developerhub.io/prod/2x2P/8i7f2mbwaacgbnkkdrtxbybusndrgwbt3u2mb1c923qqytxvdydeoldzo8yb1119.png)

2. In the **Windows Defender** console, click on **Virus & threat protection** in the main panel, or in the left-hand navigation panel.

![](https://uploads.developerhub.io/prod/2x2P/nclldffuicrptrc20pcqdvbzyel6oy63zph0yuwj7yaqgleqsfe56ealehh0u4rp.png)

3. On the **Virus & threat protection** page, click on **Protection updates**.

![](https://uploads.developerhub.io/prod/2x2P/453zk8h2fwk3eahdj6gpgn89z8w9mqbwj48d74mn8pn6qv7pkj132dkdp49d82px.png)

4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT-OT Access**) and select **Run as administrator**.

![](https://uploads.developerhub.io/prod/2x2P/h2be3ofyaaw2a4l27510b5nl2s264enrub43cal9ybfs2hq24dgv17dnnzmabuxj.png)

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

> **Please note:**
>
> This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT-OT Access servers again.

![](https://uploads.developerhub.io/prod/2x2P/mc46cfntj17yeoy8i82fr2w1g62zkzn43t4utq5xmxj5j4jsr65eqawuhgdmuweo.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Windows Defender Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
