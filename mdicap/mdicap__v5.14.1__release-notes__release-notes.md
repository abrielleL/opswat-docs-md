<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/release-notes/release-notes -->

# Release Notes

| Version | 5.14.1 |
| --- | --- |
| Release date | 24 Jun 2026 |
| Scope | This release introduces output filename override via ICAP header, security hardening measures, and performance and UI/UX improvements. A product analytics feature is also included to help OPSWAT improve product performance and reliability. |

Important Upgrade Notice

Before upgrading MetaDefender ICAP Server to v5.10.0 or newer from v5.6.0 or earlier, make sure you review the [Release Notes](/docs/mdicap/v5.14.1/release-notes/release-notes#known-limitations) and the following Documentation:

1. [PostgreSQL Database Deployment Options](/docs/mdicap/v5.14.1/installation/installation-postgresql-options)
2. [Installation Methods](/docs/mdicap/v5.14.1/installation/installation-methods)
3. [Upgrade to MetaDefender ICAP Server v5.7.0 or newer](/docs/mdicap/v5.14.1/installation/upgrade-to-version-5-7-0-steps)
### [New Features, Improvements and Enhancements](/docs/mdicap/v5.14.1/release-notes/release-notes#new-features-improvements-and-enhancements)

|  | Details |
| --- | --- |
| **Output filename override via ICAP header** | The output filename for scan results can now be overridden by passing a dedicated **ICAP header**. The specified filename is recorded in the processing history and forwarded to MetaDefender Core.  This can be enabled per workflow configuration. Go to **Workflows** > select **Workflow** > **Overrides And Metadata** > **Override Report** > **Override File Name by Header** |
| **Security Enhancements** | Upgraded third-party libraries and applied additional hardening measures to strengthen overall product security and reduce potential attack surface:   - echarts-for-react v3.0.7 - dompurify v3.4.8 - OpenSSL v3.6.3 - NGINX v1.30.3 |
| **Usage Report** | Optionally reports anonymous usage data about general usage to help OPSWAT improve its products.  more details, refer to [Usage Report](/docs/mdicap/v5.14.1/configuration/aggregated-data-reporting) |
| **Usability Improvements** | - **Enhanced High Availability with Automatic Failover for MetaDefender Core** - Failover is now enabled by default for scan requests that return a `failed` or `not scanned` result from MetaDefender Core. When triggered, the request is automatically reassigned to the next available MetaDefender Core instance within the same server profile, improving scan reliability and reducing the impact of transient processing failures. To disable this behavior, set `failover_failed` and `failover_notscanned` to `false` in the configuration. See [Additional Tuning](/docs/mdicap/v5.14.1/configuration/additional-tuning) for details - **New "Aborted" Status in Processing History**: A new `Aborted` status has been introduced in the processing history to more accurately reflect incomplete file transfer scenarios, replacing previously ambiguous result states:    - ICAP client disconnects before completing file transfer: Status Aborted and result message Client closed the connection   - ICAP client remains connected but stops sending data: Status Aborted and result message Connection timed out (no data received - **Performance** — Reduced unnecessary requests to the PostgreSQL server to improve overall product responsiveness. - **UI/UX** — Applied user interface and experience improvements across the product |

### [Bug Fixes](/docs/mdicap/v5.14.1/release-notes/release-notes#bug-fixes)

|  | **Details** |
| --- | --- |
| **Minor Fixes** | Resolved various UI cosmetic issues and minor fixes |

### [Known Limitations](/docs/mdicap/v5.14.1/release-notes/release-notes#known-limitations)

|  | Details |
| --- | --- |
| **Proxy Configuration** | Currently, HTTPS proxy configuration is not supported. |
| **SAML Directory (SSO Integration) Limitations** | In v5.5.0, users cannot create a new SAML directory via the web UI.   - **Workaround**: Use REST API to create the SAML directory - **Impact**: Existing SAML directories remain unaffected after upgrading to v5.5.0 - **Resolution**: Fixed in v5.5.1 and newer |
| **Stability Issues on Red Hat/CentOS (Kernel Version 372)** | MetaDefender ICAP Server v5.1.0 or newer may encounter stability issues on Red Hat/CentOS systems running **kernel version 372**.  **Solution**: Upgrade to **kernel version 425**, where Red Hat has resolved this issue. |
| **MetaDefender ICAP Server's NGINX Web Server Fails to Start with Weak Cipher Suites for HTTPS** | From v5.1.0, OpenSSL 1.x has been replaced with OpenSSL 3.x — across the product and its dependencies — to enhance security and address vulnerabilities.  As part of this upgrade, NGINX's OpenSSL 3.x in MetaDefender ICAP Server now enforces stricter cipher policies and rejects all weak cipher suites. The web server now only accepts "HIGH" encryption cipher suites <https://www.openssl.org/docs/man1.1.1/man1/ciphers.html> (MD5 and SHA1 hashing based are also not accepted).  As a result, if you have already configured MetaDefender ICAP Server for HTTPS using a weak SSL cipher with your certificate, the server will not start due to the enforced security policies in NGINX's OpenSSL 3.x. |
| **no_proxy Configuration** | Starting with MetaDefender ICAP Server v5.1.0, the `no_proxy` setting must support CIDR for IP addresses. For more details, see [No Proxy configuration](/docs/mdicap/v5.14.1/configuration/internet-connection#no-proxy-configuration). |
| **TLS Connectivity to MetaDefender Core on Debian** | On Debian OS, MetaDefender ICAP Server v5.1.0 requires the two following commands to enable TLS communication with MetaDefender Core:  **sudo mkdir -p /etc/pki/tls/certs/**  **sudo ln -s /etc/ssl/certs/ca-certificates.crt /etc/pki/tls/certs/ca-bundle.crt**  **Resolution:** Upgrade to **MetaDefender ICAP Server v5.1.1**, where the issue is resolved. |
| **TLS 1.3 Not Supported on Windows Server 2012** | TLS 1.3 is not supported on Windows Server 2012 due to limitations with Schannel SSP. [Reference](https://learn.microsoft.com/en-us/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp-) |
