<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-nfs-with-data-wrapping-storage -->

# Add an NFS with Data Wrapping Storage

NFS with Data Wrapping works like a [standard NFS storage](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage), except that the files on the share are kept in a wrapped form. Each file is unwrapped as it gets read, so scans always run on the original content, and wrapped as the file gets written to the share.

### Step 1:

To scan a storage that contains wrapped files, you have to integrate it as an NFS storage unit. Please see [this page](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage).

### Step 2:

In order to integrate NFS with Data Wrapping with MetaDefender Storage Security, please follow these steps:

1. As NFS with Data Wrapping is not using any credentials, you can have only one NFS with Data Wrapping account in MDSS. If you already have one, please go to step 4
2. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **NFS with Data Wrapping** and click **Next**.
3. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

![](https://uploads.developerhub.io/prod/k8zL/g6dgyoqfjltaer0fs3otqo4brtcuhlc3ds3ilc8za17iey0tojokqxgupi57krxg.png)

4. From the left side menu, navigate to **Inventory**, click **Add New** > **Unit**, choose the previously created account and click **Next**.

![](https://uploads.developerhub.io/prod/k8zL/hvb3u8lduluzlwty0zhamiq5kw3gvr36293i0z0ouvzbgwu37ag1jibviru01gdm.png)

5. Give your unit an unique name so you can easily identify it later
6. Assign your unit to a Group
7. Input the mount directory to the folder created at Step 1.
8. Click **Next** in order to finish the process.

> **Info**
>
> Remediation behavior is as follows:
>
> - Files moved between NFS with Data Wrapping storage units remain unchanged
> - Files moved from NFS with Data Wrapping to another storage type (such as Amazon S3) are unwrapped during the move
> - Files moved from another storage type (such as Amazon  S3) to NFS with Data Wrapping are wrapped during the move

> **Warning**
>
> The wrap/unwrap action is not configurable.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
