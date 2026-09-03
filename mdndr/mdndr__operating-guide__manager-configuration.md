<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/manager-configuration -->

# Manager Configuration

The Manager Configuration section of the Administration page holds the sixteen global settings that govern the MetaDefender NDR Manager itself. This chapter documents each setting and its place in the user interface. It also documents validation behavior and restart requirements. It also walks three common configuration procedures and closes with a quick-start checklist operators use when bringing a new deployment online.

This chapter is for system administrators and Site Reliability Engineers (SREs) who maintain a MetaDefender NDR Manager. It assumes an installed Manager, an administrator account, and familiarity with the Administration page layout described in the [Administration Page](/docs/mdndr/operating-guide/administration-page).

First-use acronym expansions in this chapter:

- DNS (Domain Name System)
- NTP (Network Time Protocol)
- SMTP (Simple Mail Transfer Protocol)
- SSL (Secure Sockets Layer)
- TLS (Transport Layer Security)
- SNMP (Simple Network Management Protocol)
- MOTD (Message of the Day)
- HTTP (Hypertext Transfer Protocol)
- SIEM (Security Information and Event Management)
- UI (user interface)
- API (application programming interface)
- MVP (Minimum Viable Product)
- REST (Representational State Transfer)
- IANA (Internet Assigned Numbers Authority).

## [Overview](/docs/mdndr/operating-guide/manager-configuration#overview)

Administrators reach the Manager Configuration section from the Administration page by selecting the **Configuration** tab. The tab presents a left-rail navigation drawer grouped by category (Network, Security, System, Integrations) and a scrollable right-hand stack of configuration cards. Each card is a form bound to one setting group -- DNS, NTP, SMTP, and so on. Each card has its own **Save** and **Reset** buttons that activate only when a field in that card has been edited, and every save round-trip routes through the central configuration pipeline so that validation, version history, and audit logging apply uniformly.

Not every setting ships with a graphical form in the current release. Several of the sixteen FRD-scoped settings are API-first in MVP. A subsequent release will add a user-interface surface for those settings. Administrators can fully configure those settings through the REST API of the Manager's server-manager service. The reference table below flags those settings. The UI and the API use identical functional behavior. This behavior includes validation rules, restart behavior, propagation, and audit.

## [Settings reference](/docs/mdndr/operating-guide/manager-configuration#settings-reference)

The table below enumerates the sixteen Manager Configuration settings defined in the Administration Functional Requirements Document (FRD). "Required restart" indicates whether you must restart the Manager or an affected service. Settings marked "No" apply live within seconds of confirmation.

| Setting | Purpose | Required restart | Notes |
| --- | --- | --- | --- |
| Hostname | Sets the Manager's network hostname and display name. | Yes (Manager) | Surfaces in dashboards, audit records, and outbound SIEM events. |
| MOTD | Sets the Message of the Day shown on the login screen. | No | Plain text; no Markdown. |
| Notice and Consent Banner | Sets the legal and consent banner shown above the login form. | No | Customers with regulatory requirements commonly use this surface. |
| Data Management and Retention | Sets retention periods for alerts, sessions, files, flows, and packet captures. | No | Deep dive in [Data Retention](/docs/mdndr/operating-guide/data-retention) |
| Syslog Configuration | Forwards Manager and sensor logs to one or more remote syslog collectors. | No | User Datagram Protocol (UDP) syslog in MVP; deep dive in [Integrations](/docs/mdndr/operating-guide/integrations). |
| Automatic Update Settings | Controls the cadence for OPSWAT InSights feed and signature updates. | No | Default cadence is one hour; deep dive in [Updates Management](/docs/mdndr/operating-guide/updates-management) |
| Upstream HTTP Proxy | Routes outbound Manager traffic (updates, cloud enrichments) through a corporate proxy. | Yes (affected services) | Broadcast reaches every enrichment service, the updater, and the Elasticsearch bridge. |
| SMTP | Configures an external SMTP relay for email notifications. | Yes (Manager) | Manager-local; not broadcast to sensors. |
| DNS | Sets primary and secondary DNS resolvers. | Yes (Manager and sensors) | Broadcast reaches every service. |
| NTP Server | Sets one or two NTP servers for time synchronization. | Yes (Manager and sensors) | Optional keyed authentication. |
| Timezone | Sets the system timezone used for UI rendering and log timestamps. | Yes (Manager) | IANA timezone names (for example, `America/Chicago`). |
| Password Complexity | Enforces password length, complexity, expiration, and history rules. | No | The Manager evaluates policy at user-save time. For details, see [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac). |
| Account Logon Access Control | Governs account lockout, session timeout, and concurrent-login limits. | No | Lockout thresholds apply on the next failed login after save. |
| Integration Settings | Wires in MetaDefender Core, MetaDefender Cloud, Recorded Future, and SIEM destinations. | No | Deep dive in integrations. |
| SSL Certificate | Uploads the server certificate and private key used by the Manager UI over HTTPS. | Yes (Manager) | Multipart upload against the REST API in MVP. |
| SNMP | Exposes Manager health metrics over SNMP for external monitoring. | Yes (Manager) | SNMPv2c and SNMPv3 supported. |

