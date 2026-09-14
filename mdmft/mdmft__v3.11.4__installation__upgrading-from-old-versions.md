<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/installation/upgrading-from-old-versions -->

# Upgrading from MetaDefender Vault 1.3.6 or Lower to the Latest Version

Summarize Page    Connect to Cursor Connect to VS Code

From version 1.3.7 onward, Managed File Transfer uses NGINX as the underlying web server.

While user interaction with the system remains largely unchanged, there are a few differences to note:

1. The REST API and User Interface ports can no longer physically share the same value. The REST API will be automatically re-assigned to the first free port starting from 8000 upward.
2. All REST calls will now be made to the web client's port, with NGINX rerouting them to the appropriate destination.
3. Providing a certificate hash is no longer valid for TLS/SSL settings.
4. Paths to the actual certificate and private key must be provided. For password-protected certificates, the path to the file containing the passwords is also necessary.

The migration to NGINX will be handled by the installer. During the upgrade process, if TLS/SSL settings are detected, a pop-up window will appear, asking for the user to provide the paths to the:

1. SSL certificate
2. SSL certificate private key
3. (Optional) Path to a text file containing the password for the protected certificate

Users can opt to reset to factory defaults by clicking "Proceed with default", which will result in the loss of all TLS/SSL settings.

When pressing the "Accept" button, the contents will be validated before continuing with the installation. Data is considered valid if it meets the following criteria:

1. The SSL certificate must be provided in .pem or .crt formats.
2. The SSL certificate private key must be provided in .pem or .key formats.
3. The private key must be applicable to the given certificate.
4. If the certificate is password protected, a text file containing the password must also be provided.

If the input data is invalid, a warning will be presented. Click "OK" and try again.

If everything is successful, the following screen will appear:
