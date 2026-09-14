<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/troubleshooting-errors-when-configuring-https-communication-for- -->

# Troubleshooting errors when configuring HTTPS communication for webserver

This article applies to all MetaDefender Storage Security releases deployed on Windows and Linux.

**Issue:**

The MetaDefender Storage Security (MDSS) web GUI is inaccessible via HTTPS despite enabling HTTPS and uploading SSL certificates. Symptoms include:

- The HTTPS enablement script reports SSL certificate validation failure.
- The web browser shows an endless loading loop when trying to connect via HTTPS.

**Root Cause:**

- Depending on the error message when running `mdss.ps1 -u enable_https`:

  - "**WARNING: Invalid certificate structure!**" indicates the SSL certificate is not in the correct PEM format required by MDSS, causing SSL certificate validation to fail (e.g. if the certificate is in DER format, it will cause this error).
  - "**WARNING: Invalid key structure!**" indicates the private key might have been extracted from a .pfx file with a passphrase, which MDSS does not currently support.
- The internal CA certificate also needs to be installed in the Windows "Trusted Root Certification Authorities" store to be trusted by MDSS (or `/etc/mdss/ca_certificates/` on Linux).

**Resolution:**

1. Verify that the SSL certificate and private key are in **PEM format**, indicated by headers such as "-----BEGIN CERTIFICATE-----" and "-----BEGIN PRIVATE KEY-----".
2. If extracting the certificate and private key from the .pfx file, use OpenSSL commands to extract without a passphrase:

   - Extract certificate: `openssl pkcs12 -in certificate.pfx -clcerts -nokeys -out ssl.crt`
   - Extract private key **without passphrase**: `openssl pkcs12 -in certificate.pfx -nocerts -out ssl.key -nodes`
3. Validate the certificate and key formats using OpenSSL:

   - Verify certificate: `openssl x509 -in ssl.crt -text -noout`
   - Verify private key: `openssl rsa -in ssl.key -check` (should output "RSA key ok")
4. Confirm that the MD5 hashes of the certificate and private key match:

   - `openssl x509 -noout -modulus -in ssl.crt | openssl md5`
   - `openssl rsa -noout -modulus -in ssl.key | openssl md5`
5. Ensure the internal CA root certificate is installed in the Windows "Trusted Root Certification Authorities" store so MDSS can trust the certificate chain (or `/etc/mdss/ca_certificates/` on Linux).

   - Refer to: <https://www.opswat.com/docs/mdss/configuration/custom-ca-certificates>
6. Disable HTTPS on MDSS before re-enabling it manually:

   - Run: `mdss.ps1 -u disable_https` (Windows)
   - Copy the validated `ssl.crt` and `ssl.key` files to `C:\Program Files\OPSWAT\MetaDefender Storage Security\config\nginx\certificates` on Windows (or `/etc/mdss/webclient/ on Linux`)
   - Run: `mdss.ps1 -u enable_https` (Windows)
7. Access the MDSS web console via HTTPS URL: `https://`
8. If issues persist, generate and upload a support package for further investigation.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
