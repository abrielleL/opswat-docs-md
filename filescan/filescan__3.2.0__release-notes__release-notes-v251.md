<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v251 -->

# Release Notes for v2.5.1

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## Date: 18th November, 2025

## MetaDefender Sandbox 2.5.0 Release Notes

Sandbox 2.5.1 provides OCM-10 integration and several enhancements in this release.

### What’s New

- **OCM-10 Integration -** Enhanced OCM - Sandbox integration with support for, license management, and health monitoring for improved centralized management.
- **Offline Mode Certificate Validation** - Added a transform configuration to whitelist signed files without revocation checks; auto-enabled in air-gapped environments, but can be disabled for maximum security.

### Improvements

- **Offline URL Model Update -** The URL Reputation Predictor (formerly Offline URL Model) now packs twice the training data for stronger, smarter predictions.
- **Stability & Security -** Updated core dependencies to enhance performance and security.

### Bug Fixes

- **Trends Page Accuracy -** Improved IOC accuracy by refining query logic and whitelisting trusted domains.
- **Trends Page “Last 24 Hours” Filter -** Fixed filtering logic to ensure accurate 24-hour statistics.
- **YARA Rules Display -** Improved YARA rule handling in the UI to ensure consistent and accurate display for similarly named rules.
- **Email History Pagination -** Fixed pagination on the email history page to display unique and accurate results across all pages.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
