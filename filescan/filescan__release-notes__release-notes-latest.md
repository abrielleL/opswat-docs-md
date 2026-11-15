<!-- source: https://www.opswat.com/docs/filescan/release-notes/release-notes-latest -->

# Release Notes for v3.3.1

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Date: 13th November 2026](/docs/filescan/release-notes/release-notes-latest#date-13th-november-2026)

Warning

**Direct upgrade not supported:** Versions earlier than 2.5.1 cannot be upgraded directly to v3.3.1.

**Recommended upgrade path:** Upgrade to 2.5.1 first, then install v3.3.1.

**Clean install advisory:** Use v3.3.1 (or later) for all online clean installations, since previous versions contain a breaking change.

## [MetaDefender Aether™ v3.3.1 (including MetaDefender Sandbox™ capabilities)](/docs/filescan/release-notes/release-notes-latest#metadefender-aether-v331-including-metadefender-sandbox-capabilities)

The MetaDefender Aether v3.3.1 release was created to address installation issues and recent CVEs.

## [**Improvements**](/docs/filescan/release-notes/release-notes-latest#improvements)

- **Clean installation fixed:** A clean online Aether installation was interrupted due to a breaking change in the Python pip package (v26.3). This breaking change affects previous Aether/Sandbox versions since 2.2.0. This new release fixes the installation process by relying on a stable version of the pip package.
- **Upgraded dependencies in Python and Java:** Numerous dependencies were upgraded in both Python and Java to address recently emerged CVEs.

## [**Bug fixes**](/docs/filescan/release-notes/release-notes-latest#bug-fixes)

- **Unknown verdict fixed:** In special cases, the verdict was incorrectly set to Unknown when only one Suspicious threat indicator was triggered. With this fix, the default verdict is correctly set to No Threat Detected in all cases. Therefore, the Unknown verdict can only occur when a real system failure interrupts the scan process.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
