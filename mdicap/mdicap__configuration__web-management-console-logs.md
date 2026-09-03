<!-- source: https://www.opswat.com/docs/mdicap/configuration/web-management-console-logs -->

# Web Management Console logs

The MetaDefender ICAP Server Web Management Console and REST interface is hosted by the nginix web server. Web Management Console and REST interface logs are written by nginx.

## [Linux](/docs/mdicap/configuration/web-management-console-logs#linux)

On Linux nginx logs to syslog. For details about syslog configuration see your distribution's manual.

## [Windows](/docs/mdicap/configuration/web-management-console-logs#windows)

Let us assume that MetaDefender ICAP Server is installed in:

C:\Path\To\Metadefender ICAP Server

In this case on Windows nginx logs to the following file:

C:\Path\To\Metadefender ICAP Server\nginx\nginx_error.log
