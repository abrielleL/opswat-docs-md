<!-- source: https://www.opswat.com/docs/mdcore/release-notes/archived-release-notes -->

# Archived release notes

## [Version v5.22.0](/docs/mdcore/release-notes/archived-release-notes#version-v5220)

Release Date: 26 August 2026

**New File Structure Validation Engine**

Malicious content increasingly hides within document structures where traditional signatures cannot reach. **File Structure Validation (FSV)** inspects each file against its format specification and identifies embedded files, images, fonts, hyperlinks, metadata, and other elements. It enforces structural security policies without modifying the original file, while extractable content is scanned separately so content is not judged by its wrapper alone.

FSV is integrated across MD Core: per-file-type control in workflow configuration, structural findings in the processing result, activity on the dashboard, and a dedicated section in both PDF and CSV executive reports.

**Reuse processing result for archives**

Hash-based reuse of processing results now covers archive files, not only non-archive submissions. Repeated scans of the same archive can skip a full re-extract and re-scan when reuse is enabled.

**Skip by Hash approval expiry and auto-removal**

Skip-by-hash allowlist and blocklist entries can carry an expiry date. When the time is reached, the hash is removed automatically so temporary approvals do not stay forever.

**Email alerts for RAM and CPU utilization**

Email notifications can fire when RAM or CPU crosses a configured threshold, in the same style as existing disk-space alerts.

---

**Stop processing files with a mismatched file type**

A workflow can now be configured to stop processing a file as soon as a mismatch between its detected type and its extension is identified, rather than continuing through the remaining engines. For customers who reject mismatched files as a matter of policy, this shortens scan time and spares resources on traffic that would be blocked anyway.

**Further Enhancements**

**1) Force password change on first local login**

A configurable policy can require local users to change their password on first login. LOCAL accounts only

**2) Create user API can mint an API key**
The Create user API can create an API key as part of user creation, so automation does not need a second step after the account exists. Please check details: [POST - Create user](/docs/mdcore/metadefender-core#usercreate)

**3) Webhook callback API key**

An custom header can be passed through to a webhook server when a file is submitted to the callback API, so the webhook endpoint can authenticate the request. [POST - Analyze File (Asynchronous mode)](/docs/mdcore/metadefender-core#fileanalysispost)

**4) In-product notice when a newer Core version is available**

Administrators can be notified in the console when a newer MetaDefender Core version is available.

**5) API to list**`data_id`**values**

A new API returns a list of `data_id` values so integrations can page or batch-query scan objects without walking history one file at a time. [MetaDefender Core API](/docs/mdcore/metadefender-core)

`GET` - `/file/ids`

Support filtering:

1. Time windows
2. Size and limit
3. Original file (submitted file) vs extracted file vs batch

**6) Global timeout now includes end-to-end file handling time, not only engine scan time**

Under Enable Global Timeout, a new child option Include all file handling stages in timeout calculation can count the full file lifecycle, not only time after the file enters the scan queue. That includes upload or streaming, write to storage, hash calculation, queue wait, and scan processing.

**7) Dependable central management, even when an instance is struggling**

Health status reporting to My OPSWAT Central Management (MOCM) is now paced to at most one report per configured reporting interval. A struggling instance no longer sends many reports per second, loading Central Management at the moment it is already under strain.

When MOCM offers a configuration that MetaDefender Core (MD Core) cannot apply, the rejection is now reported in full only for the first few consecutive attempts and summarized after that. One invalid setting no longer writes the complete configuration into the audit log on every sync interval.

**8) Health reporting to central management recovers automatically**

An enrolled instance that stopped reporting its health to My OPSWAT Central Management, because the reply to an outstanding report never arrived, now starts reporting again by itself. Recovery happens immediately on re-enrollment, and otherwise within the hour. Previously the instance stayed silent indefinitely and appeared stale in the Central Management console, with an unenroll or a full service restart as the only way back.

**9) More reliable engine updates from Central Management**

A damaged update package no longer stalls the engine and signature database updates queued behind it. Packages received through My OPSWAT Central Management (MOCM) that cannot be processed now fail cleanly and stay available to retry, while the remaining updates continue to install.

**10) Engine deployment that fails fast instead of hanging**

An engine or database deployment that cannot start no longer leaves the module stuck in Staging. The wait is now bounded: if the start does not complete, the deployment fails with a clear warning, cleans up after itself, and stays available to retry. Recovering no longer means removing the engine or restarting the service. Additional log detail across the staging phase also gives Support a clearer picture when a deployment does not behave as expected.

**11) A Failed count you can act on**

The *Failed* figure on the dashboard and in processing history now counts genuine processing failures only: *Failed*, *Extraction Failed* and *Scan Failed*. Objects that an operator cancelled, and objects that reached a configured processing limit, are no longer counted among them, so the number means what it says and can be trusted as an alerting signal.

**12) One consistent vocabulary across every result**

The six analysis categories in Processing History, covering advanced threats, vulnerabilities, threat signatures, origin, data loss and sanitization, now describe their outcomes in the same language. The same wording is used across the Processing History list, its CSV export and the executive report, so a result no longer reads differently depending on which column or which export it appears in.

**13) Clearer feedback when adding a certificate**

Selecting an empty certificate file in the *Add certificate by content* dialog now explains why the file cannot be used, instead of leaving the Add button disabled with no indication of the cause.

---

**Security Enhancements**

Upgraded 3rd party libraries:

- PostgreSQL v18.6
- SQLite v3.53.4

---

**Bug Fixes**

- Fixed an issue that Processing History could not show data after a scan of special cases. This is a displaying issue; your data in database is retained as is, and REST API integrations work properly.
- Fixed an issue where a cancelled scan was not reported as cancelled in JSON exports, log files, and syslog.
- Resolved an issue where importing a settings package could fail intermittently when a configuration value exceeded its length limit, silently keeping the previous configuration.

## [Version v5.21.0](/docs/mdcore/release-notes/archived-release-notes#version-v5210)

Release Date: 30 July 2026

**All-new MetaDefender Core interface**

Meet the all-new interface—designed for speed and comfort. With built-in dark mode, enhanced accessibility support, and seamless interactions, every workflow feels more natural and efficient.

Below are some of the key highlights:

A brand-new, comprehensive dashboard

A completely redesigned dashboard featuring refreshed versions of existing metrics, making it easier to monitor your system, along with brand-new insights such as the CVE Detection Trend.

Easily monitor and submit scans, including split archive submissions

New look and feel for the Processing History and Processing Results pages

Work comfortably in low light with built-in dark mode

---

**Splunk integration settings in MetaDefender Core**

A dedicated **Splunk** section in MetaDefender Core makes it easier to connect Core to your Splunk environment. Add and manage Splunk connections, set the log level, allow self-signed certificates when needed.

Users can also integrate with Splunk during installation via Wizard steps.

---

**Support PostgreSQL v18**

MetaDefender Core now starts supporting PostgreSQL v18 (verified with 18.4).

Bundled PostgreSQL server comes with MetaDefender Core standalone deployment also comes with this new version.

**Note**:

- PostgreSQL v18 itself cannot initialize its database cluster when the Windows system locale name contains non-ASCII characters. For example, Turkish Windows uses the locale `Turkish_Türkiye.1254`, which contains `ü`. Instruction for safe upgrade at [Upgrade to MetaDefender Core 5.21.0 or later on Windows systems with a non-ASCII locale](/docs/mdcore/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale).
- If your bundle PostgreSQL password contains non-ASCII characters (for example `£`, `€`, or accented letters), the upgrade may fail and prevent console login. ASCII special characters such as `&`, `~`, and `\` are not affected. Before upgrading, change the PostgreSQL password to ASCII-only - please check [Database Management](/docs/mdcore/configuration/database-management) for change password

---

**Redacted file name in output filename configuration**

Output filename formatting now supports Proactive DLP redaction results through two new tokens: `${redacted.basename}` and `${redacted.extension}` (available in `short` and `long` formats). These tokens allow for the automatic use of masked filenames across DLP output, Deep CDR sanitized output, and archive tombstone names, ensuring sensitive information is removed from file names. If no redaction occurs, the tokens automatically fall back to the original filename and extension.

---

**Block unsupported file types in Proactive DLP**

Proactive DLP can now be configured to block files it identifies as an "Unsupported File Type", rather than releasing them as "No Threat Detected". This gives security teams stricter control over content that Proactive DLP cannot fully inspect, aligning DLP behavior with fail-closed policies.

---

**Centralized "Skip by Hash" management via My OPSWAT Central Management**

MetaDefender Core now supports centrally managing the "Skip by Hash" configuration (Skip Engines, Allowlist, and Blocklist) from My OPSWAT Central Management (MOCM). Administrators managing multiple Core instances can maintain hash lists once in Central Management and have them synchronized to all enrolled Cores over the existing heartbeat channel, instead of maintaining lists on each instance individually. Centrally managed hashes are enforced as read-only on the local Core while enrolled, a new Origin column and awareness banner indicate which entries are managed by Central Management, and configuration backups from older Core versions remain importable.

**Dependency and availability:** This feature requires updates on **both MetaDefender Core and My OPSWAT Central Management (MOCM)** — the Core-side changes ship in this release, but end-to-end centralized management is only available once the corresponding MOCM support is released. MOCM plans to release this feature in **mid-August 2026**.

---

**Further Enhancements**

**1) Clearer "Extension-Based Processing Fallback" configuration**

The "Fallback file type detection to current extension if needed" option has been renamed to "Enable Extension-Based Processing Fallback" and its description has been updated to better reflect its expanded functionality. The option now uses the file extension as a secondary file type for processing when needed, reducing confusion for administrators when configuring workflows.

**2) Improved error visibility for archive extraction failures**

The scan-result UI now makes it easier to see the full error path when extraction fails deep inside large, multi-level archives, so operators can identify the problematic nested file without clicking through the archive one level at a time.

**3) More meaningful extraction error messages**

Extraction error messages have been improved to provide clearer, more detailed information, replacing generic or ambiguous wording so customers can better understand why extraction did not complete.

**4) Classify Global Timeout Exceeded as Allowed when configured in workflow general settings.**

Global Timeout Exceeded is now available under Workflow Management → General → Processing results to be classified as Allowed, so you can choose whether scans that hit the global timeout are treated as Allowed like other configurable outcomes.

**5) Post Actions support sanitized files and optional filtering by sanitized file type.**

Post Actions can now run for **sanitized** files, not only threat-related verdicts. You can also limit actions to **specific file types** (for example PDF, XLS, or DOCX) so downstream steps apply only to the formats you choose.

**6) In-app alerts when disk space is low**

When available disk space drops below configured thresholds, administrators now get an **in-app notification** in the MetaDefender Core web UI—in addition to existing email alerts and dashboard status—so low-disk conditions are hard to miss no matter which page you’re on.

---

**Security Enhancements**

- Hardened license activation connectivity test: the license activation server connectivity test endpoint has been hardened to restrict the destinations it will connect to, mitigating a blind server-side request forgery (SSRF) issue that could otherwise be used to probe internal hosts and ports
- Upgraded 3rd party libraries:

  - c-ares (bundled within the gRPC) v1.34.8
  - yamlcpp v0.9.0
  - nghttp2 v1.69.0
  - NGINX v1.30.4
  - sqlite v3.53.3
  - libxml2 v2.15.3
  - PostgreSQL v18.4

---

**Bug Fixes**

- Improved startup when several MetaDefender Core nodes share one database (shared-db), so concurrent restarts are less likely to hit database privilege deadlocks and fail to come online.
- Improved NGINX log rotation on Windows by storing runtime config outside temp and recovering when the config file is missing.

## [Version v5.20.0](/docs/mdcore/release-notes/archived-release-notes#version-v5200)

Release Date: 30 June 2026

**New Technology: OPSWAT Alin AI Deflection**

OPSWAT Alin AI Deflection is an AI-driven, ML-based malware deflection engine. It analyzes the structural and byte-level signals of executable, document, and office files to determine whether a file can be confidently skipped from heavier scanning engines — reducing scan overhead without compromising detection.

Administrators can configure deflection in the **Workflow Configuration** settings for **OPSWAT Alin AI Deflection** to define which verdicts trigger deflection and which processing engines are skipped when a file is deflected.

---

**Remote product upgrade through My OPSWAT Central Management**

Administrators can now remotely upgrade MetaDefender Core (MD Core) instances directly from My OPSWAT Central Management (MOCM), eliminating the need to log in to each instance individually. This feature is supported on both Windows and Linux.

**Note:** Remote upgrades require MD Core **5.20.0** or later. You must first manually upgrade each MD Core instance to version 5.20.0. Once an instance is running 5.20.0, all subsequent upgrades can be performed remotely through MOCM.

---

**Auto Troubleshooting — know your MetaDefender Core deployment is healthy at a glance**

No more digging through logs or running manual tests to confirm everything is running smoothly. The new Troubleshooting dashboard gives administrators a clear, real-time view of system health in one place.

Issues are surfaced automatically and explained in plain language, so you know exactly what needs attention — and what's just fine as-is. When you want a closer look, a single click runs a deeper analysis on demand.

Spend less time investigating and more time being confident that your deployment is protected. Spot problems early, resolve them faster, and share results with support in seconds.

Check more details at [Auto Troubleshooting](/docs/mdcore/operating/auto-troubleshooting).

---

**Archive Forensic**

Finding a single problematic file buried inside an archive just got easier. Archive Forensic automatically captures flagged sub-files during archive processing and stores them in a dedicated, secure location — so you can retrieve exactly what you need without sifting through the entire archive.

When enabled per scanning rule, MetaDefender Core preserves child files matching your configured trigger verdicts, encrypts them at rest with AES-256-GCM, and makes them available as password-protected ZIPs. Office documents are smartly skipped to keep your forensic store clean.

View, search, download, and manage your captures anytime: [Archive Forensic](/docs/mdcore/operating/archive-forensics).

---

**Export Templates for Core Scan Results**

Allow user to save export scan result options selection as named, reusable templates for ease of use when exporting scan results. Templates are tied to each user, maximum of 10 templates per user.

---

**MetaDefender Core Deployment Readiness Tool**

Wondering if your system is ready to install or upgrade MetaDefender Core? The new Deployment Readiness tool gives you an instant answer — no more manually cross-checking documentation. Just download the single, lightweight binary (no installation needed) and run it.

In one pass, it checks your OS, hardware, dependencies, database, ports, permissions, and potential software conflicts — then produces a clear console summary and a self-contained HTML report you can save or share. It even auto-detects your engine count and product configuration, and keeps its requirements up to date automatically from OPSWAT servers.

Available for both Windows and Linux: [Download](https://my.opswat.com/portal/home/metadefender-core)

Under MetaDefender Core / MetaDefender Core Deployment Readiness Tool

Example of HTML report

---

**Further Enhancements**

**1)** **SSO Support Behind SSL-Terminating Reverse Proxies**

Added support for the `X-Forwarded-Proto` header to improve SSO compatibility with deployments where SSL/TLS is terminated by a reverse proxy. MD Core now correctly detects the original request protocol when generating SSO redirects.

**2) SBOM and Vulnerability Assessment reporting enhancements**

Reporting coverage has been extended for software bill-of-materials (SBOM) and Vulnerability Assessment data.

- SBOM export (PDF) is now supported for batch scans.
- Vulnerability Assessment details are now included in exported reports (PDF) for subfiles within an archive scan.

**3) Sanitized file size added to logs**

The size of a file after sanitization is now recorded in the logs, improving traceability, auditing, and operational visibility when sanitization occurs.

**4) AI Content Inspector output folder included in storage monitoring**

The dedicated folder that the AI Content Inspector uses to store output images is now included in the storage-folder monitoring feature, so its disk usage is visible on the dashboard alongside other monitored storage.

**5) My OPSWAT Central Management integration enhancements**

- Newly enrolled MetaDefender Core (MD Core) instances now synchronize to their assigned set and pull engine and definition updates immediately upon registration with My OPSWAT Central Management (MOCM).
- The last MOCM sync time is now written to the MD Core logs instead of the configuration history.

**6) Configure Log Rotation from the Web Console**

Managing log retention no longer means editing config files. You can now control how MetaDefender Core handles logging directly from the web console — set the **maximum log file size**, choose your **rotation interval**, and define how many **rotated files** to keep. Tune your logging to fit your storage and compliance needs in just a few clicks.

**7) Test Your Email Server Configuration**

No more guessing whether your SMTP settings are correct. Under **Settings > Network > Email**, you can now send a test email directly from MetaDefender Core to verify your server configuration in seconds.

**8) Configurable Syslog Facility**

You can now tag MetaDefender Core syslog messages with a specific facility, making it easier for your SIEM, Splunk, or rsyslog server to route, filter, and retain Core logs separately from other applications. Set it under **Settings → Logging → General**, under Log format.

Most users can leave this alone — the default (`daemon`) keeps the same behavior as before. Change it only if your security or operations team asks Core logs to carry a specific category (commonly `local0`–`local7`). Changes take effect immediately, with no service restart required, and a single facility applies to all syslog output across both remote (UDP/TCP/TLS) and local syslog.

**9) Multiple Schedules per Report**

You're no longer limited to a single schedule per report. MetaDefender Core now lets you configure up to three scheduled times for each report type — so you can, for example, send a weekly History report every Monday morning *and* a monthly summary on the 1st. Set each schedule's timing, time range, and verdicts independently to match the way your team actually consumes reports.

**10) Richer Report Columns**

Scheduled reports and manual Processing History exports now include six new columns — **Threat Found, Total AVS Engines, Threat Detected By, File Size (KB), Threats, and Metadata** — giving you deeper insight into every scan. Columns are also reordered to group related fields logically (scan timing, threat details, and file metadata together).

**11) Usage Reporting**

With Usage Reporting enabled, MetaDefender Core shares anonymous usage metrics with OPSWAT — giving us the insight to improve performance, prioritize the features you rely on, and deliver a better overall experience.

We only collect neutral operational data. No sensitive information, no file contents, no personal data — ever. You stay in control and can enable or disable reporting at any time.

---

**Security Enhancements**

- Fixed an authentication bypass vulnerability that could allow an attacker to impersonate a user by using a valid SAML response.
- Added a limit on the number of parts accepted in `multipart/form-data` request bodies to improve request handling and security.
- Fixed an XML External Entity (XXE) injection vulnerability in the SAML response XML parser,
- Fixed an operating-system command injection vulnerability caused by unsanitized command-line arguments passed to popen().
- Fixed a postMessage origin-validation bypass in the management console caused by endsWith suffix confusion during origin checks.
- Upgraded 3rd party libraries:

  - 7z v26.02
  - OpenSSL v3.5.7
  - NGINX v1.30.3

---

**Bug Fixes**

- Fixed a heap-corruption crash in the engine process that could occur when engines were repeatedly disabled and enabled over an extended period.
- Fixed an issue where an engine's `maximum_thread_count` and a custom parallel count was not enforced at runtime, so the engine remained capped at the default limit even when configured higher.
- Fixed an issue where password-protected documents failed when "Block unsupported file types" was enabled in Deep CDR during split-archive processing.
- Fixed an issue where scan-result tab names were truncated when the tab bar overflowed.
- Fixed an issue where a temporary file created by the AI Content Inspector was not deleted after a scan request was canceled.

## [Version v5.19.0](/docs/mdcore/release-notes/archived-release-notes#version-v5190)

Release Date: 21 May 2026

**New Technology: OPSWAT AI Content Inspector**

OPSWAT AI Content Inspector is a new technology introduced in MetaDefender Core. It is an AI-driven content authenticity and document fraud detection engine designed to help organizations identify suspicious or manipulated content before review, approval, or payout processes.

It analyzes visual, textual, and structural signals across documents and images to detect potential fraud in invoices, insurance claims, accident photos, and other high-risk content.

---

**Automated support package generation and transfer to My OPSWAT Central Management**

MetaDefender Core’s support packages can now be generated on demand from MOCM and automatically uploaded to MOCM for centralized retrieval. This is particularly valuable for instances in remote or restricted environments where Support previously had to coordinate with the local administrator to collect logs.

---

**Differentiated verdict for RMS-protected Office documents**

Password-protected and RMS-protected (label-protected) Office documents were previously classified under a single verdict, "Password Protected Document." Both file types are now reported separately as *Password Protected Document* and *RMS Protected Document*. The new verdict is recognized end-to-end in verdict filtering on Processing History, the verdict result highlighter, scheduled report emails, and email notifications for processing activity.

Info

To preserve backward compatibility, *RMS Protected Document* is enabled by default in existing settings (such as email notifications and scheduled reports) during upgrade or configuration import, so customers continue to receive coverage equivalent to their previous configuration.

---

**Further Enhancements**

**1) Faster processing result retrieval during engine updates**

Processing result API calls could previously stall behind an in-progress engine update, occasionally exceeding the 150-second NGINX timeout for customers with large workloads. The internal lookup of engine configuration last-modified time is now served from a cache, so result retrieval no longer waits on engine updates to complete and returns results promptly even while engines are mid-update.

**2) Verdict origin indicator for scan categories and errors**

The management console now indicates whether a scan category or error (for example, "Calculate Hash Error") was determined by MetaDefender Core itself or by the underlying scan engine. A visual indicator clarifies the origin so administrators and Support can more quickly route and triage issues.

**3) Adaptive Sandbox skip handling for unsupported file types**

Adaptive Sandbox previously sent files with the Metascan verdict `Unsupported File Type` for sandbox analysis because that verdict was missing from the skip-evaluation list. This verdict is now recognized, ensuring unsupported file types are skipped from sandbox processing as intended and reducing unnecessary sandbox resource consumption.

**4) A clearer blocked reason for scans interrupted by the MetaDefender Core restart**

When the MD Core service restarts mid-scan, in-process scans are now reported with an explicit failed block reason rather than an empty reason. This makes interrupted scans easier to identify in processing history and downstream reporting, improving auditability after unexpected restarts.

**5) Deep CDR output filename exception by filename and extension**

Deep CDR users can now define output filename exceptions based on filename or extension, in addition to the existing exceptions based on detected true type. This enables, for example, converting one extension to .txt while preserving another extension's original suffix in the sanitized output filename, even when both files share the same detected true type.

**6) Engine package compatibility flag**

The `stat/packages` API now includes a boolean-supported field on each engine and database package entry, making it clearly visible whether a package is compatible with the currently running MetaDefender Core version. This simplifies inventory and compatibility validation for administrators and integrators.

**7) Delayed start for the MetaDefender Core service on Windows**

On Windows, the MD Core service is now configured with the "Automatic (Delayed Start)" startup type. This ensures the operating system has finished initializing dependent services — particularly network interfaces — before MD Core starts, preventing a few unexpected behaviors.

**8) Additional SBOM fields in the PDF report**

The Software Bill of Materials (SBOM) PDF report has been expanded with additional fields requested for compliance frameworks such as CERT-in. Customers benefit from a richer SBOM artifact that more closely aligns with regulatory and industry reporting requirements.

**9) Additional Metascan engine information in the Export Result**

The Export Result option for processing details now includes per-engine information for Metascan engines. The "AV Engines" column in Advanced Export has been renamed to "Engine Name," and two new fields — "Engine Version" and "Database Version" — are now exported alongside it. These values are also preserved for results that were originally scanned on a previous MetaDefender Core version after the upgrade.

**10) Reorganized workflow configuration tabs**

The Workflow configuration tabs have been reorganized by functional group, making settings easier to discover and configure.

**11) Improved tab display for long engine names in Advanced Export**

Engine names in the Advanced Export tab are now properly fitted within their containers, eliminating overflow that occurred for engines with long display names.

**12) Disk space monitoring in health check policies**

Health check policies can now monitor the free disk space on the MetaDefender Core installation drive. If available space falls below the configured threshold, the instance is flagged as not ready for file processing.

**13) Outdated engine detection in health check policies**

Health check policies can now flag engines whose definitions have not been updated within a configurable number of days. Administrators can specify which engines are required and how many days old their definitions can be before the health check fails.

**14) Email notifications based on final scan status**

Email notifications can now be triggered by a file's final status, such as when a file is blocked, in addition to the existing scan-result triggers (Infected, Suspicious, and so on). This is useful when you care more about enforcement outcomes than the specific findings behind them.

**15) Prevent engine downgrade**

MetaDefender Core now includes a setting that blocks downgrades of engine and database packages, protecting deployments from accidental rollbacks to outdated threat definitions. This setting is disabled by default.

**16) Proxy connectivity test**

Administrators can now validate proxy settings before saving them. The test verifies connectivity to the updater and activation server, helping avoid misconfigurations that would otherwise only surface when updates silently fail.

**17) Out-of-date engine notification banner**

The system banner now includes a setting to notify administrators when scan engines are out of date. A global threshold can be configured in days, with the option to override it per engine.

**18) Configuration History — Collapsed Diff View**

The Configuration History page now displays only the changed lines in a collapsed diff view, making it easier for administrators to identify what was modified in configuration or workflow policy changes.

---

**Security Enhancements**

Upgraded 3rd party libraries:

- NGINX v1.30.1
- PostgreSQL v14.23

**Bug Fixes**

- Fixed an issue where some My OPSWAT Central Management-related configuration screens reported a successful save while the underlying value failed validation.
- Fixed an issue where the Adaptive Sandbox verdict was reported as "System Error" in the PDF export when the scan was cancelled mid-processing.
- Fixed an issue where archive scan results displayed an "Exceeded Archive File Number" extraction issue without an associated count of affected files. The count is now correctly populated for the root archive.
- Fixed an issue where the workflow rule name filter in Executive Reports did not reflect renamed rules, leaving the old name in the filter. The filter now correctly reflects the current rule name.

## [Version v5.18.1](/docs/mdcore/release-notes/archived-release-notes#version-v5181)

Release Date: 15 April 2026

Upgraded 3rd party libraries:

- Libxml2 v2.15.2
- OpenSSL v3.5.6
- Angular libraries

Bug Fixes:

- Fixed a stability issue that, in rare cases under heavy load, could cause MetaDefender Core within MetaDefender Cluster to crash during extraction distribution.

## [Version v5.18.0](/docs/mdcore/release-notes/archived-release-notes#version-v5180)

Release Date: 31 March 2026

**Workflow Visualization**

The newly introduced Workflow Visualization provides a high-level overview of scan workflows. By rendering engine execution sequences as intuitive directed graphs, this feature enables users to perform inline configuration edits and search specific settings directly within the visualization interface.

---

**Workflow Setting Instant Lookup**

The introduction of global search functionality across workflow rule settings facilitates the instantaneous location of configurations. By providing the full breadcrumb navigation path within search results, the system allows for seamless redirection to any specific setting.

---

**Feature Enhancement: Blocklist and Allowlist File-Type Configuration**

Less friction, more control. Users can now configure lists in seconds via a simplified interface, while a dedicated search feature allows for navigation to specific file types. More details at [Blocklist by filetype configuration](/docs/mdcore/configuration/blocklist-by-filetype-configuration).

---

**Connectivity Monitoring and Troubleshooting**

Gain immediate visibility into the connectivity status between MetaDefender Core and its update sources. The system now diagnoses update impediments and provides remediation steps to ensure all engines remain current.

---

**Shared Database Mode supports My OPSWAT Central Management v10**

Shared Database Mode is now supported for enrollment in My OPSWAT Central Management v10 (MOCM). This enhancement enables multiple instances sharing a database to be managed through MOCM, though certain limitations apply to certificate management and configuration synchronization in mixed-mode environments.

Please refer to [My OPSWAT Central Management](/docs/mdcore/configuration/my-opswat-central-management) for more details.

---

**Centralized SSL/TLS Secure Connection Management**

MetaDefender Core has been enhanced to support synchronization of SSL/TLS configurations with MetaDefender Managed Central Management (MOCM). This improvement allows for centralized management of secure connection settings and certificates, ensuring consistent security policies across managed instances.

---

**Encrypted Download for Quarantined Files**

Starting from version 5.18.0, users can download quarantined files with password protection. This feature enhances security by allowing files to be encrypted during download, helping prevent accidental execution due to unintended user actions.

More details at [Download quarantine files](/docs/mdcore/operating/download-quarantine-files).

---

**New OS Support**

This release of MetaDefender Core introduces official supports for Debian 13, Windows 11 24H2 and Windows 11 25H2.

Note: Windows 11 only for End-User systems (e.g. Kiosk deployments).

---

**New Option to Combine SSO User Roles from All Matching Rules**

SSO role mapping now supports combining roles from all matched rules, allowing users to receive a broader set of permissions when multiple mappings apply. This option is disabled by default.

---

**Further Enhancements**

**1)** **Selective SBOM PDF Export Options**

The Software Bill of Materials (SBOM) PDF export functionality has been enhanced to allow you to selectively export only vulnerable or problematic files rather than the entire package list. This improvement significantly reduces PDF generation time for large packages and provides a more focused, concise report of security concerns.

**2)** **Default Archive Support for Adaptive Sandbox**

Adaptive Sandbox has been enhanced to enable supported archive file types by default, ensuring files such as JAR, SFX, and PKG are automatically processed for security analysis without manual configuration. This feature is available when using MetaDefender Core 5.18.0 or later in combination with Adaptive Sandbox 3.1.1 or later.

**3)** **Granular Sandbox Trigger Rules for Deep CDR Verdicts**

Adaptive Sandbox trigger rules have been enhanced to provide independent configuration options for "Sanitized" and "Sanitized Partially" verdicts. This improvement allows for more granular control, enabling users to trigger sandbox scans specifically for partially sanitized files while excluding fully sanitized ones to optimize resource usage.

**4)** **Enhanced workflow-level filtering of Reputation results for Adaptive Sandbox**

MetaDefender Core has been enhanced to allow bypassing all other scan-result filters when a file is identified as Known Good or Known Bad by the Reputation engine. This improvement prevents unnecessary sandbox analysis for files with established reputations, optimizing system performance and resource utilization by default.

**5)** **Support for Trailing Slashes in OCM Enrollment URLs**

MetaDefender Core has been enhanced to automatically handle trailing slashes in My OPSWAT Central Management (MOCM) enrollment URLs.

**6)** **Enhanced Archive Extraction Visibility in Scan Results**

Scan results and executive reports have been improved to provide greater transparency into archive processing by including critical extraction details. These reports now explicitly display the maximum archive nesting level reached, the total number of extracted files across all nested levels, and the total size of extracted data, allowing for better configuration of workflow extraction limits.

**7)** **Clearer Extraction Status for Cancelled Archive Scans**

Archive extraction monitoring has been enhanced to accurately report when a scan is manually cancelled. Extraction issues previously categorized as "Extraction Error / Unknown" due to canceled are now specifically identified as "Extraction Cancelled," providing clearer visibility into scan termination and ensuring a more precise audit trail for multi-level archive processing.

**8)** **Simplified Deep CDR Final Verdicts in API Responses**

Scan result API responses ([GET - Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget) and [GET - Fetch Analysis Result By Hash](/docs/mdcore/metadefender-core#hashget)) have been enhanced to include a top-level engine results object. This improvement introduces a `sanitization_result` field that provides a clear, simplified verdict of "Success," "Failed," or "Not Run," streamlining programmatic processing by eliminating the need to parse multiple internal fields across different file types.

**9) Layout Refinements and Minor Adjustments for the PDF Processing Result Report**

The PDF Processing Result Report has been improved with a more refined layout and formatting.

**10) Enhanced Threat Intelligence Verdict Visualization on Dashboard**

The dashboard has been enhanced to apply standardized color coding for Threat Intelligence engine verdicts, ensuring visual consistency with other analysis engines. "Allowed" verdicts now correctly display in green and "Blocked" verdicts in red within dashboard filtering and statistics.

**11) Improved Formatting for Adaptive Sandbox Verdicts in Executive Reports**

The Adaptive Sandbox verdict display in the Executive Report has been enhanced for better readability. Adaptive Sandbox results now utilize spaces instead of underscores and feature proper capitalization for each word.

**12) Enhanced Processing Result Label Styles**

The UI for processing result preference labels has been improved to align with the latest design standards, featuring updated font weights, background transparency, and refined border coloring. These enhancements ensure a consistent and modern visual experience across the management console.

**13)** **Support new filtering for multipart/form-data request**

Requests using the `multipart/form-data` content type can now be searched in the Processing History by filtering for **FormData** under the `Request Type`.

**14) Webhook optimization**

Significant improvements have been made to the webhook response mechanism, enhancing stability, reducing TCP usage, and improving overall response time.

**15) Multiple enhancements for generate support package**

- Lightweight mode: Optional lightweight support package reduces size and shortens generation time by collecting a smaller diagnostic set.
- Custom time range: Support package generation for MetaDefender Core supports a custom time range so collected logs and data match the period you select.

**16) Email notification enhancement**

- Out-of-date definitions (per engine): Administrators can control out-of-date definition notifications per engine instead of a single global setting.
- Scheduled reports: quarterly period - Adds Quarterly as an option for report time range and schedule time. The history report covers the full calendar quarter; the email is sent on the first day of the next quarter at the hour the user picks in the web console.

---

**Security Enhancements**

1. Enhanced log file security and validation: the log file configuration has been enhanced to include strict path and extension validation, preventing the use of unauthorized locations or system files. This improvement ensures system integrity by restricting log files to approved formats such as .log, .txt, .json, .csv, and .out.
2. Upgraded 3rd party libraries:

- NGINX v1.29.7
- OpenSSL v3.5.5
- PostgreSQL v14.22
- 7z v26.00
- Zlib v1.3.2
- Nghttp2 v1.68.1

**Bug Fixes**

- Fixed an issue where the system would potentially crash when a package or engine was removed while still being downloaded.
- Fixed an issue where initiating multiple license activation requests concurrently could potentially cause engine reloads to time out or fail.
- Resolved an issue where exported PDF results for Threat Intelligence engines would display incorrect or redundant options when the engine name was changed.
- Fixed an issue where validation icons failed to appear in error messages when the synchronization time was out of range.
- Fixed an issue where pickup folder is empty and cannot monitor after network issue/or folder not found.
- Fix an issue that prevented Proactive DLP engine from being deployed on Windows due to the long file path limitation.
- Fix an issue where 1 MB `multipart/form-data` requests failed when submitted to MetaDefender Core.
- Fix an issue where MetaDefender Core failed to parse `multipart/form-data` requests when the boundary parameter was enclosed in quotes.

## [Version v5.17.1](/docs/mdcore/release-notes/archived-release-notes#version-v5171)

Release Date: 26 January 2026

**Next-Gen Threat Intelligence Engine and MetaDefender Aether**

MetaDefender Core introduces a branch new technology called **MetaDefender Aether**, a next-generation technology that brings Adaptive Sandbox and Threat Intelligence together into one powerful, unified pipeline. With Aether, security teams can detect, analyze, and respond to advanced threats with unprecedented speed and precision. This upgrade streamlines your threat detection workflow, reduces complexity, and delivers deeper insights, empowering you to stay ahead of even the most sophisticated cyber threats.

For more details about the all-new Threat Intelligence engine, please refer to this documentation: [Threat Intelligence](/docs/mdcore/threat-intelligence-engine/overview).

For details on the Threat Intelligence response JSON format, as exposed in the new `threatintelligence_info` field, see: [GET - Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget)

---

**Workflow Option for Running Deep CDR Only on Certain Metascan Verdict**

Added the ability to configure Deep CDR in the workflow to trigger only for files that are reported as infected by any of the scanning engines in Metascan. Clean files will not be sent for Deep CDR, and the workflow will stop after the initial Metascan stage with the corresponding scan status.

Default behavior/value: Disabled.

When enabled, only infected files will be processed by Deep CDR, while clean files bypass the sanitization stage.

---

**Enhanced Regex Management for Proactive DLP**

MetaDefender Core made it easier for admins to manage and select regex patterns for Data Loss Prevention (DLP) workflows. With this update, you can now upload multiple TSV files containing regex definitions, view their contents in a slick pop-up modal, and pick exactly which regexes you want to enable from the Workflow console.

Please note the following as of now:

1. The “Pick regexes” pop-up model is not yet supported in My OPSWAT Central Management. Instead, you can provide the path to the TSV file in the MetaDefender Core workflow configuration on the My OPSWAT Central Management console. By default, all regexes in the TSV file are selected, and you can edit the TSV to remove existing regexes or add new ones.
2. The DLP engine currently supports only the pop-up model for Detection configuration, but this may be expanded with additional options in the future.

Here is a sample TSV format:

---

**New Threshold to Strengthen Protection Against Archive Bomb**

MetaDefender Core introduced a new archive configuration that lets you control the maximum allowed compression expansion factor for extracted archives. This helps prevent “zip bomb” attacks, where a tiny archive expands into a massive file and can overwhelm your system.

By default, the system uses a high threshold (1000:1), so existing customers won’t be affected unless they choose to tighten the setting. If an archive exceeds the configured value, it’s now blocked with a new verdict: **Exceeded Archive Expansion Factor**.

---

**Support to Configure RFC 5424 and RFC 3164 for Syslog**

The application now allows selecting the syslog message format used for CEF output to integrate with different SIEM systems without breaking existing deployments. Supported formats include: Default, CEF, RFC 3164, and RFC 5424.

---

**Support Content-type: multipart/form-data for POST /file API**

Before version 5.17.1, MetaDefender Core only supported `Content-Type: application/octet-stream` where clients must submit whole content of one file in HTTP payload.

Now with version 5.17.1, asynchronous scan of the product supports a new content type, `Content-Type: multipart/form-data`. Utilizing this new content type, clients may submit multiple files in one request payload. The product will treat and process each part of the form-data as an individual file scan and associated with the same batch-like scan.

This scan type is not supported for requests that include the following headers: batch, filepath, sanitizedurl, or downloadfrom.

**Notes:** Before upgrading to v5.17.1 or later,

1. Verify whether your client applications are using a relevant Content-Type header and its corresponding payload for [Analyze File (Asynchronous mode) - POST /file](/docs/mdcore/metadefender-core#fileanalysispost).

- `application/octet-stream`: The payload must contain exactly one file's content.
- `multipart/form-data`: The payload may contain multiple files' content and must strictly adhere to the standard format (including `Content-Disposition`, `Content-Type`, and the raw data). Non-compliant payload will result in an HTTP 400 error and the message: "Invalid multipart/form-data payload received".

2. Verify that client-side parsing logic for the endpoint [Analyze File (Asynchronous mode) - POST /file](/docs/mdcore/metadefender-core#fileanalysispost) aligns with the submitted `Content-Type` header:

- `Content-Type: application/octet-stream`: The API returns a `data_id`.
- `Content-Type: multipart/form-data`: The API returns a `batch_id`.

3. Any improper implementations sending non-standard payload or expecting a `data_id` while using multipart/form-data headers must be refactored.

Users can also view this new kind of request in Processing History, having tag "FormData".

---

**Support Multiple Login URLs for SSO Directories**

MetaDefender Core now supports **multiple** login/redirect URLs as part of the SSO authentication flow. This enhancement allows deployments spanning multiple domains or client applications to dynamically route users to the correct redirect endpoint during login.

---

**IPv6 Support for MD Core - My OPSWAT Central Management Integration**

MetaDefender Core can now communicate seamlessly with My OPSWAT Central Management in IPv6 environments. This ensures that organizations transitioning to IPv6 can confidently deploy and operate My OPSWAT Central Management in modern network domains.

---

**Further Enhancements**

**1) Data Retention Term Change for "Off" Option**

Changed the Data Retention "Off" option label to a clearer term to avoid confusion. The previous "Off" label under the "Data retention" section was misleading; it now displays as "Retain: Forever" to better indicate the actual behavior.

**2) Add Synchronous File Scan Timeout to Config Export and Import**

The synchronous file scan timeout setting (`/admin/config/file/sync`) is now included in the configuration export and import package.

By default, the `file_sync_timeout_setting` is included in the exported package.

**3) UI Streamlining: Option Relocated for Better Usability**

To make configuration more intuitive, the “Include sanitized version of blocked child files” option has been moved from the Deep CDR tab to the Compression tab. This update helps users find and manage this setting where it makes the most sense, without changing any underlying functionality.

**4) Rename OPSWAT Alin Engine**

OPSWAT Alin engine is now renamed to OPSWAT Predictive Alin AI.

**5) Enhance Archive Extraction Issues Filtering Performance**

In MetaDefender Core v5.17.0, you can filter Extraction Issues in the Processing History. However, the performance of this filtering needed improvement, and it has been optimized in MetaDefender Core v5.17.1.

**6) Improved Error Categorization for Archive Extraction Issues**

MetaDefender Core made it easier to understand and troubleshoot archive extraction errors.

Previously, when an archive exceeded certain extraction limits (like file count, size, or depth), the error was shown as “Unknown.” Now, these are clearly categorized as either Extraction Limit Exceeded or Extraction Timeout Exceeded.

**7) Update Adaptive Sandbox Displayed Verdicts on Web Console**

Starting from MetaDefender Core version 5.17.1, verdicts from the Adaptive Sandbox will be changed in the product web console and other related reports. Note that only the UI and reports are updated; the JSON response remains unchanged to ensure compatibility with existing integrations. The detailed changes are as follows:

| **Previously displayed verdict** | **Newly displayed verdict** |
| --- | --- |
| Benign | Trusted |
| No Threat / No Threat Detected | No Threat Detected |
| Unknown | Undetermined |
| Suspicious / Suspicious Verdict by Adaptive Sandbox | Low Risk / Low Risk Verdict by Adaptive Sandbox |
| Likely Malicious / Likely Malicious Verdict by Adaptive Sandbox | High Risk / High Risk Verdict by Adaptive Sandbox |
| Malicious / Malicious Verdict by Adaptive Sandbox | Confirmed Threat / Confirmed Threat Verdict by Adaptive Sandbox |

---

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- NGINX v1.29.4
- c-ares v1.27.0

**Bug Fixes**

- Addressed the crash issue that could occur when clients push files during MetaDefender Core service startup.
- Addressed an issue where API requests failed due to RAMDISK Temp Directory setup and using the `downloadfrom` header - causing incorrect disk space comparison.
- Other cosmetic fixes.

## [Version v5.17.0](/docs/mdcore/release-notes/archived-release-notes#version-v5170)

Release Date: 16 December 2025

**Brand New Technology:** **OPSWAT Predictive Alin AI**

MetaDefender Core introduces a brand new technology called **OPSWAT Predictive Alin AI** that works alongside Metascan to improve threat detection depth and accuracy.

The new technology analyzes file structures, entropy patterns and semantic relationships using a domain-trained machine learning model to identify potentially harmful files earlier and with greater precision.

---

**Revamped Processing Result Interface**

As you can see above, our processing result interface has been redesigned to deliver clearer, more actionable insights, making it easier for administrators and support teams to interpret scan outcomes and take appropriate action.

We have also made it easier for users to know original file type and Deep CDR's converted destination type directly on the processing result screen.

---

**Unified User Interface and Experience of Login and Guest Scan Screens**

Login and Guest Scan screens have been unified across MetaDefender platform, bringing the similar feeling for customers of the platform.

---

**Certificate Management Enhancements**

Certificate management now allows administrators to upload certificates directly by content, simplifying secure configuration and compliance. You can now add or update certificates by directly uploading certificate content.

---

**Support Package Enhancements**

Support packages now include additional log types and process IDs, enabling users to select specific logs and set a maximum log size prior to generating.

---

**Email Notification Enhancement**

Email notifications have been improved to support batch aggregation and clearer messaging. This improves reporting efficiency for large-scale processing.

---

**Support for Split Archive Files**

MetaDefender Core now supports comprehensive scanning Split Archive file type.

The product accepts individual requests with split-archive parts sent via a new set of API endpoints, reassemble them, then extract and process nested files. Integration instruction at [Split archive upload guideline](/docs/mdcore/integration/splitarchive-uploading-guidelinek4l).

---

**Further Enhancements**

**1)** A new synchronization interval setting for My OPSWAT Central Management integration provides greater control over data sync timing.

**2)** When you create a new workflow rule with Deep CDR enabled, all file types will be activated by default. Note: HTML and TXT, which are reserved for email-specific use cases, will stay unselected.

**3)** The product now supports teamed NIC (Network Interface Card) configurations, preserving Deployment ID and maintaining stable license activation when network adapters are changed or switched within the team.

**4)** The response of [POST - Login](/docs/mdcore/metadefender-core#userlogin) now will return the header X-Core-Id if custom header is configured. It will help the customers identify which instance behind load balancer users login to.

**5)** Introduce new metrics regarding disk IO percentage in [GET /stat/nodes](/docs/mdcore/metadefender-core#nodesstatus) API, providing better visibility into node performance and potential bottlenecks. Adding `disk_stat_info` :

- Disk utilization (%): Min-Max value from 0 to 100
- Read speed (Mb/s): Min 0, Max depend on disk
- Write speed (Mb/s): Min 0, Max depend on disk

**6)** Filtering and exporting processing history is now enhanced with file size and extraction issue filters, allowing users to quickly locate large or small files processed by the system and troubleshoot archive processing events.

**7)** Roll out a major enhancement for HotSwap-type MetaDefender Core deployments. Now, both local and My OPSWAT Central Management environments handle backup licenses with accurate engine lists, clear status reporting, and smooth configuration management.

---

**Security Enhancements**

**1)** Upgraded libraries for vulnerability fixes:

- Qt v6.8.1
- PostgreSQL v14.20

**2)** Implements rate limiting on database connection test and save endpoints to mitigate brute-force and abuse risks.

**3)** Add more length validations for text components in Workflow/Global Configuration to strengthen security and consistency.

**4)** Update the PDF export process to ensure hyperlinks are rendered as plain text, preventing accidental clicks.

**5)** Tightening up security for exporting Sandbox JSON and SBOM reports. Previously, it was possible to export these reports without providing a valid and authorized API key. Now, the system strictly validates user permissions and denies unauthorized access.

**6)** Enhance the validation on SSL certificates for HTTPS connections by rejecting mismatched cert & key, incorrect format, encrypted private key (if no passphrase provided).

---

**Bug Fixes**

- Fixed an issue where value of others_time may be negative when processing encrypted document files.
- Applied consistent name validation rules when updating workflows.
- Resolved issues with resetting global configuration for Adaptive Sandbox.
- Corrected a permissions issue where users without full module rights could modify engine configurations.
- Fixed an issue where AV engines would reappear in scan results after Metascan SDK deletion.
- Fixed an issue where AV engines of Metascan SDK could not be fully deleted and cause orphaned subprocesses after removing its database.
- Fixed an issue preventing configuration changes or AV removal when both Metascan SDK and traditional AVs were installed.
- Fixed an issue where files were retained if a download was aborted.
- Improved the accuracy of warning messages when users input invalid API keys.
- Fixed an issue where files in quarantine could not be scanned by Adaptive Sandbox, caused by missing data in the quarantine process.
- Fixed an issue where the password reset email would truncate passwords containing the '<' character.
- Other cosmetic fixes.

## [Version v5.16.1](/docs/mdcore/release-notes/archived-release-notes#version-v5161)

Release Date: 30 October 2025

**Integration with BeyondTrust Password Safe for AD Directory**

MetaDefender Core now supports integration with BeyondTrust's Password Safe, enabling secure, automated AD password retrieval of rotated Active Directory (AD) service account passwords.

This integration allows organizations to eliminate static AD bind passwords, and it supports configuration, status monitoring, and seamless login with AD users whose credentials are managed by Password Safe.

More details at [Integrate Active Directory with BeyondTrust Password Safe](/docs/mdcore/configuration/integrate-active-directory-with-beyondtrust-s-password-safe).

---

**PDF Report Restructuring & Threat Indicator Integration**

Delivering a major upgrade to MetaDefender Core’s PDF reporting. The processing result PDF report has been completely restructured for clarity and consistency, featuring a new and improved layout. Threat Indicators and IOCs from Adaptive Sandbox analysis are now included directly in the report for deeper visibility into potential threats.

---

**Enhanced SBOM PDF Report for Better Security Insights**

The SBOM PDF report has been enhanced to display vulnerability severity statistics, highlight blocked licenses, and list problematic files and libraries at the top. These improvements help users quickly identify and address the security and compliance issues in their software bill of materials.

---

**Customizable Frequency for License Expiry Email Notifications**

Users can configure how often they receive email notifications about license expiration and related events, helping to reduce alert fatigue and avoid multiple reminders in a single day.

A new setting allows administrators to set the notification frequency from 1 to 48 hours, with a default of every 4 hours.

---

**Resetting User Passwords Without SMTP Configuration**

Admins can reset user passwords even when no SMTP or email server is configured, addressing a key need for secure environments where email infrastructure is restricted.

With a new option, MetaDefender Core allows administrators to generate a temporary password and securely share it with users through alternative channels. The feature clearly instructs admins on next steps, and the temporary password will expire in 3 days, requiring a change upon first login.

---

**My OPSWAT Central Management Integration: Certificate Management**

MetaDefender Core is able to automatically synchronize certificates with My OPSWAT Central Management (MOCM), supporting both Standalone and Shared DB modes, and prevents accidental deletion or modification of synchronized certificates.

Certificates on MOCM

Admins can view the origin of each certificate, and both locally added and MOCM-synced certificates are fully supported in workflows and secure connection settings.

---

**Further Enhancements**

**1)** “InSights Threat Intelligence” has been renamed to “Threat Intelligence” across the MetaDefender Core platform. This name change applies to the following screens Workflow, Health Check, Modules, Processing Result, Export result, and Executive Report.

**2)** Display Total Extracted File Size for Archives: Begin to track and display the total extracted file size for archives, giving users a clear view of how much data is unpacked during file analysis.

**3)** YARA Processing Time is Visible in Executive Reports: The Executive Report and PDF export now display YARA processing time, providing transparency into how long YARA scans take during file analysis.

**4)** Real-Time Scan Queue Updates via readyz API: The readyz API provides real-time updates on the scan queue data, improving visibility for high-throughput environments like MetaDefender ICAP Server. Previously, queue size information was refreshed every 5 seconds, which might be inaccurate under heavy load.

**5)** Parallel deployment of scanner packages to Metascan SDK has been improved, helping reduce deployment times.

**6)** Support proxy server entries with or without the `http://` or `https://` prefix. Admins can enter proxy addresses as plain hostnames, IP addresses, or with either HTTP or HTTPS schemes, and all formats will be accepted and handled correctly by the backend.

