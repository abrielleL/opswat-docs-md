<!-- source: https://www.opswat.com/docs/myop/knowledge-base/does-high-scanning-activity-on-metadefender-core-impact-ocm-perf -->

# Does High Scanning Activity on MetaDefender Core Impact OCM Performance?

This article applies to all OPSWAT Central Management releases deployed on Windows and Linux systems.

Under normal circumstances, a high volume of files being scanned on MetaDefender Core does not impact the performance of the OCM server. This is because:

- MetaDefender Core handles file scanning independently.
- OCM is primarily used for managing configurations, monitoring product health, and gathering statistics across OPSWAT deployments.
- File traffic (uploads and scans) does not flow through OCM.

### [When OCM May Be Affected](/docs/myop/knowledge-base/does-high-scanning-activity-on-metadefender-core-impact-ocm-perf#when-ocm-may-be-affected)

There is one unique case where OCM can experience increased activity due to scanning:

**Endpoint Integration (e.g., MetaDefender Endpoint):**

1. The endpoint device submits a scan request to OCM through endpoint client.
2. OCM responds with the address of a MetaDefender Core node.
3. The endpoint uploads the file directly to the Core node for scanning.

While the scan itself still occurs on MetaDefender Core, OCM is involved in the initial coordination. If your deployment includes a large number of endpoints submitting frequent scan requests, OCM may experience some load from processing and responding to these coordination requests.

### [Recommendations](/docs/myop/knowledge-base/does-high-scanning-activity-on-metadefender-core-impact-ocm-perf#recommendations)

- Monitor MetaDefender Core for processing load, resource usage (CPU, RAM, disk), and scan throughput.
- Monitor OCM for REST API performance and communication queue sizes only if you use endpoint integration.
- New OCM v10 on-prem displaying all the submissions from endpoints shall be introduced by the end of June 2025. Its cloud version has been available on MyOPSWAT already.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
