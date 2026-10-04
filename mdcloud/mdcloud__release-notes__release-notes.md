<!-- source: https://www.opswat.com/docs/mdcloud/release-notes/release-notes -->

# Release Notes

In order to enhance our customers' experience, we will be introducing the software release in a phased approach, gradually extending it to different regions as follows:

| Region | When | Time |
| --- | --- | --- |
| JP | 3rd Wednesday of each month | 03:00AM - 05:00AM (JST) |
| IN | 3rd Wednesday of each month | 03:00 AM - 05:00 AM (IST) |
| EU | 4th Monday of each month | 02:00AM - O4:00AM (CEST) |
| CA | 4th Monday of each month | 03:00AM - 05:00AM (EDT) |
| US | 4th Wednesday of each month | 03:00AM - 05:00AM (EDT) |
| AUS | 4th Wednesday of each month | 11:00PM - 01:00AM (AEST) |

### **September 2026**

| Product Area | Release Type |
| --- | --- |
| metadefender.com   - Release date - September 16, 2026 - Version - 3.8.0 | New Features and Enhancements   - **Dedicated Enterprise and Community product pages.** [metadefender.com](http://metadefender.com) now has dedicated Enterprise and Community product pages, reachable from the expanded Product section of the main header navigation. - **Result cards now describe what each technology did.** All eight cards in the Analysis Overview grid previously shared a single status word, "Detected", so a successful sanitization appeared as "Detected - 11 Objects Sanitized" and a country match as "Detected - People's Republic of China". Each card now uses the verb appropriate to its technology: Deep CDR reports **Sanitized**, Proactive DLP reports **Identified**, Country of Origin reports **Origin**, Adaptive Sandbox reports **Verdict**, Vulnerability Assessment reports **Found**, and Metascan and Predictive AI continue to report **Detected**. Existing scan history results are displayed using the new mapping. - **Updated archive scan results view.** Scans performed with archive extraction present their extracted files and results in the current design. - **Emulation Graph design update.** The Emulation Graph on the file result Threats tab is updated to the current design. - **Similarity Search rows expand on full-row click.** Clicking anywhere on a Similarity Search row expands and collapses its detail panel. Rows are keyboard focusable, with Enter and Space toggling them, and selecting text within a row no longer triggers a toggle.   Fixed   - **Archive child files now show their own sandbox report.** Opening a file extracted from an archive issued an additional request keyed to the parent archive, which added latency and could display the parent's sandbox report on the child's page. The child's own report is now used. - **Cookie consent icon no longer covers Workflow Studio controls.** In Secure Pipeline Studio, the floating cookie consent icon overlapped the engine configuration panel and partly obscured the Cancel and Add buttons while a workflow was being configured. The icon has been relocated. |
| API   - Release date - Released based on each region's maintenance window timeframe.  - Version - 4.81 | New Features and Enhancements   - **Aether workflow.** A new detection pipeline is available in the scan flow, activated through the rule values `aether` or `aether, unarchive`. Aether runs reputation, deflection, Adaptive Sandbox and threat intelligence in sequence and stops at the first definitive verdict, with each engine's outcome surfaced on the result as it completes. Reputation, deflection and threat intelligence result objects are added to the scan result and their status codes are folded into the overall verdict. Each Aether-scanned file consumes one Sandbox unit, charged when the request is admitted**.** Aether can be combined with archive extraction only; combining it with any other workflow option is rejected. - **Sandbox allowance is enforced per extracted file on archive scans.** Each file extracted from an archive now deducts one sandbox unit as its sandbox processing completes. When the allowance is partially exhausted, only the files that fit within it are processed. When the allowance is fully exhausted, the scan reports exceeded limits and extracted file details are omitted. Prevention quota accounting is unchanged. - **Deep CDR and Proactive DLP verdicts return independently for Community users.** On Community tier scans using a combined Deep CDR and DLP workflow, neither engine's output was returned until the slower engine finished. Each engine's output now surfaces as that engine completes   Fixed   - **Consistent scan progress messaging.** Per-file completion messaging previously varied between workflows depending on when each workflow was last edited. All workflows within a region now report progress consistently. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

---

### **August 2026**

| Product Area | Release Type |
| --- | --- |
| metadefender.com   - Release date - August 12, 2026 - Version - 3.6.0 | New Features and Enhancements  Fixed   - **Result card accuracy.** Several result cards now report the engine's actual state instead of a misleading one:    - Deep CDR shows **Sanitization Successful** for a successfully sanitized clean file, instead of the red *Detected* treatment.   - MetaScan distinguishes **Not Scanned** from **Not Detected**.   - OPSWAT Predictive Alin AI shows **Not Supported** instead of *Not Active* when the file type is unsupported, and its card now reflects Alin AI's own verdict rather than threats found by other engines.   - Country of Origin reflects the detected country instead of showing *Not Detected*.   - Adaptive Sandbox shows the sandbox result for a password-protected file extracted from an archive, instead of *Not Active*. - **Engine settings no longer disable the engine.** Saving an engine-level setting no longer disables that engine in the workflow it applies to after a page refresh. - **Reputation lookups are routed correctly.** An IP address, domain or hash pasted into Analyze File/URL is now sent to the reputation lookup instead of the file-scan API — it no longer fails with an error or consumes scan quota. - **Legacy scan-result links resolve.** Deep links using the combined `/regular/overview` path — emitted by older integrations such as ICAP — now navigate to the correct scan result. - **Loading and empty states.** Certificates and Requests sections show a loading state while sandbox analysis is still running, and the Emulation Graph shows an empty state instead of an endless loader when the sandbox is unavailable or aborted. - **Navigation and layout.** Sandbox and Vulnerability result cards navigate to their sections correctly without unexpected resizing; the *AI Predictive Detection* label appears in the header when a threat is detected; Threats tab section styling is restored when no MetaScan results are present; the Indicators of Compromise label is left-aligned. |
| API   - Release date - Released based on each region's maintenance window timeframe.  - Version - 4.80 | New Features and Enhancements   - **SBOM / Software Composition Analysis.** The SBOM engine is now available in the scan flow, activated through a custom workflow. Results are returned in a new `sbom_info` object, with dedicated overall status codes and `sbom:<code>` blocked reasons. Now fully documented in the public API contract for `GET /v4/file/{data_id}` and `GET /v4/hash/{hash}`. Availability depends on the engine being deployed in your region. - **Partial result delivery for Sandbox workflows.** Scans no longer hold at 99% waiting for the sandbox. Final Multiscanning, Deep CDR and DLP verdicts are returned as soon as those engines finish; the sandbox section is merged in when it completes and the overall verdict is recalculated. Progress values are now strictly monotonic — no stuck or regressing scans. As a result, sandbox verdicts such as *Malicious Verdict by Sandbox* are also correctly reflected in `scan_all_result_a` instead of *Unknown*. - **Deep CDR skip reason.** `GET /v4/file/{dataId}` now returns `process_info.post_processing.sanitization_details.skipped_reason`, so you can see *why* sanitization was skipped (for example, the file is digitally signed) rather than only that it did not run. The bulk CDR-status lookup response is unchanged. - **Full archive child-file count.** Archive scan results now include `extracted_files.total_files_count` on the root archive — the number of extracted files across *all* nesting levels, not just the first. Additive and backward compatible; for a flat archive it matches the existing `files_extracted_count`. - **Consistent configuration across all regions.** Custom workflow and engine-profile changes made in one region are now propagated automatically to every other production region, and default workflows now resolve to a single per-region source of truth. This removes cases where the same workflow scanned differently depending on the region serving the request. Existing custom workflows and engine profiles are unaffected.   Fixed   - **Non-ASCII file names preserved.** Files uploaded with Hebrew, Arabic, Chinese, Japanese or emoji characters in the name are no longer returned mangled in the `/v4/file` response. - **Scan-by-URL resilience.** Transient errors from the source location (connection resets, throttling, brief server errors) are now retried within a bounded budget instead of failing the scan as an invalid URL. A momentary hiccup now costs a short delay rather than a lost scan. - **Limits above platform maximums no longer fail every scan.** An API key or organization whose stored file-size, archive-size, archive-depth or archive-file-count limits exceed the platform ceiling no longer fails all scans with HTTP 400 — values are clamped to the supported maximum before the scan is submitted. Your stored configuration is unchanged.  - **Engine profile updates work across regions.** Blocklist and engine-profile edits no longer fail when the connected workflows were created in a different region. - **Sandbox report handling no longer stalls scans.** Reports are copied server-side, so a slow report no longer delays its own scan or unrelated scans queued behind it. - **Vulnerability feed validation.** `GET /v4/feed/infected/latest` and `GET /v4/feed/clean/latest` now return a proper `400` for non-numeric or whitespace `page` values (previously served as page 1, or a `500`), and a corrupted cache entry is recomputed rather than returned to the caller. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### **July 2026**

| Product Area | Release Type |
| --- | --- |
| metadefender.com   - Release date - July 15, 2026 - Version - 3.4.0 - Release date - July 29, 2026 - Version - 3.5.0 | New Features and Enhancementsin 3.4.0   - **DLP configuration in Custom Workflows.** You can now configure Proactive DLP options directly inside your custom workflows. - **Download redacted files.** A dedicated button on scan results lets you download the redacted (DLP-processed) output. - **Improved CVE lookups.** CVE results are now indexed with dedicated, shareable URLs.   Fixedin 3.4.0   - AI Content Inspector: correct *Failed* status when the engine fails, a loader while processing, disabled state for unsupported file types, and better empty-state handling. - URL scan reports no longer show duplicate Certificate/Request entries. - Vulnerability Assessment: card navigation scrolls to the correct section and the table supports more page sizes. - Community Feedback comment counts now match the displayed comments. - The consent/data-sharing notice is correctly shown to free users when scans are not private. - Long file names now show their full value via tooltip. - Various layout, styling, and hover/disabled-state fixes across Results, Licensing, Processing Summary (tablet), and blog pages.   New Features and Enhancements in 3.5.0   - **Redesigned Scan Results and Analyze pages.** Refreshed experience for both signed-in and guest users, including an updated AI Content Inspection section. - **Expired-license banner.** Standalone users and members of organizations with expired licenses now see a clear banner with guidance.   Fixed in 3.5.0   - Organization notifications: users added to an organization now reliably receive their notification. - CDR workflow settings now apply consistently. - Sandbox: *Result* field now renders correctly in Safari, and the Sandbox option only appears for workflows that support it. - Hashes section: copy buttons restored and full values shown for truncated hashes; OSINT SHA-256 details display correctly. - Scan History: the scan count text now matches the graph. |
| API   - Release date - Released based on each region's maintenance window timeframe.  - Version - 4.79 | New Features and Enhancements  Fixed   - **Sandbox scans via** `downloadFrom` **no longer stall on oversized files.** When a file retrieved through the `downloadFrom` header exceeds the maximum upload size, the scan result now explicitly reports the oversized-file error instead of remaining "in progress" indefinitely. - **Accurate progress reporting for archives.** `GET /v4/file/converted` no longer reports `100%` progress while files extracted from an archive are still being processed. - **Complete CDR details in bulk lookups.** `POST /v4/file/bulklookup` with `includecdrdetails: 1` now consistently returns `file_path` and `object_sha256` for sanitized files. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### June 2026

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - June 24. 2026 - Version - 3.2.2 - Release date - June 11. 2026 - Version - 3.1.0 | New Features and Enhancementsin 3.2.2   - **CAPTCHA protection** on key user flows. - **API keys hidden by default** — keys stay masked until you reveal them, including in example queries. - **Sandbox fallback** via Filescan.io for greater resiliency. - **New Community blog:** "Static vs. Dynamic Analysis."   Fixedin 3.2.2   - **Clearer results** — clarified ambiguous "Undetermined/Unknown" labels, removed duplicate AI Content Inspector cards, and fixed status display after test-file uploads. - **Correct access controls** — custom workflows no longer appear for unpaid users, and IP Allowlist is hidden for roles that shouldn't see it. - **CDR and hash details** — CDR results render correctly, and SHA/MD5 values copy reliably on smaller screens.   New Features and Enhancementsin 3.1.0   - **Mobile and tablet responsiveness** across Home/Analyze, Results, Integrations, Product, and Licensing pages. - **More reliable sign-in** via MyOPSWAT. - **Sandbox advanced details** — "View Advanced Details" now opens reliably. |
| API   - Release date - Released based on each region's maintenance window timeframe. - Release date - June 15. 2026 - Version - 4.78.0 - Release date - June 25. 2026 - Version - 4.78.1 | New Features and Enhancements in 4.78.0   - **Private hash lookups for Sandbox** — Sandbox hash lookups now check your private collections first, falling back to public data when needed. - **Sandbox results in hash lookups** — Sandbox findings now appear in a dedicated section, and only confirmed-malicious sandbox verdicts affect the overall result (Suspicious verdicts no longer block). - **Human-readable engine names** — The license-engines endpoint can now return friendly engine names alongside engine IDs (opt-in). - **Global workflow propagation** — Creating, updating, or deleting a workflow now takes effect across all regions immediately.   Fixed in 4.78.0   - **Reliable sandbox report downloads** — Fixed invalid and prematurely expired report links that caused download errors for Filescan.io results.   New Features and Enhancements in 4.78.1   - **Earlier results with AI-generated content detection** — Anti-malware, Deep CDR, and DLP verdicts are published as soon as core engines finish. The API reports 99% progress while AI content analysis completes, so you can act on results sooner. - **AI content detection status codes** aligned to the latest specification, including a new "Unsupported File Type" code.   Fixed in 4.78.1   - **Accurate sandbox verdicts** — Sandbox (Filescan.io) results now report correctly as Suspicious, Likely Malicious, or Malicious instead of "Unknown." - **Reliable engine selection** — AI content detection is no longer requested when it isn't available for the selected scan priority, preventing failed engine requests. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### May 2026

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - May 27. 2026 - Version - 2.13.0 | New Features and Enhancements   - **CSWG Proxy — self-service customer UI configuration** — Adds a self-service UI to configure CSWG proxy settings without engineering involvement. - **Licensing — AV engine matrix aligned with MetaDefender Cloud tiers** — The Licensing comparison matrix now reflects the correct AV engine coverage per license tier. - **Settings — access for users without an organization** — Users can access the Settings area even if they are not part of an organization.   Fixed   - **SSO login redirect hardening —** Prevent open redirects after SSO login by validating allowed redirect destinations. - **postMessage origin validation —** Tighten cross-origin message validation for embedded/iframe flows. - **Workflow Studio — Deep CDR settings preserved when editing File Type configuration —** Fixes cases where main Deep CDR engine configuration was lost after applying File Type settings. - **Japanese localization — Sandbox Threat Indicators and IOCs display correctly —** Fixes missing sandbox Threat Indicators and IOC content when the UI language is Japanese. - **Japanese localization — Dashboard chart legends show correct file type labels —** Fixes duplicate/incorrect legend labels on "Top 5 file types" charts in Japanese. - **Japanese localization — Advanced Analysis table pagination shows correct numeric options —** Fixes the "Items per page" selector showing garbled / date-like values instead of numeric options. - **Notifications panel — long IDs no longer overflow the container —** Long notification identifiers wrap/fit so content stays readable in the Notifications panel. - **Sandbox results — remove redundant "No Threat" label on YARA rule rows —**Removes duplicate verdict text so Sandbox YARA rows render consistently. - **Cloud Security for Salesforce card — inputs use full width —** Input fields on the Salesforce card layout correctly without clipping. - **Reports — chart values align with report table results —** Addresses discrepancies between chart data and the corresponding report table. |
| API   - Release date - Released based on each region's maintenance window timeframe. - Version - 4.77.0 - Release date: 5.28.2026 - Version - 4.77.1 - Release date: 6.3.2026 | New Features and Enhancements in 4.77.1  **Support new AIGCD 2.0 status codes** — Community users will receive the new AIGCD scan results and codes.  New Features and Enhancements in 4.77.0  **Support migration of file submission history across organizations** — __SRE-facing capability to move a user's file submission history from one organization to another so that transferred users keep their reporting continuity in the new organization.  **Enforce FilescanIO file size limit in workflows** — Default and existing custom workflows now use `MAX_SANDBOX_FILE_SIZE` for the FilescanIO node. The limit is also enforced when creating or updating custom workflows.  Fixed in 4.77.0  **Standardize authentication error responses across endpoints** — All authentication failures (missing header, wrong strategy, invalid API key, invalid/expired token) now return a single generic `401 Unauthorized` payload. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### April 2026

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - April 23rd - Version - 2.11.0 | New Features and Enhancements  **Custom Workflows now available to individual paid users** — Paid subscribers who are not part of an organization can now create and maintain custom workflows directly from Workflow Studio. Custom Workflows are no longer limited to organization-based accounts, giving solo professionals the same workflow customization power as teams.  **Notification subscriptions by scan result code** — You can now configure notifications to fire on specific scan result codes, giving you finer-grained control over which scan outcomes trigger an alert.  **Adaptive Sandbox — IOC verdict columns** — Indicators of Compromise lists now include verdict columns, making it easier to interpret sandbox IOC output at a glance.  **Adaptive Sandbox — Clearer geolocation context** — Sandbox results now expose richer geolocation context for analyzed traffic, helping analysts understand where observed activity originated.  **Multiple passwords for layered archives** — When scanning archives that contain nested encrypted archives with different passwords, you can now supply more than one password in a single scan request, removing the need for repeated scans.  **Analyze page — Default workflow now in the picker** — The built-in default workflow now appears in the workflow dropdown alongside your custom workflows, making it easier to switch between default and customized scanning behavior.  **Licensing page — Clearer copy and layout** — Subscription and plan information has been reorganized and reworded for easier reading.  **Performance improvements across the application** — Page load and responsiveness have been improved across the Dashboard, Analyze, and Profile pages through frontend optimization, smarter image loading, and reduced layout shift on key components.  Fixed  **Settings now reachable for paid individual users** — Users on paid plans without an organization can now reliably access Settings (Profile and Licensing tabs), instead of hitting a Page Not Found error.  **Unarchiving — Password cleared when option unchecked** — Disabling Unarchiving now also clears any previously entered archive password, so it cannot be silently carried into subsequent scans.  **Engine timeout fields preserve non-round values** — Sandbox, antivirus, extraction, Deep CDR, DLP, and file-type timeout values from engine profiles are now displayed and retained correctly, even when they don't map to round minute or hour increments.  **Engines list — Active status reflects workflow usage** — Engines referenced by custom workflows are now correctly marked as Active, instead of incorrectly appearing as inactive.  **Engines page — Layout no longer clips horizontally** — Engine configuration now displays cleanly on supported viewport widths, without horizontal content clipping.  **Non-ASCII filenames preserved through UI uploads** — File names with non-ASCII characters submitted via the UI now preserve their encoding consistently with scans performed via other interfaces.  **Adaptive Sandbox — Summary aligns with Sandbox verdict** — Summary banners now correctly report "No Threat" when the Sandbox returns a clean verdict, instead of showing an undetermined placeholder.  **Archive extraction — Clearer failure wording** — Fail-extraction conditions now display "unsupported extraction method" wording that matches the actual Archive Extraction behavior, making errors easier to interpret.  **Accessibility improvements** — Multiple accessibility fixes have been applied across the application, including readable labels on Profile form inputs, accessible names on Licensing pricing plan controls, improved text contrast on Resources documentation cards in light theme, and removal of nested interactive controls between Licensing and Notifications. |
| API   - Release date - Released based on each region's maintenance window timeframe. - Version - 4.76.0 - Release date: 4.22.2026 - Version - 4.76.1 | New Features and Enhancements in 4.76.0  **Public Maintenance Status API** — A new public, read-only endpoint (`GET /v4/status/maintenance`) provides machine-readable maintenance status per region, making it easier to incorporate platform health into your own automation, dashboards, or status pages.  **Sandbox verdicts on organization scan history** — Organization-level scan history now displays Sandbox verdicts inline with engine results, matching the existing behavior on personal scan history.  **Sandbox events now forwarded to SIEM** — Sandbox analysis outcomes for both files and URLs are now included in the SIEM event stream, giving security operations centers complete visibility into sandbox activity alongside other scan events.  **Improved response time for the file scan API** — Reduced internal logging overhead on the `/v4/file` endpoint so that observability operations no longer add latency to the request path.  Fixed in 4.76.0  **Sanitization no longer stuck in Processing for CDR-only archive scans** — Resolved intermittent cases where CDR-only archive scans completed at the engine level but appeared stuck in Processing at the platform level (progress frozen near 99%).  **Sandbox scanning of raw S3 URLs no longer fails** — Sandbox scans submitted with a raw S3 URL no longer return an error.  **Sandbox archive scans no longer miss extracted files** — Archive sandbox reports now consistently include all extracted child file entries.  **Sandbox-only scans no longer leave extracted files In Progress** — Extracted artifacts in sandbox-only flows now reach a terminal state instead of remaining at 0% / In Progress indefinitely.  **SIEM forwarding recovers reliably after upstream failures** — Resolved a failure mode where SIEM forwarding workers could become unresponsive following an upstream messaging crash. Workers now terminate and restart correctly.  Fixed in 4.76.1  **SIEM event delivery to Direct MSK restored** — Resolved an issue where SIEM events forwarded to per-tenant could be dropped before reaching the destination. Events now flow reliably to all configured topics. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### March 2026

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - March 4th - Version - 2.8.3 - Release date - March 18th - Version - 2.9.1 - Release date - March 25th - Version - 2.10.0 | New Features and Enhancements in 2.8.3  **Custom Workflows — Visual Canvas for Engine Configuration** — Security workflows can now be built and managed on an interactive visual canvas. Enable or disable engine nodes individually, configure them via a side drawer, and connect them using conditional routing paths — giving you full control over how files move through your security stack. Multiscanning, Deep CDR, DLP, Sandbox, Archive Extraction, and more are all supported.  **Custom Workflows — Conditional Allow/Block Nodes** — Workflows now support conditional routing nodes that allow or block files based on file size, type (PDF, DOCX, ZIP, EXE, MIME types, etc.), hash, filename pattern, or regex. The right files reach the right engines — and nothing else. Conditional nodes are available before the Sandbox engine and at the final workflow exit.  **Custom Workflows — Engine Profiles** — Engine configurations can now be saved as named, reusable profiles, making it easy to apply consistent settings across multiple workflows without reconfiguring from scratch. Profiles support full create/read/update/delete, version history, duplication, and locking for default and system profiles.  **Custom Workflows — Engine Profile Summary View** — Every engine node on the canvas now displays a clear, human-readable summary of its active configuration — engine count, rules, timeouts, and detected actions — alongside a status badge and an Edit button. Understanding what a workflow is configured to do is now immediate.  **Custom Workflows on the Analyze Page** — Custom workflows are now available directly from the Analyze page. Select any workflow from the dropdown and it's applied as the active scan rule when submitting a file.  Fixed in 2.8.3  **Organization name now shown in place of raw organization ID** — The URL and UI now display the organization's name instead of its internal ID, improving readability across multi-org accounts.  **Limit notifications now reflect the correct billing interval** — Accounts with monthly limits now receive monthly limit reached notifications instead of daily limit messages.  **"View Advanced Analysis" button disabled until sandbox completes** — The button is now unavailable until the sandbox result is successfully generated, preventing users from reaching an infinite loading state if the process is aborted.  **Sandbox scan results now display correctly on the Threats Prevented page** — Sandbox results that previously appeared blank are now rendered correctly.  **File password correctly included when using drag-and-drop upload** — When a user enters an archive password and uploads via drag and drop, the password is now always included in the scan request, ensuring extraction succeeds.  **Sandbox available for all supported URL types** — URL types supported for sandbox analysis are no longer incorrectly restricted in the UI. The sandbox option is now available for all eligible URLs.  **File sizes now displayed in decimal units** — File sizes are displayed using decimal units (1 MB = 1,000,000 bytes), matching documented behavior and user expectations.  **"User Removed from Organization" notification now saves correctly** — A missing field in the request payload was preventing this notification setting from being persisted. Changes now save as expected.  **Duplicate limit notification no longer shown** — When reputation limit consumption reached 50%, two identical notifications appeared in the dropdown. Only one notification is now shown.  **Dragging a deleted file no longer causes infinite loading** — If a user drags a previously downloaded file that has since been deleted into the upload area, the UI now correctly identifies the file as inaccessible and does not attempt to initiate a scan.  New Features and Enhancements in 2.9.1  **Deep CDR — File Type settings expanded and aligned** — File Type engine configuration now matches the full set of supported backend options. Obsolete or non-functional fields have been removed, and additional controls are now exposed where relevant — including fallback behavior, detection options, and block/classification settings.  **Workflow conditional routing — Stricter validation on Allow paths** — Conditional Allow paths in workflows now reject invalid filename patterns at configuration time. Misconfigurations are caught in the UI before they reach a scan.  **Clearer error message for unsupported IP scans** — IP scan requests that the API cannot process now return a clear, descriptive message in the UI instead of a generic failure.  Fixed in 2.9.1  **Custom scan options** — Missing engine selection now flagged — If no scanning engine is selected when submitting a custom scan, the UI now surfaces a proper validation error instead of silently defaulting to a multiscan profile.  **Custom scan options — Unarchiving now combines correctly with other engines** — When Unarchiving is selected alongside Deep CDR, Sandbox, DLP, and/or Private Scan, the resulting scan now correctly reflects the full combination of selected options.  **Stripe checkout redirect corrected** — Users are now sent to the expected post-purchase page after completing Stripe checkout, instead of an incorrect destination.  **Sandbox threat indicators restored** — Threat indicators that were missing from the Sandbox results view are now displayed again.  **Drag-and-drop no longer triggers unintended scans** — Dragging certain UI icons into the upload area no longer initiates a scan.  **Sanitization page — Duplicate block removed and capitalization corrected** — A duplicate "Unused Objects" block has been removed, and inconsistent capitalization on type section headers has been fixed.  **Scan result cards** — Consistent formatting — Button text formatting is now consistent across scan result cards, and "Download Sanitized Data" uses the correct icon.  **OAuth2 clients — Pagination fixed** — Pagination on the OAuth2 clients page now works as expected.  **RSA key — Corrected error message** — The error message shown for invalid or problematic RSA key input has been corrected.  **Rename Workflow dialog — Stable layout** — The Rename Workflow dialog no longer resizes or jumps while typing the new name.  **Deep CDR File Type Settings — Layout overlap resolved** — Overlapping text and controls on the Deep CDR File Type Settings panel have been resolved; labels and controls are now readable.  **Archive child file names — Clearer truncation** — File names for archive child files now use end truncation instead of middle truncation in the side menu, making them easier to read at a glance.  New Features and Enhancements in 2.10  **postMessage integration for embedded UI** — When MetaDefender Cloud is embedded as an iframe within a parent site, the embedded UI now broadcasts navigation and usage events to the parent page via `postMessage`. This keeps parent-site analytics accurate and avoids double-counting events.  **NPS feedback banner** — A Net Promoter Score feedback banner is now available on the dashboard, making it easier to share product feedback directly from within the application.  Fixed in 2.10  **Japanese localization improvements** — Additional UI strings are now translated when the interface language is set to Japanese, reducing remaining English text on key screens.  **Sanitization Details — Consistent dark theme styling** — The Sanitization Details view now uses the same card and hover styling as the Data Loss Prevention Details view in dark theme, for visual consistency.  **Advanced Analysis — Stable tab URLs** — Tab state on the Advanced Analysis page now uses a single, normalized URL parameter; switching tabs no longer accumulates duplicate parameters in the address bar.  **Adaptive Sandbox workflow node** — Timeout displayed correctly — The timeout value shown on the Adaptive Sandbox workflow node now matches the selected profile, and related labels have been updated for clarity.  **Conditional workflow node** — Layout no longer overflows — Long hash values and filenames entered in "Add file hashes to allow" and "Add filenames to block" now stay within the layout without overflowing. |
| API   - Release date - 4.75.0 - Version - Released based on each region's maintenance window timeframe. | New Features and Enhancements  **Prevention API** — **Unified consumption per file** — When using engines bundled in the Prevention API package (Multiscanning, Deep CDR, DLP, Country of Origin), only a single API call is now consumed per file. Previously, Deep CDR consumed an additional Prevention limit, leading to higher-than-expected quota usage.  **Private processing now inherited by sub-organizations** — When a sub-organization is created under a parent that has private processing enabled, the setting is now automatically applied to the new sub-organization — no manual configuration needed.  Fixed  **Limit-reached notifications now respect the configured billing interval** — API keys with monthly limits no longer receive misleading "daily limit" notifications. Alerts now align with each account's actual billing cycle.  **Splunk forwarding restored** — Resolved an issue where the Splunk destination failed to receive scan event payloads. Forwarding now works reliably, and payload formatting has been validated across all supported SIEM destinations.  **Hash lookup returns the correct verdict for DLP results** — In certain cases, hash lookups returned a stale verdict from a previous scan instead of the current evaluation. The correct, current result is now returned.  **Sandbox reports no longer return empty for certain files** — Cases where sandbox analysis returned blank reports for specific files have been resolved.  **Hash lookup on rescanned encrypted archives no longer returns "not found"** — Inner files of rescanned encrypted archives are now correctly returned by hash lookup, instead of erroring out as if they didn't exist. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### February 2026

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - - Version - | New Features and Enhancements  Fixed |
| API   - Release date - Released based on each region's maintenance window timeframe. - Version - 4.74.0 | New Features and Enhancements  **SIEM integrations: Microsoft Sentinel and ServiceNow** Security events and scan results from MD Cloud can now be routed directly to Microsoft Sentinel or ServiceNow, feeding your existing SOC workflows without manual export steps. Setup requires connector configuration and credential provisioning on your end — see the integration guide before enabling.  **Per-file sandbox results and lighter reporting** Sandbox scans now return individual verdicts and report URLs for each file, replacing single oversized archive reports. Results are faster to review, easier to act on, and more focused — especially for container content with multiple files.  **Org-wide scan report visibility** Users within your organization can now view scan reports generated by their teammates, subject to your org's access policies. No more re-running scans or manually sharing results to give colleagues visibility during investigations.  **Workflow inheritance for sub-organizations** Workflows defined at the parent organization level can now be propagated to sub-organizations automatically. New teams and business units inherit the right configuration from the start, reducing setup time and keeping policies consistent across your org hierarchy.  **File size enforcement for sandbox scans** Sandbox scans now enforce the file size limits set in your configuration. Files that exceed the threshold are skipped or return a clear status, keeping sandbox capacity protected and scan behavior predictable.  Fixed  Quota accuracy for password-protected archive scans Archive scans submitted with the `filepassword` header now consume quota as expected. Customers who regularly scan password-protected archives will see consistent, predictable usage with no unexpected spikes.  **Sandbox reliability in the ap-southeast-1 region** Sandbox processing in `ap-southeast-1` is now stable and correctly routed. Jobs in this region should complete reliably without failures related to queue configuration. |
| ICAP Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |
| Menlo Plugin   - Release date - - Version - | New Features and Enhancements  Fixed |
| MetaDefender Storage Security Cloud   - Release date - - Version - | New Features and Enhancements  Fixed |

### January 2026

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - TO BE ADDED - Version - TO BE ADDED | New Features and Enhancements  Fixed |
| API   - Released based on each region's maintenance window timeframe. - Version - 4.73.0 | New Features and Enhancements   - Improved performance under heavy URL-validation traffic   Fixed   - **URL scan validation hardening**    - Better detection/handling of invalid URLs and redirect chains (including max-redirect protection).   - Block URL submissions that ultimately resolve (directly or through redirects) to **f**orbidden IP ranges (IPv4/IPv6).   - Notes/impact: Some previously-accepted URLs may now fail validation with clearer client errors; redirect-heavy URLs should fail faster instead of tying up resources. - **Cancellation + long-polling stability**    - Stop/short-circuit long-running polling when scans are cancelled, reducing wasted work under cancellation scenarios. |
| ICAP Cloud | TO BE ADDED |
| Menlo Plugin | TO BE ADDED |
| MetaDefender Storage Security Cloud | TO BE ADDED |

### December 2025

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - Dec 8 - Version - 2.5.0 | New Features and Enhancements   - Improved overall security posture by adding additional hardening measures implemented to increase platform resilience   Fixed   - Resolved issue on items per page is display incorrectly - Resolved issues on UI for AV logos on dark mode - Resolved issue in Org switch option visible for non-org users - Resolved issue in column for Processing Report table - Resolved alerts when scan fails due to date limit exceeded - Resolved issues on File Details overview - Resolved issue on Colors on Dashboard - Resolved issue on MDFS Private key payload - Resolved issue on Embedded image in notifications box to be dragged and scanned |
| API   - Version - 4.72.0 - Released in Dec 17 based on each region's maintenance window timeframe. | New Features and Enhancements   - Add sandbox_id on /v4/file/{data_id} endpoint - Support for multiple password within archives   Fixed   - Resolved issue on hash lookup to return results with final verdicts - Handle invalid request URLs - Resolved failures during the formatting of SIEM messages - Fixed issue on Filename header URL-encoding to properly handle decoding of accented characters |
| ICAP Cloud | TO BE ADDED |
| Menlo Plugin | TO BE ADDED |
| MetaDefender Storage Security Cloud | TO BE ADDED |

### November 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - Nov 12 - Version - 2.3.0 |  | New Features and Enhancements   - Improved overall security posture by adding additional hardening measures implemented to increase platform resilience - **Added Volume Heat Map to the Usage page** A new heat map visualization is now available on the Usage page, providing clearer insights into volume patterns and activity trends. - **Added Usage & Trends to the Usage page** New insights and trend metrics have been introduced on the Usage page to help visualize activity and usage patterns over time. |
| API   - Version - 4.71.0 - Released in Nov 19 based on each region's maintenance window timeframe. |  | New Features and Enhancements   - **Added SIEM integrations for ELK Stack and IBM QRadar** The solution now supports log forwarding to ELK Stack and IBM QRadar for enhanced security monitoring - Improved overall security posture by adding additional hardening measures implemented to increase platform resilience - S3 URL handling has been updated from bucket-in-path to the modern virtual-hosted–style format for improved compatibility. - Enhancements to hash-based reputation checks improve detection accuracy and consistency. - **OAuth Client ID now included in scan result logs** Logging visibility has been improved by adding the OAuth Client ID to scan result entries. - **Added new verdict types to the Sandbox service** Expanded verdict categories provide clearer classification and more granular scan results.   Fixed   - **Resolved issue causing “Unknown” verdict when scan result exceeded global timeout** The correct verdict is now returned even when scans hit the global timeout threshold. - **Corrected sanitization verdicts** Verdicts displayed after sanitization now accurately reflect the correct results. |
| ICAP Cloud |  | TO BE ADDED |
| Menlo Plugin |  | TO BE ADDED |
| MetaDefender Storage Security Cloud |  | TO BE ADDED |

### October 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - Oct 2 - Version - 2.1.0 - Release date - Oct 22 - Version - 2.2.0 |  | Fixed in 2.1.0 version   - Resolved an issue on hash lookup when the hash doesn’t have a corresponding sandbox result - Resolved an issue on the incorrect verdict for Sandbox when performing URL Analysis - Resolved Status Mapping on the UI - Resolved issue on Sandbox results to be displayed when accessing from Reports   New Features and Enhancements in 2.1.0 version   - Support for Scan History added at Organization level - Added the Scan Result Report to the external release notes   Fixed in 2.2.0 version   - Resolved an issue on misleading Metascan results for infected archive files. - Resolved issue with Drag&Drop functionality. - Resolved issue where the new UI did not display an authorization message when accessing unauthorized scan result links. - Resolved typos in the Reports.   New Features and Enhancements in 2.2.0 version   - Added placeholders on chats with no data added. |
| API   - Version - 4.69.2 - Released in Oct 8 based on each region's maintenance window timeframe. - Version - 4.70.0 - Released based on each region's maintenance window timeframe. |  | New Features and Enhancements in 4.69.2   - Improvements on internal logic to prevent disconnections on large archives   Fixed in 4.69.2   - Resolve issue on main archive sanitization status stuck at in progress   New Features and Enhancements in 4.70.0   - Enhance OAuth2 Endpoints to Support Organizations   Fixed in 4.70.0   - Resolved issues on archive files - Resolved issue for file scanning when files were submitted with downloadFrom - Resolved issue on DLP to return the correct value for archive files |
| ICAP Cloud |  | TO BE ADDED |
| Menlo Plugin |  | TO BE ADDED |
| MetaDefender Storage Security Cloud |  | TO BE ADDED |

### September 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - Sep 24 - Version - 2.0.0 |  | New Features and Enhancements  We’re excited to announce a complete overhaul of our metadefender.opswat.com user interface.  We rethought the entire UI to make navigation easier and your day-to-day use more seamless. |
| API   - Version - 4.68.2 - Released in Sep 8 based on each region's maintenance window timeframe. - Version - 4.69.0 |  | New Features and Enhancements in 4.68.2   - Improved logs for Domain/IP/URL Reputation service - Improved logs for Dynamic Analysis   Fixed in 4.69.0   - Resolved an issue so that organization history now shows activity from its members - Resolved an issue so aborted Sandbox scans are now logged with the correct reasons - Resolved an issue that occurred when scanning a file exceeding set limits - Resolved an issue so aborted Sandbox scans now show the correct verdict in the description - Resolved issue where scanning unsupported file versions with CDR-only now returns the correct result code.   New Features and Enhancements in 4.69.0   - Organization admins can now view submission history across the entire organization, including sub-organizations - Improved Sanitization Results aggregation for archive files with partial failures |
| ICAP Cloud |  | TO BE ADDED |
| Menlo Plugin |  | TO BE ADDED |
| MetaDefender Storage Security Cloud |  | TO BE ADDED |

### August 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - N/A - Version - N/A |  | Nothing this month |
| API   - Version - 4.67.1 - Released in Aug 5 based on each region's maintenance window timeframe. - Version - 4.68.1 including 4.68.0 - Released as per the schedule above |  | New Features and Enhancements in 4.67.1   - Optimize POST /v4/file handler to reduce high response times causing 408s timeouts - Scan results verdict added on hash lookup access log   Fixed in 4.67.1   - Resolved an issue where scans of raw S3 URLs using downloadFrom would remain stuck in progress.   New Features and Enhancements in 4.68.1   - **Improved overall security posture** by addressing recently identified vulnerabilities. - **Crowdstrike** is now removed from the Antivirus Engine packages   Fixed in 4.68.1   - Resolved 400 response issue on DownloadFrom case - Resolved issue on Sandbox response to have additional_info included - Resolved issue on hash lookup cache mechanism when scanning archive files - Resolved issue on long processing time for some scans - Resolved issue on value for ‘stored’ not being updated |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

### July 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - July 23, 2025 - Version - 1.99.0 |  | Fixed   - Fixed 500 Internal Server Error when handling safe redirects with IPv6 addresses.   New Features and Enhancements   - Addressed vulnerabilities to strengthen overall security. - **Policy Update**: Updated link to the latest Terms of Service. |
| API   - Version - 4.67.0 - Released as described in the table above |  | New Features and Enhancements   - **Faster Processing**: Improved performance across multiple functions for quicker response times. - **Scan History Optimization**: Added `organization_id` to Scan Results for better filtering and performance. - **Improved overall security posture** by addressing recently identified vulnerabilities.   Fixed   - Resolved an issue where scan result was stuck at 99% - **API Fix**: Resolved permission issue on `/v4/file/{hash}/download` endpoint. |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - July 23, 2025 - Version - 1.99.0 |  | Fixed   - Fixed 500 Internal Server Error when handling safe redirects with IPv6 addresses.   New Features and Enhancements   - Addressed vulnerabilities to strengthen overall security. - **Policy Update**: Updated link to the latest Terms of Service. |
| API   - Version - 4.67.0 - Released as described in the table above |  | New Features and Enhancements   - **Faster Processing**: Improved performance across multiple functions for quicker response times. - **Scan History Optimization**: Added `organization_id` to Scan Results for better filtering and performance. - **Improved overall security posture** by addressing recently identified vulnerabilities.   Fixed   - Resolved an issue where scan result was stuck at 99% - **API Fix**: Resolved permission issue on `/v4/file/{hash}/download` endpoint. |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

### June 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - June 25, 2025 - Version - 1.97.1 |  | Fixed   - Nothing this month   New Features and Enhancements   - Addressed vulnerabilities to strengthen overall security. |
| API   - Version - 4.66.0 - Released as described in the table above |  | New Features and Enhancements   - **Enhanced the API Key Scan History endpoint** by adding `start_date` and `end_date` as supported query parameters. - **Improved performance** by reducing the processing time specific functions. - **Added dataquery parameter support** to the `/v4/feed/hashes` and `/v4/feed/false-positives` API endpoints. - **Improved overall security posture** by addressing recently identified vulnerabilities.   Fixed   - Resolved an issue where `process_info.result.verdict` could fail when the file exceeded the maximum number of archive files or the maximum archive size. - Resolved an issue affecting `process_info.post_processing.actions_ran` handling. - Updated `final_verdict.threatLevel` to return an integer value consistently. - Resolved an issue where a callback was attempted with an invalid or missing URL (`ERR_INVALID_URL`). - Fixed an issue retrieving vulnerability data via the `GET Vulnerability Lookup` API. - Resolved an issue affecting `sandbox final_verdict.confidence` accuracy or consistency. |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

### May 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - May 14, 2025 - Version - 1.96.0 |  | Fixed   - Resolved issue on the Sandbox verdict name   New Features and Enhancements   - MTCWallets IOC type included - Extracted Strings page updated with interesting strings marker - Reputation service is printing the service in column to highlight the difference between offline and OPSWAT reputation |
| API   - Version - 4.65.1 - Released as described in the table above |  | New Features and Enhancements   - Ability to share scan results within the same organization when using private processing - You can now add up to 25 API Clients when using Bring Your Own Identity Provider (BYOIdP)   Fixed   - Resolved issue on inconsistent variable types when querying `/file/{dataId}` - Resolved issue on prevention limit consumption when using `multiscan_sanitize` custom workflow. |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## April 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - April 10, 2025 / April 17, 2025 - Version - 1.94.0 / 1.95.0 |  | Fixed   - Resolved issue on the UI for Sandbox verdict in case of Benign files - 1.94.0 - Resolved issue on the UI on Dashboard to have the data loaded correctly when selecting different time spans - 1.95.0   New Features and Enhancements   - Items reorganized on the top menu on the landing page on the UI - 1.94.0 - Improved mechanism for Sandbox verdict aggregation - 1.95.0 |
| API   - Version - 4.64.0 - Released as described in the table above |  | New Features and Enhancements  Fixed   - Resolved an issue where the `total_detected_avs`field was missing from bulk hash lookup results. - Fixed a problem with the alerting mechanism that occurred when organizational limits were exceeded. - Resolved issue on the DELETE /v4/hash/{hash}/vote to return 200 when the vote is successfully deleted. |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## March 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - March 12, March 26, 2025 - Version - 1.92.0/1.93.1 |  | Fixed   - Resolved issue on the missing result text on the UI for *OSINT Lookup page* when the engines detect threats - Resolved issue on the pop-up notification to be displayed fully on the UI when opened in the same time with the menu - Resolved the mismatch result on the *Extracted Files* when scanning an archive which is exceeding the depth limit - Fixed Safe-Redirect Issue with OTP URLs.   1.93.1   - Resolved issue on the Deep CDR Result when sanitization was not finished on time   New Features and Enhancements   - Improved messaging and customizable options for Cookie Consent banner on the UI   1.93.1   - InQuest insights are now available for users when scanning IP, URLs, or Domains. - Enhanced the Verdict names on the UI for Adaptive Sandbox - The color for tags on Adaptive Sandbox are now changed |
| API   - Version - 4.63.0 / 4.63.1 / 4.63.1-support - Released as described in the table above |  | New Features and Enhancements   - A new Enterprise-only capability was added that enables direct SIEM integration with Splunk; this allows Enterprise customers to automatically forward security logs related to file scanning and user activity from MetaDefender Cloud API’s Prevention Package to their Splunk instance. - This enhancement provides organizations with a centralized view of security events, enabling faster threat detection, improved compliance and better operational control. More details available on the Use Guide. - Enhanced logging mechanism - introduced in 4.63.1 - Description field from JSON response when using Sanitization changed to "File is sanitized successfully and its structure is validated." - introduced in 4.63.1-support   Fixed   - Resolved an issue where the scan result of a file displayed an incorrect status when an archive exceeded the depth limit. - Resolved an issue with `private_processing` in the sanitization process. - Corrected Error Codes and Response Status to ensure they match as expected. - Resolved issue related to AVs definitions. - Addressed a file name decoding issue that caused certain names to be displayed incorrectly (e.g., as “w^”). - Resolved high queue times when no scan server was available. - Resolved a missing parameter issue when adding a user to an organization. |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## February 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - February 12, 2025 - Version - 1.90.0 - Release date - February 26, 2025 - Version - 1.91.0 |  | Fixed   - Resolved issue on the redirect to Thank You page after purchasing - Resolved issue on the missing alert message when Sandbox URL Analysis exceeds the rate limit - Resolved mismatch result of multiscanning displayed on the Overview page and the results on the Multiscanning page, as well as for the Extracted Files page - Resolved issue on the Extracted File page to remove the duplicated value of the SHA512. - Resolved small issues on UI when the language is changed to Japanese on 1.91.0 version   New Features and Enhancements   - Improved Security posture of the application. Upgraded multiple packages to enhance security and reliability. - Tooltip implemented for truncated information on 1.91.0 version |
| API   - Version - 4.62.0 - Released as described in the table above |  | New Features and Enhancements   - Improved Security posture of the application. Upgraded multiple packages to enhance security and reliability. - Enhanced the Clear API Keys cache endpoint for improved functionality.   Fixed   - Fixed an issue where the Encrypted Archive verdict could incorrectly overwrite the Password Protected Document verdict in certain cases involving multiple verdicts. - Resolved issue on /v4/feed/hashes endpoint - Fixed an issue where the Sandbox last ID was not updating correctly during update operations. |
| ICAP Cloud |  |  |
| Menlo Plugin  Version 1.6.4 Release date - February 13, 2025 |  | New Features and Enhancements   - `downloadFrom` header has been added, as well as `sanitizedLink` added on GET Result endpoint - File name will be suffixed with `_sanitized` in case sanitization was used |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## January 2025

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - January 8, 2025 - Version - 1.88.0 - Release date - January 23, 2025 - Version - 1.89.0 |  | Fixed   - Fixed error message on the UI in case Dynamic Analysis is not performed - Fixed issue on the UI for Sandbox URL Analysis result of latest scan to not overlay on previous scan result   Fixed on 1.89.0 version   - Fixed issue on the Results page to display the blocked status for exceeded limits propagation - Fixed issue to have the right message displayed when no Sandbox is performed. |
| API   - Version - 4.61.0 - Released as described in the table above |  | New Features and Enhancements   - Enhanced the performance and efficiency of infrastructure components.   Fixed   - Resolved an issue with Archive file types related to prevention limits. - Addressed a problem with the DLP verdict functionality. - Resolved issue on `scan_all_result` when scanning an unsupported file with `cdr_only` rule - Resolved 404 errors type when retrieving scan result from `downloadFrom` |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## December 2024

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - December 3rd - Version - 1.87.1 |  | Fixed   - Fixed issue on the undefined redirect from button on landing page |
| API   - Version 4.60.0 - Released as described in the table above |  | New Features and Enhancements   - Improved API documentation for scan history, hash lookup, and api key limits endpoints. The documentation now includes detailed descriptions and usage instructions. - Improved Security posture of the application. Upgraded multiple packages to enhance security and reliability.   Fixed   - Resolved issue on the Encrypted archive for the verdicts on Sensitive data found - Fixed issue on Archive exceeded limits propagation |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin   - Release date - December 11th - Version 1.6.2 |  | Fixed   - Resolved issue on the file name to be sent as header to MetaDefender Cloud |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## November 2024

| Product Area |  | Release Type |
| --- | --- | --- |
| metadefender.opswat.com   - Release date - November 5th / November 27th - Version - 1.86.0 / 1.87.0 |  | New Features and Enhancements  1.86.0   - UI enhancements to strengthen the security posture. - Upgraded multiple packages to enhance security and reliability.   1.87.0   - Renamed *Informational* Sandbox verdict into *No Threat*   Fixed  1.86.0   - Fixed issue on the nickname by removing the whitespaces.   1.87.0   - Fixed issue on the client name column in Japanese language on the UI - Fixed issue on the number of engines shown in URL Multiscan |
| API   - Version - 4.59.1 including 4.58.3 an 4.59.0 - Released as described in the table above |  | New Features and Enhancements   - Improved API documentation for bulk hash lookup Endpoint. The documentation now includes detailed descriptions and usage instructions. - Improved Security posture of the application. Upgraded multiple packages to enhance security and reliability.   Fixed   - Resolved issue on files password protected with special characters - Resolved issue on URI malformed - Resolved issue on Failed to scan verdict - Resolved issue on Rescan of Password protected documents - Resolved issue on the duplicate verdict displayed for Password protected documents |
| ICAP Cloud |  | Nothing this month |
| Menlo Plugin |  | Nothing this month |
| MetaDefender Storage Security Cloud |  | Nothing this month |

## October 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - October 23 - Version - 1.85.1 | New Features and Enhancements   - UI enhancements to strengthen the security posture   Fixed   - Fixed issue on Safe Redirect for shortURL - Fixed issues on creating the apikey |
| API   - Version 4.57.2/4.58.0/4.58.1 - Released as described in the table above | New Features and Enhancements   - New endpoint for rescan mechanism added - Security Enhancements - Improve API Documentation   Fixed   - Resolved issues on the archive use case when remaining without limits - Resolved issues on the archive use case when a child file is returning *exceeded archive limit* - Resolved issues on the *cdr_options* to be updated when sending requests - Resolved issues on Vulnerability Lookup pagination to return the right values - Resolved issue on Scan History data to match hash lookup data - Fixed issue on showing the right name for Webroot instead of Webroot SMD in results - Fixed issue on inconsistent filename when downloading Sanitized file - Fixed issues on wrong scan result which are sent to webhook |
| ICAP Cloud | Nothing this month |
| Menlo Plugin | Nothing this month |
| MetaDefender Storage Security Cloud | New Features and Enhancements   - **MetaDefender Storage Security Cloud** bring the power of our trusted storage security platform to the cloud, enabling seamless data protection for business transitioning to cloud-based and SaaS environments. MetaDefender Storage Security Cloud delivers centralized security for cloud storage systems, ensuring that all your data is protected in real time, wherever your data is. Starting with this month, OPSWAT also offers a SaaS-native solution which is the perfect fit for organizations looking to leverage the advantages of the cloud while maintaining strong security protocols, hosted alongside our MetaDefender Cloud. |

## September 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - 24th of September - Version - 1.84.0 | New Features and Enhancements   - UI enhancements to enforce the security posture - Changes on the Sandbox result display - Log-in enforcement on Licensing Page is now disabled - Ensure Community submitted links from [metadefender.opswa.com](http://metadefender.opswa.com) will be redirected to [metadefender.com](http://metadefender.com) - Enhancement on Adaptive analysis - Network subpage - OSINT Lookups modifications   Fixed   - Fixed Sandbox bugs within the UI to show the right score - Fixed issue on language switch. |
| API   - Version 4.57.1 - Including changes from 4.57.0 - Released as described in the table above | New Features and Enhancements   - Security enhancements - Enhancements on the structure of sanitization response to include *display_name, file_path, details, reason* - Pagination added on CVE - List endpoint - Operational Security enhancements - Enhancements on GET */apikey/scan-history* endpoint - Logs enhancements   Fixed   - Fixed sanitization failure - Fixed *sanitize_unarchive* scan stuck at 99% - Fixed issues on verdicts to be aligned with the actions. - Fixed issues on the aggregation of verdicts - Fixed issues on the engine lists - Fixed issues on the documentation for dataId bulk lookup - Resolved issues on URL Reputation throttling exception - Resolved issues on Password protected cases with special characters - Resolved issue on Intermittent Payload Validation Failed Errors for Bulk Hash Lookups - Resolved issue on sanitized file */v4/file/converted/data_id* - Resolved issue on Multiple CVE Collection Queries from Community - Resolved issue on Incorrect *sandbox_id* Handling in Hash Lookup Response for Private Scans. |
| ICAP Cloud | Nothing this month |
| Menlo Plugin | Nothing this month |

## August 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - 19th of August - Version - 1.82.0 | New Features and Enhancements  1.82.0   - UI enhancements to ensure the naming consistency   Fixed   - Fixed issue on Safe-redirect - Safe URL redirect is now working as expected for Hebrew ended URL - Fixed issue on Safe-redirect for URL stuck in analyzing forever when the result returns from BE take more than 1 min |
| API   - Version 4.56.0 - Released as described in the table above | New Features and Enhancements   - Security enhancements - Update AV Engine Selection Process - Sandbox is now performing when using downloadFrom - Enhancement for the Corrupt file structure detection - Accuracy of Dashboards and Reported SLAs - Enable additional information support - Enhance file scan statistic logs   Fixed   - Fixed issue found by the Penetration testers - Potential Denial of Service - Fixed issue on Duplicate *Sensitive Data Found* in verdicts - Fixed issue on API Key throttling limit for MetaDefender License types - Fixed issue on the calculation of process_info.progress_percentage - Fixed issue on Hash lookup for bulk hash lookup - Fixed issue on improper filename encoding - Fixed issue on detection of an infected archive - Fixed issue for scanning .rar files which sometimes are taking too long to be scanned - Fixed issue on Lookup returns *Unauthorized* when *private_processing* is disabled |
| ICAP Cloud | New Features and Enhancements   - **MetaDefender ICAP Cloud** is OPSWAT's advanced cloud-based security solution that offers comprehensive threat detection and prevention for network traffic. Started with this month OPSWAT also offers a SaaS-based ICAP service, hosted alongside our MetaDefender Cloud. |
| Menlo Plugin | Nothing this month |

## July 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - 10th of July - Version - 1.80.0 - Release date - 24th of July - Version - 1.80.1 | New Features and Enhancements  1.80.0   - UI enhancements and filtering clickable mechanism on MITRE Techniques - UI enhancements for the first annotation for signed URL on [metadefender.opswat.com/licensing](http://metadefender.opswat.com/licensing). *As a recommendation, for requests which are bigger than 1GB, you can include a signed URL of the file, instead of the file itself*   1.80.1   - UI implementation for Cloud Security for Salesforce large file support - more information on *Cloud Security for Salesforce - File Security - Large File Support*   Fixed   - Nothing this month |
| API   - Version 4.55.4 - Released as described in the table above | New Features and Enhancements   - Security enhancements - Updated scan history endpoint structure - Enhance the structure of the sanitization response   Fixed   - Fixed issue on the worker timeout - Fixed issue on vulnerability lookup - Fixed issue on exceeded archive file depth, in case the limit is exceeded the result returned will be code 9 |
| Menlo Plugin | Nothing this month |

## June 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - 19th of June - Version - 1.79.2 | New Features and Enhancements   - UI enhancements for Sandbox to show a preview when hover the elements - Icons added for interesting items on Indicators of Compromise page - Security enhancements - New tags added when collapsing Threat Indicators on Dynamic Analysis section - Two tabs where renamed: *File Details* is now the *File name,* and *Extracted Files Details* is now *Extracted Files* - Two new tabs where added: *OLE Streams* and *Downloaded Files* under Dynamic Analysis - If a string has a *triggeredConsumerIDs* we will display which one, or the threat indicator verdict for *Extracted Strings Subpage* and *Overview Page > Suspicious* - Expend All/Collapse All button added on *Extracted Strings* page - The Notification mechanism has been adjusted to reflect the daily/monthly value - Online Store product names have been changed: Analysis API -> MetaDefender Cloud Sandbox, Prevention API -> MetaDefender Cloud Prevention, Reputation API -> MetaDefender Reputation Service, Threat Intelligence API -> MetaDefender Threat Intelligence   Fixed   - Fixed typos on the Sandbox page - *Is DotNet, Is Packed, Is Digitally Signed* were removed from the UI on the Sandbox page - Fixed issue to not have the DLP page displayed when the file type is not supported - Fixed issues on Logout error - Fixed issue on VBA Stomping to print *false* when it is not true - Fixed issue on line spacing for FileModifiedTimestamps - Fixed font size on *MITRE Techniques* tile |
| API   - Version 4.54.1 - Released as described in the table above | New Features and Enhancements   - New API endpoint was created for url-sandbox - Security enhancements - The Free and unregistered users can now scan up to 3 scans per hour and up to 15 scans per day. - The Free and registered users can now scan up to 9 scans per hour and up to 45 scans per day.   Fixed   - Fixed issue on the worker timeout - Fixed issue on `files_in_archive.progress_percentage`calculation - Fixed issue on vulnerability lookup - Fixed issue on exceeded archive file depth, in case the limit is exceeded the result returned will be code 9 |
| Menlo Plugin | Nothing this month |

## May 2024

| Product Area |  |
| --- | --- |
| metadefender.opswat.com   - Release date - 29th May - Version | New Features and Enhancements   - UI enhancements for Sandbox - Security enhancements - "Threats Detected" message from Sandbox is now "Malicious activity detected" - Malicious and Likely Malicious items are now grouped together under "Malicious" tab - "Informational" is now "No threat" in YARA rule page - "Dynamic Analysis" menu is now "Adaptive Analysis" - "Indicators of Compromise" is now underneath "Emulation Data" - The extracted links from Downloaded Files are now displayed under Extracted Strings - Infrastructure enhancements - Now you have the possibility to go back to My OPSWAT from metadefender.opswat.com - Navigate backwards functionality improvement   Fixed   - Fixed issues on IP Allowed list - The Chrome extension link in the footer of the page was changed - Fixed issue on OSINT Lookup Subpage |
| API   - Version 4.53.0 - Released as described in the table above | New Features and Enhancements   - Private scan is now enabled by default - Failed requests mechanism is now up to date - Improvements were made on the logs and Audit logging - The structure of response result was enhanced for "unsupported version file" case - Security enhancements   Fixed   - Fixed issue on file processing retry mechanism - Fixed issue on Oauth Client and now can be created/deleted successfully - Fixed issues on the message for consumed allocated limits - Fixed issue on scanning encrypted archive without/wrong password to return error code 12 - Fixed issue on 504 Gateway Timeout: API/Bulk Hash Lookup - Fixed issues on file upload - Fixed issue on Sandbox Queue - Fixed issues on ISV enabled api keys |
| Menlo Plugin | Nothing this month |

April 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - 17th of April - Version - 1.77.0 | New Features   - Operational Improvements - mTLS is now supported for PROFESSIONAL customers - Magnify and change the color for Terms of Service and Privacy Policy text on metadefender.opswat.com - Security enhancements |
| API   - Version 4.52.1 - Released as described in the table above | New Features   - API Documentation update for CDR    - missing headers and description added for the main workflows (`multiscan_sanitize`, `multiscan_sanitize_unarchive`)   - `x-file-metadata` header was removed from documentation and code since this header was deprecated. - Infrastructure enhancements - New Investigation on the AV engines on different license tiers and different workflows. - Security enhancements   Fixed   - Fixed issue to return positive values for `total_detected_avs` - Fixed issue on scan history endpoint timeout - Fixed 404 errors on GET /v4/file calls - Fixed issue on download link in child `data_id` to have the same value as for `process_info.post_processing.converted_to` - Fixed issue on `sanitized`.`file_path` to have `sanitized`.`result: "Allowed"` when scanning with `downloadfrom_sanitize` rule |
| Menlo Plugin | Nothing this month |

## March 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date - No release this month | New Features  Fixed |
| API   - Version 4.51.0 - Released as described in the table above | New Features  Fixed   - Fixed issue to ensure the seamless processing of file scans - Fixed issues on filetype detection for .tiff files. - Fixed issues on CDR only for encrypted documents with password included - Fixed issues on `extracted_files` for Free and Standard users. - Fixed issues on unarchiving on eml/msg files for Free and Standard users, for `multiscan_unarchive` profile. - Fixed issues on the scans to have `file_info.file_type_category` field for Free and Standard users. - Fixed issues on `failure_reason` to not be present in the result which is sent to webhook - Fixed issues on password protected files for Free and Standard users |
| Menlo Plugin | Nothing this month |

## February 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date February 14, 2023 - Version 1.75.0 | New Features  Fixed   - Resolved issue on the Emulation Data graph - Fixed issue on the Indicators of Compromise (IOCs) table column to have the right alignment - Removed API Key from Chrome Extension and the preview image of the api key is now blurred - Resolves issues on MITRE table - The Tactic column has a `word-break: break-word`prop which is now removed. - The “;“ from the **MITRE Techniques** table title is now removed. - Resolved issues on the overlapping button with the text section - the width of the text section was reduced. |
| API   - Version 4.50.0 - Released as described in the table above | New Features  Fixed   - Fixed issue regarding call back URL when a password-protected file is uploaded with `multiscan_sanitize`rule. - Fixed issue to have the Max Size error in return when trying to submit a file bigger than the expected limit. - Resolved issue on `detected_by` for Extracted Files. - Resolved issue to return the expected result in case of an Archive when Maximum depth of extracted files was reached. - Resolved issue to have “file_type_extension” field displayed in the result for different file types - otf, ttf, woff, cdr, cr2, webp, flac, mkv, mped, ogg, opus, webm. - Resolved issue on quotation mark in the URL for the “filename”. - Fixed issue on downloader error log size. - Resolved issue to not have any null value returned in verdicts. - Fixed issue on the `total_detected_avs` to return the correct value when the file is unknown. |
| Menlo Plugin | Nothing this month |

## January 2024

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date January 17, 2023 - Version 1.74.2 - Release date January 29, 2023 - Version hotfix/1.74.3 | New Features  Fixed   - Resolved issues on the remaining limit status to be displayed with the correct color - Resolved issues to have the table from Indicators of Compromise (IOCs) responsive - Resolved issue on Report Vulnerabilities button and tooltip - Resolved issue on CDR table column alignment - Resolved issue on the DLP result on the pdf report when no detection is found - Resolved issues on the DLP report content and alignment of the column - Resolved issues on the Sandbox verdict typo and file details   Fixed   - The logo for the AV engine, previously identified as 'AegisLab,' has undergone a rebranding and is now associated with the 'Lionic' AV engine. |
| API   - Version 4.49.0 - Released as described in the table above | New Features  Fixed   - Fixed issues on Bulk hash lookup to return the total_detected_avs - CDR is now returning an error when it is not available for a specific API Key/account - Dynamic Analysis public documentation is now up to date - Fixed issues on license limits count for sandbox and prevention consumption - Sanitization for TXT File type on MetaDefender Cloud is now disabled - Resolved issues when getting the results for multiscan_unarchive workflow |
| Menlo Plugin | Nothing this month |

## December 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date December 13, 2023 - Version 1.74.0 | New Features  **DLP PDF Export:**   - - *New Feature:* DLP results now export seamlessly to .pdf.   - *Benefits:* Enhanced portability, detailed security insights on the go.   **Object Details Upgrade:**   - - *What's Improved:* More detailed info on processed objects.   - *Why It Matters:* Deeper data exploration for more control. - **Infrastructure Boost:**    - *Under the Hood:* Performance upgrade with state-of-the-art infrastructure.   Fixed   - Resolved issues on password field when using special characters - Resolved issues on external links where needed - Resolved issues on DLP page - Resolved issue on the available limits for MetaDefender Cloud Organization users - Resolved issue to display results for external hashes - Resolved issues on Indicators of Compromise page - Resolved issue on Deep CDR enablement. Deep CDR will be enabled by default only for Free and Anonymous users. |
| API   - Version 4.48.1 - Released as described in the table above | New Features   - DLP Information added in the MD Cloud API docs <https://docs.opswat.com/mdcloud/metadefender-cloud-api-v4#file-lookupbydataid>   Fixed   - Fixed issues on Sanitized progress of a Child file to return 100% when all scan results are completed - Fixed issue on `progress_percentage` stuck at 99% for an encrypted archive file. - Fixed issue on bulk hash lookup - Fixed issues on binary octet-stream request when uploading PDF. |
| Menlo Plugin | Nothing this month |

## November 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date November 8, 2023 - Version 1.73.0 | New Features   - Enhancements for **Proactive Data Loss Prevention** Feature - UI enhancements - Infrastructure updates   Fixed   - Resolved issues on all images to have attributes added - Resolved issues on external links where needed - Resolved issues on internal links to have Anchor added where needed - Resolved issues on .PDF export to show the Sensitive Data found within a file - Anonymous users are now able to download the Redacted version of the file after using DLP and completing the form. - Resolved issues on extended details link to point to the appropriate "File Details" of the extracted files - Resolved issues on Extended Details information - Resolved issues on images to have these aligned to the left |
| API   - Version 4.47.1 - Released as described in the table above | New Features   - Infrastructure enhancements - Enhancements for **Proactive Data Loss Prevention Engine (DLP)**   Fixed   - Fixed issues on Sandbox license limit reached to not get 429 when send the header together with Multiscanning - Fixed issues on counter for threats detection - Fixed issues on some lookup calls - Fixed issues on Archive verdict aggregation |
| Menlo Plugin | Nothing this month |

## October 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date October 12, 2023 - Version 1.72.0 | New Features   - **Proactive Data Loss Prevention** Feature enabled for all MetaDefender Cloud Users - New information are available within your PDF Export - **Deep CDR and Extracted Files for Static Analysis are now available** - Infrastructure updates - Security enhancements   Fixed   - Resolved issues on the 'Origin' in Summery Overview - Resolved issues on tag hover to display the "i" info icon - Resolved issues on the UI to display proper wording in some cases - "Prevalence" columns removed in IOC subpage - Resolved issues on extracted strings - "Triggered Signal" is now "Threat Indicator" on Extracted Strings subpage - "Indicator of Compromise" description updated - Resolved some typos in the UI - Fixed wording on Online Store |
| API   - Version 4.46.4 - Released as described in the table above | New Features   - A new AV Engine was added on our list for : **Cylance** - Infrastructure enhancements - Security enhancements   Fixed   - Resolved issues on backend and Deep CDR module |
| Menlo Plugin | Nothing this month |

## September 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date September 13, 2023 - Version 1.71.0 | New Features   - Ability to get dynamic analysis results by submitting the file with the 'Adaptive Threat Analysis' enabled - Your session will expire after 15 minutes, if you will close the browser - Placeholder added for 'Overview', 'APKData' pages - Infrastructure updates - Security enhancements   Fixed   - Resolved issues on the UI for the map - Resolved issues on the UI to display properly the scan result for the sanitized file - Resolved issue on polling apk-manifest endpoint when user requests a new scan - Resolved issue on the UI to display the proper message error for Archive file type - Resolved issues on 'Location' and 'Network' pages |
| API   - Version 4.46.0 - Released as described in the table above | New Features   - You can now utilize the ability to see how many requests/minute you have left - You can now sanitize OneNote file using MD Cloud - Infrastructure Enhancements   Fixed   - Resolved issues on PE information - Resolved issues on *scan_result_i* and detected engines to display the correct values - Resolved issue to be able to download a sanitized file if it contains "*,*" in the name - Resolved issue on field *file_type_skipped_scan* to be displayed in hash lookup response - Resolved issues on scanning a repository, and archive files - Added required fields for CRD scan only as per spec definition: *stat_time, total_time, total_avs, total_detected_avs* - Resolved issue to have large files successfully scanned - Resolved issues on EXIF and APK hash lookups to return the right values - Resolved issue when the file exceeded the file depth to return the right value - Exceeded Archive File Depth when the *progress_percentage*: 100 - Resolved issue with the *process_percentage* calculation - Fixed issue to have /v4/hash/{hash}/exif returns ExIf information - Fixed timeout to be triggered in case after 60s any result is not received - Resolved issue with Max archive file number to count the overall total file number of all levels |
| Menlo Plugin | Nothing this month |

## August 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date August 17, 2023 - Version 1.70.0 | New Features   - You can now download your multi-scanning results in a .pdf report from the UI. Check out: <https://docs.opswat.com/mdcloud/operation/scan-result-page> - Private Scanning enabled by default for the Enterprise customers that opted for it - Security enhancements   Fixed   - Resolved issues on the UI for the sanitization page - Resolved issues on the tooling - Resolved issue on the UI for the marker icon on IP location page - Resolved issue on colorways on the Emulation data graph |
| API   - Next Release date September 27, 2023 - Version 4.45.0 | New Features  Fixed |
| Menlo Plugin | Nothing this month |

## July 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date July 10, 2023 - Version 1.69.0 | New Features   - New placeholders for Package Efficacy, Community, Extracted Files, Emulation Data, Thank you, on Store pages - A new product - Threat Intelligence Search API can be purchased via Online Store - Security enhancements   Fixed   - Resolved issues on the UI to have the graph loaded and reflects files that have been submitted - Resolved issues on the UI to check all the links and add external links where appropriate |
| API   - Release date July 26, 2023 - Version 4.44.0 | New Features   - MetaDefender Cloud Prevention API can be purchased from AWS Marketplace - Enhance of Platform infrastructure upgrades and deployments for all environments and regions - Security enhancements   Fixed   - Resolved issues on the scan result to be consistent before and after refreshing the result page - Resolved issues on `file_info.file_type_extension` to be included in the result - Resolved issue on `responseTime` of upload function - Resolved issue to have `total_detected_avs` and `detected_by`synchronized, showing the same value for child file - Resolved issue to have the exceeded archive triggered when the file depth exceeds `max_archive_file_depth` - Resolved issue to have mapping of non-existent file extensions removed and Platform API treats encrypted files extensions accordingly. |
| Menlo Plugin | Nothing this month |

## June 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date June 14, 2023 - Version 1.68.0 | New Features   - Enhance of documentation - Security enhancements - Enhance of UI to have target point to docs.opswat.com in terms of user documentation   Fixed   - Resolved issues on notification pop-up style - Resolved issues on Market share report text - Resolved issues on Store placeholders style - Resolved issue on Summary page to show the table when clicking on Dynamic Analysis |
| API   - Release date June 28, 2023 - Version 4.43.3 | New Features   - Support new MetaDefender Cloud attributes - Infrastructure enhancements - Documentation enhancement - Enable two additional file types for CDR - SPF and WEBM - Enhance of Scan Server file limit by increasing the size   Fixed   - Resolved issues on notification mechanism for Daily Limit for Prevention and Reputation - Resolved issues on the Infrastructure component - Resolved issues on Sanitized flow - Resolved issues on file name to not be affected when the extension is missing |
| Menlo Plugin | Nothing this month |

## May 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date May 10, 2023 - Version 1.67.0 | New Features   - Enhance for the AV engines by changing the name from Cyren to Varist. - Enhance of UI to have target point to docs.opswat.com in terms of user documentation   Fixed |
| API   - Release date May 24, 2023 - Version 4.42.3 | New Features   - Enhance for the AV engines by changing the name form Cyren to Varist.   Fixed   - Resolved issue on filetype response |
| Menlo Plugin | Nothing this month |

## April 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date April 12, 2023 - Version 1.66.0 | New Features   - Enhance Security and Infrastructure by reviewing the tools and Infrastructure - 'Sandbox' replaced with Adaptive Threat Analysis - Enhance for the UI to display the scan result of sanitized file instead of data_id   Fixed   - Resolved issue on UI to have the extracted file results displayed correctly - Resolved issue on Adaptive Threat Analysis UI to have the proper messages in case of an error |
| API   - Release date April 26, 2023 - Version 4.42.0 | New Features   - New file type has been enabled for sanitization on MDCloud - webm - Enhance for Enterprise and Professional Customers in terms of exceeding their limit.   Fixed   - Resolved issue on Suborganization to be able to exceed limit - Resolved issue on S3 files to be deleted when the scan is completed 100% |
| Menlo Plugin   - Release date April 26, 2023 - Version 1.5.0 | New Features   - Infrastructure updates have been made - Enhance of the POST error notification to contain all the expected information - Enhance of the custom error notification   Fixed   - Resolved issues on sanitized result to show the right information |

## March 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date March 8, 2023 - Version 1.65.0 | New Features   - Enhance Security and Infrastructure by reviewing the tools and infrastructure - New Adaptive Threat Analysis added to the Advanced Options on MD Cloud UI   Fixed   - Resolved issues on typos in the UI - Resolved issue on consumed Dynamic Analysis limit users were using Multi Scanning - Resolved issue when display on the UI the extracted file results correctly - Resolved issue on Multiscan result to return the correct message when a scan is aborted |
| API   - Release date March 22, 2023 - Version 4.41.3 | New Features   - Routing mechanism for failover - Infrastructure updates to improve performance   Fixed   - Resolved issues on code 500 error when scanning with rule sandbox only - Resolved issue on 403004 error when submitting files for scanning in some cases |
| Menlo Plugin   - Release date March 8, 2023 - Version 1.4.1 | New Features  Fixed   - Resolved issues on the main flow |

## February 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date February 8, 2023 - Version 1.64.0 | New Features   - Enhance of text on MD Cloud UI after Sanitization - Security Enhancements   Fixed   - Downloading and View content buttons were removed - Resolved issue on Safe Redirect and to have the right target on documentation page and Terms and Conditions page |
| API   - Release date February 28, 2023 - Version 4.41.0 | New Features   - Security Enhancements   Fixed   - Resolved potential bugs |
| Menlo Plugin | Nothing this month |

## January 2023

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com | Nothing this month |
| API   - Release date: January 11, 2023 - Version: 4.40.8 | New Features   - Improved routing for failover regions for paying customers   Fixed   - Resolved issue with missing sanitize result for child files in the archive - Resolved issue where Progress_percentage tag was appearing as decimals in some scans - Resolved issue where users could not use "privateprocessing" header when using OAUTH - Resolved issue where total_detected_avs was showing an incorrect number for child file(s) in an archive |
| Menlo Plugin | Nothing this month |

## December 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: December 14, 2022 - Version: 1.62.0 | Notice   - Sandbox scan via UI is only available for paid users   Fixed   - Resolved layout issue with the summary page of dynamic analysis |
| API   - Release date: December 14, 2022 - Version: 4.40.6 | New Features   - Updated engines for free users   Fixed   - Improved engine timeout - Resolved issue where sanitize did not return result for a child file in a nested archive - Fixed scan result code when scanning a password protected archive without an input password |
| Menlo Plugin | Nothing this month |

## November 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com | No updates this month |
| API   - Release date: November 17, 2022 - Version: 4.40.3 | New Features   - Backend architecture improvements to increase performance   Fixed   - Resolved issue with missing file scan results for children files in a nested archive |
| Menlo Plugin   - Release date November 16, 2022 - Version 1.3.7 | Fixed   - Resolved issue with the uncaught exception error |

## October 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: October 12 & 26, 2022 - Version: 1.61.3 | Fixed   - Updated number of engines on online store page - Prevention API 2000 daily limit product was missing on online store, this has been corrected - Resolved issue with display of Mitre data (for sandbox) - Resolved issue with incorrect message for password protected files |
| API   - Release date: October 5, 2022 - Version: 4.39.1 | New Features   - File type mismatch detection   Fixed   - File type mismatch detection caused issues with some customers, rolled it back shortly after release |
| Menlo Plugin   - Release date October 24, 2022 - Version 1.3.5 | New Features   - Improved logging for easier detection of issues   Fixed   - Resolved issue with file name getting messed up when it contained non-English characters |

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: October 12 & 26, 2022 - Version: 1.61.3 | Fixed   - Updated number of engines on online store page - Prevention API 2000 daily limit product was missing on online store, this has been corrected - Resolved issue with display of Mitre data (for sandbox) - Resolved issue with incorrect message for password protected files |
| API   - Release date: October 5, 2022 - Version: 4.39.1 | New Features   - File type mismatch detection   Fixed   - File type mismatch detection caused issues with some customers, rolled it back shortly after release |
| Menlo Plugin   - Release date October 24, 2022 - Version 1.3.5 | New Features   - Improved logging for easier detection of issues   Fixed   - Resolved issue with file name getting messed up when it contained non-English characters |

## September 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: September 14 & 28, 2022 - Version: 1.61.1 | New Features   - Updated online store with new MD Cloud Standard tier and more options for limits - Multi-level organizations   Fixed   - Added legal disclaimer on online store front - Updated language around who can use private scanning (any paid customer can use it) to reflect updated MD Cloud tiers |
| API   - Release date: - Version: | Nothing |
| Menlo Plugin   - Release date: September 28, 2022 - Version: 1.3.2 | New Features   - Updated logic to show status as "unknown" for file types not supported by CDR - Implemented a CDR only workflow (CDR with no multiscanning) - Support for larger file sizes   Fixed   - Resolved issue with hash lookups done via Menlo UI |

## August 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: August 10, 2022 - Version: 1.59.2 | New Features   - Multi-level organizations view in the UI   Fixed   - Resolved bug with hash lookups - Resolved bug with message in UI for file type mis-match |
| API   - Release date: - Version: | Nothing |

## July 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: July 13, 2022 and July 27, 2022 - Version: 1.59.0 | New Features   - Introduced hash lookup first (before file scanning) for those using unpaid licenses of MD Cloud - New [licensing page](https://metadefender.opswat.com/licensing) to highlight new tiers of MD Cloud   Fixed   - Updated connection with [Online Store](https://metadefender.opswat.com/store) - Fixed incorrect message when user exceeded archive file number |
| API   - Release date: July 27, 2022 - Version: 4.38.0 | New Features   - Backend changes to accommodate the new tiers of MD Cloud |

## June 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: June 8, 2022 and June 22, 2022 - Version: 1.58.0 | Fixed   - Resolved bug on notifications page preventing users from selecting certain options - Resolved error when users tried to access security page in MD Cloud UI |
| API   - Release date: June 8, 2022 - Version: 4.37.0 | Fixed   - Security enhancements - Updated with new geolocation service - Resolved TLS socket error - Resolved bug with sanitized file not opening properly   New Features   - Include total detected AVs in scan results |

## May 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: May 11, 2022 and May 25, 2022 - Version: 1.57.0 | New Features   - Merged security related pages on UI - Mitre Att&ck UI for Sandbox scans - Improved geolocation service   Fixed   - Security enhancements - Database enhancements - Resolved false positive issue with allowlist |
| API   - Release date: May 11, 2022 and May 25, 2022 - Version: 4.36.0 | Fixed   - Security enhancements |

## April 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: Apr 27, 2022 - Version: 1.54.3 | New Features   - Fixed grammatical error on "Thank you for registering" page |
| API   - Release date: Apr 27, 2022 - Version: 4.35.6 | Fixed   - Security enhancements - Backend performance improvements |

## March 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: Mar 9, 2022 - Version: 1.54.2 | New Features   - More inclusive language used throughout the product - Updated statistics on metadefender.opswat.com to reflect growth of OPSWAT   Fixed   - Fixed grammatical error on Settings page |
| API   - Release date: Mar 9, 2022 - Version: 4.34.0 | Fixed   - Updated Sandbox documentation - Improved integration with CrowdStrike store |

## February 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: Feb 7, 2022 - Version: 1.53.4 | New Features   - Patents have been updated on metadefender.opswat.com   Fixed   - Deep CDR score now displays on overview page after scanning zip file - "No Threats Detected" text displays properly on overview page - Fixed broken links on licensing page that go to docs.opswat.com - Fixed market share page - Fixed incorrect curl command provided for Sandbox |
| API   - Release date: Feb 23, 2022 - Version: 4.33.1 | Fixed   - Resolved issue with details section of Sandbox JSON response not showing properly - Resolved issue with progress percentage displaying properly |

## January 2022

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: Jan 20, 2022 - Version: 1.53.1 | New Features   - Admins of an organization can now manage their own notifications independent of the other organization admins   Fixed   - Only admins of an organization will receive notifications |
| API | No release notes this month |

## December 2021

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: Dec 23, 2021 - Version: 1.53.0 | New Features   - Updated metadefender.opswat.com with patents relevant to product - Removed "beta" labels on dashboard and statistics pages after addressing feedback - Improved "suspicious" file warning/notification in scan results   Fixed   - Analysis API limit now shows properly in dropdown menu - Fixed issue with feedback mechanism not displaying as intended |
| API   - Release date Dec 23, 2021 - Version 4.31.0 | New Features   - Replaced old sandbox with new OPSWAT Sandbox   Fixed   - Updated Threat Intelligence Feed documentation - Fixed download error for "large metadata" |

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - Release date: Dec 1, 2021 - Version: 1.52.0 | New Features   - Feedback mechanism for users to let us know what improvements they would like to see to the dashboard and statistics pages - Updated UI for RSA Key management - Organization users can now view both their and their organizations submission information on the dashboard and statistics pages - Updated AV engine names on scan reports - Updated average data breach cost to reflect 2021 numbers   Fixed   - Fixed buttons on Safari browser to match OPSWAT blue - Fixed error with webhook |
| API   - Release date Dec 3, 2021 - Version 4.29.2 | New Features   - Enhanced secure webhook calls for sanitized file   Fixed   - Updated AV engine names to current names |

## November 2021

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - **Release date:** Nov 10, 2021 - **Version:** 1.51.0 | New Features   - Notifications and Alerts: allows admins of organizations to get notified via email or in app for.    - users removed from the organization   - user role changes   - Access attempts outside the IP allowlist   - when certain % thresholds of daily API limits are reached   - Users added to the organization   Fixed   - Updates to our [licensing table](https://metadefender.opswat.com/licensing) - Fixed scan history pages (before only would show one page even if there were multiple) - Fixed username dropdown menu on metadefender.opswat.com |
| API   - **Release date:** Nov 10, 2021 - **Version:** 4.28.3 | Fixed   - The rescan API has been disabled - The limits/status endpoint now returns organization level limits (instead of account level limits) for those who are part of an organization |

## October 2021

***No releases***

## September 2021

| Product Area | Release Type |
| --- | --- |
| metadefender.opswat.com   - **Release date:** Sept 08, 2021 - **Version:** 1.50.0 | Fixed   - Updated number of commercial engines on licensing page to reflect current agreements - Fixed issue with Mitre Att&ck UI in dynamic analysis - Resolved issue with main header when scrolling |
| API   - **Release date:** Sept 16, 2021 - **Version:** 4.26.6 | New Features   - Improved scan times for commercial and enterprise customers   Fixed   - Resolved issue with v4/apikey/limits endpoint not updating correctly |
