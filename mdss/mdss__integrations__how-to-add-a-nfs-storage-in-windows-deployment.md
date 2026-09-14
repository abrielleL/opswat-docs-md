<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-in-windows-deployment -->

# [Windows] How to add an NFS storage unit

For steps 1 and 2, please see [this page](https://docs.opswat.com/mdss/integrations/add-a-nfs-storage)

Limitation

NFS shares originating from **Dell OneFS PowerScale** are incompatible with MDSS deployments on Windows. A Linux-based MDSS deployment is required to scan these shares.

To add NFS share on Linux deployment, please follow [this article](/docs/mdss/integrations/how-to-add-a-nfs-storage-unit-in-linux-deployment).

### [3. Setting up the NFS Client machine](/docs/mdss/integrations/how-to-add-a-nfs-storage-in-windows-deployment#3-setting-up-the-nfs-client-machine)

On the same machine where MetaDefender Storage Security is installed, run this powershell command from an admin console:

BashCopyInstall-WindowsFeature NFS-Client

With the default options, a user has read permissions when mounting an NFS share using the anonymous user. We can give the anonymous user write permissions by changing the UID and GID that it uses to mount the share.

To change the UID and GID we must make a simple change to the Windows registry by performing the following steps:

- Open regedit by typing it in the search box end pressing Enter.
- Browse to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default`.
- Create a new New DWORD (32-bit) Value inside the Default folder named `AnonymousUid` and assign the UID 0
- Create a new New DWORD (32-bit) Value inside the Default folder named `AnonymousGid` and assign the GID 0
- Reboot the machine to apply the changes.

### [4. Mount the NFS share](/docs/mdss/integrations/how-to-add-a-nfs-storage-in-windows-deployment#4-mount-the-nfs-share)

The below command needs to be run as NTSYSTEM user because NFS service is running as NTSYSTEM user.

To run terminal as NTSYSTEM, please do the following:

- download and extract [PsTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools)
- Open an Administrator console
- cd to PsTools folder
- run `.\PsExec.exe -i -s cmd.exe` . It will open another terminal as a NTSYSTEM user

In the above-opened terminal, run the following command:

BashCopymount -o "nolock,sec=sys" {nfs-server-ip}:{nfs-share-location} {mounted-drive}

For example, the NFS share will be mounted in the Y drive:

BashCopymount -o "nolock,sec=sys" 192.168.207.139:/srv/company-public-files/ Y:

To make the mount persistent, please follow [this article](/docs/mdss/knowledge-base/windows-deployment--how-to-create-a-persistent-mount-for-smb-and).

### [5. Add the NFS share in MDSS UI](/docs/mdss/integrations/how-to-add-a-nfs-storage-in-windows-deployment#5-add-the-nfs-share-in-mdss-ui)

In order to integrate NFS with MetaDefender Storage Security, please follow these steps:

1. From the left side menu, navigate to **Storage units,** click on **Add storage unit** and choose **NFS**

2. Give your [accounts](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Assign a meaningful name to your NFS storage for easy identification later.
4. Input the mount drive used at step 4. In this example, should be `Y:\`
5. Click **Add** in order to finish the process.

Info

Please follow the [Microsoft recommendations](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#naming-conventions) for file and directory names.
