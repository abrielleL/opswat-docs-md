<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-clamav-show--permanently-failed--after-enabling-the-dae -->

# Why does ClamAV show "permanently failed" after enabling the daemon log file?

After enabling the ClamAV daemon log file, you may encounter the error message: `Permanently failed`

This error occurs because no valid path for the log file has been specified.

Cause:

This is intended behavior. The ClamAV engine requires a valid path for the daemon log file to function correctly. Without it, the daemon cannot initialize properly.

## [Steps to Resolve](/docs/mdcore/knowledge-base/why-does-clamav-show--permanently-failed--after-enabling-the-dae#steps-to-resolve)

1. **Specify the Destination Path and Log File Name** Select a destination path and specify a file name for the ClamAV daemon log file. **Example:** `C:\Users\user.name\Desktop\AV\clamav.log`
2. **Update Configuration** Navigate to **MetaDefender Core > ClamAV > Configuration** and update the Path of the ClamAV daemon log file with the chosen path and file name.

3. **Re-enable the ClamAV Engine** After saving the changes, disable the ClamAV engine and then re-enable it. This forces the daemon to reinitialize with the updated configuration.

| Log File | Description |
| --- | --- |
| oms_clamav.log | Located at `C:\Program Files\OPSWAT\MetaDefender Core\data\logs\oms_clamav`. This log file is specific to the MetaDefender Core integration and provides logs for integration-related activities. |
| Daemon Log File | The ClamAV daemon’s own log file, offering detailed information for debugging ClamAV-specific issues. |

The daemon log file is particularly useful for troubleshooting issues specific to the ClamAV engine, while the `oms_clamav.log` focuses on MetaDefender Core’s operations.

Support:

If you have any further questions please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
