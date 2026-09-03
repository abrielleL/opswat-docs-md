<!-- source: https://www.opswat.com/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5/ref -->

## About This Guide

Welcome to the MetaDefender Cloud Threat Intelligence guide. This guide is intended to provide the information for:

- Organizations that want to be on the lookout for the hottest malware
- IT specialists that implement file blacklists based on hashes
- Researchers analyzing trending malware on the market
- Security products that leverage Threat Intelligence capabilities to harden security measures

---

## WARNING

**A commercial license is required to access the Threat Intelligence v5 API endpoints. Free users will not be able to access these endpoints. Please [contact OPSWAT Sales](https://www.opswat.com/contact) to set up a time-limited evaluation license for your organization.**

---

## How to use MetaDefender Cloud Threat Intelligence Public APIs

Learn about new features, updated features, and bug fixes
Learn about frequently asked questions and additional concepts through our library of knowledge base articles

## Key Features of MetaDefender Cloud Threat Intelligence

> ***AV File Reputation***

> ***File Analysis***

> ***Scan History***

> ***Expression Search***

> ***Similarity Search***

Serverhttps://api.metadefender.com/v5Server Variables
## Av File Reputation

Returns AV file reputation status for a file hash by MD5, SHA1, or SHA256 The status can be: MALICIOUS, SUSPICIOUS, BENIGN, or UNKNOWN. This status depends on the confidence level:

- when confidence_level = 0 then 'benign'
- when confidence_level < 50 then 'suspicious'
- when confidence_level >= 50 then 'malicious'
- else 'unknown'

The confidence level is calculated using the AV detection percentage and the dynamic analysis result (if it exists).

[More about file types](https://docs.opswat.com/mdcloud/v5/integrations/description-of-file-categories)

**WARNING: This is an experimental endpoint, it may change in the future!.**

Endpoints[GET/threat-intel/av-file-reputation/{hash}](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#av-file-reputation) [POST/threat-intel/av-file-reputation/](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#av-file-reputation-bulk)
### AV file reputation status

Retrieve AV file reputation information by looking up a hash using MD5, SHA1 or SHA256

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |
| extended | integer | Include additional metadata about the hash. By default, it is false (0). WARNING: When this flag is enabled (1), it results in DOUBLE credit consumption against the daily limit!  *Allowed values*   - *0 (get reputation only)* - *1 (get additional details)* |  |

Path Params

| hash | string | A hash is used to identify a file (MD5, SHA1 or SHA256) |  |
| --- | --- | --- | --- |

GET /threat-intel/av-file-reputation/{hash}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

AV_File_ReputationAV_File_Reputation_Extended

| AV File Reputation | object |  |  |
| --- | --- | --- | --- |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| reputation | string | Enum: `benign`,`suspicious`,`malicious`,`unknown` |  |
| reputation_i | int32 |  |  |

400

Bad request

 Response
### AV file reputation status (Bulk lookup)

Retrieve AV file reputation information by looking up a list of hashes (MD5, SHA1 or SHA256)

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |
| Content-Type | string | Specify the http content type  *Allowed values - application/json* |  |
| extended | integer | Include additional metadata about the hash. By default, it is false (0). WARNING: When this flag is enabled (1), it results in DOUBLE credit consumption against the daily limit!  *Allowed values*   - *0 (get reputation only)* - *1 (get additional details)* |  |

Request Body application/json

List of hashes whose reputation you are interested in

| JSON payload for bulk lookup | object |  |  |
| --- | --- | --- | --- |
| hash | array[string] |  |  |

POST /threat-intel/av-file-reputation/cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

OK

AV_File_Reputation_BulkAV_File_Reputation_Extended_Bulk

| AV File Reputation (Bulk lookup) | object |  |  |
| --- | --- | --- | --- |
| data5 fields | array[object] |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| reputation | string | Enum: `benign`,`suspicious`,`malicious`,`unknown` |  |
| reputation_i | int32 |  |  |

400

Bad request

 Response
## File Analysis

Provides file analysis data on hashes (MD5, SHA1, or SHA256). Metadata can include relevant portions of static analysis, AV scan information, file sources and any related IP/domain information.

**WARNING: This is an experimental endpoint, it may change in the future!.**

Endpoints[GET/threat-intel/file-analysis/{hash}](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#file-analysis) [POST/threat-intel/file-analysis/](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#file-analysis-bulk)
### File analysis data

Provides file analysis data on hashes (MD5, SHA1, or SHA256). Metadata can include relevant portions of static and dynamic analysis, AV scan information, file sources.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |

Path Params

| hash | string | A hash is used to identify a file (MD5, SHA1 or SHA256) |  |
| --- | --- | --- | --- |

GET /threat-intel/file-analysis/{hash}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| File Analysis | object |  |  |
| --- | --- | --- | --- |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| first_seen | date-time |  |  |
| last_seen | date-time |  |  |
| update_timestamp | date-time |  |  |
| file_info5 fields | object |  |  |
| file_size | int32 |  |  |
| file_type | string |  |  |
| file_type_category | string |  |  |
| file_type_description | string |  |  |
| file_type_extension | string |  |  |
| file_sources | array[string] | Enum: `partner`,`customer` |  |
| last_av_scan11 fields | object |  |  |
| malware_families | array[string] |  |  |
| malware_types | array[string] |  |  |
| platforms | array[string] | Enum: `Generic`,`MacOS`,`DOS`,`Win32`,`Win64`,`Android`,`Linux` |  |
| scan_all_result_i | int32 |  |  |
| scan_details1 field | object |  |  |
| scan engine | object |  |  |
| threat_found | string |  |  |
| scan_result_i | int32 |  |  |
| standard_threat_name | string |  |  |
| start_time | date-time |  |  |
| sub_platform | string |  |  |
| total_avs | int32 |  |  |
| total_detected_avs | int32 |  |  |
| total_time | int32 |  |  |
| trust_factor | int32 |  |  |

400

Bad request

 Response
### File analysis data (Bulk lookup)

Bulk lookup of file analysis data on hashes (MD5, SHA1, or SHA256). Metadata can include relevant portions of static and dynamic analysis, AV scan information, file sources.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |
| Content-Type | string | Specify the http content type *Allowed values - application/json* |  |

Request Body application/json

List of hashes whose analysis you are interested in

| JSON payload for bulk lookup | object |  |  |
| --- | --- | --- | --- |
| hash | array[string] |  |  |

POST /threat-intel/file-analysis/cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| data10 fields | array[object] |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| first_seen | date-time |  |  |
| last_seen | date-time |  |  |
| update_timestamp | date-time |  |  |
| file_info5 fields | object |  |  |
| file_size | int32 |  |  |
| file_type | string |  |  |
| file_type_category | string |  |  |
| file_type_description | string |  |  |
| file_type_extension | string |  |  |
| file_sources | array[string] | Enum: `partner`,`customer` |  |
| last_av_scan11 fields | object |  |  |
| malware_families | array[string] |  |  |
| malware_types | array[string] |  |  |
| platforms | array[string] | Enum: `Generic`,`MacOS`,`DOS`,`Win32`,`Win64`,`Android`,`Linux` |  |
| scan_all_result_i | int32 |  |  |
| scan_details1 field | object |  |  |
| scan engine | object |  |  |
| threat_found | string |  |  |
| scan_result_i | int32 |  |  |
| standard_threat_name | string |  |  |
| start_time | date-time |  |  |
| sub_platform | string |  |  |
| total_avs | int32 |  |  |
| total_detected_avs | int32 |  |  |
| total_time | int32 |  |  |
| trust_factor | int32 |  |  |

400

Bad request

 Response
## Av Scan History

Provides up to 50 historic AV scan results (threat detections from over 24 AV scanners) based on the file hash (in MD5, SHA1 or SHA256 format).

**WARNING: This is an experimental endpoint, it may change in the future!.**

Endpoints[GET/threat-intel/av-scan-history/{hash}](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#av-scan-history) [POST/threat-intel/av-scan-history/](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#av-scan-history-bulk)
### AV scan history results

Provides up to 50 historic AV scan results (threat detections from over 24 AV scanners) based on the file hash (in MD5, SHA1 or SHA256 format).

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |

Path Params

| hash | string | A hash is used to identify a file (MD5, SHA1 or SHA256) |  |
| --- | --- | --- | --- |

GET /threat-intel/av-scan-history/{hash}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| AV Scan History | object |  |  |
| --- | --- | --- | --- |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| first_seen | date-time |  |  |
| last_seen | date-time |  |  |
| update_timestamp | date-time |  |  |
| av_scan_history5 fields | array[object] |  |  |
| av_detections | object |  |  |
| scan_all_result_i | int32 |  |  |
| start_time | date-time |  |  |
| total_avs | int32 |  |  |
| total_detected_avs | int32 |  |  |

400

Bad request

 Response
### AV scan history results (Bulk lookup)

Bulk lookup of historic AV scan results for multiple files (using hashes in the MD5, SHA1 or SHA256 format). For a given hash, it is possible to retrieve up to 50 scan results (including threat detections from over 24 AV scanners).

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |
| Content-Type | string | Specify the http content type *Allowed values - application/json* |  |

Request Body application/json

List of hashes whose scan history you are interested in

| JSON payload for bulk lookup | object |  |  |
| --- | --- | --- | --- |
| hash | array[string] |  |  |

POST /threat-intel/av-scan-history/cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| data10 fields | array[object] |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| first_seen | date-time |  |  |
| last_seen | date-time |  |  |
| update_timestamp | date-time |  |  |
| file_info5 fields | object |  |  |
| file_size | int32 |  |  |
| file_type | string |  |  |
| file_type_category | string |  |  |
| file_type_description | string |  |  |
| file_type_extension | string |  |  |
| file_sources | array[string] | Enum: `partner`,`customer` |  |
| last_av_scan11 fields | object |  |  |
| malware_families | array[string] |  |  |
| malware_types | array[string] |  |  |
| platforms | array[string] | Enum: `Generic`,`MacOS`,`DOS`,`Win32`,`Win64`,`Android`,`Linux` |  |
| scan_all_result_i | int32 |  |  |
| scan_details1 field | object |  |  |
| scan engine | object |  |  |
| threat_found | string |  |  |
| scan_result_i | int32 |  |  |
| standard_threat_name | string |  |  |
| start_time | date-time |  |  |
| sub_platform | string |  |  |
| total_avs | int32 |  |  |
| total_detected_avs | int32 |  |  |
| total_time | int32 |  |  |
| trust_factor | int32 |  |  |

400

Bad request

 Response
## Expression Search

Search for hashes using multi-part search criteria. The available search fields and expressions are described in the “Body (payload)” section below.

Endpoints[POST/threat-intel/search/](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#expression-search)
### Search for hashes

Search for hashes using multi-part search criteria.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |
| Content-Type | string | Specify the http content type *Allowed values - application/json* |  |

Request Body application/json

The JSON payload specifies the search terms and expressions. The limit value specifies how many hashes should be returned per page. The default and maximum value is 1000. Lower limit values might result in faster query executions.

| JSON payload for search | object | The supported wildcards match the behavior of * and ? on Unix-like systems:   - * matches any number of any characters including none - ? matches any single character   All search patterns are case-insensitive. The following search fields and expressions are allowed in the filters object:  **Text fields**   - Possible formats:   - string (using wildcards)   - array of strings (using wildcards) : matches any element - Field names:   - reputation   - risk_level   - file_info.file_type   - file_info.file_type_category   - file_info.file_type_extension   - platforms   - standard_threat_name   - malware_types   - malware_families   - malware_threat_names   **Numeric fields**   - Possible formats:   - scalar number (integer or floating point)   - array of numbers: matches any element   - object including comparison operators (matches all conditions if multiple operators are given):     - “gt”: Greater than (>)     - “gte”: Greater than or equal (>=)     - “lt”: Less than (<)     - “lte”: Less than or equal (<=)     - “eq”: Equal (=)     - “ne”: Not equal (!=) - Field names:   - reputation_i   - total_avs   - av_detection_count   - av_detection_percentage   - confidence_level   - file_info.file_size   **Timestamp fields**   - Possible formats:   - single timestamp in the ISO 8601 format: YYYY-MM-DDTHH:mm:ss.sssZ (or a date in the YYYY-MM-DD format)   - array of timestamps: matches any element   - object including comparison operators (same as for numeric fields) - Field names:   - first_seen   - last_seen   - update_timestamp |  |
| --- | --- | --- | --- |
| filters19 fields | object |  |  |
| reputation | string |  |  |
| risk_level | string |  |  |
| file_info.file_type | string |  |  |
| file_info.file_type_category | string |  |  |
| file_info.file_type_extension | string |  |  |
| platforms | string |  |  |
| standard_threat_name | string |  |  |
| malware_types | string |  |  |
| malware_families | string |  |  |
| malware_threat_names | string |  |  |
| reputation_i | int32 |  |  |
| total_avs | int32 |  |  |
| av_detection_count | int32 |  |  |
| av_detection_percentage | number |  |  |
| confidence_level | number |  |  |
| file_info.file_size | int32 |  |  |
| first_seen | date-time |  |  |
| last_seen | date-time |  |  |
| update_timestamp | date-time |  |  |
| limit | int32 | maximum: 1000 |  |

Expand POST /threat-intel/search/cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

OK

| Search response | object | The answer will include the fields that were included in the query. |  |
| --- | --- | --- | --- |
| items_on_current_page | int32 |  |  |
| has_next_page | boolean |  |  |
| continuation_token | string |  |  |
| data19 fields | array[object] |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| reputation | string | Enum: `benign`,`suspicious`,`malicious`,`unknown` |  |
| reputation_i | int32 |  |  |
| first_seen | date-time |  |  |
| last_seen | date-time |  |  |
| update_timestamp | date-time |  |  |
| file_info5 fields | object |  |  |
| file_size | int32 |  |  |
| file_type | string |  |  |
| file_type_category | string |  |  |
| file_type_description | string |  |  |
| file_type_extension | string |  |  |
| total_avs | int32 |  |  |
| av_detection_count | int32 |  |  |
| av_detection_percentage | number |  |  |
| confidence_level | number |  |  |
| risk_level | string | Enum: `low`,`medium`,`high` |  |
| standard_threat_name | string |  |  |
| malware_families | array[string] |  |  |
| malware_threat_names | array[string] |  |  |
| malware_types | array[string] |  |  |
| platforms | array[string] |  |  |

400

Bad request

 Response
## Similarity Search

Provides a list of similar files and similarity scores for SHA-256 hashes.

Endpoints[GET/threat-intel/similarity-search/{hash}](/docs/mdcloud/metadefender-cloud-threat-intelligence-api-v5#similarity-search)
### Search for similar files and scores

Retrieves the list of similar files and scores that have been previously scanned using Filescan, using SHA256.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user |  |
| --- | --- | --- | --- |
| verdict | string | Filescan verdict of a file. *Allowed values*   - *MALICIOUS (Filescan's determination of a file's MALICIOUS verdict).* - *LIKELY_MALICIOUS (Filescan's determination of a file's LIKELY_MALICIOUS verdict).* - *INFORMATIONAL (Filescan's determination of a file's INFORMATIONAL verdict).* - *SUSPICIOUS (Filescan's determination of a file's SUSPICIOUS verdict).* - *BENIGN (Filescan's determination of a file's BENIGN verdict).* - *UNKNOWN (Filescan's determination of a file's UNKNOWN verdict).* |  |
| start_date | string | Only return samples that were scanned after the start_date (inclusive). Date format ISO 8601. *Allowed values*   - *All valid ISO 8601 timestamps*. |  |
| tags | string | Tags of a file. *Allowed values*   - *The quantity of tags is continuously expanding.* - *Example (peexe, greyware, overlay, packed, shell32.dll, xml, meterpreter, swrort, adware, anti-debug, anti-security, anti-vm, apt, backdoor, banker, botnet, crimeware, fingerprint, greyware, exploit, evasive, hacktool, installer, keylogger, macros, macros-on-change, macros-on-close, macros-on-open, masquerade, obfuscated, overlay, packed, phishing, pos, pup, ransomware, rat, shellcode, spyware, stealer, stripped, vbastomped, worm, xlm, autoit, delphi, embedequation.).* |  |
| threshold | integer | Similarity threshold from 0% to 100%. Higher score means higher similarity. By default, it is (30). *Allowed values*   - *1 to 100 any integer* |  |
| limit | integer | Number of returned items. By default, it is (100). *Allowed values*   - *1 to 100 any integer* |  |

Expand Path Params

| hash | string | A hash is used to identify a file (MD5, SHA1 or SHA256) |  |
| --- | --- | --- | --- |

GET /threat-intel/similarity-search/{hash}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| SimilaritySearch response | object |  |  |
| --- | --- | --- | --- |
| data4 fields | array[object] |  |  |
| sha256 | string |  |  |
| overall_similarity | number |  |  |
| similarities11 fields | object |  |  |
| binary_metadata | number |  |  |
| version_info | number |  |  |
| pdb_guid | number |  |  |
| rich_header_compiler_ids | number |  |  |
| sections | number |  |  |
| resources | number |  |  |
| signal_ids | number |  |  |
| extracted | number |  |  |
| imports | number |  |  |
| certifications | number |  |  |
| weighted_numerics | number |  |  |
| details8 fields | object |  |  |
| start_date | date-time |  |  |
| tags | array[string] |  |  |
| items | string |  |  |
| is_dotnet | boolean |  |  |
| file_size | number |  |  |
| architecture | string |  |  |
| entropy | number |  |  |
| verdict | string |  |  |

400

Bad request

 Response
