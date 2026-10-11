<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v310 -->

# Release Notes for v3.1.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Date: 30th April 2026](/docs/filescan/3.2.0/release-notes/release-notes-v310#date-30th-april-2026)

Warning

**Upgrading directly** from versions prior to 2.5.1 to 3.1.0 is **not possible!**

**Recommended Upgrade Path:** First upgrade to **2.5.1**, then install **3.1.0**.

## [MetaDefender Aether™ 3.1.0 (including MetaDefender Sandbox™ capabilities)](/docs/filescan/3.2.0/release-notes/release-notes-v310#metadefender-aether-310-including-metadefender-sandbox-capabilities)

We're excited to announce MetaDefender Aether v3.1.0 extends its dynamic analysis capabilities with key advances in emulation and behavioral intelligence capabilities. New DLL Emulation enables detection of library-based attack techniques such as DLL side-loading, while MBC Mapping adds MITRE Malware Behavior Catalog coverage alongside existing ATT&CK mappings for richer threat classification.

Together, these enhancements as well as others, deliver broader zero-day detection coverage and deeper behavioral insights across the full threat processing pipeline.

### [What's New](/docs/filescan/3.2.0/release-notes/release-notes-v310#whats-new)

- **MBC mapping added to sandbox signals** — Threat indicators now include mappings to the MITRE Malware Behavior Catalog (MBC), alongside existing MITRE ATT&CK coverage.

- **C2 URL construction from malware configuration** — For supported malware families, C2 server syntax is now parsed and final URLs are constructed when possible. This construction enables the next-stage download attempt.

- **DLL emulation support** — Aether now supports PE emulation for DLL files. It supports detection for attacks that deliver the malicious code in libraries, such as DLL side loading.

- **Enable emulation for base64 strings in documents** — Aether now emulates base64 decoded files, even in cases where string chunks appear separated. Also, it detects invalid Base64 characters within otherwise valid strings.
- **Rust binary metadata detection** — Aether can now detect metadata specific to Rust-compiled binaries, improving classification accuracy for this increasingly common language target.
- **INI file parser and heuristic detection** — Aether now detects and parses INI configuration files, correctly recognizing the media type and extracting embedded artifacts including URLs and threat indicators.
- **HTTP status codes for connection attempts** — HTTP status codes are now added to URL IOCs in the report, providing visibility into whether a download attempt was active at scan time.

- **Threading support improvements and thread‑creation event logging in PE emulation** Emulation now logs thread‑creation events (including creator and new thread IDs and entry addresses), improving visibility into malware execution behavior and concurrency patterns.
- **User configuration for PE emulator -** The user can now specify a custom configuration file for the PE emulator (a default config is delivered with the transform, custom is disabled by default)
- **Configurable PE emulation memory dumping -** New configuration options for API calls allows the PE emulator to dump buffers specified as API call arguments, the moment the configured API is called.
- **Improved offline database update workflows with downloader tooling** Enhanced support for using the downloader tool to apply offline Aether Standalone database updates, making it easier and more reliable to keep isolated or restricted environments up to date.
- **Extended script emulation coverage** for PowerShell, VBScript, JScript and HTML‑embedded scripts, including support for CryptoStream APIs, iterable `Get-Process` results and new PowerShell function patterns.
- **Added new detection “clues”** for encoded / decrypted content, such as `DecodeData` in JScript (`TextDecoder.decode`) and `DecompressData` in PowerShell, improving visibility into unpacking and de‑obfuscation behavior.
- **Introduced richer environment and DOM support** (e.g., `System.Environment]::UserName` in PowerShell, `NodeList.forEach()`, `Document.importNode()` for SVG, WshShell environment getters/setters and additional environment types), enabling more realistic script execution paths.

---

### [Improvements](/docs/filescan/3.2.0/release-notes/release-notes-v310#improvements)

