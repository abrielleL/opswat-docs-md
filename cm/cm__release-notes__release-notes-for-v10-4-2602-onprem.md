<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-4-2602-onprem -->

# Release Notes for v10.4.2602

| Version | v10.4.2602 |
| ---- | ---- |
| **Release Date** | February 6th, 2026 |
| **Release Summary** | This release brings **new integration with MetaDefender Industrial Firewall** and includes new features, improvements, and bug fixes across **Kiosk**, **Core**, **Endpoint**, and **Drive** solutions. It offers easy update rollouts, better scan insights, improved reporting, and higher system reliability. With expanded verdict displays, automated notifications, and better integration, this update helps you stay secure and in control with less effort. |

### **Peripheral Media Protection Solution**

New Features **Kiosk Update Rollout**

Introduced phased deployment of Kiosk updates to ensure smoother rollout and improved operational stability.

![](https://uploads.developerhub.io/prod/97qW/wtma1qzhnty1n6u05istoejq2sqj3i64yw96wq5555ixl2ja3608xqelt0iyfucr.png)

Enhancements **Expanded Scan Verdict Display on Kiosk Dashboard**

Enhanced the Dashboard to show additional scan result verdicts for improved visibility and analysis.

![](https://uploads.developerhub.io/prod/97qW/oq95b3drexf6ax8supsupo9r8n41knvhid7056dfa4xvwtj87eysnqdjscaii2mp.png)

Bug fixes **Health Status Reset on Kiosk Disconnection**

Corrected a condition where system **Health Status** did not revert to **Unknown** when the Kiosk instance disconnected.

![](https://uploads.developerhub.io/prod/97qW/14nygb6pevwj3w5j7p99tn5fg9kac1pamsjy8ee5fwaftnau9zcv5a9nfsreoxgs.png)

Bug fixes **Resolved 500 Error for Kiosk Policy Retrieval**

Fixed an issue where Kiosks received a 500 Internal Server Error and failed to obtain customized policy configurations.

---

### **File Security Solution**

Enhancements **Prioritized Display of Blocked Leaf Files**

Processing History now surfaces blocked leaf files at the top of the results for quicker identification.

![](https://uploads.developerhub.io/prod/97qW/x6mv02mrj5un1g5lim8eqjc4f3ug377akdus7uw5ov1vbo86puqazicmg1r5derd.png)

Enhancements **Batch, File, and Object Filtering Support**

Added new filter types and improved grouping of file and object results to streamline analysis in Processing History.

![](https://uploads.developerhub.io/prod/97qW/fk1r9asp3ham57ss90ezywgxspuwypszztz58x5czuzo3rr1s6lykuil9t671i68.png)

Enhancements **Tag Linking and Inheritance from Kiosk to Core**

Tags assigned at Kiosk level now automatically propagate and synchronize with Core for consistent metadata handling.

![](https://uploads.developerhub.io/prod/97qW/dwdaeywfnef8wia5rp8q9kvgpciczdsz1qhdzgjlje6kdpz1ejcc81yoxywv4prd.png)

Enhancements** Remove Unlicensed or Unwanted Engine**

Enabled administrators to remove unlicensed or unwanted engines from the Modules tab, giving you greater control over your deployed modules.

![](https://uploads.developerhub.io/prod/97qW/yogi35ea8jhvj0uldmp2hxp2bybcvh5am5o6sbl0yfcv1j854iu6gmfr3ww1be2w.png)

Bug fixes **Health Status Reset on Core Disconnection**

Corrected a condition where system **Health Status** did not revert to **Unknown** when the Core instance disconnected.

![](https://uploads.developerhub.io/prod/97qW/anih70w9596w8z5vqv8xejctl0js55njkx1n5bzw1vvzc7kz75bdfzl3vwe39hk8.png)

Bug fixes **Removed Core Instances Displayed in “All Services” after deleted**

Fixed an issue where deleted Core instances continued appearing in the All Services view.

---

### **Endpoint Security Solution**

New Features **Disconnected Endpoint Notification**

Introduced notifications when MetaDefender Endpoint becomes disconnected for a defined period, supporting timely incident response.

![](https://uploads.developerhub.io/prod/97qW/iz73vsipti8c5ajjwvwcvx3i9ug1zicqn02fe0c0m06v6thar9hx9k7d93qtpas1.png)

Enhancements **Extended Export Attributes for Device Inventory**

Exported device inventories now include serial number, device model, and manufacturer for improved asset tracking.

---

### **Hardware Supply Chain Solution**

New Features **MetaDefender Industrial Firewall Integration**

Introduced the ability to enroll and monitor all your Industrial Firewall devices with real-time health and alert visibility directly from My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/fnfz6nlay6l01bxkeo5ejcrrkprrhfutyp6feh4o05q41k0ea1de58q71au08x45.png)

New Features **Report Details in Scanned Host Page**

Added visibility of detailed scan reports directly within the Scanned Host view.

![](https://uploads.developerhub.io/prod/97qW/wyk4fsw70pqbe7bhvf18br7e0q47390op8ys0eb7gfjk3e9r3dgyr2l4svzab454.png)

Enhancements **Expanded Verdict Display on MetaDefender Drive Dashboard**

Improved the MetaDefender Drive Dashboard with additional scan result verdicts for clearer threat assessment.

---

### **Additional Features**

New Features **MetaDefender Cloud API Key Usage Monitoring**

Added support for displaying API key usage metrics and limits to improve visibility into cloud resource consumption.

![](https://uploads.developerhub.io/prod/97qW/gf73f6gxn3r9j6mr6jylohk4kfhh215zpmehmcpelb5mm74gc85y938684ayrraf.png)

Enhancements **CEF Format Support for Syslog**

Added support for Common Event Format (CEF) to enhance compatibility with SIEM and log management platforms.

![](https://uploads.developerhub.io/prod/97qW/bhx3hbhu6fsrdh8qbr3brrlgux8enq9c35rezuwlxbw2k4ypirvdohp0v7c5svsj.png)

Enhancements** "Update Package" Menu Relocation**

Introduced a new “Updates” tab in the left navigation, replacing the previous **Settings > Update Package** sub-tab. This change brings a clearer structure for managing endpoints, modules, firmware, applications, and patches, making update management more intuitive and accessible.

![](https://uploads.developerhub.io/prod/97qW/6qxgpbqx94w4ibt2gllc7tt6iy1qt9es1bbwry53896vdpmt918g74mqa60e6c9y.png)
