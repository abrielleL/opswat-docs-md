<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-22 -->

# 3.22

Summarize Page

| Release date | Version |
| --- | --- |
| 19th May 2026 | 3.22 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, MetaDefender Aether Sandbox for advanced dynamic threat analysis, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. By combining signature-based detection, behavioral sandboxing, and proactive content sanitization, email security extends beyond traditional defenses to identify and neutralize both known and zero-day threats. With multi-layered, proactive protection and advanced technologies designed to combat evolving attack techniques, the solution deploys rapidly and integrates seamlessly without disrupting mail flow.

### [Enhancements](/docs/mdces3/release-notes/version-3-22#enhancements)

- Added a dedicated **Invalid File Structure** verdict under Zero-Day Malware Prevention with its own policy action, Event/Quarantine/SIEM filters, dashboard chart series, and statistics, plus a one-time migration that re-labels historical Suspicious invalid-structure events (upgrade behavior matches the prior Suspicious action).
- Excluded Invalid File Structure events from Advanced Threat Prevention totals so they no longer inflate threat counts.
- Added an **Un-Sanitized Files** section to the Dashboard with a top-5 file-types chart and counters for Sanitization Failures, Unsupported File Types, and Invalid File Structure.
- Added human-readable Microsoft Exchange anti-spam labels (SCL, BCL, SFV, CAT, dest) to Event Details, grouped by spam detection and threat analysis.
- Enabled drill-down into child files of non-archive containers such as `.ics` calendar invites.

### [Bugs](/docs/mdces3/release-notes/version-3-22#bugs)

- Corrected the per-integration user count for tenants with multiple M365 integrations.
- Replaced the maintenance page shown when releasing an email past the retention window with a clear "no longer available" message.
- Fixed a `document_parsing_exception` that prevented SIEM `MESSAGE_PROCESSING` events from being delivered.
- Adjusted the SIEM HTTP Custom Header form — renamed "API key" to "Header value" and "Custom Header" to "Header name", and aligned the input width with the destination dropdown.
- Fixed the wrong value displayed for the current hour on Dashboard charts.
- Reconciled top blocked sender and recipient counts between the Dashboard and the Scan Report for the same time window.
- Corrected text alignment in Advanced Threat Detection and renamed "Suspicious (Sandbox)" to "Suspicious (Aether)".
- Stopped the event list from clearing its column headers during refresh.
