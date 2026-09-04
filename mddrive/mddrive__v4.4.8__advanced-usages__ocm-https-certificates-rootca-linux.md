<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux -->

# OCM Uses a Complete Certificate Chain with a Private Root CA (Linux)

All commands in this guide use the **Linux shell (bash)**.

## [Prerequisites](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#prerequisites)

- **MetaDefender Drive v4.4.5 or later** and **OPSWAT Central Management v10 or later**. Reliable HTTPS enrollment between MetaDefender Drive and Central Management v10 using a private root CA requires Drive v4.4.5+; earlier versions can fail the TLS handshake even with a correctly configured chain.
- OpenSSL installed (it is preinstalled on most distributions; otherwise install it with your package manager, e.g. `sudo apt install openssl`).
- A bash shell.
- Run every command from the **same working directory**.

Create a working folder and move into it:

mkdir -p ~/certs && cd ~/certs
## [1. Generate the Root CA](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#1-generate-the-root-ca)

The root CA is the trust anchor for the whole chain. Keep `root.key` private — anything signed by this key will be trusted.

openssl genrsa -out root.key 4096
openssl req -x509 -new -nodes -key root.key -sha256 -days 3650 \
-out root.crt -subj "/CN=MyRootCA"

This creates:

- `root.key` – private key for the root CA
- `root.crt` – self-signed root CA certificate (valid 10 years)

Verify:

openssl x509 -in root.crt -noout -subject -issuer -dates
## [2. Generate the Intermediate CA](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#2-generate-the-intermediate-ca)

The intermediate CA is signed by the root and is used to sign the server certificate, so the root key can be kept offline.

openssl genrsa -out intermediate.key 4096
openssl req -new -key intermediate.key -out intermediate.csr \
-subj "/CN=MyIntermediateCA"
cat > intermediate.ext <<'EOF'
basicConstraints=CA:TRUE,pathlen:0
keyUsage=critical,keyCertSign,cRLSign
subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid,issuer
EOF
openssl x509 -req -in intermediate.csr -CA root.crt -CAkey root.key \
-CAcreateserial -out intermediate.crt -days 1825 -sha256 \
-extfile intermediate.ext

This creates:

- `intermediate.key` – private key for the intermediate CA
- `intermediate.crt` – intermediate CA certificate signed by the root

Verify (expect `CA:TRUE, pathlen:0`):

openssl x509 -in intermediate.crt -noout -text | grep -E "CA:|pathlen"
## [3. Generate the Server Certificate](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#3-generate-the-server-certificate)

This is the certificate the OCM server presents to clients. It is an end-entity certificate (`CA:FALSE`), marked for TLS server authentication, and includes a Subject Alternative Name (SAN). Replace `myserver.local` with the FQDN of your OCM server.

**A SAN is required.** MetaDefender Drive rejects a certificate that has a Common Name only and no SAN (this appears as curl error 60). The `server.ext` file below adds the SAN together with the correct key-usage flags.

openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr \
-subj "/CN=myserver.local"
cat > server.ext <<'EOF'
basicConstraints=CA:FALSE
keyUsage=critical,digitalSignature,keyEncipherment
extendedKeyUsage=serverAuth
subjectAltName=DNS:myserver.local
EOF
openssl x509 -req -in server.csr -CA intermediate.crt -CAkey intermediate.key \
-CAcreateserial -out server.crt -days 825 -sha256 \
-extfile server.ext

This creates:

- `server.key` – private key used by the OCM server
- `server.crt` – server certificate signed by the intermediate CA

Verify that the SAN is present (it must not be empty):

openssl x509 -in server.crt -noout -text | grep -A1 "Subject Alternative Name"X509v3 Subject Alternative Name:
DNS:myserver.local

**Multiple host names or IP addresses:** if the OCM server is reached by more than one name or by IP, list every value in `subjectAltName`, separated by commas, then re-run the signing command in this step. Use `DNS:` for host names and `IP:` for IP addresses, and make sure the certificate's CN is one of the listed names. For example:

