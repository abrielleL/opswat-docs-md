<!-- source: https://www.opswat.com/docs/mdcloud/threat-intelligence/threat-intelligence -->

# Threat Intelligence

Threat Intelligence Search API at OPSWAT has multiple offerings:

**Pattern Search (expression search)**: Expression search, involves searching for specific patterns or expressions within threat intelligence data. This approach focuses on finding exact matches of predefined expressions such as malware families, malware threat names, AV detection filtering, first/last seen, etc. By performing expression searches, security professionals can quickly identify known threats or indicators associated with specific malware, campaigns, or threat actors. It is a highly effective method for detecting previously identified threats and known attack patterns.

**Similarity Search**: Similarity search, involves looking for patterns or indicators that are similar to known threats or IOCs, even if they are not exact matches. Instead of relying on exact matches, this approach utilizes algorithms and techniques such as clustering or machine learning to identify similarities between data points. Similarity search is useful when dealing with variations or mutations of known threats, where attackers may slightly modify their tactics to evade detection. By identifying similar patterns or behaviors, security professionals can uncover new or emerging threats that share characteristics with known malicious activities.

| Key Features: |
| --- |
| - Pattern search (expression search) intelligence data that focuses on finding exact matches of predefined expressions such as malware families, malware threat names, AV detection filtering, first/last seen, etc |
| - Similarity search that are looking for for patterns or indicators that are similar to known threats or IOCs, even if they are not exact matches |
| - Retrieves the list of similar files and scores that have been previously scanned using Filescan, using SHA256 |
| - Rapid search for hashes using multi-part search criteria |
| - Returns AV file reputation status for a file hash by MD5, SHA1, or SHA256 The status can be: MALICIOUS, SUSPICIOUS, BENIGN, or UNKNOWN |
| - Provides file analysis data on hashes (MD5, SHA1, or SHA256). Metadata can include relevant portions of static and dynamic analysis, AV scan information, file sources |

Read more about our Threat Intelligence capabilities [here](https://docs.opswat.com/mdcloud/metadefender-cloud-threat-intelligence-api-v5/ref#top).
