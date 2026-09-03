<!-- source: https://www.opswat.com/docs/mdicap/installation/uninstall -->

# Uninstall

## [CentOS](/docs/mdicap/installation/uninstall#centos)

BashCopysudo yum remove mdicapsrv
## [Debian](/docs/mdicap/installation/uninstall#debian)

BashCopysudo apt remove mdicapsrv
## [Windows](/docs/mdicap/installation/uninstall#windows)

uninstall the MD ICAP Server application

## [Delete below folders if exist after uninstall](/docs/mdicap/installation/uninstall#delete-below-folders-if-exist-after-uninstall)

- - Linux:

    - /var/lib/mdicapsrv/pg_data
    - /usr/lib/mdicapsrv/postgres
    - /usr/lib/mdicapsrv/postgres-old
  - Windows:

    - C:\Program Files\OPSWAT\Metadefender ICAP Server\data\pg_data
    - C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres
    - C:\Program Files\OPSWAT\Metadefender ICAP Server\postgres-old
