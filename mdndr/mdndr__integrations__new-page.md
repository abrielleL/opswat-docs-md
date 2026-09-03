<!-- source: https://www.opswat.com/docs/mdndr/integrations/new-page -->

# Integrations

This page describes the enterprise integrations that MetaDefender NDR adds in v5.2.0. It covers Single Sign-On (SSO) for administrator access and Security Information and Event Management (SIEM) integration through syslog.

For the full Administration-page reference for all integrations, see the [Integrations chapter](/docs/mdndr/operating-guide/integrations) in the Operating Guide.

## [Single Sign-On (SSO)](/docs/mdndr/integrations/new-page#single-sign-on-sso)

MetaDefender NDR supports Single Sign-On (SSO) through a trusted Identity Provider (IdP). Your organization uses the IdP to control the access to the Manager. SSO removes the need for a separate local account for each administrative user.

Configure the role mapping rules and keep one local administrator account before you enable SSO. A local account gives you access when the IdP is not available.

### [Supported protocols](/docs/mdndr/integrations/new-page#supported-protocols)

MetaDefender NDR supports these authentication protocols:

- **Security Assertion Markup Language 2.0 (SAML 2.0).** The Manager is the Service Provider (SP). The Manager supports the SP-initiated flow and the IdP-initiated flow.
- **OpenID Connect (OIDC).** OIDC is the preferred protocol for Microsoft Entra ID.

### [Supported identity providers](/docs/mdndr/integrations/new-page#supported-identity-providers)

| Identity Provider | Recommended protocol | Notes |
| --- | --- | --- |
| **Microsoft Entra ID** (formerly Azure AD) | OIDC | SAML 2.0 is an alternative. Entra ID is the primary target for enterprise deployments. |
| **Okta** | SAML 2.0 or OIDC | Both protocols are supported. |
| **A SAML 2.0 compliant IdP** | SAML 2.0 | Use the general SAML 2.0 option for any compliant IdP. |

### [Key capabilities](/docs/mdndr/integrations/new-page#key-capabilities)

- **Just-In-Time (JIT) provisioning.** The Manager creates a user account automatically at the first login. You do not create the account in the Manager first.
- **Role mapping.** The Manager maps a group from the IdP to an NDR role, for example Admin or Analyst. The role controls the permissions of the user through Role-Based Access Control (RBAC).
- **Local fallback.** You can keep local username and password authentication as a fallback. Use a local account for the initial setup and for a break-glass situation.
- **Single Logout (SLO).** The Manager supports Single Logout (SLO) when the IdP supports it. The Manager logs the user out when the user logs out of the IdP.
- **Multi-factor authentication (MFA).** The Manager honors the MFA policy of the IdP, for example a Microsoft Entra ID Conditional Access policy or an Okta MFA policy.
- **Audit logging.** The Manager records each authentication event in the audit log. The events are a successful login, a failed login, and a role change.

### [Security](/docs/mdndr/integrations/new-page#security)

The Manager uses a secure protocol, a signed assertion, and an encrypted token. The Manager validates the IdP certificate and supports certificate rotation.

### [Configure SSO](/docs/mdndr/integrations/new-page#configure-sso)

1. Open the Manager.
2. Go to Administration.
3. Select Authentication.
4. Select the identity provider (Microsoft Entra ID, SAML 2.0, or Okta).
5. Upload the IdP metadata, or enter the configuration fields manually.
6. Upload the IdP certificate.
7. Configure the role mapping rules.
8. Enable JIT provisioning.
9. Set the local fallback option.
10. Save the configuration.
11. Select Test connection to validate the IdP.

### [Not available in this release](/docs/mdndr/integrations/new-page#not-available-in-this-release)

Do not expect these functions in this release. Plan your rollout without them.

- System for Cross-domain Identity Management (SCIM) provisioning.
- Multiple identity providers at the same time.
- A passwordless method, for example FIDO2 or a passkey.

## [SIEM Integration via Syslog](/docs/mdndr/integrations/new-page#siem-integration-via-syslog)

The Manager forwards logs to one or more external SIEM platforms over syslog. Syslog integration is the primary way that MetaDefender NDR events reach a long-term retention, correlation, and compliance pipeline.

For the complete field-level reference, the REST surface, and the connectivity test, see [SIEM Integration via Syslog](/docs/mdndr/operating-guide/integrations#siem-integration-via-syslog) in the Operating Guide.

### [What gets forwarded](/docs/mdndr/integrations/new-page#what-gets-forwarded)

The Manager forwards seven log categories. The Manager sends each category in real time and keeps the full context, for example the sensor identifier and the tenant identifier.

- **Audit.** User actions and system actions, for example a login, a policy change, or a configuration change.
- **Engine.** Suricata engine events, rule reloads, and detection-engine lifecycle.
- **System.** Operating system, service, and resource logs from the Manager and the sensors.
- **Alert.** Suricata alerts, C2 alerts, MetaDefender Core verdicts, machine-learning anomaly detections, and threshold detections.
- **File info.** Carved artifact metadata, with or without a MetaDefender Core verdict.
- **Enrichment.** Threat-intelligence enrichment results applied to events.
- **Session.** Suricata protocol events, for example HTTP, Domain Name System (DNS), and TLS.

### [Transport and formats](/docs/mdndr/integrations/new-page#transport-and-formats)

This release forwards standard syslog over User Datagram Protocol (UDP) on port 514. You can override the destination port for each destination. Each destination has its own filter rules and format.

The Manager supports the RFC 5424 format by default. You can select the Common Event Format (CEF) for a destination whose SIEM expects that format.

Syslog over Transmission Control Protocol (TCP) and Transport Layer Security (TLS) per RFC 5425 is planned for a later release. The certificate store for syslog ships in this release to support a low-effort migration.

### [Configure a syslog destination](/docs/mdndr/integrations/new-page#configure-a-syslog-destination)

The Manager sends all syslog messages. A sensor sends its events to the Manager first. A sensor does not send syslog directly to an external destination.

1. Open the Manager.
2. Go to Administration.
3. Go to Integrations.
4. Select Syslog.
5. Add a destination.
6. Enter the destination hostname or IP address, and the port.
7. Select the log categories for this destination.
8. Select the format (RFC 5424 or CEF).
9. Save the destination.
10. Run the connectivity test.

## [See Also](/docs/mdndr/integrations/new-page#see-also)

- [Integrations chapter (Operating Guide)](/docs/mdndr/operating-guide/integrations)
- [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac)
- [Administration Page](/docs/mdndr/operating-guide/administration-page)
- [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration)