## [Setting details](/docs/mdndr/operating-guide/manager-configuration#setting-details)

### [Hostname](/docs/mdndr/operating-guide/manager-configuration#hostname)

Short description: the Manager's fully-qualified network hostname. The Manager writes the hostname to outbound syslog, SNMP traps, and any audit export. Thus, use a consistent naming scheme across a multi-Manager deployment.

UI location: Configuration -> System -> Hostname.

Validation: the Manager checks the value against RFC-1123 hostname rules. Labels are 1-63 characters, alphanumeric plus hyphen, not starting or ending with a hyphen. Total length is at most 253. A rename triggers a Manager restart and, in deployments where the hostname appears in issued certificates, may require a new SSL certificate upload.

### [MOTD](/docs/mdndr/operating-guide/manager-configuration#motd)

Short description: the Message of the Day rendered above the login form. Operators use it to communicate maintenance windows, escalation contacts, or shift notes.

UI location: Configuration -> System -> Message of the Day.

Validation: plain-text, length-bounded. The Manager renders the banner verbatim -- no Markdown, no HTML -- to avoid injection risk on an unauthenticated page.

### [Notice and consent banner](/docs/mdndr/operating-guide/manager-configuration#notice-and-consent-banner)

Short description: the legal or consent banner displayed above the login form. Common content includes regulatory warnings (for example, banking or critical-infrastructure consent text) and terms-of-use statements.

UI location: Configuration -> System -> Notice and Consent Banner.

Validation: plain-text, length-bounded. If the "require explicit acknowledgement" toggle is on, users must acknowledge the banner before the login form accepts credentials.

### [Data management and retention](/docs/mdndr/operating-guide/manager-configuration#data-management-and-retention)

Short description: retention periods for each category of stored data -- alerts, sessions, files, flow records, and packet captures. The retention policy caps how long each category lives in its storage backend before age-off.

UI location: Configuration -> System -> Data Retention.

Validation: each category has its own lower bound (days or hours depending on category) and an upper bound derived from the deployment's storage capacity. The Manager rejects out-of-range values on save. Deep dive in [Data Retention](/docs/mdndr/operating-guide/data-retention).

### [Syslog configuration](/docs/mdndr/operating-guide/manager-configuration#syslog-configuration)

Short description: forwards Manager logs (audit, system, engine) and enriched alert events to one or more remote syslog collectors. Administrators use this surface to feed MetaDefender NDR events into a SIEM.

UI location: API-first in MVP. Administrators drive the surface through the REST endpoints `GET/POST /api/server/syslog-forward` and test it with `POST /api/server/syslog-forward/test`. OPSWAT plans a graphical form for a subsequent release.

Validation: the Manager validates each destination for a resolvable host and a port in the 1-65535 range. If TLS is enabled, the Manager also requires a matching client certificate in the syslog-forward certificate store. You can run a connectivity test before you save. Deep dive in [Integrations](/docs/mdndr/operating-guide/integrations).

