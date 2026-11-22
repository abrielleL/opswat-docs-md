<!-- source: https://www.opswat.com/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve -->

# Is MetaDefender OT Access affected by NGINX2Root (CVE-2026-123007)?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Last reviewed: November 2026

## [Answer](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve#answer)

No. MetaDefender OT Access is not affected by CVE-2026-123007 or the four related NGINX2Root vulnerabilities in its shipped configuration. No patch, workaround, or configuration change is required.

## [About the vulnerability](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve#about-the-vulnerability)

NGINX2Root is a set of five vulnerabilities in the nginx web server. The lead vulnerability, CVE-2026-123007, is a memory corruption flaw in the HTTP/2 flow-control handling that can allow unauthenticated remote code execution. Its upstream CVSS 4.0 score is 9.2. It affects nginx versions 1.9.5 through 1.31.8 when HTTP/2 is enabled on at least one listener. Fixed versions are 1.30.7 (stable) and 1.31.9 (mainline), released on November 18, 2026.

The five vulnerabilities and the conditions each one needs are:

| CVE | Condition |
| --- | --- |
| CVE-2026-123007 | HTTP/2 enabled on a listener |
| CVE-2026-123633 | HTTP/2 enabled, with requests forwarded to an upstream server |
| CVE-2026-123634 | A `resolver` directive, a request-derived `proxy_pass` destination, and a subrequest feature such as `mirror` |
| CVE-2026-121810 | HTTP/3 (QUIC) listener, nginx 1.25.0 or later |
| CVE-2026-113425 | nginx configured as a mail proxy (`mail` block with `auth_http`) |

## [Why MetaDefender OT Access is not affected](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve#why-metadefender-ot-access-is-not-affected)

MetaDefender OT Access uses nginx as a reverse proxy in front of its web interface and its HTTP/HTTPS clientless access. In the shipped configuration:

- **HTTP/2 is not enabled.** All listeners use plain HTTPS (HTTP/1.1). An HTTP/2 negotiation test against the web interface and the clientless access port confirms that only HTTP/1.1 is offered. This removes CVE-2026-123007 and CVE-2026-123633.
- **HTTP/3 is not available.** The nginx version used by the product predates HTTP/3 support, so CVE-2026-121810 does not apply.
- **No mail proxy is configured.** The product does not use the nginx mail module, so CVE-2026-113425 does not apply.
- **No resolver or mirror is configured.** The conditions for CVE-2026-123634 are not present.

## [Affected versions](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve#affected-versions)

No supported version of MetaDefender OT Access is affected in its shipped configuration. The nginx package used by the product is within the affected version range, so the product would become exposed if HTTP/2 were enabled on a listener. Do not enable HTTP/2 on MetaDefender OT Access.

## [Action required](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve#action-required)

No action is required.

## [References](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-by--nginx2root-cve#references)

- CVE-2026-123007, CVE-2026-123633, CVE-2026-123634, CVE-2026-121810, CVE-2026-113425
