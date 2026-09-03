<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-an-nfs-with-sisl-storage -->

# Add an NFS with SISL Storage

Simple Information Serialization Language (SISL) is a simple structured text format designed for use in the [NCSC Safely Importing Data Pattern](https://www.ncsc.gov.uk/guidance/pattern-safely-importing-data). MDSS provides the functionality to wrap and unwrap files with an XOR scrambling technique using the following algorithm [pySISL](https://pypi.org/project/pysisl/).

### [Step 1:](/docs/mdss/4.4.2/integrations/add-an-nfs-with-sisl-storage#step-1)

To scan a storage that contains wrapped files, you have to integrate it as an NFS storage unit. Please see [this page](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage).

### [Step 2:](/docs/mdss/4.4.2/integrations/add-an-nfs-with-sisl-storage#step-2)

From MetaDefender Storage Security user interface, add an NFS with SISL storage unit, setting the **Mount directory to** the folder created at Step 1.

Info

Remediation behavior is as follows:

- Files moved between NFS with SISL storage units remain unchanged
- Files moved from NFS with SISL to another storage type (such as Amazon S3) are unwrapped during the move
- Files moved from another storage type (such as Amazon S3) to NFS with SISL are wrapped during the move
Warning

The wrap/unwrap action is not configurable.
