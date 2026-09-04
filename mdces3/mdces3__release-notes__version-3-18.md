<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-18 -->

# 3.18

Summarize Page

| Release date | Version |
| --- | --- |
| 19th February 2026 | 3.18 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. With multi-layered, proactive protection, email security goes beyond signature-based detection with advanced technologies against evolving threats. Designed for seamless integration, the solution deploys rapidly without disrupting mail flow.

## [Improvements & Fixes](/docs/mdces3/release-notes/version-3-18#improvements--fixes)

### [Allowlist](/docs/mdces3/release-notes/version-3-18#allowlist)

- Introduced **scope-based Email Sender Allowlist**, allowing configurable security bypass levels.

### [Events](/docs/mdces3/release-notes/version-3-18#events)

- Added flags for:

  - Signed / Encrypted emails (sanitization skipped)
  - Emails delivered after correct password provided.

### [Integration wizard](/docs/mdces3/release-notes/version-3-18#integration-wizard)

- Added Summary step during onboarding
- Implemented **consent polling and auto-resume onboarding** **(Microsoft Entra)**.

### [Mailflow & Processing](/docs/mdces3/release-notes/version-3-18#mailflow--processing)

- Improved ARC signing/sealing support.
- Fixed processing latency calculation
- Fixed suspicious files inside archives returning incorrect overall verdict
- Fixed txt/html attachments not appearing in Attachments tab
- Fixed empty plain text bodies causing “Failure to Analyze” verdict
- Fixed failed-to-scan verdict incorrectly marked as “Skipped” instead of “Failure to Analyze”
- Fixed allowlisted emails with Deep CDR disabled not detecting encrypted content
