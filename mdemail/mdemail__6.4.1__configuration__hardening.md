<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/hardening -->

# Hardening

## [Sign notifications sent by the product](/docs/mdemail/6.4.1/configuration/hardening#sign-notifications-sent-by-the-product)

Enable digitally signing alert, notification and report emails sent by the product so that end-recipients can trust the authenticity of these system messages.

For details how to enable S/MIME signing of these emails see [Configuration/Alert. notification and quarantine report emails](/docs/mdemail/6.4.1/configuration/alert--notification-and-quarantine-report-emails).

## [Networking](/docs/mdemail/6.4.1/configuration/hardening#networking)

### [Transport Layer Security](/docs/mdemail/6.4.1/configuration/hardening#transport-layer-security)

No TLS by default

By default TLS is not enabled for none of the web management console port, public rescan port and SMTP port. It is also disabled for outbound connections towards MetaDefender Core and Metadefender Managed File Transfer (HTTP), Active Directory (LDAP) or SMTP services (SMTP).

To enable TLS, follow the instructions in [Configuration/Transport Layer Security](/docs/mdemail/6.4.1/configuration/transport-layer-security).

#### [TLS versions](/docs/mdemail/6.4.1/configuration/hardening#tls-versions)

Old versions of SSL and TLS protocols, such as SSLv2, SSLv3, or TLS 1.0 and TLS 1.1, are no longer supported. Use the most recent TLS 1.2 version if available. For details see: [Configuration/Transport Layer Security](/docs/mdemail/6.4.1/configuration/transport-layer-security).

No options for TLS clients

When Email Gateway Security acts as a client (connection to Core, Active Directory or an SMTP service), then there is currently no way to configure the preferred TLS versions on the client side.

TLSv1.3 is partially supported

For compatibility reasons, TLSv1.3 is currently supported for the web management console only.

#### [Cipher suites](/docs/mdemail/6.4.1/configuration/hardening#cipher-suites)

Verify that the strongest algorithms and cipher suites are set as preferred.

Reasonable defaults

By default Email Gateway Security comes with the following cipher configuration: ssl_ciphers HIGH:!aNULL:!MD5;.

Cipher suites can be customized in the following way:

1. Create a configuration file under your installation folder’s nginx directory (default C:\Program Files\OPSWAT\MetaDefender Email Security\nginx). The extension must be *.conf.

copy con "C:\Program Files\OPSWAT\MetaDefender Email Security\nginx\cipher.conf"

2. Add the desired cipher config as a single line entry as the ssl_ciphers directive

ssl_ciphers TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256;

3. Restart the Email Gateway Security service

net stop mdemailsecurity
net start mdemailsecurityRecommended settings

As vulnerabilities in protocols and ciphers are continuously discovered, we recommend to keep the cipher configuration up-to-date.

