<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/installation/scan-files-folder-cli -->

# Scan files/folder CLI

The MetaDefender Endpoint CLI can be run from the command line to scan files/folders with the options as described in the below table.

The CLI executable is **mdcl-cli.exe** found at the root of your installation directory of MetaDefender Endpoint

Or download standalone executable [here](https://opswat-gears-cloud-clients.s3-us-west-2.amazonaws.com/PublicTool/mdcl.exe)

## [Example](https://docs.opswat.com/macloud-sdp/configuration---management/scan-files-folder-cli#example)

C:\Program Files (x86)\OPSWAT\GEARS Client\mdcl-cli.exe [<option>=<value>]

## [Command Line Options](https://docs.opswat.com/macloud-sdp/configuration---management/scan-files-folder-cli#command-line-options)

A list of available command line options is also available by running the MetaDefender Endpoint executable from the command line without any options

| 1 | Option | Value Types | Example(s) | Comments |
| ---- | ---- | ---- | ---- | ---- |
| 2 | server | <standard url> | -server= http://127.0.0.1:8008/ | Specifies the URL of the MetaDefender server to be used |
| 3 | rule | String | -rule=Client | Specifies the MetaDefender security rule to process files |
| 4 | apikey | String | -apikey=13e5f8h4r3s | Specifies the MetaDefender apikey |
| 5 | workflow | String | -workflow=Client | Specifies the MetaDefender workflow profile to process files |
| 6 | verbose | n/a | -verbose | Enables verbose logging of scans. |
| 7 | user_agent | String | -user_agent=Client | Specifies the value of user_agent that will be provided to MetaDefender |
| 8 | scan_type | A list of one or more of the following strings - physical - system - removable - process - remote | -scan_type= "system&#124; process&#124; physical&#124; removable&#124; remote" -scan_type= "process&#124;physical&#124; removable" -scan_type=process | Indicates which type of scans MetaDefender Endpoint should do - **physical** - all physical drives (excludes removable) - **system** - only system drives - **removable** - all removable media - **process** - only system processes - **remote** - network drives ***Note: Any invalid parameters will be ignored with a warning*** |
| 9 | scan_location | "C:\somedir &#124; C:\somefile" | -scan_location= "c:\somedir with space&#124; c:\somefile" | Specifies the location of the files and/or directories to be scanned ***Note: A trailing \ is needed for directories***____ ***__***_ **__Note: invalid or malformed paths will be ignored**_ |
| 10 | exclude_drive | E:&#124;F: | -exclude_drive=”E:&#124;F:” | Excludes from the scan *Only drive letters supported currently |
| 11 | report_dir | Directory Path | -report_dir= "%AppData%\logs" | Specifies the location where scan logs should be saved. If this option is not specified no log file will be generated. |
| 12 | report_type | One or more of the following strings - pdf - txt - csv | -report_type=”csv&#124;pdf” | Specifies which type of log file to write out at the end of scan. ***Note: Defaults to txt if option is not specified or option is unavailable*** |
| 13 | max_file_size | <val>[GB&#124;G&#124;MB&#124;M&#124;KB&#124;K] | -max_file_size=512KB | Specifies the maximum size of files for which MetaDefender Endpoint will process with MetaDefender ***Note: Any file greater than the max file size will display "Exceeded File Size"*** |
| 14 | gen_config_file | n/a | -gen_config_file | Generate a config.json file in *C:\ProgramData\OPSWAT\MetaDefenderClient\settings* with default options ***Note:*** - *If config file exists and option is not defined, the scan will run with default value set in config.json file.* - *Options in config file will be overridden by command line options* - *mdcl command won’t run in case config file is wrong-formatted, or specified options are not valid with bellow schema**:*`{` `"server"`: String,`` `"rule"`: String,`` `"apikey"`: String,`` `"workflow"`: String,`` `"force_rescan"`: Boolean,`` `"disable_hash_check"`: Boolean,`` `"user_agent"`: String,`` `"scan_type"`: StringArray,`` `"scan_location"`: StringArray,`// Don't support expand environment variables` `"exclude_drive"`: StringArray,`` `"report_dir"`: String,`// Environment variable in dir will be expanded` `"report_type"`: StringArray,`// posible values: ["csv", "txt", "pdf"]` `"max_file_size"`: String,`` `"thread_count"`: Number`` `}` |
| 15 | thread_count | Number | -thread_count=3 | Specify parallelism factor - maximum number of files will be scanned in concurrently |
| 16 | disable_hash_check | boolean | disable_hash_check= true | Specifies to skip performing a hash check on file(s) in the current scan when set to 'true' Note: A value of 'false' indicates default behavior (i.e. hash check will be enabled) |
| 17 | process_priority | One of the following strings - real_time - above_normal - normal - below_normal - low | -process_priority=high | Specifies users to change the priority |
