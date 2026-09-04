<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-20 -->

# 3.20

Summarize Page

| Release date | Version |
| --- | --- |
| 1st April 2026 | 3.20 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

### [Enhancements](/docs/mdces3/release-notes/version-3-20#enhancements)

- Added customizable SMTP routing table per integration to support third-party MTA environments in front of M365
- Added MetaDefender Aether statistics to the dashboard and Policies section
- Grouped file scan verdicts by technology in the event details view
- Added full SMTP server error message to audit history for delivery failures

### [Bugs](/docs/mdces3/release-notes/version-3-20#bugs)

- Fixed archive scan exceeding size limit not being handled correctly
- Fixed user not reappearing in the list after being deleted and re-added
- Fixed encrypted flag disappearing from event details after a failed rescan
- Fixed role label mismatch in the user management modal
- Fixed missing loading indicator when opening the sandbox full report
