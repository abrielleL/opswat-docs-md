<!-- source: https://www.opswat.com/docs/mdss/integrations/recommended-approach-when-adding-smb-compatible-storage -->

# Recommended approach when adding SMB units on Linux deployments

This article is **applicable only for MetaDefender Storage Security deployed on Linux**. If your deployment is on **Windows**, please follow [this article](/docs/mdss/integrations/add-an-smb-compatible-unit-in-windows-deployments).

For production environments, we recommend using **OS-level SMB/CIFS mounts** instead of application-level connections.

This approach provides:

- Better stability under high load
- Improved file descriptor management
- Enhanced performance
- More reliable connections

Success

Many of our enterprise customers have already migrated to OS-level SMB mounts and are experiencing significantly improved stability and performance in their production environments.

## [Why We Recommend This Approach](/docs/mdss/integrations/recommended-approach-when-adding-smb-compatible-storage#why-we-recommend-this-approach)

Through extensive testing and production deployments, we've identified challenges with the **3rd-party SMB client library** that we are using when handling:

- **High concurrent workloads**: connection drops intermittently
- **Large file descriptor usage**: the SMB client library may open excessive file descriptors, leading to system resource exhaustion
- **Connection stability**: Network interruptions can cause SMB connections created from the SMB client library to become stale or unresponsive

## [Technical Background](/docs/mdss/integrations/recommended-approach-when-adding-smb-compatible-storage#technical-background)

OS-level mounts leverage the operating system's native **SMB/CIFS** **client**, which:

- **Handles connection pooling automatically**: The OS manages connection lifecycle and recovery
- **Manages file descriptors more efficiently**: Kernel-level implementation prevents descriptor leaks
- **Provides better fault tolerance**: Built-in retry logic and connection recovery
- **Reduces application-level overhead**: Direct kernel I/O without library abstraction layers

This configuration has been validated across multiple production deployments with varying workloads and is now our recommended best practice for enterprise installations.

## [Choose Your Platform](/docs/mdss/integrations/recommended-approach-when-adding-smb-compatible-storage#choose-your-platform)

- **Linux Deployment**: [[Linux] How to Expose an SMB Share as an NFS Storage Unit](/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage)
