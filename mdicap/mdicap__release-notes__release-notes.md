<!-- source: https://www.opswat.com/docs/mdicap/release-notes/release-notes -->

# Release Notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| Version | 5.16.3 |
| --- | --- |
| Release date | 19 Nov 2026 |
| Scope | **Security update: third-party library upgrades**This maintenance release upgrades the bundled NGINX web server to address a recently disclosed vulnerability. It introduces no new features, configuration changes or changes to scanning behavior. We recommend all customers running an earlier version upgrade to this version. |

Important Upgrade Notice

Before upgrading MetaDefender ICAP Server to v5.10.0 or newer from v5.6.0 or earlier, make sure you review the [Release Notes](/release-notes/release-notes#known-limitations) and the following Documentation:

1. [PostgreSQL Database Deployment Options](/installation/installation-postgresql-options)
2. [Installation Methods](/installation/installation-methods)
3. [Upgrade to MetaDefender ICAP Server v5.7.0 or newer](/installation/upgrade-to-version-5-7-0-steps)
### New Features, Improvements and Enhancements

|  | Details |
| --- | --- |
| **Security Enhancements** | Upgraded third-party libraries to address known vulnerabilities:   - NGINX v1.30.7 |

### Known Limitations

|  | Details |
| --- | --- |
| **Log Rotation Not Functioning on Windows** | Log rotation failed to function correctly on Windows systems.**Impact:** Introduced in v5.13.0**Resolution:** Fixed in v5.14.0 and newer. |
| **Proxy Configuration** | Currently, HTTPS proxy configuration is not supported. |
| **SAML Directory (SSO Integration) Limitations** | In v5.5.0, users cannot create a new SAML directory via the web UI.   - **Workaround**: Use REST API to create the SAML directory - **Impact**: Existing SAML directories remain unaffected after upgrading to v5.5.0 - **Resolution**: Fixed in v5.5.1 and newer |
| **Stability Issues on Red Hat/CentOS (Kernel Version 372)** | MetaDefender ICAP Server v5.1.0 or newer may encounter stability issues on Red Hat/CentOS systems running **kernel version 372**.  **Solution**: Upgrade to **kernel version 425**, where Red Hat has resolved this issue. |
| **MetaDefender ICAP Server's NGINX Web Server Fails to Start with Weak Cipher Suites for HTTPS** | Starting in v5.1.0, OpenSSL 3.x replaced OpenSSL 1.x across the product and its dependencies, to improve security and address vulnerabilities.  As part of this upgrade, the NGINX web server in MetaDefender ICAP Server now enforces stricter cipher policies and rejects all weak cipher suites. The web server now only accepts "HIGH" encryption cipher suites <https://www.openssl.org/docs/man1.1.1/man1/ciphers.html> (cipher suites based on MD5 or SHA-1 hashing are also rejected).  As a result, if you have already configured MetaDefender ICAP Server for HTTPS using a weak SSL cipher with your certificate, the server will not start due to the enforced security policies in NGINX's OpenSSL 3.x. |
| **no_proxy Configuration** | Starting with MetaDefender ICAP Server v5.1.0, the `no_proxy` setting must support CIDR for IP addresses. For more details, see [No Proxy configuration](/configuration/internet-connection#no-proxy-configuration). |
| **TLS Connectivity to MetaDefender Core on Debian** | On Debian OS, MetaDefender ICAP Server v5.1.0 requires the two following commands to enable TLS communication with MetaDefender Core:  **sudo mkdir -p /etc/pki/tls/certs/**  **sudo ln -s /etc/ssl/certs/ca-certificates.crt /etc/pki/tls/certs/ca-bundle.crt**  **Resolution:** Upgrade to **MetaDefender ICAP Server v5.1.1**, where the issue is resolved. |
| **TLS 1.3 Not Supported on Windows Server 2012** | TLS 1.3 is not supported on Windows Server 2012 due to limitations with Schannel SSP. [Reference](https://learn.microsoft.com/en-us/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp-) |
