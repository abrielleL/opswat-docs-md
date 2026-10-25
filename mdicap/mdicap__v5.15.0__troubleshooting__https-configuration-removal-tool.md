<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/troubleshooting/https-configuration-removal-tool -->

# HTTPS Configuration Removal Tool

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

This article is only applicable when:

- You have configured HTTPS on MetaDefender ICAP Servr via UI options (not via NGINX custom config file).
- Unexpected failure with your certificate causing MetaDefender ICAP Server service failed to start, and thus you have no option to revert the configuration change already made on the UI.

The removal tool can be located and run as following:

## [Windows](https://docs.opswat.com/mdcore/troubleshooting/https-disablement-tool#windows)

**Step 1**: Start command Prompt as administrator

**Step 2**: Run **mdicapsrv-reset-ssl-conf.exe**

BashCopy<MetaDefender ICAP Server installation folder>\mdicapsrv-reset-ssl-conf.exe
E.g:
"C:\Program Files\OPSWAT\Metadefender ICAP Server\mdicapsrv-reset-ssl-conf.exe"

**Step 3:** Restart MetaDefender ICAP Server service upon done.

## [Linux](/docs/mdicap/v5.15.0/troubleshooting/https-configuration-removal-tool#linux)

**Step 1**: run below command as administrator

BashCopysudo LD_LIBRARY_PATH=/usr/lib/mdicapsrv /usr/sbin/mdicapsrv-reset-ssl-conf

**Step 2 :** Restart MetaDefender ICAP Server service upon done.
