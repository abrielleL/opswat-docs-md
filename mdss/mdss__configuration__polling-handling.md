<!-- source: https://www.opswat.com/docs/mdss/configuration/polling-handling -->

# Polling handling

The **Polling file discovery method** retrieves and processes new or modified files directly from the storage.

Key characteristics include:

- Each identified file is processed independently.
- Files are processed only once, preventing redundant scans.
- The storage is checked for updates **every 10 seconds**, or immediately after a complete storage discovery cycle.

Note:

Using the **Polling** method significantly increases the number of requests to the storage system, ensuring timely detection of file changes.

### [Special considerations for Dell Isilon / SMB Compatible Storage](/docs/mdss/configuration/polling-handling#special-considerations-for-dell-isilon--smb-compatible-storage)

#### [Dell Isillon / Smb Compatible](/docs/mdss/configuration/polling-handling#dell-isillon--smb-compatible)

Real-time processing for Dell Isilon and SMB-compatible storage units employs a distinct approach compared to other storage types.

The behavior of this processing mode is governed by environment variables.

Refer to the [the custom configuration page](/docs/mdss/configuration/custom-configuration) for detailed information on these settings.