### [Automatic update settings](/docs/mdndr/operating-guide/manager-configuration#automatic-update-settings)

Short description: the cadence at which the Manager polls OPSWAT InSights for new intelligence feeds and new signature packs. The default interval is one hour for feeds and one day for signatures.

UI location: Configuration -> System -> Automatic Updates.

Validation: the product ontology bounds the interval at a minimum frequency and a maximum frequency. The minimum avoids excessive polling. The maximum avoids feed staleness. Deep dive in [Updates Management](/docs/mdndr/operating-guide/updates-management).

### [Upstream HTTP proxy](/docs/mdndr/operating-guide/manager-configuration#upstream-http-proxy)

Short description: routes outbound Manager traffic through a corporate HTTP/HTTPS proxy. Applies to intelligence feed downloads, cloud-backed enrichment lookups, and the update channel.

UI location: Configuration -> Network -> Upstream Proxy.

Validation: the Manager checks the host for resolvability and the port for the 1-65535 range. The Manager stores credentials encrypted. The Manager broadcasts the configuration change to the enrichment services, the updater, and the Elasticsearch bridge. Each affected service restarts its outbound HTTP client to use the new proxy.

### [SMTP](/docs/mdndr/operating-guide/manager-configuration#smtp)

Short description: the outbound SMTP relay used for email notifications -- password-reset emails, administrative alerts, and license-expiry notices.

UI location: Configuration -> Network -> SMTP.

Validation: the Manager network must reach the host. The port must be in the 1-65535 range. The TLS toggle controls whether the Manager negotiates STARTTLS on the relay connection. The From and Reply-To addresses must be valid email addresses. SMTP configuration is Manager-local -- the setting is not broadcast to sensors.

### [DNS](/docs/mdndr/operating-guide/manager-configuration#dns)

Short description: primary and optional secondary DNS resolvers used by the Manager and every sensor. The Manager accepts both IPv4 and IPv6 resolver addresses.

UI location: Configuration -> Network -> DNS.

Validation: the Manager checks each address for well-formedness as an IPv4 or IPv6 address. The Manager broadcasts the change to every service. The Manager and each sensor rewrite their host resolver configuration on the underlying operating system. They restart any client pool that caches resolver handles.

### [NTP server](/docs/mdndr/operating-guide/manager-configuration#ntp-server)

Short description: one or two NTP servers used for time synchronization. Optional keys authenticate the exchange.

UI location: Configuration -> Network -> NTP.

Validation: each host must be a reachable IPv4 address. The Manager stores keys encrypted. The change is broadcast to every service and applied host-side by rewriting the time-daemon configuration and restarting that daemon.

### [Timezone](/docs/mdndr/operating-guide/manager-configuration#timezone)

Short description: the Manager's system timezone. Governs log timestamp rendering, UI time display, and the alignment of scheduled jobs.

UI location: Configuration -> System -> Timezone.

Validation: the value must be a valid IANA timezone identifier (for example, `UTC`, `America/Chicago`, `Europe/Berlin`). The Manager rejects invalid values on save.

### [Password complexity](/docs/mdndr/operating-guide/manager-configuration#password-complexity)

Short description: enforces password length, character-class mix, maximum age (expiration), and reuse history. The Manager evaluates the policy every time an administrator or user sets a password.

UI location: Configuration -> Security -> Password Policy.

Validation: each rule has its own bounds (minimum length at least 8, history depth at least 0, expiration days at least 0). A relaxed policy applies only to future password changes -- existing passwords are not invalidated. Deep dive in [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac).

### [Account logon access control](/docs/mdndr/operating-guide/manager-configuration#account-logon-access-control)

Short description: account lockout policy (failed-attempt threshold and window), session timeout, and concurrent-login limits.

UI location: Configuration -> Security -> Account Logon.

Validation: lockout threshold and window are positive integers. The Manager bounds session timeout to prevent indefinite sessions. Concurrent-login limits apply per user. Lockout thresholds apply on the next failed login after save -- already-locked accounts are not retroactively unlocked by raising the threshold.

