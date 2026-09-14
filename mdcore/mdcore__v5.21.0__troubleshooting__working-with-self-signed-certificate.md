<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/working-with-self-signed-certificate -->

# Working with self-signed certificate

When setting up the webhook server for the callback URL, customers may want to configure HTTPS and use a self-signed certificate.

Since self-signed certificates are not trusted by the system by default, this error might occurs

MarkdownCopyThe certificate is self-signed and untrusted

The certificate must first be added to the Trusted Root Certificate store - both Windows and Linux:

1. Add the certificate to the Trusted Root Certificate store.
2. Restart the MetaDefender Core service for the changes to take effect.
