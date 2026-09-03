<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/what-happens-if-the-os-hostname-changes- -->

# What happens if the OS hostname changes?

Summarize Page    Connect to Cursor Connect to VS Code

Problem description: MetaDefender Managed File Transfer™ is bound to the hostname of the machine/OS that hosts it. MetaDefender Managed File Transfer™ will not auto-update its own settings when a hostname change occurs on OS level. Any config or integration that references the old host will break until updated.

Info

Changing hostname on OS level is usually not a problem when a stable DNS alias is used in MetaDefender Managed File Transfer™ configurations as it is not directly bound to the machine's hostname.

## [What symptoms might occur?](/docs/mdmft/knowledge-base/what-happens-if-the-os-hostname-changes-#what-symptoms-might-occur)

- Broken links, invalid redirects, or redirect_uri errors
- TLS/HTTPS failures due to certificate name mismatch
- SSO (SAML/OIDC) callbacks failing
- Requests rejected by AllowedHosts/CORS or wrong proxy binding
- Webhooks/callbacks/self-referential URLs hitting the old host
- Monitoring, alerts, or firewall rules tied to the old host failing

## [What app config must be updated?](/docs/mdmft/knowledge-base/what-happens-if-the-os-hostname-changes-#what-app-config-must-be-updated)

- Server bindings: HTTP(s) hostnames
- TLS certification

Refer to [Server Configuration](/docs/mdmft/configuration/server-configuration) to update the above properties.
