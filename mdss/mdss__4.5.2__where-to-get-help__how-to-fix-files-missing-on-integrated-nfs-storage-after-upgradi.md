<!-- source: https://www.opswat.com/docs/mdss/4.5.2/where-to-get-help/how-to-fix-files-missing-on-integrated-nfs-storage-after-upgradi -->

# NFS storage unit is not detecting any files

## Root Cause

The `nolock` flag was not included in the NFS mount command previously. While it is generally not required, certain environments, especially those using older NFS servers or specific NFS configurations, depend on this flag to ensure proper file access during MDSS scans. In such cases, omitting the `nolock` flag can lead to scanning failures.

Some older NFS servers lock files when opened by another application, which prevents MDSS from scanning them. To prevent this issue, the `nolock` flag is required in the mount command.

## Solution

### [Linux]

1. Execute the following command to mount the NFS storage: `sudo mount -o nolock {nfs_server_ip}:/srv/company-shared-files /mnt/mdss/nfs/company-files`

This command mounts the shared files from the NFS Server to the company-files directory on the NFS Client.

2. Ensure Persistent Mounting To maintain the mount across reboots, add the following entry to the `/etc/fstab` file: `{nfs_server_ip}:/srv/company-shared-files /mnt/mdss/nfs/company-files nfs rw,hard,intr,nolock 0 0`

Without this step, the mount will be lost when the NFS Client machine is restarted.

For more details, refer to this article: [[Linux] How to add an NFS storage unit](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-unit-in-linux-deployment)

### [Windows]

For instructions on setting up NFS storage in Windows, refer to the following article: [[Windows] How to add an NFS storage unit](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-in-windows-deployment)

Following the instruction mentioned in the article and in the terminal, run the following command:

`mount -o "nolock,sec=sys" {nfs-server-ip}:{nfs-share-location} {mounted-drive}`

For example, the NFS share will be mounted in the Y drive:

`mount -o "nolock,sec=sys" 192.168.207.139:/srv/company-public-files/ Y:`

> **Support:**
>
> If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
