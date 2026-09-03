<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-can-performance-of-metadefender-core-be-increased-when-deplo -->

# How can performance of MetaDefender Core be increased when deployed on K8S environments?

This article applies to all supported versions of MetaDefender Core

## [**Background**](/docs/mdcore/knowledge-base/how-can-performance-of-metadefender-core-be-increased-when-deplo#background)

While resource allocation influence the performance of MetaDefender Core, there are also internal environmental variables specific to the MetaDefender Core application that can be updated to increase performance on a Kubernetes deployment as well as we do on regular package installs.

## [**Steps**](/docs/mdcore/knowledge-base/how-can-performance-of-metadefender-core-be-increased-when-deplo#steps)

For Kubernetes deployments, you can make updates to performance parameters using the CORE_CONG_JSON variable locates in the values.yaml file, like is done in [metadefender-k8s/helm_charts/mdcore/values.yaml at f13e458b58b730d0735d2624abc4aef655c4487e · OPSWAT/metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s/blob/f13e458b58b730d0735d2624abc4aef655c4487e/helm_charts/mdcore/values.yaml#L112)

Using this environment variable, different values detailed in [MetaDefender Configuration](https://www.opswat.com/docs/mdcore/configuration/metadefender-configuration#linux) can be set. In particular the ones related to performance like parallecount, db_connection, etc. Keep in mind that the format for these entries should follow the format below:

`[Section]/[parameter]: [value]`

## [**Example**](/docs/mdcore/knowledge-base/how-can-performance-of-metadefender-core-be-increased-when-deplo#example)

For example, to set the parallel_count from its default, you can add an entry like: **"internal/parallelcount": 40**. This line would be updated as follows:

`CORE_CONF_JSON: '{"global/restaddress": "0.0.0.0", "internal/parallelcount": 40, "internal/next_extraction_polling_interval": 1000}'`

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
