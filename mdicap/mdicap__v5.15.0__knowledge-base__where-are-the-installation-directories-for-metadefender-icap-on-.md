<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/where-are-the-installation-directories-for-metadefender-icap-on- -->

# Where are the installation directories for MetaDefender ICAP on Linux?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender ICAP releases deployed on Linux systems.

For automated deployment, ignition file is located at: `/etc/opswat/mdicapsrv.conf`

| **Directory** | **Files** |
| --- | --- |
| /var/lib/mdicapsrv | Main installation folder where Database tools, engines, and support package script are found |
| /etc/mdicapsrv  /usr/share/mdicapsrv | Configuration files for ICAP |
| /var/run/mdicapsrv | Webserver nginx processes and configuration |
| /var/tmp/mdicapsrv | Client-body and temporary files |
| /var/lib/mdicapsrv/engines | Filetype engine for file identification |
| /var/log/mdicapsrv | Rotating ICAP logs for files, NGINX logs for webserver and upgrade history log. |
| /usr/lib/mdicapsrv | Essential libraires and executables, postgres, and resources. |
| /sys/fs/cgroup/system.slice/mdicapsrv.service | ICAP service |
| /usr/share/doc/mdicapsrv | ccopyright and changelog |

[Additional configuration](https://www.opswat.com/docs/mdicap/installation/deployment-automation-support#ignition-file) for automated deployment is located in this file:

`/etc/opswat/mdicapsrv.conf`

Support:

**If** **Further Assistance** **is required, please proceed to log a** [****support case or chatting with our support engineer****](https://my.opswat.com/support) **.**
