<!-- source: https://www.opswat.com/docs/mdcore/configuration/logging -->

# Logging

Since Metadefender Core (MD Core) v5.15.1, we’ve supported advanced log configuration, you can configure the log settings directly through the MetaDefender Core UI or via My OPSWAT Central Management: [Advanced Log Configurations](/docs/mdcore/configuration/advanced-log-configuration). However, the traditional configuration method (via registry or configuration file) is still supported: [MetaDefender Configuration](/docs/mdcore/configuration/metadefender-configuration). Logs settings configured through the MetaDefender Core UI, Endpoints or via My OPSWAT Central Management take precedence over those set via the registry or configuration file.

Note

Permissions to set:

- The directory that contains the logs: read, write and execute permissions for ometascan user or at least for ometascan group
- The other directories on the path to the logs: at least read and execute permissions for ometascan user and/or ometascan group

The new log settings will be used after a service restart or a HUP signal.

## [Remote Syslog](/docs/mdcore/configuration/logging#remote-syslog)

For SIEM integration such as Splunk, on MetaDefender Core side, enable syslog to send to Splunk syslog server via specific protocol and port. Then on that syslog server, configure to listen all incoming messages over the protocol and port.

Supported protocols are

- TCP. Example: `tcp://192.168.56.1:3586`
- UDP. Example: `udp://192.168.56.1:3585`
- TCPS - TLS over TCP. Example: `tcps://192.168.56.1:3586`

Info

When using TCPS - TLS over TCP, by default - MetaDefender Core will not allow for self-signed certs. If the users want to allow it, please change the option allow self signed cert with this [Remote Syslog API](https://www.opswat.com/docs/mdcore/metadefender-core#postsyslogconfig)
