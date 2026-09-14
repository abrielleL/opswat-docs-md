<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-unit-in-linux-deployment -->

# [Linux] How to add an NFS storage unit

For steps 1 and 2, please see [this page](https://docs.opswat.com/mdss/integrations/add-a-nfs-storage)

### [3. Setting up the NFS Client machine](https://docs.opswat.com/mdss/integrations/add-a-nfs-storage#3-setting-up-the-nfs-client-machine)

Before integrating NFS storage with MetaDefender Storage Security, a mount needs to be created from the NFS Client machine to the NFS Server. Follow these steps **on the NFS Client machine**:

1. Install NFS:

   - For Debian-based distributions, install `nfs-common`.
   - For Fedora-based distributions, install `nfs-utils`.
   - Our product is not bound to a specific NFS version. It should work as expected with the version provided by the above package.
2. Prepare the Mount Directory:

   - The default directory for all mounts is `/mnt/mdss/nfs`. Within this directory, create a new folder, for example, `company-files`, where the NFS mount will be performed

Info

/mnt/mdss/nfs is the default mount directory. This can be changed a custom location by setting *NFS_MOUNT_LOCATION=/path/to/your/location* in customer.env. Information on how to modify customer.env: [Custom configuration](/docs/mdss/configuration/custom-configuration)

All new files and folders created by MetaDefender Storage Security (during Sanitization, Remediations) will adopt the same read, write and execute permissions as the parent directory. This means you need to set the appropriate permissions to the `company-files` folder in order new items to be accessible for the desired audience.

1. Perform the NFS Mount:

   - Execute the following command: **sudo mount -t nfs -o rw,hard,intr,nolock {nfs-server-ip}:/srv/company-shared-files /mnt/mdss/nfs/company-shared-files/**
   - This command mounts the shared files from the NFS Server to the `company-files` directory on the NFS Client.
   - It is required the `mount`command to have the `nolock` flag as some older NFS servers are locking the file when opened by another application. Apart from `nolock` , we do not require any specific flags. As long as the mount command is working as expected and we have permissions to the mount directory, should be enough. READ permissions are required for scanning, WRITE permissions are required for remediation operations that implies writing to the storage.
2. Ensure Persistent Mounting:

   - To maintain the mount across reboots, add the following entry to the `/etc/fstab` file: `{nfs_server_ip}:/srv/company-shared-files /mnt/mdss/nfs/company-files nfs rw,hard,intr,nolock 0 0`
   - Without this step, the mount will be lost when the NFS Client machine is restarted.

### [4. Adding an NFS storage in MDSS](https://docs.opswat.com/mdss/integrations/add-a-nfs-storage#4-adding-an-nfs-storage-in-mdss)

In order to integrate NFS with MetaDefender Storage Security, please follow these steps:

1. From the left side menu, navigate to **Storage units,** click on **Add storage unit** and choose **NFS**

2. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Assign a meaningful name to your NFS storage for easy identification later.
4. Input the mount directory where your NFS shared files are mounted on the MetaDefender Storage Security machine. For instance, if your files are mounted at `/mnt/mdss/nfs/company-files`, simply enter `company-files` in the text box.
5. Click **Add** in order to finish the process.

Warning

Absolute paths (e.g. `/home`) are not functional in versions prior to 4.4.0. Paths configured this way must be manually reconfigured using relative paths — there is no automatic migration.

Starting in 4.4.0, path normalization (`/home` → `home`) is supported for newly created storage.

### [5. Additional NFS Configuration](/docs/mdss/integrations/how-to-add-a-nfs-storage-unit-in-linux-deployment#5-additional-nfs-configuration)

NFS offers a wide range of configurations to suit different needs. For more detailed information on NFS configurations, please refer to the following resources based on your operating system:

- [NFS Server](https://www.server-world.info/en/note?os=Fedora_34&p=nfs&f=1) and [NFS Client](https://www.server-world.info/en/note?os=Fedora_35&p=nfs&f=2) configuration on Fedora
- [NFS Server and NFS Client](https://ubuntu.com/server/docs/service-nfs) configuration on Ubuntu