### [Integration settings](/docs/mdndr/operating-guide/manager-configuration#integration-settings)

Short description: the shared surface for external integrations -- MetaDefender Core and MetaDefender Cloud for file scanning, Recorded Future for threat intelligence, and SIEM destinations (see Syslog Configuration above).

UI location: Configuration -> Integrations.

Validation: varies by integration. Each integration form runs a connectivity probe before persisting credentials. Deep dive in [Integrations](/docs/mdndr/operating-guide/integrations).

### [SSL certificate](/docs/mdndr/operating-guide/manager-configuration#ssl-certificate)

Short description: the server certificate and private key used by the Manager UI when reached over HTTPS.

Administrators upload certificates through `POST /api/server/tls/certificates` (multipart form upload of the certificate and key) and check status with `GET /api/server/tls/certificates`. A graphical upload form is planned for a subsequent release.

Validation: the Manager parses the uploaded certificate. It checks for a matching private key, validity dates, and the Manager hostname as a common-name or subject-alternative-name match. The Manager rejects mismatches before it installs the certificate. You must restart the Manager for the new certificate to bind.

### [SNMP](/docs/mdndr/operating-guide/manager-configuration#snmp)

Short description: exposes Manager health metrics over SNMP for an external network-management station (NMS).

UI location: Configuration -> System -> SNMP.

Validation: the Manager stores the community string (for SNMPv2c) or user and authentication/privacy credentials (for SNMPv3) encrypted. The port must be in the 1-65535 range. Enabling SNMP binds the Manager's SNMP agent on that port. You must restart the Manager.

## [Validation, confirmation, and propagation](/docs/mdndr/operating-guide/manager-configuration#validation-confirmation-and-propagation)

Every save on a Manager Configuration card uses the same pipeline. The Manager validates the value against the product ontology. It persists the value to the configuration store with a new version identifier. It broadcasts the value to every affected service. Affected services apply the new value live where they can. They report health back to the configuration store. The UI shows that health in the status line on each card. The form shows a banner for settings that require a restart before **Save** is active. The confirmation dialog shows the restart requirement again. The underlying rules for validation, propagation order, health reporting, and precedence when group-level and sensor-level overrides disagree live in the [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration).

The audit trail records each completed save with the actor, prior and new values, timestamp, and correlation identifier. The Manager controls versions for configuration changes. You can restore an earlier version of any setting through the `/api/server/config/:configType/versions` and `/api/server/config/:configType/revert` REST endpoints.

## [Common procedures](/docs/mdndr/operating-guide/manager-configuration#common-procedures)

### [Change the Manager hostname](/docs/mdndr/operating-guide/manager-configuration#change-the-manager-hostname)

1. Confirm with stakeholders that downstream consumers are prepared for the new hostname. These consumers include SIEM collectors, certificate subjects, firewall rules, and bookmarks.
2. Navigate to Administration -> Configuration -> System -> Hostname.
3. Enter the new fully-qualified hostname and click **Save**.
4. Acknowledge the restart-required banner in the confirmation dialog.
5. Wait for the Manager to restart (typically under a minute). The UI becomes unreachable at the old hostname at this point.
6. Reconnect using the new hostname. If the Manager UI uses an SSL certificate whose subject does not match the new hostname, follow "Uploading a New SSL Certificate" next.
7. Verify the audit log shows the hostname-change entry with the correct actor and timestamp.

### [Upload a new SSL certificate](/docs/mdndr/operating-guide/manager-configuration#upload-a-new-ssl-certificate)

1. Obtain the server certificate and private key files from the certifying authority or internal public-key infrastructure. Both must be PEM-encoded.
2. Verify locally that the certificate matches the Manager hostname. The hostname must appear as the common name or a subject-alternative-name entry.
3. Upload the pair through the REST API with a multipart `POST /api/server/tls/certificates` request. Supply the certificate and the private key as form parts.
4. The Manager validates the pair, rejects on mismatch or expiry, and otherwise installs the certificate into its TLS keystore.
5. Restart the Manager so the new certificate binds.
6. Reconnect and verify the browser accepts the new certificate.
7. Verify the audit log shows the certificate-rotation entry.

