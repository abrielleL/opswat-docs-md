<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/metadefender-core-and-out-of-support-windows-os -->

# MetaDefender Core and Out-of-Support Windows OS

Beginning with version **5.17.0**, MetaDefender Core **no longer supports Windows Server 2016, Windows 10 LTSB 2016, and Windows 10 version 1607.** As a result, attempting to install MetaDefender Core on these OS will trigger an error message:

After users click OK button, the installer will automatically roll back to the previously installed version, and the system should continue to function normally after the rollback.

However, please note that **Windows Server 2016, Windows 10 LTSB 2016, and Windows 10 version 1607** **are no longer supported**, and MetaDefender Core 5.17.0 or later must not be installed or upgraded on these operating systems. Please prepare a migration to newer OS such as Windows Server 2019, 2022, 2025.

Please check here for more details: [How will End of Life Support for Windows Server 2016 and Windows 10 versions before 21H2 in MetaDefender Core affect my deployments?](/docs/mdcore/v5.21.0/knowledge-base/how-will-end-of-life-support-for-windows-server-2016-and-windows)
