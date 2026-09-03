<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-customize-the-bundled-postgresql-server-configuration-i -->

# How do I customize the bundled PostgreSQL server configuration in MetaDefender Core?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

### [**Overview**](/docs/mdcore/knowledge-base/how-do-i-customize-the-bundled-postgresql-server-configuration-i#overview)

This article describes how to customize the PostgreSQL configuration for the bundled PostgreSQL server that comes with MetaDefender Core.

For example, one goal of making such configurations is to meet requirements in the CIS benchmark for PostgreSQL server.

### [**Steps to Configure**](/docs/mdcore/knowledge-base/how-do-i-customize-the-bundled-postgresql-server-configuration-i#steps-to-configure)

To resolve the issues and achieve CIS benchmark compliance without affecting MetaDefender Core operations, follow these steps:

Important:

Do not modify the bundled `postgresql.conf` located at `OPSWAT\MetaDefender Core\data\pg_data\postgresql.conf` because it is controlled by MetaDefender Core and resets on service restart.

1. Instead, create and edit a new configuration file, which overrides the default configuration, and changes made here will persist after restarts:

   1. Windows: `<installation directory>\OPSWAT\MetaDefender Core\postgres\postgresql.conf`
   2. Linux: `/usr/lib/ometascan/postgres/postgresql.conf`
2. Add any configuration parameters needed, such as `ssl_ciphers`, and save the file.
3. Restart the MetaDefender Core service (which also restarts the bundled PostgreSQL server).

**Note**: if SSL configuration for PostgreSQL server needs to be made, such as enabling SSL connection, please refer to [SSL Connection for bundled PostgreSQL](/docs/mdcore/configuration/ssl-connection-for-postgresql-communication).

### [**Verify the Change**](/docs/mdcore/knowledge-base/how-do-i-customize-the-bundled-postgresql-server-configuration-i#verify-the-change)

After the service restarts, check and verify that the custom parameters have overridden the default ones.

If you’re making these configurations according to CIS benchmarks, refer to the relevant CIS documentation for the audit steps to verify that PostgreSQL is using the recommended settings.

Remote PostgreSQL server:

For more control over PostgreSQL configuration, consider deploying MetaDefender Core with a **remote PostgreSQL server** that you manage. This avoids limitations of the bundled PostgreSQL server.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
