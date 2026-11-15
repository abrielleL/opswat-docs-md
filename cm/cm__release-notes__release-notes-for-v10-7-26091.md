<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-7-26091 -->

# Release Notes for v10.7.26091

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | v10.7.26091 |
| --- | --- |
| **Release date** | August 25, 2026 |
| **Release Summary** | This release brings centralized synchronization of Password Storage for MetaDefender Core. It also extends patch management with a new Driver/Firmware Updates visibility control, giving greater control over what end users see and can act on. |

## [Peripheral Media Protection Solution](/docs/cm/release-notes/release-notes-for-v10-7-26091#peripheral-media-protection-solution)

Bug Fixes **Display Correct File Threat Reason and File Type**

The Peripheral Media Protection scan reports now display correct file threat reason and the associated file type.

Bug Fixes **Apply Configured Data Retention For Custom Timeframe Filtering**

The custom timeframe filtering on the Peripheral Media Protection Reports page now applies the configured data retention period.

## [Endpoint Security Solution](/docs/cm/release-notes/release-notes-for-v10-7-26091#endpoint-security-solution)

Enhancements **Added Support to Show or Hide "Driver/Firmware Updates" Page for End Users**
Administrators can now control whether the "Driver/Firmware Updates" page is shown or hidden on the MetaDefender Endpoint interface for end-users.

## [File Security Solution](/docs/cm/release-notes/release-notes-for-v10-7-26091#file-security-solution)

New Features **Centralized Synchronization of Password Storage for MetaDefender Core**

My OPSWAT Central Management now synchronizes Password Storage entries to all managed MetaDefender Core, ensuring password-based workflow rules apply consistently across every Core instance. See [Password Storage](/docs/cm/file-security-solution/password-storage) for detailed guidelines.

## [**Network Access Control Solution**](/docs/cm/release-notes/release-notes-for-v10-7-26091#network-access-control-solution)

New Features **Backup and Restore for On-Premises Appliance**

MetaDefender NAC on-premises appliances can now take an encrypted snapshot of the appliance and roll back to a previous snapshot. This supports disaster recovery and rollback of a failed change or upgrade. Backup and restore are available from the appliance console, under **Basic System Configuration → Backup & Restore**.

New Features **Export logs from the CNC console**

With this release, an export action is available in the console UI. Logs are packaged and transferred to a destination you configure (via ftp), so you can gather diagnostics yourself and attach them to a support ticket without sharing privileged system credentials.
