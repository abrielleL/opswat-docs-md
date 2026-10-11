<!-- source: https://www.opswat.com/docs/filescan/3.2.0/faq/sandbox-ioc-feed-reputation-service -->

# How do you integrate the Sandbox IOC feed into the MetaDefender Cloud Reputation Service?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Introduction](/docs/filescan/3.2.0/faq/sandbox-ioc-feed-reputation-service#introduction)

It is important to mention the 2-way integration between MetaDefender Aether and the MetaDefender Reputation service in the Cloud:

1. MetaDefender Aether uses the MetaDefender Cloud Reputation API to perform [OSINT Lookups](/docs/filescan/3.2.0/configuration/engine-config-osint-lookups) for supported IOC types (hashes, IPs, domains and URLs). This represents Layer 1 of the full analysis pipeline, and the reputation checks greatly improve the efficacy of the overall analysis.
2. MetaDefender Aether generates an IOC feed based on the public samples submitted to the <filescan.io> and <metadefender.com> Community sites. This IOC feed is continuously ingested into the internal database of the MetaDefender Reputation service to enrich the results of the Reputation API.

## [Processing Pipeline](/docs/filescan/3.2.0/faq/sandbox-ioc-feed-reputation-service#processing-pipeline)

The IOC processing pipeline includes the following steps:

1. [Filescan.io](filescan.io) aggregates scan reports and calculates individual verdicts for the IOCs included in these scan reports. Note that <filescan.io> might also ingest Sandbox scan results from <metadefender.com> (public scan reports are shared between the two Community sites).
2. The <filescan.io> backend creates a continuous IOC feed based on the summary of scan reports: <https://www.filescan.io/feed/reports>
3. The MetaDefender Reputation service periodically ingests the IOC feed data from <filescan.io>. All IOCs with a **valid verdict** are saved to the Reputation database with **all metadata** that is included in the IOC feed. Each IOC is indexed separately in the database to allow efficient lookup operations.

## [Example API Responses](/docs/filescan/3.2.0/faq/sandbox-ioc-feed-reputation-service#example-api-responses)

**Hash lookup** API response example including scan results from MetaDefender Aether:

Hash lookupCopy{
"file_info": {
"sha256": "D426DEFD9FC742C1E1524A7FBB93655C35735594F3C3E64B1F13280D7EDD24C9"
},
"scan_results": {
"scan_details": {
"MetaDefender Sandbox": {
"scan_result_i": 1,
"verdict": "MALICIOUS",
"parent_verdict": "MALICIOUS",
"origin": "VBA_EMULATION",
"flow_id": "6810b62e3be9346af4496cf5",
"def_time": "2025-04-30T15:23:18.000Z",
"first_seen": "2024-01-30T10:22:02.000Z",
"last_seen": "2025-04-30T15:23:18.000Z",
"scan_count": 10,
"tags": [
"keylogger",
"packed",
"anti-vm",
"anti-debug",
"fingerprint",
"expired-cert"
]
}
},
"scan_all_result_i": 1,
"scan_all_result_a": "Infected",
"total_detected_avs": 1,
"total_avs": 1
}
}

**URL lookup** API response example including MetaDefender Aether as a reputation provider:

JsonCopy{
"address": "http://example.com.cn",
"lookup_results": {
"start_time": "2025-05-08T16:04:59.024Z",
"detected_by": 2,
"sources": [
{
"provider": "MetaDefender Sandbox",
"assessment": "high risk",
"verdict": "MALICIOUS",
"parent_verdict": "MALICIOUS",
"origin": "INPUT_FILE",
"flow_id": "6810b62e3be9346a54346476et7t7",
"detect_time": "2025-04-30T15:23:18.000Z",
"first_seen": "2025-02-30T10:22:02.000Z",
"last_seen": "2025-04-30T15:23:18.000Z",
"scan_count": 3,
"tags": [
"peexe",
"html",
"javascript",
"overlay",
"packed",
"microsoft_visual_cc"
],
"update_time": "2025-05-08T16:07:28.306Z",
"status": 1
},
{
"provider": "webroot.com",
"assessment": "high risk",
"category": "Malware Sites",
"detect_time": "",
"update_time": "2025-05-08T16:07:28.306Z",
"status": 1
},
{
"provider": "www.team-cymru.org",
"assessment": "",
"detect_time": "",
"update_time": "2025-05-08T16:04:59.041Z",
"status": 5
},
{
"provider": "blocklist.de",
"assessment": "",
"detect_time": "",
"update_time": "2025-05-08T16:04:59.041Z",
"status": 5
},
...
]
}
}

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
