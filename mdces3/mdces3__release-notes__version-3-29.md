<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-29 -->

# 3.29

Summarize Page

| Release date | Version |
| --- | --- |
| 17th September 2026 | 3.29 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

## [**Enhancements**](/docs/mdces3/release-notes/version-3-29#enhancements)

- Added an Add to Allowlist action to Dashboard Top Blocked Senders
- Added a Threats-only / All-Traffic toggle to the Country of Origin & Geolocation dashboard card
- Added an Invalid File Structure action item to the dashboard panel
- Introduced a dedicated Microsoft 365 Anti-Spam Analysis view in event details
- Added a confirmation step when finishing the integration wizard without enabling mail flow rules

## [**Bugs**](/docs/mdces3/release-notes/version-3-29#bugs)

- Fixed wizard footer buttons being hidden behind the page footer on short viewports
- Fixed onboarding buttons being unreachable on very narrow screens before sign-in
- Fixed Prevention result showing "Skipped" instead of "Not Sanitized" for files that failed analysis
- Fixed TNEF-embedded email attachments missing the enclosing subject prefix in filenames
