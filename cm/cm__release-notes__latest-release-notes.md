<!-- source: https://www.opswat.com/docs/cm/release-notes/latest-release-notes -->

# SaaS Release Notes

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | **v10.7.26100** |
| --- | --- |
| **Release date** | October 20, 2026 |
| **Release Summary** | This release strengthens **file security** with role-based access controls for **Quarantined Files**, **expiration dates for Skip by Hash entries**, and **Data ID search in File Processing History**. **Endpoint & Patch Management** tightens patch control by **hiding and blocking rejected updates on MetaDefender Endpoint**. Administrators investigating removable-media scans also gain a fuller picture of each host, with expanded system information for MetaDefender Drive scanned hosts. |

### [Endpoint Security Solution](/docs/cm/release-notes/latest-release-notes#endpoint-security-solution)

**Enhancements Hide Unapproved Patches and Block Automatic Updates on MetaDefender Endpoint**

A new setting allows admins to hide unapproved patches and prevent them from being updated automatically on MetaDefender Endpoint.

To enable this feature, go to: Settings > Global > Endpoint Clients > Select **Only display allowed updates on MetaDefender Endpoint user interface.**

### [Portable Malware Scanning](/docs/cm/release-notes/latest-release-notes#portable-malware-scanning)

Enhancements **Display System Information for MetaDefender Drive Scanned Hosts**

Administrators can now view detailed system information for scanned hosts, including BIOS details, CPU architecture, storage capacity, operating system specifications, and more.

### [File Security Solution](/docs/cm/release-notes/latest-release-notes#file-security-solution)

Enhancements **Set Expiration Dates on Skip by Hash Entries**

Administrators can set optional expiration dates on Skip by Hash entry. Expired entries are automatically removed and the removal syncs to your enrolled MetaDefender Core instance, while entries without an expiration stay in place as before.

Refer to [Skip by Hash](/docs/cm/product-management/skip-by-hash) guidelines for more details.

Enhancements **Dedicated Role-Based Access Controls for MetaDefender Core Quarantined Files**

Administrators can now control access to MetaDefender Core quarantined files with a dedicated role-based permission to Hide, Read and Write, securing sensitive malware samples from unauthorized actions.

See [Quarantined Files Permissions](/docs/cm/product-management/quarantined-files#quarantined-files-permissions) for more detailed instructions.

Enhancements**Search MetaDefender Core File Processing History by Data ID**

Administrators can now search the File Processing History directly by Data ID. Select **Data ID** in the **Search by** menu on File Processing History page or on a Core instance's Processing History tab.
