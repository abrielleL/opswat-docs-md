<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-solve-eset-endpoint-security-issues-on-opswat-client-me -->

# How do I solve ESET Endpoint Security issues on MetaDefender Endpoint/MetaDefender IT Access devices?

This article applies to ESET Endpoint Security for Windows, the current MetaDefender IT Access Console and API, and all MetaDefender Endpoint releases deployed on Windows systems.

The following article covers three common MetaDefender IT Access device compliance warnings that users may encounter when running ESET Endpoint Security in conjunction with MetaDefender IT Access/MetaDefender Endpoint.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Anti-Malware**.

Please follow the relevant instructions below.

## [MetaDefender IT Access Compliance Warning: ESET Endpoint Security - No Successful Scan Recently](/docs/macloud-sdp/kb/how-do-i-solve-eset-endpoint-security-issues-on-opswat-client-me#metadefender-it-access-compliance-warning-eset-endpoint-security---no-successful-scan-recently)

1. Launch **ESET Endpoint Security** for Windows.

2. Click **Computer scan** in the left-hand navigation bar.
3. On the **Computer scan** page, click on **Custom scan**.

4. From the **Custom scan** pop-up window, select **Local drives**, then click the **Scan** button, as illustrated below.

5. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT Access**) and select **Run as administrator**.

6. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

## [MetaDefender IT Access Compliance Warning: ESET Endpoint Security - Realtime Protection Disabled](/docs/macloud-sdp/kb/how-do-i-solve-eset-endpoint-security-issues-on-opswat-client-me#metadefender-it-access-compliance-warning-eset-endpoint-security---realtime-protection-disabled)

1. Launch **ESET Endpoint Security** for Windows.

2. Click **Setup** in the left-hand navigation bar.

3. On the **Setup** page, click **Real-time file system protection** to enable it.

4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT Access**) and select **Run as administrator**.

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

## [MetaDefender IT Access Compliance Warning: ESET Endpoint Security - Virus Definition Out Of Date](/docs/macloud-sdp/kb/how-do-i-solve-eset-endpoint-security-issues-on-opswat-client-me#metadefender-it-access-compliance-warning-eset-endpoint-security---virus-definition-out-of-date)

1. Launch **ESET Endpoint Security** for Windows.

2. Click **Update** in the left-hand navigation bar.

3. On the **Update** page, click on **Update virus signature database**.

4. Open the Windows **Start** menu, then search for **MetaDefender Endpoint** (or **MetaDefender IT Access** and select **Run as administrator**.

5. Once the app is running, right-click on the MetaDefender Endpoint tray icon and, from the pop-up menu, click **Recheck**.

Please Note:

This will trigger the MetaDefender Endpoint to scan all device compliance data and report to the MetaDefender IT Access servers again.

Support:

If you have followed the instructions above but **Continue To Experience ESET Endpoint Security Issues On Your** **MetaDefender Endpoint/MetaDefender IT Access** **Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
