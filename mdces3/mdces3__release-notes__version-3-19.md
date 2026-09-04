<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-19 -->

# 3.19

Summarize Page

| Release date | Version |
| --- | --- |
| 10th March 2026 | 3.19 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

## [**Enhancements**](/docs/mdces3/release-notes/version-3-19#enhancements)

- Added signed and encrypted email flags in Events list and details.
- Added password-provided email flag visibility in the UI.
- Added `RETRYING_DELIVERY` status support in UI filters and views.
- Implemented retry delivery audit trail tracking with error codes.
- Added retry delivery history visibility in email audit trail UI.
- Improved file scan details presentation and consistency.
- Added email direction filter in Events list and advanced search.
- Added sandbox policy configuration support.
- Added sandbox details in file scan results UI.

## [**Onboarding**](/docs/mdces3/release-notes/version-3-19#onboarding)

- Improved onboarding deployment step messaging for better clarity.

## [**Bugs**](/docs/mdces3/release-notes/version-3-19#bugs)

- Fixed user synchronization failures for high user-count tenants.
- Fixed allowlist email field appearing editable when read-only.
- Fixed missing config update broadcasts after new integrations.
- Fixed Firefox render loop caused by cache invalidation behavior.
- Fixed missing Message-ID generation when no ID was provided.
