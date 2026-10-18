<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit -->

# How to add an Amazon EFS as an NFS storage unit

## Prerequisites:

1. an Amazon EFS file storage.
2. a Linux machine where MDSS is installed. This machine needs to be inside AWS and to have access to file storage from 1

### Step 1:

On MDSS machine, please install the **cifs-utils** package

### Step 2:

On machine where MetaDefender Storage Security is installed, create a new folder at the following path **/mnt/mdss/nfs/{my-new-folder}**

### Step 3:

On machine where MetaDefender Storage Security is installed,  mount the Amazon EFS file storage in the folder created at step 1. In our testing, we have used the following command, provided by Amazon:

```bash
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-42f1fa845a1b23ece.efs.eu-central-1.amazonaws.com:/ /mnt/mdss/nfs/{my-new-folder}
```

Please note the mount command has multiple parameters that can be configured in many ways. Feel free to adapt it to your needs. Any configuration works with our product, as long as the Amazon EFS file storage is mounted successfully and we have, at least, read access to it (to benefit from our remediation capabilities, we will need write access).

### Step 4:

To ensure the mount is persistent, please add it in **/etc/fstab .** Otherwise, the mount will be lost when machine restarts.

### Step 5:

In order to integrate Amazon EFS with MetaDefender Storage Security, please follow these steps:

1. As NFS is not using any credentials, you can have only one NFS account in MDSS. If you already have one, please go to step 4
2. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **NFS (Network File System)** and click **Next**.
3. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

![](https://uploads.developerhub.io/prod/k8zL/g6dgyoqfjltaer0fs3otqo4brtcuhlc3ds3ilc8za17iey0tojokqxgupi57krxg.png)

4. From the left side menu, navigate to **Inventory**, click **Add New** > **Unit**, choose the previously created account and click **Next**.

![](https://uploads.developerhub.io/prod/k8zL/hvb3u8lduluzlwty0zhamiq5kw3gvr36293i0z0ouvzbgwu37ag1jibviru01gdm.png)

5. Give your unit an unique name so you can easily identify it later
6. Assign your unit to a Group
7. Input the mount directory where your Amazon EFS shared files are mounted on the MetaDefender Storage Security machine. For instance, if your files are mounted at `/mnt/mdss/nfs/efs`, simply enter `efs` in the text box.
8. Click **Next** in order to finish the process.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
