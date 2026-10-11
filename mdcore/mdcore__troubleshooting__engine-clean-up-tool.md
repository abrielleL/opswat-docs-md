<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/engine-clean-up-tool -->

# Engine Clean-up Tool

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

This article is only applicable to MetaDefender Core 4.19.0 and 4.19.1.

For MetaDefender Core 4.19.2 or newer, all engines could be removed directly on the MetaDefender Core management console UI under Modules page.

For MetaDefender Core 4.18.0 or older, please follow instructions here [What are the engine clean-up instructions?](/knowledge-base/what-are-the-engine-clean-up-instructions).

Sometimes, during the engines downloading/deployment process, some of them may remain in **"failed"** or **"permanently failed"** status. In that case, you could perform an engine clean-up by using MetaDefender Core built-in engine sweeper tool:

- Locate the tool in MetaDefender Core installation folder named ometascan-engine-sweeper

Usage: `ometascan-engine-sweeper [options]`

BashCopyMetaDefender Core v4 Engine Sweeper
Options:
?, -h, --help Displays this help.
e, --engine <engine> Engine name to clean. ('*' for matching any string, '?' for matching any character)
l, --list List installed engines.
d, --retain-database Retain engine\'s database.
H, --host <host> Host of PostgreSQL server.
P, --port <port> Port of PostgreSQL server.
U, --username <username> Username for PostgreSQL server.
D, --database <database> Database name to connect.
B, --builtin-postgres Only use if that is a built-in PostgreSQL server (installed on the same machine with MetaDefender Core)
## MetaDefender Core 4.19.x database information to connect

- **Host and port:** Specified while installing Core 4.19.0. In default installation option, MetaDefender Core setups local and connect to PostgreSQL server at localhost via port 5432
- **Username:** Specified while installing Core 4.19.0. In default installation option, MetaDefender Core uses username postgres
- **Database name:** MetaDefender Core metadefender_core_xxxxxx - whereas xxxxxx is the 6 characters in lower case following product code name (Windows: MSCW, Linux: MSCL) in your current Deployment ID.

Info

**Making sure to lower case on all 6 characters**

For example: database name should be metadefender_core_lrmgvs in the sample screenshot below

## Example usages

Assuming we will connect to a local PostgreSQL server with following info:

- localhost via port 5432
- username = postgres
- database name = metadefender_core_lrmgvs

## Example 1: List all installed engines

BashCopyometascan-engine-sweeper.exe -B -H localhost -P 5432 -U postgres -D metadefender_core_lrmgvs -l

note

Making sure to use “-B” parameter option if that is a local PostgreSQL server

Then the tool requires you to input PostgreSQL server password for MetaDefender Core (specified while installing MetaDefender Core)

Example output:

BashCopyMetaDefender Core v4 Engine Sweeper.
 
 
Data directory detected: "C:/Program Files/OPSWAT/Metadefender Core/data/"
 
Enter PostgreSQL password:
Querying installed engines in database...
Installed engines:
"oesis_3_windows" | "Vulnerability Scanning"
"mdcloud_5_windows" | "Threat Intelligence"
"7z_13_windows" | "Archive engine"
"ds_3_windows" | "Deep CDR"
"yara_5_windows" | "Yara"
"dlp_8_windows" | "Proactive DLP"
"clamav_1_windows" | "ClamAV"
"filetype_1_windows" | "FileType"
## Example 2: Remove engine package and database package of Archive engine (e.g. 7z_13_windows)

BashCopyometascan-engine-sweeper.exe -B -H localhost -P 5432 -U postgres -D metadefender_core_lrmgvs -e 7z_13_windows

Note: Making sure to use “-B” parameter option if that is a local PostgreSQL server

Example output:

BashCopyMetaDefender Core v4 Engine Sweeper.
 
 
Data directory detected: "C:/Program Files/OPSWAT/Metadefender Core/data/"
 
Enter PostgreSQL password:
Engine(s) to clean: ("7z_13_windows")
 
 
The OPSWAT Metadefender Core service was stopped successfully.
 
 
The OPSWAT Metadefender Core Node service was stopped successfully.
 
PostgreSQL connection has lost. Please check the parameters.
 
The OPSWAT Metadefender Core service is starting.....
The OPSWAT Metadefender Core service was started successfully.
 
The OPSWAT Metadefender Core Node service is starting...
The OPSWAT Metadefender Core Node service was started successfully.
## Example 3: Remove engine only (retain its database)

BashCopyometascan-engine-sweeper.exe -B -H localhost -P 5432 -U postgres -D metadefender_core_lrmgvs -e 7z_13_windows -d

Note: Making sure to use “-B” parameter option if that is a local PostgreSQL server

Example output:

BashCopyMetaDefender Core v4 Engine Sweeper.
 
 
Data directory detected: "C:/Program Files/OPSWAT/Metadefender Core/data/"
 
Enter PostgreSQL password:
Engine(s) to clean: ("7z_13_windows")
 
 
The OPSWAT Metadefender Core service was stopped successfully.
 
 
The OPSWAT Metadefender Core Node service was stopped successfully.
 
PostgreSQL connection has lost. Please check the parameters.
 
The OPSWAT Metadefender Core service is starting.....
The OPSWAT Metadefender Core service was started successfully.
 
The OPSWAT Metadefender Core Node service is starting...
The OPSWAT Metadefender Core Node service was started successfully.
## Example 4: Remove all engines

BashCopyometascan-engine-sweeper.exe -B -H localhost -P 5432 -U postgres -D metadefender_core_lrmgvs -e "*"

Note: Making sure to use “-B” parameter option if that is a local PostgreSQL server

Example output:

BashCopyMetaDefender Core v4 Engine Sweeper.
 
 
Data directory detected: "C:/Program Files/OPSWAT/Metadefender Core/data/"
 
Enter PostgreSQL password:
Engine(s) to clean: ("ds_3_windows", "7z_13_windows", "clamav_1_windows", "mdcloud_5_windows", "oesis_3_windows", "dlp_8_windows", "filetype_1_windows", "yara_5_windows")
 
 
The OPSWAT Metadefender Core service was stopped successfully.
 
 
The OPSWAT Metadefender Core Node service was stopped successfully.
 
PostgreSQL connection has lost. Please check the parameters.
 
The OPSWAT Metadefender Core service is starting.....
The OPSWAT Metadefender Core service was started successfully.
 
The OPSWAT Metadefender Core Node service is starting...
The OPSWAT Metadefender Core Node service was started successfully.
