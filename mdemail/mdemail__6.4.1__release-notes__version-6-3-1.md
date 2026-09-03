<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/release-notes/version-6-3-1 -->

# Version 6.3.1

| Release date | Scope |
| --- | --- |
| 23rd February, 2026 | This release features GUI based proxy configuration for all external services. |

## [New & improved](/docs/mdemail/6.4.1/release-notes/version-6-3-1#new--improved)

### [Proxy configuration](/docs/mdemail/6.4.1/release-notes/version-6-3-1#proxy-configuration)

Email Gateway Security can now be configured with a global *proxy / no proxy* option that can be overriden for each connected service type.

For details see [Proxy configuration](/docs/mdemail/6.4.1/configuration/settings#proxy-configuration).

### [Graph API server profile](/docs/mdemail/6.4.1/release-notes/version-6-3-1#graph-api-server-profile)

Besides SMTP, outbout email submission is now supported via Graph API to Microsoft 365 as the email destination.

For details see [Microsoft 365 via Graph API](/docs/mdemail/6.4.1/configuration/server-profiles#microsoft-365-via-graph-api).

Licensing

This feature licenses separately, not available by default.

### [Rescan notifications](/docs/mdemail/6.4.1/release-notes/version-6-3-1#rescan-notifications)

If notifications are configured for quarantined emails, Email Gateway Security will send the notification again when the email gets rescanned (directly from **Quarantine**, from the actions of a notification or a quarantine report email) and after the rescan it is kept being quaranined.

For details see [Alert, notification and quarantine report emails](/docs/mdemail/6.4.1/configuration/alert--notification-and-quarantine-report-emails).

## [Changed](/docs/mdemail/6.4.1/release-notes/version-6-3-1#changed)

### [SMTP server profiles](/docs/mdemail/6.4.1/release-notes/version-6-3-1#smtp-server-profiles)

To cover integration to Microsoft 365 via SMTP, connectors and Graph API, the server profile type `SMTP server` was extended to the server profile type `Outbound server` .

The `Integration type` property of this new server profile type can switch between the traditional SMTP integration (default) and the new Graph API integration.

Old SMTP server type server profile:

The same with the new configuration:

Backwards compatible change

This change is backwards compatible. During an upgrade old server profiles are automatically upgraded.
