<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-nfs-with-sisl-storage -->

# Add an NFS with SISL Storage

Simple Information Serialization Language (SISL) is a simple structured text format designed for use in the [NCSC Safely Importing Data Pattern](https://www.ncsc.gov.uk/guidance/pattern-safely-importing-data). MDSS provides the functionality to wrap and unwrap files with an XOR scrambling technique using the following algorithm [pySISL](https://pypi.org/project/pysisl/).

### [Step 1:](/docs/mdss/integrations/add-an-nfs-with-sisl-storage#step-1)

To scan a storage that contains wrapped files, you have to integrate it as an NFS storage unit. Please see [this page](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage).

### [Step 2:](/docs/mdss/integrations/add-an-nfs-with-sisl-storage#step-2)

In order to integrate NFS with SSL with MetaDefender Storage Security, please follow these steps:

1. As NFS with SISL is not using any credentials, you can have only one NFS with SISL account in MDSS. If you already have one, please go to step 4
2. From the left side menu, navigate to **Inventory,** click on **Add account** and choose **NFS with SISL**.
3. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

4. From the left side menu, navigate to **Inventory,** click on **Add unit** and choose the previously created account.

5. Give your unit an unique name so you can easily identify it later
6. Assign your unit to a Group
7. Input the mount directory to the folder created at Step 1.
8. Click **Next** in order to finish the process.

Info

Remediation behavior is as follows:

- Files moved between NFS with SISL storage units remain unchanged
- Files moved from NFS with SISL to another storage type (such as Amazon S3) are unwrapped during the move
- Files moved from another storage type (such as Amazon S3) to NFS with SISL are wrapped during the move
Warning

The wrap/unwrap action is not configurable.
