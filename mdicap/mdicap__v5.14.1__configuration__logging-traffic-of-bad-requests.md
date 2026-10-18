<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/logging-traffic-of-bad-requests -->

# Logging traffic of bad requests

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Logging raw TCP traffic can be used to identify issues with bad requests. It provides debug level details for requests that were refused by ICAP Server's request parser due to syntax errors.

## Important notes

Warning

Logging raw TCP traffic is not designed to be constantly enabled. It should only be used for investigating issues for short periods of time. Keeping it enabled permanently may impact performance. If running for too long, the log database can become huge and significantly reduce the available disk space.

Warning

Raw TCP traffic logs may contain sensitive or private information in a clear-text format.

## Step-by-step guide

Info

For configuration details see [3.1.2 MetaDefender ICAP Server configuration file](/configuration/configuration-file).

## Windows

### Enable logging raw TCP traffic

Perform the following steps to enable traffic logging:

1. Make sure MetaDefender ICAP Server is stopped

> net stop mdicapsrv

2. Open the Windows Registry with regedit. Go to the HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger entry
3. Add following entry with value:

   1. Name: capture_traffic
   2. Type: String (REG_SZ)
   3. Value: 1
4. Close the registry editor
5. Start MetaDefender ICAP server

> net start mdicapsrv
### Disable logging raw TCP traffic

Perform the following steps to disable traffic logging:

1. Make sure MetaDefender ICAP Server is stopped

> net stop mdicapsrv

2. Open the Windows Registry with regedit. Go to the HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger entry
3. Delete or modify the following entries with the following values:

   1. Name: capture_traffic
   2. Type: String (REG_SZ)
   3. Value: 0
4. Close the registry editor
5. Start MetaDefender ICAP server

> net start mdicapsrv
## Linux (CentOS syntax)

### Enable logging raw TCP traffic

Perform the following steps to enable traffic logging:

1. Make sure MetaDefender ICAP Server is stopped

# service mdicapsrv stop

2. Edit /etc/mdicapsrv/mdicapsrv.conf
3. Add or modify the following entry under the [logger] section with the following value:

   1. capture_traffic=1
4. Save and close the configuration file
5. Start MetaDefender ICAP server

# service mdicapsrv start
### Disable logging raw TCP traffic

Perform the following steps to enable traffic logging:

1. Make sure MetaDefender ICAP Server is stopped

# service mdicapsrv stop

2. Edit /etc/mdicapsrv/mdicapsrv.conf
3. Delete or modify the following entry under the [logger] section with the following value:

   1. capture_traffic=0
4. Save and close the configuration file
5. Start MetaDefender ICAP server

# service mdicapsrv start