- **Security hardening of dynamic analysis and emulation components** - Reduced security vulnerabilities across the dynamic analysis and emulation stack to lower risk and increase trust in analysis outputs and integration points.
- **Cleaner uninstall behavior for database data** - Updated the uninstall process to remove sandbox‑related database files, reducing leftover data on systems after removal and simplifying environment resets.
- **Higher‑fidelity string and IOC extraction** - Improved the string extraction pipeline and rule coverage using PE emulation output, resulting in more relevant strings and behavior matches with less noise.
- **More robust geolocation handling and reporting** - Improved handling of the new geolocation data structure across background jobs, storage, and report views so that IP counting and country information are stored, processed, and displayed accurately in dashboards and reports.
- **Cleaner data lifecycle and maintenance operations** - Optimized background cleaner modules and user‑data handling so that obsolete or deleted user information and related artifacts are removed more reliably, reducing database clutter and improving long‑term maintainability.
- **Hardened background jobs and OCM‑related flows** - Addressed failures and inconsistencies in scheduled jobs and OCM‑related flows to make background processing more stable across environments.
- **Improved security and usability for credential management** - Enhanced password‑related behavior and configuration in the admin UI to provide a more flexible and secure password setting experience for administrators.
- **More consistent results across related OSINT views** - Aligned the presentation of results between the OpswatReputation and Opswat Metadefender OSINT providers to improve user experience when comparing reputation and OSINT‑driven outputs.
- **Proxy support on Red Hat and Rocky operating systems -**The product can be installed with a standard proxy configuration on these operating systems similarly to Ubuntu: <ADD LINK TO PROXY USAGE PAGE>
- **More efficient extraction and prioritization of deeply nested content** - Refined how embedded archives and extracted files are handled across layers, including updated extraction‑layer semantics and smarter file‑prioritization on the whole layer. This reduces over‑processing of deeply nested archives while still prioritizing the most relevant content for analysis.
- **Stronger stability and robustness around database updates and housekeeping** - Hardened the engine around database package handling and update workflows by improving disk‑space checks, error reporting, and logging; making the consumer hot‑reload process more resilient; and fixing cleanup logic for task‑related temporary files to avoid noisy exceptions and inconsistent states.
- **Cleaner, more secure dependency and configuration baseline** - Resolved multiple dependency‑related security findings, removed unused or obsolete configuration options and helper utilities, and improved test structure for specific emulators. Together these changes reduce attack surface, simplify configuration, and make automated test coverage more targeted.
- **Higher‑quality IOC and URL processing for real‑world content** - Improved decoded‑string and URL handling in scripts (including encoded PowerShell), refined URL renderer behavior in offline mode and for non‑URL resources, and tightened email and URL‑IOC extraction rules. These updates reduce false positives and make extracted IOCs and URLs more accurate and actionable.
- **Enhanced handling of password‑protected and obfuscated samples** - (including reflection by name and password‑protected macros), so more real‑world malicious workflows can be exercised during emulation.
- **Enriched PowerShell “LoadNetAssembly” and related behaviors** - With symbol / context information, making analysis results more informative and actionable.
- **Upgraded underlying packages** - In internal components to keep the emulation stack more robust and maintainable.
- **Detect-It-Easy packer detection integrated into PE emulation filtering** — PE emulation candidate selection now considers packer detections from Detect-It-Easy, not just PEID.
- **IOC extraction moved to direct MWCFG parsing** — IOCs are now extracted directly from parsed malware configurations instead of relying on a generic method, which was less accurate. This removes duplicate URLs and ensures IOCs correctly reflect their malware config origin.

---

### [Bug Fixes](/docs/filescan/3.2.0/release-notes/release-notes-v310#bug-fixes)

- **Aligned malware configuration data model with network indicators** - Updated the malware configuration data model to match the latest network‑indicator schema so that network‑related artifacts are represented correctly and consistently across the platform.
- **More resilient handling of large and problematic documents** - Improved system behavior when processing oversized or malformed content so that “document too large” conditions and related failures are handled gracefully, with clearer reporting and fewer noisy errors in both logs and UI.
- **More stable configuration, profile, and settings workflows** - Fixed multiple issues around export profiles, scan profiles, and settings persistence—including inconsistent validation, incorrect status codes, invalid defaults, and revert behavior—so that profile configuration and settings changes behave reliably across the API, Swagger UI, and admin console.
- **More accurate and reliable reporting and UI behavior** - Resolved several issues in the UI and reporting layer—such as incorrect permalinks, missing CSS in API docs, incorrect URL details in private email scans, and 500 errors when opening specific scan reports—leading to more predictable navigation and reporting.
- **Better filtering, downloading, and sample handling in the UI** - Fixed string and tag filters, scan‑profile‑related download inconsistencies, and incorrect encryption behavior for Daily Samples downloads so that operators can reliably filter data and retrieve samples in the expected formats.
- **More reliable archive extraction and file-type handling** - Fixed failures when unzipping certain ZIP files and addressed scan issues for specific file types, so that previously problematic content is now extracted and analyzed as expected.
- **Improved stability for update handling and engine housekeeping** - Resolved problems where database package re‑submission did not behave as expected and where cleanup of temporary task files could fail, reducing noisy errors and improving the robustness of update workflows and engine housekeeping.
- **More predictable consumer and downloader behavior** - Fixed an issue where the consumer hot‑reload could fail due to an inconsistent Python interpreter state and corrected recursive URL processing in the file‑downloader task, resulting in more stable long‑running processes.
- **More accurate detection for encrypted Office files and emails** - Fixed cases where encrypted Office attachments were not scanned even when the password was guessed correctly, and corrected email detection behavior in the filesystem transform, ensuring these data sources are consistently inspected.
- **Corrected URL and IOC handling in reports and offline scenarios** - Fixed problems where URLs derived from redirects were missing from JSON reports, addressed the URL renderer being active in offline mode, and corrected IOC processing behavior for allowlisted IOCs, so that reported URLs and indicators better match real analysis conditions.
- **PE emulation minor bugfixes -** Addressed a null‑pointer issue in PE emulator results for special cases. Reduced event noise on certain events.
- **Fixed hashing edge‑case errors** - Corrected hash calculation for rendered OOXML images, removing edge‑case failures and making verdicts and hashes more reliable for downstream systems.
- **Fixed multiple emulation failures - S**uch as VBA emulation issues on specific customer malware samples and long delays in samples due to improper `WScript.Quit()` handling.
- **Corrected base capabilities needed for stable detection** **(e.g., PowerShell XOR logging, PowerShell base64 decoding, reverse‑proxy detection logic)** - So that previously failing or noisy behaviors now run reliably.
- **Packed detection overwritten by PE parser** — The parser was overwriting this with its own heuristic result, undoing the DIE detection. The PE parser no longer overwrites a value already set by DIE.
- **UPX not detected as packer for some samples** — Certain UPX-packed binaries were not being flagged as packed. Detection logic has been corrected.
- **Ineligible file types sent to PE unpacking and disassembly** — Files without a valid structure were reaching the PE unpack and disassembly stages, producing errors. These files are now filtered out before reaching those stages.
- **False positives in BTC wallet IOC detection** — The BTC wallet YARA rule was matching Base64 content and producing false positives.
- **Network indicator model mismatch in malware config DTO** — The malware config data transfer object was using an outdated network indicator model. Updated to align with the current model definition.
- **Password extraction regex missing matches** — Two bugs fixed in password extraction from file content process, making extraction more reliable.
- **Installation in FIPS mode** - The product can be installed if FIPS mode is enabled on the host operating system. However, the product does not use FIPS crypto modules internally.

