<!-- source: https://www.opswat.com/docs/cm/release-notes/latest-release-notes -->

# SaaS Release Notes

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | **v10.8.26110** |
| --- | --- |
| **Release date** | Nov 10, 2026 |
| **Release Summary** | This release expands centralized management capabilities across supported products. **Endpoint Security** adds application allowlisting and performance monitoring for macOS and Linux. **Peripheral Media Protection** gains backup & restore for MetaDefender Kiosk, alongside remote reboot & shutdown. **Additional improvements** include centralized upgrade and rollback controls, encrypted backups, and automated file transfer job management. |

### [**Peripheral Media Protection Solution**](/docs/cm/release-notes/latest-release-notes#peripheral-media-protection-solution)

New Features **Back Up and Restore for MetaDefender Kiosk Configuration**

Administrators can now back up and restore MetaDefender Kiosk configurations, with password-protected backups, manual or scheduled jobs, and centralized view into job records.

Refer to [Backup & Restore for MetaDefender Kiosk](/docs/cm/product-management/backup---restore-for-metadefender-kiosk) guideline for details.

New Features **Remote Reboot and Shut Down for MetaDefender Kiosk**

Remote reboot and shutdown are now supported for enrolled MetaDefender Kiosk devices **version 4.8.7 or later**.

Refer to [Remote Reboot and Shutdown](/docs/cm/product-management/remote-reboot-and-shutdown) guidelines for more details.

Enhancements **Support Additional Filters for Peripheral Media Protection Dashboard**

The Peripheral Media Protection dashboard now supports filtering by device type, location, device, and user, with additional option to exclude specific groups from the results.

Refer to [Peripheral Media Protection](/docs/cm/product-management/peripheral-media-protection) guidelines for detailed instruction.

### [**Endpoint Security Solution**](/docs/cm/release-notes/latest-release-notes#endpoint-security-solution)

New Features **Approve Temporary End-User Access with Challenge-Response Codes**

Administrators can now generate challenge-response codes for MetaDefender Endpoint and MetaDefender Endpoint Validation to approve temporary access requests from end users.

New Features **Control Application Allowlisting and Blocklisting for Managed MetaDefender Endpoint**

Administrators can now configure application allowlists and blocklists for managed MetaDefender Endpoint devices, defining which applications are permitted or blocked from running.

New Features **View Security Score for MetaDefender Endpoint**

A new Security Score data table helps administrators review score information for enrolled MetaDefender Endpoint.

Enhancements **View Third-Party Applications by Installed or Not Installed Status**

Administrators can now view and filter third-party applications by installed or not installed status. Available on MetaDefender Endpoint Windows persistent agent version 7.6.2612 or later.

View [Third Party Applications](/docs/cm/patch-management/patch-centric-third-party-applications) for more details.

Enhancements **Manage Patch Settings and Events in One Place**

Administrators can now access patch settings and related events directly within the Patch Management solution, bringing patch configuration and event monitoring together in one place.

Enhancements **Temporarily Exempt Devices from Compliance Checks**

Administrators can now exempt individual devices or device groups from compliance checks for a timed period.

Enhancements **Support** **Encrypt MetaDefender Endpoint Backups with a Passphrase**

Admins can turn on passphrase encryption when creating a backup job, adding a protection requirement when restoring backup data. Requires MetaDefender Endpoint **version 7.6.2611 or later**.

Refer to [Backup & Restore for MetaDefender Endpoint](/docs/cm/endpoint-security-solution/backup---restore) guidelines for more details.

Enhancements **Recognize Windows 10 with Extended Security Updates as a Supported OS**

Windows 10 22H2 devices covered by Extended Security Updates are now correctly recognized as running a supported operating system.

Enhancements **Display Detected Applications in MetaDefender Endpoint Device Details**

Device Details page now displays both managed and unmanaged third-party applications detected on Windows endpoints.

Enhancements **Endpoint Performance Monitoring Now Supports macOS and Linux**

Endpoint performance monitoring now extends to devices running the MetaDefender Endpoint agent on macOS and Linux.

See [Endpoint Performance Monitoring](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring) for more details.

### [**Portable Malware Scanning**](/docs/cm/release-notes/latest-release-notes#portable-malware-scanning)

New Features **Track** **Quarantine Files in MetaDefender Drive In-Session Scan Reports**

Track and export quarantined file details directly from MetaDefender Drive in-session scan reports.

### [**File Security Solution**](/docs/cm/release-notes/latest-release-notes#file-security-solution)

**New Features  Centrally Manage MetaDefender Managed File Transfer Automated Jobs**

Administrators can now configure, trigger, and review MetaDefender Managed File Transfer automated jobs from one console.

Refer to [MetaDefender Managed File Transfer Automation Jobs](/docs/cm/product-management/metadefender-managed-file-transfer-automation-jobs) guidelines for more details.

New Features **Remote Application Upgrade for MetaDefender ICAP Server**

Remotely roll out software upgrades for MetaDefender ICAP Server across individual device and group, reducing manual maintenance effort.

Refer to [Remote Application Update](/docs/cm/product-management/application-update-overview) guidelines for more details.

**Enhancements Support Additional Filters for File Security Dashboard**

**Admins can view** scanned file counts alongside object counts on the MetaDefender Core dashboard, and filter processing metrics by individual instance on both MetaDefender Core and MetaDefender ICAP Server dashboards.

**Enhancements Display New Engine Results in File Processing History**

File processing history details now display two new engine results:

1. **OPSWAT Alin AI Deflection**: show verdict banner and scan details in a dedicated tab.

2. **OPSWAT Predictive Alin AI**: show verdict banner with scan results available under the Metascan™ tab.

Bug Fixes **Correct “Last Updated” Sorting on MetaDefender Core Policy List**

Fixed an issue where sorting the “Last Updated” column on the MetaDefender Core policy list ordered policies by creation date instead of last updated date.

### [SDP Solution](/docs/cm/release-notes/latest-release-notes#sdp-solution)

New Features **IPv6 Support for Protected Applications**

SDP now supports secure access to IPv6-only protected applications. Administrators can define protected applications by IPv6 address or prefix, and configure IPv6 on the gateway to reach them.

### [**Additional Features**](/docs/cm/release-notes/latest-release-notes#additional-features)

Enhancements **Redesigned Platform Interface**

The platform interface has been revamped to provide administrators with streamlined navigation and a consistent visual experience across product consoles.

Enhancements **Improve Security User Management Module**

The Security User Management module now includes improvements to account handling, permission management, and system stability for more secure and reliable user administration.
