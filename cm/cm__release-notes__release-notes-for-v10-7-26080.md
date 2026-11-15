<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-7-26080 -->

# Release Notes for v10.7.26080

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | v10.7.26080 |
| --- | --- |
| **Release date** | August 11, 2026 |
| **Release Summary** | This release introduces new Peripheral Media Protection dashboard that **centralizes USB device threat visibility**, expands patch management with **patch notifications and SLA compliance**, and adds new **Skip by Hash** **management**, alongside enhanced notifications and alerts across the console, giving administrators earlier warning of issues and tighter central control over distributed deployments. |

## [Peripheral Media Protection Solution](/docs/cm/release-notes/release-notes-for-v10-7-26080#peripheral-media-protection-solution)

**New Features New Centralized Dashboards and Reports for USB-Threat Detection Events**

New Peripheral Media Protection dashboards and reports provide centralized visibility for USB-threat detection events from MetaDefender™ Kiosk and MetaDefender Endpoint.

Refer to [Peripheral Media Protection](/docs/cm/product-management/peripheral-media-protection) and [BadUSB Protection](/docs/cm/product-management/badusb-protection) guideline for more details.

## [Endpoint Security Solution](/docs/cm/release-notes/release-notes-for-v10-7-26080#endpoint-security-solution)

New Features **New Patch Notifications for Key Patching Events**

New Patch notifications alert administrators in real time to key events, including newly detected missing patches, completed deployments, per-device failures, SLA compliance, and more.

Refer to [Patch Notification](/docs/cm/patch-management/patch-notification) guidelines for more detailed instruction.

New Features **New** **Patch SLA Compliance Tracking**

New Patch SLA lets you set timeframe for how quickly patches must be applied by severity level. Track compliance in real time, see which updates are overdue, and get notified automatically when a patch misses its due date.

Refer to [Patch SLA](/docs/cm/patch-management/patch-sla) guidelines for more detailed instruction.

New Features **Enhanced Patches Display with Bulletin ID and Data Source Metadata**

Patches display now show Bulletin ID for associated security bulletin and Data Source field indicating the origin of the patch record.

Learn more in the [Bulletin and Data Source](/docs/cm/patch-management/bulletin-and-data-source) document.

## [File Security Solution](/docs/cm/release-notes/release-notes-for-v10-7-26080#file-security-solution)

New Features **Centralized Skip by Hash Management for MetaDefender Core**

Define and manage hash-based scan-skip rules across all your managed MetaDefender Core instances from one console.

Refer to [Skip by Hash](/docs/cm/file-security-solution/skip-by-hash) guide for more detailed instruction.

Enhancement **Automated Email Notifications for Configuration Changes in Product Groups**

Administrators can trigger email notifications when product groups are created, updated, or deleted. Email notifications include the action type, group name, product name, actor, and timestamp.

Enhancements **Supports Workflow Selection for Managed MetaDefender ICAP**

Administrators can now assign a specific workflow to managed ICAP instance via Server Profiles configuration, directly from My OPSWAT Central Management.

Bug Fixes **Fixed Excessive MetaDefender Managed File Transfer Error Logs**

Fixed an issue where MetaDefender Managed File Transfer generated continuous error-level log entries.

## [**Additional Features**](/docs/cm/release-notes/release-notes-for-v10-7-26080#additional-features)

Enhancements **Show Assigned Groups on the Users and Groups Page**

The Users and Groups page now displays the assigned groups for every account, providing a clear audit trail of permissions.

Enhancements **Supports Role-Based Session Duration Configuration**

Admins can now configure session time out per user role, allowing designated roles to remain signed in without automatic logout.

Refer to [Configure Role-Based Session Timeout](/docs/cm/user-management/configure-role-based-session-timeout) for configuration guidelines.

Enhancements **Added Real-Time Alerts and Recovery Actions for Update Jobs**

New real-time alerts trigger when a software upgrade job fails, stalls, or run past its maintenance window, with a failure reason and recommended next steps.

Enhancements **Automatic Recovery of Stalled Upgrade Jobs**

Upgrade jobs stuck in a perpetual "Updating" state are now automatically resolved every four hours, or on demand with a manual cleanup trigger.
