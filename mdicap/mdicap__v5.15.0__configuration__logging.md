<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/logging -->

# Logging

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender ICAP Server has wide variety of options to configure logging. Log settings are in the configuration files or in the Windows Registry. To see more details about log configuration see the following pages:

- [3.5.1 Configuration](/docs/mdicap/v5.15.0/configuration/configuration)
- [3.5.2 Debug logging](/docs/mdicap/v5.15.0/configuration/debug-logging)
- [3.5.3 Web Management Console logs](/docs/mdicap/v5.15.0/configuration/web-management-console-logs)
- [3.5.4 Logging traffic of bad requests](/docs/mdicap/v5.15.0/configuration/logging-traffic-of-bad-requests)

For SIEM integration such as Splunk, on MetaDefender ICAP side, enable syslog to send to Splunk syslog server via specific protocol (TCP/UDP) and port. Then on that syslog server, configure to listen all incoming messages over the protocol and port (refer to syslog option in [Configuration file](/docs/mdicap/v5.15.0/configuration/configuration-file))
