<!-- source: https://www.opswat.com/docs/myop/knowledge-base/kb-virtual-appliance-extend-disk-storage -->

# How to increase the disk storage for the My OPSWAT On-premises virtual appliance?

To increase the disk storage for the My OPSWAT On-premises virtual appliance, please follow the below instructions:

1. Increase the disk size allocated to the My OPSWAT On-premises virtual appliance in the hypervisor's interface.

The exact procedure will depend on the hypervisor.

For vSphere 7.0, in the ESXi web client, open the virtual appliance's **Edit Settings** wizard and increase the size of **Hard disk 1**.

For VMWare Workstation Player, open the virtual appliance's **Virtual Machine Settings** wizard and increase the size of **Hard Disk.**

2. Restart the virtual appliance from the hypervisor to ensure that the change takes effect.
3. Log into the virtual appliance's CLI terminal using the **Local User** credentials configured during [the setup wizard](/docs/myop/deployment/deployment).
4. Run the disk extension script.

**sudo /os/prod-scripts/cent-extend-disk.sh**

This script will temporarily stop and then restart the My OPSWAT server to perform the disk extension procedure. If successful, the entire newly added disk storage will be allocated to the virtual appliance's main partition.

**WARNING:** If the My OPSWAT On-premises server has already reached its full disk storage capability, the **/os/prod-scripts/cent-extend-disk.sh** might not function correctly because of insufficient disk space. Please follow the instructions below instead.

1. Increase the disk size allocated to the My OPSWAT On-premises virtual appliance in the hypervisor's interface.
2. Restart the virtual appliance from the hypervisor to ensure that the change takes effect.
3. Log into the virtual appliance's CLI terminal using the **Local User** credentials configured [during the setup wizard](/docs/myop/deployment/deployment).
4. Stop the My OPSWAT On-premises server if it has not stopped.

**sudo /os/prod-scripts/cent-ocm-service.sh stop**

Please be aware that this script may encounter errors due to system failures caused by full disk storage capacity.

5. Run the the below disk extension script.

**sudo /os/prod-scripts/cent-extend-disk-manual.sh**

If successful, the entire newly added disk storage will be allocated to the virtual appliance's main partition.

6. Restart the virtual appliance from the hypervisor.
7. My OPSWAT On-premises server should now start successfully on the new boot.
