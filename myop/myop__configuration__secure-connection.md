<!-- source: https://www.opswat.com/docs/myop/configuration/secure-connection -->

# Secure Connection

By default, the communication between an OPSWAT product instance and a My OPSWAT On-premises server is not encrypted. If HTTPS is enabled, encrypted communication between the server and the product instances can be enforced. This section describes how to enable HTTPS connection for My OPSWAT On-premises.

## [Requirements](/docs/myop/configuration/secure-connection#requirements)

In order to enable HTTPS on My OPSWAT On-premises server, a trusted certificate issued by a certificate authority provider or a self-signed certificate along with their private key and password (if needed) files must be provided.

## [Adding Certificates](/docs/myop/configuration/secure-connection#adding-certificates)

To add a certificate for the **Secure Connection** settings, please refer to [Certificates](/docs/myop/configuration/certificates#certificates).

## [Enabling HTTPS](/docs/myop/configuration/secure-connection#enabling-https)

1. On the left navigation, navigate to **Settings > Server** tab **> Secure Connection** section**.**

2. Toggle **Enable HTTPS** to ENABLE
3. Choose a certificate you added in [the Certificates tab](/docs/myop/configuration/secure-connection#adding-certificates).
4. Select the TLS version(s) you want to enforce HTTPS for. The port configuration currently cannot be changed.
5. Click **Save** to confirm your selection.
6. My OPSWAT On-premises should immediately refresh itself for the new settings to take effect. Please note that the refresh process can take several minutes and the server cannot be accessed until its completion.

Using self-signed certificate

Please note that when using a self-signed certificate to enable HTTPS mode, the managed product instances should have this certificate in their trust store to be able to establish a connection to the My OPSWAT server.

For MetaDefender Kiosk L-series instances, they should be on version 5.6.2 or newer.

## [Disabling HTTPS](/docs/myop/configuration/secure-connection#disabling-https)

1. On the left navigation, navigate to **Settings > Server** tab **> Secure Connection** section**.**
2. Toggle **Enable HTTPS** to DISABLE**.**
3. Click **SAVE**.
4. My OPSWAT On-premises should immediately refresh itself for the new settings to take effect. Please note that the refresh process can take several minutes and the server cannot be accessed until its completion.

### [Server URL](/docs/myop/configuration/secure-connection#server-url)

The **Server URL** setting is used to set the My OPSWAT On-premises' server address, such as when generating download URLs for product reports. The server URL can be either a domain or an IP address.

For example, with the server URL **http://myopswat.local,** a report's download URL is formatted as **http://myopswat.local/console/reports/<report>/location>/report.json**

Please note that the chosen Server URL should be resolvable by the system that you are using to browse the My OPSWAT On-premises console.

The **Enable HTTPS** setting affects the protocol scheme used for the server URL, which is either http or https.