---

## [Threat Detection [v3.0] Release Notes](/docs/filescan/3.2.0/release-notes/release-notes-v310#threat-detection-v30-release-notes)

### [What's New](/docs/filescan/3.2.0/release-notes/release-notes-v310#whats-new)

- **PDF vulnerability coverage** — New detection rules added for file-based PDF vulnerabilities, covering four CVEs identified in recent threat research (CVE-2025-70401, CVE-2025-66520, CVE-2026-1592, CVE-2025-66519), all involving XSS-based exploitation.

- **PHP and ASP webshell parsers** — New parsers for PHP and ASP file types enable detection of server-side webshell files by unwrapping layered obfuscation, recovering executable payloads, commands, hidden strings and decoding vbe files, expanding Aether's coverage of web-based post-exploitation techniques.

- **XOR loop detection for VBScript, JS, and PowerShell** — It detects scripts that perform an abnormally high number of XOR operations at runtime, a common pattern used to decode and execute payloads.

- **Concatenated PDF analysis** — Aether now analyzes both PDFs in a concatenated PDF file. A simple trick that confuses anti-malware engines and AI systems.

  - OPSWAT’s blog: [Concatenated PDFs: A Simple Trick That Confuses Anti-Malware Engines and AI Systems - OPSWAT](https://www.opswat.com/blog/concatenated-pdfs-a-simple-trick-that-confuses-anti-malware-engines-and-ai-systems)
- **New malware config extractors** — Added malware configuration extraction support for malware families `Pikabot` and `Vidar.`
- **Detection for ClickFix-abused command lines** — New threat indicators cover command line patterns used by recent ClickFix variants.

### [What's Improved](/docs/filescan/3.2.0/release-notes/release-notes-v310#whats-improved)

- **Malware config framework refactored to pydantic-based validation** — The MWCFG framework has been fully migrated to a pydantic-validated output structure. Validation is now enforced across all extractors, unprotectors, and community modules via a shared adaptor layer — invalid or malformed configs are no longer surfaced in reports.
- **Rule coverage expanded using PE emulator output** — Closed detection gaps identified by analyzing PE emulator output across known malware samples.

### [What's Fixed](/docs/filescan/3.2.0/release-notes/release-notes-v310#whats-fixed)

- **Data origin correctly set for files extracted by parsers** — Files extracted during parsing now have their data origin assigned correctly, fixing misattribution in scan reports.
- **Hex-decoded IP addresses not handled in HTML parser** — The HTML parser was not correctly processing hex-encoded IP addresses in URLs, such as those appearing in ClickFix samples.
- **Unhandled whitespace in URLs in the HTML parser** — URLs containing whitespace (valid per RFC 3986) were not being parsed correctly.
- **HTML threat indicator incorrectly raising email report verdicts** — An HTML threat indicator increased noise and verdict severity in email scan reports. It was excluded from triggering in the email context.
- **Excluded weak MISP Galaxy tags** — Weak tags were broadly escalating verdict scores across scans, producing widespread false positives. Those weak tags, like `blackhole` and `spyeye`, have been excluded from verdict scoring.
- **Corrected Office document files incorrectly flagged by filename** — Office files containing keywords in their filename were being wrongly flagged as suspicious by the emulator.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
