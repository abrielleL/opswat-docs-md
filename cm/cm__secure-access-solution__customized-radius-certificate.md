<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/customized-radius-certificate -->

# Customized RADIUS certificate

## Overview

This guide explains how to configure custom RADIUS server certificates on NAC Edge for EAP authentication. Using a custom certificate provides better security and allows you to use certificates with longer validity periods than the default OPSWAT certificate.

### Benefits of Custom RADIUS Certificates

- **Longer Validity Period**: Use certificates valid for 2+ years, reducing maintenance frequency
- **Enterprise Integration**: Use certificates issued by your organization's Certificate Authority
- **Better Security**: Stop relying on shared default certificates
- **Client Trust**: Domain-joined clients automatically trust AD-issued certificates
- **Compliance**: Meet organizational security and compliance requirements

### Supported EAP Methods

Custom certificates work with all EAP protocols:

- EAP-TLS (Certificate-based authentication)
- EAP-PEAP (Protected EAP with MSCHAPv2/GTC)
- EAP-TTLS (Tunneled TLS)

---

## Prerequisites

Before configuring a custom RADIUS certificate, ensure you have:

1. **Server Certificate File** (.pem format)

- Must be in PEM (Base64-encoded) format
- Should include Subject and Issuer information
- Must have valid dates (not expired)

2. **Private Key File** (.key format)

- Must be in key format
- **Must be unencrypted** (no password protection)
- Must match the server certificate

3. **CA Certificate** (for client devices)

- The Certificate Authority that issued your server certificate
- Needed for client trust configuration

4. **Administrator Access**

- Permission to modify NAC Edge configuration
- Access to My OPSWAT Central Management console

---

## Part 1: Generating Self-Signed Certificates

### Generate Using OpenSSL

```bash
##Step 1. Generate CA key and cert

		openssl genrsa -out ca.key 4096
		openssl req -new -x509 -days 3650 -key ca.key -out ca.pem   -subj "/C=US/ST=YourState/L=YourCity/O=YourOrg/CN=YourOrg-RADIUS-CA"

	##Step 2. Generate server key and CSR
		openssl genrsa -out server.key 2048
		openssl req -new -key server.key -out server.csr   -subj "/C=US/ST=YourState/L=YourCity/O=YourOrg/CN=radius.yourdomain.com"

	##Step 3. Create extensions file for server cert
    "cat > server_ext.cnf << EOF
    basicConstraints = CA:FALSE
    keyUsage = digitalSignature, keyEncipherment
    extendedKeyUsage = serverAuth
    subjectAltName = DNS:radius.yourdomain.com
		EOF"

  ##Step 4. Sign server cert with CA
		openssl x509 -req -in server.csr -CA ca.pem -CAkey ca.key   -CAcreateserial -out server.pem -days 730 -sha256   -extfile server_ext.cnf
```

**Important**: Replace `radius.yourdomain.com` with your actual RADIUS server hostname or IP.

---

## Part 2: Upload Custom Certificate to NAC Edge

### Step 1: Access NAC Edge Configuration

1. Log in to **My OPSWAT Central Management** console
2. Navigate to **RADIUS NAC** → **Configuration**
3. Select your **Edge Type**
4. Click on **Authentication Methods** tab

### Step 2: Enable Authentication Methods

1. Check the box:  **Enable Authentication Methods**
2. Scroll to the **Server Certificate (for EAP Authentication)** section

### Step 3: Upload Server Certificate

1. In the **Server Certificate** section:

- Click **Upload certificate .pem files only**
- Select your server certificate file (e.g., `radius-server.pem`)
- Click **Open**

### Step 4: Upload Private Key

1. In the **Private Key** section:

- Click **Upload private key .key files only**
- Select your private key file (e.g., `radius-server.key`)
- Click **Open**

### Step 5: Apply Configuration

1. Click the **Apply** button at the top of the page
2. Wait for the notification: **"Authentication Methods has been updated"**
3. The NAC Edge will automatically:

- Update FreeRADIUS configuration
- Restart RADIUS service with new certificate
- Begin using the custom certificate for all EAP authentications

### Step 6: Verify Configuration

**Check Certificate Status:**

- Status should show: ✓ **Custom certificate is configured**
- Default certificate indicator should be removed

---

## Part 3: Configure Client Devices (for EAP-TLS)

For clients to trust your RADIUS server, they must trust the Certificate Authority that issued it.

### For Self-Signed Certificates

Deploy the CA certificate (same as server certificate) to all client devices.

---

### Windows Clients - Manual Configuration

For individual machines or testing:

#### Configure WiFi Profile

1. **System Preferences** → **Network**
2. Select **Wi-Fi** → **Advanced**
3. Remove existing profile (if any)
4. Connect to your SSID
5. Configure 802.1X settings:

- **User Name**: Your username
- **Mode**: Automatic
- **Identity**: Select your client certificate (for EAP-TLS)

6. Click **Trust** when prompted about the server certificate

---

## Part 4: Testing and Verification

