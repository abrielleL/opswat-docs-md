<!-- source: https://www.opswat.com/docs/mdemail/configuration/settings -->

# Settings

Runtime settings of Email Gateway Security can be configured under **Settings > General**.

## [Email](/docs/mdemail/configuration/settings#email)

### [Retry](/docs/mdemail/configuration/settings#retry)

When scanning or relaying the email fails (e.g. the internal processing component or the relay SMTP server is not available), Email Gateway Security will retry.

Under **Settings > General / Email** the retry count and the interval between each attempt can be configured.

### [Email/Attachment size restrictions](/docs/mdemail/configuration/settings#emailattachment-size-restrictions)

Maximum email and/or attachment size restrictions can be configured under **Settings > General / Email**.

You can configure a maximum total email size (un-decoded; including the size of all the headers, email bodies and all attachments) by enabling *Restrict maximum email size* and enter a desired limit.

An attachment size limit can also be configured by enabling *Restrict maximum attachment(s) size* and enter a desired limit. This setting refers to all the attachments of an email.

Default

By default Email Gateway Security does not apply any restriction on the size of emails or attachments.

### [Prioritize header charset setting in HTML](/docs/mdemail/configuration/settings#prioritize-header-charset-setting-in-html)

Enabling this option forces MetaDefender Email Gateway Security to treat the charset encoding specified in the HTML body's header as the content encoding (used for parsing and sanitization), as opposed to the default, which is to try and extract the charset from the HTML body's *<meta>* tag.

**Example**

When *Prioritize header charset setting in HTML* is enabled, the charset is taken from here:

When *Prioritize header charset setting in HTML* is disabled, the charset is taken from here:

## [SMTP servers](/docs/mdemail/configuration/settings#smtp-servers)

Email Gateway Security’s inbound SMTP server port and the SMTP server’s encryption configuration can be found under **Settings > Security** / SMTP Server Connection Settings.

Email Gateway Security can listen on multiple SMTP ports providing the option to apply different settings for each SMTP port.

Click the  button to add a new SMTP server port.

## [Anti-spam](/docs/mdemail/configuration/settings#anti-spam)

With the *Aggressiveness level* Email Gateway Security’s anti-spam component can be configured how eager it should be when looking for (potential) spam.

Enabling the *Add analytical email headers* Email Gateway Security will add special headers to emails so that later it can track false positive or negative spam.

In the *IP allowlist* a list of IPv4 addresses can be specified for which anti-spam checks will be bypassed.

## [Licensing](/docs/mdemail/configuration/settings#licensing)

### [Automatically assign license to users](/docs/mdemail/configuration/settings#automatically-assign-license-to-users)

Email Gateway Security is capable to automatically discover users and count them for licensing using machine learning techniques. To enable automatic user discovery turn **Settings > General / Licensing / Automatically assign license to users** on.

### [Only license users from Active Directory](/docs/mdemail/configuration/settings#only-license-users-from-active-directory)

Email Gateway Security can have a tight integration with Active Directory (or other LDAP based directory services). Enabling **Settings > General / Licensing / Only license users from Active Directory** will make the product to refuse all recipients (for inbound rules) and senders (for outbound rules) that do not exist in the Active Directory.

Licensing non-existing users

Licensing users from Active Directory only can eliminate the risk that non-existing users will be counted for license.

For further details see [Installation/Licensing](/docs/mdemail/installation/licensing) and [Configuration/Server profiles](/docs/mdemail/configuration/server-profiles).

### [Synchronize licensed users with Active Directory](/docs/mdemail/configuration/settings#synchronize-licensed-users-with-active-directory)

Enabling this setting will sync licensed users with users in Active Directory. If certain users have been removed from the Active Directory then those users get unlicensed in Email Gateway Security, too.

Sync time

Synchronization runs once every day at midday according to the server time.

On-demand synchronization to Active Directory is also available. For details see [Operating/User based licensing](/docs/mdemail/operating/user-based-licensing).

### [Block emails whe user or product not licensed](/docs/mdemail/configuration/settings#block-emails-whe-user-or-product-not-licensed)

Enabling this setting will cause Email Gateway Security to block and quarantine emails when recipients or the product is not licensed.

## [Configuration](/docs/mdemail/configuration/settings#configuration)

### [Deployment mode](/docs/mdemail/configuration/settings#deployment-mode)

