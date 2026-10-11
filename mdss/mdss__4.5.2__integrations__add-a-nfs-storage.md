<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/add-a-nfs-storage -->

# Add an NFS Storage

**Network File System (NFS)** is a popular distributed file system protocol that allows a user on a client computer to access files over a network in a manner similar to how local storage is accessed. This document guides you through the process of integrating NFS storage with MetaDefender Storage Security.

### 1. Understanding NFS Server and Client

In a NFS setup, there are two primary components:

1. **NFS Server**: This is the machine where your files are stored. It must be configured to share files using the NFS protocol.
2. **NFS Client**: This is the machine where MetaDefender Storage Security is installed. It accesses the files stored on the NFS Server.

### 2. Setting up the NFS Server machine

Please make sure your files are shared via NFS protocol.

To enable remediations capabilities of MetaDefender Storage Security (sanitization, file moving / deleting), we need to have write access to your shared folder. To allow write access, please choose the appropriate configuration for your server. More details [in this article](https://www.opswat.com/docs/mdss/integrations/what-is-user-squashing-for-network-file-system-nfs).

The next steps are tailored to your deployment type, please choose yours:

- [Windows deployment](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-in-windows-deployment)
- [Linux deployment](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-unit-in-linux-deployment)

> **Info**
>
> **Symlink Support:** MetaDefender Storage Security is able to follow all types of symbolic links (symlinks)  and process the files they point to when integrating with NFS storage on both Linux and Windows deployments. This includes:
>
> - **Soft links (symbolic links)**
> - **Hard links**
> - **Junction points (on Windows)**
>
> For more details on this functionality, follow [this link](https://www.opswat.com/docs/mdss/knowledge-base/does-metadefender-storage-security-support-symlinks-scanning-).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