**7)** Support displaying multiple items from an object list in a single row under Workflow Rule, ensuring that up to three fields can be neatly aligned on one line. Prepared for future enhancements of engines.

**8)** Scan processing continues even if the client-identity JSON cannot be parsed, addressing rare but disruptive edge cases. Instead of halting the scan and returning an error, the system logs a warning and proceeds. The log level is also downgraded from ERROR to WARNING, making it clear that the issue is non-critical.

[WARNING] Failed to parse client-identity's JSON, dataId='aa4ceafda8e242fca99eea4971472251',
..., jsonError.errorString()='...' [msgid: 7451]

**9)** Improved Error Visibility for CLI Extraction: displays extraction errors for files processed with the CLI Extraction feature. Previously, these error messages were hidden or hard to find, but now they are classified and surfaced as "General Unextractable Errors" when appropriate.

---

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- Protobuf v32.1
- OpenSSL v3.5.4

Permissions have been tightened so only users with the appropriate right can access and view the data of "Config History".

Adjusted [Webhook worker count](/docs/mdcore/metadefender-core#configupdatewebhook) boundary:

- Setting the webhook worker count to a very high value would prevent MetaDefender Core from starting, causing it to hang.
- The worker count is now limited to a maximum of 100, and any higher values from previous versions are automatically adjusted during upgrade to ensure stable operation.

---

**Logging Enhancements**

Milliseconds are now included in CEF log timestamps, with a setting to maintain backward compatibility.

Sep 04 15:56:56.123 SE Asia Standard Time ... CEF:0|OPSWAT|MSCW|5.16.1|core.config|Request change logger configs|3|OMSrequest=... OMSmsgid=6274

**Bug Fixes**

- Fixed an issue where error messages weren’t shown correctly after a password reset if users entered the wrong password on the login page.
- Fixed an issue that allowed users to save configuration changes in Deep CDR file type handling modal even when required fields were left empty.
- Fixed an issue where users couldn’t save workflow configuration changes after removing a row in Deep CDR file type handling section.
- Fixed an issue where HTML in workflow names could be injected into certificate expiration notification emails, affecting how the email was displayed.
- Fixed an issue where MetaDefender Core would crash when changing the database password on Windows and restarting itself, resulting in a crash dump and missing logs END.
- Fixed an issue where the blocked-leaves APIs did not consistently include YARA rule information in their JSON responses when a file was blocked due to a matched YARA rule.
- Fixed an issue where users could not navigate to the last page in processing history when filtering by "Object" request type, due to a database query error.
- Fixed an issue where audit log data retention was not working properly, causing old audit log entries to be removed much more slowly than expected.
- Fixed an issue where upgrading MetaDefender Core on Ubuntu 24 could cause the service to lose connection with Postgres due to a specific system warning.
- Fixed an issue where audit logs and syslog entries only displayed user ID instead of username when a local user was deleted.

## [Version v5.16.0](/docs/mdcore/release-notes/archived-release-notes#version-v5160)

Release Date: 30 September 2025

**Support for CIS Level 2**

MetaDefender Core now aligns with CIS Level 2 benchmarks for Windows Server 2022. This enhancement supports organizations that require stricter security controls.

---

**Access History Screen, tracking Session Activities**

A dedicated interface under the History menu displays a comprehensive log of user session activities, including:

- Sign-in and sign-out events with timestamps and IP addresses.
- Session timeout occurrences.
- Password change events.
- Role and permission modifications, with details of the initiating user.

Administrators can filter logs by date range, action type, IP or user to streamline investigations and reporting.

---

**New Exportable SBOM Report**

This version introduces a new PDF report specifically for Software Bill of Materials (SBOM) processing results. This dedicated report provides detailed library information including:

- Library metadata and versions
- Associated CVE (Common Vulnerabilities and Exposures) information
- License information and compliance details
- Component dependency relationships

This new report type enables users to receive complete SBOM analysis results in a shareable PDF format, addressing enterprise workflows where detailed library information should be distributed and verified for security assessment, vulnerability remediation, and compliance review.

---

**Full Report of Remote Adaptive Sandbox in HTML and PDF Formats**

Previously, users had to retrieve the full report from Adaptive Sandbox interface. Now, the life is easier when users can directly download complete reports in PDF or HTML from MetaDefender Core web console with a single click.

---

**SSL Certificate Expiration Notification**

Administrators can now configure alerts for SSL certificates that are approaching expiration. The notification window is customizable. This helps prevent service disruptions and ensures secure communication remains uninterrupted.

These options can be found under Email Notification tab in Settings.

---

**Better Experience for Deep CDR File Type Selection**

A new search textbox enables users to quickly locate specific file types, such as JPG, by typing keywords and Enter. Info section and option to select all `All File Types` are also arranged.

---

**Multi-Password Input Interface**

Users can now specify a list of passwords during file upload processes on Web Console, allowing the system to iteratively attempt decryption against each provided password.

---

**Blocklist All Except Child File Type, Extending Capability to more File Type Groups**

The option `Allow child files` under `Blocklist All Except` feature allows users to define predefined child file types for further processing while instantly blocklisting others.

This update now, besides Archive Files, is covering more file type groups: Disk Image Files, Email Files, Encrypted Archive Files, Executable Files, and Office Documents.

For example, with the following settings, XML and RELS child files of DOCX file will be processed, meanwhile, other file types else will be blocklisted.

---

**Logging Enhancements**

**1)** When available disk space is low (< 10%), there will be a log message filed in core.log.

[WARNING]... Disk is running out of space, drive=..., total_space_gb=..., used_space_gb=..., folders=... [msgid: 7693]

**2)** Additional fields in msgid 82 for same-level extracted files and total extracted files.

- files_extracted_count: number of extracted files in the DIRECT level.
- total_extracted_files: total number of extracted files in ALL level.

[INFO]... files_extracted_count='...', total_extracted_files='...', totalProcessingTime='...' [msgid: 82]

---

**REST API Enhancements**

**1)** APIs [GET - Fetch a list of blocked leaf files inside archive](/docs/mdcore/metadefender-core#retrieveblockedleaffile) and [Fetch a list of blocked leaf files inside archive by hash](/docs/mdcore/metadefender-core#retrieveblockedleaffilebyhash) include

Hash-related fields:

- `md5`
- `sha1`
- `sha256`
- `sha512`
- `is_skip_hash`

And YARA rule fields: `yara_info`

2. Begin tracking Proactive DLP wait time: `dlp_wait_time` . This new field is included in [Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget) and other result fetching APIs.

---

**Further Enhancements**

**1)** Improved workflow configuration handling to prevent save errors and validation issues while scanning engines are being updated.

**2)** Quarantine feature now hides or grays out the option `Check with` when the respective module is inactive or unlicensed.

**3)** Quarantine feature offers options for searching for Technology results like SBOM, Adaptive Sandbox and sorting by Date Added.

**4)** Administrators may enable SSL connection for bundle PostgreSQL. More details at [How to setup SSL connection for PG](/docs/mdcore/installation/bundle-postgresql-ssl-connection).

**5)** Session cookie sent or not sent with cross-site requests is configurable on web console under Security tab in Settings.

**6)** Ability to export results of all single files (non-archive) files within an archive file as JSON.

---

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- Libxml2 v2.14.6
- OpenSSL v3.5.2
- ng2-file-upload, ngx-bootstrap, ngx-infinite-scroll

YARA rules using HTTP are now subject to the following restrictions:

- Archive size limit: Maximum of 50 MB.
- File count limit: Maximum of 1,000 files.
- Folder depth limit: Maximum of 50 nested levels.
- Path length limit: Maximum of 255 characters, excluding the engine database folder path length.
- Extracted size limit: Maximum of 50 MB total after extraction.

**Bug Fixes**

- Addressed an issue that negated `data` type in the option `Allow child files` of Block All Except in Blocklist.
- Addressed a rare crash issue in the product that occurred after enrolled with MOCM.
- Addressed an issue that did not set correct customized IP and port to Desktop shortcut.
- Addressed an issue that caused a failure to Email Server authentication mode `None`.
- Addressed a UI issue that displayed an incorrect number of supported file types of Adaptive Sandbox in workflow configuration.
- Addressed an issue that incorrectly prohibited certain accepted special characters (e.g., underscores and hyphens) in usernames within the Email Server configuration settings.

## [Version v5.15.2](/docs/mdcore/release-notes/archived-release-notes#version-v5152)

Release Date: 28 August 2025

**OAuth for Email Server Authentication for Microsoft 365**

In March 2026, Microsoft will be retiring Basic authentication with SMTP AUTH, and the change will complete after April. That means applications will no longer be able to use this authentication method to send emails.

This change prompts us to prioritize implementing OAuth support for Email Server as soon as possible. If you are using Basic Auth, we encourage you to review this document [Microsoft 365 OAuth](/docs/mdcore/configuration/email-configuration#microsoft-365-oauth) and change your MetaDefender Core's configurations to OAuth.

---

**Enhanced Extraction Issue Visibility for Nested Archives**

Earlier, users might have struggled to determine the cause of extraction errors in nested archive files. This update introduces a additional interface that highlights any extraction issues, making it easier for users to identify problematic nested files quickly.

---

**Configuration Import & Export Supports Certificates**

The ability to export certificates with database mode simplifies the process of backing up certificates. Administrators no longer need to manually configure Certificates settings.

The export/import feature will export/import certificate data by default. Its compatibility checks, automatic routing based on database mode and automatic deletion of existing certificates before import ensure integration of certificates without conflicts and prevent duplication. When an import fails, the product restores the previous state.

---

**Rejected Scan Request Logging**

Scan requests that are rejected such as those surpassing file size limits or occuring when local scanning mode is turned off, are not stored and displayed in the Processing History. A new optional setting now enables users to store these requests for later review and analysis.

**Note:** This feature only supports Standalone mode.

More details at [Track Rejected Requests](/docs/mdcore/configuration/system-configuration#track-rejected-requests).

---

**Non-TLS Communication for Local User Management Configuration in My OPSWAT Central Management**

Added support for non-TLS communication with My OPSWAT Central Management (MOCM) for Local User Management configuration in specific on-premises deployments. This feature allows MOCM and MetaDefender Core to operate without TLS when both are deployed within the same isolated network.

- **Use Case**: This enhancement is designed for scenarios where MOCM and MetaDefender Core are running in a secure, isolated network environment, and TLS is deemed unnecessary.
- **Recommendation**: While non-TLS communication is now supported, TLS is strongly recommended to ensure secure communication. Non-TLS should only be used in environments where security risks are minimal and well-understood.

---

**Improved Stability for Group Configuration in My OPSWAT Central Management**

In collaboration with My OPSWAT Central Management, MetaDefender Core begins to use dedicated endpoints and storage for configuration data and status, minimizing scenarios where a Core instance in a group fails to apply the group configuration. This should make life easier for system administrators managing large or complex groups.

---

**REST API Enhancements**

**1)** A dedicated API endpoint to fetch and monitor system's resources including Disk space usage, CPU and RAM utilizations. Document at [GET - Get server system resource](/docs/mdcore/metadefender-core#getserverstats).

**2)** The feature Scan-from-Link can now skip its metadata check and proceed directly to file downloading when clients set the new header `skip-head-request` of [POST - Analyze File (Asynchronous mode)](/docs/mdcore/metadefender-core#fileanalysispost) to false.

---

**Further Enhancements**

**1)** Human-readable display for package URLs in engine processing results.

**2)** Filetype engine has been offering enhanced features and detection rates, which requires slightly more resources and processing time. Tracking the wait time at the Filetype engine will provide useful observability insights.

**3)** Setting private username for PostgreSQL can now have "-" (dash) character.

**4)** Slightly improved performance for scanning large archive files.

**5)** Retired the page Data Reporting from registration wizard screens since this feature was deprecated for years.

**6)** Enforced rate limiting on PIN entry attempts.

---

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- PostgreSQL v14.19
- NGINX v1.28.0
- 7zip v25.01

---

**Bug Fixes**

- Addressed an issue that poped up `No modification detected` message while assigning new workflow template to existing workflow rules.
- Addressed an issue that intermittently caused `Not Scanned` to file scannings with an error `Can't convert to engine message`. This issue was observed to occur only when two actions, posting a file and performing a local scan for a file with the same hash, are executed.
- Addressed an edge case issue where the product failed to retrieve the workflow configuration for the Filetype engine, resulting in an error `Missing preferences.filetype_mismatch`.
- Addressed an issue that prevented editing of the Country of Origin's advanced settings while the engine was disabled or inactive.
- Addressed an issue where a negative value for `others_time` could occur after Compression sanitization execution.
- Addressed a comestic issue where Metascan tile was temporarily grayed out while Country of Origin was processing files.

## [Version v5.15.1](/docs/mdcore/release-notes/archived-release-notes#version-v5151)

Release Date: 30 July 2025

**New Operating System Support: Ubuntu 24.04**

This release introduces support for Ubuntu 24.04 across most engines. The majority of engines are now compatible and operational on this new operating system. MetaDefender Core now also supports CIS Level 2 system hardening benchmarks on this OS. For more details, refer to [CIS Level 2 - Linux Guidelines](/docs/mdcore/installation/cis-level-2-guidelines).

Few engines still require additional time for full compatibility with Ubuntu 24.04:

