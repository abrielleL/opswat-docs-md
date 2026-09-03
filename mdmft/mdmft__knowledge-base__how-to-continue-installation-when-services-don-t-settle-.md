<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-to-continue-installation-when-services-don-t-settle- -->

# How to continue installation when services don't settle?

Summarize Page    Connect to Cursor Connect to VS Code
## [Applies to](/docs/mdmft/knowledge-base/how-to-continue-installation-when-services-don-t-settle-#applies-to)

- MetaDefender Managed File Transfer™ version 3.11.0 or later
- Upgrade or Uninstallation

## [Symptoms](/docs/mdmft/knowledge-base/how-to-continue-installation-when-services-don-t-settle-#symptoms)

For stability reasons the installer tries to prevent installation from progressing until the services are completely started or stopped, but in some cases they start up slower or become stuck.

1. The installation waits for services to settle and leave starting or stopping state
2. The wait times times out with an installation failure.

This window is not a sign of error itself. Installer is monitoring the service states.

Services are still stuck after the time elapsed

## [Resolving by addressing known problems](/docs/mdmft/knowledge-base/how-to-continue-installation-when-services-don-t-settle-#resolving-by-addressing-known-problems)

- When database server is on the same host machine as MetaDefender Managed File Transfer™ and the installer was started shortly after machine startup, the delayed start of the database service might delay the MetaDefender Managed File Transfer™ services as well. This is expected to finish before the timeout period is reached.
- Ensure database service is running and is reachable for MetaDefender Managed File Transfer™ services

## [Resolving the stuck services](/docs/mdmft/knowledge-base/how-to-continue-installation-when-services-don-t-settle-#resolving-the-stuck-services)

If the known problems didn't help, the services can be forced to be stopped and let the installer continue.

While the installer is waiting do the following

1. Disable all the MetaDefender Managed File Transfer™ services that are in a starting or stopping state. Setting it to Manual is not enough.
2. Close the service manager window. This sometimes interferes with service removal.
3. Kill allMetaDefender Managed File Transfer™ processes (opswat.vault.<servicename>.service.exe)
4. The installer will detect the service change and continue
5. During an upgrade, the services will be reinstalled with the services active again.

Set services to disabled

If the service manager wasn't closed, you might see this error. Close the window and select retry.
