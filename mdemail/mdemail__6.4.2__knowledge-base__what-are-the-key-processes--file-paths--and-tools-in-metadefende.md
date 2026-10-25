<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende -->

# What Are the Key Processes, File Paths, and Tools in MetaDefender Email Security Gateway?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all OPSWAT Email Security Gateway product releases deployed on Windows systems.

## [**Overview**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#overview)

This document provides a comprehensive reference for the key processes, file locations, and utilities used by OPSWAT MetaDefender Email Security Gateway (ESG). This information is essential for monitoring, security auditing, and operational maintenance of the product.

---

## [**1. Services Registered by the Product**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#1-services-registered-by-the-product)

The product installs and registers the following Windows services:

- `mdemailsecurity` - Main service process
- `mdemailsecurity-database` - Database service (when using embedded database)

---

## [**2. Operational Processes and Their Functions**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#2-operational-processes-and-their-functions)

### [**Core Service Processes**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#core-service-processes)

### [**Database Processes (Embedded Database)**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#database-processes-embedded-database)

---

## [**3. Critical File and Directory Locations**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#3-critical-file-and-directory-locations)

### [**Installation Directory**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#installation-directory)

HtmlCopyC:\Program Files\OPSWAT\MetaDefender Email Security\
### [**Log Files Directory**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#log-files-directory)

HtmlCopyC:\Program Files\OPSWAT\MetaDefender Email Security\Logs\

*Processes that write to logs: All operational processes listed above*

### [**Database Storage**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#database-storage)

HtmlCopyC:\Program Files\OPSWAT\MetaDefender Email Security\data\
### [**Email spool directories**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#email-spool-directories)

#### [**Inbound**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#inbound)

HtmlCopyC:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\in
#### [**Outbound**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#outbound)

HtmlCopyC:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\out
### [**Configuration Files**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#configuration-files)

Located throughout the installation directory. Primary configuration is managed through:

- Web interface configurations
- Database-stored settings
- Registry configurations

---

## [**4. Database Migration and Initiation Tools for Product Upgrades**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#4-database-migration-and-initiation-tools-for-product-upgrades)

---

## [**5. Support Package Generation Tools**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#5-support-package-generation-tools)

---

## [**Conclusion**](/docs/mdemail/6.4.2/knowledge-base/what-are-the-key-processes--file-paths--and-tools-in-metadefende#conclusion)

This reference provides the essential information needed to effectively monitor and maintain OPSWAT MetaDefender Email Security Gateway. Proper monitoring of these processes and file locations ensures optimal performance and security of the email protection system.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
