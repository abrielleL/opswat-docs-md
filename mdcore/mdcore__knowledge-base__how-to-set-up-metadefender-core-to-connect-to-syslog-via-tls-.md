<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-set-up-metadefender-core-to-connect-to-syslog-via-tls- -->

# How to Set Up MetaDefender Core to Connect to Syslog via TLS?

This article applies to MetaDefender Core version **5.15.1** releases deployed on Windows and Linux systems.

**In this version, MetaDefender Core introduces a user interface for configuring syslog settings** (refer to the [Release notes](/docs/mdcore/release-notes/release-notes)).

Your Splunk server is configured to listen on a TLS port and is using a self-signed certificate.

You can easily set up the syslog integration through the MetaDefender Core web UI:

1. Access the **Web Dashboard**.
2. Navigate to **Settings > Logs** to begin the configuration.

3. Next, click on “Edit” to modify the syslog settings.

4. You will now see an option in the settings to allow the use of self-signed certificates.

5. Once enabled, the syslog connection status will show as “Connected,” indicating that MetaDefender Core has successfully established a connection with the syslog server.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