Deployment mode options are used to evaluate/test MetaDefender Email Gateway Security without necessarily affecting your existing email traffic. The following deployment modes are available:

#### [Protection mode](/docs/mdemail/configuration/settings#protection-mode)

Use this mode when you deploy MetaDefender Email Gateway Security in a production environment. This mode will protect your emails from malicious and untrusted content.** **

#### [Out-of-band monitoring mode](/docs/mdemail/configuration/settings#out-of-band-monitoring-mode)

Use this mode ONLY when you want to evaluate MetaDefender Email Gateway Security in an out-of-band scenario. This mode will NOT deliver any processed email. It requires you to send copies of emails to MetaDefender Email Gateway Security for processing.

#### [Inline monitoring mode](/docs/mdemail/configuration/settings#inline-monitoring-mode)

Use this mode ONLY when you want to evaluate MetaDefender Email Gateway Security without making modifications to processed emails. This mode will NOT protect your emails from malicious or untrusted content.

Notification

A notification message will warn administrators when Email Gateway Security is in a monitoring mode.

### [Public server address](/docs/mdemail/configuration/settings#public-server-address)

**Settings > General / Configuration / Public server address** is the IP or DNS address that will be used in URLs generated by Email Gateway Security (e.g. notifications, reports) to identify this server.

Empty value

When this field is left empty there won't be any links in the notification and reports to this instance.

Publicly visible value

When setting this property please be aware that this address may be sent for recipients outside of your company (e.g. in a notification about password protected document).

### [Use X-Core-Id header for scan URLs](/docs/mdemail/configuration/settings#use-x-core-id-header-for-scan-urls)

When MetaDefender Core servers are behind a load balancer, it is often the load balancer's address that is provided as the Core server address in the Server Profile. The problem with this setup is that when the processing is done, the load balancer won't be able to direct scan result requests to the appropriate Core.

MetaDefender Core can be configured to return its own IP address or FQDN in the newly added `X-Core-Id` custom response header. This header can be used to create a direct link to the scan result, bypassing a load balancer and ensuring that the request is directed to the Core server that processed the email.

Core configuration

The `X-Core-Id` custom header can be configured on Core using the REST API.

For example for Core listening on localhost:8008 you can set the `X-Core-Id` `address_str` to `https://1.2.3.4:8888` sending

`PUT http://**localhost:8008**/admin/config/customresponseheader`

with the request body

`"include_address": { "enabled": true, "address_str": "**https://1.2.3.4:8888**" }, "include_deployment_id": true, "specify_users_agent": { "enabled": false, "allowed_users_agent": [ "kiosk", "email" ] }, "authorized_only": false }`

Default

When this option is enabled but `X-Core-Id` not returned or empty, then scan URLs fall back to the URL defined int the server profile.

Also, the scan is always initiated using the URL defined int the server profile cause Email Gateway Security does not know the `X-Core-Id` yet.

When the option is enabled now on Email Gateway Security and Core returns its custom IP or FQDN in the `X-Core-Id` header, the scan results in Email History and Quarantine will open using the URL from `X-Core-Id`.

### [Login banner](/docs/mdemail/configuration/settings#login-banner)

Enabling the *Show login banner* option a customizable warning text can be displayed in the login screen.

The login banner is text-only, no images or formatted text is supported.

Default

The default banner is:

*This system is for use by authorised users only. User activity may be monitored. Users of this system expressly consent to such monitoring and are advised that if such monitoring reveals possible criminal activity, security staff may provide the evidence of such monitoring to law enforcement officials.*

The text can be at most 1000 characters long.

By default the banner is not enabled.

### [Proxy configuration](/docs/mdemail/configuration/settings#proxy-configuration)

Enabling the *Use proxy server* option instructs Email Gateway Security to use the configured proxy when communicating towards external services (e.g. license activation, MetaDefender Core, etc.).

Email Gateway Security can be configured with a global *proxy / no proxy* option that can be overriden for each connected service type.

## [Attachment password patterns](/docs/mdemail/configuration/settings#attachment-password-patterns)

When extraction of passwords for encrypted attachments is enabled for a security rule (see the section *Encrypted attachments* in [Advanced Threat Prevention](/docs/mdemail/configuration/policy#advanced-threat-prevention)), regular expressions defined in this section are used to attempt to match the passwords.

Regular expression dialect

Email Gateway Security uses *Perl Compatible Regular Expressions* (PCRE) to match passwords in email bodies.

For details see <https://www.pcre.org>.
