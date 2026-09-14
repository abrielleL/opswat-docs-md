<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-16-1 -->

# 3.16.1

Summarize Page

| Release date | Version |
| --- | --- |
| 17th December 2025 | 3.16.1 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. With multi-layered, proactive protection, email security goes beyond signature-based detection with advanced technologies against evolving threats. Designed for seamless integration, the solution deploys rapidly without disrupting mail flow.

## [Improvements & Fixes](/docs/mdces3/release-notes/version-3-16-1#improvements--fixes)

### [Email Protection & Policy Enforcement](/docs/mdces3/release-notes/version-3-16-1#email-protection--policy-enforcement)

- Fixed an issue where policies were not correctly applied to group recipients, ensuring the intended policies are enforced consistently.
- Improved OTP validation to support secondary domains and email aliases.
- Resolved issues with certain attachment types incorrectly failing analysis.

### [Reporting & Dashboard](/docs/mdces3/release-notes/version-3-16-1#reporting--dashboard)

- Fixed discrepancies between Dashboard metrics and report data for prevented threats and event counts.
- Improved accuracy of Dashboard event counters for released and quarantined messages.
- Updated “Top Blocked Senders” logic to use the sender’s From: address across Dashboards and Reports.
- Improved report filtering and field availability in Quarantine Reports.
- Enhanced date handling in Quarantine Reports.

### [Search & Event Visibility](/docs/mdces3/release-notes/version-3-16-1#search--event-visibility)

- Improved email search reliability when From: header information differs from the SMTP envelope sender.
- Improved audit trail completeness for message rescans and related events.

### [SIEM / SOAR Enhancements](/docs/mdces3/release-notes/version-3-16-1#siem--soar-enhancements)

- Improved SIEM/SOAR configuration experience with clearer guidance and safer handling of sensitive fields.
- Expanded SIEM/SOAR event coverage to include:

  - Quarantined and blocked emails
  - Login and logout events (successful and failed)
- Added configurable filtering to control which events are sent to SIEM/SOAR platforms.

### [Operational & Platform Improvements](/docs/mdces3/release-notes/version-3-16-1#operational--platform-improvements)

- General performance, reliability, and maintainability improvements across the platform.
