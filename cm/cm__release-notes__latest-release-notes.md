<!-- source: https://www.opswat.com/docs/cm/release-notes/latest-release-notes -->

# SaaS Release Notes

| **Version** | v10.7.26091 |
| ---- | ---- |
| **Release date** | August 25, 2026 |
| **Release Summary** | This release brings centralized synchronization of Password Storage for MetaDefender Core. It also extends patch management with a new Driver/Firmware Updates visibility control, giving greater control over what end users see and can act on. |

## Peripheral Media Protection Solution

Bug Fixes** Display Correct File Threat Reason and File Type**

The Peripheral Media Protection scan reports now display correct file threat reason and the associated file type.

![](https://uploads.developerhub.io/prod/97qW/u78mhokzueh05hwv628lduijkwrnsj3198tt2yrdayx8l40owd2931gpeuhsftfu.png)

Bug Fixes** Apply Configured Data Retention For Custom Timeframe Filtering**

The custom timeframe filtering on the Peripheral Media Protection Reports page now applies the configured data retention period.

![](https://uploads.developerhub.io/prod/97qW/773fqved1b65iza67z1do7wicd55xcis2b3lb2wlhil3kqancyk5mlnvmwelthcz.png)

## Endpoint Security Solution

Enhancements **Added Support to Show or Hide "Driver/Firmware Updates" Page for End Users**
Administrators can now control whether the "Driver/Firmware Updates" page is shown or hidden on the MetaDefender Endpoint interface for end-users.

![](https://uploads.developerhub.io/prod/97qW/12vxz8j1fbm64xkj6t6oqdrnvvq9js5y918vzocn56vf7ubyq0wk4k73i0q6n3j2.png)

## File Security Solution

New Features** Centralized Synchronization of Password Storage for MetaDefender Core**

My OPSWAT Central Management now synchronizes Password Storage entries to all managed MetaDefender Core, ensuring password-based workflow rules apply consistently across every Core instance. See [Password Storage](https://www.opswat.com/docs/cm/product-management/password-storage) for detailed guidelines.

![](https://uploads.developerhub.io/prod/97qW/jmnovjeco0j85admrnuv9ue8e87mjop9abv4hv354yg2h53d6tbvwt0h821hlayi.png)

## **Network Access Control Solution**

New Features** Backup and Restore for On-Premises Appliance**

** **MetaDefender NAC on-premises appliances can now take an encrypted snapshot of the appliance and roll back to a previous snapshot. This supports disaster recovery and rollback of a failed change or upgrade. Backup and restore are available from the appliance console, under **Basic System Configuration → Backup & Restore**.

![](https://uploads.developerhub.io/prod/97qW/sq3gl3i7xv5mjcm6l610l7qnr3y6lw54jwoiu7qcikmcgadq9bg3a9gysl49dpsb.png)

New Features** Export logs from the CNC console**

With this release, an export action is available in the console UI. Logs are packaged and transferred to a destination you configure (via ftp), so you can gather diagnostics yourself and attach them to a support ticket without sharing privileged system credentials.

![](https://uploads.developerhub.io/prod/97qW/lwo6ngv6ealm8dyilsk6aton93tqz9ases35qoku28jp4sqgudtjw6o9vwhgaxkl.png)