- Adaptive Sandbox
- File-based Vulnerability Assessment
- Reputation
- YARA

Further updates will be provided in future releases.

---

**New Operating System Support: Windows Server 2025**

This release of MetaDefender Core also introduces official support for Windows Server 2025, expanding platform compatibility for our suite.

Few engines still require additional time for full compatibility with Windows Server 2025:

- Adaptive Sandbox
- File-based Vulnerability Assessment
- Reputation
- YARA

Further updates will be provided in future releases.

---

**Support Advanced Log Configurations on Web Console**

Starting with MetaDefender Core version 5.15.1, the following advanced log configurations including local time zone, Common Event Format, product logs and syslog settings are supported.

Most settings, except for the product file path, do not require a service restart to take effect.

The product now offers three means of log configurations:

- Through MetaDefender Core web console ([Advanced Log Configurations](/docs/mdcore/configuration/advanced-log-configuration)).
- Using REST API endpoints ([PUT - Update log configuration](/docs/mdcore/metadefender-core#putlogfileconfig)).
- Enrolling and managing with My OPSWAT Central Management.

---

**Processing History Export as CSV Supports More Filters**

Added support for additional filters in the CSV export functionality for processing history. Users can now apply the following filters for CSV export:

- Result
- User
- Status
- Request Type (Batch, File, Object)

---

**REST API Enhancements**

Introduced a new field, `post_processing.sanitization_details.status`, to the response JSON when retrieving processing results. This field indicates the status of the sanitization process with the following possible values:

- `Queued`: The file is currently waiting in the MetaDefender Core's queue before being sent to the Deep CDR engine.
- `Processing`: The file has been sent to the Deep CDR engine and is currently being processed.
- `Finished`: The Deep CDR process has completed, with additional states available for further inspection.

Impacted REST API endpoints:

- [GET /file/{data ID}](/docs/mdcore/metadefender-core#fileanalysisget)
- [POST /file/sync](/docs/mdcore/metadefender-core#fileanalysissyncpost)
- [GET /hash/{hash value}](/docs/mdcore/metadefender-core#hashget)
- [GET /file/archive/{data ID}](/docs/mdcore/metadefender-core#fileanalysisgetallchildfiles)

---

**Further Enhancements**

**1)** **Optimized PostgreSQL Query Performance**: Enhanced the PostgreSQL query to improve performance when handling a large number of batches, resulting in faster data retrieval and processing.

**2) Enhanced Connection Persistence to My OPSWAT Central Management**: Improved handling of connection persistence for MetaDefender Core to My OPSWAT Central Management (MOCM) in specific edge cases, enhancing user experience by avoiding the need for re-enrollment. Key scenarios addressed include:

- When the machine loses internet connectivity to MOCM and the service is subsequently restarted.
- When the system's root certificates are corrupted or invalid and are later updated or restored.

**3)** A tool for Admin to remove an existing PIN code or set a new one. More details at [PIN Code Reset Tool](/docs/mdcore/troubleshooting/pin-code-reset-tool).

**4)** Audit Log covers activities related to API [PUT - Update list of custom response headers](/docs/mdcore/metadefender-core#configputcustomresponseheader).

**5)** Extended the option "Fallback file type detection to current extension" to Adaptive Sandbox.

**6)** No longer processing zero-byte files with Adaptive Sandbox.

**7)** Enhanced engineprocess's thread pool mechanism to achieve immediate response post-termination and improved thread reusability. This increases the total number of tasks handled over time. Nevertheless, at the cost of performance boost, it could increase the load on the service if clients frequently request scan results.

---

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- Libxml2 v2.14.5
- 7z v25.0
- OpenLDAP v2.6.10
- Redis++ v1.3.14

**Bug Fixes**

- Resolved an issue that caused slowdowns in warehouse updates for the Executive Report and high CPU consumption when the service received a large volume of requests in a short period.
- Resolved an issue that caused Executive Report data to freeze following a sudden shutdown of the service.
- Resolved an issue that caused unnecessary retry attempts when Adaptive Sandbox returned a SKIPPED result.
- Resolved an issue where slots in the queue for Batch processing were not released and temporary files were not cleaned up when the client connection was closed, resulting in improper transmission of error responses.
- Resolved a potential issue that could cause the service to crash due to incompatibility between a library with Qt6.

## [Version v5.15.0](/docs/mdcore/release-notes/archived-release-notes#version-v5150)

Release Date: 03 July 2025

**Supports CIS Level 2 for Ubuntu 22.04**

MetaDefender Core now supports CIS Level 2 system hardening benchmarks on Ubuntu 22.04. This enables organizations to meet more rigorous compliance requirements in regulated or high-assurance environments.

For more details, refer to [CIS Level 2 - Linux Guidelines](/docs/mdcore/installation/cis-level-2-guidelines). Support for additional systems is planned for future releases.

---

**Export & Import Engine Advanced Settings**

A new feature has been added to support exporting and importing engine advanced settings. This enhancement allows administrators to:

- Export all engine settings, even for modules that are currently deactivated.
- Import these settings into a new installation, ensuring that module activation states and configurations are preserved.
- Restore previous settings for engines if they are re-enabled after import.
- Control the feature via the API header `engine_config`: [GET - Export configuration](/docs/mdcore/metadefender-core#adminexportv2).

This feature improves configuration management and migration scenarios, especially for customers who need to maintain consistent engine settings across deployments.

---

**User Management via My OPSWAT Central Management API Endpoints**

MetaDefender Core now supports local user management through the REST APIs of My OPSWAT Central Management when integrated with that platform. This allows administrators to automate user account provisioning and role assignments across distributed environments, enabling better alignment with centralized identity practices.

This support is available starting from **MetaDefender Core version 5.15.0** and **My OPSWAT Central Management** **version v10.1.2507.**

For more information, please refer to the official My OPSWAT Central Management documentation.

---

**Additional File Size Limit Enforcement**

Administrators can now define a file size limit at the NGINX layer. This enables earlier enforcement of policy controls and supports more distributed or containerized environments.

This is configurable at the key `body_size` in ignition file. More details at [Ignition file fields](/docs/mdcore/installation/deployment-automation-support#ignition-file-fields).

---

**Post-Action Triggers Scoped to Root Archive Files**

To improve processing efficiency, post-action triggers, such as copying or quarantining files, now apply to root archive files. This refinement avoids unnecessary processing of nested archive layers and aligns more closely with typical workflow logic.

You can find the new option `Only trigger post action on root archive file` under tag Post Action in Workflow Rule.

---

**System Specification Warning at License Activation**

The product now displays a warning if the system does not meet the minimum recommended hardware specifications.

This post-activation check helps administrators verify whether their environment is properly sized. While continuing with an under-spec setup is allowed, doing so may lead to performance issues or instability under certain workloads.

---

**Setting Up A Secure Connection During Installation**

Administrators can configure HTTPS during the initial deployment process using ignition file, rather than post-installation on web console or via API call. This simplifies secure setup and reduces deployment time.

A new set of settings are introduced at [HTTPS section in Ignition file](/docs/mdcore/installation/deployment-automation-support#ignition-file-fields).

---

**Executive Report with Blocked Reasons Summary**

Administrators can obtain number of objects blocked by several reasons.

---

**Improved Local Folder Update Functionality**

Using the Local Folder Update folder with a UNC path previously consumed significant network bandwidth.

An optimization for new update check in this version considerably reduces network bandwidth and hardware resource usage.

---

**Allow OPSWAT Module Update Packages**

MetaDefender Core always performs integrity checks and verification to ensure the packages remain untampered. Therefore, Administrators can allow trusted OPSWAT update packages to pass through policy filters, ensuring essential updates are applied reliably without triggering unnecessary scan and consuming additional resources for deep processing.

New options have been introduced in the Allowlist workflow configuration to automatically allow the OPSWAT engine and database packages.

---

**Usability Enhancements & Changes**

**1)** Automatic Cleanup for File Corruption: The product now includes automatic cleanup functionality to address file corruption and residual files caused by external issues, such as connection loss, during the process of adding files to sanitizing storage. This enhancement ensures improved cleanliness of the storage environment.

**2)** Improved the look and feel of multiple text boxes within lists in Workflow Rule.

**3)** When Local Folder Update is selected and in use, the button `Update all` , which manually triggers update of engine and database packages, becomes unnecessary and is therefore grayed out.

**4)** A new sub-option, **Exception by file types** , has been added under the `Output filename format` section in the Deep CDR tab of Workflow Rules. This feature allows users to control and customize the naming convention of sanitized files, particularly enabling the retention of original file extensions when required.

**REST API Enhancements**

**1)** Attach MetaDefender Core server information in the response header X-Core-Id of the following API endpoints:

