<!-- source: https://www.opswat.com/docs/mdss/release-notes/release-notes -->

# Release notes

## [**MetaDefender™ Storage Security 4.5.2**](/docs/mdss/release-notes/release-notes#metadefender-storage-security-452)

**Release date:** August 19, 2026

**End of support**: February 19, 2028

#### [**Maintenance Release**](/docs/mdss/release-notes/release-notes#maintenance-release)

- Deep CDR carries dedicated workflow branches for file types it does not sanitize, so you can keep, move, copy or delete them and clear the source folder in one pass.
- Workflows validate before a scan runs, and Deep CDR requires an API key on every scan instance in the primary and failover pools.
- Reports name the exact outcome per file, including unsupported file types, the sanitization detail returned by MD Core, and the remediation you configured.
- Scanning applies a retry budget while MD Core is busy and holds its scaling steady while an instance is unavailable, so throughput stays predictable under load.
- Stopping a real-time scan completes in seconds, the report refreshes on its own, and rescan sits in the report actions.
- Schedules coordinate so a location runs one scan at a time, consecutive FTP scans run back to back, and real-time scans follow newly created child folders.
- The portable package and the offline Docker toolkit deploy on a clean host, and upgrades carry databases holding non-Latin file names.
- MDSS runs on the cache you already have, including AWS ElastiCache, and reads CPU and memory from pod limits on Kubernetes.
- The NetApp ONTAP Connector ships at 1.0.44 with the full share path, so several SVMs connect to one MDSS.
- OPSWAT SAML sign-on, email notifications and telemetry collectors follow your configuration, and inventory tables let you pick the columns you need.

## [**MetaDefender™ Storage Security 4.5.1**](/docs/mdss/release-notes/release-notes#metadefender-storage-security-451)

**Release date:** July 30, 2026

**End of support**: January 30, 2028

#### [**Maintenance Release**](/docs/mdss/release-notes/release-notes#maintenance-release)

- Real-time protection jobs each apply their own workflow, so multiple policies can run against a single storage unit.
- Disk usage in the warning band keeps scanning running, scan health reflects real load, and autoscaling ships enabled on all deployment types with per-instance sizing recommendations.
- The NetApp ONTAP Connector delivers files over HTTPS, and you can configure the response it returns to NetApp when a file scan times out.
- Real-time protection keeps its status and discovery cycle detail, and partition-based FTP scans resume without reconfiguration.
- Stopped jobs report accurately, their files can be rescanned in place, FTP scans run to completion, and event-based scans handle partitioned storage units.
- Remediation actions deliver to a second destination, tags follow files moved into folder-based units, and Central Management copy workflows run as configured.
- PDF exports honor the filters you applied accurately per storage unit.
- The dashboard loads faster against a 10 million file scan with a searchable unit selector, and job schedules support valid month days and 52-week cycles.
- Single sign-on from the virtual appliance keeps its identity provider, notification targets are validated, and S3 accounts show the correct region and endpoint fields

---

### [**MetaDefender™ Storage Security 4.5.0**](/docs/mdss/release-notes/release-notes#metadefender-storage-security-450)

**Release date:** July 22, 2026

**End of support**: January 22, 2028

#### [**Highlights**](/docs/mdss/release-notes/release-notes#highlights)

MetaDefender Storage Security 4.5.0 introduces a redesigned user interface, centralized management through OPSWAT Central Management (OCM) v10, a new autoscaling engine, significant security enhancements, and multiple platform and storage integration improvements.

#### [**New Features**](/docs/mdss/release-notes/release-notes#new-features)

#### [**Redesigned User Interface**](/docs/mdss/release-notes/release-notes#redesigned-user-interface)

The application has been rebuilt using the Blue Line design system, delivering a modern user experience with:

- Updated Dashboard, Reports, Inventory, Jobs, Workflows, Settings, and Users pages
- Improved reporting with dedicated Threats, Sanitization, and Data Loss Prevention views
- Guided onboarding for first-time deployments
- Dark theme support
- Backward-compatible legacy URL redirects

