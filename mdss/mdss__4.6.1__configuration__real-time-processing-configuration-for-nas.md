<!-- source: https://www.opswat.com/docs/mdss/4.6.1/configuration/real-time-processing-configuration-for-nas -->

# Real Time Processing configuration for NAS

> **Info**
>
> This is applicable only to **NFS**, **SMB**, **SFTP, FTP**, **NetApp ONTAP** and **Dell Isilon** storage units.

> > **DISCOVERY_SERVICE_{PROTOCOL}_RTP_HANDLING** is no longer available starting with version 4.6.0. Please find below instructions on how to enable the same functionality from our Web UI.

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

To ensure all newly copied files are properly detected regardless of their modification timestamps, we have implemented enhanced detection capabilities:

1. Create a Job -> RealTime Scan
2. Select an older date for **Pick files modifies since**

   ![](https://uploads.developerhub.io/prod/k8zL/isps6nxrkel1cm2x9616y44d61xx1zvupgc5jugw41jgcr9ad6fz1lhx9jfdouug.png)

   This means that we will process all the files that have the LastModified newer than the selected.

For example, date is selected to January 24, 2022. When we discover a file that has LastModified on February 1, 2022, we will process it. If we discover a file that has LastModified on January 20,2022, that file will be skipped.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/4.6.1/llms.txt)
