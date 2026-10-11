<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-7-26080 -->

# Release Notes for v10.7.26080

| **Version** | v10.7.26080 |
| ---- | ---- |
| **Release date** | August 11, 2026 |
| **Release Summary** | This release introduces new Peripheral Media Protection dashboard that **centralizes USB device threat visibility**, expands patch management with **patch notifications and SLA compliance**, and adds new **Skip by Hash** **management**, alongside enhanced notifications and alerts across the console, giving administrators earlier warning of issues and tighter central control over distributed deployments. |

## Peripheral Media Protection Solution

New Features** New Centralized Dashboards and Reports for USB-Threat Detection Events**

New Peripheral Media Protection dashboards and reports provide centralized visibility for USB-threat detection events from MetaDefender™ Kiosk and MetaDefender Endpoint.

Refer to [Peripheral Media Protection](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection) and [BadUSB Protection ](https://www.opswat.com/docs/cm/product-management/badusb-protection)guideline for more details.

![](https://uploads.developerhub.io/prod/97qW/jhx0n7ss6w6di5wjlgfo07kee0k0xorcgmrocfvd9qzlstlhbogwzctm6v8mxl76.png)

## Endpoint Security Solution

New Features **New Patch Notifications for Key Patching Events**

New Patch notifications alert administrators in real time to key events, including newly detected missing patches, completed deployments, per-device failures, SLA compliance, and more.

Refer to [Patch Notification](https://www.opswat.com/docs/cm/patch-management/patch-notification) guidelines for more detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/t6vwj5t1gps2oylr4gucpsdxgxhgystvsjuhevw1nkpb9xcipv88otc1d91jbnbw.png)

New Features **New** **Patch SLA Compliance Tracking**

New Patch SLA lets you set timeframe for how quickly patches must be applied by severity level. Track compliance in real time, see which updates are overdue, and get notified automatically when a patch misses its due date.

Refer to [Patch SLA](https://www.opswat.com/docs/cm/patch-management/patch-sla) guidelines for more detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/5d5ucpbaqlx534xbrfqqfuynr98vqsag29bhejtziuty8wmu7lz3xebtfau1zdm5.png)

New Features** Enhanced Patches Display with Bulletin ID and Data Source Metadata**

Patches display now show Bulletin ID for associated security bulletin and Data Source field indicating the origin of the patch record.

Learn more in the [Bulletin and Data Source](https://www.opswat.com/docs/cm/patch-management/bulletin-and-data-source) document.

![](https://uploads.developerhub.io/prod/97qW/w4gbf1b0ngfnxjxbmre1q08qe15bkymd7458tykil3gnx1kcz2r7mivwveaa093w.png)

## File Security Solution

New Features** Centralized Skip by Hash Management for MetaDefender Core**

Define and manage hash-based scan-skip rules across all your managed MetaDefender Core instances from one console.

Refer to [Skip by Hash](https://www.opswat.com/docs/cm/product-management/skip-by-hash) guide for more detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/5t93l6mp33qeh4sbprbxv2ivpo5pec2e96ns48vtzxd3mux82du3kcn5d7fyzrc2.png)

Enhancement** Automated Email Notifications for Configuration Changes in Product Groups**

Administrators can trigger email notifications when product groups are created, updated, or deleted. Email notifications include the action type, group name, product name, actor, and timestamp.

![](https://uploads.developerhub.io/prod/97qW/qpn4o9ug9x9p9tmuidbtdektqgb2b2krrmy2wilsnhljbpaliz1o1324h4r2lu3s.png)

Enhancements **Supports Workflow Selection for Managed MetaDefender ICAP**

Administrators can now assign a specific workflow to managed ICAP instance via Server Profiles configuration, directly from My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/dbu7ptq0sp83yxqk141zvvzacl4ndga6tr6k1ci4623zojjosm3litgbd62ulz4p.png)

Bug Fixes** Fixed Excessive MetaDefender Managed File Transfer Error Logs**

Fixed an issue where MetaDefender Managed File Transfer generated continuous error-level log entries.

## **Additional Features**

Enhancements** Show Assigned Groups on the Users and Groups Page**

The Users and Groups page now displays the assigned groups for every account, providing a clear audit trail of permissions.

![](https://uploads.developerhub.io/prod/97qW/shfkzu2xdb522q9sgiuojj2o0x8fdbqlcl86fd7wt7wiie4iel3emuqblz71qjen.png)

Enhancements **Supports Role-Based Session Duration Configuration**

Admins can now configure session time out per user role, allowing designated roles to remain signed in without automatic logout.

Refer to [Configure Role-Based Session Timeout](https://www.opswat.com/docs/cm/user-management/configure-role-based-session-timeout) for configuration guidelines.

![](https://uploads.developerhub.io/prod/97qW/a3xfb4bjk2elsjc73wivr9xic8nngv64xnmgh12ik7eq81mc9zk4ef5vagxnq7aj.png)

Enhancements** Added Real-Time Alerts and Recovery Actions for Update Jobs**

New real-time alerts trigger when a software upgrade job fails, stalls, or run past its maintenance window, with a failure reason and recommended next steps.

![](https://uploads.developerhub.io/prod/97qW/3qi9rx8z4jek17st9bmamtfdl0swymcwrjgr8tmtevaobf4acdn2egqsrnkw7xz6.png)

Enhancements** Automatic Recovery of Stalled Upgrade Jobs**

Upgrade jobs stuck in a perpetual "Updating" state are now automatically resolved every four hours, or on demand with a manual cleanup trigger.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
