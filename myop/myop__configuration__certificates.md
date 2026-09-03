<!-- source: https://www.opswat.com/docs/myop/configuration/certificates -->

# Certificates

The **Certificates** tab manages the the certificates that My OPSWAT On-premises uses for secure connection with the TLS protocol.

Please note that the certificates and their accompanying private keys should fit the format described below:

- Cryptography format

  - PKCS#1 in Base64 encoding
  - PKCS#8 in Base64 encoding (both unencrypted and encrypted)
- File extension

  - .crt and .pem for certificates
  - .key for private keys

## [Certificates](/docs/myop/configuration/certificates#certificates)

The Certificates section includes the certificates used to set up Secure Connection settings for My OPSWAT On-premises. Please refer to [Secure Connection](/docs/myop/configuration/secure-connection) for more information.

To add a certificate:

1. Click **Add Certificate**.

2. In the **Add Certificate** dialog, enter the **Certificate Name** and use the upload buttons to select your certificate, private key, and password files via the file browser.

3. Click **Add Certificate** to confirm your selection. If the certificate-key pair is successfully, the web console will show a success message.

## [Trust Certificates](/docs/myop/configuration/certificates#trust-certificates)

When My OPSWAT On-premises need to make connections to external servers, such as an email server, active directory servers, proxy servers, that use self-signed certificates, administrators need to add those server certificates or intermediate certificates to My OPSWAT On-premises' trust store.

To add a certificate to My OPSWAT On-premises' trust store, a user can follow the following steps:

- On My OPSWAT On-premises console, navigate to Settings > Global > select Certificates tab
- In the Trust Certificates section, click the Add Certificate to Trusted List button to open the upload dialog
- Enter the Certificate Name and use the upload button to upload the certificate file. Certificate files need to be in .cer and .crt formats.

- Click **Save** to save the added certificates.

**The Verify SSL Certificates setting**

To skip the certification verification for **an email server**, administrators can uncheck (disable) the **Verify SSL Certificates** setting. This setting is enabled by default.

Certificate chain

Normally, for a self-signed certificate chain, you should only need to import the root certificate if the external server is configured to present the full certificate chain (except for the root certificate)

However, in case the external server is misconfigured and does not present the full certificate chain, you may need to import additional certificates in order for My OPSWAT On-premises to properly establish the chain of trust.

For example, for the following certificate chain:

- Root certificate (self-signed)

  - Intermediate certificate 1 (not presented by the external server)

    - Intermediate certificate 2 (presented by the external server)

      - Server certificate (presented by the external server)

You will need to import the root certificate and the intermediate certificate 1.

Warning

Please take caution when disabling the **Verify SSL Certificates** setting as My OPSWAT On-premises will then trust a self-signed certificate for an email server, which can present a potential security risk.

This setting should be only used for troubleshooting connection issues.
