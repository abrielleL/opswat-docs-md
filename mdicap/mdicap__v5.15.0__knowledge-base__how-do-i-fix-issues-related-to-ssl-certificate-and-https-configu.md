<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-do-i-fix-issues-related-to-ssl-certificate-and-https-configu -->

# How do I fix issues related to SSL certificate and HTTPS configuration?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Error

When adding an HTTPS-enabled MetaDefender Core instance to ICAP’s server profile, you might encounter some SSL errors.

To ensure that everything is configured correctly, please follow these troubleshooting steps:

1. Check that the **HTTPS certificate is issued to MetaDefender Core’s domain**.

   - The certificate's subject and/or ***subjectAlternativeName*** should contain the MetaDefender Core server’s FQDN or IP address.
   - In the case of a wildcard certificate, it should include the MetaDefender Core server’s domain name.
2. Check that **the full certificate chain**, including any intermediate and root certificate authorities, **is trusted on the MetaDefender ICAP server**.

   - You can do this by importing any intermediate and root certificate authorities to the server’s trusted root store.
3. Check that the **certificate revocation list is available and reachable** from the MetaDefender ICAP server:

   - Please follow this knowledge article to [verify that the certificate revocation list is available and valid](/docs/mdicap/v5.15.0/knowledge-base/how-do-i-resolve--the-revocation-function-was-unable-to-check-re).

Error

After enabling HTTPS for MetaDefender ICAP Server, the web management console is inaccessible.

If this happens, there’s a good chance that **the HTTPS configuration is wrong, or there’s a problem with the certificate**. Please follow these troubleshooting steps to ensure the configuration is valid:

1. Remove the HTTPS configuration to access the web management console:

   - You can utilize the [HTTPS Configuration Removal Tool](/docs/mdicap/v5.15.0/troubleshooting/https-configuration-removal-tool) to remove HTTPS and access the ICAP web console via HTTP.
2. Review the [HTTPS configuration steps](/docs/mdicap/v5.15.0/configuration/configuring-tls) to ensure that everything is set up correctly.
3. Verify that the certificate-private key pair is valid:

   - You can run the following OpenSSL commands:

BashCopy# Replace "cert.crt" with the path to the certificate
openssl x509 -noout -modulus -in cert.crt | openssl md5
# Replace "key.key" with the path to the private key
openssl rsa -noout -modulus -in key.key | openssl md5

- If the output MD5 hash values of the certificate and private key don’t match up, then you will need to generate a new certificate-private key pair.

Support:

For further assistance regarding **Issues related to SSL certificate and HTTPS configuration**, please follow these instructions on [**How To Create a Support Package**](https://www.opswat.com/docs/mdicap/troubleshooting/how-to-create-support-package), before [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
