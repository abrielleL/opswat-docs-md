<!-- source: https://www.opswat.com/docs/mdemail/configuration/transport-layer-security -->

# Transport Layer Security

For production MetaDefender Email Gateway Security deployments a more sophisticated TLS configuration is recommended than what is described below. Please consult the [nginx documentation on Configuring HTTPS servers](http://nginx.org/en/docs/http/configuring_https_servers.html) for further details.

Warning

It is not recommended to use self-signed certificates in production environments. If you do not have a suitable certificate, you can apply to a Certificate Authority to obtain one.

Supported key standards

MetaDefender Email Gateway Security supports PKCS#1 public keys; PKCS#1 and PKCS#8 private keys for all applicable use-cases (TLS for the HTTP and SMTP services; S/MIME signing of notification alert and report emails; DKIM and ARC signing of emails).

## [Recommended TLS versions and cipher suites](https://www.opswat.com/docs/mdicap/configuration/configuring-tls#recommended-tls-versions-and-cipher-suites)

MetaDefender Email Gateway Security supports TLS 1.3 or below.

Security level of TLS versions and cipher suites may change when new vulnerabilities are discovered.

The range of applied TLS versions and cipher suites may depend on the clients' compatibility at a certain deployment.

Because of this, OPSWAT recommends following frequently updated best practices from 3rd parties like <https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices> or <https://wiki.mozilla.org/Security/Server_Side_TLS>.

## [Certificates](/docs/mdemail/configuration/transport-layer-security#certificates)

MetaDefender Email Gateway Security uses private key file and certificate file pairs as digital identifiers to authenticate itself to the clients for the different services it provides and to the servers when it acts as a client; to digitally sign alert, notification and report emails; and to digitally sign outbound emails when DKIM is enabled.

File format

Key and certificate files must be in PEM format.

Private key file and certificate file pairs can be defined under **Settings > Certificates** for the different use-cases that are supported by the product.

The supported use cases are

- Transport Layer Security (TLS)
- Secure/Multipurpose Internet Mail Extensions (S/MIME)
- DomainKeys Identified Mail (DKIM)

### [Transport Layer Security (TLS)](/docs/mdemail/configuration/transport-layer-security#transport-layer-security-tls)

The *Transport Layer Security (TLS)* use-case certificates are for cases when the product acts as a client or a server in a TLS communication.

For details see [Server profiles](/docs/mdemail/configuration/server-profiles).

### [Secure/Multipurpose Internet Mail Extensions (S/MIME)](/docs/mdemail/configuration/transport-layer-security#securemultipurpose-internet-mail-extensions-smime)

The *Secure/Multipurpose Internet Mail Extensions (S/MIME)* use-case certificates are for cases when the product is to digitally sign alert, notification or quarantine report emails.

For details see [Alert, notification and quarantine report emails](/docs/mdemail/configuration/alert--notification-and-quarantine-report-emails).

### [DomainKeys Identified Mail (DKIM)](/docs/mdemail/configuration/transport-layer-security#domainkeys-identified-mail-dkim)

The *DomainKeys Identified Mail (DKIM)* use-case certificates are for cases when the product is to DKIM sign or DKIM (ARC) re-sign outbound emails.

## [Inbound connections](/docs/mdemail/configuration/transport-layer-security#inbound-connections)

### [Web Management Console and Public Rescan Page](/docs/mdemail/configuration/transport-layer-security#web-management-console-and-public-rescan-page)

OpenSSL required

To enable TLS for the web management console, OpenSSL must be installed on the server.

For details see [Installation/Prerequisites](/docs/mdemail/installation/prerequisites).

MetaDefender Email Gateway Security supports accessing the Web Management Console and the Public Rescan functionality (for details see [Operating/Password protected attachments](/docs/mdemail/operating/password-protected-attachments)) via HTTPS. This feature is, however, not enabled by default. To enable HTTPS you should perform the following steps.

Public server address

The TLS settings of the web management console are propagated to the *Public server address* under **Settings > General** / Configuration.

For example, when TLS is enabled for the web management console, then the scheme for the *Public server address* will be changed to *https*. When TLS is disabled for the web management console, then the scheme for the *Public server address* will be downgraded to *http*.

For details see [Configuration/Settings](/docs/mdemail/configuration/settings).

1. Define a certificate and private key pair under **Settings > Certificates** for the HTTPS connections.

2. Using the certificate defined in the previous step, enable HTTPS under **Settings > Security**.

#### [Cipher suite configuration](https://www.opswat.com/docs/mdicap/configuration/configuring-tls#cipher-suite-configuration)

Cipher suite configuration for the Web Management Console can be done using configuration files. Perform the following steps:

1. Create a configuration file under the Nginx configuration directory of your system (by default `C:\Program Files\OPSWAT\Metadefender Email Security\nginx` )

Extension

The extension of the additional TLS configuration file must be `.conf` in order to be interpreted correctly by the product.

2. Add the necessary configuration to the configuration file

Configuration syntax

The configuration file must follow the Nginx syntax. For details see <http://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_ciphers>.

Example

`ssl_ciphers HIGH:!aNULL:!MD5;`

Recommended cipher suites

For cipher suite recommendations see the section *Recommended TLS versions and cipher suites*.

3. The Email Gateway Security service must be restarted for the configuration to take effect.

### [Inbound SMTP services](/docs/mdemail/configuration/transport-layer-security#inbound-smtp-services)

Email Gateway Security can listen on multiple SMTP ports providing the option to apply different TLS settings for each SMTP port.

To enable TLS for a certain inbound SMTP service:

1. Define a certificate and private key pair under **Settings > Certificates** for the SMTPS connections.

2. Under **Settings > Security** / SMTP Server Connection Settings select the SMTP service for which the TLS needs to be set

3. In the Edit SMTP endpoint panel apply the desired settings for the SMTP service:

   1. Select the appropriate SMTP encryption method

2. Use the certificate defined in step 1 and select the desired TLS versions

Specific port only

These TLS settings apply to this specific port only.

### [TLS cipher suite settings for inbound SMTP](/docs/mdemail/configuration/transport-layer-security#tls-cipher-suite-settings-for-inbound-smtp)

Email Gateway Security uses Window's Schannel for inbound SMTP secure connections by default. This makes possible to configure the accepted ciphers, cipher suites via Windows registry. You can find information about how to configure specific settings here: <https://docs.microsoft.com/en-us/windows-server/security/tls/tls-registry-settings>.

### [MetaDefender Core type server profile webhooks](/docs/mdemail/configuration/transport-layer-security#metadefender-core-type-server-profile-webhooks)

Email Gateway Security supports webhooks to get the scan results from MetaDefender Core. Basically for webhook notifications Email Gateway Security listens on a server port where it receives the notifications from Core. This server port can be configured for TLS.

For details about webhooks see [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

To configure TLS for the webhook service, perform the following steps:

#### [Prerequisites](/docs/mdemail/configuration/transport-layer-security#prerequisites)

- Both Email Gateway Security and Core must be configured for TLS/HTTPS on their web management console interfaces.
- The server certificate must reside in the Windows certificate store.

  - In the *Trusted Root Certification Authorities* store and in *PKCS12* / *PFX* format (containing both the certificate and the private key; notice the little key in the icon of the certificate)

1. Set the public server address to the domain name of Email Gateway Security, to what the certificate is issued to

2. Enable **Settings > Server Profiles /** MetaDefender Core type profile **/ Enable Webhook callbacks** and configure for a dedicated port

3. Get the thumbprint of the certificate (for safety copy from *certlm* and paste for example into *Notepad* first, then copy from Notepad and paste to cmd from there in the next step)

4. Use *netsh* command to bind the certificate to the webhook port

cmd
netsh http add sslcert ipport=<ip>:<webhook port> certhash=<thumbprint> appid=<guid> certstorename=rootExample (IP address 0.0.0.0 means all interfaces of the server)
netsh http add sslcert ipport=0.0.0.0:8089 certhash=09a0b5df587bc006e86508cf62cc8abfb27f48fd appid={00112233-4455-6677-8899-AABBCCDDEEFF} certstorename=root

5. When Email Gateway Security is not running as Local Service, enable access to this port for the appropriate user

cmd
netsh http add urlacl url=<scheme>://+:<port>/ user=<user>Example
netsh http add urlacl url=https://+:8089/ user=everyone
## [Outbound connections](/docs/mdemail/configuration/transport-layer-security#outbound-connections)

TLS for outbound connections can be set up at the appropriate server profile. For details see [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

Trusted certificate

In case of outbound connections the servers certificate must always be trusted by the client.

In practice it means that either the CA certificate –that was used for signing the server's certificate–, or the server's certificate itself must be installed in the Email Gateway Security's operating system's trusted certificate store.

### [MetaDefender Core](/docs/mdemail/configuration/transport-layer-security#metadefender-core)

To connect to a Core server over TLS perform the following steps:

1. Configure the Core server to listen on HTTPS. For details see [Enabling HTTPS](https://onlinehelp.opswat.com/corev4/3.8.1_Enabling_HTTPS.html),
2. Add this Core to your server profiles using https scheme. For details see [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

### [Outbound SMTP](/docs/mdemail/configuration/transport-layer-security#outbound-smtp)

To connect to an SMTP server over TLS first you need to decide which flavor to use: StartTLS (TLS over SMTP) or SMTPS (SMTP over TLS).

#### [StartTLS](/docs/mdemail/configuration/transport-layer-security#starttls)

In case of StartTLS you still need to decide whether using StartTLS is just an option or it is mandatory.

**Optional StartTLS**

If StartTLS is optional then the client will try to establish the TLS connection, and if it fails, then the connection will fail over to a clear text connection.

To connect to an SMTP server using optional StartTLS perform the following steps:

1. Configure the SMTP server to either

   1. Support StartTLS – in this case clear text SMTP connections will be upgraded to TLS; or
   2. Not support StartTLS – in this case SMTP connections will be fall back to clear text.
2. Add this SMTP server to your server profiles

   1. Using smtp scheme, with
   2. TRANSPORT LEVEL ENCRYPTION set to STARTTLS optional.
   3. For details see [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

**Mandatory StartTLS**

If StartTLS is mandatory then the client will try to establish the TLS connection, and if it fails, then the connection will fail.

To connect to an SMTP server using mandatory StartTLS perform the following steps:

1. Configure the SMTP server to Support StartTLS;
2. Add this SMTP server to your server profiles

   1. Using smtp scheme, with
   2. TRANSPORT LEVEL ENCRYPTION set to STARTTLS required.
   3. For details see [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

#### [SMTPS](/docs/mdemail/configuration/transport-layer-security#smtps)

In case of SMTPS, the TLS handshake comes first, and if (and only if) it succeeds, then the SMTP connection is established over the TLS.

To connect to an SMTP server over TLS perform the following steps:

- Configure the SMTP server to listen on SMTPS.
- Add this SMTP server to your server profiles using smtps scheme. For details see [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

#### [Certificate based client authentication](/docs/mdemail/configuration/transport-layer-security#certificate-based-client-authentication)

It is possible to configure a client certificate to be presented to the remote SMTP server when sending emails. To configure a client certificate:

1. Import the desired certificate in **Settings > Certificates**
2. In the server profile, enable the option *Certificate based client authentication.*
3. Select the imported certificate in the *Select Certificate* drop down list
