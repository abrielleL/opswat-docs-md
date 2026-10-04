<!-- source: https://www.opswat.com/docs/mdcore/release-notes/release-notes -->

# Release notes

| **Version** | 5.22.1 |
| --- | --- |
| **Release date** | 15 September 2026 |
| **Scope** | This release includes security upgrades for third-party dependencies (OpenSSL and Libxml2) and addresses UI issues in the all-new MetaDefender Core web console, restoring full engine processing visibility for Deep CDR, Sandbox, Proactive DLP, and Post Actions. |

Before you upgrade MetaDefender Core:

Making sure to check out the [Known Limitations](/docs/mdcore/release-notes/release-notes#known-limitations).

## [New Features, Improvements and Enhancements](/docs/mdcore/release-notes/release-notes#new-features-improvements-and-enhancements)

**Upgraded 3rd party libraries:**

- OpenSSL v3.5.8
- Libxml2 v2.15.4

**Bug Fixes**

Fixed a set of displaying issues introduced with the all-new MetaDefender Core interface in version 5.21.0, where the processing details for several engines showed less information than the previous interface. The following items have been restored and corrected:

- Deep CDR: the *Verdict Explanations* that state why a file received its verdict are shown again on the Sanitization tab, and rows in the sanitization details table can no longer be clicked when they have no further details to show.
- Sandbox: the scan settings tab is available again, the SHA-256 hash and file type are populated in extended details, the severity filter is matched by a visible column, long YARA rule tags are no longer cut off, the severity heading now reads *Verdict*, and the list of detected formats matches the previous interface.
- Proactive DLP: data types with long names are displayed in full, text no longer overlaps, tags are spaced correctly from the results table, the results list respects the selected number of items per page, and the message shown for an unsupported file type links to the list of supported file types again.
- Post actions: the post actions list in the processing result respects the selected number of items per page instead of showing every entry at once.

---

New Prerequisites for Core Modules

Microsoft Visual C++ Redistributable version 14.44 or later is required for version 8.0 of the following modules: File Type, Archive Extraction, Archive Compression, Country of Origin, and Deep CDR.

---

OS support discontinuation

OPSWAT will discontinue support for the following OS in MetaDefender Core and its associated engines:

- Ubuntu 22.04 since **Apr 2027**.

---

## [Known Limitations](/docs/mdcore/release-notes/release-notes#known-limitations)

|  |  |
| --- | --- |
| **Bundled PostgreSQL v18 problem with non-ASCII locale name** | PostgreSQL v18 itself cannot initialize its database cluster when the Windows system locale name contains non-ASCII characters.  For example, Turkish Windows uses the locale `Turkish_Türkiye.1254`, which contains `ü`.  Instruction for safe upgrade at [Upgrade to MetaDefender Core 5.21.0 or later on Windows systems with a non-ASCII locale](/docs/mdcore/troubleshooting/metadefender-core-with-postgresql-18-on-a-non-ascii-os-locale). |
| **Bundled PostgreSQL v18 problem with non-ASCII password** | If your bundle PostgreSQL password contains non-ASCII characters (for example `£`, `€`, or accented letters), the upgrade may fail and prevent console login. ASCII special characters such as `&`, `~`, and `\` are not affected. Before upgrading, change the PostgreSQL password to ASCII-only: [Database Management](/docs/mdcore/configuration/database-management) |
| **Displaying issue of Processing History** | In MetaDefender Core v5.21.0, PostgreSQL has problem with some special characters in results returned by engines. As a consequence, Processing History on web console becomes empty in those cases.  This is a displaying issue; your data in database is retained as is, and REST API integrations work properly.  **Upgrading to MetaDefender Core v5.22.0** will resolve this issue. |
| **Some Settings Not Editable When Managed by Central Management (CM7) in version v5.21.0** | When MetaDefender Core v5.21.0 is managed by Central Management v7, the following configurations are read-only and cannot be modified:   - Post Actions - External Scanners - Webhook Authentication   To modify these settings, temporarily disconnect the MetaDefender Core instance from CM7, apply the required configuration locally, then reconnect the instance. |
| **Kubernetes v1.35 or containerd v2.2.0 could not deploy MetaDefender Core images** | This issue is a bug of `containerd` - [containerd issue reported on GitHub](https://github.com/containerd/containerd/issues/12683).  Until the vendor provides a fix, use one of the following mitigations:   - Downgrade containerd to a supported version (e.g., 1.7.x) - Use a Kubernetes node image that does not include containerd 2.2.x - Pin node runtime version in cluster provisioning   More details at [Unable to deploy MetaDefender Core in Kubernetes with containerd engine 2.2.x](/docs/mdcore/container-deployment/unable-to-deploy-metadefender-core-in-kubernetes-with-containerd) |
| **The 'Proxy server requires password' setting cannot be disabled once it has been enabled** | **This issue has been resolved in** **version 5.14.2.**  In version 5.14.1, there was an issue that prevented disabling the `Proxy server requires password` setting once it has been enabled. As a workaround, you can export the current settings, locate and remove the username and password fields under the relevant proxy configuration, and then import the modified configuration. |
| **Database connection failure occurred in a specific circumstance after upgrading to version 5.11.0** | **This issue has been resolved in version 5.11.1.**  This issue does not affect all cases when upgrading to version 5.11.0.  After applying the authentication method `scram-sha-256` to enhance security for the bundled PostgreSQL, a database connection issue started occurring after the upgrade, in a specific circumstance.   - If the application was previously upgraded from version 5.5.1 or older to version 5.6.0 or newer, this issue will occur when users upgrade to version 5.11.0.   We prepare a Knowledge Base (KB) for troubleshooting the issue and bringing the system back online: [How to troubleshoot an error related to connection to database failing after an upgrade to v5.11.0?](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-troubleshoot-an-error-related-to-connection-to-database-f)  The issue will not occur in the following scenarios:   - Upgrading directly from version 5.5.1 or older to version 5.11.0. - Upgrading from a fresh installation of version 5.6.0 or newer to version 5.11.0. |
| **Archive compression may fail with very large archive files that contain a large number of subfiles** | **This issue has been addressed in version 5.14.0.**  MetaDefender Core has a limitation when compressing very large archive files that contain a high number of subfiles. In our test scenario, it failed when processing an archive with 300,000 or more subfiles. |
| **Reuse processing result by hash might be slow in high-load situations** | **This issue has been resolved in version 5.10.1.**  Since its introduction in version 5.8.0, this feature has helped improve overall performance and reduce significant load when processing similar files.  However, we have realized this feature might run slowly in high-load scenarios against large database sizes. |
| **Temporary files in the resource folder may not be properly cleaned up if the Archive Extraction engine crashes** | Starting from MetaDefender Core version 5.10.1, if the Archive Extraction engine crashes, temporary files from specific extraction transactions may not be properly cleaned up. However, this issue is relatively rare. |
| **Reject importing non-empty required_engines setting** **in containerized environments** | This issue occurs only in containerized environments.  If the config zip file includes non-empty **required_engines** setting, MetaDefender Core will reject the import.  **Workaround:**   1. Extract the config zip file. 2. Open the "`export_settings.json`" and set "`required_engines`" to an empty array. 3. Recompress the files into a new zip. 4. When executing the docker run command, set the following environment variables: `MDCORE_HEALTH_CHECK`, `MDCORE_REQUIRED_ENGINES`. For more details, please refer to [Health Check settings on docker](/docs/mdcore/container-deployment/docker-image-published-on-opswat-docker-hub#parameter-init-details-environmental-variables--ignition-file) |
| **The Engine Update feature may not work as expected in certain environments** | We have observed that the Engine Update feature may not work properly in an environment protected by a Palo Alto firewall. In the log file, you might find the error message '`SslHandshakeFailedError`'.  If upgrading to the latest version of MetaDefender Core does not solve the issue, please consider setting up [MetaDefender Update Downloader product](https://docs.opswat.com/mddownloader). This product is responsible for downloading engines, and MetaDefender Core will retrieve and update its engines from there. |
| **Stability issues on Red Hat / CentOS systems with kernel version 372.13** | MetaDefender Core version 5.2.1 or later may not function correctly with Red Hat or CentOS operating systems that use kernel 372.13.  Red Hat is addressing the kernel issues. Please try upgrading to kernel version ***372.26***. |
| **PostgreSQL and MetaDefender Core services cannot initialize in certain containerized environments** | **This issue was addressed in version 5.11.1.**  In a containerized environment, MetaDefender Core version 5.2.0 or newer may work properly when:   - The Linux kernel version of the host machine is newer than 4.18.0 including 5.x.y and 6.x.y. - The Docker base image is CentOS 7. - The bundled PostgreSQL database is used (`DB_TYPE=local`).   **Workarounds for older versions:**   1. Switch to using a Docker base image RHEL 8 or Debian. 2. Switch to using a remote PostgreSQL database. |
| **MetaDefender Core's NGINX web server will not start if weak cipher suites are used for HTTPS** | On MetaDefender Core version 5.2.0 and later, OpenSSL 1.x has been replaced by OpenSSL 3.x within the product and its dependencies, including PostgreSQL and NGINX, to enhance security and address known vulnerabilities in OpenSSL 1.x.  However, NGINX's implementation of OpenSSL 3.x in MetaDefender Core enforces strong encryption by rejecting all weak cipher suites. It only accepts "HIGH" encryption cipher suites as defined by OpenSSL <https://www.openssl.org/docs/man1.1.1/man1/ciphers.html>. This means ciphers based on MD5 and SHA1 hashing are no longer supported.  Consequently, if you previously configured MetaDefender Core for HTTPS connections using a weak SSL cipher with your certificate, the service will not start due to NGINX's OpenSSL 3.x security enforcement.  To prevent and remediate the issue before upgrading MetaDefender Core, please refer to the following resources: [HTTPS Failure on MetaDefender Core 5.2.0 (or newer)](/docs/mdcore/troubleshooting/metadefender-core-service-failed-due-to-weak-cipher). |
| **TCP socket port exhaustion may cause the service trouble, preventing from restarting, and Workflow configuration corrupted** | This issue affected MetaDefender Core (MD Core) version 5.15.0 and earlier and is enhanced starting from version 5.15.1.  TCP socket port exhaustion might be triggered by other applications; for example, MetaDefender KIOSK v4.7.6.3514 (fixed in later releases).  Consequently, MD Core may behave abnormally, corrupt its Workflow Configuration, and fail to restart. |
| **Workflow configuration fails to synchronize from OPSWAT Central Management to MetaDefender Core after creating a new Workflow template** | This issue affects MetaDefender Core versions 5.17.0 and 5.17.1.  Workflow configuration from OPSWAT Central Management will fail to synchronize to MetaDefender Core (MD Core) once a new Workflow template is created.  To restore normal synchronization, the newly created Workflow template must be deleted.  As a workaround for creating new templates on these affected MD Core versions, the Clone Workflow Template feature can be used as an alternative. |
| **Temporary files may persist if an OPSWAT AI Content Inspector scan is canceled** | If a scan is canceled while the OPSWAT AI Content Inspector engine is actively processing, intermediate files may remain in the temporary directory. These files do not affect the current or any subsequent scan results.  **Resolution:** This issue has been fixed in **MD Core 5.20.0**.  **Workaround (if you remain on MD Core 5.19.0):** The temporary files are automatically removed when the OPSWAT AI Content Inspector engine restarts. |