### Test Authentication

**On Client Device:**

```powershell
# Windows: Connect to WiFi
netsh wlan connect name="YourSSID"

# Check connection status
netsh wlan show interfaces

# Verify authentication
# Look for: "Authentication: WPA2-Enterprise"
#           "Cipher: CCMP"
#           "State: connected"
```

---

## Troubleshooting

### Issue 1: Certificate Upload Fails

**Error**: "Invalid certificate format"

**Solution**:

- Ensure certificate is in PEM format (Base64-encoded, starts with `-----BEGIN CERTIFICATE-----`)
- Convert DER to PEM: `openssl x509 -inform DER -in cert.der -out cert.pem`
- Check file is not corrupted: `openssl x509 -in cert.pem -noout -text`

---

### Issue 2: Private Key Doesn't Match Certificate

**Error**: "Certificate and private key do not match"

**Solution**:

```bash
# Verify the certificate modulus
openssl x509 -noout -modulus -in radius-server.pem | openssl md5

# Verify the private key modulus
openssl rsa -noout -modulus -in radius-server.key | openssl md5

# The MD5 hashes MUST match
```

---

### Issue 3: Clients Get "Unknown CA" Error

**Error**: Client can't validate server certificate

**Solution**:

1. Verify CA certificate is installed on clients:

# Windows

certutil -store Root | findstr /i "your-ca-name" 2. Ensure wireless profile trusts the correct CA:

- Check GPO wireless policy settings
- Verify "Trusted Root Certification Authorities" has your CA selected

3. Verify server certificate CN matches what clients expect: openssl x509 -in radius-server.pem -noout -subject

---

### Issue 4: Certificate Expired

**Error**: "Certificate has expired"

**Solution**:

1. Generate new certificate with longer validity
2. Upload new certificate following Part 2
3. Apply configuration
4. No need to update clients if CA is still valid

---

### Issue 5: Encrypted Private Key

**Error**: "Encrypted private keys are not supported"

**Solution**:

```bash
# Remove passphrase from private key
openssl rsa -in encrypted.key -out unencrypted.key

# Verify it's unencrypted
openssl rsa -check -in unencrypted.key
# Should not prompt for password
```

---

### Issue 6: Certificate Chain Validation Fails

**Problem**: Server certificate was issued by intermediate CA

**Solution**:

```bash
# Verify certificate chain
openssl verify -CAfile ca.pem server-cert.pem

# Should show: "server-cert.pem: OK"

# If intermediate CA is needed, clients must trust the root CA
# Export root CA from your CA infrastructure
```

---

### Issue 7: Hostname Mismatch

**Error**: Client connects to `10.244.0.150` but certificate CN is `radius.yourdomain.com`

**Solution**:

**Option A**: Add IP to certificate SAN

```bash
# Regenerate certificate with SAN including both hostname and IP
-addext "subjectAltName=DNS:radius.yourdomain.com,IP:10.244.0.150"
```

**Option B**: Configure clients to use hostname

```powershell
# Windows: Update wireless profile to use hostname
# "Connect to these servers": radius.yourdomain.com
```

**Option C**: Add DNS record

```bash
# Create DNS A record: radius.yourdomain.com → 10.244.0.150
```

---

### **Reverting to Default Certificate**

To revert to the default portal.myweblogon.com certificate:

1. Navigate to **Authentication Methods** configuration
2. Click the **Delete** (trash icon) next to "Custom certificate is configured"
3. Confirm deletion
4. Click **Apply**
5. System reverts to default certificate
6. **Note**: Active client connections may be interrupted

---

## Frequently Asked Questions

### Q: Can I use a wildcard certificate (*.yourdomain.com)?

**A**: Yes, wildcard certificates are supported and useful if you have multiple RADIUS servers.

---

### Q: Do clients need the server certificate installed?

**A**: No, clients only need the **CA certificate** (root or intermediate) that issued the server certificate, not the server certificate itself.

---

### Q: Can I use Let's Encrypt certificates?

**A**: Yes, but you need to:

- Own the domain name
- Have the RADIUS server accessible for domain validation (or use DNS validation)
- Renew every 90 days (automate this process)

---

### Q: What happens to existing connections when I change certificates?

**A**:

- Existing connections: Continue with old certificate until client re-authenticates
- New connections: Use new certificate immediately
- Impact is typically minimal

---

### Q: Can I use the same certificate for multiple NAC Edge instances?

**A**: Yes, if the certificate's CN or SAN covers all hostnames/IPs, you can use the same certificate on multiple Edge instances.

---

### Q: How do I automate certificate renewal?

**A**:

- Use API to upload new certificates programmatically
- Integrate with certbot (for Let's Encrypt) or AD CS auto-enrollment
- Schedule renewal checks 30 days before expiration

---

### Q: Does changing the certificate affect HTTPS access to the web UI?

**A**: No, the RADIUS server certificate is only used for EAP authentication (RADIUS). The web UI uses a separate HTTPS certificate.
