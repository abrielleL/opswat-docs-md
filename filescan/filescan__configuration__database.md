<!-- source: https://www.opswat.com/docs/filescan/configuration/database -->

# Database

These configurations are related to database connections within the Sandbox webservice.

The location of the ***Database*** settings are **Admin Panel > Settings >** [**Configurations**](https://www.filescan.io/admin/settings/config) **> Database.**

Screenshot of Database configuration on MetaDefender Sandbox webpage

| Field | Description |
| --- | --- |
| `DB_CONN_URL` | It specifies the connection URL for the primary database used by Sandbox. It should determine what is its primary database, what is the accessible hostname and on what port. Sandbox includes its own MongoDB container. The default setting should not be changed. |
| `GRAPH_DB_CONN_URL` | It specifies the connection URL for a graph database used by Sandbox. Sandbox includes its own graph database container. The default setting should not be changed. |
| `REDIS_CONN_URL` | This configuration specifies the connection URL for a Redis database used by the application. Sandbox includes its own Redis container. The default setting should not be changed. |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
