<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode -->

# FIPS 140-3 Validated Mode

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Overview](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#overview)

When **FIPS Mode** is enabled, the web server switches its cryptographic operations to use a **FIPS 140-3 validated cryptographic module**.

Specifically, the system:

- Uses **OpenSSL 3.1.2**
- Activates the **OpenSSL FIPS Provider**
- Reconfigures **nginx** to use a restricted, NIST-aligned TLS configuration
- Enforces modern, FIPS-approved cipher suites
- Generates strong Diffie–Hellman parameters (3072-bit)

This ensures that TLS operations are performed using FIPS-approved cryptographic algorithms and a validated cryptographic module.

Warning

Please make sure to be aware of the delay on first startup after enabling FIPS mode described at [First Startup Behavior](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#first-startup-behavior).

## [Enabled Protocols](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#enabled-protocols)

The nginx configuration is automatically updated to enforce a strict TLS policy aligned with modern NIST recommendations.

### [Enabled TLS 1.3 Cipher Suites](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#enabled-tls-13-cipher-suites)

- **TLS_AES_256_GCM_SHA384**
- **TLS_AES_128_GCM_SHA256**

These use:

- AES-GCM (AEAD)
- SHA-2
- Ephemeral key exchange

### [Enabled TLS 1.2 Cipher Suites](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#enabled-tls-12-cipher-suites)

- **ECDHE-ECDSA-AES256-GCM-SHA384**
- **ECDHE-RSA-AES256-GCM-SHA384**
- **ECDHE-ECDSA-AES128-GCM-SHA256**
- **ECDHE-RSA-AES128-GCM-SHA256**
- **DHE-RSA-AES256-GCM-SHA384**
- **DHE-RSA-AES128-GCM-SHA256**

These provide:

- Forward secrecy (ECDHE / DHE)
- AES-GCM encryption
- SHA-2 integrity

## [Disabled Cipher Categories](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#disabled-cipher-categories)

When FIPS Mode is enabled, the following are disabled:

- Static RSA key exchange (`Kx=RSA`)
- CBC-mode cipher suites
- PSK-based cipher suites
- Legacy and weak protocols

This reduces attack surface and aligns with modern cryptographic best practices.

## [First Startup Behavior](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#first-startup-behavior)

On the first startup after enabling FIPS Mode, the system generates strong Diffie–Hellman parameters. This is required for DHE-based cipher suites and ensures compliance with modern security strength recommendations.

### [Important](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#important)

The generation process:

- Is CPU intensive
- Can take **up to 10 minutes**, depending on system performance
- Happens only once
- Is not repeated on subsequent restarts

During this time, startup may appear delayed.

This is expected behavior.

### [Monitor Startup Process](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#monitor-startup-process)

After enabling FIPS mode, monitor the first startup by checking the `<installation folder>\Services\Logs\opswat.mft.helper.service.log` file. When the log contains the entry `Started Nginx process.`, the FIPS-mode startup process has completed successfully. An example of the log file after enabling FIPS mode is shown below.

opswat.mft.helper.service.logCopy2026-03-02 20:29:43,176 5 INFO Starting MetaDefender Managed File Transfer Helper
2026-03-02 20:29:43,270 5 INFO Adding worker thread NginxMonitor
2026-03-02 20:29:43,270 5 INFO All worker threads have started
2026-03-02 20:29:43,270 6 INFO Starting NginxMonitor worker thread
2026-03-02 20:29:43,379 6 INFO Installing FIPS module for OpenSSL. This may take a while...
2026-03-02 20:29:43,379 6 INFO Executing\: C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\openssl.exe
2026-03-02 20:29:43,379 6 INFO Arguments\: fipsinstall -out "C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\fipsmodule.cnf" -module "C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\fips.dll"
2026-03-02 20:29:43,379 6 INFO Working directory\: C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer
2026-03-02 20:29:43,582 6 INFO Successfully installed FIPS module for OpenSSL
2026-03-02 20:29:43,582 6 INFO Creating DH parameters for FIPS mode. This may take a while...
2026-03-02 20:29:43,582 6 INFO Executing\: C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\openssl.exe
2026-03-02 20:29:43,582 6 INFO Arguments\: dhparam -out "C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\dhparam-3072.pem" 3072
2026-03-02 20:29:43,582 6 INFO Working directory\: C\:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer
2026-03-02 20:50:34,983 6 INFO Successfully generated DH parameters for FIPS mode
2026-03-02 20:50:38,030 6 INFO Started Nginx process.
## [Operational Impact](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#operational-impact)

Enabling FIPS Mode may impact compatibility with older clients.

Clients that rely on:

- TLS 1.0 or 1.1
- RSA key transport
- CBC cipher suites
- Legacy embedded TLS stacks

may fail to connect after FIPS Mode is enabled.

Modern browsers and up-to-date TLS libraries are fully supported.

## [Certificate Compatibility](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#certificate-compatibility)

Existing HTTPS certificates remain valid.

However:

- RSA certificates require `ECDHE-RSA-*` suites (which remain enabled).
- ECDSA certificates require `ECDHE-ECDSA-*` suites (which remain enabled).

Warning

Certificates with RSA keys smaller than 2048 bits or SHA-1/MD5 signatures will be rejected in FIPS mode. Certificates issued before 2015 may need to be reissued to meet FIPS requirements.

## [When to Enable FIPS Mode](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#when-to-enable-fips-mode)

FIPS Mode is recommended when:

- Regulatory compliance requires FIPS 140-3
- Operating in government or regulated environments
- Formal cryptographic validation is required
- A hardened TLS posture is desired

## [Enabling FIPS Mode](/docs/mdmft/v3.11.5/configuration/fips-140-3-validated-mode#enabling-fips-mode)

1. Open **Registry Editor** (`regedit.exe`).
2. Navigate to: `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MetaDefender Vault`
3. Create or modify the **NginxFipsModeEnabled S tring Value (REG_SZ)**: The value must be set to the string `"true"` (case-insensitive).
4. Restart MetaDefender Managed File Transfer™ services. **Please be aware that the first FIPS enabled startup can take significantly longer as some parameters are needed to be generated.**

FIPS mode enabled in registry.