cat > server.ext <<'EOF'
basicConstraints=CA:FALSE
keyUsage=critical,digitalSignature,keyEncipherment
extendedKeyUsage=serverAuth
subjectAltName=DNS:myserver.local,DNS:myserver,IP:10.0.0.5
EOF
## [4. Create the Server Certificate Chain File](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#4-create-the-server-certificate-chain-file)

Clients such as MetaDefender Drive do not fetch missing certificates automatically, so the OCM server must present the complete chain in a single file, in this order: **server, intermediate, root**.

cat server.crt intermediate.crt root.crt > server.chain.crt

Use `server.chain.crt` on the OCM server, **not** `server.crt` alone. Check the file begins correctly:

head -n1 server.chain.crt-----BEGIN CERTIFICATE-----

The first line must be `-----BEGIN CERTIFICATE-----`.

## [5. Verify the Chain](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#5-verify-the-chain)

Verify the certificates before configuring OCM. These checks confirm the chain is valid, the private key matches the server certificate, and (after OCM is running) that the server presents the full chain.

# 1. The server certificate chains up to the root (must print: server.crt: OK)
openssl verify -CAfile root.crt -untrusted intermediate.crt server.crt
# 2. The chain file contains exactly 3 certificates
openssl crl2pkcs7 -nocrl -certfile server.chain.crt | openssl pkcs7 -print_certs -noout
# 3. The private key matches the server certificate (the two lines must be identical)
openssl rsa -noout -modulus -in server.key | openssl sha256
openssl x509 -noout -modulus -in server.crt | openssl sha256
# 4. After OCM is configured: confirm the server presents the full chain.
# Replace <OCM_HTTPS_PORT> with the HTTPS port your OCM server listens on.
echo | openssl s_client -connect myserver.local:<OCM_HTTPS_PORT> -showcerts 2>/dev/null | grep -E "s:|i:|Verify return code"

Expected results:

- Check 1 prints `server.crt: OK`.
- Check 2 lists exactly **3** certificates (server → intermediate → root).
- Check 3 prints two **identical** SHA-256 lines — this confirms the key matches the certificate.
- Check 4 shows all three certificates and `Verify return code: 0 (ok)`. If only one certificate appears, the OCM server is sending the leaf only and must be reconfigured to use `server.chain.crt`.

## [6. Configure OCM to Use the Chain](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#6-configure-ocm-to-use-the-chain)

Install these two files on the OCM server:

- `server.key` – the private key (from step 3)
- `server.chain.crt` – the full certificate chain (from step 4)

The OCM server must present `server.chain.crt`, not `server.crt` alone. If it sends only the leaf certificate, MetaDefender Drive cannot build the trust chain even when the root CA is already trusted. A web browser may still work because it can complete the chain from its own certificate store; MetaDefender Drive cannot.

## [7. Connect MetaDefender Drive to OCM](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#7-connect-metadefender-drive-to-ocm)

End users do not install the root CA on the MetaDefender Drive operating system. Drive does not expose a shell or trust store on the device, and the OS trust store is read-only. Instead, Drive uses **trust-on-first-use** at the UI: when it sees a server certificate signed by a non-public CA, it prompts the operator to review and accept it once, then adds that certificate to its own trusted store.

On the MetaDefender Drive device:

1. Boot MetaDefender Drive and go to **Settings → Central Management**.
2. Enter the OCM server URL (the FQDN you used in step 3) and the registration code, then click **Connect**.
3. When the **Invalid Certificate** dialog appears with *"This server could not prove itself. Its security certificate is not trusted by your computer's operating system."_, review the server identity (subject, fingerprint), then click *_Proceed**.

MetaDefender Drive Invalid Certificate dialog

Drive adds the OCM server certificate to its internal trusted certificate store. Subsequent connections from the same Drive to the same OCM server are silent until the certificate rotates.

