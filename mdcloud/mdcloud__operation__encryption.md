<!-- source: https://www.opswat.com/docs/mdcloud/operation/encryption -->

# Encryption

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This page explains how MetaDefender Cloud uses encryption to protect your files and data, and which extra encryption options you can use.

| Data | Protection | Managed by |
| --- | --- | --- |
| Traffic to the web portal and API | HTTPS, TLS 1.2 or higher | OPSWAT |
| Uploaded files | Encrypted at rest, AES-256 | OPSWAT, using encryption keys managed by AWS |
| Scan results, scan history and account data | Encrypted at rest, AES-256 | OPSWAT |
| Backups | Encrypted at rest, AES-256 | OPSWAT |
| Passwords | Handled by OPSWAT's identity service | OPSWAT |
| Sanitized files (optional) | Encrypted with a per-file AES-256 key that only your RSA private key can unlock | You |
| API connection (optional, Enterprise licence) | Mutual TLS with your client certificate | You and OPSWAT |

**1. Data in transit**

All communication with MetaDefender Cloud, through the web portal and the REST API, is encrypted with HTTPS. Connections using TLS versions older than 1.2 are refused.

**2. Data at rest**

All files you upload are automatically encrypted with AES-256 when stored. Scan results, scan history, account data and backups are also encrypted at rest. Your files are stored in the region that processes them; see [Locations](https://www.opswat.com/docs/mdcloud/compliance/locations).

With private processing, your file is deleted after analysis. See the [Responsibility Matrix](https://www.opswat.com/docs/mdcloud/compliance/responsibility-matrix) for how long data is kept.

**3. Key management**

- Encryption keys for stored data are managed by AWS (Amazon S3 and AWS Key Management Service) on OPSWAT’s behalf and never leave AWS unencrypted.

- Storage encryption keys are rotated regularly by AWS.

- Keys are managed by AWS. OPSWAT services use them only through the AWS storage services; OPSWAT staff do not handle key material.

**4. Credentials**

- Your API key is shown only to you, on your account page. Treat it like a password: if you think it has leaked, replace it straight away.

- Passwords are not stored by MetaDefender Cloud: sign-in is handled by OPSWAT's identity service, or by your own identity provider if you use single sign-on.

**5. Extra encryption options for you**

- **Sanitized file encryption:** if you add an RSA public key to your API key, each sanitized file is stored encrypted with its own AES-256 key, and that key is returned to you encrypted with your public key. Only your private key can unlock it. The original upload is not covered.

- **Mutual TLS** (Enterprise licence, on request): OPSWAT sets up a dedicated endpoint that accepts only connections made with your client certificate. See the [Responsibility Matrix](https://www.opswat.com/docs/mdcloud/compliance/responsibility-matrix).

**6. Your responsibilities**

- Use only HTTPS endpoints and keep TLS validation turned on in your integrations.

- Keep your API keys, RSA private keys and mutual TLS private keys secret, and rotate them on your own schedule.

- If you use your own identity provider, protect its sign-in with multi-factor authentication.
