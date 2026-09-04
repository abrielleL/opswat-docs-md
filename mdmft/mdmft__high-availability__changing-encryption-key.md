<!-- source: https://www.opswat.com/docs/mdmft/high-availability/changing-encryption-key -->

# Changing encryption key

Summarize Page    Connect to Cursor Connect to VS Code

Changing the encryption key in a High Availability (HA) setup requires manual intervention on each node.

Since the encryption key rotation changes the secret and re-encrypts the connection string for the database, you have to manually copy the new secret file and the re-encrypted connection string from the active node to the passive node.

Warning

Without copying the new secret and the connection string, the passive node won't be able to connect to the database, and failover mechanisms will not function as expected.

After encryption key change please go to the installation directory of the active node and open the `<install-dir>\Services\opswat.vault.rest.service.exe.config` and copy the value of the `codataConnectionString`attribute. This is the new re-encrypted connection string.

Use this connection string to override the old connection string on the passive node. The connection string must be copied into 3 different files on the passive node:

1. `<install-dir>\Services\opswat.vault.rest.service.exe.config` - `codataConnectionString` attribute
2. `<install-dir>\Services\opswat.vault.processor.service.exe.config` -`codataConnectionString` attribute
3. `<install-dir>\Services\appsettings.json` - `DbConnectionString` property

After the overriding the connection strings copy and override the `<install-dir>\Services\secret.bin` file from the active node to the passive node.

Info

After the secret and connection string copy, perform a manual failover to verify that the passive node can take over the active role without issues. More info about manual failover can be found [here](/docs/mdmft/high-availability/failover-scenarios#manually-triggered-failover).
