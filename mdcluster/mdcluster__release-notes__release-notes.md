<!-- source: https://www.opswat.com/docs/mdcluster/release-notes/release-notes -->

# Release notes

| **Version** | 2.9.1 |
| --- | --- |
| **Release date** | 15 September 2026 |
| **Scope** | MetaDefender (MD) Cluster 2.9.1 optimizes large archive processing to reduce memory and disk usage under heavy workloads, improves MD Core Worker reliability on non-English Windows systems, strengthens MD Cluster File Storage handling, resolves container build and REST API validation issues, and updates OpenSSL with the latest security fixes. |

---

**Improvements**

Improved MD Core resource management when scanning large archives to reduce excessive memory and disk usage and prevent archive processing from affecting other scans. Archive extraction now uses dedicated processing resources and releases threads while waiting, improving stability under heavy archive workloads.

---

**Security Enhancements**

Upgraded OpenSSL to version **3.5.8** to address known security vulnerabilities.

---

**Bug Fixes**

- Fixed an issue that could make MD Cluster Workers unusable on non-English Windows installations due to locale-dependent CPU metric collection.
- Fixed an issue that could cause Debian-based Docker image builds to fail when retrieving the `libtiff5` package required by Deep CDR.
- Fixed issues in MD Cluster File Storage gzip processing that could cause processing to hang on malformed data, accept truncated compressed content, or decompress data without a size limit.

## [Known Limitations](/docs/mdcluster/release-notes/release-notes#known-limitations)

- MD Cluster Control Center does not detect duplicate workers when one is added using its IP address and another using its hostname (or vice versa). Registering the same worker multiple times may lead to incorrect license usage calculations.
- In Kubernetes deployments, terminating a MetaDefender Core instance removes it from the processing history filters and leaves an empty slot in its assigned workflows. After redeploying the instance, reassign those workflows to it.
