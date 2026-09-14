<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-23 -->

# 3.23

Summarize Page

| Release date | Version |
| --- | --- |
| 27th May 2026 | 3.23 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

### [Enhancements](/docs/mdces3/release-notes/version-3-23#enhancements)

- Added **Additional Filters** in policy configuration, allowing end users to create inbound policies based not only on target audience, but also on sender addresses, sender domains, and email header values. This enhancement provides greater flexibility and precision in applying security controls for different sender types and risk profiles.

### [Bugs](/docs/mdces3/release-notes/version-3-23#bugs)

- Fixed an issue where the Date Sent value in scan details did not match notification timestamps.
- Fixed an issue where forked events were missing audit history entries.
- Fixed an issue causing dashboard charts to occasionally display data offset by one hour.
- Improved threat name extraction accuracy for archive scan results.

Ensured email HTML content consistently terminates with a line break.
