<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/file-debounce-configuration -->

# File Discovery Debounce

The MDSS file discovery system uses a debounce mechanism to determine when files are stable and ready for processing. Several key environment variables control this behavior, working together to create a consistent file discovery experience while accommodating the unique characteristics of different storage types.

## Environment Variables

### Global Debounce Interval

`FILE_DISCOVERY_DEBOUNCE_INTERVAL=0`

This variable applies to real-time processing only. It defines the minimum time that must elapse before a previously processed file is considered "new" again after being edited. The maximum is 3600 seconds.

- **Default value**: 0 seconds (files are considered new after any edit)
- **Purpose**: Prevents duplicate processing of the same file when multiple rapid edits occur
- **Global setting**: Applies to all storage types in real-time processing, and caps the storage-specific values below

### Storage-Specific Debounce Times

`SFTP_DISCOVERY_DEBOUNCE_TIME_SECONDS=5`

`NFS_DISCOVERY_DEBOUNCE_TIME_SECONDS=5`

`SMBSERVICE_DISCOVERY_DEBOUNCE_TIME=5`

These variables define how long the system waits to confirm a file is fully uploaded and stable before processing it. The system checks if the file has been modified within this time period. If no modifications are detected during this interval, the file is considered ready for processing.

- **Default value**: 5 seconds
- **Purpose**: Prevents processing of partially uploaded files

## Interaction Between Settings

The interaction between these settings follows this rule:

Storage-specific debounce values must be lower than or equal to the global `FILE_DISCOVERY_DEBOUNCE_INTERVAL`. If a storage-specific value is set to be bigger than the global interval, the system will automatically use the global `FILE_DISCOVERY_DEBOUNCE_INTERVAL` value instead. This keeps every storage-specific value at or below the global interval. However, if the global `FILE_DISCOVERY_DEBOUNCE_INTERVAL` is set to 0, the system will honor the storage-specific values, allowing for customized debounce intervals per storage type.

For SMB units, the default SMB service skips a file that was modified less than `SMBSERVICE_DISCOVERY_DEBOUNCE_TIME` seconds ago and picks it up at the next discovery. On Windows deployments it also skips a file that another client still holds open for writing. On Linux deployments MDSS cannot reliably detect such a file, so the time window is the main protection against scanning a partially copied file: increase it when files are copied to the share by slow clients, or set it to `0` to process files as soon as they are found.

The legacy SMB service (the `smb_legacy` module on Linux, or `USE_OPSWAT_SMB_SERVICE=false` on Windows) works differently: by default it skips a file that another client still holds open, and uses `SMBSERVICE_DISCOVERY_DEBOUNCE_TIME` only when `SMBSERVICE_FILE_READY_CHECK_MODE=0` is set.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
