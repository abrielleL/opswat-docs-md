<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/does-metadefender-storage-security-support-symlinks-scanning- -->

# Does MetaDefender Storage Security support symlinks scanning?

Yes, MDSS fully supports symbolic links (symlinks) **when using the NFS storage type**. This means that MDSS can seamlessly follow these links and process the files they point to.

All major types of symlinks are supported across both **Windows** and **Linux** deployments, including:

- **Soft links (symbolic links)**
- **Hard links**
- **Junction points** (Windows-specific)

| Feature | Soft Link | Hard Link | Junction Point |
| ---- | ---- | ---- | ---- |
| What it is | File containing a path string | Directory entry for file data | Filesystem pointer |
| Points to | File or Directory | File only | Directory only |
| Cross Volume? | Yes | No | Yes (Local Volumes Only) |
| Target Deleted? | Link becomes broken | Other links remain valid | Link becomes broken |
| Platform | Linux/Unix, Windows | Linux/Unix, Windows | Windows only |

---

> **Symlink scanning exclusivity**
>
> Symlink scanning is **exclusively applicable to NFS** and is not supported for other storage types. To learn more about integrating an NFS share, please refer to [this page](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage).

> **Broken link handling in MDSS**
>
> When MDSS encounters a broken link or a link pointing to a non-existent or inaccessible target, it will generate an error indicating that it was unable to locate the file at the specified path (the path to which the broken symlink was pointing).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
