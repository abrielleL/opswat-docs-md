<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation -->

# Temporary local files created during remediation

## [Overview](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#overview)

MDSS creates temporary files during specific remediation operations to ensure reliable data processing. These temporary files are generated during:

- File transfers between storage units
- File sanitization operations using our DeepCDR technology

To assist with troubleshooting and compliance auditing, MDSS provides configurable logging of these temporary file operations.

## [Temporary File Locations](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#temporary-file-locations)

#### [Linux deployments](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#linux-deployments)

Temporary files are created inside the docker container of the destination storage type, in the standard Linux temporary directory **/tmp/**.

| Operation | Container location |
| --- | --- |
| Moving from any storage to NFS | **mdss_nfs_remediationsservice** |
| Moving from any storage to SMB | **mdss_smb_remediationsservice** |
| Sanitization with DeepCDR | Container of the source storage(**mdss_nfs_remediationsservice** for NFS files) |

#### [Windows deployments](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#windows-deployments)

All temporary files will be created in the standard Windows temporary directory **C:\Windows\Temp**

## [Configuration](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#configuration)

The temporary file logging feature can be enabled or disabled by setting the **LOG_CREATION_OF_TEMP_FILES** variable in your **customer.env** file:

- 0: logging disabled (default value)
- 1: logging enabled

To update your **customer.env** file, please follow [this guide.](/docs/mdss/4.4.2/configuration/custom-configuration)

Example:

customer.envCopyLOG_CREATION_OF_TEMP_FILES=1Log exampleCopy[2025-03-13 14:44:40Z] [Information] remediations.nfs.service: Local temporary file created. Path: /tmp/4mn110iw.gzn. Size: 1048624. Reason: Upload non-seekable stream. AutoDelete: True. Destination: credit-card-file-v2_sanitized_by_OPSWAT_MetaDefender_9619874ae98542129d386871a8cb0268.txt
## [Log file locations](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#log-file-locations)

Linux deployments: **/etc/mdss/services_logs/**

Windows deployments**:** **{InstallDir}\services**

## [Frequently Asked Questions](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#frequently-asked-questions)

### [Are my files safe during this process?](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#are-my-files-safe-during-this-process)

Yes. Temporary files exist only within isolated Docker containers (Linux deployment) or in locations accessible only by administrators (Windows). Access to these files is restricted to MDSS processes.

### [Does this affect performance?](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#does-this-affect-performance)

The impact is minimal. Our system is optimized to handle temporary files efficiently and clean them up promptly.

### [Can I disable temporary file creation?](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#can-i-disable-temporary-file-creation)

No. Temporary files are essential for reliable data transfer between microservices in the MDSS architecture.

### [What happens if a container crashes?](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#what-happens-if-a-container-crashes)

Temporary files exist only within the container's filesystem. If a container crashes or restarts, the temporary files are automatically deleted as part of Docker's container lifecycle.

### [Are the temporary files using additional storage beyond what is already allocated?](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#are-the-temporary-files-using-additional-storage-beyond-what-is-already-allocated)

No. The temporary files are created within the allocated storage for your Docker containers. They do not consume additional storage beyond what is already allocated to your deployment.

## [Best Practices](/docs/mdss/4.4.2/configuration/temporary-local-files-created-during-remediation#best-practices)

For optimal performance and security:

1. Ensure your Docker containers have adequate storage allocation. Please follow [our guide](/docs/mdss/4.4.2/getting-started/general-system-requirements) to properly allocate disk space
2. Monitor container resource usage during large data transfers
