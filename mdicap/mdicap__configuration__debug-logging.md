<!-- source: https://www.opswat.com/docs/mdicap/configuration/debug-logging -->

# Debug logging

Debug logging can be used to identify issues with connections. It provides debug level details for each connections as well as the time each step took (e.g. parsing time, scan time, response time). It also tracks the number of active connections.

## Important notes

Note

Debug logging is not designed to be constantly enabled. It should only be used for investigating issues for short periods of time.

Keeping it enabled permanently may impact performance. If running for too long, the log file can become very large and significantly reduce the available disk space.

Note

In each case below, both logfile and loglevel settings must be set for the changes to be active.

## Step-by-step guide

## Windows

### Enable debug logging

Perform the following steps to enable debug logging:

1. Make sure MetaDefender ICAP Server is stopped

> net stop mdicapsrv

2. Open the Windows Registry with regedit. Go to the HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger entry
3. Add or modify the following entries with the following values:

   1. loglevel: debug
   2. wineventlog_level: debug
4. Close the registry editor
5. Start MetaDefender ICAP server

> net start mdicapsrv
### Disable debug logging

Perform the following steps to disable debug logging:

1. Make sure MetaDefender ICAP Server is stopped

> net stop mdicapsrv

2. Open the Windows Registry with regedit. Go to the HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger entry
3. Add or modify the following entries with the following values:

   1. loglevel: info
   2. wineventlog_level: info
4. Close the registry editor
5. Start MetaDefender ICAP server

> net start mdicapsrv
## Linux (CentOS syntax)

### Enable debug logging

Perform the following steps to enable debug logging:

1. Make sure MetaDefender ICAP Server is stopped

# service mdicapsrv stop

2. Edit /etc/mdicapsrv/mdicapsrv.conf
3. Add or modify the following entry under the [logger] section with the following value:

   1. loglevel: debug
4. Save and close the configuration file
5. Start MetaDefender ICAP server

# service mdicapsrv start
### Disable debug logging

Perform the following steps to enable debug logging:

1. Make sure MetaDefender ICAP Server is stopped

# service mdicapsrv stop

2. Edit /etc/mdicapsrv/mdicapsrv.conf
3. Add or modify the following entry under the [logger] section with the following value:

   1. loglevel: info
4. Save and close the configuration file
5. Start MetaDefender ICAP server

# service mdicapsrv start
