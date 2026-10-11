<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/troubleshooting/rectify-malformed-data-created-by-filetype-engine-in-postgresql -->

# Rectify malformed FileType data in PostgreSQL database

View as Markdown Ask ChatGPT about this page Ask Claude about this page

FileType engine v6.0.2 sometimes creates malformed data after analyzing files. When being written into PostgreSQL database, those malformed data cause MetaDefender Core warehouse stuck and result in negative impacts:

- Executive Report in Dashboard gets frozen and changed back to zero.
- CPU usage will go too high.
- A dramatical decrease in file processing performance.

Even though a recently released version of FileType engine v6.1.1 fixes the malformed data issue, there might be a few remaining data stored in PostgreSQL database.

This tool will handle those data by rectifing and converting all the malformed data of `filetype_details` in PostgreSQL database to a true format.

**Note:** If you do fresh installation of MetaDefender Core v5.4.1, you can skip the following content since we already enhance and harden the service to prevent malformed data issue.

## [Parameters](/docs/mdcore/v5.22.1/troubleshooting/rectify-malformed-data-created-by-filetype-engine-in-postgresql#parameters)

| Parameter | Mandatory |  |
| --- | --- | --- |
| `--help`/`-h` | No | display all the options and flags associated with the guides. |

## [Usage](/docs/mdcore/v5.22.1/troubleshooting/rectify-malformed-data-created-by-filetype-engine-in-postgresql#usage)

Besides an enhancement, the upcoming version 5.4.1 of MetaDefender Core will also bundle the tool `ometascan-data-normalizer` into its installation folder. For older versions, we provide following separate tools:

| MetaDefender Core version | CentOS | Debian | Windows |
| --- | --- | --- | --- |
| 5.2.0 or newer | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/5.2.0-5.4.0/centos/ometascan-data-normalizer) | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/5.2.0-5.4.0/debian/ometascan-data-normalizer) | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/5.2.0-5.4.0/windows/ometascan-data-normalizer.exe) |
| 5.0.0 - 5.1.2 | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/5.0.0-5.1.2/centos/ometascan-data-normalizer) | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/5.0.0-5.1.2/debian/ometascan-data-normalizer) | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/5.0.0-5.1.2/windows/ometascan-data-normalizer.exe) |
| 4.21.x | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/4.21.x/centos/ometascan-data-normalizer) | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/4.21.x/debian/ometascan-data-normalizer) | [download link](https://metascanbucket.s3.us-west-1.amazonaws.com/Metadefender/Core/troubleshooting/4.21.x/windows/ometascan-data-normalizer.exe) |

**Step-by-step**

1. Copy a relevant `ometascan-data-normalizer.exe`(Windows) or `ometascan-data-normalizer` (Linux) into the installation folder of MetaDefender Core
2. 1. Default Windows path: `C:\Program Files\OPSWAT\MetaDefender Core\`
   2. Default Linux path: `/usr/sbin/`
3. Stop posting files to MetaDefender Core.
4. Run the `cmd` or `Terminal` as Administrator or root.
5. Execute the command:

   1. Windows: `ometascan-data-normalizer.exe`
   2. Linux: `./ometascan-data-normalizer`
6. Start MetaDefender Core service. A few components might take time to start and refresh, so let's wait for a couple minutes.

**Notes:**

- After running the `ometascan-data-normalizer`, it might take considerable extra time to update data if database size is large.
- Ensure that MetaDefender Core server is running after the tool finishes. If it is stopped, please start it and wait for a while
- If you encounter error or warning during the execution, please wait for a couple of minutes before executing it again.

## [Log file](/docs/mdcore/v5.22.1/troubleshooting/rectify-malformed-data-created-by-filetype-engine-in-postgresql#log-file)

Filename format: `data_normalizer-yyyyMMdd.log`

- On Windows, log file will be placed at `C:\Program Files\OPSWAT\MetaDefender Core\data\logs\`
- On Linux, log file will be placed at `/var/log/ometascan/`

| Log level | Message | Troubleshooting |
| --- | --- | --- |
| INFO | [INFO ]: Data normalization is done, data: filetype, instance id: 1 | The process is completed successfully. |
| WARNING | [WARNING]: Data normalization is failed, data: filetype, instance id: 1,... | The data cannot be updated. Collect all the log files and send the support package to us for troubleshooting. |
| ERROR | [ERROR ]: Select all last_request___id unsuccessfully.... | The data cannot be updated. Collect all the log files and send the support package to us for troubleshooting. |
| ERROR | [ERROR ]: Cannot connect to Postgres server: metadefender_core...  [ERROR ]: Failed to init Postgres service | 1. Check the privilege when executing the tool and make sure that it has the true privilege to read the `.dat` file in the installation path. 2. Collect all the log files and send the support package to us for troubleshooting. |
| ERROR *on console* | ERROR: Cannot open file log: <logpath>/data normalizer-20230128.log | 1. Check the log path and make sure that its existence is valid. 2. Check the privilege when executing the tool and make sure that it has the true privilege to create and edit the log file in the log path. |
