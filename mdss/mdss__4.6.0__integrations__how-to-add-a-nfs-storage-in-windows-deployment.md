<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/how-to-add-a-nfs-storage-in-windows-deployment -->

# [Windows] How to add an NFS storage unit

> **Info**
>
> For steps 1 and 2, please see [this page](https://docs.opswat.com/mdss/integrations/add-a-nfs-storage)

> **Limitation**
>
> NFS shares originating from **Dell OneFS PowerScale** are incompatible with MDSS deployments on Windows. A Linux-based MDSS deployment is required to scan these shares.
>
> To add NFS share on Linux deployment, please follow [this article](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-nfs-storage-unit-in-linux-deployment).

### 3. Setting up the NFS Client machine

On the same machine where MetaDefender Storage Security is installed, run this powershell command from an admin console:

```bash
Install-WindowsFeature NFS-Client
```

With the default options, a user has read permissions when mounting an NFS share using the anonymous user. We can give the anonymous user write permissions by changing the UID and GID that it uses to mount the share.

To change the UID and GID we must make a simple change to the Windows registry by performing the following steps:

- Open regedit by typing it in the search box end pressing Enter.
- Browse to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default`.
- Create a new New DWORD (32-bit) Value inside the Default folder named `AnonymousUid`  and assign the UID 0
- Create a new New DWORD (32-bit) Value inside the Default folder named `AnonymousGid`  and assign the GID 0
- Reboot the machine to apply the changes.

### 4. Mount the NFS share

The below command needs to be run as NTSYSTEM user because NFS service is running as NTSYSTEM user.

To run terminal as NTSYSTEM, please do the following:

- download and extract [PsTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools)
- Open an Administrator console
- cd to PsTools folder
- run `.\PsExec.exe -i -s cmd.exe`  . It will open another terminal as a NTSYSTEM user

In the above-opened terminal, run the following command:

```bash
mount -o "nolock,sec=sys" {nfs-server-ip}:{nfs-share-location} {mounted-drive}
```

For example, the NFS share will be mounted in the Y drive:

```bash
mount -o "nolock,sec=sys" 192.168.207.139:/srv/company-public-files/ Y:
```

To make the mount persistent, please follow [this article](https://www.opswat.com/docs/mdss/knowledge-base/windows-deployment--how-to-create-a-persistent-mount-for-smb-and).

### 5. Add the NFS share in MDSS UI

In order to integrate NFS with MetaDefender Storage Security, please follow these steps:

1. As NFS is not using any credentials, you can have only one NFS account in MDSS. If you already have one, please go to step 4
2. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **NFS (Network File System)** and click **Next**.
3. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

![](https://uploads.developerhub.io/prod/k8zL/g6dgyoqfjltaer0fs3otqo4brtcuhlc3ds3ilc8za17iey0tojokqxgupi57krxg.png)

4. From the left side menu, navigate to **Inventory**, click **Add New** > **Unit**, choose the NFS account created above and click **Next**.

![](https://uploads.developerhub.io/prod/k8zL/hvb3u8lduluzlwty0zhamiq5kw3gvr36293i0z0ouvzbgwu37ag1jibviru01gdm.png)

5. Give your unit an unique name so you can easily identify it later
6. Assign your unit to a Group
7. In **Mount Directory**, enter the drive the share was mounted on in *4. Mount the NFS share*. In this example, `Y:\`
8. Click **Next** in order to finish the process.

> **Info**
>
> Please follow the [Microsoft recommendations](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#naming-conventions)  for file and directory names.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
