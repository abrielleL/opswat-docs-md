<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-create-a-sample-self-signed-certificate-with-san-using-op -->

# How to create a sample self-signed certificate with SAN using OpenSSL

This article is applied to Web Browsers (Chrome, Firefox, etc.) releases deployed on Windows Linux and macOS systems. It is required to use OpenSSL verasion 3.x to execute these steps.

> **Issue:**

Modern web browsers require a Subject Alternative Name (SAN) in SSL/TLS certificates. The Common Name (CN) field, historically used for hostname verification, is deprecated due to compatibility and security concerns. Browsers reject certificates lacking SAN with errors like: “Certificate is not valid for the name.”

**Affected Version/Platforms:** Chrome 58 and later, Firefox, and other modern web browsers.

**Resolution:** To create an sample SSL/TLS certificate for testing purposes with a Subject Alternative Name (SAN), follow these steps:

1. **Create the** `san.cnf` Configuration File:

[ req ]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn
req_extensions = req_ext
[ dn ]
CN = yourdomain.com
[ req_ext ]
subjectAltName = @alt_names
[ alt_names ]
DNS.1 = yourdomain.com
DNS.2 = www.yourdomain.com
DNS.3 = api.yourdomain.com

2. **Generate the CSR and Private Key:**

openssl req -new -nodes -out request.csr -newkey rsa:2048 -keyout private.key -config san.cnf

3. **(Optional) Verify SAN Entries:**

openssl req -in request.csr -noout -text | grep DNS

4. **Create the Self-Signed Certificate:**

openssl x509 -req -in request.csr -signkey private.key -out certificate.crt -days 365 -extensions req_ext -extfile san.cnf

**Prevention:** In case there are issues with a certificate provided from a CA, testing with a self signed certificate can help with the troubleshooting process.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
