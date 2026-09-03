<!-- source: https://www.opswat.com/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows -->

# OCM Uses a Complete Certificate Chain with a Private Root CA (Windows)

All commands in this guide use **Windows PowerShell** (5.1 or 7+).

## [Prerequisites](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#prerequisites)

- **MetaDefender Drive v4.4.5 or later** and **OPSWAT Central Management v10 or later**. Reliable HTTPS enrollment between MetaDefender Drive and Central Management v10 using a private root CA requires Drive v4.4.5+; earlier versions can fail the TLS handshake even with a correctly configured chain.
- OpenSSL installed and on `PATH`. Use [Win32 OpenSSL](https://slproweb.com/products/Win32OpenSSL.html) (the full package, not Light) or Git for Windows, which includes OpenSSL at `C:\Program Files\Git\usr\bin\openssl.exe`.
- Windows PowerShell 5.1 or PowerShell 7+.
- Run every command from the **same working directory**.

Create a working folder and move into it:

PowershellCopyNew-Item -ItemType Directory -Force -Path C:\certs | Out-Null
Set-Location C:\certs

If an `openssl req` command reports that it cannot open `openssl.cnf`, set the config path for the current session and try again: `$env:OPENSSL_CONF = "C:\Program Files\OpenSSL-Win64\bin\cnf\openssl.cnf"` (adjust the path to match your installation).

## [1. Generate the Root CA](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#1-generate-the-root-ca)

The root CA is the trust anchor for the whole chain. Keep `root.key` private — anything signed by this key will be trusted.

PowershellCopyopenssl genrsa -out root.key 4096
openssl req -x509 -new -nodes -key root.key -sha256 -days 3650 `
-out root.crt -subj "/CN=MyRootCA"

This creates:

- `root.key` – private key for the root CA
- `root.crt` – self-signed root CA certificate (valid 10 years)

Verify:

PowershellCopyopenssl x509 -in root.crt -noout -subject -issuer -dates
## [2. Generate the Intermediate CA](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#2-generate-the-intermediate-ca)

The intermediate CA is signed by the root and is used to sign the server certificate, so the root key can be kept offline.

Write the extension file with `-Encoding ascii`. A UTF-16/BOM file cannot be read by OpenSSL.

PowershellCopyopenssl genrsa -out intermediate.key 4096
openssl req -new -key intermediate.key -out intermediate.csr `
-subj "/CN=MyIntermediateCA"
Set-Content -Path intermediate.ext -Encoding ascii -Value @"
basicConstraints=CA:TRUE,pathlen:0
keyUsage=critical,keyCertSign,cRLSign
subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid,issuer
"@
openssl x509 -req -in intermediate.csr -CA root.crt -CAkey root.key `
-CAcreateserial -out intermediate.crt -days 1825 -sha256 `
-extfile intermediate.ext

This creates:

- `intermediate.key` – private key for the intermediate CA
- `intermediate.crt` – intermediate CA certificate signed by the root

Verify (expect `CA:TRUE, pathlen:0`):

PowershellCopyopenssl x509 -in intermediate.crt -noout -text | Select-String "CA:|pathlen"
## [3. Generate the Server Certificate](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#3-generate-the-server-certificate)

This is the certificate the OCM server presents to clients. It is an end-entity certificate (`CA:FALSE`), marked for TLS server authentication, and includes a Subject Alternative Name (SAN). Replace `myserver.local` with the FQDN of your OCM server.

**A SAN is required.** MetaDefender Drive rejects a certificate that has a Common Name only and no SAN (this appears as curl error 60). The `server.ext` file below adds the SAN together with the correct key-usage flags.

PowershellCopyopenssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr `
-subj "/CN=myserver.local"
Set-Content -Path server.ext -Encoding ascii -Value @"
basicConstraints=CA:FALSE
keyUsage=critical,digitalSignature,keyEncipherment
extendedKeyUsage=serverAuth
subjectAltName=DNS:myserver.local
"@
openssl x509 -req -in server.csr -CA intermediate.crt -CAkey intermediate.key `
-CAcreateserial -out server.crt -days 825 -sha256 `
-extfile server.ext

This creates:

- `server.key` – private key used by the OCM server
- `server.crt` – server certificate signed by the intermediate CA

Verify that the SAN is present (it must not be empty):

PowershellCopyopenssl x509 -in server.crt -noout -text | Select-String "DNS:|Subject Alternative"X509v3 Subject Alternative Name:
DNS:myserver.local

**Multiple host names or IP addresses:** if the OCM server is reached by more than one name or by IP, list every value in `subjectAltName`, separated by commas, then re-run the signing command in this step. Use `DNS:` for host names and `IP:` for IP addresses, and make sure the certificate's CN is one of the listed names. For example:

PowershellCopySet-Content -Path server.ext -Encoding ascii -Value @"
basicConstraints=CA:FALSE
keyUsage=critical,digitalSignature,keyEncipherment
extendedKeyUsage=serverAuth
subjectAltName=DNS:myserver.local,DNS:myserver,IP:10.0.0.5
"@
## [4. Create the Server Certificate Chain File](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#4-create-the-server-certificate-chain-file)

Clients such as MetaDefender Drive do not fetch missing certificates automatically, so the OCM server must present the complete chain in a single file, in this order: **server, intermediate, root**.

PowershellCopyGet-Content server.crt, intermediate.crt, root.crt | Set-Content server.chain.crt -Encoding ascii

Use `server.chain.crt` on the OCM server, **not** `server.crt` alone. Check the file begins correctly:

PowershellCopyFormat-Hex server.chain.crt | Select-Object -First 100 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F
00000000 2D 2D 2D 2D 2D 42 45 47 49 4E 20 43 45 52 54 49 -----BEGIN CERTI

The first bytes must be `2D 2D 2D 2D 2D` (ASCII `-----`). If they are `FF FE`, the file is UTF-16 — re-run the previous command with `-Encoding ascii`.

## [5. Verify the Chain](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#5-verify-the-chain)

Verify the certificates before configuring OCM. These checks confirm the chain is valid, the private key matches the server certificate, and (after OCM is running) that the server presents the full chain.

PowershellCopy# 1. The server certificate chains up to the root (must print: server.crt: OK)
openssl verify -CAfile root.crt -untrusted intermediate.crt server.crt
# 2. The chain file contains exactly 3 certificates
openssl crl2pkcs7 -nocrl -certfile server.chain.crt | openssl pkcs7 -print_certs -noout
# 3. The private key matches the server certificate (the two lines must be identical)
openssl rsa -noout -modulus -in server.key | openssl sha256
openssl x509 -noout -modulus -in server.crt | openssl sha256
# 4. After OCM is configured: confirm the server presents the full chain.
# Replace <OCM_HTTPS_PORT> with the HTTPS port your OCM server listens on.
echo Q | openssl s_client -connect myserver.local:<OCM_HTTPS_PORT> -showcerts 2>$null | Select-String "s:|i:|Verify return"

Expected results:

- Check 1 prints `server.crt: OK`.
- Check 2 lists exactly **3** certificates (server → intermediate → root).
- Check 3 prints two **identical** SHA-256 lines — this confirms the key matches the certificate.
- Check 4 shows all three certificates and `Verify return code: 0 (ok)`. If only one certificate appears, the OCM server is sending the leaf only and must be reconfigured to use `server.chain.crt`.

## [6. Configure OCM to Use the Chain](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#6-configure-ocm-to-use-the-chain)

Install these two files on the OCM server:

- `server.key` – the private key (from step 3)
- `server.chain.crt` – the full certificate chain (from step 4)

The OCM server must present `server.chain.crt`, not `server.crt` alone. If it sends only the leaf certificate, MetaDefender Drive cannot build the trust chain even when the root CA is already trusted. A web browser may still work because it can complete the chain from its own certificate store; MetaDefender Drive cannot.

## [7. Connect MetaDefender Drive to OCM](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#7-connect-metadefender-drive-to-ocm)

End users do not install the root CA on the MetaDefender Drive operating system. Drive does not expose a shell or trust store on the device, and the OS trust store is read-only. Instead, Drive uses **trust-on-first-use** at the UI: when it sees a server certificate signed by a non-public CA, it prompts the operator to review and accept it once, then adds that certificate to its own trusted store.

On the MetaDefender Drive device:

1. Boot MetaDefender Drive and go to **Settings → Central Management**.
2. Enter the OCM server URL (the FQDN you used in step 3) and the registration code, then click **Connect**.
3. When the **Invalid Certificate** dialog appears with *"This server could not prove itself. Its security certificate is not trusted by your computer's operating system."*, review the server identity (subject, fingerprint), then click* **Proceed**.

MetaDefender Drive Invalid Certificate dialog

Drive adds the OCM server certificate to its internal trusted certificate store. Subsequent connections from the same Drive to the same OCM server are silent until the certificate rotates.

This page does not install the root CA itself on Drive — Drive trusts the server certificate directly. Validating that the certificate is correctly issued and that OCM presents the full chain is done **externally** from any machine with OpenSSL (see step 5, check 4); it is not done from the Drive command line.

## [Full Script (generate-ocm-certs.ps1)](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#full-script-generate-ocm-certsps1)

The script below performs every step in one run. Edit the variables at the top before running it.

PowershellCopy# ============================================================
# generate-ocm-certs.ps1
# Generates Root CA -> Intermediate CA -> Server certificate,
# then builds the full chain file used by the OCM server.
# Edit $FQDN before running.
# ============================================================
$FQDN = "myserver.local" # <-- replace with your OCM server's FQDN
$DAYS_ROOT = 3650
$DAYS_INTER = 1825
$DAYS_SERVER = 825
# If OpenSSL is not already on PATH, point this at its bin folder.
$OpenSslDir = "C:\Program Files\OpenSSL-Win64\bin"
if (Test-Path -LiteralPath $OpenSslDir) { $env:Path += ";$OpenSslDir" }
# Clean up any files from a previous run
Remove-Item *.key, *.crt, *.csr, *.srl, *.ext -ErrorAction Ignore
# --- Root CA ---
openssl genrsa -out root.key 4096
openssl req -x509 -new -nodes -key root.key -sha256 -days $DAYS_ROOT `
-out root.crt -subj "/CN=MyRootCA"
# --- Intermediate CA ---
openssl genrsa -out intermediate.key 4096
openssl req -new -key intermediate.key -out intermediate.csr `
-subj "/CN=MyIntermediateCA"
Set-Content -Path intermediate.ext -Encoding ascii -Value @"
basicConstraints=CA:TRUE,pathlen:0
keyUsage=critical,keyCertSign,cRLSign
subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid,issuer
"@
openssl x509 -req -in intermediate.csr -CA root.crt -CAkey root.key `
-CAcreateserial -out intermediate.crt -days $DAYS_INTER -sha256 `
-extfile intermediate.ext
# --- Server certificate (with SAN) ---
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr -subj "/CN=$FQDN"
Set-Content -Path server.ext -Encoding ascii -Value @"
basicConstraints=CA:FALSE
keyUsage=critical,digitalSignature,keyEncipherment
extendedKeyUsage=serverAuth
subjectAltName=DNS:$FQDN
"@
openssl x509 -req -in server.csr -CA intermediate.crt -CAkey intermediate.key `
-CAcreateserial -out server.crt -days $DAYS_SERVER -sha256 `
-extfile server.ext
# --- Build the chain file (order matters: server, intermediate, root) ---
Get-Content server.crt, intermediate.crt, root.crt | Set-Content server.chain.crt -Encoding ascii
# --- Verify ---
Write-Host "`n=== Verification ===" -ForegroundColor Cyan
openssl verify -CAfile root.crt -untrusted intermediate.crt server.crt
openssl crl2pkcs7 -nocrl -certfile server.chain.crt | openssl pkcs7 -print_certs -noout
Write-Host "`nFiles ready:" -ForegroundColor Green
Write-Host " OCM server key : server.key"
Write-Host " OCM server chain : server.chain.crt"
Write-Host " Drive trust root : root.crt"
## [Troubleshooting](/docs/mddrive/advanced-usages/ocm-https-certificates-rootca-windows#troubleshooting)

| Symptom | Cause | Fix |
| --- | --- | --- |
| `unable to get local issuer certificate` | OCM presents only the leaf certificate, or the root CA is not trusted on Drive | 1. Confirm OCM uses `server.chain.crt` (step 5, check 4). 2) On Drive, re-run the connection and accept the **Invalid Certificate** prompt (step 7) so Drive adds the server certificate to its trusted store. |
| Certificate rejected by Drive (curl error 60) | The server certificate has no SAN | Regenerate `server.crt` with the `server.ext` file from step 3 (it contains `subjectAltName`). |
| Key and certificate do not match | `server.key` does not correspond to `server.crt` | Run step 5 check 3 — the two SHA-256 lines must match. If not, regenerate the pair. |
| A browser reports the certificate is valid, but Drive still fails | The browser completes the chain from its own store; Drive cannot | Configure OCM to send the full chain (`server.chain.crt`) during the TLS handshake. |
| `openssl` is not recognized | OpenSSL is not on PATH | Install the full Win32 OpenSSL package, or add its `bin` folder to PATH (the full script does this via `$OpenSslDir`). |
| `Can't open ... openssl.cnf` | OpenSSL cannot find its configuration file | Set `$env:OPENSSL_CONF` to the bundled `openssl.cnf` (see the note under Prerequisites), then re-run. |
| `unable to load certificate` when building the chain | `server.chain.crt` was written as UTF-16 (BOM present) | Add `-Encoding ascii` to `Set-Content`. The file must start with `2D 2D 2D 2D 2D`, not `FF FE`. |
