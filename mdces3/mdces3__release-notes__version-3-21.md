<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-21 -->

# 3.21

Summarize Page

| Release date | Version |
| --- | --- |
| 22nd April 2026 | 3.21 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

### [Enhancements](/docs/mdces3/release-notes/version-3-21#enhancements)

- Implemented full mobile responsiveness across the application — collapsible sidebar/drawer, dashboard, events page, policies, settings pages (templates, reports, integrations), and all data tables with card-based mobile layouts
- Added login and logout events to the audit log, captured on the backend and surfaced in the audit log UI

### [Bugs](/docs/mdces3/release-notes/version-3-21#bugs)

- Fixed dashboard charts aggregating in the wrong direction for the 24-hour view, showing stale data, and not updating when switching the timeframe selector
- Fixed the events page refresh button requiring two clicks to display the latest results
- Fixed the incorrect `address` label name shown in event filters
- Fixed a misleading `A task was cancelled` error message being logged on email delivery failure
- Fixed banner not being applied to malicious emails when the policy action was set to Allow
- Integration wizard: Fixed Enterprise Application permissions not being applied correctly during admin consent
