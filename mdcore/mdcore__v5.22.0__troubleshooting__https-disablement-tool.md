<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/https-disablement-tool -->

# HTTPS Configuration Removal Tool

This article is only applicable when:

- You have configured HTTPS on MetaDefender Core via UI options (not via NGINX custom config file).
- Unexpected failure with your certificate causing MetaDefender Core service failed to start, and thus you have no option to revert the configuration change already made on the UI.

The removal tool can be located and run as following:

## [Windows](/docs/mdcore/v5.22.0/troubleshooting/https-disablement-tool#windows)

<MetaDefender Core installation folder>\ometascan-reset-ssl-conf.exe

Restart MetaDefender Core service upon done.

## [Linux](/docs/mdcore/v5.22.0/troubleshooting/https-disablement-tool#linux)

export LD_LIBRARY_PATH=/usr/lib/ometascan/
/usr/sbin/ometascan-reset-ssl-conf

Restart MetaDefender Core service upon done.
