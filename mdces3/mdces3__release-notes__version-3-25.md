<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-25 -->

# 3.25

Summarize Page

| Release date | Version |
| --- | --- |
| 24th June 2026 | 3.25 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

### [Enhancements](/docs/mdces3/release-notes/version-3-25#enhancements)

- Added a Sanitization Operations breakdown to the Zero-Day Malware Prevention dashboard, showing CDR operation counts
- Added configurable retention for sandbox reports

### [Bugs](/docs/mdces3/release-notes/version-3-25#bugs)

- Fixed admin role changes not taking effect after a user's next SSO login, which left downgraded users with elevated access
- Fixed the Not Sanitized counter incorrectly rising when an email was sanitized but an individual attachment was not
- Fixed events remaining stuck in "Rescanning" after their original policy was deleted
- Limited Microsoft 365 user sync to active and licensed users
- Fixed whitespace-only integration names bypassing the name filter and creating ghost integrations
- Added validation requiring at least one direction to be selected for Policies
- Added an input length limit for Advanced Filters
- Fixed the incorrect message shown when reviewing an already-released email
- Reordered allowlist audit history into a more logical sequence
- Fixed a bad request error on CSV export
