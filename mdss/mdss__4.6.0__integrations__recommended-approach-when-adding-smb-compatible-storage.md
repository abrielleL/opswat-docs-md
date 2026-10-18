<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/recommended-approach-when-adding-smb-compatible-storage -->

# Recommended approach when adding SMB units on Linux deployments

> This article is applicable only for MetaDefender Storage Security deployed on Linux. If your deployment is on Windows, please follow [Add an SMB-Compatible unit in Windows deployments](https://www.opswat.com/docs/mdss/integrations/add-an-smb-compatible-unit-in-windows-deployments).

Starting with version 4.6.0, the recommended way to add an SMB share on a Linux deployment is the **SMB Compatible** storage type. The SMB service mounts each share on demand with the SMB/CIFS client built into the Linux kernel, so the deployment gets the stability and performance of an operating-system mount without any manual mount, `fstab` entry or `cifs-utils` package on the MDSS machine. Follow [Add an SMB-Compatible unit in Linux deployments](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage).

Releases before 4.6.0 relied on an application-level SMB client, and for production environments the recommendation was to mount the share on the MDSS machine and add it as an NFS storage unit instead. Units configured that way keep working after the upgrade. To move them to the SMB service, add the share as an SMB Compatible storage and remove the NFS unit and the host mount.

Hosts that cannot run the new SMB service (no `cifs` kernel module, a rootless container runtime, or a policy that refuses its container privileges) can use the previous SMB service through the `smb_legacy` module. See *Fallback: the legacy SMB service* in [Add an SMB-Compatible unit in Linux deployments](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
