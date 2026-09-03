<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-connect-a-metadefender-core-container-to-the-same-instanc -->

# How to Connect a MetaDefender Core Container to the same instance in Shared Database Mode?

**Introduction:**

This knowledge base article provides detailed instructions on deploying MetaDefender Core in a containerized environment using a shared database.

**Details:**

If you have a MetaDefender Core container deployment and wish to upgrade or make changes that involve removing and recreating one or more MetaDefender Core containers, but you want to retain all previous configurations and historical data, it is important to proceed carefully. To ensure continuity, the following environment variables are mandatory in order to connect to the same instance. Failing to use these variables will result in the creation of a new MetaDefender Core instance:

- *MD_INSTANCE_NAME*
- *MDCORE_DB_NAME*

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