### [Configure SMTP](/docs/mdndr/operating-guide/manager-configuration#configure-smtp)

1. Obtain the SMTP relay details from the networking team. These details include host, port, STARTTLS requirement, and service-account credentials if authenticated.
2. Navigate to Administration -> Configuration -> Network -> SMTP.
3. Enter Host, Port, enable TLS if the relay requires STARTTLS, and populate Username and Password.
4. Enter a From address that the relay accepts (commonly `ndr-noreply@<organization-domain>`) and a Reply-To address that routes to a staffed mailbox.
5. Enter a To address for the connectivity test. Typically, use an administrator mailbox that accepts inbound mail from the From address.
6. Click **Save** and acknowledge the restart-required dialog. The Manager restarts its mail client.
7. Trigger a test notification. For example, request a password reset for a test account. Verify that the message arrives at the destination mailbox.
8. Verify the audit log shows the SMTP-configuration entry.

## [Quick-start checklist](/docs/mdndr/operating-guide/manager-configuration#quick-start-checklist)

The checklist below runs through the Manager Configuration settings that operators typically set before a MetaDefender NDR deployment enters daily use. Items that link to later chapters receive their full treatment there; this list is a pre-production sanity pass.

| Item | Action | Verification |
| --- | --- | --- |
| Hostname | Set the Manager hostname and confirm the Manager restarts cleanly. | The UI is reachable at the new hostname; the audit log shows the change. |
| DNS | Configure primary and (optional) secondary DNS resolvers. | Resolution tests from the Manager and one adopted sensor succeed for a known hostname. |
| NTP | Configure one or two NTP servers. | The Manager and each sensor show a time offset under one second in health monitoring. |
| Timezone | Set the IANA timezone. | UI timestamps and exported logs render in the expected local time. |
| SSL Certificate | Upload a certificate whose subject matches the Manager hostname. | The browser connects without warning; `GET /api/server/tls/certificates` returns the new subject and expiry. |
| SMTP | Configure the outbound SMTP relay. | A test password-reset email delivers to the destination mailbox. |
| Upstream HTTP Proxy | Configure the proxy if the Manager cannot reach the Internet directly. | The next automatic update check succeeds; the enrichment services report healthy. |
| Automatic Updates | Verify the default one-hour feed cadence meets organizational policy. | [Updates Management](/docs/mdndr/operating-guide/updates-management) verification steps pass. |
| Syslog Configuration | Wire the Manager to the organization's SIEM. | The SIEM receives events within minutes of the first alert; the connectivity-test endpoint succeeds. |
| SNMP | Enable SNMP if an NMS will poll the Manager. | The NMS receives responses on the configured port. |
| Notice and Consent Banner | Apply the organization's login-screen legal text. | The banner renders on the login page. |
| MOTD | Apply any operator-shift or maintenance message. | The MOTD renders on the login page. |
| Password Complexity | Align the password policy with organizational policy. | The Manager rejects new user creation when a user enters a weak password. |
| Account Logon Access Control | Set lockout, session timeout, and concurrent-login limits. | A deliberate failed-login run locks the test account as expected. |
| Data Management and Retention | Confirm default retention matches the organization's policy. | [Data Retention](/docs/mdndr/operating-guide/data-retention) verification steps pass. |
| Integration Settings | Wire in MetaDefender Core and Cloud, Recorded Future, and SIEM as applicable. | [Integrations](/docs/mdndr/operating-guide/integrations) verification steps pass for each wired integration. |

## [See also](/docs/mdndr/operating-guide/manager-configuration#see-also)

- [Administration Page](/docs/mdndr/operating-guide/administration-page) -- the Administration page structure, access control, audit trail, and chapter map.
- [Sensor Management](/docs/mdndr/operating-guide/sensor-management) -- per-sensor configuration and overrides, including settings that inherit from the Manager.
- [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration) -- deep dive on validation, propagation, precedence, and troubleshooting of configuration changes.
