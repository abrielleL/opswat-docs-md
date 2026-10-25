<!-- source: https://www.opswat.com/docs/cm/release-notes/latest-release-notes -->

# SaaS Release Notes

| **Version** | **v10.7.26100** |
| ---- | ---- |
| **Release date** | October 20, 2026 |
| **Release Summary** | This release strengthens **file security** with role-based access controls for **Quarantined Files**, **expiration dates for Skip by Hash entries**, and **Data ID search in File Processing History**. **Endpoint & Patch Management** tightens patch control by **hiding and blocking rejected updates on MetaDefender Endpoint**. Administrators investigating removable-media scans also gain a fuller picture of each host, with expanded system information for MetaDefender Drive scanned hosts. |

### Endpoint Security Solution

Enhancements** Hide Unapproved Patches and Block Automatic Updates on MetaDefender Endpoint**

A new setting allows admins to hide unapproved patches and prevent them from being updated automatically on MetaDefender Endpoint.

To enable this feature, go to: Settings > Global > Endpoint Clients > Select **Only display allowed updates on MetaDefender Endpoint user interface.**

![](https://uploads.developerhub.io/prod/97qW/csdyfi7p87walxf79s5iff217hujss7ffeq2i0vd9hlos92zl9kupwguu4bq7mav.png)

### Portal Malware Scanning

Enhancements** Display System Information for MetaDefender Drive Scanned Hosts**

Administrators can now view detailed system information for scanned hosts, including BIOS details, CPU architecture, storage capacity, operating system specifications, and more.

![](https://uploads.developerhub.io/prod/97qW/iu424cqii2z2kroh1x4hmr5g90nnrusdorvtoir7e0lpojuzsdtpokfhihjcti0n.png)

### File Security Solution

Enhancements** Set Expiration Dates on Skip by Hash Entries**

Administrators can set optional expiration dates on Skip by Hash entry. Expired entries are automatically removed and the removal syncs to your enrolled MetaDefender Core instance, while entries without an expiration stay in place as before.

Refer to [Skip by Hash](https://www.opswat.com/docs/cm/product-management/skip-by-hash) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/7hcik4foe872gfmlpvaziksguqxobwev3gtjx5gsm79b0ypvr7rnamd6d33toet3.png)

Enhancements **Dedicated Role-Based Access Controls for MetaDefender Core Quarantined Files**

Administrators can now control access to MetaDefender Core quarantined files with a dedicated role-based permission to Hide, Read and Write, securing sensitive malware samples from unauthorized actions.

See [Quarantined Files Permissions](https://www.opswat.com/docs/cm/product-management/quarantined-files#quarantined-files-permissions) for more detailed instructions.

![](https://uploads.developerhub.io/prod/97qW/24q1jbo5xnoyjmmqb0rhtsnz8qyyi9k317yfi2mhoaehhi8m4awhjj9je3lbldgl.png)

Enhancements**Search MetaDefender Core File Processing History by Data ID**

Administrators can now search the File Processing History directly by Data ID. Select **Data ID** in the **Search by** menu on File Processing History page or on a Core instance's Processing History tab.

![](https://uploads.developerhub.io/prod/97qW/jqeb128k56rervkd4780y0hsjs0t27ego8vouq6whngpq0qfk27cy4urtz5kyw3e.png)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
