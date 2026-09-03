<!-- source: https://www.opswat.com/docs/mdinsights/data-formats/json-feed -->

# JSON Feed Format

MetaDefender InSights threat intelligence feeds are available in clear and concise [JSON](https://www.json.org/) data formats. JSON is a widely used serialization format that has become the de facto standard for online data interchange, and is broadly supported in many systems and platforms. This makes it simple to integrate MetaDefender InSights in your environment. This page documents the currently implemented formats.

## [Lookups](/docs/mdinsights/data-formats/json-feed#lookups)

The lookup is an API query returning a response in JSON format. Intel lookups may be issued on demand and are useful as part of automated workflows or application integrations. The response format consists of an object containing the following elements:

| Field | Description | Type |
| --- | --- | --- |
| **artifact** | The response object contains an inner object, where the key is the queried artifact (typically a domain name, IP address or URL). | String |
| **report** | The inner artifact object contains an inner object named report, which contains the report fields for the queried artifact. | Object |
| **score** | Resulting severity score for the queried artifact.  Range: 1-10 (higher numbers indicate greater severity). | Integer |
| **sources_alarmed** | Number of InSights intel sources that list the artifact. | Integer |
| **sources_evaluated** | Number of InSights intel sources evaluated for listing. | Integer |

The inner **report** object contains additional detail:

| Field | Description | Type |
| --- | --- | --- |
| **asn** | Autonomous system number (ASN) advertising the IP address artifact (enriched at time of ingestion). | String |
| **inquest** | InQuest verdict details containing proprietary information from reputation data sources.  *hits*: (Integer) Number of hits against tracked sources.  *malicious*: (Boolean) Verdict on the artifact (source).  *sources*: (Array) Names of tracked InSights TI sources. | Object |
| **malicious** | Verdict on the artifact (overall). | Boolean |
| **opswat** | OPSWAT verdict details containing proprietary information from our reputation data.  *hits*: (Integer) Number of hits against tracked sources.  *malicious*: (Boolean) Verdict on the artifact (source).  *sources*: (Array) Names of tracked InSights TI sources. | Object |

### [InSights C2 response samples](/docs/mdinsights/data-formats/json-feed#insights-c2-response-samples)

JsonCopy{
"details": {
"shatterbreathepsw.shop": "Lumma stealer is a multipurpose information stealing (stealer) trojan believed to be a fork of Vidar or Mars stealers."
},
"success": true
}JsonCopy{
"details": {
"xwsev7sb.top": "Cryptbot - InQuest Labs Analyst Network"
},
"success": true
}JsonCopy{
"details": {
"103.96.130.107": {
"asn": "",
"country": null,
"description": "Evasive Panda C2 host. This IP address is reported to be used for C2 during intrusions reportedly carried out by the Evasive Panda Chinese targeted threat group in the course of DNS poisoning attacks against target organizations."
}
},
"success": true
}
### [Reputation response samples](/docs/mdinsights/data-formats/json-feed#reputation-response-samples)

JsonCopy{
"centersoftwaresupports.azurewebsites.net": {
"report": {
"asn": {},
"inquest": {
"hits": 1,
"malicious": true,
"sources": [
"inquest-intelligence"
]
},
"malicious": true,
"opswat": {
"hits": 0,
"malicious": false,
"sources": []
}
},
"score": 6,
"sources_alarmed": 1,
"sources_evaluated": 24
}
}

The following example shows the response received when a queried indicator is **not** listed in the the threat intelligence collection:

- *score* is **0**.
- *sources_alarmed* is **0**.
- *report* does not have a *malicious* field set to **true**.

JsonCopy{
"thereisnosuchdomain.example.com": {
"report": {
"asn": {}
},
"score": 0,
"sources_alarmed": 0,
"sources_evaluated": 24
}
}
## [Snapshots](/docs/mdinsights/data-formats/json-feed#snapshots)

The snapshot feed download is an API query returning a response in JSON format. Intel data snapshots are intended to be retrieved on a continual basis, and each download provides the complete set of validated and relevant threat indicators that are active at the time of download. Indicators that have expired and are no longer active are not included in the snapshots feed in order to keep it fresh and actionable. The feed format consists of an array of indicator objects, each containing fields as described below:

### [Indicator formats](/docs/mdinsights/data-formats/json-feed#indicator-formats)

#### [InSights C2 format](/docs/mdinsights/data-formats/json-feed#insights-c2-format)

| Field | Description | Type |
| --- | --- | --- |
| **artifact** | Artifact type; one of:  *address*: IP address  *host*: hostname (or domain name) | String |
| **value** | Artifact value; the actual IP address or domain name | String |
| **score** | Severity (criticality) score; a rating of the threat level ranging from 1-10 | Integer |
| **source** | Internal feed source identifier; one of:  *labs-c2*: InSights C2 data | String (CSV) |
| **confidence** | Confidence score; a rating indicating the level of confidence that sightings of the artifact relate to a threat of the given severity ranging from 1-10 | Integer |
| **description** | Free-form descriptive context providing known details about the artifact | String |
| **created** | ISO 8601 timestamp (UTC) for artifact creation time in OPSWAT intelligence | ISO timestamp |
| **lastSeen** | ISO 8601 timestamp (UTC) for the last time the artifact was last seen in OPWAT’s collection | ISO timestamp |

#### [InSights TI format](/docs/mdinsights/data-formats/json-feed#insights-ti-format)

| Field | Description | Type |
| --- | --- | --- |
| **artifact** | Artifact type; one of:  *address*: IP address  *host*: hostname (or domain name)  *url*: Universal Resource Locator (URL) | String |
| **value** | Artifact value; the actual IP address, domain name, or URL | String |
| **score** | Severity (criticality) score; a rating of the threat level ranging from 1-10 | Integer |
| **source** | Internal feed source identifier; one of:  *labs-C2*: InSights C2 data  *labs-reputation*: InSights TI data  *labs-osint*: InSights OSINT data | String (CSV) |
| **confidence** | Confidence score; a rating indicating the level of confidence that sightings of the artifact relate to a threat of the given severity ranging from 1-10 | Integer |
| **description** | Free-form descriptive context providing known details about the artifact | String |
| **reference** | Reference to the origin or context for the classification of the artifact; examples:   - InQuest InSights Risky Domain - InQuest Labs - InQuest InSights Detected IP - InQuest InSights Detected RAT - InQuest InSights Risky IP   This field is only present in InSights TI artifacts. | String |
| **created** | ISO 8601 timestamp (UTC) for artifact creation time in OPSWAT intelligence | ISO timestamp |
| **lastSeen** | ISO 8601 timestamp (UTC) for the last time the artifact was last seen in OPWAT’s collection | ISO timestamp |
| **expiresOn** | ISO 8601 timestamp (UTC) for the time the artifact is scheduled to age out | ISO timestamp |

#### [InSights OSINT format](/docs/mdinsights/data-formats/json-feed#insights-osint-format)

| Field | Description | Type |
| --- | --- | --- |
| **artifact** | Artifact type; one of:  *domain*: hostname (or domain name) | String |
| **value** | Artifact value; the actual indicator value | String |
| **severity** | Severity (criticality) score; a rating of the threat level ranging from 1-10 | Integer |
| **confidence** | Confidence score; a rating indicating the level of confidence that sightings of the artifact relate to a threat of the given severity ranging from 1-10 | Integer |
| **sources** | Internal feed source identifiers, providing context by indicating the source of validation or overlap of OSINT indicator with OPSWAT data:  *<file-hash>*: Indicator overlapped with IOCs extracted by OPSWAT in our backend [DFI](https://labs.inquest.net/dfi) file processing corpus. This field provides the hashes of a small sample of relevant file hashes.  *iocdb*: Indicator identified in overlap with InQuest Labs [IOCDB](https://labs.inquest.net/iocdb) data  *repdb_derived*: Indicator identified in overlap with InQuest Labs [REPDB](https://labs.inquest.net/repdb) data  *domain-analysis-dfidb*: Indicator identified in overlap with OPSWAT [DFI](https://labs.inquest.net/dfi) file processing  *domain-analysis-iocdb*: Indicator identified in overlap with InQuest Labs [IOCDB](https://labs.inquest.net/iocdb) data  *domain-analysis-labs*: Indicator identified in overlap with [InQuest Labs](https://labs.inquest.net/) data  *domain-analysis-repdb*: Indicator identified in overlap with InQuest Labs [REPDB](https://labs.inquest.net/repdb) data  *domain-analysis-tidb*: Indicator identified in overlap with OPSWAT [MetaDefender InSights TI](https://www.opswat.com/products/metadefender/insights-ti) threat intelligence data | Array |
| **created_on** | ISO 8601 datestamp (UTC) for artifact creation time in OPSWAT intelligence | ISO datestamp |
| **modified_on** | ISO 8601 datestamp (UTC) for the last time the artifact was last seen in OPWAT’s collection | ISO datestamp |
| **expires_on** | ISO 8601 datestamp (UTC) for the time the artifact is scheduled to be age out | ISO datestamp |

### [Indicator samples](/docs/mdinsights/data-formats/json-feed#indicator-samples)

#### [InSights C2 feed samples](/docs/mdinsights/data-formats/json-feed#insights-c2-feed-samples)

JsonCopy{
"artifact": "host",
"value": "newlink.duckdns.org",
"score": 10,
"source": "labs-c2",
"confidence": 90,
"description": "Remcos C2 - Remcos is a commercial remote access tool (RAT) sold by Breaking Security. Distributed through malicious Microsoft Office documents attached to spam emails, the malware is executed using known UAC-bypass techniques. Once installed, Remcos is able to access all the controls commonly found in RATs. Unlike other RATs, Remcos features a built in Automatic Tasks feature that allows attackers to mimic spyware/malware downloader behavior. - https://x.com/1ZRR4H/status/1798735303286685905",
"created": "2024-06-06T17:41:33",
"lastSeen": "2024-06-06T17:43:27"
}JsonCopy{
"artifact": "host",
"value": "bernardofata.icu",
"score": 10,
"source": "labs-c2",
"confidence": 90,
"description": "Stealc C2 - Stealc is an information stealing trojan that targets client systems for theft of credentials and other sensitive data. - InQuest Empirical O
bservations",
"created": "2023-11-17T22:51:13",
"lastSeen": "2023-11-17T22:53:21"
}JsonCopy{
"artifact": "address",
"value": "154.12.23.136",
"score": 10,
"source": "labs-c2",
"confidence": 80,
"description": "Malware: Cobalt Strike C2 TCP connection on port 4444 last seen active on 2024-07-30 - InQuest Labs Partner Network",
"created": "2024-08-02T06:27:38",
"lastSeen": "2024-08-02T14:13:42"
}
#### [InSights TI feed samples](/docs/mdinsights/data-formats/json-feed#insights-ti-feed-samples)

JsonCopy{
"artifact": "host",
"value": "sjcb1ogmbxaefzo.xyz",
"score": 8,
"source": "labs-reputation",
"confidence": 30,
"description": "Website has been identified as malicious by Bing",
"reference": "InQuest Labs",
"created": "2024-08-09T00:42:56",
"lastSeen": null,
"expiresOn": "2024-10-06T06:42:56"
}JsonCopy{
"artifact": "address",
"value": "154.204.34.7",
"score": 8,
"source": "labs-reputation",
"confidence": 20,
"description": "InQuest Network Intelligence. Multiple communications observed between 154.204.34.7 on port 44728 and 110.34.181.109 (validated QuasarRAT C2 Server) on port 509 on 2024-08-10 at 04:17 UTC.",
"reference": "InQuest InSights Risky IP",
"created": "2024-07-04T08:51:21",
"lastSeen": "2024-08-13T23:06:00",
"expiresOn": "2024-08-28T23:06:00"
}
#### [InSights OSINT feed samples](/docs/mdinsights/data-formats/json-feed#insights-osint-feed-samples)

JsonCopy{
"artifact": "domain",
"value": "case7853.facebook-safe.com",
"severity": 5,
"confidence": 6,
"sources": [
"domain-analysis-tidb"
],
"created_on": "2025-02-11",
"modified_on": "2025-02-11",
"expires_on": "2025-05-12"
}