This page does not install the root CA itself on Drive — Drive trusts the server certificate directly. Validating that the certificate is correctly issued and that OCM presents the full chain is done **externally** from any machine with OpenSSL (see step 5, check 4); it is not done from the Drive command line.

## [Full Script (generate-ocm-certs.sh)](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#full-script-generate-ocm-certssh)

The script below performs every step in one run. Edit the variables at the top before running it.

#!/usr/bin/env bash
# ============================================================
# generate-ocm-certs.sh
# Generates Root CA -> Intermediate CA -> Server certificate,
# then builds the full chain file used by the OCM server.
# Edit FQDN before running.
# ============================================================
set -euo pipefail
FQDN="myserver.local" # <-- replace with your OCM server's FQDN
DAYS_ROOT=3650
DAYS_INTER=1825
DAYS_SERVER=825
# Clean up any files from a previous run
rm -f ./*.key ./*.crt ./*.csr ./*.srl ./*.ext
# --- Root CA ---
openssl genrsa -out root.key 4096
openssl req -x509 -new -nodes -key root.key -sha256 -days "$DAYS_ROOT" \
-out root.crt -subj "/CN=MyRootCA"
# --- Intermediate CA ---
openssl genrsa -out intermediate.key 4096
openssl req -new -key intermediate.key -out intermediate.csr \
-subj "/CN=MyIntermediateCA"
cat > intermediate.ext <<'EOF'
basicConstraints=CA:TRUE,pathlen:0
keyUsage=critical,keyCertSign,cRLSign
subjectKeyIdentifier=hash
authorityKeyIdentifier=keyid,issuer
EOF
openssl x509 -req -in intermediate.csr -CA root.crt -CAkey root.key \
-CAcreateserial -out intermediate.crt -days "$DAYS_INTER" -sha256 \
-extfile intermediate.ext
# --- Server certificate (with SAN) ---
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr -subj "/CN=$FQDN"
cat > server.ext <<EOF
basicConstraints=CA:FALSE
keyUsage=critical,digitalSignature,keyEncipherment
extendedKeyUsage=serverAuth
subjectAltName=DNS:$FQDN
EOF
openssl x509 -req -in server.csr -CA intermediate.crt -CAkey intermediate.key \
-CAcreateserial -out server.crt -days "$DAYS_SERVER" -sha256 \
-extfile server.ext
# --- Build the chain file (order matters: server, intermediate, root) ---
cat server.crt intermediate.crt root.crt > server.chain.crt
# --- Verify ---
echo "=== Verification ==="
openssl verify -CAfile root.crt -untrusted intermediate.crt server.crt
openssl crl2pkcs7 -nocrl -certfile server.chain.crt | openssl pkcs7 -print_certs -noout
echo "Files ready:"
echo " OCM server key : server.key"
echo " OCM server chain : server.chain.crt"
echo " Drive trust root : root.crt"
## [Troubleshooting](/docs/mddrive/v4.4.8/advanced-usages/ocm-https-certificates-rootca-linux#troubleshooting)

| Symptom | Cause | Fix |
| --- | --- | --- |
| `unable to get local issuer certificate` | OCM presents only the leaf certificate, or the root CA is not trusted on Drive | 1. Confirm OCM uses `server.chain.crt` (step 5, check 4). 2) On Drive, re-run the connection and accept the **Invalid Certificate** prompt (step 7) so Drive adds the server certificate to its trusted store. |
| Certificate rejected by Drive (curl error 60) | The server certificate has no SAN | Regenerate `server.crt` with the `server.ext` file from step 3 (it contains `subjectAltName`). |
| Key and certificate do not match | `server.key` does not correspond to `server.crt` | Run step 5 check 3 — the two SHA-256 lines must match. If not, regenerate the pair. |
| A browser reports the certificate is valid, but Drive still fails | The browser completes the chain from its own store; Drive cannot | Configure OCM to send the full chain (`server.chain.crt`) during the TLS handshake. |
| `openssl: command not found` | OpenSSL is not installed | Install it with your package manager, e.g. `sudo apt install openssl` or `sudo yum install openssl`. |
