<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/third-party-integrations -->

# Third Party Integrations

MetaDefender NDR connects to other security tools in your environment. These integrations extend detection, response, and context. The platform supports these integration types:

- **SIEM**: Syslog (UDP 514 / TLS) forwards all events, alerts, and analytics.
- **SOAR**: REST API and webhook triggers start automated playbooks.
- **EDR/XDR**: Correlation through API or syslog adds endpoint context enrichment.
- **Sandboxes**: Automatic file submission sends extracted files to an external sandbox.
- **Identity solutions**: Active Directory, LDAP, and Okta integration adds user context.
- **Access control**: Dynamic block through firewall or Network Access Control (NAC) APIs acts on threat verdicts.

For the response integrations that stop an attack, the platform uses the firewall and NAC APIs. A threat verdict triggers a block action at the enforcement point. The sensor stays passive and does not sit inline.

## [See also](/docs/mdndr/deployment-guide/third-party-integrations#see-also)

- Network services and external dependencies
- Communication ports and protocols
