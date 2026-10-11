<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/enable-https-via-auxiliary-tool -->

# Enable HTTPS via Auxiliary Tool

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## Quick Overview

1. Prepare a self-signed or third-party certificate.
2. Use the "ChangeProtocol" tool to switch to HTTPS protocol.

## Step-by-Step Guide

1. Open the "ChangeProtocol.exe" tool by navigating to the "Tools" folder in the installation directory. By default, it is located at *C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Tools.*
2. Run the tool on the machine where MetaDefender Managed File Transfer is installed.
3. Provide login details for the local administrator account and click "Login".

4. Select the "HTTPS" protocol.

5. Refer to [Information Regarding Certificates](/configuration/information-regarding-certificates) section to obtain the "certificate and the certificate key"**.**
6. Fill the desired settings in the configuration window. Detailed information about each field is provided below.

7. The table below provides a detailed description of each setting.

| Name | Description | Example |
| --- | --- | --- |
| IP address | Limits the IP addresses that can access the Web UI  Set the binding to 0.0.0.0. for all IP addresses | 0.0.0.0 → allow unrestricted access 192.168.16.16 → only allow clients from this IP address |
| REST settings: Port | The port used for internal communication between MetaDefender Managed File Transfer Services  The default value is 8000 | The REST service will no longer be shared with the Web UI port  All calls to the REST endpoints should be made through the Web UI port  The port remains exposed to configuration for backwards compatibility reasons but should not be changed |
| Web UI settings: Host | The host name used to reach the MetaDefender Managed File Transfer Web UI  This host name should be accessible inside your network to allow clients to access the web UI  This value will also be used when composing links in email notifications | files.opswat.com → access the user interface at [**https://files.opswat.com**](https://files.opswat.com) Links in email notifications will also use this value. If you have SMTP configured it will look like this: [**https://files.opswat.com/file/8b822a734eea4afdaf5bcd01bfec8416**](https://files.opswat.com/file/8b822a734eea4afdaf5bcd01bfec8416) DNS settings should be previously configured to ensure clients can resolve files.opswat.com |
| Web UI settings: Port | The port used to reach MetaDefender Managed File Transfer Web UI and REST API endpoints  Leaving this to default value 443 allows users to access the interface without specifying the port in the browser address bar | 443 → access the user Interface for REST API calls at [**https://files.opswat.com:8010**](https://files.opswat.com:8010)  443 → expose the API at [**https://localhost/vault_rest**](https://localhost/vault_rest) 8010 → expose the API at [**https://localhost:8010/vault_rest**](https://localhost:8010/vault_rest) |
| SSL certificate | The path to the SSL certificate to use | Refer to [Information Regarding Certificates](/configuration/information-regarding-certificates) for more details |
| SSL certificate key | The path to the SSL certificate's private key | Refer to [Information Regarding Certificates](/configuration/information-regarding-certificates) for more details |
| SSL Password file | The path to the text file containing the password for the protected certificate | Refer to [Information Regarding Certificates](/configuration/information-regarding-certificates) for more details |

8. Click "Apply" to confirm your settings.

Note

For detailed instructions on setting up MetaDefender Core v4 with HTTPS, refer to the Enabling HTTPS with Metadefender Core v4 page.
