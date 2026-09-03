<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-6-2605 -->

# Release Notes for v10.6.2605

| **Version** | v10.6.2605 |
| ---- | ---- |
| **Release date** | May 12th, 2026 |
| **Release Summary** | This release enhances security operation with **Third-Party Application Patch Management** and unified control across OPSWAT Ecosystem. Key updates include new **MetaDefender** **Media Firewall integration,** **remote application updates** for Core and Industrial Firewall, **Kiosk rollback support**, and **remote Core support package generation**. Complemented by automated Core instance naming and new "Last Seen" activity filters, these enhancements ensure maximum system reliability and a hardened security posture across all environments. |

### **Peripheral Media Protection Solution**

New Features** MetaDefender Media Firewall Integration**

You can now enroll Media Firewall devices and manage them centrally. Monitor device real-time health status, update device settings, and import/apply Media Firewall policies all from My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/mcygweymshixrsq1po7p8msm28m15zf3ce3tqanw4ezuauq4rdslkl1bj6xbxnyj.png)

New Features **Roll Back Kiosk Application Updates**

Kiosk remote application update now supports rollback to the previous stable version to keep operation running. This update removes the need for manual workarounds, ensuring high availability across large-scale Kiosk environments.

![](https://uploads.developerhub.io/prod/97qW/fjlme22dj3xxwdrdsdjov9uk00i1ypja99tf10u2val3ujtyi1qtzxphswqv38mk.png)

Enhancements **Enhanced Peripheral Media Visibility & Reporting Across Device Scans**

Introduced consolidated visibility into peripheral media usage. A new **By Peripheral Media** tab aggregates all Kiosk-scanned devices into one exportable view. Access detailed scanned host info, scan history, and copy destinations to ensure full audit compliance across your entire Kiosk deployment.

![](https://uploads.developerhub.io/prod/97qW/p9xmtc73wxhalj7k1gnwvs8ankmb2jpph3jpd98p2qngms097s63c6pfxkguy2yx.png)

### **Endpoint Security Solution**

New Features** Unified** **Third-Party Applications Patching**

End-to-end patching for third-party applications is now live, with proactive workflows to identify missing patches, automate deployments through one-time or recurring policies, and monitor progress through consolidated  deployment logs, ensuring a strong security posture and compliance.

Refer to [Patch Management Solution Overview](https://www.opswat.com/docs/cm/patch-management/overview-patch-management) guidelines for detailed instructions.

![](https://uploads.developerhub.io/prod/97qW/cphh67qdpyh2clxu2dmhb9oif7fzq6tzugd4iunnid5mh8o1gxcli4183yy9i7up.png)

New Features **OAuth APIs for Vulnerability Management**

Programmatically manage vulnerabilities at scale using new OAuth APIs, including [Update Vulnerabilities Allowlist](https://www.opswat.com/docs/cm/developer-guidelines/update-vulnerabilities-allowlist), [Get Vulnerabilities](https://www.opswat.com/docs/cm/developer-guidelines/get-vulnerabilities), and [Get Policy Blocklist CVE](https://www.opswat.com/docs/cm/developer-guidelines/get-policy-blocklist-cve) via CSV upload/download for faster, high-volume vulnerability control across  environment.

![](https://uploads.developerhub.io/prod/97qW/p7xyaypdtadrjpbc3o0amhal7jzpdza45y9sf9gxweyw93d32ct31z8sl7l8hzf1.png)

Enhancements**Auto-Assign Devices to Groups Across Multiple Domains**

Auto-assign devices across multiple domains into a single group using wildcard matching, eliminating the need to create separate groups per domain.

![](https://uploads.developerhub.io/prod/97qW/rctmi9z8w6vralkpjpmyfjpr590029cy3c89pz8nsxmdl5gq08rrx5hfx136whvg.png)

Enhancements**Configure Settings for Application Control Notification**

Admins can now enable or disable pop-up notifications for end-users when an application is disabled or uninstalled, as well as personalize the pop-up message text at both Global and Group policy settings.

![](https://uploads.developerhub.io/prod/97qW/0zn4cdasalql51kjvupgn6mplreg6ju6k3s2kjdjzn80djmvemextgfsjd72er0e.png)

Enhancements"**Get Devices API" Now Supports Group Filtering**

The OAuth [Get Devices](https://www.opswat.com/docs/cm/developer-guidelines/get-devices) API now supports filtering devices by group ID, retrieving only the devices belonging to specific groups in a single API call.

Enhancements **Fetch Log Action Extends to Mobile Endpoints**

Fetch Log is available for mobile devices through My OPSWAT Central Management. Logs are securely encrypted and uploaded with size and time limits. Supported on agent v3.0.2605+ (Android) and v3.2605+ (iOS).

![](https://uploads.developerhub.io/prod/97qW/3unekxzukk7e36oh0o2jprhe5s789vyxx4zm8jbjdguudqezdfl4lowes7v3vja8.png)

---

### **Hardware Supply Chain**

New Features **Auto-Sync Configuration and Version Compatibility for MetaDefender Drive**

Automate group policies configuration workflow  for MetaDefender Drive with **auto-sync toggle** and **group settings apply** across multiple instances at once. Eliminate "incompatible version" errors with improved version compatibility and gain total oversight with real-time status tracking and detailed timestamps.

![](https://uploads.developerhub.io/prod/97qW/90jri0xwlf4r1kzh5bb7s730pu8mm3408rgt03hcyebii554ny4efdw24mn3g8ec.png)

![](https://uploads.developerhub.io/prod/97qW/8fhp2qn2u397qziis4j16jlttqlccy8gkh0a0yxr8t4snl27eq5gl97xn46nlped.png)

Enhancements **Automated Email Alerts When MetaDefender Drive Detects An Unsafe Device**

Configure My OPSWAT Central Management to automatically send email alerts when MetaDefender Drive detects an unsafe device. These notifications include downloadable reports summarizing the scan results.

![](https://uploads.developerhub.io/prod/97qW/y9pj5hv5ndugyycjvzy04jys5op7rh7kyhes3vr6g8rmxb2e9gq7kkaugbqtwt8o.png)

![](https://uploads.developerhub.io/prod/97qW/kcudypbxky6rt2kul03a9k92xsksvh72koti2q1q0yk4zdhq4r7ijtxjmrol6esc.png)

Automate group policies configuration workflow  for MetaDefender Drive with **auto-sync toggle** and **group settings apply** across multiple instances at once. Eliminate "incompatible version" errors with improved version compatibility and gain total oversight with real-time status tracking and detailed timestamps.

---

### **OT and Cyber-Physical Systems Solution**

Enhancements **Streamlined MetaDefender Industrial Firewall Application Update Management**

Extending application update feature to support **MetaDefender Industrial Firewall**. Admins can now manage the entire update lifecycle, from importing update packages, scheduling update jobs, and monitoring progress, all from a single console.

![](https://uploads.developerhub.io/prod/97qW/u4r7y0qyqxdrqlo485406b327v1dnw2eos6q8zm5y2njurjf2ju6o7z3cotcpmjj.png)

### **File Security Solution**

New Features **Centralized Application Update Management for** **MetaDefender Core**

Admins can now roll out MetaDefender Core application update remotely from My OPSWAT Central Management. Target specific instances or groups, schedule rollouts, and monitor progress in real time with automated email notifications.

**Please note:** This feature is available for MetaDefender Core version 5.20.0.

![](https://uploads.developerhub.io/prod/97qW/2v6koztz28pqoepoofh9u7kpailpl97oungresut7lvhvcaxx2gpcckzfke1omrk.png)

New Features **Remote Support Package Fetching for MetaDefender Core**

Support packages can now be generated and retrieved remotely from managed Core instances for faster troubleshooting.

![](https://uploads.developerhub.io/prod/97qW/jthpp5ynecjok0dlajk0eod4iicx4gilp7h6xsvktxqq90g5l01h0gsv90wnax29.png)

New Features **New API to Change Module Update Settings for MetaDefender Core Instances**

Introduced new API to remotely configure module update settings for MetaDefender Core instances. Refer to our [Update Module Update Settings](https://www.opswat.com/docs/cm/10.7.26062/direct-instance-management/ref#updatemoduleupdatesettings) documents for details.

Enhancements **Automated Naming Using Hostname for Enrolled MetaDefender Core Instances**

MetaDefender Core instances automatically display their **Hostname** instead of a system-generated Deployment ID as the **Instance Name** upon enrollment, eliminating manual renaming and providing clear asset visibility from day one.

![MetaDefender Core instances display **Hostname** instead of a Deployment ID upon enrollment.](https://uploads.developerhub.io/prod/97qW/444d4muidqmyb1ljgt1cn222oy8r7rbye6lmyd1dggygbl3roe13hp0891paofzd.png)

### **Additional Features**

Enhancements **Improved Support Package Management**

Support Packages now feature better tracking with clearer status updates, automatic failure handling for unenrolled instances, and smarter storage limits (2 per instance) with auto-cleanup based on your data retention settings.

Enhancements**"Last Seen" Filter for Device & Service Search Across All Products**

A new "Last Seen" filter enables searching across all product services by activity timeframe, instantly surfacing inactive devices within the last hour or missing for over 30 days.

![](https://uploads.developerhub.io/prod/97qW/v3z9oebpyjbuqk55y3y4du4uskvhs1ktn8xfuvny37xzatc96xy7f3ppyeyr2t6m.png)
