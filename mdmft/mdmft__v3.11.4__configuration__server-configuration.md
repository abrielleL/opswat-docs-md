<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/server-configuration -->

# Server Configuration

Summarize Page    Connect to Cursor Connect to VS Code
### [Quick Overview](/docs/mdmft/v3.11.4/configuration/server-configuration#quick-overview)

Starting with v2.0.6, a new settings page allows the configuration of all security aspects of the product.

The old procedure is still supported, and details can be found [here](/docs/mdmft/v3.11.4/mdmft/configuration/enable-https-via-auxiliary-tool).

### [Host and Rate Limit](/docs/mdmft/v3.11.4/configuration/server-configuration#host-and-rate-limit)

For configuring the host and the rate limiting visit the "Settings" -> "Security"-> "Server configuration" tab.

Fill in the desired settings in the configuration window. Detailed information about the fields is provided below.

| Name | Description |
| --- | --- |
| Host | DNS name or IP Address of the machine running the MetaDefender Managed File Transfer server. A DNS name causes the server to listen on all network interfaces, while an IP address binds the server to that particular value. Note: this value is also used to generate links in email notifications. |
| Port | The port used to listen for connections. |
| Shared Memory Size | Allocated memory for rate-limiting coordination. |
| Rate | Maximum allowed requests within a defined time period. |
| Burst Size | Maximum requests temporarily permitted during bursts. |
| No Delay | Useful if imposing a rate limit without constraining the allowed spacing between requests. |

### [Enabling HTTPS](/docs/mdmft/v3.11.4/configuration/server-configuration#enabling-https)

Info

An SSL/TLS certificate must be created before activating HTTPS. Refer to the [Information Regarding Certificates](/docs/mdmft/v3.11.4/configuration/information-regarding-certificates) for obtaining a "certificate and certificate key"**.**

1. After creating the SSL certificate, go to the "Settings" -> "Security"-> "Server configuration" tab.
2. Enable HTTPS Connection

3. Fill in the desired settings in the configuration panel. Detailed information about each field is provided below.

| Name | Description |
| --- | --- |
| Certificate Path | Path of the separately created certificate. |
| Private Key Path | Path of the created certificate private key. |
| Password Path | Optional path of the created certificate password file. |
| TLS version | TLS protocol version to use. Connections with clients that do not support at least one of the configured TLS versions will fail. |

Info

Certificate paths containing whitespaces are accepted by default; there is no need to quote the paths.

4. Click "Update" and wait to be redirected to the new URL.

### [Enforcing TLS Version](/docs/mdmft/v3.11.4/configuration/server-configuration#enforcing-tls-version)

Upgrading from a previous version or leaving all TLS options unchecked will revert to default as follows:

- Outbound connections (i.e. requests made by Managed File Transfer) will use the operating system's default TLS protocol
- Inbound web requests will default to TLS v1.2 or TLS v1.3 for Managed File Transfer's web server (NGINX)

To enforce a particular TLS version, please select only that option.
