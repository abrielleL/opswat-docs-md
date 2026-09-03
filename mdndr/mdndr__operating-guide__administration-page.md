<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/administration-page -->

# Administration Page

This chapter introduces the Administration page of MetaDefender NDR. The Administration page is the single place where system administrators configure the Manager, adopt and govern sensors, manage users, schedule updates, wire in integrations, and set data-retention policy. Each subsequent chapter in this section describes one surface. This overview explains the page, access, and configuration propagation.

This chapter is for system administrators, Site Reliability Engineers (SREs), and analyst leads who own configuration of a MetaDefender NDR deployment. It assumes an installed Manager with at least one adopted sensor and an administrator account.

First-use acronym expansions in this chapter:

- SRE (Site Reliability Engineer)
- UI (user interface)
- RBAC (role-based access control)
- DNS (Domain Name System)
- NTP (Network Time Protocol)
- SMTP (Simple Mail Transfer Protocol)
- SSL (Secure Sockets Layer)
- SNMP (Simple Network Management Protocol)
- MOTD (Message of the Day)
- SIEM (Security Information and Event Management).

## [The Administration page](/docs/mdndr/operating-guide/administration-page#the-administration-page)

The Administration page is the central configuration surface of the Manager. It consolidates every system-wide setting, per-sensor configuration control, and administrative workflow behind a single tabbed page optimized for large desktop monitors. Administrators open it from the main sidebar; the default landing tab is the Manager Configuration section. The Manager controls versions for all changes here. The Manager requires confirmation before changes take effect. The audit trail records each change.

**📷 INSERT IMAGE HERE**

*Subject:* The Administration page top-level layout showing the Manager Configuration and Sensor Management sections side by side.

*Suggested capture:* `/administration/configuration` at 1440×900, full viewport, with the left-rail navigation expanded so the section grouping is visible.

## [Two-section layout](/docs/mdndr/operating-guide/administration-page#two-section-layout)

The Administration Functional Requirements Document (FRD) defines two primary sections. Both are reachable from the Administration page's top-level tabs.

- **Manager Configuration.** This section contains global settings for the Manager. These settings include hostname, MOTD, notice and consent banner, retention settings, syslog forwarding, automatic update settings, upstream Hypertext Transfer Protocol (HTTP) proxy, SMTP, DNS, NTP, timezone, password complexity, account logon controls, integration settings, SSL certificate, and SNMP. Sixteen distinct settings exist in total. Each setting applies to the Manager first. If the setting supports inheritance, it propagates to every sensor that the Manager governs.
- **Sensor Management.** This section contains configuration for sensors and sensor groups. It includes the sensor list view with filter and search. It also includes group creation and management. It includes per-sensor Suricata configuration surfaces (Detect Engine, Basic Global Settings, AF_PACKET, Threading and CPU Affinity, Stream and Flow, File Extraction, Logging and Stats, Output). Bulk operations apply one configuration or policy change across every member of a group. The adoption process completes most sensor configuration automatically. Administrators use this section for governance and per-sensor overrides.

A third administrative surface, the Access page, is co-located with the two FRD sections in the UI and hosts user, group, and role management. The chapters that follow cover it under [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac).

## [Who can access administration](/docs/mdndr/operating-guide/administration-page#who-can-access-administration)

The Administration page accepts administrative roles only. Non-administrator users (Security Operations Center (SOC) analysts, hunters, compliance auditors) have no link to it and no Uniform Resource Locator (URL) path into it.

- **Super Administrator.** Full administrative authority across every Manager section, every sensor, every group, every user, and every integration. Installation creates this account. The deployment requires at least one Super Administrator account.
- **Tenant Administrator.** Administrative authority scoped to the tenant's assets — sensors, groups, users, and integrations that the tenant owns. Tenant Administrators cannot configure Manager-global settings that cross tenant boundaries.

[Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) documents the full seven-role matrix. It includes Super Administrator, Tenant Administrator, Group Administrator, SOC Analyst, Security Engineer, Read-Only Analyst, and Compliance Auditor. It also includes the page-by-page permission map.

## [Audit trail](/docs/mdndr/operating-guide/administration-page#audit-trail)

The Manager records every change on the Administration page in an immutable audit log. The log captures the actor, the changed setting, the prior and new values, and the timestamp. It also captures a correlation identifier for downstream propagation events. Audit records are tamper-proof, searchable, and exportable; the chapter on [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) describes the audit viewer and its filters in detail. The storage layer also controls versions for configuration changes. An administrator can reconstruct an earlier state if a change must be reverted. Because the administrator confirms each change before the Manager applies it, the audit log distinguishes intended changes from accidents. The confirmation dialog is the last gate before the log entry is written.

## [How configuration changes propagate](/docs/mdndr/operating-guide/administration-page#how-configuration-changes-propagate)

The Administration page is the entry point; the underlying configuration pipeline is what actually delivers a change to the Manager process or to a sensor. At a high level the pipeline has three stages: validation, persistence, and broadcast. When an administrator confirms a change, the server validates it against the product ontology. The server persists the new value to the configuration store. Then the server broadcasts the change to every affected service. Affected services apply the new value live where possible. They report their health back to the configuration store. The UI shows that health in the status of each setting.

A small subset of settings require a service restart to take effect. Each form identifies those settings. The [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration) chapter also lists them in a table. The remainder apply in place within seconds of confirmation.

The dedicated configuration guide gives the step-by-step rules. It explains value validation, propagation, and health reports. Administrators read that guide to debug a configuration that did not take effect. They also use it to trace a health-report failure or understand precedence rules.

| Chapter | Covers |
| --- | --- |
| [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration) | The sixteen Manager-global settings — hostname, MOTD, banners, retention, syslog, automatic updates, proxy, SMTP, DNS, NTP, timezone, password policy, logon controls, integrations, SSL, SNMP. |
| [Sensor Management](/docs/mdndr/operating-guide/sensor-management) | Sensor adoption, grouping, per-sensor Suricata configuration, bulk operations, health monitoring cross-link, and disown/decommission. |
| [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) | The seven predefined roles, user and group lifecycle, asset ownership, password and multi-factor policies, the audit log viewer, and the multi-tenancy foundation. |
| [Updates Management](/docs/mdndr/operating-guide/updates-management) | OPSWAT InSights intelligence feeds, signature updates, automatic and manual update modes, per-sensor distribution status, and policy-based enable/disable. |
| [Integrations](/docs/mdndr/operating-guide/integrations) | MetaDefender Core and MetaDefender Cloud, SIEM integration over User Datagram Protocol (UDP) syslog, and Recorded Future threat intelligence. |
| [Data Retention](/docs/mdndr/operating-guide/data-retention) | Retention periods for alerts, sessions, files, flows, and packet captures; storage-backend mapping; capacity planning; pre-expiry export. |

## [See also](/docs/mdndr/operating-guide/administration-page#see-also)

- [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring) — the operational view that complements the configuration view, used after a configuration change to confirm services are healthy.
- [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration) — the deep dive on configuration validation, propagation, precedence, and troubleshooting.
