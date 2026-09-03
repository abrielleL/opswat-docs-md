<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-v300 -->

# Release Notes for v3.0.0

## [Date: 26th January 2026](/docs/filescan/3.1.1/release-notes/release-notes-v300#date-26th-january-2026)

Warning

Upgrading directly from versions prior to 2.5.0 to 3.0.0 is **not supported!**

**Recommended Upgrade Path:** First upgrade to **2.5.1**, then proceed to **3.0.0**.

### [MetaDefender Aether™ 3.0.0 (including MetaDefender Sandbox™ capabilities)](/docs/filescan/3.1.1/release-notes/release-notes-v300#metadefender-aether-300-including-metadefender-sandbox-capabilities)

We are excited to announce **MetaDefender Aether 3.0.0**, OPSWAT’s next-generation unified zero-day detection solution. With this release, the proven **MetaDefender Sandbox dynamic analysis engine is now fully integrated into MetaDefender Aether as Layer 2**, strengthening Aether’s multi-layered detection architecture and delivering deeper, faster, and more scalable threat analysis at the perimeter.

MetaDefender Aether combines **Threat Reputation (Layer 1), Dynamic Analysis via emulation-based sandboxing (Layer 2), and Threat Scoring (Layer 3), and Threat Hunting (Layer 4)** into a single, cohesive solution. This unified approach enables organizations to detect and block known, unknown, and zero-day threats across files, URLs, and IPs before they enter the environment.

#### [What This Means for MetaDefender Sandbox Customers](/docs/filescan/3.1.1/release-notes/release-notes-v300#what-this-means-for-metadefender-sandbox-customers)

MetaDefender Sandbox remains available as a standalone product for customers whose needs are met by a dedicated sandbox solution. However, going forward:

- **All MetaDefender Sandbox capabilities are included within MetaDefender Aether as part of its Layer 2 Dynamic Analysis**
- **MetaDefender Sandbox release updates will also be reflected within MetaDefender Aether release communications**
- Customers upgrading to Aether gain sandbox capabilities plus additional layers of threat intelligence, correlation, and hunting that are not available in a standalone sandbox deployment

#### [Why OPSWAT Integrated MetaDefender Sandbox into MetaDefender Aether](/docs/filescan/3.1.1/release-notes/release-notes-v300#why-opswat-integrated-metadefender-sandbox-into-metadefender-aether)

The threat landscape has evolved beyond what isolated dynamic analysis tools can efficiently address. While sandboxing remains critical, modern security teams face challenges related to **alert fatigue, false positives, performance bottlenecks, and the need to analyze all files at scale.**

OPSWAT evolved MetaDefender Sandbox into a unified MetaDefender Aether architecture to deliver:

- **Higher accuracy over time** through continuously updated, built-in Threat Intelligence
- **Faster detection and response** without the latency of traditional VM-based sandboxes
- **Reduced false positives** through threat scoring, correlation, and contextual enrichment
- **Operational efficiency** by eliminating the need to deploy and manage multiple disconnected tools

By embedding emulation-based dynamic analysis within MetaDefender Aether, OPSWAT enables sandbox verdicts to be immediately enriched with reputation data, historical intelligence, and cross-signal correlation, providing SOC analysts with clearer, more actionable results.

#### [Key Benefits of MetaDefender Aether](/docs/filescan/3.1.1/release-notes/release-notes-v300#key-benefits-of-metadefender-aether)

Organizations adopting MetaDefender Aether benefit from:

- **99.9% zero-day detection efficacy** - Best-in-class file verdicts driven by multi-layer analysis, real-time threat intelligence, and advanced emulation
- **Up to 20× faster file analysis than traditional sandboxes** - Emulation-based dynamic analysis delivers high-fidelity results without the performance penalties of VM-based sandboxing.
- **Massive file volume handling at the perimeter** - MetaDefender Aether is designed to sit at the edge of the organization, inspecting all inbound and outbound files without slowing business operations.

#### [MetaDefender Aether: Built for Modern SOCs & Analysts](/docs/filescan/3.1.1/release-notes/release-notes-v300#metadefender-aether-built-for-modern-socs--analysts)

With a redesigned, intuitive user interface, MetaDefender Aether provides security teams with **clear insights, comprehensive reports, and prioritized threat scoring**, helping analysts focus on what matters most. By correlating sandbox findings with live threat intelligence and historical attack data, MetaDefender Aether reduces noise, accelerates investigations, and improves decision-making across SOC and threat hunting teams.

#### [Next Steps to Upgrade](/docs/filescan/3.1.1/release-notes/release-notes-v300#next-steps-to-upgrade)

