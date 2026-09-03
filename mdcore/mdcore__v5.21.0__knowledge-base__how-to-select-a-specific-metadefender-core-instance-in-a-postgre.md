<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-select-a-specific-metadefender-core-instance-in-a-postgre -->

# How to Select a Specific MetaDefender Core Instance in a PostgreSQL Database with Multiple Instances?

This article is applied to MetaDefender Core releases deployed on Windows and Linux systems.

**Issue**:

When connecting MetaDefender Core to a PostgreSQL database that contains multiple MetaDefender Core instances, there is currently no option within the Core installation interface to select a specific instance. In a Shared Database configuration, MetaDefender Core will connect to and use the first available MetaDefender Core shared instance found within the database. The selection is made automatically by the application and cannot be overridden.

**Resolution**:

If it is mandatory to use a database with multiple instances, use the Docker or Kubernetes environments, where this option is available. For example, in a docker deployment, the environmental variable `MDCore_DB_NAME` can be used to point to a specific database instance.

Support:

Support: If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
