<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/temporary-local-files-created-during-remediation -->

# Temporary local files created during remediation

## Overview

MDSS creates temporary files during specific remediation operations to ensure reliable data processing. These temporary files are generated during:

- File transfers between storage units
- File sanitization operations using our DeepCDR technology

To assist with troubleshooting and compliance auditing, MDSS provides configurable logging of these temporary file operations.

## Temporary File Locations

#### Linux deployments

Each storage integration runs as a single Docker container named mdintegrations_<storage type> (for example mdintegrations_nfs), which hosts the Discovery, Storage, and Remediation services for that storage type. Temporary files are created inside the container of the destination storage type, in the standard Linux temporary directory** /tmp/**.

| Operation | Container location |
| ---- | ---- |
| Moving from any storage to NFS | **mdintegrations_nfs** |
| Moving from any storage to SMB | **mdintegrations_smb** |
| Sanitization with DeepCDR | Container of the source storage(**mdintegrations_nfs **for NFS files) |

#### Windows deployments

All temporary files will be created in the standard Windows temporary directory **C:\Windows\Temp**

## Configuration

The temporary file logging feature can be enabled or disabled by setting the **LOG_CREATION_OF_TEMP_FILES** variable in your **customer.env** file:

- 0: logging disabled (default value)
- 1: logging enabled

To update your **customer.env** file, please follow [this guide.](https://www.opswat.com/docs/mdss/configuration/custom-configuration)

Example:

```powershell
LOG_CREATION_OF_TEMP_FILES=1
```

```powershell
[2025-03-13 14:44:40Z] [Information] remediations.nfs.service: Local temporary file created. Path: C:\Windows\Temp\4mn110iw.gzn. Size: 1048624. Reason: Upload non-seekable stream. AutoDelete: True. Destination: credit-card-file-v2_sanitized_by_OPSWAT_MetaDefender_9619874ae98542129d386871a8cb0268.txt
```

## Log file locations

Linux deployments: **/etc/mdss/services_logs/**

Windows deployments**:** **{InstallDir}\services**

## Frequently Asked Questions

### Are my files safe during this process?

Yes. Temporary files exist only within isolated Docker containers (Linux deployment) or in locations accessible only by administrators (Windows). Access to these files is restricted to MDSS processes.

### Does this affect performance?

The impact is minimal. Our system is optimized to handle temporary files efficiently and clean them up promptly.

### Can I disable temporary file creation?

No. Temporary files are essential for reliable data transfer between microservices in the MDSS architecture.

### What happens if a container crashes?

Temporary files exist only within the container's filesystem. If a container crashes or restarts, the temporary files are automatically deleted as part of Docker's container lifecycle.

### Are the temporary files using additional storage beyond what is already allocated?

No. The temporary files are created within the allocated storage for your Docker containers. They do not consume additional storage beyond what is already allocated to your deployment.

## Best Practices

For optimal performance and security:

1. Ensure your Docker containers have adequate storage allocation. Please follow [our guide](https://www.opswat.com/docs/mdss/getting-started/general-system-requirements) to properly allocate disk space
2. Monitor container resource usage during large data transfers

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
