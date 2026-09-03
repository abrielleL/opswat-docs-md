<!-- source: https://www.opswat.com/docs/mdcluster/release-notes/release-notes -->

# Release notes

| **Version** | 2.9.0 |
| --- | --- |
| **Release date** | 26 August 2026 |
| **Scope** | MetaDefender (MD) Cluster 2.9.0 improves file scanning and result access from MD Cluster Control Center, provides greater control over how MD Core instances are assigned to workflows, and adds RAM disk and TLS configuration options. This release also simplifies Kubernetes and container operations, enhances Processing History and Proactive DLP usability, strengthens container security, updates key third-party components, and resolves customer-reported issues. |

## [New Features, Improvements and Enhancements](/docs/mdcluster/release-notes/release-notes#new-features-improvements-and-enhancements)

### [Scan and Access Results from Control Center](/docs/mdcluster/release-notes/release-notes#scan-and-access-results-from-control-center)

Users can now submit files for scanning directly from MetaDefender (MD) Cluster Control Center, view scan results, and look up previous results by data ID or file hash.

When available, sanitized or processed files can also be downloaded directly from MD Cluster Control Center. Anonymous scanning is supported when anonymous access is enabled.

### [Assign Specific MD Core Workers to Workflows](/docs/mdcluster/release-notes/release-notes#assign-specific-md-core-workers-to-workflows)

Administrators can now assign specific MD Core to individual workflows, providing greater control over which MD Core instances process requests for each workflow.

Assigned instances are displayed with CPU and memory information, making it easier to identify and manage the appropriate processing instances.

### [RAM Disk Support](/docs/mdcluster/release-notes/release-notes#ram-disk-support)

MD Cluster now supports configuring MD Core working and temporary directories to use a RAM disk. This can reduce disk I/O and improve processing performance in environments with sufficient memory.

### [TLS Configuration for RabbitMQ and Redis](/docs/mdcluster/release-notes/release-notes#tls-configuration-for-rabbitmq-and-redis)

MD Cluster Control Center now provides TLS configuration options when adding or editing RabbitMQ and Redis service connections. Administrators can enable TLS, configure certificate verification, and specify a CA certificate path directly from Control Center.

---

**Further Enhancements**

**1. Simplified Kubernetes and Container Deployment**

Kubernetes and container deployments are now easier to manage with a unified Helm chart, bundled MD Core installers, improved service import, and improved graceful shutdown behavior.

**2. Simplified HTTPS Configuration for Kubernetes Deployments**

Improved HTTPS configuration for Kubernetes deployments, making it easier to enable secure connections for Control Center and API Gateway.

**3. Customizable Processing History CSV Export**

Users can now choose which fields are included when exporting Processing History data to CSV, providing greater flexibility for reporting and integration with external systems.

**4. Improved Proactive DLP Regex Selection**

Improved the Proactive DLP configuration experience by displaying regex entries loaded from TSV files and allowing users to select which regex patterns are used for processing.

**5. Allow Zero Active AV Engines in System Health**

The Minimum number of active AV engines setting can now be configured to `0`, supporting deployments that use technologies such as Deep CDR or Proactive DLP without requiring antivirus engines.

---

**Security Enhancements**

MD Cluster containers running on Kubernetes are now configured to run as non-root users with additional security restrictions, including prevention of privilege escalation and read-only root file systems.

Several bundled components have been updated to improve security, stability, and compatibility, including:

- PostgreSQL 18.6
- nghttp2 1.70.0
- SQLite 3.53.4

---

**RESTful API**

- Added support for the `client-identity` header in the POST `/file` API endpoint provided by MD Cluster API Gateway.

---

**Bug Fixes**

- Fixed an issue where invalid or malformed `metadata` headers were not validated correctly or could return incorrect error messages.
- Improved MD Cluster File Storage cleanup to ensure orphaned physical files are removed correctly and do not accumulate over time.

## [Known Limitations](/docs/mdcluster/release-notes/release-notes#known-limitations)

- MD Cluster Control Center does not detect duplicate workers when one is added using its IP address and another using its hostname (or vice versa). Registering the same worker multiple times may lead to incorrect license usage calculations.
- In Kubernetes deployments, terminating a MetaDefender Core instance removes it from the processing history filters and leaves an empty slot in its assigned workflows. After redeploying the instance, reassign those workflows to it.
