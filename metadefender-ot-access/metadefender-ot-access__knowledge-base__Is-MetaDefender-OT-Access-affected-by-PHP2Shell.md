<!-- source: https://www.opswat.com/docs/metadefender-ot-access/knowledge-base/Is-MetaDefender-OT-Access-affected-by-PHP2Shell -->

# Is MetaDefender OT Access affected by PHP2Shell (CVE-2026-109618 and CVE-2026-109619)?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## Answer

No. MetaDefender OT Access is not affected by CVE-2026-109618 or CVE-2026-109619. No patch, workaround, or configuration change is required.

## About the vulnerability

PHP2Shell refers to two critical vulnerabilities in the PHP interpreter, disclosed on 21 October 2026, which can allow unauthenticated remote code execution. The affected versions are PHP 8.2 before 8.2.35, 8.3 before 8.3.36, 8.4 before 8.4.27, and 8.5 before 8.5.12.

## Why MetaDefender OT Access is not affected

MetaDefender OT Access does not include, bundle, or execute PHP in any component. Because no PHP interpreter is present in the product, the vulnerable code path does not exist.

## Affected versions

None. All supported versions of MetaDefender OT Access are unaffected.

## Action required

None for MetaDefender OT Access.

Customers should continue to patch PHP in any other systems in their environment that run it, following the guidance in the PHP project's security advisories.

## References

- CVE-2026-109618
- CVE-2026-109619
- PHP project security advisories: https://www.php.net/ChangeLog-8.php

Last reviewed: October 2026
