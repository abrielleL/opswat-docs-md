<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/does-metadefender-email-gateway-security-supports-sendmail-in-li -->

# Does MetaDefender Email Gateway Security supports SendMail in Linux?

## [Integration Methods](/docs/mdemail/knowledge-base/does-metadefender-email-gateway-security-supports-sendmail-in-li#integration-methods)

1. Sendmail as an SMTP Client
2. Sendmail sends emails to MetaDefender Email Gateway Security (EGS) using the SMTP port.
3. You can configure Sendmail to insert custom headers, allowing MetaDefender Email Security to process or modify messages accordingly.
4. Refer to the [SMTP Servers Configuration](/docs/mdemail/configuration/settings#smtp-servers) for details.
5. Sendmail as an SMTP Server
6. Sendmail receives emails from EGS using an SMTP-type server profile.
7. This configuration ensures incoming emails are scanned by MetaDefender Core before being handed over to Sendmail for local delivery.
8. Refer to the [SMTP Server Profiles](/docs/mdemail/configuration/server-profiles) for setup instructions.

## [Custom Headers](/docs/mdemail/knowledge-base/does-metadefender-email-gateway-security-supports-sendmail-in-li#custom-headers)

When Sendmail is acting as a client, its processing can be manipulated by adding or modifying custom headers. For more information, see the [Additional Email Headers](/docs/mdemail/configuration/additional-email-headers) documentation.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
