<!-- source: https://www.opswat.com/docs/mdces3/release-notes/version-3-17 -->

# 3.17

Summarize Page

| Release date | Version |
| --- | --- |
| 3rd February 2026 | 3.17 |

**MetaDefender** **Cloud Email Security**™ is an advanced solution that bolsters Microsoft 365’s native email defenses with industry-leading threat prevention. It is purpose-built to detect and neutralize malware, zero-day exploits, and embedded file-based threats before they reach the inbox.

This solution is powered by OPSWAT’s Metascan™ Multiscanning, adding more AV (antivirus) engines, and Deep CDR™ (Content Disarm & Reconstruction) against file-based threats. With multi-layered, proactive protection, email security goes beyond signature-based detection with advanced technologies against evolving threats. Designed for seamless integration, the solution deploys rapidly without disrupting mail flow.

## [Improvements & Fixes](/docs/mdces3/release-notes/version-3-17#improvements--fixes)

### [Dashboard Improvements](/docs/mdces3/release-notes/version-3-17#dashboard-improvements)

- Dashboard license card now shows:

  - License type
  - Expired status
  - User count vs. licensed maximum

### [Operational & Platform Improvements](/docs/mdces3/release-notes/version-3-17#operational--platform-improvements)

- Added **ARC (Authenticated Received Chain) signing** to preserve DKIM/SPF authentication results as emails pass through MDCES.

  - ARC signing activity is also visible in **audit logs** for transparency.
- Super administrators can now manage **multiple organizations (tenants)** from a single account and switch between them directly in the UI.
- Added permission option to **allow users to view scan results** from notifications and reports.
- Added the **Ozzy chatbot** inside the User Actions wizard for quick access to help.

### [Events Improvements](/docs/mdces3/release-notes/version-3-17#events-improvements)

- Events and Quarantine now show **email direction (Inbound / Outbound)**, making it easier to understand where threats originate.
- Email direction is also available in Event Details.
- Added **“Last 1 hour”** time range for Events and Quarantine to quickly investigate active incidents.
