<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-5-2603 -->

# Release Notes for v10.5.2603

| **Version** | v10.5.2603 |
| ---- | ---- |
| **Release date** | March 31st, 2026 |
| **Release Summary** | This release introduces a new level of security control with end-to-end **Patch Management solution** and deeper **Industrial Firewall integration**. It further accelerates security operations through remote **Kiosk support package generation**, precise **custom tag-based filtering** for effortless asset management, and upgraded  **scan session exports** for faster, more actionable analysis. Accompanied by various enhancements and critical bug fixes across **Kiosk**, **Core**, and **Endpoint** to ensure maximum system reliability and protection. |

### **Peripheral Media Protection Solution**

New Features **Auto-Sync Policy for New Kiosk Instances via Group Settings**

New kiosk instances are now automatically synced with predefined policies through group settings, reducing manual configuration effort.

![](https://uploads.developerhub.io/prod/97qW/afdwtiabevcbqd1wdvmuyg0injnmq67tnwep4zit0ktlty7z1y1rm03lp8qhq1dr.png)

New Features **Enhanced Scan Session Details for MetaDefender Endpoint**

Support for viewing scan session details for MetaDefender Endpoint, providing granular insight for easier analysis and auditing.

![](https://uploads.developerhub.io/prod/97qW/s9b1syyuseemaejazshe7wmmtlkyrupq1ngj6aijzl0kxnapzto0ff3z6982m5ks.png)

New Features**Screensaver Upload Support for MetaDefender Kiosk**

Administrators can now upload and manage custom screensavers from My OPSWAT Central Management, simplifying rollout of branded images, videos, or URLs across large Kiosk deployments.

![](https://uploads.developerhub.io/prod/97qW/vs2v2lb2i1bnu6xpz9k53p1lwhetp3ib5ozbn3allotkswnkouu5yie9215y3i6j.png)

New Features **Centralized Certificate Management for MetaDefender Kiosk**

Managing MetaDefender Kiosk certificates is now integrated within My OPSWAT Central Management, strengthening trust and validation protocols during file scanning and transfer.

![](https://uploads.developerhub.io/prod/97qW/29khcvsktq1849pmp49nvz5low6vtw2f710cvsuni5mpiwgsojdjv8srox88cbu9.png)

New Features **Support Package Generation for MetaDefender Kiosk**

Administrators can now generate support packages of connected Kiosk instances directly from My OPSWAT Central Management, without accessing each device individually.

In the **Actions** menu of specific instances, choose **Generate Support Package** to begin.

![](https://uploads.developerhub.io/prod/97qW/hb8oqt4t0udvwqxfe7r8ctn85dda6wzy1vn1jlvri7zlt24zamo0yx3yjefcbytn.png)

Enhancements**Email Notifications for Kiosk Availability and Disconnection Events**

Email alerts are now available when kiosks are offline or remain disconnected beyond a configurable time threshold.

![Navigate to **Settings > Notification Groups** to set triggers for email notification.](https://uploads.developerhub.io/prod/97qW/b4rglqhxrwnw0dppmk7mk6qsdcuzg59txjmxgo9yt64tbq3y9xquxgjhbojgreyj.png)

Enhancements **Dedicated Dashboard for Kiosk-Only Users**

Automatically adjusts dashboard layout for Kiosk-only users, so you only see the data that matters to your environment, making security monitoring faster and more efficient.

![A dedicated dashboard layout for customers managing only MetaDefender Kiosk](https://uploads.developerhub.io/prod/97qW/isov8b1h9k95jzar7c0casn6tgetxiflm37wmvg6aasggswnxfqwknes04etvjoh.png)

Enhancement **Enhanced "Endpoint Last Seen" Widget for MetaDefender Endpoint**

Introducing an enhanced "Endpoint Last Seen" widget to provide clear visibility into endpoint agent connectivity patterns. Streamline troubleshooting and maintain network-wide oversight effortlessly.

![](https://uploads.developerhub.io/prod/97qW/j1xot40rn36a6wc35m060v50599bz02o2m7w9yutxflgfimhdp5s5pc7gsaael87.png)

Bug fixes **Kiosk Workflow Auto-Sync Issues**

This fix optimized the auto-sync mechanism to ensure workflow configurations are pushed consistently to all enrolled Kiosks, preventing server overloads during large-scale policy syncs.

Bug fixes **Kiosk Reporting Mismatch**

Fixed issues that cause Kiosk exports to return inconsistent results for the same date range, ensuring accurate and reliable reports.

Bug fixes **Resolved “Failed to Calculate Hash” Error on MetaDefender Core Scan Results**

Fixed a visual issue where some file scan reports incorrectly showed “Failed to calculate hash” even though the hash was available.

### **Endpoint Security Solution**

New Features **Unified Patch Management Solution**

New unified patch management solution automates end-to-end patching workflows to remove manual tasks and speed up the remediation of critical vulnerabilities.

Refer to [**Patch Management**](https://www.opswat.com/docs/cm/patch-management)  guidelines for detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/u35uxcz5y4zf070pkho0x2x2l4ey4sf0t24ymgizryck1vja1xuavqfwx0h88726.png)

Enhancements**Streamlined Dashboard Experience for Endpoint-Only Users**

Customers managing only MetaDefender Endpoint will now land on the Endpoint Security Dashboard by default upon login, ensuring critical data is front-and-center from the start.

![](https://uploads.developerhub.io/prod/97qW/xmeojogdp7j7z2d46co231f2uqwlk2wv1dslfn5l4rjneiyfmkhgobhyt5n8aifi.png)

Enhancements**Improved Flexibility for Application Control Exception Policies**

Admins can now create application control exceptions by **Device Username** and **Hostname**, making it easier to manage exceptions at scale.

![](https://uploads.developerhub.io/prod/97qW/82t4nl5qle1awyiqln8hi3weahhue0lhp394ez5bf791ni34dqglp6ws0apgcpyr.png)

### **OT and Cyber-Physical Systems Solution**

Enhancements **Enhanced Configuration and License Management for MetaDefender Industrial Firewall**

This update brings enhanced integration over MetaDefender  Industrial Firewall deployments via new Industrial Firewall dashboard, streamlined policy configuration and simplified license management, eliminating operational silos.

Navigate to **Policies**> **Industrial Firewall** to create new policy.

![](https://uploads.developerhub.io/prod/97qW/z4lrf4c0p7kw3dd56vm2d0k0225k5wtq80am8sphih1qpmol46vrpxuy9xfkkhlx.png)

### **File Security Solution**

Enhancements **Improved MetaDefender Core Processing History with Aether Engine**

Processing history now supports the Aether engine, ensuring My OPSWAT Central Management delivers a consistent and accurate representation of threat analysis data.

![](https://uploads.developerhub.io/prod/97qW/aqbfknbofxxz8mwpbp0tmfdgoan41yt9x0dpdc97fr804pvsck2w5jkk5mbgabnk.png)

Enhancements **Update New Verdicts for Filtering**

Introducing new verdict filters in Processing History, including **Exceeded Archive Expansion Factor**; **Allowed Verdict by Threat Intelligence**, and **Blocked Verdict by Threat Intelligence** for clearer security analysis.

![](https://uploads.developerhub.io/prod/97qW/76ie5szk9aik9ip6zcuo8lg2va1kkbcimhye8ej48mwhjx3w0jmww0bt8jxq0rrz.png)

### **Network Access Control Solution**

New Features **Device Block Notifications**

NAC now sends in-app notifications when a device is blocked as a result of a "Device Unresponsive" event. A notification will appear in the bell icon, clicking the notification redirects you directly to the Device Inventory page for immediate visibility and action.

![](https://uploads.developerhub.io/prod/97qW/30w0bcvs8p6eg5ekaw7mitsq6rwigjhcy5dmmyuufbrlywhyugb11zplzl4tc54t.png)

![](https://uploads.developerhub.io/prod/97qW/wqm41cb06175o8gszz2b51nd82b926kt6bto0b5k96rhpw2fmnr0ie1tufw7m8em.png)

New Features **VOIP Device Type Support**

NAC introduces support for a new device type: VOIP. This addition extends the device enrollment use case to cover VOIP devices, allowing administrators to onboard and manage them alongside existing supported device types.

![](https://uploads.developerhub.io/prod/97qW/2wo8ro4km4vmdphsvfyf534nxusm53eb4j0xg1zt78u8qmvzpo4q2or03vwunzkp.png)

![](https://uploads.developerhub.io/prod/97qW/jbi97e3zpxw4qgw8l813pc002imq8qmsbxvf22gc3ljyvz7qru9qfthr9z7vm460.png)

### **Additional Features**

New Features **Inventory Search with Custom Tag Filtering**

Administrators can search for any instances using custom-defined tag keys, making it more intuitive to find and manage inventory across large-scale, multi-location deployments.

![Admins can customize tag keys and values to search through in Inventory.](https://uploads.developerhub.io/prod/97qW/hrzcwi4v45583lfgijavgyfohvns9bsp2qooshejmm2mn6pqiiufyr8sk3cp3rtr.png)

Enhancements **Flexible 24-Hour Time Format Support**

Admins can now switch between 12-hour and 24-hour formats globally, eliminating timestamp confusion in logs and reports.

![](https://uploads.developerhub.io/prod/97qW/yvriu1mrkgzj11njd44atofhsfugtdevo5iukdn43tal466krsu0w2sifrc6ho9m.png)
