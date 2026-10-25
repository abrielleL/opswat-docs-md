<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/installation/insertion -->

# Insertion

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Email Gateway Security enhances existing email security gateways adding proactive and preventive measures to them. To be able to do so, Email Gateway Security must be inserted into the email flow, typically between the email gateway and the mail server.

Depending on the direction of the email flow (for details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy)), the following needs to be set:

1. Inbound emails

   1. The email gateway must forward emails to Email Gateway Security
   2. Email Gateway Security must forward emails to the mail server
2. Outbound emails

   1. The mail server must forward emails to Email Gateway Security
   2. Email Gateway Security must forward emails to the email gateway

## [Inbound emails](/docs/mdemail/6.4.2/installation/insertion#inbound-emails)

To insert Email Gateway Security into the email flow in case of inbound emails:

1. Configure your email gateway to forward emails to Email Gateway Security

   1. Set your Email Gateway Security instance’s IP address or DNS name as the outbound mail relay in your email gateway
   2. Set 10025 as the outbound mail relay SMTP port in your email gateway(to customize this port see [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings))
2. Configure Email Gateway Security to forward emails to your mail server

   1. Create an SMTP server profile for the mail server (for details see [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles))

2. Set this server profile as *SMTP relay server profile* for your inbound security rule (for details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy))

## [Outbound emails](/docs/mdemail/6.4.2/installation/insertion#outbound-emails)

To insert Email Gateway Security into the email flow in case of outbound emails:

1. Configure your mail server to forward emails to Email Gateway Security

   1. Set your Email Gateway Security instance’s IP address or DNS name as the outbound mail relay in your mail server
   2. Set 10025 as the outbound mail relay SMTP port in your mail server (to customize this port see [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings))
2. Configure Email Gateway Security to forward emails to your email gateway

   1. Create an SMTP server profile for the email gateway (for details see [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles))
   2. Set this server profile as *SMTP relay server profile* for your outbound security rule (for details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy))
