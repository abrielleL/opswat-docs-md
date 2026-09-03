<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-completely-uninstall-metadefender-icap- -->

# How to completely uninstall MetaDefender ICAP?

This article applies to all MetaDefender ICAP releases deployed on Windows and Linux systems.

Info

If you installed using an ignition file (located at C:\OPSWAT\mdicapsrv.conf or /etc/opswat/mdicapsrv.conf), this file is not removed automatically by any of the steps below - you must delete or manage it yourself.

## [**Windows**](/docs/mdicap/knowledge-base/how-to-completely-uninstall-metadefender-icap-#windows)

1. Uninstall the software from Apps & Features or the Control Panel.
2. Remove leftover Registry keys (if any exist):

   - Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server
   - Computer\HKEY_CURRENT_USER\Software\OPSWAT\Metadefender ICAP Server
3. Remove leftover folders (if any exist):

   - C:\Program Files\OPSWAT\Metadefender ICAP Server
   - C:\ProgramData\OPSWAT\MetaDefender ICAP

## [**Linux**](/docs/mdicap/knowledge-base/how-to-completely-uninstall-metadefender-icap-#linux)

1. Uninstall the ICAP software

**Debian/Ubuntu (deb-based systems):**

sudo dpkg --purge mdicapsrv

This single command uninstalls the package and removes its configuration files.

**RedHat/CentOS/Rocky (rpm-based systems):**

sudo yum remove mdicapsrv

2. Ensure all remaining files are removed (both distro families):

sudo find / -name "mdicapsrv*" 2>/dev/null

e.g. directories commonly left behind include:

/var/lib/mdicapsrv
/etc/mdicapsrv
/usr/lib/mdicapsrv
/usr/share/mdicapsrv
/var/tmp/mdicapsrv
/var/log/mdicapsrv

3. Remove any that the find command turns up:

sudo rm -rf <directory_name>

**Support:**

Support:

If **further assistance** is required, please log a [**support case or chat with our support engineer**](https://my.opswat.com/support).
