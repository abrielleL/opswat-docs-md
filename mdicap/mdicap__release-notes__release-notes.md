<!-- source: https://www.opswat.com/docs/mdicap/release-notes/release-notes -->

# Release Notes

| Version | 5.15.0 |
| --- | --- |
| Release date | 28 Aug 2026 |
| Scope | **Complete verdicts for every file, workload visibility, and secure integration.****Smarter Scan Timeout Handling** — Background scan delivers a final verdict for every file even after a timeout; failover on scan timeout is now configurable.**Heat Map for Scan Workload Visibility** — Spot peak hours, anomalies, and workload trends over the last 30 days.**mTLS Support for MetaDefender Core™** — Connect securely to MD Core instances enforcing mutual TLS.**In-Product ICAP Test Client** — Validate the full scan pipeline directly from the Web UI.**Real-Time Central Management Sync** — MD Core workflows appear instantly when configuring server profiles via My OPSWAT Central Management |

Important Upgrade Notice

Before upgrading MetaDefender ICAP Server to v5.10.0 or newer from v5.6.0 or earlier, make sure you review the [Release Notes](/docs/mdicap/release-notes/release-notes#known-limitations) and the following Documentation:

1. [PostgreSQL Database Deployment Options](/docs/mdicap/installation/installation-postgresql-options)
2. [Installation Methods](/docs/mdicap/installation/installation-methods)
3. [Upgrade to MetaDefender ICAP Server v5.7.0 or newer](/docs/mdicap/installation/upgrade-to-version-5-7-0-steps)
### [New Features, Improvements and Enhancements](/docs/mdicap/release-notes/release-notes#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| **Heat Map for Scan Workload Visibility** | A new interactive **Heat Map** visualizes scan request patterns and load intensity over time, helping operators detect peak hours, anomalies, and workload trends across the last 30 days — supporting day-to-day monitoring and capacity planning.**Scan Requests & Files Views** — Switch between heat maps of ICAP scan requests and processed files to analyze traffic from both perspectives.  **Action Distribution** — See how outcomes are distributed (Allowed, Blocked, Malformed Request, and more), with a detailed per-verdict action breakdown in each cell. |
| **Smarter Scan Timeout Handling** | Scan timeout behavior is now more flexible, giving you both a definitive verdict for every file and faster final decisions when timeouts are intentional.**Background Scan on Timeout** — Previously, when scanning exceeded the configured timeout, the ICAP client immediately received the configured timeout verdict (Blocked by default, or Allowed if overridden to preserve system availability), and the in-flight scan was canceled — so the actual scan result of the file was never known. With the new **background scan** option enabled, the configured timeout verdict is still returned to the client immediately, but scanning continues in the background — ensuring every file submitted for scanning eventually receives a final verdict.      **Failover on Scan Timeout — Now Configurable** — By default, when a scan request times out on one scan server, it fails over to the next scan server in the server profile. For large or complex files that consistently time out, this means the request traverses every scan server before a final verdict is reached, significantly delaying the response. Since scan timeouts are typically configured intentionally, you can now **switch off failover on scan timeout**: the first timeout immediately produces the final verdict and ends the scan process. |
| **Secure MetaDefender Core Integration with mTLS** | MetaDefender ICAP Server can now connect to MetaDefender Core instances that enforce mutual TLS, satisfying zero-trust and regulated-environment requirements.      Supporting this, mTLS certificates and TLS configuration can now be exported and imported for easier migration and multi-node rollout, and the Certificate page indicates when a certificate is currently in use to prevent accidental removal. Client certificates used for mTLS connections are managed under **Library > mTLS Certificate** |
| **In-Product ICAP Test Client** | Validate your deployment end-to-end without external ICAP tooling: send a test file directly from the Web UI and follow it through the full scan pipeline — from ICAP request handling to the MetaDefender Core verdict. Useful for verifying a new installation, confirming configuration changes, and troubleshooting integration issues.  for security reasons, this feature is **disabled by default**. To enable it, set the corresponding flag in the configuration file with **diagnostic section**  (referfor [Linux](/docs/mdicap/configuration/configuration-file#diagnostic-section) or [Windows](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverdiagnostic)) and restart MetaDefender ICAP Server. |
| **Real-Time Server Profile Sync with My OPSWAT Central Management** | When managing MetaDefender ICAP Server through **My OPSWAT Central Management**, the available scan workflows (rules) of a MetaDefender Core instance are now displayed for selection immediately when configuring a server profile. Previously, instances only pushed data up to Central Management and pulled configuration changes on a sync interval — so after adding an MD Core instance from the Central Management UI, you had to save the configuration and wait for the next sync cycle before its workflow list appeared. A new real-time synchronization mechanism for server profiles between ICAP Server and Central Management removes this delay |
| **Usability Improvements** | **ImprovementsConfiguration Search** — Both the **Workflow** and **Settings** pages now include a search box to quickly locate any configuration option.      **Unsaved-Changes Protection** — Switching tabs in the Workflow editor with unsaved changes now prompts for confirmation, preventing accidental loss of edits. **Dynamic Load Balancing by Default** — New deployments now default to dynamic load balancing for server profiles. **Up-to-Date Verdict List** — The verdict list is synchronized with the latest MetaDefender Core releases. |

### [Bug Fixes](/docs/mdicap/release-notes/release-notes#bug-fixes)

|  | **Details** |
| --- | --- |
| **Stale Connection Reuse to MetaDefender Core** | Fixed an issue where the HTTP client could reuse a connection that had been idle for too long, resulting in intermittent scan failures. |
| **Proxy Routing Issues** | Fixed the `/readyz` health endpoint being routed through the proxy even when the proxy was disabled |
| **OCM Enrollment Dropping Web UI Session** | Fixed an issue where the Enroll API returned HTTP 503 when OCM was unreachable, causing the Web UI to drop the active session |
| **NGINX Log Rotation Cleanup Not Working** | Fixed an issue where rotated NGINX log files were not cleaned up as expected, causing disk usage to grow over time |
| **Minor Fixes** | Resolved various UI cosmetic issues and minor fixes |

### [Known Limitations](/docs/mdicap/release-notes/release-notes#known-limitations)

|  | Details |
| --- | --- |
| **Log Rotation Not Functioning on Windows** | Log rotation failed to function correctly on Windows systems.**Impact:** Introduced in v5.13.0**Resolution:** Fixed in v5.14.0 and newer. |
| **Proxy Configuration** | Currently, HTTPS proxy configuration is not supported. |
| **SAML Directory (SSO Integration) Limitations** | In v5.5.0, users cannot create a new SAML directory via the web UI.   - **Workaround**: Use REST API to create the SAML directory - **Impact**: Existing SAML directories remain unaffected after upgrading to v5.5.0 - **Resolution**: Fixed in v5.5.1 and newer |
| **Stability Issues on Red Hat/CentOS (Kernel Version 372)** | MetaDefender ICAP Server v5.1.0 or newer may encounter stability issues on Red Hat/CentOS systems running **kernel version 372**.  **Solution**: Upgrade to **kernel version 425**, where Red Hat has resolved this issue. |
| **MetaDefender ICAP Server's NGINX Web Server Fails to Start with Weak Cipher Suites for HTTPS** | From v5.1.0, OpenSSL 1.x has been replaced with OpenSSL 3.x — across the product and its dependencies — to enhance security and address vulnerabilities.  As part of this upgrade, NGINX's OpenSSL 3.x in MetaDefender ICAP Server now enforces stricter cipher policies and rejects all weak cipher suites. The web server now only accepts "HIGH" encryption cipher suites <https://www.openssl.org/docs/man1.1.1/man1/ciphers.html> (MD5 and SHA1 hashing based are also not accepted).  As a result, if you have already configured MetaDefender ICAP Server for HTTPS using a weak SSL cipher with your certificate, the server will not start due to the enforced security policies in NGINX's OpenSSL 3.x. |
| **no_proxy Configuration** | Starting with MetaDefender ICAP Server v5.1.0, the `no_proxy` setting must support CIDR for IP addresses. For more details, see [No Proxy configuration](/docs/mdicap/configuration/internet-connection#no-proxy-configuration). |
| **TLS Connectivity to MetaDefender Core on Debian** | On Debian OS, MetaDefender ICAP Server v5.1.0 requires the two following commands to enable TLS communication with MetaDefender Core:  **sudo mkdir -p /etc/pki/tls/certs/**  **sudo ln -s /etc/ssl/certs/ca-certificates.crt /etc/pki/tls/certs/ca-bundle.crt**  **Resolution:** Upgrade to **MetaDefender ICAP Server v5.1.1**, where the issue is resolved. |
| **TLS 1.3 Not Supported on Windows Server 2012** | TLS 1.3 is not supported on Windows Server 2012 due to limitations with Schannel SSP. [Reference](https://learn.microsoft.com/en-us/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp-) |
