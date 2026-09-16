<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-require-removing-the-ssl-private-key- -->

# Why Does MetaDefender Core Require Removing the SSL Private Key Passphrase for PostgreSQL?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

When enabling SSL for PostgreSQL, the documentation instructs removing the passphrase from the private key (`server.key`). This can raise concerns, as passphrases are usually seen as a security measure.

### [**Why It’s Required**](/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-require-removing-the-ssl-private-key-#why-its-required)

PostgreSQL runs as a background service and starts automatically on system reboot. It cannot prompt for a passphrase during startup. If the key is still protected, the database fails to start, preventing MetaDefender Core from running.

Removing the passphrase allows the key to be loaded automatically, ensuring reliable, hands-off operation.

### [**Can the Passphrase Be Kept?**](/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-require-removing-the-ssl-private-key-#can-the-passphrase-be-kept)

Technically yes, but it’s impractical:

- You would need to manually start PostgreSQL and enter the passphrase after each reboot.
- Secure automation would require advanced solutions like hardware key management, which are not part of standard deployments.

### [**How the Key Is Secured**](/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-require-removing-the-ssl-private-key-#how-the-key-is-secured)

Even without a passphrase:

- Run MetaDefender Core under a dedicated service account.
- Restrict file permissions so only that account and administrators can access `server.key`.

SSL encryption remains fully active; only the key access method changes.

### [**Conclusion**](/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-require-removing-the-ssl-private-key-#conclusion)

Removing the passphrase is necessary for automatic startup and reliable operation. Security is maintained through OS-level access controls, while SSL encryption continues to protect database communication.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
