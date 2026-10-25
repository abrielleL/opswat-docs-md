<!-- source: https://www.opswat.com/docs/mdendpoint/opswat-media-validation-agent--omva-/is-opswat-media-validation-agent--omva--affected-by-php2shell--c -->

# Is OPSWAT Media Validation Agent (OMVA) Affected by PHP2Shell (CVE-2026-109618 and CVE-2026-109619)?

> ## **Check Your Version**
>
> Based on the product-level security assessment, OPSWAT Media Validation Agent does not include or execute PHP.

> ## **Security Assessment: Not Affected**
>
> OPSWAT Media Validation Agent (OMVA) is not affected by CVE-2026-109618 or CVE-2026-109619 within the assessed product scope.

## **Overview**

PHP2Shell refers to two security vulnerabilities in the PHP interpreter: **CVE-2026-109618** and **CVE-2026-109619**. Under certain conditions, an affected PHP runtime may allow remote code execution.

## **Product Assessment**

The reviewed OMVA application is implemented in C++. Its source code, third-party libraries and packaged installer were checked for PHP.

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

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
