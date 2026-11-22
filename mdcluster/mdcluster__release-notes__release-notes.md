<!-- source: https://www.opswat.com/docs/mdcluster/release-notes/release-notes -->

# Release notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | 2.11.1 |
| --- | --- |
| **Release date** | 20 November 2026 |
| **Scope** | MetaDefender Cluster 2.11.1 is a maintenance release focused on improving security by updating the bundled NGINX component. |

**Security Enhancements**

- Upgraded NGINX to version **1.30.7**

## [Known Limitations](/docs/mdcluster/release-notes/release-notes#known-limitations)

- MD Cluster Control Center does not detect duplicate workers when one is added using its IP address and another using its hostname (or vice versa). Registering the same worker multiple times may lead to incorrect license usage calculations.
- In Kubernetes deployments, terminating a MetaDefender Core instance removes it from the processing history filters and leaves an empty slot in its assigned workflows. After redeploying the instance, reassign those workflows to it.
