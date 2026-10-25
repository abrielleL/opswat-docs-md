<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/is-metadefender-storage-security--mdss--affected-by-php2shell--c -->

# Is MetaDefender Storage Security (MDSS) Affected by PHP2Shell (CVE-2026-109618 and CVE-2026-109619)?

> ## **Check Your Version**
>
> Based on the product-level security assessment, no PHP component was identified in the reviewed MetaDefender Storage Security application or its bundled container dependencies.

> ## **Security Assessment: Not Affected**
>
> MetaDefender Storage Security (MDSS) is not affected by CVE-2026-109618 or CVE-2026-109619 within the assessed product scope.

## **Overview**

PHP2Shell refers to two security vulnerabilities in the PHP interpreter: **CVE-2026-109618** and **CVE-2026-109619**. Under certain conditions, an affected PHP runtime may allow remote code execution.

## **Product Assessment**

The assessment reviewed the application's container images and software dependencies and did not identify PHP.

## **Is Any Action Required?**

No product-specific patch, hotfix or configuration change is required for the assessed product to address these two PHP vulnerabilities. PHP installed separately as part of another application or service must be assessed independently.

**Note:** This article addresses only the two CVEs above. It does not assess other vulnerabilities or independently installed third-party software.

## **Additional Resources**

- [PHP Security Release Information — October 21, 2026](https://www.php.net/archive/2026.php#2026-10-21-5)

> ## **Support**
>
> If you have questions about this security assessment or a reported vulnerability finding, please [contact OPSWAT Support](https://my.opswat.com/support).

*This article was last updated on 2026-10-22.*

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
