<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-24 -->

# 3.24

Summarize Page

| Release date | Version |
| --- | --- |
| 11th June 2026 | 3.24 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

### [Enhancements](/docs/mdces3/release-notes/version-3-24#enhancements)

- Introduced sandbox integration to analyze files with active content for deeper threat detection
- Added configurable engine-count thresholds for malicious and suspicious verdicts to reduce false positives
- Added file hash allowlist support for managing trusted files across scanning, verdict, and audit flows
- Added CSV export for the Events and Messages pages
- Enabled rescanning of emails carrying a sandbox verdict
- Fixed an error in the integration wizard that disrupted onboarding
- Fixed the onboarding wizard not pre-populating a sample integration name
- Fixed the Dashboard integrations counter incorrectly counting empty integrations

### [Bugs](/docs/mdces3/release-notes/version-3-24#bugs)

- Fixed emails incorrectly receiving a 'Failure to Analyze' verdict
- Fixed Dashboard graphs and counts not updating without a hard refresh
- Fixed the policy page refreshing when changing a policy status
- Fixed a 'Bad Request' error when creating a policy with a duplicate name
- Fixed the Scan Report showing external recipient addresses under top blocked recipients
