<!-- source: https://www.opswat.com/docs/mdcluster/release-notes/release-notes -->

# Release notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| **Version** | 2.10.0 |
| --- | --- |
| **Release date** | 5 October 2026 |
| **Scope** | MetaDefender Cluster 2.10.0 introduces file scanning from URLs, extends processing result reuse to archives, and adds support for OPSWAT Alin AI Deflection. This release also improves Docker deployment, Kubernetes license management, and reliability during file processing. |

## New Features, Improvements and Enhancements

### Scan Files from URLs

You can now submit a file for scanning by providing its URL. The **MetaDefender Cluster Download Service** downloads the file and makes it available for processing. The service also supports Docker deployments, allowing you to use URL-based scanning in these environments.

If the download times out or fails, the result shows **Download Timeout** or **Download Failed** to help you identify the problem. You can configure your workflow to classify these outcomes as Allowed.

### Reuse Processing Results for Archives

The Reuse Processing Results option now supports archive files. When an archive file qualifies for reuse, MetaDefender Cluster uses its previous processing results to avoid repeating the same work. Reuse also covers CDR and DLP compression and supports results with the Exceed Archive Depth verdict.

### **OPSWAT Alin AI Deflection Integration**

MetaDefender Cluster now supports the OPSWAT Alin AI Deflection engine. Deflection information is available in scan results, Processing History, and Executive Reports, so you can review these outcomes alongside other processing results.

---

**Further Enhancements**

**1. Kubernetes License Management**

You can now update licenses through helm upgrade. When a MetaDefender Core instance is uninstalled, its license slot is released so another instance can use it.

**2. Dependency Updates**

- Updated nghttp2 to version **1.70.0**.
- Updated SQLite to version **3.53.4**.

---

**Security Enhancements**

- Updated NGINX to version **1.30.5** to fix a buffer overflow vulnerability.
- Updated OpenSSL to version **3.5.9** to address security issues involving memory handling, denial-of-service, and timing side channels.

---

**RESTful API**

- POST `/file` now supports URL-based scanning through the **MetaDefender Cluster Download Service** using the **downloadfrom** header, with an optional **redirect-support** header for URLs returning 3xx responses without a Location header.
- The following APIs now support **Download Timeout** and **Download Failed** verdicts in their JSON responses for files submitted by URL:

  - `GET/file/{data_id}`
  - `GET/file/batch/{batch_id}`
  - `POST/file/batch/{batch_id}/close`
  - `GET/file/{data_id}/blocked-leaves`
  - `GET/stat/log/scan`

- When OPSWAT Alin AI Deflection is enabled, the JSON responses from GET `/file/{data_id}` and GET `/hash/{hash_id}` now include deflection information in the `deflection_info` field.

---

**Bug Fixes**

- Fixed an issue where MetaDefender Core instances could unexpectedly stop receiving new scan tasks.
- Fixed an issue where a parent scan was marked as finished while its child objects remained stuck in In Progress.
- Fixed an MetaDefender Cluster API Gateway crash when GET `/file/{data_id}` was called after a TLS-enabled Redis connection disconnected and reconnected.

## Known Limitations

- MD Cluster Control Center does not detect duplicate workers when one is added using its IP address and another using its hostname (or vice versa). Registering the same worker multiple times may lead to incorrect license usage calculations.
- In Kubernetes deployments, terminating a MetaDefender Core instance removes it from the processing history filters and leaves an empty slot in its assigned workflows. After redeploying the instance, reassign those workflows to it.
