<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/-kcm-2576--how-to-remediate-metadefender-email-gateway-security- -->

# How to remediate MetaDefender Email Gateway Security's inbound SMTP server connectivity issue?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MetaDefender Cloud Email Security releases deployed on Windows systems.

## [**Issue:**](/docs/mdemail/6.4.2/knowledge-base/-kcm-2576--how-to-remediate-metadefender-email-gateway-security-#issue)

MetaDefender Email Gateway Security (EGS) may alert that the **inbound SMTP server** is not reachable, not responding or that an error occurred while attempting to establish an SSL or TLS connection:

[ERROR ]: (EmailSender:TryConnect (<localhost or public_server_address>:25)) MailKit.Security.SslHandshakeException: An error occurred while attempting to establish an SSL or TLS connection.[ERROR ]: (EmailSender:TryConnect (<localhost or public_server_address>:25)) System.Net.Sockets.SocketException: No such host is known.
## [**Causes:**](/docs/mdemail/6.4.2/knowledge-base/-kcm-2576--how-to-remediate-metadefender-email-gateway-security-#causes)

By default, EGS monitors the inbound SMTP server on **localhost** or the **public server address**, if that's been configured.

- If MD EGS is attempting to monitor the inbound SMTP server using a configured [public server address](https://www.opswat.com/docs/mdemail/configuration/settings#public-server-address) that is **not resolvable**, that can cause "No such host is known."

  - One scenario this can happen is if the public server address is used for password-protected attachment rescan links to end users, which is resolvable from the end user's side but not from the EGS instance itself.
- If the inbound SMTP server requires SSL/TLS, but the certificate does not contain "localhost" in the subject alternative name, or if the certificate is not issued to the configured public server address, that can cause "An error occurred while attempting to establish an SSL or TLS connection."

## [**Resolution:**](/docs/mdemail/6.4.2/knowledge-base/-kcm-2576--how-to-remediate-metadefender-email-gateway-security-#resolution)

- If the inbound SMTP server requires SSL/TLS, then the certificate's subject or subject alternative name should contain the configured public server address or “localhost” so that trust can be established.
- Override the default monitoring address by setting a registry key to the correct Fully Qualified Domain Name (FQDN) that is resolvable internally and also in the subject or subject alternative name of the certificate.

### [**Steps:**](/docs/mdemail/6.4.2/knowledge-base/-kcm-2576--how-to-remediate-metadefender-email-gateway-security-#steps)

1. Open the Registry Editor.
2. Navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\smtp_config`.
3. Create a new string value named `monitor_server_name`.
4. Set the value of `monitor_server_name` to the resolvable and trusted FQDN of the EGS instance.

For more details on this, refer to [Registry configuration](https://www.opswat.com/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitysmtp_config).

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
