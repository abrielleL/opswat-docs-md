<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-view-ssl-tls-certificate-details-from-the-command-line--w -->

# How to View SSL/TLS Certificate Details from the Command Line (Windows and Linux)

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**Issue:**

When troubleshooting an SSL/TLS certificate issue, you may need to confirm that the certificate contains the required information, such as the Subject Alternative Name (SAN), expiration date, or issuer. You can view these details from the command line on both Windows and Linux without installing additional certificate management tools.

**Solution:**

Use the commands below to print the contents of a certificate file. Both PEM-encoded (`.pem`, `.crt`) and DER-encoded (`.cer`, `.der`) certificates are supported.

**Windows:**

Windows includes the built-in `certutil` tool. Open **Command Prompt** or **PowerShell** and run one of the following.

**Offline environment - Print the certificate details only:**

certutil -dump C:\path\to\cert.cer

**(Optional) For Internet connected environment - Print the certificate details and validate the full certificate chain, including CRL/OCSP revocation checks:**

certutil -verify -urlfetch C:\path\to\cert.cer

**Linux:**

OpenSSL must be installed before you can run the commands in this section. Most distributions include it by default; if not, install it with your package manager.

**Ubuntu / Debian / Linux Mint**

sudo apt install openssl -y

**RHEL / CentOS / Fedora / Rocky Linux**

sudo dnf install openssl -y

Once OpenSSL is installed, run the command that matches your certificate format.

**PEM-encoded certificate:**

openssl x509 -in cert.pem -noout -text

**DER-encoded (.cer) certificate:**

openssl x509 -in cert.cer -inform DER -noout -text
> **Tip:** If you are not sure which format the file is in, open it in a text editor. A PEM file begins with `-----BEGIN CERTIFICATE-----`; a DER file appears as unreadable binary.

### [Verifying the Output](/docs/mdcore/knowledge-base/how-to-view-ssl-tls-certificate-details-from-the-command-line--w#verifying-the-output)

In the output, check the following fields to confirm the certificate is correct:

| Field | What to check |
| --- | --- |
| **Issuer** | The Certificate Authority (or your internal CA) that signed the certificate. For a self-signed certificate, Issuer and Subject are identical. |
| **Subject** | The Common Name (CN) of the server the certificate was issued to. |
| **Not Before / Not After** | The validity period. Confirm the current date falls within this range. |
| **Subject Alternative Name (SAN)** | All hostnames and IP addresses the certificate is valid for. The hostname clients use to connect must appear here. |

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
