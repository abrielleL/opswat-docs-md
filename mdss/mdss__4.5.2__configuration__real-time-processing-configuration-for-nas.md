<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/real-time-processing-configuration-for-nas -->

# Real Time Processing configuration for NAS

> **Info**
>
> This is applicable only to **NFS**, **SMB**, **SFTP, FTP**, **NetApp ONTAP** and **Dell Isilon** storage units.

When activating Real-Time Processing (RTP) for your storage resources, please note the following operational characteristics:

### Scope of Detection

Real-Time Processing monitors and detects only files that are newly created or modified subsequent to scan initiation. The system does not retroactively process pre-existing files that were present in your storage prior to enabling RTP.

### Comprehensive File Assessment

To ensure complete analysis of your storage repository, including all pre-existing files, we recommend implementing either:

- Scheduled scans - Configured at predetermined intervals
- On-demand scans - Initiated manually as needed

These comprehensive scan types will process the entirety of your storage contents, including files that predate your RTP implementation. This differentiated approach allows for both continuous monitoring of new content and periodic comprehensive assessment of your complete data repository.

### Timestamp Behavior and Detection Implications

When using certain file transfer tools such as WinSCP and similar GUI-based applications, the original file's **LastModifiedDate** is typically preserved during the copy operation. This behavior means:

- Files copied via WinSCP to SMB/NFS/SFTP/FTP shares will retain their original modification dates
- A file last modified in January 2023 and copied in June 2024 will still display January 2023 as its modification date

As a result, Real-Time Processing (RTP) may not detect these files if their modification timestamps predate the RTP scan initialization. For example, if a file with a modification date of "January 2023" is copied to your storage in "June 2024" after RTP has been activated, standard detection mechanisms will not identify this file as newly added content.

### Advanced Configuration for Comprehensive Detection

To ensure all newly copied files are properly detected regardless of their modification timestamps, we have implemented enhanced detection capabilities through the following configuration parameters:

**DISCOVERY_SERVICE_SMB_RTP_HANDLING=1**

**DISCOVERY_SERVICE_SFTP_RTP_HANDLING=1**

**DISCOVERY_SERVICE_NFS_RTP_HANDLING=1**

**DISCOVERY_SERVICE_FTP_RTP_HANDLING=1**

### Implementation Procedure

To activate enhanced file detection, add the appropriate parameter (following [this guide](https://www.opswat.com/docs/mdss/configuration/custom-configuration)) in your **customer.env** file and then restart our product for changes to apply.

Once implemented, these configuration options ensure that all files added to your storage will be detected during Real-Time Processing, irrespective of their modification timestamps.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