- `POST` `/file/batch` - [Initiate Batch](/docs/mdcore/metadefender-core#batchcreate)
- `GET` `/hash` - [Fetch Analysis Result By Hash](/docs/mdcore/metadefender-core#hashget)

**2)** Supporting customizable parameters with new header `info` in the REST API [GET /readyz](/docs/mdcore/metadefender-core#healthcheck) allows users to query specific system metrics, such as CPU load thresholds, relevant to their use case. Available values:

- all: return all the information
- database: obtain database status
- license: obtain license status
- avg_duration_time: obtain average duration (processing) time
- cpu_load: obtain CPU load as of calling the API
- scan_queue: obtain scan queue stats
- number_active_av_engines: obtain the number of active AV engines threshold
- engines: obtain engine status

**3)** Introduce a new API endpoint to fetch a list of blocked leaf files inside the archive by Hash: [GET /hash/{hash value}/blocked-leaves](/docs/mdcore/metadefender-core#retrieveblockedleaffilebyhash).

**4)** Introduce a dedicated API endpoint to validate PIN code: [POST /admin/pincode/validate](/docs/mdcore/metadefender-core#validatepincode).

**5)** Provide a new API endpoint to trigger `Local Folder Update` even during business hours or pause update window: [POST /admin/update/folder](/docs/mdcore/metadefender-core#postforce-update-folder-trigger).

---

**Logging Improvements**

- Improved audit logs to include all activities on administrative configurations.
- To easily investigate network error while using SSO, we added more detailed log messages for authentication module.

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- PostgreSQL v14.18
- Angular v19
- yaml-cpp v0.8.0

**Bug Fixes**

- Fixed a crash issue that potentially happens during proxy setup. Network management is unavailable when the proxy configuration is applied, leading to a crash of MetaDefender Core. This scenario occurs with an extremely low likelihood.
- Fixed an issue where the setting `Processing results to be classified as Allowed` was not applied correctly, causing erroneous blocking of results.

## [Version v5.14.2](/docs/mdcore/release-notes/archived-release-notes#version-v5142)

Release Date: 28 May 2025

**Integration with MetaDefender Distributed Cluster v2.0**

Enables integration with a new product, MetaDefender Distributed Cluster v2.0, giving organizations exclusive benefits:

- High availability: Distributed architecture ensures continuous inspection, even during instance-level outages or maintenance.
- Fault tolerance: Isolate failures and support automatic recovery, preserving uptime and service continuity.
- Load distribution across MetaDefender Core instances: Share file scanning tasks across multiple instances, eliminating performance bottlenecks.
- Parallel archive file handling: Extract and distribute archive contents across Core instances, reducing scan time for large files and enabling resumption of interrupted processing.
- Elastic scalability: Easy to add more instances as file volumes grow, scaling capacity seamlessly to meet organizational demand.
- Centralized orchestration: Manage all MetaDefender Core instances and API Gateways from a single Control Center web console. Provide a zero-downtime upgrade mechanism with just a few simple operations.

More details about this new product at [MetaDefender Distributed Cluster Overview](https://www.opswat.com/docs/mddistributedcluster/installation/mddc-overview).

**New Operating System Support: Amazon Linux 2023**

This release introduces support for Amazon Linux 2023 across most engines. The majority of engines are now compatible and operational on this new operating system.

Few engines still require additional time for full compatibility with Amazon Linux 2023:

- NANOAV
- File-based Vulnerability Assessment
- RAR compression of Archive Compression

Further updates will be provided in future releases.

**Client Identity Tracking**

This release introduces support for sending client identity information with file scan requests into MetaDefender Core via a new header `client-identity`, enhancing visibility into the scan request lifecycle.

This optional header captures details provided by the clients a scan request passes through (e.g., MetaDefender KIOSK → MetaDefender MFT → MetaDefender Core), including:

- Client name
- Client host
- Username
- Client's deployment ID
- Received timestamp at client
- Client product version

All the following methods support this header: asynchronous mode, synchronous mode, local scan, scan from link, batch scan, multi-part uploading.

More details at:

- [GET - Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget)
- [GET - Fetch Analysis Result By Hash](/docs/mdcore/metadefender-core#hashget)
- [GET - Status of Batch Analysis](/docs/mdcore/metadefender-core#batchstatus)
- [POST - Analyze File (Asynchronous mode)](/docs/mdcore/metadefender-core#fileanalysispost)
- [POST - Analyze File (Synchronous mode)](/docs/mdcore/metadefender-core#fileanalysissyncpost)
- [POST - Initiate Batch](/docs/mdcore/metadefender-core#batchcreate)
- [POST - Create multipart uploading session](/docs/mdcore/metadefender-core#createmultipartuploadpost)

The client identity details are accessible through:

- **MetaDefender Core web console**: View detailed scan request information directly in the user interface.
- **JSON Processing Result**: Client identity data is included in the processing result output.
- **My OPSWAT Central Management (MOCM)**: MetaDefender Core forwards client identity information as part of the scan report to MOCM for centralized management and reporting.

**Archive Password Support for Multi-part Uploading**

Starting with version 5.14.2, MetaDefender Core introduces support for archive password handling in multipart upload APIs, enhancing functionality for processing password-protected archives.

The passwords are transmitted via header `archivepwd` and are secured through at-rest encryption.

More details at [POST - Create multipart uploading session](/docs/mdcore/metadefender-core#createmultipartuploadpost).

**SBOM Package Filter for Archive Files and Batch**

A new SBOM filter functionality has been added to the Scan Results page. This feature enables users to efficiently filter and view results for nested files in archives and batch-processed files containing SBOM package information.

**Usability Enhancements & Changes**

- Setting "Block files if the process fails or times out" under Deep CDR workflow now flags a result as Blocked even when sanitized version of a file cannot be added to storage successfully.
- Ensure log rotation has unique filename and no remaining file.

**Technology Integration Enhancements**

- Enable engines to display hyperlink within its result details.
- Future versions of Archive Extraction engine will move away from the ID format `7z_` and provide a new format `extraction_` . Since this version of MetaDefender Core, the new format is supported along with the old one.

**Security Enhancements**

- Upgraded libraries for vulnerability fixes:

  - NGINX v1.26.3
  - Libxml2 v2.13.8
- Improved API endpoints' validation.
- Replaced deprecated functions of 3rd libraries.

**Bug Fixes**

- Fixed an issue that prevented access to web console after OS reboot. This issue happened with standalone mode and a remote PostgreSQL. When the issue happened, an error "Can't create connection" was found in log.
- Fixed an issue that stopped email sending after the machine lost internet connection.
- Fixed an issue that blocked modification of webhook configuration after enrolled into My OPSWAT Central Management.
- Fixed an issue that failed enrollment via ignition file.
- Fixed an issue that omitted blocked reason "Extraction Failed" when a temporary extracted file was absent.
- Fixed an issue that incorrectly disabled Country of Origin engine after importing a configuration with "Allowlist by vendor" setting enabled.

## [Version v5.14.1](/docs/mdcore/release-notes/archived-release-notes#version-v5141)

Release Date: 28 April 2025

**New OS support: Oracle Linux 9.5**

This release of MetaDefender Core introduces official support for Oracle Linux 9.5, expanding platform compatibility for our suite.

**New endpoint for API Key Management**

To offer automated user management, MetaDefender Core provides a new REST API that Administrators can call to set or change a permanent apikey for local-type users.

API document at [Update user's API key](/docs/mdcore/metadefender-core#changeuserapikey).

**Securing syslog communication over TLS**

This version introduces support for securing syslog communication over Transport Layer Security (TLS), enhancing the confidentiality and integrity of log data transmitted across networks.

New protocol `tcps` is supported. Documentation at [Logging](/docs/mdcore/configuration/logging), and API can be found at [Apply syslog server configurations](/docs/mdcore/metadefender-core#postsyslogconfig).

**Post Action and External Scanner**

Introduce a command restriction for Post Action and External Scanner features enabling server Administrators to specify a list of permitted commands that these features can only use.

More details at [Hardening feature for Post Action and External Scanner](/docs/mdcore/configuration/hardening-for-external-scanners-and-post-actions).

**Post Action with permitted-only commands.**

**An ability to adjust maximum slots** **of queue capacity** **for archive processing**

Previously, archive processing was fixed at 25% of the maximum queue size. Now, Administrators can configure this value within a range of 25% to 75%, providing better flexibility to optimize resource allocation for archive processing to improve efficiency in high-throughput environments.

You can find the setting `Queue ratio for archive` at Settings/General.

**Embedded Adaptive Sandbox engine with Daily Scan Quota**

When the daily scan quota is reached, Sandbox engine will reject scan requests and display a warning message `Declined due to license limit reached` .

Users can decide to block files due to out-of-quota by ticking a new option `Block files if the execution limit reached` . It can be found in Workflow/Adaptive Sandbox.

**Continuous Integration with** **My OPSWAT Central Management**

To close the experience gap, the product now supports more features in Inventory/Modules of MetaDefender Core on My OPSWAT Central Management like engine activation, update lock & unlock.

**Usability Enhancements & Changes**

- Get prepared for a new engine ID of Archive Extraction engine.
- Changes in extracted object aggregation, `total_extracted_files` now excludes nested folder/directory.
- Handle an edge case where a missing test sample results in engine initialization failure.
- Improved the detection and redaction of support package generator tool. It coincidentally mistook engine versions for sensitive data.
- Provide new options for having Blocklisted and Allowlisted reasons in PDF result export.
- Introduce a new display option to switch between 12-hour and 24-hour clock format. This applies to either web console or exported PDF/CSV file. You can find the setting "Date & Time format" at Settings/General.
- No longer showing a misleading label `True Type` in result details of File Type engine when the result is "Not Available".
- "Processing results to be classified as Allowed" setting now included “Suspicious Verdict by Sandbox” by default.

**Technology Integration Enhancements**

- An ability to continue further processing based on results concluded by InSights Threat Intelligence engine.
- Adjust timeout value for the following engines (File Type Verification, YARA, SBOM, Reputation, COO, InSights Threat Intelligence) to reflect correct remaining time. Only applicable when global timeout is enabled.
- Create permanent storage folder for internal jobs of Adaptive Sandbox engine.

**Security Enhancements**

- Restricted modifications to information of an Administrator account to exclusively be performed by accounts with Administrator privileges.
- Implemented secure random number generator.
- Improved endpoints' validation.

**Bug Fixes:**

- Fixed an issue that stopped periodic email notifications for out-of-disk-space and database maintainance events from being sent.
- Fixed an Email Notification issue that kept checking license expiration despite of that the setting was disabled.
- Fixed a display issue that blocked users to view workflow or user directory on touch screen.
- Fixed an Import issue that temporarily (~3mins) caused lack-of-permission issue for a user who previously had imported configuration to the product.
- Fixed a Data Retention issue that mistakenly cleaned up sanitized files and DLP-processed files. This issue only occured when feature "Skip hash calculation" is enabled.
- Fixed an issue that sent too frequently an event log "Synchronized configuration" to My OPSWAT Central Management (MOCM).
- Fixed a crash issue happening during unenrollment the product on Linux from MOCM.
- Fixed an issue that stopped syncing engine advanced settings to MOCM when an engine is being updated.
- Fixed issues that failed engine advanced setting synchronization after editing multiple engines' settings on MOCM.
- Fixed an issue that failed to apply engine advanced settings after several configurations have been edited on MOCM previously.
- Fixed an issue that failed to sync YARA source settings from the product to MOCM after performing import configuration.
- Fixed an issue that interrupted the group policy inheritance of MOCM and failed to apply those settings on the product.
- Fixed a display issue that showed up an empty screen of Inventory/Modules on MOCM after upgrading to v5.14.0.
- Fixed a display issue that sometimes showed up an empty screen of Workflow on MOCM after enrollment.

## [Version v5.14.0](/docs/mdcore/release-notes/archived-release-notes#version-v5140)

Release Date: 31 March 2025

**New features:**

- Advanced SSL Settings Support: Configure and manage advanced SSL settings directly through the web console for a seamless user experience and flexibility.
- Passphrase Support for Encrypted Private Keys in Certificates: An ability to add encrypted private keys to Certificates with the option to include a passphrase, providing an additional layer of security for sensitive data.
- Email Notification Feature Enhancements

  - Customizable Email Subjects: Tailor email notification subjects to suit your preferences or organizational needs.
  - Outdated-Definition Engine Alerts: Receive email notifications when engine definition becomes outdated, ensuring timely updates.
  - Disk Space Warnings: Get notified via email when your system is running low on disk space, helping you avoid disruptions.
  - Database Maintenance Reminders: Stay on top of database maintenance with periodic reminders displayed on the web console and sent via email.
- Quarantine Feature Enhancements

  - Stronger Encryption Algorithm: The Quarantine feature now supports a more robust encryption algorithm, ensuring greater protection for quarantined items. This protection is off by default to avoid affecting existing integration performance.
  - Configurable Quarantine Conditions: Define file size limit for files that should not be quarantined, giving you control over resource allocation and quarantine behavior. You can find this setting under Workflow Rule.
- Integration with My OPSWAT Central Management

  - Introduce first integration with My OPSWAT Central Management v10. Most of available features on v8 are migrated and retained on the v10 integration.
  - In addition, Administrator can manage and control Modules and advanced module settings seamlessly through My OPSWAT Central Management, streamlining administration and oversight from a single interface.
- Usability Enhancements & Changes

  - Support login with format `<domain>\<username>` for AD/LDAP user accounts.
  - An ability to export offline activation license for backup and restore. The exported license is safely stored in password-protected ZIP file.
  - Introduce a new child setting under 'Block files that exceed the file size threshold' to exclude good verdicts from specific technologies, preventing those files from being blocked due to exceeding the file size threshold.
  - Support nomination for hot-backup instance with OLMS activation.
  - Add more accurate load factors such as CPU load and Avg. duration time in the health check API. For more details, refer to [Get health check status](/docs/mdcore/metadefender-core#healthcheck).
  - New API for AD-bound password rotation automation. For more details, refer to [Change Password for AD/LDAP User Directory](/docs/mdcore/metadefender-core#userdirectorychangepass).
  - Reason details for blocklisted and allowlisted results.
  - An ability to search for users of user groups in Processing History.
  - New audit logs for JSON and PDF result export from Processing History.
- Technology Integration Enhancements

  - Provide YARA results to Sandbox engine for further analyzing.
  - Provide MIME type for sanitized and DLP-redacted files.
  - Support workflow settings for Archive Extraction and Archive Compression engines.
- Security Enhancements

  - Upgrade libraries for vulnerability fixes:

    - OpenSSL v3.4.1
    - quazip v1.4.0
    - libxml2 v2.12.10
  - Remove unnecessary .NET 6 from Windows Azure image.
  - Make Password Recovery feature more robust: Users now only receive an expirable token in password-reset email and use that token to set a new password. For more details, refer to [Forgot Password](/docs/mdcore/configuration/password-recovery#forgot-password).
  - Enhance error response to not return raw messages and HTML source code.
- UI updates

  - Display password strength meter.
  - Save "X items per page" as user preference.
  - Rebrand "My OPSWAT" to "My OPSWAT Central Management".
  - Display tooltip for items in workflow dropdown list.
  - Minor cosmetic UI changes.

**Fixes:**

- Addressed an issue that caused update failure to a version of FileType engine which supports result preference.
- Resolved a limitation that made compression failed while handling more than 300K file entries.
- Addressed an issue that caused JSON config import failure with message `an unexpected property: "dlp.filescan.certainty_threshold": "Low"` .
- Addressed an issue that displayed "mismatch db_api" while upgrading from a quite old Proactive DLP.
- Addressed an issue that omitted blocked reasons when a file is blocked by COO engine due to "Unsupported file type".
- Addressed an issue that caused Proactive DLP to return "Unsupported File Type" when processing .docx, .xlsx, .txt files in a random manner.
- Addressed an issue that caused a crash when stopping engine process during big archive file scanning.
- Addressed an issue that caused HTTP 500 Internal Server Error when filtering Processing History with null parameters.
- Addressed an issue that caused product upgrade failure when upgrading from v5.11.1 to 5.12.x or 5.13.x with activated SSO. The error message is "Failed to init AES cipher".
- Addressed an issue that caused high CPU consumption on PostgreSQL process after product upgrade.
- Addressed an issue that caused a considerable delay in fetching results of a large batch scan.
- Addressed an issue that caused an incorrect proxy settings retrieval.
- Addressed an issue that caused Deep CDR unable to sanitize file after upgrading from product v4 to the latest.

## [Version v5.13.3](/docs/mdcore/release-notes/archived-release-notes#version-v5133)

Release Date: 27 February 2025

**New features:**

- Enhanced Data Retention mechanism to perform effectively and reduce execution time.
- Upgrade PostgreSQL to v14.17 for vulnerability fix.
- Upgrade Angular to v18.
- Minor cosmetic UI changes.

**Fixes:**

- Addressed an issue that used up Linux file descriptor when using synchronous scan method.
- Enhanced query to avoid max stack depth error while cleaning up numerous depth levels of archive files.
- Improved NGINX logging to indicate initialization failure clearer.
- Resolved an issue that caused upgrade process suspended.

## [Version v5.13.2](/docs/mdcore/release-notes/archived-release-notes#version-v5132)

Release Date: 21 January 2025

**New features:**

- Triggering condition for Post Action: To focus needed requests and save up resources, it is necessary to introduce a triggering condition for Post Action where Administrators can select and filter what verdicts to trigger the actions only.

**Fixes:**

- Addressed an issue that caused license activation failure in K8S when using MetaDefender Core with HTTPS enabled.
- Addressed an issue that caused automated license activation failure after Azure image instance was restarted.
- Addressed a crash issue that happened when checking invalid sanitized file existence.

## [Version v5.13.1](/docs/mdcore/release-notes/archived-release-notes#version-v5131)

Release Date: 16 January 2025

**New features:**

- New technology: MetaDefender InSights Threat Intelligence

  - This technology can detect known malicious IP addresses and domains inside document files.
  - To enable the technology, you need to contact OPSWAT to update your license. Then you can just go to Workflow Rule, turn the switch on and explore its capability.
- New OS support: Debian 12

  - Since v5.13.1, we also replace base image Debian 11 with Debian 12 minimal base image.
- Prohibited from downloading produced files when original file is flagged as Blocked

  - Introduced a setting to add an extra layer of security that makes files produced by Deep CDR or Proactive DLP unavailable for download when original file's result is flagged as Blocked for any reasons. This setting is off by default and can be found under tab General in workflow rule.
- Deep CDR analysis mode

  - When analysis mode is turned on in workflow rule, Deep CDR no longer sanitize file, remove object and generate a new file. Instead, the technology will report objects inside the file for analysis purpose. Under this mode, you can see a tag flagging the mode on, number of detected objects and a neutral green message.
- Usability enhancements / changes

  - Precisely calculate "hash time" of nested files to have more relevant "Child files hashing" time.
  - In Linux non-persistent mode and local scan method, webhook callback is enhanced to ensure responses eventually to be sent even if there is permission issue or else with scanned local files.
  - Users now can download list of IoCs detected by Adaptive Sandbox from the web console.
  - New option to block files whose size is larger than file size threshold of Adaptive Sandbox.
  - Users now can granularly customize time period in Data Retention settings.
  - Enabled verdict searching in Advanced filter of Processing History.
  - Moderate UI changes to display hash values in full text as well as make other metadata result shown more clearly.
- Security enhancements

  - Upgrade OpenSSL to v3.4.0 for vulnerability fix.
  - Upgrade protobuf to v3.21.12 for vulnerability fixes.
- Modify Docker setup for Rocky Linux to ensure proper dependency checking for Proactive DLP.
- Minor cosmetic UI changes.

**Fixes:**

- Addressed an issue that caused service crash when validating non-existed ID of output files returned by Deep CDR and Proactive DLP.
- Addressed an issue that might cause memory leak when using scan-from-link feature.
- Addressed an issue that caused service unresponsive due to slow data retention process.
- Addressed an issue that made upgrade process and service hang in container while running with remote PostgreSQL v14 Windows.
- Addressed an issue that was "Fallback file type detection to current extension if needed" setting did not apply to Proactive DLP.
- Addressed an issue that caused misleading Proactive DLP result while processing archive file. It displayed "No Specific Configuration" meanwhile it should have been "Unsupported File Type".
- Addressed an issue that misvalidated setting file during Import process and made workflow rules inaccessible.
- Addressed an issue that caused SSL handshake error when downloading file with scan-from-link feature.
- Addressed an issue that caused product in Rocky container did not automatically activate license after HTTPS enabled.
- Addressed an issue that caused misleading Metascan result in PDF result of a batch. It displayed "No Threat Detected" whilst it should have been "Not Scanned".
- UI bug fixes:

  - On Average File Size chart, title sometimes was not truncated correctly.
  - Fixed an issue that caused UI infinite reload on Change Password screen.
  - Fixed an issue that caused Accessibility mode not be switched with Tab and Enter keys.
  - Fixed an issue that wrongly displayed "No Specific Configuration" at Deep CDR tile despite of the fact that result is "Sanitization Failed".
  - Other minor bugs.

## [Version v5.13.0](/docs/mdcore/release-notes/archived-release-notes#version-v5130)

Release Date: 18 December 2024

**New features:**

- New OS support: Rocky Linux 9

  - We also provide a new Docker image based on official Rocky Linux repository. You can try it here: MetaDefender Core [Rocky Linux image](https://hub.docker.com/r/opswat/metadefendercore-rocky) and [Rocky Linux for non-root image](https://hub.docker.com/r/opswat/metadefendercore-rocky-nonroot).
- OPSWAT has discontinued support for CentOS 7 and RHEL 7 since December 2024 in MetaDefender Core and its associated engines. If you need some more time to transition from legacy OS, refer to this instruction [Lock Your Engine and Plan for Migration](/docs/mdcore/knowledge-base/end-of-life-support-for-centos-7-and-RedHat-7-in-metadefender-co#continuing-with-centos-7redhat-7---pinning-your-engine--not-recommended).
- Report scheduling

  - MetaDefender Core provides a new feature that enables Administrators to schedule not only when executive report and processing history report are sent but also set recurring schedules for automated delivery.
  - This feature goes with abilities to specify email recipients, apply filters to tailor the data and define precise time range.
- Administrators now can directly generate and download support packages right on web console.
- Advanced rate limiting configuration via web console

  - For more details, refer to [Request rate limit configuration](/docs/mdcore/configuration/request-rate-limit) and [Request rate limit test scenarios](/docs/mdcore/integration/request-rate-limiting).
- Syslog configuration via REST API

  - [Apply new syslog server configurations](/docs/mdcore/metadefender-core#postsyslogconfig)
  - [Remove syslog servers or clear all syslog configurations](/docs/mdcore/metadefender-core#removesyslogconfig)
- Ability to download summarized user list
- New chart and statistics to display how many percentages/files are reused by hash.
- Tool to hide specific data from support package.

  - Provides an ability to hide sensitive data from logs, support package, which may contain information such as IPv4, IPv6, MAC address and file path.
  - For instruction, refer to [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-) and try the new parameter `-enable-redact` .
- Introduces an ability for Administrators to download a summary list of users and groups present on the product. You can find the Export button in User Management which generates a CSV file listing all the users and groups' information.
- Supports CIS Level 1 for Ubuntu 22.04 and RHEL 9. For more details, refer to [CIS Level 1 - Linux Guidelines](/docs/mdcore/installation/cis-level-1-guidelines).
- PostgreSQL v16 support (remotely).

  - The product does not perform any version upgrade on customer's remote PostgreSQL.
  - Note: The bundled PostgreSQL version is v14.15 in this release.
- For files scanned with Adaptive Sandbox, result display now provides more details as well as adding informative records in "Quarantine" feature.
- Usability enhancements / changes

  - An ability to add description for users in the product.
  - Optimized UI rendering to improve display speed especially when rendering an immensely long list of file types in Blocklist.
  - Only display Unmanaged when My OPSWAT returns HTTP 404 and error "Instance not found".
  - Display correct involved disks and its purposes of use in System Health.
  - Display current number of finished files inside batch report.
  - Enhanced certificate loading to ensure Webhook communication over TLS.
  - Support "smaller than" operator for Blocklist and Allowlist by filename.
  - Reused scan results in Processing History now are tagged with a specified label to help users identify easily.
  - New changes in workflow setting "Exceptional verdicts": add "Cancelled" by default, and remove "Scan failed".
  - Unchecked "Detect file type mismatch" setting of "MetaDefender Software Supply Chain" workflow rule.
  - Enhanced retry mechanism to reconnect OLMS when receiving unregistered state.
  - Added new option to display 200 items per page in Processing History.
  - No longer trigger "Reuse processing result by hash" for files when all its type IDs are different.
  - Improved performance for exporting or importing an enormous list of hashes.
  - Retained deployment ID regardless of network interface card change, when the product is deployed on the same machine.
  - Sum up and display hash time of all directly nested child files.
  - Tracking first/last files received in batch and its timestamps.
- Enhancement for webhook use case including request receiving, webhook status storing and fetching, optimizing thread allocation.
- Security improvements

  - Upgraded bundle PostgreSQL to v14.15 for vulnerability fixes.
  - Upgraded NGINX to v1.26.2 for vulnerability fixes.
  - Upgraded 7z to v24.09 for vulnerability fixes.
  - Upgraded Npgsql to v4.0.17 for vulnerability fixes.
  - Applied patch to Qt for vulnerability fix.
  - Hardened OS command validation for External Scanner setup.
  - Improved login mechanism for SAML Single-SignOn.
  - Hardened regex validation.
- Engine integration

  - Support tab switching and breadcrumb in detailed result UI.
  - Populate tombstone flag to Archive Compression engine to enhance PST file sanitization.
  - New setting for Country of Origin engine to immediately block all unsupported file types.
- Docker enhancements

  - Eliminated unused components/libraries from DockerFile.
  - Gathered containerization information into support package.
- More detailed log messages for LDAP integration especially when not found a LDAP user.
- Added audit logs for Email Notification, Banner and Scan-from-link settings.
- New engine icons for Country of Origin, Adaptive Sandbox, and Threat Intelligence.
- Improved the login behavior to ensure that users can login even right after a successful product upgrade.
- Display extraction error code and details.
- Compression tab in workflow will be disabled when Deep CDR and Proactive DLP are both disabled. In addition, corresponding sections under Compression tab will be disabled depending on which engine is disabled.
- And many cosmestic UI changes.

**Fixes:**

- Addressed an issue that ignored filtering settings, causing Adaptive Sandbox to analyze sanitized or partially sanitized files that should not have been analyzed.
- Addressed an issue that caused detail view in Configuration History UI unresponsive after failed to import configuration.
- Addressed an issue that caused error "Invalid certificate responded" when using ForgeRock, KeyCloak, PingOne, and resulted in that user could not login to web console.
- Addressed an issue that was inproperly respecting "Fallback file type detection to current extension" setting for Proactive DLP.
- Addressed an issue that caused selected config file lost after clicking Enter at Password For Decryption textbox.
- Addressed an issue that was failing to extract encrypted archive file while integrated with Central Hub.
- Resolved an issue related to "Email Configuration" when using None as "Auth method" caused the setting to become misconfigured.
- Resolved an issue that might cause local user session repeatedly expired after its password was reset.
- Resolved an intermitten issue that caused file extension of downloaded file wrong.

## [Version v5.12.1](/docs/mdcore/release-notes/archived-release-notes#version-v5121)

Release Date: 30 October 2024

**New features:**

- Support user login for nested AD groups

  - When enabling a new setting `Nested Group Login`, the product allows users who are indirect members of an AD group to log in and take on the corresponding roles and rights.
- MetaDefender Core now supports CIS Level 1 for RHEL 9. For more details, refer to [CIS Level 1 - Linux Guidelines](/docs/mdcore/installation/cis-level-1-guidelines).
- Result display enhancements.

  - Introduces filtration options for the display of processing results, enabling users to quickly filter which file types violate the blocklist policy.
- Skip-by-hash enhancements

  - Boosts hash lookup performance.
  - Refines new REST API parameters for better functionality and usability.
  - Users can now download a CSV template for easy content input, simplifying data entry processes.
- Processing History enhancements

  - Ability to export history based on status `Allowed` or `Blocked`.
  - New column: `File size`.
  - New filtration option: by `Duration`.
- Selective analysis of files containing specific Active Content(s) with Adaptive Sandbox engine

  - Giving users more flexibility to analyze their own files with Adaptive Sandbox.
  - With this setting, only files containing specific Active Content(s) will be analyzed by Adaptive Sandbox engine.
  - Please note that this setting is only available if using Adaptive Sandbox version 2.1.0.
- Total size is sanitized and processed by Deep CDR in Executive Report.
- Usability enhancements / changes

  - Support new operator '**smaller than**' for file size condition in `Blocklist`& `Allowlist.`
  - REST API [Fetch a list of blocked leaf files inside archive](/docs/mdcore/metadefender-core#retrieveblockedleaffile) now includes AV engine name and detected threat name.
  - Addressed a case where Firefox browser sometimes incorrectly detects CSV file type, causing CSV uploading to fail with message '`File format is invalid. Please upload a CSV file.`'
  - Added more options for Data Retention of sanitized files and the Proactive DLP engine processed files.
  - Based on the override classification in `Workflow Rule` making blocking decision for the SBOM engine results.
  - Begin including engine state in export and import progress.
  - Support AD domain controller.
  - Removed PLPython from bundled PostgreSQL in Linux.
  - Improved validation for file scanning.
  - No longer deploy and initialize unsupported engine types.
  - Distribute SHA256 and file size data to the SBOM engine for analysis.
  - Move '`File download`' timeout setting from `MetaScan` tab to `General` tab.
  - Group settings '`Enabled file hash for only selected types`' and '`Skip Hash Calculation`'.
- Central Hub enhancements

  - Support a REST API to download digitally signed status reports for the entire batch. The specification is the same as [Download Signed Batch Result](/docs/mdcore/metadefender-core#batchsignedresult).
  - Support a REST API to fetch the product version. The specification is the same as [Get Product Version](/docs/mdcore/metadefender-core#productversion).
- Additional logging for the Single Sign-On (SSO) feature.
- Updated the UI to reflect engine state in case of inactivity.
- Ensured color consistency for table titles across UI modes.
- Implemented minor user interface refinements.

**Fixes:**

- Fixed an issue that caused the filename of the sanitized file to be assigned a different text than the workflow rule setting '`Output filename format`', when the '`Reuse processing result`' feature was enabled.
- Fixed an issue that caused a JSON attribute to be set incorrectly for encrypted archive files.
- Addressed a bug that caused newly supported file types to not be automatically checked after Deep CDR was updated.
- Improved an inconvenience with `Allowlist`/`Blocklist` settings where users were unable to save changes, and instead received an error message '`No modification detected`'.
- Fixed an issue that caused the `Revert`button to disappear sometimes.
- Fixed a problem that led to incorrect sanitization results due to a miscalculation of the tombstone files quantity.
- Fixed an issue that displayed an empty first page of `Module Update` history when no search criteria were specified.
- Fixed a potential data race in sending webhook result by multiple workers.
- Fixed an issue that caused activation to not be cleaned up properly in a Docker container.
- Fixed an issue that generated wrong database name when running in standalone mode with the parameter `IGNITION_JSON` in Docker container.
- Fixed an issue with Non-persistent mode that prevented the service from starting in Docker container.

## [Version v5.12.0](/docs/mdcore/release-notes/archived-release-notes#version-v5120)

Release Date: 30 September 2024

**New features:**

- Email notification
- CSV upload for feature Skip-by-Hash
- Password storage for handling encrypted file
- By default, the workflow rule "MetaDefender Software Supply Chain" now includes SBOM license enforcement, enhancing compliance and security.
- Refines the user interface for Modules to enhance usability and streamline workflows.
- Now you can manage and configure "Post Actions", "External Scanners", "Webhook Authentication" and "Health Check" from My OPSWAT.
- Blocklist All Except treats child file types in separate ways
- Usability enhancements / changes:

  - Introduced a setting under Deep CDR in workflow rule to set Blocked to original file if sanitization is successful.
  - Optimized PostgreSQL query.
  - Desktop shortcut of the product now can redirect to HTTPS.
  - Users now can specify different workflow rules for files in a batch.
  - Introduced an option to include vulnerability information into manifest file.
  - An ability to export a specific date range from Processing History.
  - Applied a better flow for Sandbox timeout handling.
  - `outdated_data` now can reflect changes related to engine advanced settings.
  - Display "Cancelled" for affected AV engines when client cancels a request in the middle.
  - Rename Sandbox verdict "INFORMATIONAL" to "NO_THREAT".
  - Added smaller options to Data Retention settings.
  - Updated name of engines in Health Check settings.
  - An ability to change file size unit in Blocklist and Allowlist.
- Security improvements

  - Enhanced key generation and destruction flow.
  - Improved login mechanism for SAML Single-SignOn.
  - Upgraded libxml2 to v2.12.9 for vulnerability fix.
  - Upgraded protobuf to v3.19.5 for vulnerability fix.
- Docker enhancements

  - Upgrade PostgreSQL to v15.8 for vulnerability fix.
  - Upgraded libldap to v2.5, python to v3.12.6 for vulnerability fixes.
  - Upgraded the preinstalled JRE to v17 in our Docker Images to support new requirement of Adaptive Sandbox v2.0.0+.
- Central Hub supports new header `scan-options`
- Made some settings' description more informative.
- Implemented minor user interface refinements.

**Fixes:**

- Fixed an upgrade issue when upgrading from v4.20.0
- Fixed an issue in container environment that product could not deactivate when PostgreSQL instance stopped or terminated.
- Fixed an issue that support package could not collect log files in Windows Server.
- Resolved an issue making temp files sometimes could not be removed when an engine crashed.
- Fixed an issue making obsolete functions for storing Sandbox and SBOM report left after an upgrade.
- Corrected Maximum and Total processed object size in PDF Executive Report.

## [Version v5.11.1](/docs/mdcore/release-notes/archived-release-notes#version-v5111)

Release Date: 28 August 2024

**New features:**

- Support two standard formats for SBOM generation.

  - **SPDX** (Software Package Data Exchange): Developed by the Linux Foundation, SPDX is an open-source, machine-readable format designed to promote transparency and compliance in open-source and proprietary software management.
  - **CycloneDX** (CDX): Created by the OWASP community, CycloneDX is another open-source, machine-readable format that prioritizes ease of use and automation in SBOM generation throughout the software development lifecycle.
- New statistics in Executive Report

  - Introduces new settings to filter data by workflow, by user, by source in Executive Report.
  - There is an ability to switch statistics display on file or object.
- Introduces an updated system health dashboard that offers a new way to visualize scan queue and allocation.
- New scan-from-link settings

  - Introduces Max download queue setting which you can modify number of file downloads at a time for your use case and network. Also introduces pattern validation setting which users define blocklist and allowlist based on link pattern.

You can find these in Settings\Security tab. For more details: [Scan-from-link Settings](/docs/mdcore/configuration/scan-from-link-settings)

- Usability enhancements / changes

  - Supports proxy for On-Premises License Management Server (OLMS).
  - Provides improved visibility for SAML SSO user directory settings.
  - Supports Windows 11, version 23H2.
  - Changes the display name for decrypted documents.
  - Allows users to export and import queue size settings.
  - Enhances the support package generation script to enable users to collect a variety of log files from newest to oldest. For more information, see [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-)
  - Enables users to search for file types in Blocklist and Allowlist settings.
  - Exposes sanitized file sizes in the REST API, even when they are 0 bytes.
  - Allows users to switch between hours and days for setting the "Definition age threshold" under Workflow Rule \ Metascan.
  - Optimizes processing report synchronization for My OPSWAT.
  - Mode switching (from Standalone to Shared) during upgrade is no longer supported. Users are recommended to setup a Shared DB instance through a fresh installation instead.
- Adaptive Sandbox's supported archive file types

  - The Adaptive Sandbox engine now scans only supported archive file types that are selected by users in Workflow Rules.
  - This enhancement helps ensure that the Adaptive Sandbox engine focuses on processing relevant files, improving performance and overall system efficiency.
  - Nested files within supported archive file types will no longer be scanned by the Adaptive Sandbox engine.
- Security improvements

  - Implemented additional validations for administrative configurations and the scan-from-link feature.
  - Upgraded the bundled PostgreSQL database to version 14.13 for CVE-2024-7348.
  - Upgraded Qt to version 6.5.3.
  - Upgraded nghttp2 to version 1.61.0.
  - Upgraded curl to version 8.9.1 in the Docker image.
- Docker enhancements

  - Allows users to add license comments during activation.

    - Introduces a new optional parameter, MDCORE_LICENSE_COMMENT, type string.
  - Provides new settings for the On-Premises License Management Server (OLMS) proxy.

    - For more details: [Docker run parameters](/docs/mdcore/container-deployment/docker-image-published-on-opswat-docker-hub#parameter-init-details-environmental-variables--ignition-file)
- Logging improvements

  - Optimized logging for unlicensing events.
  - Added more logs for synchronous operations.
- UI updates

  - Changed the YARA engine name.
  - Froze the header in the engine detail table.
  - Implemented minor user interface refinements.

**Fixes:**

- Database connection failure

  - Resolved a database connection issue that occurred after users upgraded to version 5.11.0. This issue did not affect all cases when upgrading to version 5.11.0. If the application was previously upgraded from version 5.5.1 (or older) to version 5.6.0 (or newer), this issue would occur when users upgraded to version 5.11.0.
- Fixes on product stability issues

  - Addressed an issue where the ometascan process consumed excessive memory when serving scan-from-link requests.
  - Resolved an issue that prevented users from searching Processing History for AD users.
  - Fixed an issue that prevented header metadata from working with Hub.
- Implemented UI enhancements and resolved minor bugs.

## [Version v5.11.0](/docs/mdcore/release-notes/archived-release-notes#version-v5110)

Release Date: 31 July 2024

**New features:**

- Multipart uploading support

  - This feature enhances upload efficiency and reliability for large data transfer.
  - **Seamless handling of large files**: Clients can now upload files seamlessly by breaking them into smaller parts.
  - **Simultaneous part uploads**: Clients can upload multiple parts of a file simultaneously, further boosting speed and efficiency of the upload process.
  - **Resumable part uploads**: In case of network interruption or even after a restart of MetaDefender Core service, clients can now resume part uploading from where it left off.
  - Multipart uploading support can work with Standalone mode and Shared mode. For Shared mode, client needs to ensure that parts of a file must be sent to 1 MetaDefender Core instance.
  - This mechanism is only compatible with Asynchronous scan, Batch scan and Webhook functionality.
  - Users can enable this mechanism in Workflow Rule and set a time-to-live for received parts.
  - [Initiate multipart upload session: POST /file/multipart](/docs/mdcore/metadefender-core#createmultipartuploadpost)
  - [Upload individual part of file to the conducted session: POST /file/multipart/{dataID}](/docs/mdcore/metadefender-core#uploadpartpost)
  - [Check uploading status: GET /file/multipart/{dataID}](/docs/mdcore/metadefender-core#uploadpartget)
  - [Abort multipart uploading: DELETE /file/multipart/{dataID}](/docs/mdcore/metadefender-core#uploadpartdelete)
- Module Update settings and Data Retention settings are now managed in My OPSWAT product inventory.

  - After enrolled, these settings will be locked on MetaDefender Core management console, and users can only make changes on My OPSWAT console.
- My OPSWAT integration: PIN code required for configuration edit
- Central Hub offers the ability for client to cancel their scan requests submitted to MetaDefender Core instances behind it.

  - Single file and Archive file
  - Distributed archive file
  - Batch
- Queue size configuration

  - Size of the product queue (processing slots) now can be adjusted and defined on management console.
  - Note: setting this size too high could end up a potential risk of overloading MetaDefender Core and affecting the entire scanning service.
- New hash type: SHA-512

  - Introducing support for SHA-512 hash type for enhanced security.
  - You can toggle a new option in Workflow Rule to enable this new hash calculation.
- Definition age threshold rejection

  - This release introduces new settings for Metascan thresholds.
  - MetaDefender Core will reject file submission when there are too many outdated AV engines.
  - Error message in this case: "Failed to request scan. Insufficient number of up-to-date anti-malware engines"
  - You can find the settings in Workflow Rule > Metascan, and configure definition age (days) and number of outdated engines.
- Ability to display a custom notice during login process.
- Usability enhancements / changes

  - Non-persistent and Central Hub modes will not sync scan reports with My OPSWAT.
  - Optimize database partition creation for smoother performance.
  - Enhanced startup process to ensure service reliability, even with prolonged or failed temporary directory cleanup.
  - Added support for handling "General unextractable error" from Archive Extraction engine.
  - Expanded reuse of processing results by hash to include metadata header.
  - Corrected sanitization result for nested files in archives when reusing processing results by hash.
  - Improved backup method for database configuration files.
  - Accelerated Data Retention for Processing History.
  - Prevent engine initialization during paused update time when downloaded packages exist.
  - Added filter for batch scans in Processing History.
  - Introduced "Skipped assessment" verdict for File-based Vulnerability engine when "Skip hash calculation" is enabled in workflow rule.
  - Restructure workflow settings for Filetype engine.
- Performance improvements

  - Optimized ID generation process.
  - Enhanced report synchronization for improved performance impact when enrolled in My OPSWAT.
  - Improved dedicated slots allocation for efficient archive file scanning.
  - Standardized user and license validation for reduced costs and processing time.
- Security improvements

  - Implemented additional validations for administrative configurations.
  - Upgraded bundled PostgreSQL authentication method scram-sha-256 for enhanced security.
- PostgreSQL 15 support (remotely)

  - MetaDefender Core starts supporting remote PostgreSQL database v15, and now can work with PostgreSQL either v14 or v15.7
  - Product does not perform any version upgrade on customer's remote PostgreSQL.
  - Note: The bundled PostgreSQL version remains at v14.11 in this release.
- Prepared v15.7 PostgreSQL CLI tools.
- Logging improvements

  - Expanded logging for "Pause scheduled updates" feature.
  - Incorporated rootDataId into Hub log messages.
  - Implemented Workflow deletion tracking in logs.
  - Increased logging for the cleaning process during service startup.
  - Optimized log writing to reduce redundancy.
- Enhanced UI accessibility across multiple areas.

**Fixes:**

- Resolved an issue where temporary files were not cleaned up when the Archive Extraction crashed before MetaDefender Core could send a stop task.
- Fixes on product stability issues

  - Corrected discrepancy between actual and file submission counts on the Dashboard.
  - Resolved a service crash issue occurring during its restart after My OPSWAT enrollment.
  - Fixed missing "=== END ===" long marker on Debian when stopping the service.
  - Addressed inaccurate processed objects counts in Executive Report and Processing.
  - Correct pagination errors when adjusting the items per page.
  - Resolved reuse processing result by hash history incompatibility with URL encoding metadata headers.
  - Eliminated leftover files after import failures.
  - Resolved performance degradation in shared DB mode that occurred when more than 4 instances were running concurrently, particularly affecting handling of high traffic loads.
- Implemented UI enhancements and resolved minor bugs.

## [Version v5.10.1](/docs/mdcore/release-notes/archived-release-notes#version-v5101)

Release Date: 27 June 2024

**New features:**

- Upgrade data at-rest encryption algorithm

  - Improved security by upgrading the at-rest encryption algorithm to AES (Advanced Encryption Standard).
  - Sensitive data stored in the system will now be protected using AES encryption algorithm, enhancing the confidentiality and integrity.
- Add new OS support for Ubuntu 22.04
- New SBOM detection mechanism

  - SBOM technology introduces enhanced capabilities for analyzing and detecting license issues to gain deeper insights into the licensing status of the software components they use, ensuring compliance and minimizing legal risks.
- Usability enhancements / changes

  - Splitting the waiting time for the Adaptive Sandbox engine from the "Others" time to provides better visibility into the Adaptive Sandbox analysis process, enabling users to identify and address any scan time effectively.
  - Users can now perform a look-up of quarantined files using hash values.
  - Extended the support for the API download quarantine functionality by accepting input SHA256 hash values as uppercase.
  - Displaying a "No License" message when enrolling MD Core to My OPSAWT without license.
- Performance improvements

  - Enhanced a case that dedicated slots of scan queue might not be applied when scanning archive files.
  - Standardized user validation and license validation to reduce the cost and time.
- Able to set External Scanner as mandatory engine
- Introducing a new workflow rule for streamlining the integration with the product MetaDefender Software Supply Chain.
- Upgraded to OpenLDAP v2.5.17 for vulnerability fix.
- Docker environment: Able to upgrade the application with a database password containing specific characters
- Cloud K8S environment: Skip checking available disk space on database instance when lacking of super-user permission
- Reducing size of engineprocess logs.

**Fixes:**

- Improved feature Reuse Processing Result by Hash
- Addressed an issue where tasks were not being released properly when they timed out on engine side.
- Addressed an issue that in certain circumstances, when MD Core sent a stop task, but Archive engine had not finished opening the corresponding file, temporary files in the Archive Extraction temp folder were not cleaned up by the engine.
- Fixed an issue by ensuring that even if MD Core has realized a timeout and removed the stop extraction task, the response from Archive engine will still be processed correctly, and the associated temporary file will be removed accordingly.
- Resolved a corner case where task_id of next and stop tasks were duplicated, leading to the retention of the temporary file.
- In high-load situations, when Archive engine received a next task and proceeded to extract a file, but MD Core experienced a timeout while waiting for a response, later responses from Archive engine regarding successfully extracted files will still be processed and acknowledged to ensure proper cleanup of extracted files.
- Fixes on product stability issues

  - Addressed an issue where upgrading from older versions to version 5.7.1 or newer was not possible when using non-persistent mode in Linux environments.
  - Fixed an issue with the rotation of engine log files. It will now rotate correctly according to the configured rotation settings.
  - Resolved an issue where scan results were not updating correctly when canceling scans that involved External Scanners.
  - When using the Accessibility mode, there was a UI issue where only one AV engine appeared on the Modules screen, instead of displaying all available AV engines.
  - Fixed an issue where Webhook Authentication would fail after upgrading the system.
- Identified a memory leak issue where abandoned resources were not cleaned up when a request timed out in the queue.
- Fixes on My OPSWAT integration

  - Could not save configuration on My OPSWAT UI when session lifetime almost pasts.
  - Logs were flood with numerous "Config was changed on OCM" message when license is changed.
- Fixes on Non-Persistent mode

  - Failure to logging in with SSO.
  - Could not import configuration with v2 method.
  - Failed to add Webhook Certificate, External Scanner and Post Action.
  - Several redundant error logs appear when using this mode.
- Central Hub, unabled to create batch: Fixed an issue that client could not create batch to Central Hub

## [Version v5.10.0](/docs/mdcore/release-notes/archived-release-notes#version-v5100)

Release Date: 21 May 2024

**New features:**

- Continuous support for My OPSWAT and Central Management v8 integration

  - Workflow rules configurations.
  - Product license activation.
  - Engine module update.
  - Processing history browsing.
  - Processing details of each scan.
  - Dashboard overview with processing statistics.
- Sandbox engine technology name updates

  - "Sandbox" engine is now displayed as "Adaptive Sandbox".
  - New filtration setting to allow triggering Adaptive Sandbox engine to run when hitting "Blocked Verdict by Deep CDR" result determined by Deep CDR.
- The default workflow rule for “MetaDefender for Secure Storage” is now renamed to "MetaDefender Storage Security".
- Managing and sharing YARA rules has never been easier with new export and import functionality.
- Security improvements

  - Upgraded to Cyrus SASL 2.1.27 for vulnerabilities.
  - Upgraded to libpng 1.6.43 for vulnerabilities.
  - Upgraded to zlib 1.3.1 for vulnerabilities.
- Significantly improved the base64 decoding performance.
- Usability enhancements / changes

  - Allow setting Multiscanning AV related timeout settings less than 1 minute (in seconds), applicable to both "Per AV" and "Global timeout" settings. ***Note***: upgrade process will convert 0 (min) value to 1 min.
  - Make "others_time" more granular and precise in case of processing archives.
  - Retry mechanism with License Manager to handle any potential unstable network issue better.
  - Distinguish Multiscanning AV's "wait_time" and "scan_time" in case of scan timeout.
  - Separate Multiscanning AV's wait_time from "others_time".
  - No longer flag Reputation engine's database outdated.
  - Default non-admin roles now can be deleted completely.
- Performance improvements

  - Optimized algorithm to boost parallel performance when functionning with 20+ Multiscanning engines.
  - Resolved slow responsing and reducing memory usage for file submission.
  - Optimized communication channel between MetaDefender Core service and its engineprocesses for product resilience under load.
  - Improved a mechanism to ensure engine initialization can be executed even when Windows ever runs out of resources.
  - Applied thread-pool mechanism in task management to reduce resource consumption and improve file processing performance.
  - Optimized workflow logic to maximize the utilization of system resources.
- Containerization improvements

  - Supported non-root use case.
  - Supported to start shared-DB instances in a parallel way when using an internal (bundled) PostgreSQL user.
  - Supported YARA rule settings import.
- Logging improvements

  - Logs now can be rorated by day and size, at 1GB.
  - Data retention: keeping the last 30 days of log files.
  - Standardized key format in log file: "data_id".
  - Distinguished "Unexpected server response" from "Invalid deployment ID" error.
  - Ensure log message from Multiscanning engines should not mess up product log format.
  - Track timestamps of first chunk received and last chunk received in millisecond.
  - Track which AV engine takes most scan time (max_scan_time) and wait time (max_wait_time).
- Change the term "Waiting child files" to "Nested files".

**Fixes:**

- Addressed leftover temporary file issue in certain circumstances under high load.

  - When users cancel a request or terminate a connection in the middle, temp files of the cancelled/terminated requests could be left over.
  - When users cancel an archive file processing which is being extracted, it causes temp child files might be remaining while root file can be removed in advance.
  - When there are numerous archive timeouts, then required further commands cannot be sent to Archive Extraction engine for temporary file cleanup.
- Fixed issues caused by archive engine timeout and threshold exceeding that negatively impacted performance, and potentially caused memory leak issue.
- Fix issue that Multiscanning engines sometimes cannot active back after a timeout or failure termination.
- Status code and response body does not reflect Synchronous Scan timeout result.
- Fix issue that support package script overwrited new-location logs with the default-location logs.
- MetaDefender Core container cannot start when UID and GID are different.
- Fix issue that MetaDefender Core container could not auto deactivate.
- Multiscanning exclusion setting did not work properly when configured engine(s) are "Inactive".

## [Version v5.9.0](/docs/mdcore/release-notes/archived-release-notes#version-v590)

Release Date: 21 March 2024

**New features:**

- Reputation engine integration

  - The OPSWAT Reputation Engine enables instant threat identification by comparing hashes against a growing database cataloging known good and bad files.
  - The Reputation Engine utilizes hash reputation based on advanced analysis like metadata evaluation, content inspection, and contextual correlation to minimize false positives. This allows accurate threat detection with limited business disruption. Through database updates and hash contributions, the Reputation Engine enhances protection against new and evolving attacks.
  - In MetaDefender Core, customers need to opt-in to enable the Reputation Engine through the workflow management settings.
  - Learn more details at [Overview](/docs/mdcore/reputation-engine/reputation-engine)
  - ***Warning:*** *The Reputation engine will be automatically added into all existing and new customers' license to fulfill our security protection committed to our customers. That means the engine will be downloaded and deployed when applicable, but users must opt-in to enable the engine's processing under MetaDefender Core workflow rule.*
  - *Without taking any action to enable it, this engine deployment should not cause any impact to our customers integration and scanning service.* __
- Country of Origin (COO) engine integration

  - The OPSWAT Country of Origin (COO) engine enables instant detection of a file's geographic source. It analyzes digital fingerprints and metadata to identify restricted locations and vendors automatically. This allows precise filtering that blocks unauthorized data access based on origin while ensuring cross-region regulatory compliance.
  - The COO engine provides organizations with visibility into file upload origins. With precise data origin insights, organizations can streamline audits, protect sensitive data, and prevent malicious file uploads. This enhances security and compliance at reduced cost.
  - By combining advanced technologies like Deep Content Disarm and Reconstruction (Deep CDR), Multiscanning, and Proactive Data Loss Prevention with origin-based access controls, organizations can secure intellectual property, maintain compliance, and block illegal or non-compliant foreign data. This mitigates breach risks and avoids substantial fines per regulations like GDPR.
  - The COO engine supports signed file types like PE files, MSI, and Self-extract.
  - Learn more details at [Country of Origin](/docs/mdcore/country-of-origin/country-of-origin)
  - ***Warning:*** *For those customers who using older version of MetaDefender Core where we provided a feature for allowlisting files based on vendor, then those settings will be migrated to COO engine's settings under MetaDefender Core workflow rule on the latest version.*
  - *In that case (applicable to whom already using existing older version of MetaDefender Core's allowlisting file based on vendor), COO engine is not licensed by default for customers, so please reach out to OPSWAT to acquire license for COO engine and use that license* **before** **_ upgrading**_ __*your MetaDefender Core to ensure settings migration to be made properly.* __
  - *Once upgraded, exppecting that COO engine will be displayed on MetaDefender Core inventory page, but inactive. It requires users to disable COO engine and re-enable it back. All previous allowlisting file based on vendor's settings will be then found under "Country Of Origin" tab in the corresponding workflow rule.* __
- Windows Server 2012 discontinued support

  - Windows Server 2012 has been out of support by the vendor (Microsoft) since Oct 2023 - Reference: <https://learn.microsoft.com/en-us/lifecycle/announcements/windows-server-2012-r2-end-of-support>
  - MetaDefender Core version 5.9.0 will no longer support this OS version, and recommend our customers migrating their systems to newer supported Windows Server version.
  - List of current supported Windows OS versions can be found at [Supported Windows Operating Systems](/docs/mdcore/installation/recommended-system-configuration#windows-supported-operating-systems).
- API key protection

  - Strengthening MetaDefender Core's security by protecting users' API key (if created) in the database using SHA256 hashing. Then actual API key value could not be retrieved back for good.
  - By default, this feature is not enabled for backward compatibility. Administrators need to opt-in by enabling that. Expecting to see the following UI notification poped up upon signed in:
  - ***Warning:*** *Once enabled, administrators cannot turn back the feature for security enforcement. Before switching on this feature, it's strongly recommended to backup your users' API key in a secured vault / secrets manager.*
  - When this feature is enabled, API key will be hashed out in the database, and no one, including administrators, will be able to see actual API key value anywhere in the product.
  - In case API key is lost or not remembered, then administrators must re-create a new one. The new one will be displayed for only one time on the UI.
  - ***Note:*** __*Nothing should be changed from client side integration, client should keep using actual API key in plain text for REST API calls.* __
- PostgreSQL 14.11 supported

  - That also includes PosgreSQL 14.11 bundled with MetaDefender Core for local bundle database deployment. This upgrade addressed PostgreSQL own vulnerabilities in older versions, and helps protect our customers from supply chain attack.
- "Block all accept" under "Blocklist by file name"

  - Supporting a new option to allow users to block all except certain things against file name.
- Central Hub architecture updates

  - Distributed archive compression is supported.
  - Metadata header is supported for Proactive DLP while running in Central Hub
  - Country of Origin and Reputation engines are supported.
  - Secure API key is supported.
  - Including instance name in status response API.
  - Enhanced the organization of files in an archive result and a batch result by sorting based on statuses and verdicts.
  - Optimized batch processing in Central Hub.
  - Optimized request header processing in Central Hub.
  - Upgraded to OpenSSL 3.2.0 for vulnerabilities.
  - Upgraded to Hiredis 1.2.0 for vulnerabilities.
  - Upgraded to Nghttp2 1.58.0 for vulnerabilities.
  - Upgraded to rabbitmq-c 0.13.0 for performance.
- Security improvements

  - New option to disable user information caching via using designated administrative REST API endpoint (PUT /admin/config/cacheuser). Details at [MetaDefender Core API](/docs/mdcore/metadefender-core)
  - Upgraded to PostgreSQL 14.11 bundled with the product for vulnerabilities.
  - Upgraded to OpenSSL 3.2.0 bundled with the product for vulnerabilities.
  - Handled URL encoded characters.
  - Removed Lodash version in product JS file.
  - Addressed minor potential security related issues.
- Usability enhancements / changes

  - Updated default parallel count setting value (maximum number of threads) for Sandbox engine to 5 (formerly 20).
  - Enhanced engine deintialization mechanism to ensure all dependent engine process(es) cleaned up and stopped gradually.
  - Prioritized to list and display all blocked nested files inside batch first over allowed items.
  - Supported to process scan request with local file path contains double backslash characters.
  - Changed the Content-Type header value for POST /file and POST /admin/update/upload (old: application/json; charset=utf-8 - new: application/octet-stream)
  - When setting value for global/tempdirectory key for MetaDefender Core temporary folder, if that folder does not exist, now the product no longer automatically create temporary folder. Instead expecting users to have that folder created upfront and set permission (write) on that folder.
  - Prevented the product upgrade proceeding when insufficient disk space is detected. Faiure reason will be caught in the product log when encountered.
- Performance improvements

  - Optimized [PUT - Modify 'skip by hash' list](/docs/mdcore/metadefender-core#configupdateskiphash) to process a large volume of hashes data - up to hundreds of thousands of entries, which is not possible before the optimization.
- Logging improvements

  - Added more information into the product log in the event of scan submission was blocked due to out of workflow time window (included filepath, filename, callbackurl, sanitizeurl, downloadfrom)
  - Added data ID of root archive level to the log in the event of any child files of that root archive, regardless of any extraction level, is done with processing.
  - Optimized to trim down unnecessary data captured in the product audit log when users modified a configuration comes with large content e.g. large list of hashes to be skipped.
  - On Linux OS, supported log rotation for NGINX web server by MetaDefender Core built-in mechanism without relying on logrotate service on Linux OS.
  - Added deployment ID into the product log in some relevant licensing events.
  - Provided data retention setting for PostgreSQL bundled logs, by default: 1 month, and can be adjusted up to 12 months.
- UI updates

  - Display processing time details
  - Child (nested) checkboxes are no longer automatically checked/unchecked when their parent checkboxes are.

**Fixes:**

- Failed to process signed file via local file path mode (using filepath header).
- Failed to start MetaDefender Core service when using log overriden with multiple entries separated by semicolon.
- Mismatch values of Percentage column between the executive report PDF and actual product UI.
- Engines failed to re-download back when removing them while downloading definition packages.
- Failed to export Sandbox result JSON report on the UI with 403 error.
- Failed to update Deep CDR settings on Central Management 7.
- Scan could be hung while being processed with batch in Central Hub architecture.
- MetaDefender Core service could be crashed when using distributed load extraction with file size filtration setting in Central Hub architecture.

## [Version v5.8.0](/docs/mdcore/release-notes/archived-release-notes#version-v580)

Release Date: 20 December 2023

**New features:**

- Allow post action to override final processing verdict

  - The new setting under "Post Action" section in MetaDefender Core workflow rule (disabled by default) will let authorized users configure the product to scan for the pre-defined final output code returned by your custom post action script (or custom post action webhook server) to determine if the final processing verdict should be overriden as "blocked" by that or not.
  - This new setting create an opportunity for MetaDefender Core customers to customize even better their security policy with their own action's logic.
- Reuse processing result by hash

  - The new setting under "General" section in MetaDefender Core workflow rule (disabled by default) will let authorized users configure the product to automatically reuse eligible processed results with the same hash for all other in-progress submitted requests.
  - A great approach to tremendously boost up the entire processing throughput for certain use-cases such as Email Security, DevSecOps, Cross Domain etc. to avoid repeatedly processing same files within a short time period.
  - Learn more at [Reuse scan results for the same hash](/docs/mdcore/configuration/workflow-rule-configuration#reuse-scan-results-for-the-same-hash-)
- Support Red Hat Enterprise 9

  - Enrich supported OS porfolio in MetaDefender Core with new support for Red Hat Enterprise 9.
  - **Note:** For Deep CDR engine, it is required to install all neccessary libraries mentioned in .[NET 5 dependencies](https://docs.opswat.com/mdcore/knowledge-base/how-to-install-net-31-5-6-runtime-dependencies-on-Linux-Distribu) on RHEL 9
- Support PST archive file sanitization

  - When enabled, MetaDefender Core will remove infected and encryted child files inside original PST file, and create a sanitized version of PST without them.
- Prevent potential brute force attack with forgot-password entries by applying cool down period.
- Improve LOCAL scan mode on MetaDefender Core (by using scan request header `filepath`) to prevent unpredicted behavior when processed files are altered (moved / deleted), but they appear in many other different local locations. Beneficial for File upload or Cross domain use-cases.
- Allow you to track hostname of endpoint machine, and client side's logged-on user information on each MetaDefender Core scan session via using `current_logged_on_user` and `hostname`key under metadata header respectively, and this information will be displayed under MetaDefender Core processing history UI at "metadata" column (hidden by default).

  - For example, you can specify the information for client endpoint's host name and current logged-on user by writing those information in your scan request's header `metadata`as following: `{ "hostname": "<hostname>", "current_logged_on_user": "<whoami>" }`
- Set value of 0 (zero) to scan queue threshold under MetaDefender Core health check now means that, MetaDefender Core will disable checking scan queue status as an input for its health check logic (Legacy previous logic: setting 0 means when no current on-going scans, then it will meet the condition for heath check logic).
- Support URL encode for `metadata` header applied in file or batch processing request.
- Track the last login time for local and SSO user when they login via `POST /login` request.
- Include host name information via using new header `X-Core-Id` of the response HTTP 503 (scan queue is full) returned to `POST /file` request.
- Disable (uncheck) Deep CDR advanced setting `Remove conditional comment` belongs to HTML under MetaDefender Email Gateway Security workflow rule due to Outlook HTML parser limitations.
- Performance improvement: Cache user session information in memory for user validation in every applicable scan request, so MetaDefender Core can skip database reading and improve processing speed.
- Logging improvements

  - Log all SQL statements which took longer time than expecterd in bundled PostgreSQL database log.
  - Enhance MetaDefender Core log for the scan-from-download-link feature to write more information for both sucessful (HTTP 200) and unsucessful (non 200 HTTP) circumstances.
  - Include details of each engine process (path, process ID, working-set size) running under MetaDefender Core in the product support package.
- UI notification when MetaDefender Core configurations are locked due to being managed by Central Management.

**Fixes:**

- Import configuration with big amount of blocklist rules could freeze up MetaDefender Core.
- Quarantined files could be corrupted and unrecoverable under certain circumstance.
- MetaDefender Core randomly crashed at some points when running under "distributed extraction" mode as a part of Central Hub architecture.
- In K8S deployment, random MetaDefender Core instance restarted when starting all available MetaDefender Core instances at the same time in shared and remote PostgreSQL database mode.
- In docker mode, MetaDefender Core cannot start when making change on environmental variable `CORE_DATA _PATH` without attached volume.
- Some UI cosmetics and minor bugs are addressed.

## [Version v5.7.1](/docs/mdcore/release-notes/archived-release-notes#version-v571)

Release Date: 09 November 2023

**New features:**

- MetaDefender Core supports to receive engine update packages from Central Management v8.
- Custom time range for Executive Report.
- Upgraded bundled PostgreSQL to version 14.9 for vulnerability (CVE-2023-39417).
- Improved the integration between MetaDefender Core and Deep CDR to avoid wasting system resource working on timed-out tasks.
- Change Deep CDR retry count default value to 1.
- Introduce Sandbox engine file size limit.
- User password minimum length enforcement from 8 to 30 characters.
- Whenever an user modifies UI settings such as time range or processing history columns, the modified setting value will be remembered and retained for the next user login, without having to re-select again.
- Other blocked reasons added for batch processing.
- Decrypted time in the JSON scan result.
- Logging improvements.

**Fixes:**

- Submiting gzipped file failed with "Content-Encoding: gzip" if the file size is a power of 2 (2^n) bytes.
- Password protection was not retained when scanning a file without file name.
- Wrong status displayed for Threat Intelligence when processing a file bigger than 140 MB and timed out.
- Installation failed on Red Hat Enterprise 8 due to missing wkhtmltopdf library.
- The number of sanitization tasks might exceed than allowed threshold under high load.
- Failed to close large batch when file type detection timed out on files in batch.
- Temporary files generated by Deep CDR and Proactive DLP engines were not cleaned up properly when cancelling scan request.
- Failed to export scan result PDF report on Red Hat Enterprise.

## [Version v5.7.0](/docs/mdcore/release-notes/archived-release-notes#version-v570)

Release Date: 09 October 2023

**New features:**

- SBOM engine integration
- Upgraded NGINX to version 1.22.1 for vulnerability remediation
- Central Hub enhancements

  - Version 2 for MetaDefender Core NAS (file storage server) that supports continuous file streaming directly to MetaDefender Core instance over NAS (without waiting for file streaming to finish at NAS first), and data encryption capacity.
  - Optimized processing for archive extraction load distribution.
- Optimized scan result polling query (GET /file API) for faster response
- New scan results when engine stopped executing due to hitting global processing timeout
- Separated processing time for archive compression
- Separated processing time for external scanner
- Various improvements in MetaDefender Core log for a better visibility when processing files and troubleshooting.
- UI updates

  - Continuous improvements for UI accessibility for WCAG 2.0 and 2.1 level A, AA compliance.
  - Hash comparison after sanitization
  - Search processing results based on Data ID, using the existing search box at the top of the product management console.
  - In-product tagline, and other UI cosmetic updates.

**Fixes:**

- Deep CDR engine failed to install and became permanently failed when MetaDefender Core contains a lot of custom worflow rules.
- File processing could hang up when timing out during hash lookup with File Reputation.
- DLP result of archive file was "No Specific Configuration" instead of "Unsupported File Type" when containing allowed file.
- "Not scanned" returned by AV engines when processing archive file but disabling extraction mode.
- "Others_time" in the JSON scan result was mistakenly set to negative when a file is quarantined due to global processing timeout exceeded.
- "start_time" in the JSON scan result was set to 1970-01-01 for in-progress file processing.

## [Version v5.6.1](/docs/mdcore/release-notes/archived-release-notes#version-v561)

Release Date: 28 August 2023

**New features:**

- Integration with My OPSWAT portal

  - Get ready for My OPSWAT integration where MetaDefender Core can connect and be managed in My OPSWAT product inventory.
  - Stay tuned for My OPSWAT further updates (end of September) to get hold of this integration on My OPSWAT.
- Continuous improvement on UI accessibility

  - Various UI updates and remediations for UI accessibility support.
- New filtration sub-setting for file type detection fallback to extension

  - The new setting is under MetaDefender Core workflow - File Type tab. This new setting can be only enabled when the existing parent setting "Fallback file type detection to current extension if needed" is checked.
  - When enabled, MetaDefender Core will avoid using current file extension as a fallback when actual file type is not enabled for Deep CDR engine's setting.
- More comprehensive details for processing time in the JSON scan result

  - Introduce a new key `post_action_time` (separated from `others_time`) for actual time spent on post action (if applicable). This key is under `processing_time_details` key in the JSON scan result.
  - Introduce a new key `cdr_wait_time` to determine actual time spent when request is sitting in queue waiting for Deep CDR available to start processing. This new key is under `sanitization_details` in the JSON scan result.
  - Introduce new keys `cdr_storage_time`/ `dlp_storage_time`/ `quarantine_storage_time`to determine actual time spent on output file being saved in storage for sanitization / sensitive data processing / quarantine processing (applicable when Deep CDR, Proactive DLP and Quarantine is enabled for that scan). These new keys are under `processing_time_details`key in the JSON scan result.
  - Applicable to all of those above new processing time, we also support for data statistics for admins to view under Executive report UI when needed.
- Enhancement on database connection pool

  - Revamped back-end logic for database connection pool to mitigate potential bottleneck on database queries under extreme load.

**Fixes:**

- Sometimes failed to close batch under high load and problematic circumstances with files inside batch.
- Batch signature was not generated when batch contains hundreds thousands of files inside.
- Failed to send callback for sanitizeurl webhook requests.
- MetaDefender Core could rarely crash when repeatedly processing .docx large files.
- Temporary files could not be cleaned up when hitting global timeout.
- Memory increasing abnormally and leaking with data statistics against PostgreSQL.
- Other minor stability issues.

## [Version v5.6.0](/docs/mdcore/release-notes/archived-release-notes#version-v560)

Release Date: 14 July 2023

**New features:**

- Support PostgreSQL 14.8

  - MetaDefender Core now also supports PostgreSQL 14 (verified with 14.8).
  - Bundled PostgreSQL server comes with MetaDefender Core standalone deployment also comes with this new version.
  - **NOTE*:*** *For MetaDefender Core upgrade from older version 5.5.1 or older (using PostgreSQL 12) to version 5.6.0 (using PostgreSQL 14), it is required to run MetaDefender Core installer as admin privileges to ensure the database migration task finish successfully.*
- Priority for workflow

  - Provide better option for Quality of Service on workflow, MetaDefender Core now supports users to define certain priority for each workflow rule. This enhancement will help users control better business priority in file processing.
  - You can find this new setting under "General" workflow tab.
- Time availability for workflow

  - Only allow scan requests using certain workflow during pre-defined time windows. You can find this new setting under "General" workflow tab.
- Global processing timeout per workflow

  - MetaDefender Core provides one global timeout for entire processing applied to every scan request. This is expected to help client integration control its SLA for every scan at ease.
  - This new setting could be configured separately for each workflow rule.
  - When a scan request is timed out by this global processing timeout setting, the scan request will be blocked with "Global timeout exceeded" as blocked reason.
  - **NOTE:** *This global processing timeout, when enabled, it should be greater or equal to the sum of all other engine related timeout settings such as Metascan timeout, Deep CDR timeout etc.*
  - You can find this new setting under "General" workflow tab.
- Override global processing timeout for specific scan requests

  - Client also can override the new setting of global processing timeout per specific scan requests when needed, by using a new request header `global-timeout` for the file submission request.
  - Details: [POST - Analyze File (Asynchronous mode)](/docs/mdcore/metadefender-core#fileanalysispost)
  - If this header is not set, or its value is empty, then MetaDefender Core will use the pre-defined global processing timeout in corresponding workflow rule (only when enabled).
- Hash lookup supported for in-progress scan

  - Before having to submit another scan request for a same file to MetaDefender Core and duplicate the effort of scanning, client could now utilize the hash lookup API [GET - Fetch Analysis Result By Hash](/docs/mdcore/metadefender-core#hashget) to be acknowledged that a same file is actually being processed, so client could waive the same request to MetaDefender Core.
  - Introduce a new header `include-inprogress` for [GET - Fetch Analysis Result By Hash](/docs/mdcore/metadefender-core#hashget) to indicate whether or not client would want to receive "In-progress" (instead of not found result) in such circumstance.
- Allowlist by vendor filtration

  - Allow users to create a filter on MetaDefender Core to add PE (Portable Executable) files tied to certain vendors into the allowlist.
  - Furthermore, users can be supported to block those PE files when unsatisfied the pre-defined conditions. You can find this new setting under "Allowlist" workflow tab.
- Continuous improvement for Sandbox (formerly OPSWAT Filescan) engine integration

  - Rename "OPSWAT Filescan" engine to "Sandbox".
  - Add `extraction_info` to the scan result JSON of [GET - Fetch analysis reports containing all files in archive](/docs/mdcore/metadefender-core#fileanalysisgetallchildfiles)
  - Adjust default enabled file types for Sandbox file processing under workflow:
  - Remote Sandbox: all file types are selected by default.
  - Local Sandbox: all file types except archive are selected by default.
- New option to skip sanitizing empty files

  - When enabled, MetaDefender Core will avoid sanitizing empty file (zero bytes). By default, it is disabled. You can find this new setting under "Deep CDR" workflow tab.
- Attach MetaDefender Core server information in scan result fetching response

  - When enabled via using a new supported API endpoint [PUT - Update list of custom response headers](/docs/mdcore/metadefender-core#configputcustomresponseheader), MetaDefender Core will return allowable server information (deployment ID, server IP address and port) in designated header `X-Core-Id` in the scan result fetching response (e.g. GET /file/<data_id>).
  - This new API endpoint also supports users to only return those pre-defined data to authenticated scan requests (where uses API key in the request).
- Throttling option for scanning webhook

  - Support new parameters `workercount` , `requestqueue` in the existing API endpoint [PUT - Webhook set configuration](/docs/mdcore/metadefender-core#configupdatewebhook) to define better flexibility for scan webhook:

    - workercount: the total number of workers for the webhook responser (for sending callbacks to the webhook client). Default is 1. **Note:** a service restart is required for changes to take effect.
    - requestqueue: the maximum number of requests allowed for each worker. Default is 100.
  - Besides that, now users can set zero (0) for the existing parameter transfertimeout for the [PUT - Webhook set configuration](/docs/mdcore/metadefender-core#configupdatewebhook), that means, disable timeout for sending callbacks to webhook client.
  - **NOTE:** *These throttling options only apply to webhook mechanism that notify processing result, do not apply to the mechanism where MetaDefender Core sends sanitized file back to the client just yet.*
- Enhance sorting feature in processing history UI

  - Enhance the existing feature to allow sorting entire scan history across all pages (previously only allow sorting current UI page on MetaDefender Core version 5.5.1).
- Continuous improvement for UI accessibility

  - Address issues and enhance GUI for better accessibility readiness.
- Display file size and file type even when file is being processed

  - On processing result UI screen. Including when the file is being processed, or already finished.
- Display setting for scan duration on the UI

  - Allow users to specify preferred time format for scan duration to be displayed on the UI.
- Other UI enhancements

  - Move max file size setting from "Metascan" tab to "General" time in workflow.
  - Update to rename and logo from Cyren (AV engine) to Varist.
  - Other enhanced UI cosmetics.

**Fixed:**

- Callback responses got stuck

  - Under high load, MetaDefender Core could fail to send callback responses to webhook client.
- Health check API returned out of date data

  - Under high load, the heath check API [GET - Get health check status](/docs/mdcore/metadefender-core#healthcheck) could return out-of-date data for scan queue and engine status.
- Inconsistent scan result with Threat Intelligence under Quarantine

  - Scanning with Threat Intelligence under Quarantine could return inconsistent result.
- Leftover temporary files when timing out with Sandbox (formerly OPSWAT Filescan) engine

  - When a scan is done with timeout for Sandbox (formerly OPSWAT Filescan), temporary file was not cleaned up properly.
- Other minor bug fixes

## [Version v5.5.1](/docs/mdcore/release-notes/archived-release-notes#version-v551)

Release Date: 18 May 2023

**New features:**

- Continuous improvements on OPSWAT Filescan engine integration
- - New configuration to trigger OPSWAT Filescan processing when number of scan failures from AV engines' results exceeded certain amount of threshold.
  - Behavior changes: skip sending extracted child files of MS Office files to OPSWAT Filescan engine for processing.
  - Fixed some minor bugs related to UI display.
- Blocking file processing based on Deep CDR forensic analysis policy

  - New configuration to allow authorized users to block file processing based on Deep CDR forensic analysis policy. The policy will be managed and defined under Deep CDR engine advance settings.
  - ***Requires Deep CDR 6.6.0 or above (to be released at the end of Q2-2023).***
- Workflow rule cloning

  - Similar to workflow template, now allowing authorized users to clone / duplicate existing workflow rule.
- UI accessibility continuous improvements

  - Enormous changes and improvements towards UI accessibility support. This UI accessibility mode can be enabled on the top section of every UI page.
- Auto enabling any newly supported file types for sanitization

  - New setting to allow MetaDefender Core to auto enable any file option that newly supported by Deep CDR for sanitization.
  - This option is unchecked by default to keep backward compatibility. You can enable it under Deep CDR tab in workflow rule > Enable for file types section.
- New attribute added into existing key `extraction_info` in the JSON scan result structure

  - is_encrypted_file (optional, only accept "true"/"false"): a flag to indicate a file is encrypted or not.
  - See more details on [GET - Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget)
- Handling MSG file with archive sanitization use-case

  - When enabling "Block unsupported file type" under Deep CDR section, then sanitization on MSG file failed due to msg.data file (blocked as unsupported).
  - This change on MetaDefender Core to avoid that situation, and instead let the archive compression engine take care of the MSG archive sanitization properly.
  - ***Requires archive compression engine version 6.2.3 or above.***
- Optimizing memory consumption by ometascan service under load

  - Possibly helped reduce up to 50% memory consumption with ometascan service.
- Sorting columns in table under processing history UI

  - Currently supported users to sort processing history UI based on start time and scan duration.
- Adding parsing digital signature processing time

  - New key named `parse_dgsg_time` added into the existing `processing_time_details` __to indicate actual processing time spent on parsing digital signature against file.
  - See more details on [GET - Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget)
- Support retry configurations for webhook post action

  - Users now can customize retry mode and timeout setting for webhook post action in Workflow Rule.
- Including current process name, ram usage, cpu usage into the support package

  - New data will be collected and stored in new CSV files located in the support package.
- Improve query time for filter labels API

  - Helped improve search response time on the processing history UI page.
- UI enhancements

**Fixed:**

- Handle processing properly with content-encoding of gzip or x-gzip

  - When submitting file request, if mistakenly specified Content-Encoding header value = gzip or x-gzip, MetaDefender Core returned HTTP 500 error with unexpected JSON output.
  - For example: {"err":"Invalid gzipped body"}{"data_id":"a3179bc183a6494694768c315a21867d"}
  - Now addressed the issue to let MetaDefender Core return HTTP 500 error with proper JSON output, for example: {"err":"Invalid gzipped body"}
- Timeout occurred with synchronous submission requests

  - Addressed the issue when MetaDefender Core returned scan timeout immediately against synchronous scan requests.
- URL encoded "rule" header in scan request
- - MetaDefender Core did not decode values in the "rule" header when it is URL encoded (for example: "rule" = "File%20process")

## [Version v5.5.0](/docs/mdcore/release-notes/archived-release-notes#version-v550)

Release Date: 06 April 2023

**New features:**

- OPSWAT Filescan integration

  - OPSWAT Filescan is an unique adaptive threat analysis technology, enabling zero-day malware detection and more Indicator of Compromise (IOCs) extraction. Learn more at <https://docs.opswat.com/filescan>
  - MetaDefender Core now fully integrate with OPSWAT Filescan (as an engine module), and provide two separate engines:

    - **OPSWAT Filescan Embedded engine:** bundled in MetaDefender Core server, and the engine will process files locally itself.
    - **OPSWAT Filescan Remote engine:** the engine is supposed to send file requests to another remote OPSWAT Filescan system for processing. Requiring users to provide proper remote OPSWAT Filescan URL and API key.
  - We need separate MetaDefender Core license key for each engine option (Embedded vs. Remote).
  - Both OPSWAT Filescan engines require Java 8 JRE x64 (Windows and Linux) and Microsoft Visual C++ Redistributable for Visual Studio 2015 x64 (Windows only) as dependencies. Please make sure to have them installed on MetaDefender Core server before deploying OPSWAT Filescan engine.
  - The integration comes with two modes:

    - **Inline:** working as a part of MetaDefender Core processing workflow (real-time processing). Allowing users to block entire processing based on OPSWAT Filescan engine's outcome and decision.
    - **Out of band:** working as a part of MetaDefender Core quarantine (post-investigation processing).Providing additional option to analyze quarantined items along with the existing Threat Intelligence technology.
  - OPSWAT Filescan engine (both Embedded and Remote) provides configurations under workflow rule (for inline mode), and under engine module - Inventory (for out of band mode).
- UI accessibility

  - MetaDefender Core provides a new UI mode to support accessibility view. By default, this option is disabled.
- Licensing with On-prem License Management Server (OLMS)

  - This feature requires the upcoming new product (On-prem License Management Server) and our existing cloud-based service (Activation Server) to operate.
  - New licensing managment model for MetaDefender Core to allow On-prem license management server (OLMS, to be released later) to manage the product's license status including activation, deactivation.
- Shared Authentication Session

  - In the shared database model, MetaDefender Core instances now can share same authentication session among them. That helps eliminate the need to manage separate authentication sessions on load balancer side.

This new feature supports local authentication, AD / LDAP authentication and also Single Sign-On (SSO).

- Customized Proxy Configurations

  - In constrast to what we provided in the past for proxy configuration, which is only one setting for all network involved modes on MetaDefender Core, now we provides a much more flexible way to define separate proxy configurations for each MetaDefender Core functionalities that require network connection.
- Webhook for post action

  - Besides the existing option to allow MetaDefender Core trigger each separate sub-processes to run your pre-configured post action script, now you are provided with another new option to run post action in multi-threading mode, as a part of workflow processing.
  - When configured under post action page (Inventory menu), for each file processing, MetaDefender Core will send pre-configured callback URL to your designated webhook server, and you can define to run series of actions on webhook server asynchronously. Please note you will want to setup webhook server on your own.
  - This new post action model helps improve overall performance.
  - Note: Currently, only HTTP protocol is supported for callback URL.
- SHA256 checksum for sanitized file

  - MetaDefender Core provides SHA256 checksum for sanitized file in the final JSON scan result. You can find it at`sanitization_details.sanitized_file_info.sha256`
- UI enhancements

**Fixed:**

- Archive engine integration issue

  - Fixed issues caused by archive engine integration that could make negative impact on archive extraction performance, as well as cause memory leak issue.
- MetaDefender Core service crashed under certain circumstance

  - When scanning some special files, MetaDefender Core could crash due to its file signature analysis feature.
- RootCA ceritificate store could not be loaded in Linux

  - When having *.0 files in rootCA trusted store.
- Some UI cosmetics and minor bugs are addressed.

## [Version v5.4.1](/docs/mdcore/release-notes/archived-release-notes#version-v541)

Release Date: 28 February 2023

**New features:**

- [Central Hub] High availability for distributed archive extraction

  - While handling distributed extraction, if a MetaDenfeder Core instance dies for whatever reasons, then distributed extraction task should keep running on another alive MetaDefender Core instance.
- [Central Hub] New setting to set file size limit (min - max) for distributed archive extraction
- Exception for file types based blocklist

  - A new setting under "Blocklist by file type" option for Blocklist configuration to allow users configure to block everything but excluding certain file types.
- Comprehensive session timeout settings on UI
- Security enhancements

  - Support TLS v1.3: Harden security policy with TLS v1.3 supported for HTTPS connection. By default, both TLS v1.2 and v1.3 are allowed for client handshake.
  - Upgraded to OpenSSL 3.0.8 for vulnerabilities.
  - Addressed vulnerability with security through obscurity, and information leakage.
  - Improved license enforcement mechanism for corner cases while communicating with the licensing server.
- Retain original file name with special encoding for archive extraction

  - Note: This feature requires Archive engine version 6.2 or newer.
  - By specifying correct encoding of original file name via engine-metadata header while doing file submission POST /file, MetaDefender Core will work with archive engine to retain original filename with the same designated encoding after extracted.
  - For example: engines-metadata={ "extraction": { "charset": "SJIS" } }
- Support to sign in MetaDefender Core via Identity Provider site (also known as IdP-initiated SSO)

  - IdP-initiated SSO allows users to login to MetaDefender Core dashboard directly from IdP homepage.
  - Users must enable this new setting under SSO user directory page on MetaDefender Core UI.
- Support proxy_pass for NGINX web server on MetaDefender Core

  - Use proxy_pass to redirect the URL to another designated location.
  - For example - redirect <https://localhost:443> to <https://localhost:8008> Add file *.conf under C:\Program Files\OPSWAT\MetaDefender Core\nginx
- Supported same date selection for processing history filtering
- Display "In-progress" label in processing history UI
- UI enhancements

  - Addressed UI accessibility issues
  - Sensitive Data Protection statistics on the Dashboard UI: Changed to calculate and display total number of sensitive result detections (previously: total number of hit objects).
  - Update UI labels and hyperlinks for My OPSWAT portal.

**Fixed:**

- [Central Hub] Hub service could be crashed while running under high load circumstance.
- [Central Hub] Failed to link files in batch

  - Hub refused to correlate files to a batch which was initiated by a MetaDefender Core instance (returned HTTP error 400 - Cannot scan in given batch)
- Deep CDR engine process could be crashed on Linux based system

  - While processing MS Office 2003 files, only impacted Linux based MetaDefender Core.
- Synchronous scan submission issue

  - "Require a min number of AV engines for the whole file processing" setting, if enabled and configured, did not work as expected for synchronous scan submission with local file scan feature.
- Data warehouse failed to refresh, when data contains non-Unicode characters.
- File type mismatched result was not displayed

  - When there was another higher blocked verdict (e.g. Sensitive Data Found) is also available.

## [Version v5.4.0](/docs/mdcore/release-notes/archived-release-notes#version-v540)

Release Date: 04 January 2023

**New features:**

- Central Hub enhancements

  - Applicable to Central Hub version 1.1.0 or above.
  - Load shared among MetaDefender Core instances for archive processing (extraction).
  - Shared authentication session among MetaDefender Core instances using Redis caching server.
  - Batch processing supported.
- Docker containerization enhancements

  - Supported MetaDefender Core upgrade with zero down time on containerization environment Kubernetes (blue/green and rolling strategies).
  - Supported MetaDefender Core upgrade with data retention.
  - Log rotate service built in docker base image.
  - Supported proxy configuration for docker run.
  - Supported new option to enable "allowCrossIPSessions" when starting MetaDefender Core on container environment.
- UI enhancements

  - UI remediations and enhancements for accessibility support and compliance.
  - Backup license status displayed on UI.
  - Sanitized label as indicator in the processing history.
  - Search by name supported for workflows.
  - Appropriate UI result for vulnerability assessment when "skip hash calculation" setting is enabled.
  - Descriptive tooltip for "Fallback file type detection to current extension if needed" setting.
  - Changed setting name "Blocklist unsupported file types" to "Block unsupported file types".
- Security enhancements

  - Upgraded 3rd party libraries (gperftool, libxml2) for vulnerability risk.
  - Digest verification supported in FIPS enabled environment while installing MetaDefender Core.
- Logging enhancements

  - Avoided misleading (and unharmful) error messages in PostgreSQL logs.
  - Added batch ID and data ID information in NGINX access logs
  - Removed misleading warning messages in MetaDefender Core logs while updating engines via folder.
- Hash lookup performance improvement
- Support Windows 11
- New configuration to reject file submission based on engine availability

  - Only allowing MetaDefender Core to accept file processing submissions when certain crucial engines are available.
  - This setting can be found under workflow rule - General tab.
- New configuration to add exception for unsupported file types for sanitization

  - Adding exception list for unsupported file types for sanitization. By doing so, those file types configured in the exception list will not be blocked.
  - This setting can be found under workflow rule - Deep CDR tab.
- New configuration to block or allow file processing if smaller or bigger than certain file size

  - Allowing MetaDefender Core to block or allow file processing submission if its payload exceeds or smaller certain size.
  - This setting can be found under workflow rule - Blocklist and Allowlist tab.
- New configuration to skip processing fast symlink in archive file

  - By default, MetaDefender Core will try to process any files, including fast symlink in archive. However that could cause sanitization failure due to unsupported.
  - This setting can be found under workflow rule - Genertal tab.
- Import full configuration package (.zip) via the ignition file

  - Supported automation better with full configuration package (.zip) via the ignition file. Example: eula=true [config] import=settings.zip import_password=123 ....
  - Details: [Ignition file](/docs/mdcore/installation/deployment-automation-support#ignition-file)
- Webhook callback retry mechanism enhancement

  - Enhanced webhook retry mechanism for resending callback result in case of either timeout or not receiving webhook server’s response.
  - Timeout threshold could be defined via new key `transfertimeout` (by default, 30000 ms) with [PUT - Webhook set configuration](/docs/mdcore/metadefender-core#configupdatewebhook)
- New CLI tool to clean up database created by no-longer-used MetaDefender Core instance in the shared DB mode

  - Using this tool to clean all scan data from MetaDefender Core instance(s) that you no longer use, applicable in the shared DB mode.
  - This tool can be found:

    - Windows: C:\Program Files\OPSWAT\MetaDefender Core\ometascan-db-cleaner.exe
    - Linux: /usr/sbin/ometascan-db-cleaner
  - Details: [Database Cleanup Tool in Shared DB Mode](/docs/mdcore/troubleshooting/database-cleanup-tool-in-shared-db-mode)
- New CLI tool to check remote PostgreSQL user compliance

  - This tool is to help your database system admin quickly determine whether or not your remote PostgreSQL database have sufficient user privileges as described at [PostgreSQL User Privilege Requirements](/docs/mdcore/troubleshooting/postgresql-user-privilege-requirement) to work properly with MetaDefender Core application.
  - Details: [Remote PostgreSQL User Privileges Checking Tool](/docs/mdcore/troubleshooting/remote-postgresql-user-privileges-checking-tool)

**Fixed:**

- Retrieving file processing result hit 404 not found

  - Could happen when using archive compression with Proactive DLP
- Incorrect memory resource utilization report

  - Updated to recalculate memory available reported on the UI.
- Undesired behavior on the UI with API rate limiting

  - When hitting the limit, the UI hung at the uploading screen.
- Some UI cosmetics and minor bugs are addressed.

## [Version v5.3.1](/docs/mdcore/release-notes/archived-release-notes#version-v531)

Release Date: 07 November 2022

**New features:**

- Upgraded OpenSSL framework from version 3.0.5 to version 3.0.7 for its recent vulnerability patches ([CVE-2022-3358](https://www.openssl.org/news/vulnerabilities.html#CVE-2022-3358), [CVE-2022-3786](https://www.openssl.org/news/vulnerabilities.html#CVE-2022-3786) and [CVE-2022-3602](https://www.openssl.org/news/vulnerabilities.html#CVE-2022-3602)). More details: <https://www.openssl.org/news/openssl-3.0-notes.html>

## [Version v5.3.0](/docs/mdcore/release-notes/archived-release-notes#version-v530)

Release Date: 27 October 2022

**New features:**

- Central Hub new architecture (BETA)

  - Serving large scale deployments with better dynamic auto-scaling, high availability and fault tolerant.
  - The Central Hub architecture incorporates multiple newly crafted components running as service, and also containerization environment friendly:

    - MetaDefender Core.
    - PostgreSQL database server.
    - Central hub (known as "MetaDefender Core Hub").
    - File storage server (known as "MetaDefender Core NAS").
    - Redis (the open-source caching server).
    - RabbitMQ (the open-source messaging broker).
  - More details: [MetaDefender Cluster Deployment](/docs/mdcore/cluster-deployment/md-cluster-deployment)
- PostgreSQL bundle upgrade

  - Applicable to PostgreSQL server bundled with MetaDefender Core installation. It is upgraded to version 12.12 (from old version 12.11) for vulnerability fixes.
- Engines integration improvements

  - Back-end related improvements against engines integration for more scalable, flexible and robust engines' new features and furture changes without MetaDefender Core upgrade requirement.
- New workflow setting for Proactive DLP

  - Allow users to configure MetaDefender Core to block file processing (final verdict = Blocked) if the Proactive DLP processing fails or times out.
- Vendor information added into processing result PDF report

  - Only applicable to files which are detectable for file signature.

**Fixed:**

- Product stability improvement

  - MetaDefender Core service could crash under certain circumstance (modifying workflow rules while actively scanning files).
  - Integration issue with Deep CDR that could possibly wipe up sanitized files by mistake when Deep CDR engine is stopped.
  - Engine ID was wrongly displayed in workflow rule for "excluded engines" section after removing that engine.
- Product UI fixes

  - Custom date and time feature: users could not set PM for start time, and AM for stop time as a range. For example: Sep 07 12:00:00 PM to Sep 08 12:00:00 AM

## [Version v5.2.2](/docs/mdcore/release-notes/archived-release-notes#version-v522)

Release Date: 06 October 2022

**New features:**

- External scanner and post action are now available configurable for the workflow

  - Use certain external scanners and post actions with corresponding settings in each workflow rule.
  - The import & export configuration feature will also support to cover external scanners and post actions defined in the workflow.
  - For MetaDefender Core upgrade scenario:

    - When you already have external scanners and post actions defined in the Inventory in older product version, then all of them will be automatically added to every available workflow rule (not template) in the new product version once upgraded.
    - Applied to shared DB mode, all external scanners and post actions settings will be auto shared among MetaDefender Core instances, unless the license for external scanner on each MetaDefender Core is different.
  - Details: [External Scanner and Post Action](/docs/mdcore/configuration/workflow-configuration-template#external-scanner-and-post-action)
- File digital signature vendors in the executive report

  - Vendor statistics information for file digital signature is now calculated and displayed in the executive report.
- More details for file digital signature analysis information

  - Detect multiple signers (co-signers).
  - Verbose information of digital signature: version, issuer, serial number, digest algorithm, digest encryption algorithm.
- Archive extraction performance improvement

  - When processing archive file that includes empty folders.
- UI updates

  - Vulnerabilities Detection now is clickable.
  - Support to check enabled file types for sanitization in the workflow rule when MetaDefender Core is managed by OPSWAT Central Management.
  - Some other minor UI changes.

**Fixed:**

- Product stability improvement

  - Iterrupted connection with syslog server could crash the MetaDefender Core service.
  - Nested files was not be extracted correctly if its filename and its parent folder name are identical.
  - Did not display the result and error correctly when processing unsupported file types with Threat Intelligence.
  - User management UI loaded very slowly while handling numerous (thousands+) users.
- Product UI fixes

  - Too aggressive polling for file processing result when users navigated to some last pages.
  - UI cosmetic bug fixes.

## [Version v5.2.1](/docs/mdcore/release-notes/archived-release-notes#version-v521)

Release Date: 30 August 2022

**New features:**

- Compression tab in workflow

  - MetaDefender Core workflow is organized better with new compression tab to provide the archive compression related configuration for both existing Deep CDR use-case, and now, for the new-feature Proactive DLP use-case as well on archive files.
  - More context: archive compression technically covers the archive sanitization feature that we know so far, but now we take them out from Deep CDR workflow tab to mange everything relevant under the new Compression tab for both Deep CDR and Proactive DLP use-case.
- Archive processing (Compression) with Proactive DLP

  - MetaDefender Core now supports the archive compression for Proactive DLP use-case, along with already-supported Deep CDR so far.
  - That means, MetaDefender Core will also pack applicable output files produced by Proactive DLP as well for the new compressed archive.
  - By default to keep backward compatibility, this feature is turned off for Proactive DLP use-case, and you must enable it under the new Compression workflow tab.
- Hash lookup API new features

  - Hash lookup API is prefered to optimize the file processing especially when same files to be processed over again within a short time period.
  - MetaDefender Core now supports 2 new modes for the hash lookup API via new headers called `timerange` and `selfonly`:

    - `timerange` (number of hours): allow scoping down the recent number of hours that hash lookup task should start from till now, instead of searching the entire scan history in MetaDefender Core database.
    - `selfonly` (true/false): useful to archive hash lookup, allow specifying to only perform hash lookup against the original archive file self only, and skip searching all child files result within the original archive.
  - More details: [Fetch Analysis Result By Hash](/docs/mdcore/metadefender-core#hashget)
- Verbose file type analysis data

  - Support to expose verbose file type analysis data in JSON scan details. This can be done via setting `include_`file___`details` in the `engines-metadata` header for POST file submission request.
- Expose file type ID information

  - The info can be found in both JSON scan details, and on the scan result page UI. The file type ID will help indicate unique file type identification, e.g. PDF / TXT
- Engine dependency missing error response

  - Certain engines on MetaDefender Core require specific dependencies to run properly, otherwise failing on engine is expected. MetaDefender Core now make the dependency missing error more visible in both UI and log, and help troubleshooting easier and faster.
- Custom internal PostgreSQL user

  - MetaDefender Core once installed, it will automatically create an internal PostgreSQL user for operation purpose, and so far that user name is auto randomized by MetaDefender Core and non adjustable (`usr_<random characters>`).
  - Now MetaDefender Core supports database system admin to define and change to their own PostgreSQL user instead.
  - More details: [Customize Internal PostgreSQL User](/docs/mdcore/troubleshooting/customize-internal-postgresql-user)
- Security enhancements

  - Continuing to harden and secure MetaDefender Core even better to prevent potential HTML injection and XSS attacks.
- UI updates

  - The setting page is auto refreshed itself after importing configurations.
  - Added copy button to copy entire file path on the scan result UI.
  - Pagination supported for "Skip by hash" UI.
  - Numbers on the dashboard are now clickable.

**Fixed:**

- Product stability improvement

  - MetaDefender Core on Linux crashed randomly while processing archive files.
  - Very long list of hashes in the Skip by hash caused slow response time on some admin API endpoints.
  - Regular expression validation failed with mode modifier (?i).
  - Display issue with pagination on the processing history UI.
  - Engine download could be hung up if keep hitting download error.
  - Failed to show blocked leaf files if searching by hash.
  - Filtering by post action was not correct on the processing history UI.
- Product UI fixed

  - UI cosmetic bug fixes.

## [Version v5.2.0](/docs/mdcore/release-notes/archived-release-notes#version-v520)

Release Date: 12 July 2022

**New features:**

- New OS support

  - Windows Server 2022
  - Debian 11
- Security enhancements

  - As a regular security practice, we upgraded 3rd party dependencies and development framework to prevent critical vulnerabilities:

    - Upgraded OpenSSL 3
    - Upgraded Qt framework 6
- Executive report in PDF

  - The executive report is now supported for PDF file export. Details: [Executive Report](/docs/mdcore/operating/dashboard#executive-report)
- File digital signature verification

  - File digital signature is now analyzed and recognized by MeDefender Core while processing. The vendor digitial signature is available on both processing details UI page and JSON scan result, and also calculated for the statistics found on [Executive Report](/docs/mdcore/operating/dashboard#executive-report). Also supporting users to allowlist files based on specific vendor names (using regular expression) configured in the workflow rule (under "Allowlist" tab).
  - Currently only PE files are supported `.`acm,`.ax, .cpl, .dll, .drv, .efi, .exe, .mui, .ocx, .scr, .sys, .tsp` ([Portable Executable](https://en.wikipedia.org/wiki/Portable_Executable))
- Blocked leaf files filtered in archive scanning

  - Leaf file (in archive scanning context): file that not having any successful extracted file inside.
  - Support to filter and display blocked leaf files in archive scanning on the processing details UI page ("Show blocked leaf files" checkbox). That helps narrow down the searching scope, and spot out exactly blocked files that should be investigated further.
- Blocked reasons exposure

  - All blocked reasons are exposed on the processing details UI page (if archive file, then also inheriting from child files' blocked reasons if available), that helps with further context on unclear failures, and troubleshooting.
- A setting to exclude sanitize version of blocked child files from archive sanitization

  - By default ([Archive Sanitization](/docs/mdcore/deep-cdr/archive-sanitization)) feature will pack following into sanitized archive file:

    - All allowed child files (or their sanitized version if available).
    - Sanitized versions of blocked child files (if blocked child files are sanitized successfully).
  - A new setting "Include sanitized version of blocked child files" under Deep CDR tab in MetaDefender Core workflow rule will allow you skipping not to include sanitized versions of blocked child files, so that you can conduct further investigation on those blocked files first.
- Sanitization tag on processing details UI page

  - Especially helpful to archive processing when you can tell which child files are sucessfully sanitized, and which files are not on one UI screen (without checking every single child file for details).
- Data retention for statistics

  - The new setting can be found under Settings page - Data Retention tab with named "Statistics". By default, the retention range is set to 6 months.
  - Details: [Data Retention](/docs/mdcore/configuration/data-retention)
- An installation option to skip startup UI screens

  - Better support for automation environments. A new setting `skip`**_startup _**`pages` supported in the ignition file to skip all welcome and other startup pages (e.g. upgrade result) when installing / upgrading MetaDefender, and going straight to the product index default page.
  - Details: [Ignition file](/docs/mdcore/installation/deployment-automation-support#ignition-file)
- Skipped sanitization result

  - A new sanitization result to indicate the santization is skipped due to certain reasons ruled by Deep CDR configurations.
- Child files processing time displayed in achive processing JSON result

  - Original archive file will want to wait for all child files processing to be finished before finalizing the overall processing.
  - Previously `others_time` covered that as well in JSON result, but now we make a dedicated new field for that in JSON result called `wait`*_*`child_``files_time`
- HTTPS configuration removal tool

  - Just in case you configured HTTPS via MetaDefender Core UI but due to unexpected failures on certificates, and thus being blocked to make any change because MetaDefender Core service is not running, thus you need to disable HTTPS configuration on MetaDefender Core using a dedicated CLI tool - ([HTTPS Configuration Removal Tool](/docs/mdcore/troubleshooting/https-disablement-tool)
- Minor UI changes

  - Some UI updates on the executive reports, modules.

**Fixed:**

- Product stability improvement

  - Failed to process same files repeatedly with scan-by-download-link feature.
  - Failed to extract archive files occasionally.
  - SSL certificate issue on RedHat 8.
  - Memory leak during PostgreSQL disconnection and more scan requests are still coming.
  - Other minor product bug fixes.
- Product UI fixes

  - UI cosmetics bug fixes.

## [Version v5.1.2](/docs/mdcore/release-notes/archived-release-notes#version-v512)

Release Date: 27 April 2022

**New features:**

- Vulnerability CVSS v3 scoring

  - File-based Vulnerability Assessment now supports CVSS v3 scoring, also comes with attack classification and impact details.
- Fallback for engine (module) deployment

  - Engine deployment on MetaDefender Core is now fault-tolerant support i.e. just in case a new version of engine ever failed to be deployed, the current (older) working engine version will be re-used and kept running well.
  - Notes:

    - Disable and re-enable engine: MetaDefender Core will try to re-deploy the new engine version again, if still failing, then the old-working engine version build will be re-used (fallback).
    - Remove engine: MetaDefender Core will remove all engine package(s) entirely, including new and old-working versions.
    - Not supported for custom engines which require separate engine installation setup

**Fixed:**

- Product stability improvement

  - Faster API responses when processing very long list of users (>= 1000 users).
  - Custom engines sometimes could be inactive after being updated.
  - Even when enabling processing of allowlisted file in Workflow Rule, the file could not be processed properly.
  - Fixed minor product bugs.
- Fixed some security vulnerabilities on the product:

  - Privilege escalation: allows non-admin users to gain unauthorized privileges on the product to execute harmful actions via the user management configuration. Details: CVE-2022-32272
  - Information leakage: an MetaDefender Core user without permission of accessing to the MetaDefender Core server could leverage the observable discrepancy attack method to expose file system structure on where the product resides via the certification configuration. Details: CVE-2022-32273
- Product UI fixes

  - The pie chart in the Executive Report page was not rendered and displayed correctly occasionally.
  - Some other UI cosmetic minor fixes.

## [Version v5.1.1](/docs/mdcore/release-notes/archived-release-notes#version-v511)

Release Date: 31 March 2022

**New features:**

- Product performance improvement

  - Up to 50% throughput increased while processing archive / office files. Applicable under certain circumstances, configurations and data.
- Product security improvement

  - Remediate some potential security related issues while operating MetaDefender Core.
- Optimize processing flow for office files

  - All child nested files inside original office file are no longer sanitized and DLP processed separately.
- Bundle PostgreSQL upgrade (v12.10)

  - Applicable to the local PostgreSQL server bundled with MetaDefender Core installation.
- User's API key redeployment

  - Allow API key of an already-removed user to be assigned to another user, this is to ensure no interruption or changes in the cross-system integration.
- Health check settings supported for the configurations export/import feature

  - Health check settings ([Health Check API Configuration](/docs/mdcore/configuration/heath-check-api)) is now included in the MetaDefender Core configurations export/import feature
- Auto upgrade when connecting to an older database version

  - Allow MetaDefender Core auto detect and upgrade its database when connecting to an older database version as expected.
- Single Sign On (SSO) SAML enhancements

  - Support AES128-GCM and AES256-GCM encryption algorithms.
- Product UI/UX enhancements

  - Add OS information to the dashboard UI
  - Resizable column width on tables (workflow rules, workflow templates, workflow zones, modules)
  - Toggle configuration for proxy credentials

**Fixed:**

- Product stability improvement

  - Avoid potential Nginx socket read timeout, and MetaDefender Core crash issue under certain memory shortage circumstances.
  - MetaDefender Core service crashed when trying to load an empty advanced configuration of engines.
  - Some minor bugs.
- Product UI fixes

  - Pagination is broken when the page number is too large.
  - Inconsistency multiscanning engine names on the module page.
  - User Management page didn't display any record.
  - Cannot traverse the list of files in a batch on the scan result page.
  - Incorrect results are returned when filtering the datetime on Statistic page.
  - Scan result report in PDF text alignment issue.
  - Cosmetic minor fixes.
- Incorrect callback messages mistakenly sent

  - "In-progress" scan result callback message was mistakenly sent to webhook server while the scan is not yet finished.
- Disk space availability check omitted before processing file request

  - MetaDefender Core is supposed to check for disk space availability on where the product temporary folder is configured to ensure it could store file and serve processing request.
- Kaspersky and NanoAV engine failed to load on MetaDefender Core Linux

  - The issue was due to incorrect handling within symlink in the engine package.
- Engine manual upload issue

  - Re-uploading the same engine package again immediately after a failed attemp on the same engine might cause issue on engine upload feature until MetaDefender Core service is restarted.
- Processing failure with the encrypted archive ALZ/EGG file

  - Failed to sanitize and re-compress those file types.
- Failed to remove AD/LDAP users

  - Hit error message "Item does not exist" on the UI when trying to remove AD/LDAP users.
- Temporary files and folders cleanup

  - Obsolete temporary files and folders were not cleaned up when user configured to set a new tempdirectory location.
  - Temporary files downloaded from a link were not cleaned up when disabling engines during scan.

## [Version v5.1.0](/docs/mdcore/release-notes/archived-release-notes#version-v510)

Release Date: 23 February 2022

**New features:**

- New statistics data for executives report

  - Average file size based on processed file types
  - Hash calucaltion time
  - Archive extraction time
  - Per AV engine processing time
  - Details: [Executives Report](/docs/mdcore/operating/dashboard#executives-report)
- Exclusion list for proxy server configuration

  - Define an exclusion list of destination addresses to bypass going through proxy server configured on MetaDefender Core. Applied to connections triggered by MetaDefender Core for following activities:

    - Callback (webhook)
    - Engine update
    - Scan by download link
    - Single Sign On integration (Fetch metadata from URL and login)
    - Remote PostgreSQL database connection
  - Details: [Exclusion List](/docs/mdcore/configuration/proxy-configuration#exclusion-list)
- Support Ubuntu 20.04

  - See the list of supported OS at [Recommended System Configuration](/docs/mdcore/installation/recommended-system-configuration)
- API key in the ignition file

  - Local admin user's API key could be now definied in the ignition file for automation enhancement.
  - Details: [Ignition file fields](/docs/mdcore/installation/deployment-automation-support#ignition-file-fields)
- Network drive and UNC path for update folder pickup

  - Allow users to define UNC path and network drive for update folder pickup setting.
  - Details: [Local folder update](/docs/mdcore/configuration/engines-update-configuration#local-folder-update)
- Timeout indication for Proactive DLP processing

  - Whenever Proactive DLP processing timed out, a clear and explicit timeout result is now used (instead of a generic failure reason).
- More logging comprehensive information for scanning activity

  - Absolute submitted file path for local scan feature.
  - Clear indication to distinguish between asynchronous and synchronous scan.
  - File path, file name, callback URL, sanitize URL, download-from URL for both asynchronous and synchronous scans.
- New simplified REST API to download output file after sanitized and Proactive DLP processed

  - Details: [GET - Download either sanitized files or DLP processed files](/docs/mdcore/metadefender-core#downloadfile)
- Clear indication for archive extraction in STDIN for post action

  - A new key of "extracted_files" is added into the STDIN for post action to indicate whether MetaDefender Core indeed extracted to child files from original file or not.
  - Details: [Post Actions](/docs/mdcore/configuration/external-scanners-and-post-actions#post-actions)
- Resizable table column on the UI

  - Applied to tables on the UI including processing history, quarantine, user management, engine list, quarantine etc.
- Security enhancements

  - UI setting input validation.

**Fixed:**

- Product stability improvement

  - Fixed minor bugs regarding to product stability.
- Samesite cookie modification with SAML based SSO

  - Value of samesite cookie was not updated correctly while using SSO with SAML integration.
- Wrong error code and error message with user role and directory removal

  - Wrongly returned 404 (item does not exist) instead of 400 when attempting to remove non-existed user role and directory.
- Custom data directory configuration

  - MetaDefender Core did not point to custom data directory after upgrading on CentOS / RHEL.
- YARA engine failure

  - YARA engine could become permanently failed after updating.
- Minor UI fixes

  - Cosmetic bug fixes

## [Version v5.0.1](/docs/mdcore/release-notes/archived-release-notes#version-v501)

Release Date: 28 December 2021

**New features:**

- New fields supported for PDF scan report

  - Receive data timestamp (indicating when a first byte was uploaded to MetaDefender Core from client)
  - Upload timestamp (indicating when entire upload was finished)
  - Upload time (indicating total time spent for upload)
- Product UX improvement

  - Under MetaDefender Core modules page: Different color (Orange) for engine and database when they are still being downloaded and deployed, not reached yet to final state. And some other minor UI changes.
- Archive compression engine auto enabled after product upgrade from v4 to v5

  - This engine is supposed to be inactive and permanently failed on MetaDefender Core v4, when upgrading to v5.0.1, now this engine will be auto re-enabled back without any user action required.
- Hot backup register API behavior updated

  - Not possible now to register a MetaDefender Core instance as backup when `active-deployment-id` header value equals to that own instance's deployment ID. Otherwise, expecting to hit an error: `{ "error": "active-deployment-id cannot be the same with this Core's deployment ID" }`
- Security hardening

  - 3rd party vulnerabilities check and remediation.

**Fixed:**

- Sanitization of files without extension on Windows

  - Applicable to Windows
  - When configured to keep both original file name and extension `${original.basename|long}.${original.extension}` , but original file name does not have extension: Previously MetaDefender Core auto changed the dot (.) between file name and extension (which is empty) to underscore (_). Now it is no longer the case, expecting to have only original file name.
- User agent "webscan" took no effect

  - Adding user agent "webscan" to any workflow should now force MetaDefender Core to display that workflow for selection on processing scan UI.
- Engine communication was not resumed correctly after engine timed out or crashed

  - When happened, causing not scanned / not available result on engine processing.
- Missing Proactive DLP failure details

  - Previously it just showed failed to process for Proactive DLP, now the failure reason should be exposed correctly (e.g. file size limit exceeded).
- Wrong archive handling details description

  - Mistakenly changed from "Corrupted Archive" to "Unsupported Archive"
- Wrong sanitization time when timed out

  - When sanitization timed out, cdr_time was mistakenly set to zero (0).
- Leftover Node related folder / key

  - On Windows (`Computer\HKEY` _ LOCAL _ MACHINE\SOFTWARE\OPSWAT\Metascan Node`` )
  - On Linux (`/etc/ometascan-node`)
  - They should be all cleaned up after upgrading to MetaDefender Core v5.
- Leftover archive engine temp folder

  - Only encountered when disabling archive extraction engine during extraction.
- Exporting scan history for all instances in shared database mode

  - Applicable to CSV / STIX export. The report only contained scan history records made on that current MetaDefender Core instance.
- UI bug fixes

  - Engine status color display on UI.
  - Processing scan highlighter.
  - Total number of processed objects displayed on Dashboard UI when being too big.
  - Error message on User Management disappeared when hitting Save changes button twice.
  - Unable to view sanitization details on UI when XFA form is sanitized.
  - MetaDefender Cloud API key was not redacted on Firefox.
  - Not displaying error message on UI when failing to import product configurations.
  - While file processing is happening, hitting details in DLP section was mistakenly redirected to AV section instead.
  - Error message was misleading when modifying a certificate being used by workflow rule or HTTPS setting.
  - Not able to continue testing LDAP configurations on UI after previous attempt was successful.

## [Version v5.0.0](/docs/mdcore/release-notes/archived-release-notes#version-v500)

Release Date: 30 November 2021

**New features:**

- Processing performance improvement

  - In typical use-cases, expecting better throughput on version 5 with architecture changes and processing flow optimization (30% - 200% depending on specific circumstances, configurations and data set)
- RedHat 8.x is supported (official)

  - Installation guide: [Red Hat Enterprise Linux 8.x package (.rpm)](/docs/mdcore/installation/standalone-mode#red-hat-enterprise-linux-8x-package-rpm)
- Security hardening

  - Eliminated critical and major vulnerabilities found in 3rd party libraries as well as the application itself.
- Hot backup mode supported for high availability

  - Supporting to setup backup MetaDefender Core instance(s) to run in parallel with your production (active) instance. Backup instance(s) will be allowed to use the same license key as your active one without actually being accumulated into the activation slots, and allowed to have all engines downloaded and deployed, configurations pre-setup, share the same database with active one (except of processing files).
  - Any of backup instance(s) should be ready to take over the active one anytime as a part of your disaster recovery plan to minimize the down time as much as possible.
  - More details: [Hot Swap Backup Configuration](/docs/mdcore/configuration/hot-backup-configuration)
- Health check API

  - Determining MetaDefender Core server's readiness to process upcoming files based on pre-defined criteria / policy that configurable by administrators. Allowing native support for a large pool of MetaDefender instances (load balancer in autoscaling groups. or liveness probe in Kubernetes, etc.)
  - More details: [Health Check API Configuration](/docs/mdcore/configuration/heath-check-api)
- Server active performance statistics API

  - Determining MetaDefender Core performance (processing time, throughput, queue time etc.) within specific time window to help you make better decision on which server is the best to route upcoming requests. Metrics that can be also collected and reported in external tools, not just via SIEM.
  - More details: [GET - Active performance](/docs/mdcore/metadefender-core#activeperformance)
- Bulk hash skipping modification API

  - No longer need to import one by one hash for either or both whitelisting and blacklisting. Allows you to import a list of hashes instead in a form of file.
  - More details: [POST - Add new hashes to 'skip by hash' list](/docs/mdcore/metadefender-core#configpostskiphash)
- Parallel engine deployment

  - Only applicable to bundled engines for now. Bundled engines will be deployed and initialized in parallel, to make MetaDefender Core get to ready state faster, and possibly reduce down time in dynamic environments (Containers, Cloud Autoscaling, etc.).
- More data points in log message for processing finished event

  - Applicable to log event generated upon a processing analysis task is finished. New information added:

    - Parent data ID
    - File size
    - File type description
    - Total processing time
- Estimated completion time on product upgrade

  - Upgrading time depends on various conditions including system specs itself, data size, characteristics etc. thus a roughly upgrade estimation time would be useful to set right expectation, especially to big size database that typically requires hours in upgrade. As a reminder, there is already an existing option on product to skip migrating processing data for upgrade when you do not really need it.
- Preferred encoding supported for sanitization and DLP processing

  - A new header `engines-metadata` for `POST /file` (asynchronous scan) and `POST /file/sync` (synchronous scan) to specify explicitly payload's preferred encoding (e.g. ISO-2022-JP) for sanitization and DLP processing. If not specified, then default encoding (UTF-8) will be applied.
  - More details: [POST - Analyze File (Asynchronous mode)](/docs/mdcore/metadefender-core#fileanalysispost)
- Proactive DLP integration enhanced

  - Helped expose new Proactive DLP features on MetaDefender Core workflow rules, and make the product workflow flexible for changes and improvements.
  - More details: [Proactive DLP release notes](/docs/mdcore/release-notes/proactive-dlp-release-notes)
- SHA256 checksum of objects in Deep CDR analysis result details displayed

  - SHA256 checksum calculated on every sanitized objects processed by Deep CDR is now displayed on MetaDefender Core's processing result UI.
- Handle unsupported file type for archive compression

  - Under MetaDefender Core workflow rule - Archive tab. A new setting option where you can select to fail the scan with unsupported file type for archive compression / sanitization.
- Enhanced logic to help avoid MetaDefender Core initialization failed due to database failure

  - Possibly encountered in container based environment with remote PostgreSQL database in certain circumstances.
- A new option for unsupported compression method handling

  - Under Archive handling settings in MetaDefender Core workflow, a new option to allow failing archive extraction task for unsupported compression method.

**Fixed:**

- Advanced Deep CDR settings were reverted under certain circumstances

  - Only encountered when using workflow rule based on custom workflow template (this issue had happened since MetaDefender Core version 4.20.0) Changes made on Deep CDR advanced settings were reverted after MetaDefender Core service restarted or Deep CDR engine re-enabled.
- Vulnerability processing result was wrong in PDF scan report

  - When actual result was a potentially vulnerable file, but reported as no vulnerability found mistakenly in the PDF report.
- Fix memleak when handling Proactive DLP errors

  - Possibly happened when Proactive DLP encountered errors while processing files.
- Reinstalling MetaDefender Core could be failed

  - Uninstalling the product and then reinstalling back on the same machine but with different deployment ID.

## [Version v4.21.2](/docs/mdcore/release-notes/archived-release-notes#version-v4212)

Release Date: 30 August 2021

**New features:**

- Mutual authentication for secured webhook (callback) mode

  - An additional security mode for callback HTTPS to authenticate requests indeed sent by MetaDefender Core, and help against man-in-the-middle attack. Details could be found at: [Webhook Authentication](/docs/mdcore/operating/library-management#webhook-authentication)
- Webhook (callback) for sanitized file download (BETA feature - not recommend to be used on production)

  - When registered by client, whenever a sanitized file is produced and ready, a new callback with sanitized file content will be sent back to client.
- Configurable relevant session cookie attribute aided in CSRF attack prevention

  - "*SameSite*" attribute on the session cookie "*session_id_ometascan*" with supported values: Lax (default), Strict, None (i.e. empty) to be configurable. Supported to configure via either administrative REST API, or ignition file. Details could be found at: [Configure session cookie attribute](/docs/mdcore/metadefender-core#configputsessioncookie)
- Support SSL connection between MetaDefender Core and PostgreSQL

  - Along with a setup guidance for SSL database connection. Details could be found at: [SSL Connection for bundled PostgreSQL](/docs/mdcore/configuration/ssl-connection-for-postgresql-communication)
- SQL Injection prevention check and ensurement

  - On all supported REST APIs
- Adaptive mode when moving AD / LDAP users to other OU (Organization Unit)

  - Allowed users to change DN information in AD / LDAP directories
- Logging details enhancement on Webhook (callback) failures

  - Enhanced on generic failure (error code = 444) to expose more details in WARNING log level. Details could be found at: [Webhook error message description](/docs/mdcore/metadefender-core#webhookstatus)
- Logging details enhancement when failing to open PostgreSQL service

  - In a circumstance of when failing to open PostgreSQL configuration file.
- Separate JSON configuration file now collected in the support package

  - For easier analysis and import back into MetaDefender Core when needed.
- Preinstall Deep CDR and Proactive DLP dependencies in MetaDefender Core docker image (libgomp, libgdiplus, mscorefonts)

**Fixed:**

- MetaDefender Core upgrade failures

  - Handled duplicated sanitization detail records
  - Handled empty key in registry when installing by commandline
  - Handled invalid value of type in ignition file
  - Handled invalid Unicode characters
- Initialization failure of Threat Intelligence engine on Ubuntu

  - Updated openssl linkage to address the issue
- Improper value type of "*archive_handling_details*" in JSON response

  - In a case of processing password-protected archive file, the value was set incorrectly, it should always be a map data type (not string).
- Lacked of compression failure detail (archive sanitization)

  - When MetaDefender Core fails to re-construct email file (.eml) in archive sanitization.
- Incorrect error message when recovering user password

  - In a case of the email server address configuration is not setup correctly for password recovery.
- Out of bound value of session timeout handling

  - Setting value on session timemout to 1 million or above resulted in authentication failure.
- Update hang up on engine in certain circumstance

  - Engine remained in "staging" status indefinitely if the configuration validation failed for engine.
- Missing Proactive DLP engine processing result

  - Making sure all engine results return correctly in both failure and success circumstance.
- Incorrect scan result in PDF report

  - In a case of using skip scan on engine setting
- License auto deactivation did not work properly in docker container deployment

  - When stopping docker container, the docker automation script in the toolkit (entrypoint.sh) did not handle license deactivation properly.
- Retry mechanism of Webhook (callback) did not work as expected in special circumstance

  - When MetaDefender Core service is restarted while operating, the callback was not sent as designated in callback retry configuration.
- Intermediate certificate was stripped out

  - HTTPS configured with full chain certificate scenario, the intermediate certificate could be stripped out before importing into the product

## [Version v4.21.1](/docs/mdcore/release-notes/archived-release-notes#version-v4211)

Release Date: 13 July 2021

**New features:**

- A new setting to exclude password-protected documents from being blacklisted due to unsupported sanitization

  - The password-protected document is not supported for sanitization and possibly blacklisted when enabling "BLACKLIST UNSUPPORTED FILE TYPE" option under Deep CDR workflow rule.
  - Now you can exclude it via a new setting. By default, the new setting is not enabled to keep backward compatibility.
- Upgrade 3rd party libraries for security enhancement

  - (Built-in) PostgreSQL from 12.6 to 12.7
  - NGINX web server from 1.18.0 to 1.20.1
  - Remove outdated jsPDF 1.5.3
- A new CLI tool to analyze and deeply vacuum database

  - PostgreSQL database could be more bulky over time with high scanning traffic. The tool which is bundled with MetaDefender Core installation is to analyze database and vacuum database effectively, and simplify IT administration. Even though it is not required to stop MetaDefender Core service while running, but still recommended to run the tool when the scanning service is at rest, or not in peak hours to avoid scanning performance impact.
  - Details: [Database Maintenance | MetaDefender Core 4.19.0 or above](/docs/mdcore/operating/database-maintenance---metadefender-core-4-19-0-or-above)
- More data points collected for the support package

  - Including size of objects from MetaDefender Core database to help us determine better the characteristics of the data for troubleshooting purpose.
- Other minor changes

  - Enhanced integration logic on engine configuration handling to avoid potential configuration corruption.
  - Enhanced installation script in Linux-based installer to avoid misleading warning.
  - When the Vulnerability assessment module is not enabled, the relevant vulnerability result on the MetaDefender Core scan result UI will be now as "not configured" (instead of no vulnerability found).

**Fixed:**

- OPSWAT Central Management integration issues

  - Workflow rule list order was different between MetaDefender Core and OPSWAT Central Management UI.
  - Last configuration import timestamp was invalid.
- Deep CDR's advanced settings was not applied

  - Occurred when creating a new workflow rule on MetaDefender Core.
- Negative duration processing time

  - Under certain corner circumstances, the wait_time and queue_ time in JSON scan result could be mistakenly calculated.
- User on old database was left out during the MetaDefender Core upgrade

  - When upgrading MetaDefender Core with standalone database mode to shared mode.
- Leftover files when canceling batch

  - Occurred when handling archive files.

## [Version v4.21.0](/docs/mdcore/release-notes/archived-release-notes#version-v4210)

Release Date: 14 June 2021

**New features:**

- Docker container support

  - A new deployment support for MetaDefender Core on docker container environment.
  - Supporting for Linux based environment (CentOS / RedHat, Ubuntu / Debian). Windows based more to come later.
  - Comes with 2 options: (1) Docker images hosted by OPSWAT (2) A build kit with docker file and scripts to use with your own docker image.
- Synchronous scan

  - One more new scan API interface for Core with a sync mode (blocking mode). That helps ease integration hassles on some of your web applications.
  - The connection of file submission request must be held by client side until MetaDefender Core returns processing result of individual scan when finished, or return data ID associated to that request if timed out (which is configurable).
- Scan performance improvement

  - Optimized for resource conflict handling, even better under high scan rate with many AV engines.
- Azure AD supported with OIDC

  - Continuous Sigle-Sign-On (SSO) improvement with OIDC supported for Azure AD.
- New scan result "Potential Unwanted" for PUA/PUP

  - Applicable to AV engine scan result.
- Crash dump auto collected for support package

  - Only if crash dump is available for MetaDefender Core related processes.
- Statistics page enhancement

  - New section"Custom Regular Expression" applicable to Proactive DLP.
- Proactive DLP settings limit range extended

  - Extended maximum character length limitation of Proactive DLP settings under workflow rule.
- Secure the integration with Central Management product

  - The integration credentials meet complexity requirement.
- Retain password protection for RAR file sanitization

  - A new option for RAR file could be found under CDR tab in workflow rule, applicable to password protection for archive sanitization.
- More data points for /stat/nodes API endpoint

  - Including:

    - Total disk space
    - Total scan queue
    - Service uptime
- Upgrade 3rd party libraries

  - Built-in PostgreSQL 12.3 to 12.6
  - Lodash 4.17.10 to 4.17.21
- Product upgrade process enhancement

  - For back-end processing efficiency when upgrading MetaDefender Core from standalone to shared DB mode.

**Fixed:**

- Product upgrade issues

  - Fixed some failures when upgrading the product with malform data in database.
- Default workflow template mistakenly modified with Central Management integration

  - On Central Management, changing any setting in a new workflow rule unexpectedly resulted in changing associated workflow template.
- Wrong data in PDF report for processing result

  - Under certain circumstances, some information in PDF report could be invalid / misleading.
- Incorrect blocked_reason in tombstone file

  - When processing an archive file contains at least one child file returning Sanitization Timed Out / Sanitization Failed.
- Minor fixes

  - Some other minor bug fixes.

## [Version v4.20.1](/docs/mdcore/release-notes/archived-release-notes#version-v4201)

Release Date: 31 Mar 2021

**New features:**

- MetaDefender Core's PostgreSQL database admin credentials management

  - Supported via both web management UI and CLI tool to change Core's PostgreSQL database information.
  - The CLI tool could be used for older PostgreSQL based Core versions as well (4.19.0 to 4.20.0)
- MetaDefender Core upgrade mechanism changes

  - Ensure the old product database is always kept regardless of upgrade result, and easier to rollback when needed.

**Fixed:**

- MetaDefender Core upgrade failures

  - Addressed various upgrade failures occurred with Core version 4.20.0
- Scan stuck until timeout hit under certain circumstances

  - Possibly happened with Core 4.20.0 when the data retention is enabled for sanitized / DLP processed file, and only when the system keeps processing the same file over again while running the data retention.
  - This issue could only be applicable when CDR and(or) DLP feature is used.
- MetaDefender Core service failed to start

  - Encountered when the Core's PostgreSQL database admin password contains special characters */-+"?<>:{}*&^%$#@!~`';.,\
- Invalid batch signature

  - Due to a bug in 3rd party library, batch signature could be invalid.
- MetaDefender Core service issue on docker

  - Only applicable when replacing systemctl to start Core service within docker container.
- MetaDefender Core service failed to start automatically after reboot

  - Thus sometimes required manual start action.
- Minor fixes

  - Some other minor bug fixes.

## [Version v4.20.0](/docs/mdcore/release-notes/archived-release-notes#version-v4200)

Release Date: 08 Feb 2021

**New features:**

- Centralized (or shared) database mode

  - A complete new database design to support to use single PostgreSQL database shared among all connected MetaDefender Core applications. That helps auto-sync all product configurations (except Single-Sign-On that requires unique settings for each Core), processing histories, live/on-going scan result query, audit, statistics data. All product functionalities are updated to support both standalone and shared database deployment model.
  - Database migration (configurations and processing history) is also supported for older Core versions upgrade.
- Workflow based for Deep CDR advanced configurations

  - Deep CDR advanced configurations now could be defined differently for each workflow rule on MetaDefender Core.
- HEAD request is now optional for the scan-from-link feature

  - MetaDefender Core no longer requires to send HEAD request to check for metadata of file before downloading with scan-from-link feature. Some storage web services such as AWS S3 with signed URL, it does not support unauthorized HEAD request.
  - When HEAD request is omitted, expecting no support for download progress status and insufficient disk space pre-checking.

**Fixed:**

- Statistics data failed to migrate after Core ugprade

  - Upgrading from old Core version 4.17.3 or below failed at statistics data migration.
- Processed file content duplicated

  - The issue could sometimes occur when we have two or more same file to be processed.
- Minor UI fixes

  - Tooltip for processed file cleanup explanation

## [Version v4.19.2](/docs/mdcore/release-notes/archived-release-notes#version-v4192)

Release Date: 07 Dec 2020

**New features:**

- Non-persistent scan mode

  - A stateless scanning solution to improve performance. When triggered, MetaDefender Core will not write any scan result into its database.
  - Note: Webhook scanning fashion must be used from client side to retrieve scan result back from MetaDefender Core.
- Interactive engine removal on UI

  - Any engine module could be removed on the management console (instead of using CLI tool). No service restart is required, no command to run.
- New Identity Provideres (IDP) supported and verified for Single Sign On (SSO)

  - Microsoft Azure AD Connect
  - Ping Identity
  - Idaptive
  - Xecurity
  - OneLogin
- Data retention supported for statistics

  - Data stored in statistics warehouse could be configured to clean up.
- Minor supports / changes

  - File type processing time included in final JSON response
  - DLP image cropping feature support (Only available starting Proactive DLP version 2.6.0)
  - Remove BETA from Statistics page
  - UI clarity with scan result page
  - Unicode characters better support for DB migration (product upgrade)
  - Better performance for statistics page
  - Support package to include engine logs (only available when engines start writing it)
  - Workflow rule setting values validation
  - Case sensitive support in header "filepath" for POST /file request

**Fixed:**

- Performance degradation issue mitigation

  - Archive scanning performance
  - Hash lookup slow response
  - Batch close request potential bottleneck
  - Database dynamic query optimization
- Memory leak

  - Both could happen on ometascan and ometascan-node processes under certain circumstances.
- Incompatible Nginx cipher algorithm

  - Default acceptance cipher algorithm list modified to be less strict.
- Missing vulnerability detailed result

  - Vulnerability detailed result could be missing from final scan report in some cases.
- Very high CPU continuous usuage occupied by node process

  - Might happen when extraction failed and then affecting to the completion of hash calculation process, result in high CPU usuage continously.
- Potential service crash

  - While cancelling archive scanning
  - Engine package download
- Issues with scan result report

  - Wrong AV and Deep CDR result
  - Missing Proactive DLP section
  - User right issue (i.e. who is allowed to download the scan report)
- Proactive DLP setting issue with unicode characters

  - The unicode setting value could be malformed after Core / Proactive DLP upgrade
- Other product functional issues

  - Blocked files was not stored in quarantine with local file path scan, or scan from link fashion.
  - Wrong data calculation on statistics page

## [Version v4.19.1](/docs/mdcore/release-notes/archived-release-notes#version-v4191)

Release Date: 21 Oct 2020

**New features:**

- Processing file with input as a download link

  - Supporting users to process file by just specifying a direct download link, which means no required for the payload in HTTP(S) request body.
- Tombstone file supported for archive sanitization

  - Whenever any child file in original archive file are not sanitized successfully, the product supports to append tombstone file into sanitized archive file to indicate which original child file(s) are removed from sanitized archive output file with details.
- No hash calculation configurable setting

  - Support an option to skip hash calculation on every processing file (using dummy hash values instead) regardless it is individual file or a part of archive.
  - Expecting to be used against giant file processing to significant reduce overall processing time.
- Nginx web server component ugprade

  - Nginx web server has been upgraded to its latest stable version 1.18.0.
- Comprehensive individual scan report in PDF

  - Support users to download a detailed scan report in PDF format on any processed individual file.
- PostgreSQL performance improvement on scan result query

  - Improved scan result query against PostgreSQL server in certain circumstance (query by hash value).
  - Enhanced mechanism in selecting relevant database connections for serving data related requests.
- PostgreSQL connections configurable setting is supported (for scaling up)

  - A new setting called " db_connection" to define a maximum number of concurrent connections allows MetaDefender Core to open and work with PostgreSQL database server.
- UNC path supported for local file scan

  - Local file scan feature now accepts UNC path specified on desired workflow rule's setting
- New processing time in JSON scan report for each stage in workflow processing

  - The JSON response for scan result will include processing time on each major workflow processing step.
- New workflow rule configuration supported for file-based vulnerability assessment

  - File-based vulnerability assessment will be supported to be managed under each workflow rule, comes with new configurable settings.
- New workflow rule configuration supported for file type analysis

  - File type analysis will be supported to be managed under each workflow rule, comes with new configurable settings.
- New configuration to skip further processing (and block) in certain malware scan results

  - Support an option to skip any further processing (e.g. sanitization) EXCEPT post action run (if configured) on every processing file if the AV scan engines' final result matched to any supported and checked scan result in the list.
- New configuration to skip further processing (and block) if file type detection failed

  - Enabling it to let MetaDefender Core skip further processing if actual file type could not be detected by file type engine for following reasons:

    - File type engine process crashed
    - Waiting tasks in queue aborted when file type engine process terminated
    - File type analysis task timed out
    - User cancelled entire processing while analyzing file type
  - When triggered, the final scan verdict will be “Not scanned”.
- Enhance existing configuration to skip further processing (and block) if archive engine is not available

  - Support an option to skip any further processing (e.g. sanitization) and fail any processing archive file if archive engine was not available for any reasons (disabled, crashed, timed out…) before trying to extract that archive file. The final processing verdict will be “Failed”.
- Proper blocked reason in JSON scan result when sanitization failed or timed out

  - With Deep CDR's workflow setting "Block files if sanitization fails or times out" is enabled, when the sanitization result meets those conditions, then now the "blocked_reason" key value would represent actual sanitization failure result (instead of other scan results such as No Threat Detected which could cause misleading to client integration).
- Override whitelist certain file types in archive file scanning

  - When triggered, the whitelist setting will be ignored if pre-configured file types belong to archive file processing.
- Proactive DLP default threshold value changed to high

  - The previous threshold value was low under Proactive DLP workflow rule settings. For those customers already tweaked this setting value, this change will not revert their pre-configured setting.
  - This change is to address false positive concern on DLP processing against files inside document by default.
- Email server configuration now accepts no authentication option

  - That helps integrate with external email server without authentication required.
- MetaDefender Core could be activated via offline mode without any network card enabled

  - In an isolated environment, we understand that your machine's network card could be disabled completely for security reasons. Hence now MetaDefender Core could be activated under that circumstance with offline yml file upload as usual.
- Log enhancement on webhook callback failure on HTTPS mode

  - When the callback failed to send to client side over HTTPS, the status code will be 444, and now the product log is enhanced to reveal more why the secure connection was not made successfully.
- Improved search performance on MetaDefender Core processing history page

  - Earlier users could observe the slowness in search by username while MetaDefender Core was running data retention.

**Fixed:**

- Advanced engine settings mistakenly reset back to default values

  - The issue could encounter in following circumstances:

    - Upgrading MetaDefender Core
    - Engine reloaded (disable and enable back)
    - Engine updated (and then reloaded)
- Ignition file with configuration file location import issue

  - Using ignition file for configuration file location import was not working.
- Sanitized archive compression failed with same password retainment

  - Archive sanitization could be failed with same password retain feature enabled under Deep CDR workflow settings.
- Potential memory leak issue

  - Leaking on Node component (ometascan-node) while updating engines online, or via Central Management.
- Input validation

  - Enhanced and fixes bad input validation for data queries.
- Service crashed in certain circumstance

  - Core component could be crashed when stopping the service immediately upon the product service start command.
- Update from folder feature issue

  - Update from folder trigger failed to skip in what pre-configured for update pause time frame.
- Failed to download big sanitized files

  - Failure could be exposed (failed to download) against big sanitized files in GB in size.
- Product database migration issue

  - Failed for statistics data migration.
- Proactive DLP regex validation failed for Unicode characters

  - Fixed to support encoded Unicode characters in Proactive DLP's regex (Proactive DLP version 2.5.0 or above is required)
- Sanitized archive file contained blocked watermarked file

  - The issue could only happen when Proactive DLP was used with watermarking triggered on child files inside archive sanitization.

## [Version v4.19.0](/docs/mdcore/release-notes/archived-release-notes#version-v4190)

Release Date: 27 Aug 2020

**New features:**

- New Database Management System (PostgreSQL) to replace SQLite

  - PosgreSQL is now MetaDefender Core's new database management system to replace its predecessor SQLite. That expects to step by step help the product easily scale out, network based database support, gain better performance, migrate high load bottleneck and native high availability. MetaDefender Core supports users to create a local PostgreSQL server running in the box, or allow leveraging a pre-installed remote PostgreSQL server.
  - Data migration auto runs in background upon product uprade.
  - For large database migration, MetaDefender Core comes with a web-based data migration to walk users through quick steps to move all your SQLite data to PostgreSQL at ease.
- FIPS-140 security compliant

  - We are now FIPS-140 compliant with a new support for RSA186-4 on OpenSSL
- Native proxy management with authentication support

  - MetaDefender Core now will allow users to control proxy settings for product (instead of using system configuration), and also support authentication for proxy which is not possible on older Core versions.
  - That comes with a UI configuration support on MetaDefender Core management console.
- Harden Nginx web server settings for security

  - Secure MetaDefender Core web server even more based on nginx vendor guideline to protect your MetaDefender server from being vulnerable (i.e. cross site scripting, MIME sniffing, TLSver 1.1 or below forbidden)
  - Still we keep all supported functionalities working as expected.
- Nginx web server statistics (on web server report)

  - Support to enable better statistics for the HTTP Server for web server healthcheck and debugging.
- Origin client source address retrieval when running via load balancer

  - MetaDefender Core now will be able to retrieve your origin client source address even when the client communicates over a load balancer.
- Enhanced search for processing history page

  - Searching by attributes represented via corrensponding column on the list.
- Enhanced user experience on statistics page

  - Instant statistics processing data calculated and visualized on UI
- Logic improvement to handle better against sanitization timed out

  - New logic implemented on MetaDefender Core to offload concurrent tasks on Deep CDR engine, and to reduce sanitization timed out as a result.
- Enhanced log messages

  - Log events enhanced with more sufficient and clear information, easier for traceability while troubleshooting.
- Pre-check mode for file submission

  - Refuse file upload immediately when MetaDefender Core does not have enough disk space to handle, expecting to hit error 400. This is to avoid wasting upload time on big files.
- Sanitized file information appended into JSON scan result

  - Including sanitized file size and its SHA-256 hash value.
- Blacklist overidden on nested files within archive

  - New configurable setting to allow overridening blacklist enablement on nested files within an archive.
- New engine sweeper tool bundled into the product

  - New engine sweeper troubleshooting tool tailored for PostgreSQL, and now it is bundled into MetaDefender Core product (not a separate download tool).

**Fixed:**

- Setting inputs validation

  - Threat detection threshold, wizard password and SSO profile settings affected.
- Batch signature sometimes contained redundant characters

  - That could make signature becomes invalid.
- Processing time of nested files in archive not calculated correctly

  - Processing time of nested files could be very big due to incorrect caculation (but actually they are processed much faster).
- Statistics page to support multiple users simultaneously

  - The statistics UI now could handle multiple users query at the same time.
- Proactive DLP timeout setting mistakenly reset upon engine restart

  - The setting was reset back to default value (3 minutes).

## [Version v4.18.0](/docs/mdcore/release-notes/archived-release-notes#version-v4180)

Release Date: 26 May 2020

**New features:**

- Single Sign On (SSO) Authentication

  - Additional to already-supported various authentication models (Local, Active Directory, LDAP), now MetaDefender Core also supports authentication using SSO with widen integration coverage for most of Identity Providers (IDP) via SAML 2.0 and OpenID Connect 1.0 standard support.
- Brand New MetaDefender Core API Guide (Sample Codes Available)

  - Brand new design and standardized API documentation (following OpenAPI V3 specification), auto-generated sample codes on various programming languages supported helps your API integration even easier.
- Database Defragmentation and Optimization

  - When your scan database grows big, it might cause performance degradation (e.g. timeout on client requests). Now MetaDefender Core administrators can be notified on the UI (also warning logs), and you are supported to perform database defragmentation and optimization including multiple stages to vacuum and defrag your database without loss of actual scan data.
  - As a result, your database file size could be reduced which helps boost processing performance tremendously over usage time.
- Comprehensive Statistics On Processing Data

  - Featured in an interactive UI help you gain deeper insights on your processing filtered by every workflow rule, breaking down into each file type. Last but not least, you are also supported to select time range to calculate statistics data.
- Data Reporting (Business Intelligence)

  - When enabled, MetaDefender Core will auto-sync your historic processing data to OPSWAT dedicated servers. That helps us gain more visibility on your processing load and how our product is being used, and thus we could improve our product to accommodate your use-case better. You are supported to customize which piece of information should be shared with OPSWAT, and when to share.
  - By default, this feature is disabled to respect your privacy rights and save performance impact.
- Webhook Continuous Improvement

  - New setting mode to control callback timeout and retry (configurable via REST API)
  - Stability improvement to avoid being stuck on callback and crashing on Node service
- High Load Processing Improvement

  - When running under high load, file type usually returns "Not Available" caused by various reasons. Product logic enhanced to elaborate causes, and improved stability on the product.
  - We keep working on this matter to ensure our customers have the most stable product running under high load as much as possible.
- Configurable Behavior On Archive Extraction Failure

  - Configurable settings on workflow rule to let you tweak and decide MetaDefender Core final scan verdict when a processing archive file failed to extract for some reasons.
  - The default selection on each designated extraction failure reasons (invalid file structure, extracted partially,...) will be different on each workflow rule depending on use-case characteristics. Please make sure you are aware of the new settings and adjust them accordingly tailored to your security demand.
- Archive Extraction Failure Exposure

  - Archive extraction failure reasons exposed to both REST API response and UI.
- Encryption on Archive & Document Sanitized Files

  - Help retain password protection on supported archive and document files (.zip, .7z, .pdf, MS Offices) upon sanitized successfully.
- Sanitization Forensic Details Enhancement

  - When sanitized successfully, an even more comprehensive forensic available on both UI and REST API level letting you know all processed object details (e.g. what exact hyperlink was sanitized).
- Processing File Information Enhancement (File Type Category)

  - File type category is now available on REST API response along with other already-supported file information.
- MetaDefender Core Log Rotation Experience Improvement

  - This feature is now enabled by default applicable to both upgrade and fresh install scenario.
- Workflow Rule For MetaDefender For Secure Storage

  - With the best practice to serve MetaDefender For Secure Storage use-case, we have a new dedicated workflow rule with designated configurations.
- Archive Processing Result Retrieval API Enhancement

  - Applicable to pagination fashion polling *GET /stat/log/scan?first={start_item}&size={number_of_items_next}* , now the action ran information available in JSON response
- FIPS Object Module 2.0 Bundled

  - Operating product in FIPS mode enabled on Operating System

**Fixed:**

- File Scanning Process Stuck

  - When the custom engines stopped its process for reasons (updating while scanning / crashed), the running scans on Core could not be finished and stayed at 95% forever.
- MetaDefender Core Service Crashed (Webhook Mode)

  - When using webhook mode, and callback can't be sent back to client, the MetaDefender Core service could be crashed.
- Memory Leak While Updating Engines Automatically

  - The memory could be leaked on *ometascan-node* process while updating engines in online mode.
- Scan Details Missing From Recursive Scan Results

  - While fetching scan results on all nested files in big archive file *GET /archive/{data_id}* the "scan_details" field from the top-level root archive was empty.
- Input Field Overflow On Management Console UI

  - Preventing invalid values putting in UI configuration controls (Deep CDR, Archive)
- Archive Timeout File Skipped For Scanning

  - None of AV engines actually scanned archive file when archive timeout occurred

## [Version v4.17.3](/docs/mdcore/release-notes/archived-release-notes#version-v4173)

Release Date: 06 Apr 2020

**New features:**

- Configurable setting to run database optimization

  - Database optimization has been introduced since Core 4.17.0 to help run database queries faster. The downside is while running (for a few seconds), Core queries hold up causing possibly timeout on client side.
  - This new setting allows users setting specific time to run database optimization task (to avoid peak hours), or just disable to prevent this task from running (to avoid performance degradation while running). Learn more how to configure: [Startup Core Configuration](/docs/mdcore/configuration/metadefender-configuration#startup-core-configuration))
- Scan database rollback mechanism

  - In some circumstances (e.g. Core crashes, out of disk/memory etc.), the atomicity of product database could be compromised causing inconsistent processing scan history returned. Rollback mechanism helps retain that atomicity of database.
- Logging improvement with configurable settings

  - Log rotation for Core, Node, Nginx web server logs (Configurable settings supported).
  - More comprehensive support package (to include engine and database info, Nginx web server info).
  - More informative log message on sanitization related tasks.
  - Sensitive info redacted (on debug level logging mode).
  - Performance impacted warning on both MetaDefender Core GUI and logs when the scan database (ometascan.db.sqlite) starts growing up big (>10 GB).
- Webhook mode continuous refinement

  - Retry to send scan results to client upon network interim disconnected.
  - Resend file scan results to client after Core service restarted.
- New download mechanism for Processing History on MetaDefender Core management console

  - Support IE / Edge web browsers to download processing history report.
- MetaDefender Drive use-case better support when engine packages corrupted

  - Support to re-new engine packages to re-download engine packages again when corrupted (due to upon unexpected reboot).
- Central Management v7 support to revert download source when unhooked

  - Respect skipped scan settings (Whitelist / Blacklist) to keep backward compatibility, and also save Core resource for processing files as well.
- RoleIDs JSON field validated when creating / modifying user

  - Effective to *POST*_/admin/user_ and *POST /user* endpoint REST APIs. Role ID value must be an array of strings according to current user guide.
- Account name value validated on Core wizard setup

  - Effective to "Admin User Setup" screen during wizard setup, "Account name" validated against special characters (e.g. @ & )
- Better support for sanitized file download when under load

  - When under load and certain circumstance with system write failed, the sanitized download on the same file might return 404 HTTP response (not found) to client. Enhanced our Core caching mechanism to ensure next time sanitization on the same file will not rely on the previous failed time.
- Minor UI changes

  - Hide "Edit Workflow" button in "Workflow Templates Management" screen
  - Remove space between date and time in "Definition date" field on "Modules" screen

**Fixed:**

- Data tunnel between Node and engines could be lost under high load

  - When occurred, expecting to see " process communication timed out" message repeatedly in Node log, and none of engines could be able to scan files.
- Node crashed when swapping engines during update

  - Node could be crashed under certain circumstances, applied to swapping engine instances during update.
- File processing was stuck at 95%

  - Encountered when custom engine stopped its process, all of running tasks on that engine becomes stuck, or when ClamAV engine can't return consistent scan result during its engine update.
- Overflow issue with unexpected inputs

  - Overflow value issue could occur within product causing unexpected behavior or result.
- Unexpected result with non-ASCII password protected document scanning

  - When occurred, document file could not be sanitized properly.
- Proactive DLP displayed wrong result within archive scanning

  - When occurred, Proactive DLP engine could return misleading result (Not scanned) while archive file processing result is "Sensitive Data Found".
- Session expired on IE / Edge web browser

  - When session cleared out, authenticated users could be logged out repeatedly due to session expired error on MetaDefender Core management console.

## [Version v4.17.2](/docs/mdcore/release-notes/archived-release-notes#version-v4172)

Release Date: 03 Mar 2020

**New features:**

- Quarantine cleanup task no longer blocks Core service starting procedure
- Empty file submission is no longer be blocked at REST API level

  - Retain same behavior on Core 4.16.3 or older, to support back some corner use-cases from MD Kiosk and ICAP
- Custom engine initialization enhancement

  - Increased timeout to 10 minutes to support engine deployment on under-specs hardware (formerly 1 minute)
- Processing history report enhancement

  - Added "username" column to the processing history export from MD Core
- Validation mechanism on file scan and batch init REST API changed

  - When using via REST API, no longer validate session cookie, only API key header is validated when exists (same behavior on Core 4.16.3 or older)
- Configurable Proactive DLP timeout is supported

  - Support to adjust timeout for Proactive DLP handling (formerly fixed on 3 minutes)
- Respecting whitelist and blacklist configurations

  - Respect skipped scan settings (Whitelist / Blacklist) to keep backward compatibility, and also save Core resource for processing files as well.
- Response for POST /login no longer returns cookie back to client

  - When using via REST API, by default the response for POST /login no longer returns cookie back to client (same behavior on Core 4.16.3 or older, to avoid breaking F5 LTM scenario with cookie header is auto added)
- Removing failed dummy scan results on Core processing history UI due to upload failure

  - When file upload is failed for some reasons (e.g. network corrupted) between clients and MD Core, dummy record results are still available and displayed on Core processing history UI, but actually MD Core never processed those files, and client never got results from MD Core on those files. Those dummy records will be removed since this version to avoid misleading.

**Fixed:**

- Deadlock could possibly happen when engine update task is timed out

  - When encountered, all files happens in "Failed" result with "Not available" result for file type analysis after timeout hit (~ 70 seconds), and only Node service relaunched can bring the scanning be operational back.
- Node service could be crashed when archive engine crashed

  - When archive engine crashed for some reasons, Node service could be crashed as well (but not happened all the time)
- Core and Node service could be crashed when under high load

  - Core and Node service could be crashed when under high load
- Archive file extraction when timed out, or failed to extract, the original archive itself could not be scanned by AV engines

  - When archive extraction hits timeout or failed to extract, the original archive itself could not be scanned by AV engines
- Core could return 404 not found HTTP(S) response to client for sanitized file download API request

  - When processing the same file many times on Core, it could return 404 not found HTTP(S) response to client (e.g. MD Email) due to file sync issue between Core and Node
- Memory leak issue on Core process

  - The process ometascan could be leaked on memory with auto update mode enabled and Proactive DLP engine is enabled
- Anonymous user can't submit file scan to MD Core web scan UI

  - When not logged in, anonymous user can't submit file scan to MD Core web scan UI (error: Invalid session ID given)
- Core service can't restart due to configurations corrupted while running Proactive DLP engine

  - Core service can't restart due to configurations corrupted while running Proactive DLP engine
- Document files inside sanitized password protected archive file could not be sanitized

  - When document file is also treated as an archive file, there was a bug on archive compression level calculation to prevent document files not being sanitized inside original archive file
- Timeout on hash calculation task resulted as Blocked regardless of "override scan results classified as allowed" setting

  - When this task timed out, regardless what users set on "override scan results classified as allowed" setting, the final verdict were "Blocked"
- Webhook continuous fixes and updates

  - Duplicated callbacks returned to client
  - Support retry mode for sending callback to client (when client is temporarily unresponsive etc.)
  - Enhance validation callbackurl header against IP version 6 and domain format
- Minor UI fixes

  - Added margin to bottom edge of scan result UI
  - Name of rights under user management did not match to Inventory

## [Version v4.17.1](/docs/mdcore/release-notes/archived-release-notes#version-v4171)

Release Date: 06 Jan 2020

**New features:**

- Archive extraction details

  - Available on both scan result UI and
- Advanced engine configurations enhancement

  - UI interactive and schema based for advanced engine settings
- Proactive DLP engine integration enhancement
- MetaDefender Cloud integration enhancement

  - MetaDefender Cloud API version 4 upgraded
- Engine integration enhancement to avoid product crash
- User validation update for file and batch processing

  - File scan and batch init endpoint API is now validated on API key input when that key information is available.
- More ready for adding password back to sanitized archive and document files
- Minor UI update

**Fixed:**

- Core could become unavailable to clients when under high load

  - Data communication channel between Core and Node service could be broken when under high load
- Processing giant files (> 50 GB) could be stuck at hash calculation

  - Hash calculation with pre-set timeout value (10 minutes) could be exceeded when processing giant files (> 50 GB) and then stuck at 5% forever
- Scan could be failed with "not available" result for File type analysis when under certain circumstances
- Memory leak issue on Core process
- Temporary files not cleaned up when archive extraction timed out
- Webhook continuous fixes and updates

  - Redundant warning log messages populated even when not using webhook mode
  - Core could be crashed itself when trying to close a not-found bath with callback
  - Callback sent to client with wrong status when Core is restarted
- Visibility level smaller than full details might break batch result display
- Minor UI fixes

  - The field "File Password" on the file processing UI not cleared up after empty file selected

## [Version v4.17.0.1](/docs/mdcore/release-notes/archived-release-notes#version-v41701)

Release Date: 27 Nov 2019

**Fixed:**

- Deadlock issue on batch handling

  - Under certain circumstances, a deadlock issue could encounter locking database from being queried (timeout on REST requests)

## [Version v4.17.0](/docs/mdcore/release-notes/archived-release-notes#version-v4170)

Release Date: 14 Nov 2019

**New features:**

- Callback URL (Webhooks) for file and batch scanning (to avoid polling result from client)

  - Support for individual file and batch scanning to eliminate polling mechanism i.e. MetaDefender Core will notify client based on designated / configurable callback URL whenever an individual scan finished or a batch can be closed.
- Security enhancements

  - Harden MetaDefender Core management console against security vulnerabilities found on pen-test's result
- Log correlation from parent archive file to child files
- Comprehensive failure reason on archive extraction (available on JSON response)
- Sanitization output name on password protected document fully respects value set on UI

  - No longer appended with fixed value "decrypted_document" in output name
- UTF8-encoding password for file scan request via REST

  - File scan REST API now supports "archivepwd" header with encoding password
- Total number of files inside archive (all recursive levels), available on scan result UI
- Archive scanning enhancements

  - Better integration logic with archive engine
  - Support empty folder inside archive engine
  - Not try to extract archive file if extracted size exceeded is anticipated
- Database query optimization
- Processing input refinement

  - Empty file scan request no longer is accepted at API level
- MetaDefender Core's nginx log location no longer requires double backslashes
- UI enhancements

  - Password field supported for password-protected archives or documents on the UI (web scan)

**Fixed:**

- Relaunching Proactive DLP engine process after timeout could crash Node service
- Nginx custom configuration file and certificates is unexpectedly erased when upgrading MetaDefender Core
- Overall failure on scan could encounter when system goes wrong while analyzing file type

  - When something wrong occurred while analyzing file type, the scan process could be immediately stopped and ended up as overall failed.
- Override scan result setting did not apply properly to empty batch
- Changes on workflow template could interfere Core service

  - Excluding engines in workflow template could make Core service failed to start
- Return incorrect REST response code when closing batch with invalid API key
- Fail to create local user directory under certain settings

  - Creating "Local" user directory type could be failed when "Enhance password policy" setting is unchecked
- Nginx access log location customized on registry is not retained when upgrading MetaDefender Core

  - When upgrading MetaDefender Core, nginx log location (nginx_logfile) could be unexpectedly reverted back to default value, not retained to what users configured.
- Minor UI fixes

  - Some display and hyperlink minor issues related to table and navigation
  - Hitting cancel batch button on UI causing error

## [Version v4.16.3](/docs/mdcore/release-notes/archived-release-notes#version-v4163)

Release Date: 16 Oct 2019

**New features:**

- Support new header (metadata) for file submission API
- Enhance MetaDefender Core service starting procedure
- Enhance engine update procedure
- Remove restriction on Core version retrieval REST API

**Fixed:**

- MetaDefender Core service on Linux could not be started when running on FIPS mode
- MetaDefender Core service could be unexpectedly restarted when engines repeatedly crashed
- Uninstalling MetaDefender Core did not terminate its processes properly (nginx)
- Password protected document could not be decrypted properly for data sanitization
- Uninstalling MetaDefender Core did not clean up its leftover data folder

## [Version v4.16.2](/docs/mdcore/release-notes/archived-release-notes#version-v4162)

Release Date: 10 Sep 2019

**New features:**

- Restrict APIs based on user roles (configurable)
- Support displaying and filtering username on processing history UI
- Enhance logging with YARA matched rules appended
- Upgraded nginx web server component to latest version 1.16.0
- Add new scan result - Unsupported file type
- Refined JSON output when users want to quarantine items which are already in quarantined folder
- Updated UI (minors)

**Fixed:**

- In-progress files could be deleted mistakenly, causing failures when scanning
- Engines repeatedly disable and re-enable
- File processing could be stuck until archive timeout value reached
- Non UTF-8 characters were not displayed correctly when exporting process history via UI
- Dependency installation issue on Ubuntu 18 & Debian 9

## [Version v4.16.1](/docs/mdcore/release-notes/archived-release-notes#version-v4161)

Release Date: 12 Aug 2019

**New features:**

- Supported to pin & unpin engines and their database on the UI to prevent auto update being applied
- Gently handled timeout on Archive and Deep CDR engines
- New logging mode for archive processing troubleshooting
- Enhanced logic for non-archive file processing
- Limited number of characters on some applicable text fields on the UI
- Enhanced security with unquote service exploit

**Fixed:**

- Node crash issue when under high load
- Issue with resource manager with in-use temp files
- Memory leaking issue on archive engine process
- Memory leaking issue on Node process
- Batch handling issue causing failure on batch
- Stuck scan issue at 5% when parallelcount_7z_extract is set with definitive number
- Detection issue on Proactive DLP engine with regrex rule applied
- UI issue where YARA result is not displayed
- UI visibility issue on Internet Explorer (IE) web browser
- Some other minor UI issues
- Wrong timezone set on exported CSV scan report

## [Version v4.16.0](/docs/mdcore/release-notes/archived-release-notes#version-v4160)

Release Date: 08 July 2019

**New features:**

- Proactive DLP engine (ver 2.0) integration
- Password policy enforcement
- Support archive partial sanitization for Vault and Email integration
- New REST API for local update server source
- Better handle archive sanitization timeout
- Support configurable settings for archive extraction and compression parallel count
- Enhance syslog message format
- Retouch UI
- Better logging with timeout on engines
- Enhance logic to apply engine definition files

**Fixed:**

- Wrong outcome when archive engine process unexpectedly stopped
- Wrong UI result on sanitization timeout
- Memory leak issue on engine package uploading

## [Version v4.15.2](/docs/mdcore/release-notes/archived-release-notes#version-v4152)

Release Date: 19 June 2019

**Fixed:**

- Stability issue

  - Potential deadlock issue on batch scan handling prevents querying batch information
- Usability issue

  - Enhanced error log messages when the engine process is terminated due to engine timeout
  - Exposed log messages on warning level when there is an archive extraction failure

## [Version v4.15.1](/docs/mdcore/release-notes/archived-release-notes#version-v4151)

Release Date: 06 June 2019

**New features:**

- Partial sanitization use-case for archive file types
- Clarified error messages for terminated engine processes
- New REST API for cleaning up idle batch scans
- UI improvement
- License EULA update

**Fixed:**

- Stability issue

  - Potential memory handling issue that could cause the node service to crash
  - Empty and read-only files are no longer extracted
- Usability issue

  - Not able to remove abandoned temp. files of archive files when they are empty and read-only
- Security issue

  - AD user credential is not masked properly on the audit log while sending over to AD server for authentication
- Scanning batch REST API issues
- Engine custom configuration
- UI issues

  - Dashboard refresh button sometimes did not work as expected
  - List of processing records didn't show when changing "number records per page" while not staying at first page
  - Not user-friendly error messages when adding duplicate hashes to a backlist
  - Typos on the UI

## [Version v4.15.0](/docs/mdcore/release-notes/archived-release-notes#version-v4150)

Release Date: 06 May 2019

**New features:**

- Data Sanitization details displayed on Core management console
- User password recovery and reset enforcement
- API rate limiting
- Support Windows Server 2019 (The support is still on beta)
- Suspicious results returned by engines are now configurable to be handled as a different circumstance (infected, ignore)
- Improve usability

  - Return zero for definition dates on non-AV engines' database
  - "Select all" option added to the Data Sanitization page
- Improve handling on node

  - Improve cleanup mechanism on nodes to avoid deleting files in use
  - Improve validation process when starting the node service, support to try creating temp. folder with a configurable timeout

**Fixed:**

- Fixed stabilization issues that possibly caused Node services to crash
- Scan batch API closing issues

  - No longer returns total time of -1 in response
  - Should not randomly fail due to " 400 - One or more scan is still in progress" even when all linked scans already finished
- Upgrading Core when installed in a non-default installation path prevented users from choosing another folder path by mistake
- UI issues

  - The "Process File" button no longer disappears in case of sanitization failed
  - Max recursive level under archive handling tab must equal 1 or greater
  - non-Unicode file name displayed on web scan UI encoded properly
- Sanitizing empty archive file no longer returns failed

## [Version v4.14.3](/docs/mdcore/release-notes/archived-release-notes#version-v4143)

Release Date: 01 Apr 2019

**New features:**

- Support built-in integration with OPSWAT Central
- New setting for archive sanitization timeout
- Add process time field into CSV exported history report
- Effectively wipe out necessary data from support package
- Revamp Inventory UI page with "Utilities" group
- More relevant REST error message for scan request where file is non-existed / inaccessible
- Syslog message for scan-finish event more comprehensive
- Consolidated scan info for archive scan result fetching
- Add libcurl4 as alternative dependency to libcurl3 for better support on Ubuntu 18.04
- Outputs and indicators for Threat Intelligence feature on Quarantine UI page more relevant and informative

**Fixed:**

- Node becomes unstable under high load processing
- Closing batch with ongoing scans could result in failed verdict on batch
- Inconsistent behavior with password protected document
- Temporary files are not cleaned up when cancelling an ongoing scan
- Inconsistent returned error message between batch and file scanning via REST
- DLP verdict returns incorrect value for some cases
- Logs in support package did not handle non-Unicode characters

## [Version v4.14.2](/docs/mdcore/release-notes/archived-release-notes#version-v4142)

Release Date: 28 Feb 2019

**New features:**

- New result page, n ew look and more informative badge

**Fixed:**

- Engine configurations could not be saved
- Make error message more relative for case where file exceeded the size limit
- Pinning engines and their databases independently

## [Version v4.14.1](/docs/mdcore/release-notes/archived-release-notes#version-v4141)

Release Date: 31 Jan 2019

**Fixed:**

- Missing "pinned" option from "/stat/packages" JSON response
- Inconsistent "progress_percentage" and "result" values
- Hash validation (blacklist/whitelist)
- Upload performance

## [Version v4.14.0](/docs/mdcore/release-notes/archived-release-notes#version-v4140)

Release date: 19 Dec 2018

**New features:**

- Send quarantined files to MetaDefender Cloud for scanning
- Automation support:

  - Support ignition file to automate the welcome wizard
  - Configuration API functions have been documented
- Enhanced password policy can be enabled for local users
- Files with Failed to sanitize result can be set to be blocked

## [Version v4.13.2](/docs/mdcore/release-notes/archived-release-notes#version-v4132)

Release date: 21 Nov 2018

**New features:**

- Tiles on Dashboard are linked to the corresponding pages
- More options to filter Processing History (Post Actions and CDR)

**Fixed issues:**

- In case of an engine hangs, the communication channel is blocked between the Node and the Core, so more engines can time out
- Clean-up mechanism removes files still in use
- Various engine handling issues

## [Version v4.13.1](/docs/mdcore/release-notes/archived-release-notes#version-v4131)

Release date: 31 Oct 2018

Fixed issues:

- YARA and DLP tasks are not stopped on cancelling a processing
- Batch processings cannot be cancelled via web management console
- "Can't process shared resource file" error message did not contain the file name

## [Version v4.13.0](/docs/mdcore/release-notes/archived-release-notes#version-v4130)

Release date: 16 Oct 2018

Important:

- YARA engine integration

New features:

- Processing history entries can be colorized
- Files can be marked as suspicious if less than a given number of engine mark it as infected
- Processings can be cancelled via web management console
- Default rules are added for MetaDefender Email Security
- Bulk operations in quarantine

Fixed issues:

- Extracted files are left behind
- On Debian based systems, on upgrades, engines are deleted and disabled engines are re-enabled

## [Version v4.12.2](/docs/mdcore/release-notes/archived-release-notes#version-v4122)

Release date: 3 Oct 2018

Fixed issues:

- In case of archive processing, sometimes clean-up mechanism removes some extracted files before processing is finished

## [Version v4.12.1](/docs/mdcore/release-notes/archived-release-notes#version-v4121)

Release date: 26 Sept 2018

New features:

- Files can be whitelisted/blacklisted by their checksums
- More specific log entries for CDR

Fixed issues:

- Details of scan result for nested archives (for the file itself not for the content) is not propagated to the top level
- The value, set in "MAX TOTAL SIZE OF EXTRACTED FILES" is handled incorrectly
- Older configs cannot be imported into v4.12.0

## [Version v4.12.0](/docs/mdcore/release-notes/archived-release-notes#version-v4120)

Release date: 15 Sept 2018

Important:

- Data Loss Prevention functionality

New features:

- Possibility to set the number of engines that required to start file processings (per workflow)
- Possibility to exclude engines from processings (per workflow)
- Improved user interface performance
- Possibility to blacklist/whitelist files by file types besides file type groups
- Re-designed workflow tab list appearance
- Possibility to set timeout for sessions regardless of user activity

Fixed issues:

- On Node details page, every issue appears multiple times
- Despite not detecting any vulnerabilities, the vulnerability tab appears
- On hash lookup page, empty hash can be searched
- Sanitized output file name validation can cause user interface stalled

## [Version v4.11.3](/docs/mdcore/release-notes/archived-release-notes#version-v4113)

Release date: 30 Aug 2018

Fixed issues:

- Whitelist page under Inventory menu does not exist (only UI issue)

## [Version v4.11.2](/docs/mdcore/release-notes/archived-release-notes#version-v4112)

Release date: 29 Aug 2018

New features:

- The access_log Nginx directive now can be overridden
- The parallel count parameter now can be set per engine
- Minor changes on user interface for better user experience

Fixed issues:

- A critical CSV injection vulnerability in the CSV export functionality (issue reported by Wojciech Reguła, SecuRing)
- Archives can be sanitized even in case of partial processing (e.g. exceeded archive size, exceeded archive file number)
- In some cases, blocked results can be overwritten by an allowed result with higher priority
- Inconsistent operation of MetaDefender Cloud integration
- Typos on the user interface
- Abandoned files left behind after processings

## [Version v4.11.1](/docs/mdcore/release-notes/archived-release-notes#version-v4111)

Release date: 8 Aug 2018

Fixed issues:

- Unexpected Core and Node service restart in some corner cases
- Using remote syslog server slows down the product in case of missing PTR record in DNS
- Empty files are skipped in archives
- Incomplete archive extraction issue happened on heavily overloaded systems

## [Version v4.11.0](/docs/mdcore/release-notes/archived-release-notes#version-v4110)

Release date: 11 July 2018

New Features:

- Exceptions (by mime-type) from whitelist/blacklist
- New engine page called Technologies
- Support for user-friendly engine configuration (depends on the engine version)
- Welcome wizard

Fixed issues:

- Slow clean-up mechanism
- Abandoned files after uninstall in Windows
- Temporary files are left behind after processings
- Wrong sanitized output file name in some cases
- Default workflows can be overridden on config import
- Core crashes

## [Version v4.10.2](/docs/mdcore/release-notes/archived-release-notes#version-v4102)

Release Date: 27 June 2018

Fixed issues:

- Uninstall not properly cleans the system
- The "whitelisted" and "blacklisted" results are overriden by "infected" result
- Node crashes
- Inconsistent results in case of archive processing: In case of processing an archive more times, the result may be different by cases (infected/exceeded archive file number/exceeded archive size)

## [Version v4.10.1](/docs/mdcore/release-notes/archived-release-notes#version-v4101)

Release Date: 23 May, 2018

New features:

- Data Sanitization engine time-out and retry count is now configurable
- REST API: process info contains the name of the last scanned file when scanning archive file types
- REST API: Configurations that may change the final scan result since the time of processing will be included in the [process info response](/docs/mdcore/metadefender-core) (i.e., outdated definitions)
- Hash based result lookups can be filtered by rule name

Fixed issues:

- Sanitized DB integrity issue
- On the dashboard, category names of doughnut charts were truncated
- In case of archive processing, the "Not scanned" result to a file is not propagated to a higher level (overall verdict)

## [Version v4.10.0](/docs/mdcore/release-notes/archived-release-notes#version-v4100)

Release Date: 2 May, 2018

Important:

- Added support for the LDAP directory type
- Syslog messages can now be sent to multiple log aggregators
- MetaDefender installers no longer use eicar test files

New features:

- AD and LDAP directories can now be configured with multiple servers
- Sanitization failures are marked with a badge in the scan session summary
- Admin’s will be notified if a third party solution is blocking MetaDefender from working as expected
- Users can now be granted API keys manually
- Paginated archive results
- HTTPS can now be enabled from web management console

Fixed issues:

- Improved license status info
- In some cases, sanitized files had faulty names
- Suspicious scan results were not always at the top of the list in archive file types
- Inappropriate handling of user rights in the Whitelist page
- AD group members did not have user profiles
- Misleading license information

## [Version 4.9.1](/docs/mdcore/release-notes/archived-release-notes#version-491)

Release Date: 28 February, 2018

New features:

- New-looking user interface
- Workflows based on the default one (not edited by workflow editor) will be kept and upgraded on version upgrade in the future
- It is allowed blacklisted/whitelisted files to be processed

Fixed issues:

- Security zone: IP address validation
- Cancelled batches are displayed as in-progress
- Removing certificates from the inventory caused policies to disappear
- Memory leak in Node
- Access via Active Directory is not logged
- Sluggish pages under Policy menu

## [Version 4.9.0](/docs/mdcore/release-notes/archived-release-notes#version-490)

Release Date: 13 December, 2017

New features:

- IPv6 support
- Global whitelist by hash
- Whitelist by file type group
- Display more security related information on dashboard
- Changed default port for external nodes to 8007
- New default security rule for Metadefender Secure File Transfer (SFT)
- Performance tuning of processing history
- Improved resource handling on Node
- On Linux, multiple nginx worker processes for better scaling

Fixed issues:

- Upgrades overwrite existing configuration (IP, port, etc.)
- Resource folder clean up after data sanitization
- Update timing settings affect manual updates
- Poorly handled invalid update files
- Poorly handled UTF-8 characters in output file name for sanitized files
- /hash API can give "in progress" result

## [Version 4.8.2](/docs/mdcore/release-notes/archived-release-notes#version-482)

Fixed issues:

- Fixed a memory leak caused by failed update download
- Fixed a possible crash issue at Scan history manual cleanup in case of high load
- Fixed a memory leak in case of recurrring failed database deployment on Node

## [Version 4.8.1](/docs/mdcore/release-notes/archived-release-notes#version-481)

Release Date: 5 October, 2017

New features:

- Improved engine/database update distribution to nodes
- Improved archive extraction limit handling
- Improved engine monitoring
- More precise time duration measurement for requests
- API for canceling scans (file/batch scans)
- Option to disable archive extraction of office documents
- For batch scans, certificate validity interval can be set
- Improved scan result badge

Fixed issues:

- Fixed issue of scans stuck in "in progress" state
- Fixed possible product crash during archive scanning
- Fixed update bug where incorrect packages left behind
- Fixed failed quarantine handling
- Fixed handling unavailable engine during scans
- Scan result JSON now contains file name in UTF-8 format
- Limited number of parallel Post Action and External Scanner scripts
- Archive handling parameters now have upper bound
- Improved archive handling
- Archive related failure handling

## [Version 4.8.0](/docs/mdcore/release-notes/archived-release-notes#version-480)

New features:

- Quarantine for blocked files
- Scanning files in batch (REST API)
- Certificate and key handling for scan batch signing
- Configurable sanitized file name
- Post action commands gets the result JSON with final verdict included
- Increased scan history export interval
- Improved archive bomb handling
- Added eng_id to scan_results.scan_details (REST API)
- Showing in-progress files in "extracted files" list of archives
- Added "scan_all_result_a" into "extracted_files" (REST API)

Fixed issues:

- Fixed case insensitive username comparison in Active Directory integration
- Process workflow revamped (post actions run every time)
- Fixed non-updated policy user interface after added new user roles
- Fixed handling of database upgrade errors in linux package installers
- Fixed error handling when scan target was sent in the body and via filepath (/file REST API)
- Fixed disconnected ghost node issue displayed on user interface

## [Version 4.7.2](/docs/mdcore/release-notes/archived-release-notes#version-472)

Issues fixed:

- Fixed bug that could cause policies to not contain any elements and forbid user to create new items
- Fixed bug where Core could download older version of engines where newer one was already downloaded

## [Version 4.7.1](/docs/mdcore/release-notes/archived-release-notes#version-471)

Issues fixed:

- Fixed upgrade of scan configuration
- Fixed ghost nodes appeared on Inventory→ Nodes page

## [Version 4.7.0](/docs/mdcore/release-notes/archived-release-notes#version-470)

New features:

- Active Directory integration
- Custom post actions
- Redesigned user interface
- External (customer developed) scanner integrations
- Policies export/import
- Archive sanitization
- Individual log message level override
- Aggregated archive scan result in Scan History
- Self-lockout protection, admins can not delete themselves
- gzip and base64 encoding now supported on /file REST API
- Able to navigate through archive hierarchy
- Timezone changed to local in log messages

Issues fixed:

- Fixed scanning of .lnk files on Windows
- Fixed blacklisting of Unicode filenames
- Automatically downloads packages again if the previous download failed
- Fixed order of extracted files on scan details view
- Fixed rare temporary file leak during archive scan

## [Version 4.6.3](/docs/mdcore/release-notes/archived-release-notes#version-463)

Issues fixed:

- Improved scan result fetching performance for big archives

## [Version 4.6.2](/docs/mdcore/release-notes/archived-release-notes#version-462)

Issues fixed:

- Improved archive extraction performance
- Fixed a race condition in /file/<data id> REST API that could provide access error in some cases
- Fixed advanced engine config reload for Data sanitization engine
- Fixed login issue which happened when many login request was initiated concurrently
- Fixed calculation of extracted file count

## [Version 4.6.1](/docs/mdcore/release-notes/archived-release-notes#version-461)

New features:

- List of path for local filescan can be blacklist / whitelist with specific error message on REST

Issues fixed:

- Invalid external Node listening IP/port config stops product startup
- Connection to remote syslog is reactivated on network error
- If user has no right to use a rule, following rules in order will still be checked
- sending HEAD request where GET should have been sent will not lead to product crash
- Ensure resource file deletion on Microsoft Windows when a scan engine locks file further than expected
- Scan history CSV export uses comma as separator
- Fixed potential Node service crash when stopping during scanning
- More specific error message when uploaded file size limit exceeded
- Fixed a rare race condition in update downloader component
- Fixed login issue when Core v3 like URL is used by the admin

## [Version 4.6.0](/docs/mdcore/release-notes/archived-release-notes#version-460)

New features:

- Multiple user roles introduced with different access rights
- Scan Agent has been renamed to Scan Node
- Role (user group) based rule availability configuration
- Role based scan result visibility with different level of details exposed
- Ability to export part of scan history into STIX/Cybox format
- Ability to export part of scan history into CSV format
- Filter on rule and source added into Scan history
- Configurable lockout feature against brute force login attack
- Official support introduced for Ubuntu 16.04
- Detection threshold (suppress threat detection if less then X engines detected a threat)
- Custom engine configuration via user interface
- Free text search functionality in user guide
- Suspend engine testing/deployment to Node when 3rd party security software blocks access to malware files
- Successful login / unsuccessful login / lockout events are logged
- Option to send engine issue count info during update
- [REST API] /file/{data_id} response for scan results now contain process info block for extracted files
- Initiating local scan is faster as no wait for hashing is required

Issues fixed:

- [REST API] /file/{data_id} blocked reason change to mirror V3 API
- Fixed handling of archive extraction depth
- More flexible and stable internal database upgrade when upgrading product
- Custom engine update timeout increased to one hour to deal with slow engine updates
- Archive engine fixes (non-ASCII filenames in archive)
- Engine handling fixes, improved handling of engine deinitialization
- More precise engine cleanup when removing engines
- Fixed bug where random connections were rejected every 2 min
- Fixed bug regarding updates handling (conflicting names)
- Filesize is now correctly displayed on scan result user interface
- Support package generator now includes auditlog db

## [Version 4.5.1](/docs/mdcore/release-notes/archived-release-notes#version-451)

Issues fixed:

- Fixed possible crash of Agent when there is database which is handled by engine
- Fixed possible crash of Core that could occur when updating a package

## [Version 4.5.0](/docs/mdcore/release-notes/archived-release-notes#version-450)

New features:

- Data Sanitization of files to protect against unknown threats
- Filetype mismatch detection
- Improved user interface responsiveness for small screens
- Real filetype based blacklist option in rules/workflows
- Improved licensing for offline deployments
- Added product specific proxy settings in the Linux version
- Advanced configuration for allowed/blocked file scan result types

Issues fixed:

- Fixed local scan option user interface for new rules
- Fixed Scan History auto cleanup collision with manual cleanup
- Potential issue fixed for update file upload
- /apiversion interface is added to easily determine REST API compatibility level

## [Version 4.4.1](/docs/mdcore/release-notes/archived-release-notes#version-441)

New features:

- Added several features/improvement for better Metadefender Kiosk integration
- Full audit log about any configuration changes via Web user interface or REST API
- Able to disable applying update in user configurable time periods
- Core can act as an update source for OESIS product line
- Detect if the analyzed binary is a part of any vulnerability detection
- Improved scan engine status monitoring and auto recovery
- Custom directory can be set for storing temporary files
- Able to set up apikey for every user for easier REST API integration
- Improved hardware detection in license component

Issues fixed:

- Fixed message content format in Windows Event log
- Fixed system wide proxy usage on Windows
- Improved browser cache handling in case of product upgrades
- Fixed a path specification issue in local file scanning feature on Windows
- Fixed engine counting on Agent details page (do not count utility type engines)
- Fixed lost agent connection handling
- Fixed handling of unsupported Transfer-Encoding on REST API
- Patched internal nginx web server to fix CVE-2016-4450
- Fixed archive timeout handling and user interface
- Fixed scan results in case of archive related findings
- Improved logging of proxy usage
- Improved handling of slow file uploads
- Detailed logging in case of SSL connection issues
- Improved auto-recovery of engines running under Emulated Windows

## [Version 4.3.0](/docs/mdcore/release-notes/archived-release-notes#version-430)

New features:

- Introduced official support for Microsoft Windows 7 or newer and Microsoft Windows Server 2008 R2 or newer
- Added offline update picker feature to make it easy to apply offline updates without user interaction or scripting
- Able to scan local files stored on server without transferring the content via REST API
- Added hardware related info into generated support package
- Created a framework in Linux version to be able to run Windows scan engines on Linux server
- Option added to log to a remote syslog server
- Inventory / Scan Agents page extended with more detailed agent information
- Parameter workflow renamed to rule in some REST APIs
- Improved system issue notification on Web Management Console
- Added detection of 3rd party anti-malware products that break operation of Metadefender Core
- Improved scan performance of various engine integrations

Issues fixed:

- Improved documentation of multiple REST APIs
- Fixed failed scans during some engine or database update
- Removed unmeaningful database age display of non-anti-malware engines

## [Version 4.2.0](/docs/mdcore/release-notes/archived-release-notes#version-420)

New features:

- product name has changed to Metadefender Core
- able to use scan results from [metadefender.com](http://metadefender.com)
- workflow options can be configured from Web Management Console
- workflow options can be overridden from rule editor window
- support for system wide HTTPS proxy
- it is possible to configure maximum file size of scanned files
- filtering security rule by user agent is now possible
- eliminate limitations on the size of scanned files
- improved scan related log messages
- deployment can now be deactivated on the License page
- automatic deployment reactivation of online installations if license becomes invalid
- Metascan v3 URLs (/management and /metascan_rest) are now redirected to the proper v4 URLs
- check disk space before/during scan requests

Issues fixed:

- fixed encrypted communication error with activation server on Ubuntu 12.04
- fixed temporary folder cleanup
- fixed support data collector scripts
- do not download database without the corresponding engine package
- number of engines and maximum file size is now reflect the current status

## [Version 4.1.0](/docs/mdcore/release-notes/archived-release-notes#version-410)

New features:

- https support for REST API and for Web Management Console
- update history to track every database/engine change
- new option to globally disable or enable specific scan engine
- reworked result page for archive files
- user guide is available within the product
- no scan downtime while updating engine/database (if engine supports)

Issues fixed:

- more descriptive communication error messages instead of error codes in logs
- proper handling of update download issues
- fixed handling of scan engine crashes
- fixed manual update package upload
- fixed unwanted warning message after successful activation

## [Version 4.0.1](/docs/mdcore/release-notes/archived-release-notes#version-401)

New features:

- new script to help log collection for support
- inform the user if browser is not HTML5 compatible
- show a spinner if loading a page takes too much time
- support lower screen resolution for web interface
- support for non-ascii character filenames in archives

Issues fixed:

- fix stability issue in update downloader
- optimize database queries
- do not check for updates at product startup if auto update is off
- fixed a page auto refresh issue with Internet Explorer

## [Version 4.0.0](/docs/mdcore/release-notes/archived-release-notes#version-400)

New features:

- Able to to monitor Metascan v4 for Linux instances
- Able to to monitor Metascan v3 for Windows instances
- Collect Files scanned and Infections found stats from managed instances
- Deploy scan engine database updates to Metascan v3 for Windows instances
- Deploy scan engine and scan engine database updates to Metascan v4 for Linux instances
