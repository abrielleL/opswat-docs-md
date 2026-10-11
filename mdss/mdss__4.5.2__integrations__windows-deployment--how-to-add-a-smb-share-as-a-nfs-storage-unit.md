<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/windows-deployment--how-to-add-a-smb-share-as-a-nfs-storage-unit -->

# [Windows] How to Expose an SMB Share as an NFS Storage Unit

> This guide uses the **SMB/CIFS protocol** exclusively for all storage operations. Despite references to "NFS storage" in MDSS terminology, no NFS (Network File System) protocol is involved.  The term "NFS storage" refers to MDSS's storage subsystem name that is using the local file system API, not the NFS network protocol. **All connections use SMB/CIFS (Common Internet File System).**

### 1. Map SMB share as a drive

The below command needs to be run as NTSYSTEM user because our internal NFS service is  running as NTSYSTEM user.

To run terminal as NTSYSTEM, please do the following (on the same machine where MetaDefender Storage Security is installed):

- download and extract [PsTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools)
- Open an Administrator console
- cd to PsTools folder
- run `.\PsExec.exe -i -s cmd.exe`  . It will open another terminal as a NTSYSTEM user

In the above-opened terminal, run the following command:

```bash
net use {drive-letter} {smb-share-path} /user:{DOMAIN\username} {password} /persistent:yes
```

Alternatively, if supported, you can map the drive using QUIC transport:

```bash
net use {drive-letter} {smb-share-path} /user:{DOMAIN\username} {password} /persistent:yes /TRANSPORT:QUIC
```

For example, this SMB share is mapped to drive G:

```bash
net use G: \\152.168.212.101\smb-share /user:OPSWAT\smbuser smbpassword1234 /persistent:yes
```

> **Warning**
>
> The SMB share mapping configured using this method is temporary and will not survive system reboots. **The mapping will be automatically removed when the machine is restarted.**
>
> **To create a persistent mapping** please refer to [this article.](https://www.opswat.com/docs/mdss/knowledge-base/windows-deployment--how-to-create-a-persistent-mount-for-smb-and).

### 2. Add the SMB share as NFS storage in MDSS UI

In order to integrate NFS with MetaDefender Storage Security, please follow these steps:

1. From the left side menu, navigate to **Storage units** and choose **+ Add Storage Unit** and then select **NFS:**

![](https://uploads.developerhub.io/prod/k8zL/q3ejsgvleuzovsgbraxvlfs122tsgolqmrh4xi5hm623uqqduyh1xvrf2o5hl1j3.png)

2. Assign a meaningful name to your NFS storage for easy identification later.
3. Input the mount drive used at step 1. In this example, should be `G:\`
4. Click **Add** in order to finish the process.

> **Info**
>
> Please follow the [Microsoft recommendation](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#naming-conventions) for file and directory names.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
