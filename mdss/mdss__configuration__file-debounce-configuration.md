<!-- source: https://www.opswat.com/docs/mdss/configuration/file-debounce-configuration -->

# File Discovery Debounce

The MDSS file discovery system uses a debounce mechanism to determine when files are stable and ready for processing. Several key environment variables control this behavior, working together to create a consistent file discovery experience while accommodating the unique characteristics of different storage types.

## [Environment Variables](/docs/mdss/configuration/file-debounce-configuration#environment-variables)

### [Global Debounce Interval](/docs/mdss/configuration/file-debounce-configuration#global-debounce-interval)

`FILE_DISCOVERY_DEBOUNCE_INTERVAL=0`

This variable defines the minimum time that must elapse before a previously processed file is considered "new" again after being edited.

- **Default value**: 0 seconds (files are considered new after any edit)
- **Purpose**: Prevents duplicate processing of the same file when multiple rapid edits occur
- **Global setting**: Applies to all storage types as a baseline

### [Storage-Specific Debounce Times](/docs/mdss/configuration/file-debounce-configuration#storage-specific-debounce-times)

`SFTP_DISCOVERY_DEBOUNCE_TIME_SECONDS=5`

`NFS_DISCOVERY_DEBOUNCE_TIME_SECONDS=5`

`SMB_DISCOVERY_DEBOUNCE_TIME_SECONDS=120`

These variables define how long the system waits to confirm a file is fully uploaded and stable before processing it. The system checks if the file has been modified within this time period. If no modifications are detected during this interval, the file is considered ready for processing.

- **Default value**: 5 seconds
- **Purpose**: Prevents processing of partially uploaded files

## [Interaction Between Settings](/docs/mdss/configuration/file-debounce-configuration#interaction-between-settings)

The interaction between these settings follows this rule:

Storage-specific debounce values must be lower than or equal to the global `FILE_DISCOVERY_DEBOUNCE_INTERVAL`. If a storage-specific value is set to be bigger than the global interval, the system will automatically use the global `FILE_DISCOVERY_DEBOUNCE_INTERVAL` value instead. This ensures consistent minimum debounce times across all storage types. However, if the global `FILE_DISCOVERY_DEBOUNCE_INTERVAL` is set to 0, the system will honor the storage-specific values, allowing for customized debounce intervals per storage type.

The SMB service operates in two modes, controlled by the environment variable `SMBSERVICE_FILE_READY_CHECK_MODE`:

- `FILE_OPEN_CHECK` (value: `1`) – the default mode set by MDSS.
- `DEBOUNCE_CHECK` (value: `0`).

To enable file debounce for SMB, set `SMBSERVICE_FILE_READY_CHECK_MODE` to `0`.
