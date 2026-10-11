<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/how-to-add-a-smb-share-as-a-nfs-storage -->

# Add an SMB-Compatible unit in Linux deployments

> This guide uses the **SMB/CIFS protocol** exclusively for all storage operations. Despite references to "NFS storage" in MDSS terminology, no NFS (Network File System) protocol is involved.  The term "NFS storage" refers to MDSS's storage subsystem name that is using the local file system API, not the NFS network protocol. **All connections use SMB/CIFS (Common Internet File System).**

> This article is **applicable only for MetaDefender Storage Security **deployed on** Linux distributions**.
>
> If your MetaDefender Storage Security is deployed on **Windows Server**, please follow [this article](https://www.opswat.com/docs/mdss/integrations/add-an-smb-compatible-unit-in-windows-deployments).

## Prerequisites

1. A Linux machine where MetaDefender Storage Security is installed (let's call it MDSS machine)
2. An SMB share from a Linux or Windows machine

## Step-by-Step Guide

Follow these steps to configure the SMB share as an NFS storage unit in MDSS:

### Step 1: Install cifs-utils

On the MDSS machine, you will need the **cifs-utils** package to enable mounting of SMB shares.

Install it using your distribution's package manager.

### Step 2: Create new mounting directory

Create a dedicated directory on the MDSS machine where the SMB share will be mounted.

The new directory must be at the following path **/mnt/mdss/nfs/{my-new-folder}** where **{my-new-folder}** is a name you choose for your share.

### Step 3: Perform the mount

This step involves preparing credentials and then executing the mount command.

#### **3.1 Create a credentials file containing the SMB server credentials**

Create a file, for instance at **/etc/smb-credentials**, to store the SMB server login details. The file should contain:

```powershell
username={username}
password={password}
domain={domain} # optional
```

Replace **{username}, {password}** and (if needed) **{domain}** with the actual credentials for the SMB share.

> **Security Recommendation**
>
> It's recommended to use separate credential files for different shares

#### **3.2 Secure the credentials file**

To protect the sensitive information in the credentials file, restrict its permissions and ownership:

- set permissions so only the owner can read and write:

```bash
sudo chmod 600 /etc/smb-credentials
```

- set ownership to root:

```bash
sudo chown root:root /etc/smb-credentials
```

#### **3.3 Perform the mount**

Execute the mount command to connect the SMB share to the directory you created. The command format is:

```bash
sudo mount -t cifs //server/share /mnt/mdss/nfs/{my-new-folder} -o credentials=/etc/smb-credentials,uid=0,gid=0,file_mode=0655,dir_mode=0755
```

- replace /`/server/share` with the actual path to your SMB share
- replace `/mnt/mdss/nfs/{my-new-folder}` with the mount directory you created.
- ensure the path to your credentials file is correct

> **Info**
>
> The mount command offers various configurable parameters. You can adapt these to your specific requirements.
>
> MDSS will work with any configuration as long as the SMB share is mounted successfully and MDSS has at least read access. For remediation capabilities, write access will be necessary.

### Step 4: Ensure mount is persistent

To make sure the SMB share automatically mounts after the MDSS machine restarts, add an entry to the `/etc/fstab` file. Without this, the mount will be lost upon reboot.

An example entry in `/etc/fstab` might look like this (adapt it to your specific paths and options):

```bash
//server/share   /mnt/mdss/nfs/{my-new-folder}   cifs   credentials=/etc/smb-credentials,uid=0,gid=0,file_mode=0655,dir_mode=0755   0   0
```

You may need to adjust options like **uid** and **gid** to ensure proper file permissions for MDSS.

### Step 5: Add the mounted directory in MDSS

In order to integrate SMB share as NFS unit with MetaDefender Storage Security, please follow these steps:

1. As NFS is not using any credentials, you can have only one NFS account in MDSS. If you already have one, please go to step 4
2. From the left side menu, navigate to **Inventory,** click on **Add account** and choose **NFS**.
3. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

![](https://uploads.developerhub.io/prod/k8zL/g6dgyoqfjltaer0fs3otqo4brtcuhlc3ds3ilc8za17iey0tojokqxgupi57krxg.png)

4. From the left side menu, navigate to **Inventory,** click on **Add unit** and choose the previously created account.

![](https://uploads.developerhub.io/prod/k8zL/hvb3u8lduluzlwty0zhamiq5kw3gvr36293i0z0ouvzbgwu37ag1jibviru01gdm.png)

5. Give your unit an unique name so you can easily identify it later
6. Assign your unit to a Group
7. Specify the **Mount directory** as the folder you created and used in Step 2 (**{my-new-folder}**)
8. Click **Next** in order to finish the process.

> **Info**
>
> To avoid authentication issues the Username should have one of the following formats:
>
> - local users should be .\username (for example: .\Administrator)
> - domain users should be username@domain or domain\username

> **Info**
>
> A Samba file server needs to be enabled in order to connect to a Unix-based system **SharePath.** Since Samba doesn’t use the system account password, it needs to be set up using the *sudo smbpasswd -a username* command.

> **Info**
>
> If you use a hostname in the host portion of IPv4/v6 socket address, the program may show a non-deterministic behavior. The socket address will be resolved differently into an actual IPv4/v6 address, depending on the results from DNS resolution and/or the host configuration. For deterministic behavior use a numeric address in host portion.

> **Info**
>
> Windows client shares have a default configuration of 20 connections in the same time. Our default configuration will require 50 connections. To adjust this SMBSERVICE_SESSIONS_ON_STORAGE should be set to a value lower than 4

> **Info**
>
> Please note that SMB over QUIC is not supported at this time - only traditional SMB over TCP connections are compatible with this integration. See [[Windows] How to Expose an SMB Share as an NFS Storage Unit](https://www.opswat.com/docs/mdss/integrations/windows-deployment--how-to-add-a-smb-share-as-a-nfs-storage-unit) for more details.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
