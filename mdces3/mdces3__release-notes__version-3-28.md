<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-28 -->

# 3.28

Summarize Page

| Release date | Version |
| --- | --- |
| 2nd September 2026 | 3.28 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

## [Enhancements](/docs/mdces3/release-notes/version-3-28#enhancements)

- Added batch download for quarantined emails with optional password protection and skip-report support
- Added "No Threat Detected" verdict policy option
- Added AI-generated threat descriptions to event details
- Added Label filter to Events advanced filtering
- Added Origin information to Event and Quarantine details
- Added optional Country/City column to Events list
- Added icons for unsupported file types and sanitization failures within archives
- Split Action Items into Pending and Done sections
- Added audit history entries for Action Item Done/Reopened actions

## [Bugs](/docs/mdces3/release-notes/version-3-28#bugs)

- Fixed SMTP relay failing to relay emails with non-RFC-compliant Message-ID headers
- Fixed missing allowlisted file in scan result details
- Corrected "Blocked" label to "Detected" in the Threat Detection drawer