Customers currently using MetaDefender Sandbox can upgrade to MetaDefender Aether to unlock a unified, multi-layered zero-day detection platform while retaining familiar sandbox capabilities. To discuss upgrade options or transition planning, please contact your OPSWAT representative.

MetaDefender Aether represents OPSWAT’s vision for the future of zero-day detection: **faster, more accurate, and built to scale, without compromise.**

## [MetaDefender Aether 3.0.0 Release Notes](/docs/filescan/3.1.1/release-notes/release-notes-v300#metadefender-aether-300-release-notes)

The redesigned MetaDefender Aether UI represents a fundamental shift **from a standalone sandbox interface to a unified zero-day detection solution**. Instead of focusing solely on detonation results, the interface is structured around **the full detection lifecycle.**

From the moment a file is opened, analysts see a clear verdict, behavioral tags, and a transparent view of how reputation, emulation-based analysis, threat scoring, and threat hunting contributed to the decision.

Beyond faster understanding, the new design is optimized for real SOC workflows. The result is an interface that reduces cognitive load and accelerates triage and response.

### [What's New Deep-Dive](/docs/filescan/3.1.1/release-notes/release-notes-v300#whats-new-deep-dive)

**Zero-Day Malware Tagging** - Now you can identify high-confidence zero-day malware and hunt previously unseen threats that bypass reputation checks and up-to-date AV signatures. This gives clearer visibility into new malware campaigns before they spread. This feature requires MetaDefender Core or MetaDefender Cloud integration to submit files for AV multi-scanning.

**Report Export Profiles** - Enables configurable report export profiles which allow users to define settings (e.g., page limits, string modes) and select specific profiles via a modal before generating reports.

**Admin Creation for Admins -** Added functionality for Admins to create users with an initial passwords and group assignments via the User Management tab.

### [Improvements](/docs/filescan/3.1.1/release-notes/release-notes-v300#improvements)

**Improved Brand Spoofing Detection Accuracy** - The brand detection model has been retrained to significantly reduce false positives, resulting in more reliable phishing identification.

**Simplified and Enhanced OSINT Lookups** - OSINT lookups were simplified and local reputation results are now visible in the OSINT results as OFFLINE_REPUTATION

**IOC Skip List Migration** - Moved the IOC skip list (allow/blocklist) from the local application database to the separated detection database package to enable frequent updates

**Trends Page MITRE Landscape Table Enhancements** - Color legends have been added to clarify ranking categories and the table has been ordered according to the correct attack timeline.

**Proxy Support for Self-Signed Certificates** - Documented and enabled the addition of CA certificates to Docker containers to support installations behind proxies using self-signed certificates.

**Legacy API Endpoint Removal** - Deprecated legacy API endpoints have been removed

**Core Component Hardening** - Hardened core components with additional security safeguards to strengthen the overall defense posture.

**Batch File-Type Detection** - Enhanced to improve accuracy across complex payloads.

**QR Code Detection Improvements** - Improved to allow the scanning of rendered images in documents and emails

### [Bug fixes](/docs/filescan/3.1.1/release-notes/release-notes-v300#bug-fixes)

**Improved Background Job Reliability -** Refactored database and storage maintenance tasks to prevent job interruptions. The database cleanup job ("Delete reports marked for deletion from db") is now split into independent MongoDB and ArangoDB processes for better performance, and the cleanup jobs are more resilient to `FileNotFoundError` and `AQLQueryExecuteError` exceptions.

**Advanced Search Special Characters -** Fixed issues where Advanced Search failed or returned no results when queries contained trademark symbols or Unicode characters.

**Report Generation Latency** - Resolved performance bottlenecks that had been causing report generation to take excessively long, restoring timely delivery of reports.

**Webservice Stability** - Improved stability under high load by limiting concurrent background jobs and clearing pending scan queues upon restart.

**File Preview for Private Uploads** - Fixed image loading errors for File Preview and URL Details on privately uploaded PDF and EML files.

**BAT Script Classification Fix** - Corrected file-type misclassification for obfuscated BAT scripts, eliminating related false positives.

## [PE Emulator (Beta)](/docs/filescan/3.1.1/release-notes/release-notes-v300#pe-emulator-beta)

**Multithreaded Execution Analysis** - Implemented basic support for creation, management, and emulation of different threads within the emulated process

**Expanded API Emulation** - Extended and improved API coverage

**Expanded API Hooking & Emulation** - Improved emulation flow for nested kernel level API calls

---

