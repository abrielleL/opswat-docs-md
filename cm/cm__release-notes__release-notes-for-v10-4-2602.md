<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-4-2602 -->

# Release Notes for v10.4.2602

| **Version** | v10.4.2602 |
| ---- | ---- |
| **Release date** | January 28th, 2026 |
| **Release Summary** | This release includes new features, enhancements, and bug fixes across **Kiosk**, **Core**, **Endpoint**, and **Drive** solutions delivering centralized update rollouts, richer scan insights, improved reporting, and greater system reliability. With expanded verdict displays, automated notifications, and enhanced integration, this update helps you stay secure and in control with less effort. |

### **Peripheral Media Protection Solution**

New Features **Kiosk Update Rollout**

Introduced phased deployment of Kiosk updates to ensure smoother rollout and improved operational stability.

![](https://uploads.developerhub.io/prod/97qW/pdvs138eidl4bbxtowov9ybk9gfwe0llz961iwyyss9dj3h7ht91g5cm9t7d40wb.png)

Enhancements **Expanded Scan Verdict Display on Kiosk Dashboard**

Enhanced the Dashboard to show additional scan result verdicts for improved visibility and analysis.

![](https://uploads.developerhub.io/prod/97qW/qlxghe07lty4ndpbjecm46022dkev86m0224peprhvgq6y43kt5qsbuvfwz25bj6.png)

Bug fixes **Health Status Reset on Kiosk Disconnection**

Corrected a condition where system **Health Status** did not revert to **Unknown** when the Kiosk instance disconnected.

![](https://uploads.developerhub.io/prod/97qW/14nygb6pevwj3w5j7p99tn5fg9kac1pamsjy8ee5fwaftnau9zcv5a9nfsreoxgs.png)

Bug fixes **Resolved 500 Error for Kiosk Policy Retrieval**

Fixed an issue where Kiosks received a 500 Internal Server Error and failed to obtain customized policy configurations.

---

### **File Security Solution**

Enhancements **Prioritized Display of Blocked Leaf Files**

Processing History now surfaces blocked leaf files at the top of the results for quicker identification.

![](https://uploads.developerhub.io/prod/97qW/qcuy4nku31wbmfh35mfbx97n1x2nt5darx9g3gd27tbaw1fr0uyi8o47fiwkxim7.png)

Enhancements **Batch, File, and Object Filtering Support**

Added new filter types and improved grouping of file and object results to streamline analysis in Processing History.

![](https://uploads.developerhub.io/prod/97qW/f0fdwlbqkta6vclc2n05t6m37mm9wwe1rhmmjw4yzb8acjuyr77uboares7zj87d.png)

Enhancements **Tag Linking and Inheritance from Kiosk to Core**

Tags assigned at Kiosk level now automatically propagate and synchronize with Core for consistent metadata handling.

![](https://uploads.developerhub.io/prod/97qW/dwdaeywfnef8wia5rp8q9kvgpciczdsz1qhdzgjlje6kdpz1ejcc81yoxywv4prd.png)

Bug fixes **Health Status Reset on Core Disconnection**

Corrected a condition where system **Health Status** did not revert to **Unknown** when the Core instance disconnected.

![](https://uploads.developerhub.io/prod/97qW/anih70w9596w8z5vqv8xejctl0js55njkx1n5bzw1vvzc7kz75bdfzl3vwe39hk8.png)

Bug fixes **Removed Core Instances Displayed in “All Services” after deleted**

Fixed an issue where deleted Core instances continued appearing in the All Services view.

---

### **Endpoint Security Solution**

New Features **Disconnected Endpoint Notification**

Introduced notifications when MetaDefender Endpoint becomes disconnected for a defined period, supporting timely incident response.

![](https://uploads.developerhub.io/prod/97qW/ih5deaa5jmvf3fjsxucpp0w667hmlmz2rlsujvn3qlmpkp2axqc5gx37eriksfus.png)

Enhancements **Extended Export Attributes for Device Inventory**

Exported device inventories now include serial number, device model, and manufacturer for improved asset tracking.

---

### **Hardware Supply Chain Solution**

New Features **Report Details in Scanned Host Page**

Added visibility of detailed scan reports directly within the Scanned Host view.

![](https://uploads.developerhub.io/prod/97qW/myk6uqqk7cp1t0zr30lryxlgufa5abkrersx513b8im2wa7k9j0438qt20lcyla8.png)

Enhancements **Expanded Verdict Display on MetaDefender Drive Dashboard**

Improved the MetaDefender Drive Dashboard with additional scan result verdicts for clearer threat assessment.

---

### **Network Access Control Solution**

Enhancements **Add a troubleshooting command line to check for network connectivity**

Added support to retrieve the connection status, including connection latency and current connection state.

![](https://uploads.developerhub.io/prod/97qW/e8zv8pderuuape717accjphr607hahrwmxcwj74u9rj9p4adyiesd8o4m9ejfafn.png)

---

### **Additional Features**

New Features **MetaDefender Cloud API Key Usage Monitoring**

Added support for displaying API key usage metrics and limits to improve visibility into cloud resource consumption.

![](https://uploads.developerhub.io/prod/97qW/ez29xwz6gw4d4z1i8pa33mesgowqyj5h6igwkyuaohctnmsx4jckobh5vovke8jp.png)

Enhancements **CEF Format Support for Syslog**

Added support for Common Event Format (CEF) to enhance compatibility with SIEM and log management platforms.

![](https://uploads.developerhub.io/prod/97qW/hktex30wi3tclhhbjpwbbkciby5807i9l648cmk6utbmfanv0be4bl4loanmyq8y.png)