#### [**OPSWAT Central Management (OCM) v10 Integration**](/docs/mdss/release-notes/release-notes#opswat-central-management-ocm-v10-integration)

MetaDefender Storage Security now supports centralized management through OCM v10, including:

- Instance enrollment and license management
- Remote configuration
- Deployment ID synchronization across managed environments

#### [**Autoscaling Engine**](/docs/mdss/release-notes/release-notes#autoscaling-engine)

A new autoscaling engine dynamically adjusts system resources based on workload.

Key capabilities include:

- CPU, memory, and file throughput monitoring
- Scaling recommendations
- `/healthz` endpoint for health monitoring
- Dashboard visibility into scaling status

Supported deployment models include MetaDefender Core, Cloud and Distributed Cluster.

#### [**New SMB Service for Windows deployments**](/docs/mdss/release-notes/release-notes#new-smb-service-for-windows-deployments)

The Windows SMB Service is a new, fully in-house SMB client implementation for Windows deployments. Built with no third-party dependencies, it delivers improved reliability and resolves the connection issues found in earlier versions.

---

#### [**Security Improvements**](/docs/mdss/release-notes/release-notes#security-improvements)

This release includes multiple security enhancements, including:

- Fixes for OData injection vulnerabilities
- License forgery protection
- Penetration testing remediations, including JWT secret removal, improved SSO security, and sensitive data protection
- Non-root container enforcement for Kubernetes deployments
- Improved Windows file permission security

---

#### [**Platform Improvements**](/docs/mdss/release-notes/release-notes#platform-improvements)

Platform updates include:

- Updated infrastructure components (RabbitMQ, Garnet, Alpine Linux)
- Improved job dispatcher with automatic recovery for orphaned scan jobs
- Configurable scan result retention policies
- Database growth monitoring and protection
- Decoupled scanning service architecture for cross-product reuse
- Prevention of overlapping scans within storage groups
- Optimized scanning and results storage for archives

---

#### [**Storage and Integration Improvements**](/docs/mdss/release-notes/release-notes#storage-and-integration-improvements)

Storage connectors have been enhanced with improved reliability and functionality, including:

- Better error reporting for NFS and SFTP
- Improved SharePoint Cloud real-time protection
- Microsoft Graph connection throttling for OneDrive and SharePoint
- NetApp ONTAP enhancements
- Autodiscovery support for all S3-compatible storage providers
- Updated Diode integration documentation

---

#### [**Telemetry**](/docs/mdss/release-notes/release-notes#telemetry)

Telemetry has been renamed **Usage Report** and now includes:

- Kubernetes containerized collector
- Improved usage reporting accuracy

---

#### [**Resolved Issues**](/docs/mdss/release-notes/release-notes#resolved-issues)

This release resolves several issues, including:

- Scheduled scans starting at incorrect times due to timezone offsets
- Recovery of cancelled or stuck scan jobs after service restart
- Dashboard threat counts matching report data
- Improved stability when scanning large file volumes
- RabbitMQ startup synchronization issues
- Improved error handling across storage integrations

---

### [**Known limitation: Remediation counters on reports for scans performed before version 4.0.0**](/docs/mdss/release-notes/release-notes#known-limitation-remediation-counters-on-reports-for-scans-performed-before-version-400)

After upgrading from a version earlier than 4.0.0, reports for scans that completed on the older version may display inconsistent remediation counters:

- The **Keep** counter may show 0 even when files were kept.
- The **Remediated** counter excludes kept files, so it may show 0 when keeping files was the only configured remediation action.

All other values on these reports remain accurate, including the allowed and blocked file totals and the **Move**, **Copy**, **Delete**, and **Tagging** counters.

This limitation applies only to scans completed before the upgrade. Scans performed after the upgrade display all counters correctly.