## [Threat Detection (v2.0) Release Notes](/docs/filescan/3.1.1/release-notes/release-notes-v300#threat-detection-v20-release-notes)

**MetaDefender Aether supports independent updates to detection logic and threat intelligence**, enabling faster deployment of new protections and a more rapid response to emerging threats. The following updates have been delivered over the past several months.

### [What’s New](/docs/filescan/3.1.1/release-notes/release-notes-v300#whats-new)

- **Significant Enhancements to PE Installer Analysis** - Added deep static extraction and analysis for Windows installers: NSIS, Inno, InstallShield, Advanced Installer, Wise, WiX, InstallAnywhere, and Actual Installer. It now extracts prioritized embedded files, analyzes installer scripts, and scores custom installers heuristically.

- **AI / ML Model Security Scanning** - Introduced security analysis for Machine Learning models, including multi-serialization parsing and deep static inspection to detect hidden malicious payloads before they impact AI workflows.

- **Zero-Day Exploit Detection** - Added detection for recent Windows Explorer LNK vulnerabilities (CVE-2025-50154, CVE-2025-59214) that leak NTLM credentials without user interaction. Also, introduced detection for critical XXE exploitation in Apache Tika (CVE-2025-66516).

- **Phishing Campaign Intelligence** - Introduced indicators for seasonal / opportunistic lures (holidays, global events). Improves campaign clustering and early phishing detection.

- **Invisible String Obfuscation Detection** - It now detects *GlassWorm*-style obfuscation techniques by identifying invisible and deceptive code constructs used to evade analysis and enable silent execution. This includes detection of homoglyph characters, PUA (Private Use Area) Unicode characters, and hidden or non-printable whitespace that visually alters code without changing execution.
- **Advanced Evasion Technique Detection** - Expanded detection for techniques used to evade automated analysis, including meaningless infinite loops, abuse of password-protected in-house macros, .NET PE constant protection and control-flow obfuscation, and deobfuscation of hexadecimal-encoded JavaScript.
- **Expanded File Type & Archive Coverage** - Added support for VSIX files, CRX archives, and improved archive file filtering and prioritization.
- **HTML Threats & Web Payload Extraction** - It now extracts hidden downloadable payloads from HTML href data blobs and improves detection for abused HTML capabilities (e.g., disabled context menu).
- **Detection of IP logging and tracking services** - Added indicators to flag the presence of IP-logging URLs that may be abused by attackers to identify victim location, apply geofencing, or support other reconnaissance and targeting activities, improving visibility into early-stage attack workflows.
- **Flag Covert API Lookup technique in PE Emulation** - It now flags covert API lookup techniques observed during PE emulation, where a program avoids standard resolution methods such as GetProcAddress and instead walks the PEB-linked module lists to directly locate API addresses.

### [Improvements](/docs/filescan/3.1.1/release-notes/release-notes-v300#improvements)

- **Encrypted Documents** - Enhanced decryption for protected Office and PDF documents by introducing a multi-step password recovery with fallback logic for phishing-delivered encrypted files.

- **Base64-Encoded Payload Extraction** - Added base64 decoding for dynamically created files during emulation. This improves visibility into malware that reconstructs payloads at runtime to bypass static analysis and hide secondary stages until execution.
- **ClickFix Variant Detection** - Improved detection for new ClickFix variants that abuse hex-encoded URLs and msiexec execution.
- **Email & Phishing Analysis Accuracy** - Improved EML parsing to correctly associate images with embedded URLs, support text-based attachments, and enhance call-to-action detection across multiple languages.
- **Multi-Stage Infection Chain Visibility** - Improved emulation triggering for downloaded scripts, enabling full infection chain analysis when payloads are fetched from an external resource.
- **Malware Configuration Extraction Output** - Malware configuration results are now returned in a more structured and consistent format, improving downstream automation and reporting.
- **Better Detection Precision & URL Noise Extraction Reduction** - Reduced false positives by refining encryption-related indicators shared by malware and legitimate installers, adapting string-detection heuristics for PE files and making a high-FP URL extraction heuristic configurable.

### [Bug Fixes](/docs/filescan/3.1.1/release-notes/release-notes-v300#bug-fixes)

- **MSI Extraction Reliability** - Fixed multiple issues causing missing or incomplete payload extraction from MSI installers.
- **URL Redirection & Download Chain Handling** - Fixed missing redirected URLs, deduplicated download tasks, and added detection for delayed redirections.
- **Indicator Stability & Engine Robustness** - Fixed unintended indicator triggers (including PDF-related), skipped unnecessary PE disassembly when packers are detected, and resolved multiple internal indicator bugs.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
