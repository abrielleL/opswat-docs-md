<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/release-notes/release-notes -->

# Release notes

| **Version** | 5.21.0 |
| --- | --- |
| **Release date** | 30 July 2026 |
| **Scope** | This major version introduces a brand new web interface with new dashboard, dark mode, improved accessibility, and refreshed processing result view.  New capabilities include support PostgreSQL v18, Splunk integration (plus install wizard options), Proactive DLP blocking of unsupported file types, redacted filename tokens for outputs. |

Before you upgrade MetaDefender Core:

Making sure to check out the [Known Limitations](/docs/mdcore/v5.21.0/release-notes/release-notes#known-limitations).

## [New Features, Improvements and Enhancements](/docs/mdcore/v5.21.0/release-notes/release-notes#new-features-improvements-and-enhancements)

### [All-new MetaDefender Core interface](/docs/mdcore/v5.21.0/release-notes/release-notes#all-new-metadefender-core-interface)

Meet the all-new interface—designed for speed and comfort. With built-in dark mode, enhanced accessibility support, and seamless interactions, every workflow feels more natural and efficient.

Below are some of the key highlights:

#### [A brand-new, comprehensive dashboard](/docs/mdcore/v5.21.0/release-notes/release-notes#a-brand-new-comprehensive-dashboard)

A completely redesigned dashboard featuring refreshed versions of existing metrics, making it easier to monitor your system, along with brand-new insights such as the CVE Detection Trend.

#### [Easily monitor and submit scans, including split archive submissions](/docs/mdcore/v5.21.0/release-notes/release-notes#easily-monitor-and-submit-scans-including-split-archive-submissions)

#### [New look and feel for the Processing History and Processing Results pages](/docs/mdcore/v5.21.0/release-notes/release-notes#new-look-and-feel-for-the-processing-history-and-processing-results-pages)

#### [Work comfortably in low light with built-in dark mode](/docs/mdcore/v5.21.0/release-notes/release-notes#work-comfortably-in-low-light-with-built-in-dark-mode)

---

### [Splunk integration settings in MetaDefender Core](/docs/mdcore/v5.21.0/release-notes/release-notes#splunk-integration-settings-in-metadefender-core)

A dedicated **Splunk** section in MetaDefender Core makes it easier to connect Core to your Splunk environment. Add and manage Splunk connections, set the log level, allow self-signed certificates when needed.

Users can also integrate with Splunk during installation via Wizard steps.

---

### [Support PostgreSQL v18](/docs/mdcore/v5.21.0/release-notes/release-notes#support-postgresql-v18)

MetaDefender Core now starts supporting PostgreSQL v18 (verified with 18.4).

Bundled PostgreSQL server comes with MetaDefender Core standalone deployment also comes with this new version.

**Note**:

- PostgreSQL v18 itself cannot initialize its database cluster when the Windows system locale name contains non-ASCII characters. For example, Turkish Windows uses the locale `Turkish_Türkiye.1254`, which contains `ü`. Instruction for safe upgrade at [Upgrade to MetaDefender Core 5.21.0 or later on Windows systems with a non-ASCII locale](/docs/mdcore/v5.21.0/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale).
- If your bundle PostgreSQL password contains non-ASCII characters (for example `£`, `€`, or accented letters), the upgrade may fail and prevent console login. ASCII special characters such as `&`, `~`, and `\` are not affected. Before upgrading, change the PostgreSQL password to ASCII-only - please check [Database Management](/docs/mdcore/v5.21.0/configuration/database-management) for change password

---

### [Redacted file name in output filename configuration](/docs/mdcore/v5.21.0/release-notes/release-notes#redacted-file-name-in-output-filename-configuration)

Output filename formatting now supports Proactive DLP redaction results through two new tokens: `${redacted.basename}` and `${redacted.extension}` (available in `short` and `long` formats). These tokens allow for the automatic use of masked filenames across DLP output, Deep CDR sanitized output, and archive tombstone names, ensuring sensitive information is removed from file names. If no redaction occurs, the tokens automatically fall back to the original filename and extension.

---

### [Block unsupported file types in Proactive DLP](/docs/mdcore/v5.21.0/release-notes/release-notes#block-unsupported-file-types-in-proactive-dlp)

Proactive DLP can now be configured to block files it identifies as an "Unsupported File Type", rather than releasing them as "No Threat Detected". This gives security teams stricter control over content that Proactive DLP cannot fully inspect, aligning DLP behavior with fail-closed policies.

---

### [Centralized "Skip by Hash" management via My OPSWAT Central Management](/docs/mdcore/v5.21.0/release-notes/release-notes#centralized-skip-by-hash-management-via-my-opswat-central-management)

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

---

New Prerequisites for Core Modules

Microsoft Visual C++ Redistributable version 14.44 or later is required for version 8.0 of the following modules: File Type, Archive Extraction, Archive Compression, Country of Origin, and Deep CDR.

---

## [Known Limitations](/docs/mdcore/v5.21.0/release-notes/release-notes#known-limitations)

|  |  |
| --- | --- |
| **Bundled PostgreSQL v18 problem with non-ASCII locale name** | PostgreSQL v18 itself cannot initialize its database cluster when the Windows system locale name contains non-ASCII characters.  For example, Turkish Windows uses the locale `Turkish_Türkiye.1254`, which contains `ü`.  Instruction for safe upgrade at [Upgrade to MetaDefender Core 5.21.0 or later on Windows systems with a non-ASCII locale](/docs/mdcore/v5.21.0/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale). |
| **Bundled PostgreSQL v18 problem with non-ASCII password** | If your bundle PostgreSQL password contains non-ASCII characters (for example `£`, `€`, or accented letters), the upgrade may fail and prevent console login. ASCII special characters such as `&`, `~`, and `\` are not affected. Before upgrading, change the PostgreSQL password to ASCII-only: [Database Management](/docs/mdcore/v5.21.0/configuration/database-management) |
| **Displaying issue of Processing History** | In MetaDefender Core v5.21.0, PostgreSQL has problem with some special characters in results returned by engines. As a consequence, Processing History on web console becomes empty in those cases.  This is a displaying issue; your data in database is retained as is, and REST API integrations work properly.  **Upgrading to MetaDefender Core v5.22.0** will resolve this issue. |
| **Some Settings Not Editable When Managed by Central Management (CM7) in version v5.21.0** | When MetaDefender Core v5.21.0 is managed by Central Management v7, the following configurations are read-only and cannot be modified:   - Post Actions - External Scanners - Webhook Authentication   To modify these settings, temporarily disconnect the MetaDefender Core instance from CM7, apply the required configuration locally, then reconnect the instance. |
| **Kubernetes v1.35 or containerd v2.2.0 could not deploy MetaDefender Core images** | This issue is a bug of `containerd` - [containerd issue reported on GitHub](https://github.com/containerd/containerd/issues/12683).  Until the vendor provides a fix, use one of the following mitigations:   - Downgrade containerd to a supported version (e.g., 1.7.x) - Use a Kubernetes node image that does not include containerd 2.2.x - Pin node runtime version in cluster provisioning   More details at [Unable to deploy MetaDefender Core in Kubernetes with containerd engine 2.2.x](/docs/mdcore/v5.21.0/container-deployment/unable-to-deploy-metadefender-core-in-kubernetes-with-containerd) |
| **The 'Proxy server requires password' setting cannot be disabled once it has been enabled** | **This issue has been resolved in** **version 5.14.2.**  In version 5.14.1, there was an issue that prevented disabling the `Proxy server requires password` setting once it has been enabled. As a workaround, you can export the current settings, locate and remove the username and password fields under the relevant proxy configuration, and then import the modified configuration. |
| **Database connection failure occurred in a specific circumstance after upgrading to version 5.11.0** | **This issue has been resolved in version 5.11.1.**  This issue does not affect all cases when upgrading to version 5.11.0.  After applying the authentication method `scram-sha-256` to enhance security for the bundled PostgreSQL, a database connection issue started occurring after the upgrade, in a specific circumstance.   - If the application was previously upgraded from version 5.5.1 or older to version 5.6.0 or newer, this issue will occur when users upgrade to version 5.11.0.   We prepare a Knowledge Base (KB) for troubleshooting the issue and bringing the system back online: [How to troubleshoot an error related to connection to database failing after an upgrade to v5.11.0?](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-troubleshoot-an-error-related-to-connection-to-database-f)  The issue will not occur in the following scenarios:   - Upgrading directly from version 5.5.1 or older to version 5.11.0. - Upgrading from a fresh installation of version 5.6.0 or newer to version 5.11.0. |
| **Archive compression may fail with very large archive files that contain a large number of subfiles** | **This issue has been addressed in version 5.14.0.**  MetaDefender Core has a limitation when compressing very large archive files that contain a high number of subfiles. In our test scenario, it failed when processing an archive with 300,000 or more subfiles. |
| **Reuse processing result by hash might be slow in high-load situations** | **This issue has been resolved in version 5.10.1.**  Since its introduction in version 5.8.0, this feature has helped improve overall performance and reduce significant load when processing similar files.  However, we have realized this feature might run slowly in high-load scenarios against large database sizes. |
| **Temporary files in the resource folder may not be properly cleaned up if the Archive Extraction engine crashes** | Starting from MetaDefender Core version 5.10.1, if the Archive Extraction engine crashes, temporary files from specific extraction transactions may not be properly cleaned up. However, this issue is relatively rare. |
| **Reject importing non-empty required_engines setting** **in containerized environments** | This issue occurs only in containerized environments.  If the config zip file includes non-empty **required_engines** setting, MetaDefender Core will reject the import.  **Workaround:**   1. Extract the config zip file. 2. Open the "`export_settings.json`" and set "`required_engines`" to an empty array. 3. Recompress the files into a new zip. 4. When executing the docker run command, set the following environment variables: `MDCORE_HEALTH_CHECK`, `MDCORE_REQUIRED_ENGINES`. For more details, please refer to [Health Check settings on docker](/docs/mdcore/v5.21.0/container-deployment/docker-image-published-on-opswat-docker-hub#parameter-init-details-environmental-variables--ignition-file) |
| **The Engine Update feature may not work as expected in certain environments** | We have observed that the Engine Update feature may not work properly in an environment protected by a Palo Alto firewall. In the log file, you might find the error message '`SslHandshakeFailedError`'.  If upgrading to the latest version of MetaDefender Core does not solve the issue, please consider setting up [MetaDefender Update Downloader product](https://docs.opswat.com/mddownloader). This product is responsible for downloading engines, and MetaDefender Core will retrieve and update its engines from there. |
| **Stability issues on Red Hat / CentOS systems with kernel version 372.13** | MetaDefender Core version 5.2.1 or later may not function correctly with Red Hat or CentOS operating systems that use kernel 372.13.  Red Hat is addressing the kernel issues. Please try upgrading to kernel version ***372.26***. |
| **PostgreSQL and MetaDefender Core services cannot initialize in certain containerized environments** | **This issue was addressed in version 5.11.1.**  In a containerized environment, MetaDefender Core version 5.2.0 or newer may work properly when:   - The Linux kernel version of the host machine is newer than 4.18.0 including 5.x.y and 6.x.y. - The Docker base image is CentOS 7. - The bundled PostgreSQL database is used (`DB_TYPE=local`).   **Workarounds for older versions:**   1. Switch to using a Docker base image RHEL 8 or Debian. 2. Switch to using a remote PostgreSQL database. |
| **MetaDefender Core's NGINX web server will not start if weak cipher suites are used for HTTPS** | On MetaDefender Core version 5.2.0 and later, OpenSSL 1.x has been replaced by OpenSSL 3.x within the product and its dependencies, including PostgreSQL and NGINX, to enhance security and address known vulnerabilities in OpenSSL 1.x.  However, NGINX's implementation of OpenSSL 3.x in MetaDefender Core enforces strong encryption by rejecting all weak cipher suites. It only accepts "HIGH" encryption cipher suites as defined by OpenSSL <https://www.openssl.org/docs/man1.1.1/man1/ciphers.html>. This means ciphers based on MD5 and SHA1 hashing are no longer supported.  Consequently, if you previously configured MetaDefender Core for HTTPS connections using a weak SSL cipher with your certificate, the service will not start due to NGINX's OpenSSL 3.x security enforcement.  To prevent and remediate the issue before upgrading MetaDefender Core, please refer to the following resources: [HTTPS Failure on MetaDefender Core 5.2.0 (or newer)](/docs/mdcore/v5.21.0/troubleshooting/metadefender-core-service-failed-due-to-weak-cipher). |
| **TCP socket port exhaustion may cause the service trouble, preventing from restarting, and Workflow configuration corrupted** | This issue affected MetaDefender Core (MD Core) version 5.15.0 and earlier and is enhanced starting from version 5.15.1.  TCP socket port exhaustion might be triggered by other applications; for example, MetaDefender KIOSK v4.7.6.3514 (fixed in later releases).  Consequently, MD Core may behave abnormally, corrupt its Workflow Configuration, and fail to restart. |
| **Workflow configuration fails to synchronize from OPSWAT Central Management to MetaDefender Core after creating a new Workflow template** | This issue affects MetaDefender Core versions 5.17.0 and 5.17.1.  Workflow configuration from OPSWAT Central Management will fail to synchronize to MetaDefender Core (MD Core) once a new Workflow template is created.  To restore normal synchronization, the newly created Workflow template must be deleted.  As a workaround for creating new templates on these affected MD Core versions, the Clone Workflow Template feature can be used as an alternative. |
| **Temporary files may persist if an OPSWAT AI Content Inspector scan is canceled** | If a scan is canceled while the OPSWAT AI Content Inspector engine is actively processing, intermediate files may remain in the temporary directory. These files do not affect the current or any subsequent scan results.  **Resolution:** This issue has been fixed in **MD Core 5.20.0**.  **Workaround (if you remain on MD Core 5.19.0):** The temporary files are automatically removed when the OPSWAT AI Content Inspector engine restarts. |
