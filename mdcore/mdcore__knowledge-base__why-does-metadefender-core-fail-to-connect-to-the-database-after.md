<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-connect-to-the-database-after -->

# Why Does MetaDefender Core Fail to Connect to the Database After a System Restart?

This article applies to all MetaDefender Core version releases deployed on Windows.

#### [Scenario](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-connect-to-the-database-after#scenario)

When MetaDefender Core is configured to use a remote PostgreSQL database, the service may fail to reconnect to the database after the operating system restarts, even if the PostgreSQL server is running. As a result, you may see an error dashboard when trying to access the MetaDefender Core web UI.

When checking MD Core logs,

We can see the MetaDefender Core service could not reach the Database.

#### [The root cause](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-connect-to-the-database-after#the-root-cause)

The root cause is that MetaDefender Core service starts immediately after the operating system boots, before the network is fully initialized. As a result, the MetaDefender Core service is unable to connect to the PostgreSQL server during startup. This leads to the dashboard displaying a "could not connect to the database" message.

When the service is restarted manually, MD Core reconnects to the PostgreSQL server. By that time, the network is fully established, allowing the connection to succeed. This is why the service functions normally after a manual restart.

#### [The resolution/workaround](/docs/mdcore/knowledge-base/why-does-metadefender-core-fail-to-connect-to-the-database-after#the-resolutionworkaround)

The recommended workaround is to configure the MetaDefender Core service to start with the "Delayed Start" option.

This option allows the MetaDefender Core service to wait until the network has initialized successfully before starting service.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