For the same reason we recommend using a trusted service (e.g. <https://wiki.mozilla.org/Security/Server_Side_TLS>) to define the secure cipher configuration.

No options for TLS clients

When Email Gateway Security acts as a client (connection to Core, MFT, Active Directory or an SMTP service), then there is currently no way to configure the preferred TLS cipher suites on the client side.

### [Restrict web management port](/docs/mdemail/6.4.1/configuration/hardening#restrict-web-management-port)

Email Gateway Security provides the option to configure the web management console and the public rescan page to separate ports. For details see [Configuration/Registry configuration](/docs/mdemail/6.4.1/configuration/registry-configuration).

Shared port by default

By default the web management console and the public rescan page are configured to the same port (restport, see [Configuration/Registry configuration](/docs/mdemail/6.4.1/configuration/registry-configuration)).

Separating the web management console and the public rescan page to different ports makes it possible to restrict the web management console to be accessible from a management network only, while keeping the public rescan page available even from the internet. For details see [Configuration/Registry configuration](/docs/mdemail/6.4.1/configuration/registry-configuration).

### [Open relay](/docs/mdemail/6.4.1/configuration/hardening#open-relay)

An open mail relay is a [Simple Mail Transfer Protocol](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) (SMTP) server configured in such a way that it allows anyone on the Internet to send email through it, not just mail destined to or originating from known users. This used to be the default, but open mail relays have become unpopular because of their exploitation by spammers and worms. Many relays were closed, or were placed on blocklists by other servers. [<https://en.wikipedia.org/wiki/Open_mail_relay>]

By processing mail that is neither for nor from a local user, an open relay makes it possible for an unscrupulous sender to route large volumes of spam and/or spread malware. In effect, the owner of the server - who is typically unaware of the problem - donates network and computer resources to the sender's purpose. Moreover, open mail relays are often blocklisted as soon as they’re discovered, and email originating from these servers are marked as spam. [[https://www.acunetix.com/support/docs/wvs/configuring-email-settings/](https://www.acunetix.com/vulnerabilities/web/smtp-open-mail-relay//)]

Email Gateway Security can be configured to filter email for certain email addresses and domains. For details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy).

## [Accounts](/docs/mdemail/6.4.1/configuration/hardening#accounts)

### [Changing the default password](/docs/mdemail/6.4.1/configuration/hardening#changing-the-default-password)

After installation of versions pre 4.3.0, a default user account was created with a predefined password. This user may still exist in a post 4.3.0 version, if it was upgraded from an earlier version.

Change this predefined legacy password as soon as possible, following these steps:

1. Log in using the legacy default user account's name and password ( admin / admin ),
2. Change the password of the account as described in [Configuration/Users](/docs/mdemail/6.4.1/configuration/users).

### [Enhanced password policy](/docs/mdemail/6.4.1/configuration/hardening#enhanced-password-policy)

For *Local* type user directories Email Gateway Security provides enhanced password policy. The enhanced password policy provides higher level of security for passwords then the default password policy.

Off by default

The enhanced password policy is disabled by default for *Local* type user directories.

To enable enhanced password policy for a *Local* type user directory, follow the instructions in [Configuration/Users](/docs/mdemail/6.4.1/configuration/users).

### [Unused accounts](/docs/mdemail/6.4.1/configuration/hardening#unused-accounts)

#### [Delete unused local accounts](/docs/mdemail/6.4.1/configuration/hardening#delete-unused-local-accounts)

User accounts in *Local* type user directories must be deleted manually if they are not needed any more.

#### [AD or LDAP accounts](/docs/mdemail/6.4.1/configuration/hardening#ad-or-ldap-accounts)

User accounts from *Active Directory* or *LDAP* type user directories can not access the web management console after they have been removed from the directory service.

### [Shared accounts](/docs/mdemail/6.4.1/configuration/hardening#shared-accounts)

Verify that shared accounts are not present in *Local* type user directories (e.g. admin).

## [Components](/docs/mdemail/6.4.1/configuration/hardening#components)

### [Email Gateway Security](/docs/mdemail/6.4.1/configuration/hardening#email-gateway-security)

Always upgrade to the latest published version of the product that is available on [My OPSWAT](https://my.opswat.com/portal/products).

### [MetaDefender Core and engines](/docs/mdemail/6.4.1/configuration/hardening#metadefender-core-and-engines)

Standalone only

This section applies to Email Gateway Security *standalone edition* only. For details see [Installation/Licensing](/docs/mdemail/6.4.1/installation/licensing).

Always use the recommended versions of MetaDefender Core and the engines. For details see [Installation/Prerequisites](/docs/mdemail/6.4.1/installation/prerequisites).

### [OpenSSL](/docs/mdemail/6.4.1/configuration/hardening#openssl)

Always upgrade to the latest published version of OpenSSL. For details see [Installation/Prerequisites](/docs/mdemail/6.4.1/installation/prerequisites).

### [Microsoft .NET](/docs/mdemail/6.4.1/configuration/hardening#microsoft-net)

Always upgrade to the latest published version of the Microsoft .NET Framework. For details see [Installation/Prerequisites](/docs/mdemail/6.4.1/installation/prerequisites).
