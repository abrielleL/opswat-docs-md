<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-access-the-metadefender-core-user-interface-after- -->

# Why can’t I access the MetaDefender Core user interface after performing an upgrade?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

After performing an upgrade of MetaDefender Core, you may encounter issues accessing the user interface.

### [Scenario 1: System or Configuration-Related Issues](/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-access-the-metadefender-core-user-interface-after-#scenario-1-system-or-configuration-related-issues)

If the MetaDefender Core service fails to start or crashes, it could be due to various system-level or configuration-related problems. These may include missing dependencies, permission issues, or service conflicts.

Refer to this support article: Why does the MetaDefender Core service not start? for a detailed list of common causes and troubleshooting steps for both Windows and Linux environments.

### [Scenario 2: SSL Certificate Issue After Upgrade](/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-access-the-metadefender-core-user-interface-after-#scenario-2-ssl-certificate-issue-after-upgrade)

Another common cause, especially after an upgrade, is that SSL certificate settings are not retained. If HTTPS was previously enabled with a custom certificate, the upgrade process may not preserve that configuration. As a result, the UI may fail to load.

To resolve this, refer to the steps for checking local access and resetting the SSL configuration.

Note:

This section addresses a specific case where the MetaDefender Core UI becomes inaccessible after an upgrade, due to a lost SSL certificate configuration.

- For general UI access issues unrelated to upgrades or SSL, see Troubleshooting Inaccessible Management Console.
- For detailed steps on using the SSL configuration reset tool, see Resetting HTTPS Configuration.

Here’s how you can resolve the issue:

### [Step 1: Check local access](/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-access-the-metadefender-core-user-interface-after-#step-1-check-local-access)

1. Open your browser.
2. Try accessing the MetaDefender Core UI through one of the following addresses:

   - [http://localhost:8008](http://localhost:8008/)
   - [https://localhost:8008](https://localhost:8008/)

*If successful, you can re-add your certificate directly from the UI.*

### [Step 2: Reset SSL configuration](/docs/mdcore/v5.22.0/knowledge-base/why-can---t-i-access-the-metadefender-core-user-interface-after-#step-2-reset-ssl-configuration)

If you still cannot access the UI:

1. Navigate to the MetaDefender Core installation folder:

C:\Program Files\OPSWAT\MetaDefender Core\

2. Locate and run the tool:

ometascan-reset-ssl-conf.exe

3. This will remove the existing certificate configuration.
4. Re-add your certificate through the MetaDefender Core UI.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
