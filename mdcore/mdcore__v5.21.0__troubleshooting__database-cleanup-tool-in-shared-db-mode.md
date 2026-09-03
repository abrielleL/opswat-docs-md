<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/database-cleanup-tool-in-shared-db-mode -->

# Database Cleanup Tool in Shared DB Mode

This tool is prepared for the customers when they want to clean all the scan data from the dead instance of Core in the shared database model.

This tool can be found:

- Windows: C:\Program Files\OPSWAT\MetaDefender Core\ometascan-db-cleaner.exe
- Linux: /usr/sbin/ometascan-db-cleaner
Warning

This tool can be used for MetaDefender Core 5.2.1 or above.

## [How to run](/docs/mdcore/v5.21.0/troubleshooting/database-cleanup-tool-in-shared-db-mode#how-to-run)

Find the ometascan-db-cleaner.exe(window) or ometascan-db-cleaner(Linux) to the installation folder:

- Default Window path: C:\Program Files\OPSWAT\MetaDefender Core\
- Default Linux path: /usr/sbin/

Warning

With Linux, change permission for ometascan-db-cleaner with command:

**sudo chmod 755 ometascan-db-cleaner**

Run the cmd or Terminal as Administrator or root.

Info

If there is a mistake in the cleaning database process (clean data of a running instance), the user should restart MetaDefender Core service to re-create all its tables of scanned data again.

Otherwise the error will happen, and the error message will be saved on the core.log

## [Parameters](/docs/mdcore/v5.21.0/troubleshooting/database-cleanup-tool-in-shared-db-mode#parameters)

| Parameter | Description | Example |
| --- | --- | --- |
| `-- help` or `-h` | Display all the options and flags associated with the guides | `ometascan-db-cleaner --help`  `ometascan-db-cleaner -h` |
| `--delete / -d <INSTANCE NAME>`  or  `--delete / -d --keep-instance-name/-k <INSTANCE NAME>`  or  `-dk <INSTANCE NAME>` | Clean the database (required to indicate the instance’s name concretely).  Indicate the instance’s name for cleaning the database or display the list of tables with suffix _<instance_id>  ***Notes:*** if using the option --keep-instance-name/-k or -dk, this option means only cleaning data but **keeping** the instance name. Otherwise, the tool will delete the instance name with data. | `ometascan-db-cleaner --delete "fn2xjs"`  `ometascan-db-cleaner -d "fn2xjs"`  `ometascan-db-cleaner --delete --keep-instance-name "fn2xjs"`  `ometascan-db-cleaner -d -k "fn2xjs"`  `ometascan-db-cleaner -dk "fn2xjs"` |
| `--list`  or `-l` | List all instance’s names in database | `ometascan-db-cleaner -l`  `ometascan-db-cleaner --list` |

## [Troubleshooting](/docs/mdcore/v5.21.0/troubleshooting/database-cleanup-tool-in-shared-db-mode#troubleshooting)

If there is any problem with the tool while using, please collect all the log files in this folder and send us for investigating.

File log: `db_cleaner-yyyyMMdd.log`

- Windows: `C:\Program Files\OPSWAT\MetaDefender Core\data\logs\`
- Linux: `/var/log/ometascan/`
