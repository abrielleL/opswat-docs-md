<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad -->

# Can we disable legacy TLS ciphers (DES/3DES/RC2/IDEA) on a MetaDefender MFT server to remediate SWEET32 style collision attacks?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**Check Your Version:**

This article applies to all MetaDefender MFT releases deployed on Windows.

## [**Overview**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#overview)

Some vulnerability scanners flag **64-bit block ciphers** (notably **3DES**, also **DES/RC2/IDEA**) as vulnerable to **SWEET32-style collision attacks** when used in TLS/SSL with CBC mode.
These scanners might target the following:

- **Server OS TLS stack configuration** (on Windows: **Schannel**)
- **MetaDefender MFT inbound HTTPS** served by the embedded **NGINX** component.

---

## [**Resolution for MetaDefender MFT NGINX component**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#resolution-for-metadefender-mft-nginx-component)

1. Open nginx.conf in the MFT install directory (e.g. C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\WebServer\nginx.conf)
2. Find the ssl_ciphers line and remove :DES-CBC3-SHA from the end of the cipher list
3. Restart the MFT Web Server service

## [**Resolution for Windows / Schannel**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#resolution-for-windows--schannel)

### [**Option A (recommended): Remove 3DES/DES suites from the allowed cipher suite order (GPO)**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#option-a-recommended-remove-3desdes-suites-from-the-allowed-cipher-suite-order-gpo)

1. Open **Group Policy Management**.
2. Go to:
   **Computer Configuration → Administrative Templates → Network → SSL Configuration Settings**
3. Open **SSL Cipher Suite Order** and set it to **Enabled**.
4. In the cipher suite list, **remove any suites using 3DES/DES/RC2/IDEA** (e.g., names containing `3DES` or `DES`).

This is the preferred enterprise method because it controls what TLS can negotiate at the OS level.

### [**Option B: Disable specific TLS cipher suites via PowerShell (where supported)**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#option-b-disable-specific-tls-cipher-suites-via-powershell-where-supported)

Run PowerShell as Administrator:

- View enabled cipher suites

`Get-TlsCipherSuite`

- Disable a specific legacy suite (example name shown; disable the ones present in your environment)

`Disable-TlsCipherSuite -Name "TLS_RSA_WITH_3DES_EDE_CBC_SHA"`

- `Get-TlsCipherSuite` lists the cipher suites the system can use.
- `Disable-TlsCipherSuite` disables a named suite.
  (Availability depends on Windows version/PowerShell TLS module.)

### [**Option C (scanner-aligned): Disable Schannel ciphers (registry “Ciphers” keys)**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#option-c-scanner-aligned-disable-schannel-ciphers-registry-ciphers-keys)

If your scanner explicitly verifies these registry locations, disable the cipher(s) there as well:

- `HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\Triple DES 168` → `Enabled` = `0`
- `HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\DES 56/56` → `Enabled` = `0`

A reboot may be required for Schannel registry changes to fully apply.

*The above Windows Hardening steps are recommended for Outbound connections only.

## [**FIPS mode note**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#fips-mode-note)

If **FIPS 140-3 Validated Mode** is enabled in MetaDefender MFT, the product documentation states that NGINX is reconfigured to a **restricted, NIST-aligned TLS configuration**, with **CBC-mode cipher suites disabled** and only modern, FIPS-approved suites enabled—so SWEET32/3DES findings on the MFT HTTPS listener are not expected in that mode.

---

## [**Validation**](/docs/mdmft/v3.11.5/knowledge-base/can-we-disable-legacy-tls-ciphers--des-3des-rc2-idea--on-a-metad#validation)

1. **Re-run the vulnerability scan** to confirm if the vulnerabilities are fixed.
2. On Windows, confirm 3DES/DES suites are not enabled/negotiable:

   `Get-TlsCipherSuite | Select-String -Pattern "3DES| DES |RC2|IDEA"`
3. **Test client compatibility** (older clients may fail once 3DES/DES are removed).

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
