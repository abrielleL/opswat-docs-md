<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves -->

# Is the OESIS Framework Affected by PHP2Shell (CVE-2026-109618 and CVE-2026-109619)?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [**Check Your Version**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#check-your-version)

Based on the product-level security assessment, the OESIS Framework SDK and its content delivery services do not use PHP. No version check is required.

## [**Security Assessment: Not Affected**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#security-assessment-not-affected)

The OESIS Framework is not affected by CVE-2026-109618 or CVE-2026-109619 within the assessed product scope.

## [**Overview**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#overview)

PHP2Shell refers to two security vulnerabilities in the PHP interpreter: **CVE-2026-109618** and **CVE-2026-109619**. Both were disclosed by the PHP project on October 21, 2026 and are rated Critical (CVSS v4.0 9.2). Under certain conditions, an affected PHP runtime that serves web requests may allow unauthenticated remote code execution before application code runs. Fixed releases are PHP 8.5.12, 8.4.27, 8.3.36 and 8.2.35.

## [**Product Assessment**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#product-assessment)

The following components were assessed:

| Component | Description | PHP present | Status |
| --- | --- | --- | --- |
| OESIS Framework SDK (Windows, macOS, Linux) | Native libraries (`libwaapi`, `libwalocal`, `libwaresource` and related modules) linked into the customer's application | No | Not affected |
| OESIS data packages | `analog.zip`, `compliance.zip`, `vmod-om.dat`, `patch.dat` and related data files consumed by the SDK | No, data only | Not affected |
| VCR Gateway (`vcr.opswat.com`) | Server-side download service for SDK engine and data packages | No | Not affected |
| Legacy update gateway (`watch.opswat.com`) | Legacy server-side download service used by `DownloadDatabase` (method `50200`) | No | Not affected |

The OESIS Framework SDK is distributed as native compiled libraries and does not embed, bundle or depend on a PHP interpreter at build time or at runtime. The OESIS content delivery services do not run PHP. None of the assessed components are therefore susceptible to these PHP interpreter vulnerabilities.

## [**Is Any Action Required?**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#is-any-action-required)

No product-specific patch, hotfix, SDK update or configuration change is required for the OESIS Framework to address these two PHP vulnerabilities.

If PHP is installed on an endpoint as part of another application or service, it must be assessed and patched independently. Where PHP is a product supported by the OESIS Vulnerability module, the SDK reports CVE-2026-109618 and CVE-2026-109619 against detected installations once the corresponding vulnerability data is published, in line with the standard data update cadence.

**Note:** This article addresses only the two CVEs above. It does not assess other vulnerabilities, the customer's own application that integrates the SDK, or independently installed third-party software.

## [**Additional Resources**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#additional-resources)

- [PHP Security Release Information, October 21, 2026](https://www.php.net/archive/2026.php#2026-10-21-5)
- [GitHub Security Advisory GHSA-w8hw-w9fx-j79w (CVE-2026-109618)](https://github.com/php/php-src/security/advisories/GHSA-w8hw-w9fx-j79w)
- [GitHub Security Advisory GHSA-6wmf-4rv5-p3rp (CVE-2026-109619)](https://github.com/php/php-src/security/advisories/GHSA-6wmf-4rv5-p3rp)
- [Is MetaDefender Core Affected by PHP2Shell?](https://www.opswat.com/docs/mdcore/knowledge-base/is-metadefender-core-affected-by-php2shell--cve-2026-109618-and-)

## [**Support**](/docs/mdsdk/knowledge-base/is-oesis-framework-affected-by-php2shell-cves#support)

If you have questions about this security assessment or require a written vendor statement for your records, please [contact OPSWAT Support](https://my.opswat.com/support).

*This article was last updated on 2026-10-23.*
