<!-- source: https://www.opswat.com/docs/ocm/troubleshooting/unable-to-install-run-windows-based-opswat-client-downloaded-fro -->

# Unable to install/run Windows-based MetaDefender Endpoint downloaded from OPSWAT Central Management instance configured for HTTPS protocol

| Term | Detail |
| --- | --- |
| Problem | Unable to install/run MetaDefender Endpoint downloaded from OPSWAT Central Management configured for HTTPS protocol |
| Cause | MetaDefender Endpoint requires importing the SSL certificate used OPSWAT Central Management instance. |
| Troubleshooting | MetaDefender Endpoint shows the message "Invalid license key" |
| Solution | Import the SSL certificate into the system that MetaDefender Endpoint should be running on. |

Upon installing (for the installer version) or running (for the on-demand version), MetaDefender Endpoint runs a connection check to the OPSWAT Central Management instance it is registered to. However if said OPSWAT Central Management instances have been configured to using HTTPS protocol, this connection check will fail if the system that MetaDefender Endpoint is running on does not trust the certificate used by the OPSWAT Central Management instance Below is the generic error message MetaDefender Endpoint displays when the connection check fails.

This is because HTTPS protocol requires the system that MetaDefender Endpoint should be running on to trust the certificate OPSWAT Central Management instance is using. Establish trust requires import the aforementioned certificate into the system's trust store.

On Windows system, to import the certificate for MetaDefender Endpoint, please follow the below guidelines:

1. Locate the certificate file (such as in .pem format).
2. Open certlm in Microsoft Management Console ( In Start Menu type "manage computer certificates")

3. Select **Trusted Root Certification Authorities.

**

4. Select Action** > **All Tasks** >** Import... Follow the wizard to import the certificate file.
