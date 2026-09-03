<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit -->

# How to add an Amazon EFS as an NFS storage unit

## [Prerequisites:](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit#prerequisites)

1. an Amazon EFS file storage.
2. a Linux machine where MDSS is installed. This machine needs to be inside AWS and to have access to file storage from 1

### [Step 1:](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit#step-1)

On MDSS machine, please install the **cifs-utils** package

### [Step 2:](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit#step-2)

On machine where MetaDefender Storage Security is installed, create a new folder at the following path **/mnt/mdss/nfs/{my-new-folder}**

### [Step 3:](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit#step-3)

On machine where MetaDefender Storage Security is installed, mount the Amazon EFS file storage in the folder created at step 1. In our testing, we have used the following command, provided by Amazon:

BashCopysudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-42f1fa845a1b23ece.efs.eu-central-1.amazonaws.com:/ /mnt/mdss/nfs/{my-new-folder}

Please note the mount command has multiple parameters that can be configured in many ways. Feel free to adapt it to your needs. Any configuration works with our product, as long as the Amazon EFS file storage is mounted successfully and we have, at least, read access to it (to benefit from our remediation capabilities, we will need write access).

### [Step 4:](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit#step-4)

To ensure the mount is persistent, please add it in **/etc/fstab .** Otherwise, the mount will be lost when machine restarts.

### [Step 5:](/docs/mdss/4.4.2/integrations/how-to-add-amazon-efs-as-a-nfs-storage-unit#step-5)

From MetaDefender Storage Security user interface, add a NFS storage unit having the **Mount directory** the folder created at step 1.
