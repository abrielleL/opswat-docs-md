<!-- source: https://www.opswat.com/docs/mdcloud/metadefender-cloud-api-v4/ref -->

## About This Guide

Welcome to the MetaDefender Cloud guide. This guide is intended to provide the information you need to:

## Start analyzing files with 30+ anti-malware engines

## How to use MetaDefender Cloud Public APIs

Learn about new features, updated features, and bug fixes
Learn about frequently asked questions and additional concepts through our library of knowledge base articles

## Key Features of MetaDefender Cloud

> ***File Analysis*** - Analyzing binaries with 30+ anti-malware engines

> ***Deep CDR*** (aka Content Disarm and Reconstruction) with support for 100+ file types

> ***Sandbox*** dynamic analysis to detect more unknown and targeted attacks

> ***Binary*** vulnerability data assessment

> ***IP-Domain reputation***

> ***Threat Intelligence Feeds***

Serverhttps://api.metadefender.com/v4Server Variables
## Apikey

The apikey and related limits can be found in the [account page](https://metadefender.opswat.com/account). It is generated automatically when the account is created.

The apikey is used for all API requests to MetaDefender Cloud service.

Endpoints[GET/apikey/](/docs/mdcloud/metadefender-cloud-api-v4#apikey-get) [GET/apikey/limits](/docs/mdcloud/metadefender-cloud-api-v4#apikey-limits) [GET/apikey/scan-history](/docs/mdcloud/metadefender-cloud-api-v4#getapikey-scan-history) [GET/apikey/limits/status](/docs/mdcloud/metadefender-cloud-api-v4#getapikey-remaining-limits)
### Apikey info

Retrieve information about your apikey such as (but not limited to): max file size, API limits, created date, expiration date, and account nickname.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user. |  |
| --- | --- | --- | --- |
| safe_redirect_options | integer | By default, it is disabled (0). If enabled (1), the safe_redirect_options lists are added to the response. |  |

GET /apikey/cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| Headers | | | | |
| --- | --- | --- | --- | --- |
| X-Authenticated | string | Indicates the source of authentication. |  |
| X-Response-Time | string | Indicates the response time expressed in milliseconds. |  |
| Body | | | | |
| Account Information | object |  |  |
| max_file_download | int32 | The maximum file size for downloading |  |
| max_upload_file_size | int32 | The maximum upload size for files (expressed in MB) |  |
| max_archive_file_depth | int32 | The maximum file depth for archives |  |
| max_archive_file_size | int32 | The maximum upload size for archives (expressed in MB) |  |
| max_archive_file_number | int32 | The maximum number of files contained in an archive |  |
| max_custom_workflows | int32 | The maximum number of custom workflows allowed for the apikey |  |
| limit_prevention | int32 | The daily limit of Prevention API calls. The daily limit is reset 24 hours after the first call on a given day. |  |
| limit_reputation | int32 | The daily limit of Reputation API calls. The daily limit is reset 24 hours after the first call on a given day. |  |
| limit_threat_intel_search | int32 | The daily limit of Threat Intel Search API calls. The daily limit is reset 24 hours after the first call on a given day. |  |
| limit_sandbox | int32 | The daily limit of Sandbox API calls. The daily limit is reset 24 hours after the first call on a given day. |  |
| limit_feed | int32 | The daily limit of Feed API calls. The daily limit is reset 24 hours after the first call on a given day. |  |
| mdc_license_type | string | The apikey's MetaDefender Cloud license type |  |
| qos_scan | string | The selected scan queue, based on the apikey type |  |
| userid | string | The userid corresponding to the apikey |  |
| sandbox_qos_scan | string | The selected sandbox scan queue, based on the apikey type |  |
| time_interval | string | The duration of time your apikey limit lasts for (daily for most)  Enum: `monthly`,`daily`  Default: daily |  |
| expiration_date | string | The expiration date of the apikey. For paid apikey's this date is in the future. |  |
| workflow_rule | int32 | The flag specifies if an apikey is allowed to scan large files or archives (1GB+), 0 = not allowed, 1 = allowed |  |
| enforce_private_scan | boolean | The attribute that specifies if the apikey enforces private scans |  |
| is_enterprise | boolean | The attribute that specifies if the apikey is enterprise |  |
| throttling_limit | int32 | The maximum number of requests for the duration of time your apikey lasts (one day for most) |  |
| mtls_only | boolean | The attribute that specifies if the apikey is MTLs only |  |
| portal_api_key | string | The apikey that has been queried |  |
| nickname | string | The nickname of the user correlated to the queried apikey |  |
| vulnerability_submissions | array[string] | The number of vulnerability submissions done by the user correlated to the queried apikey |  |
| created_at | string | The date when the apikey was created |  |
| updated_at | string | The last date when the apikey information was updated |  |
| scan_with | string | The service used by the apikey for scanning |  |
| ref_token | string | The reference token for the apikey |  |
| paid_user | int32 | Specifies the user's paid status. - 1: Paid user - 0: Not paid user |  |
| safe_redirect_options | object | The safe redirect lists for the apikey |  |
| organization20 fields | object | The organization information |  |
| organization_id | string | The unique identifier of the organization |  |
| limit_prevention | int32 | The organization's daily limit for Prevention API calls |  |
| limit_reputation | int32 | The organization's daily limit for Reputation API calls |  |
| limit_threat_intel_search | int32 | The organization's daily limit for Threat Intel Search API calls |  |
| limit_sandbox | int32 | The organization's daily limit for Sandbox API calls |  |
| limit_feed | int32 | The organization's daily limit for Feed API calls |  |
| throttling_limit | int32 | The organization's request throttling limit |  |
| ip_whitelist | object |  |  |
| v4 | array[string] | IPv4 whitelist |  |
| v6 | array[string] | IPv6 whitelist |  |
| expiration_date | date-time | The organization's license expiration date |  |
| enforce_private_scan | boolean | The attribute that specifies if the organization enforces private scans |  |
| licenseLimitsTimeInterval | string | The duration of time your organization limit lasts for (daily for most)  Enum: `monthly`,`daily`  Default: daily |  |
| mdc_license_type | string | The organization's MetaDefender Cloud license type |  |
| max_upload_file_size | int32 | Maximum file upload size for the organization (MB) |  |
| max_archive_file_size | int32 | Maximum archive file size for the organization (MB) |  |
| max_archive_file_number | int32 | Maximum number of files in archives for the organization |  |
| max_archive_file_depth | int32 | Maximum archive depth for the organization |  |
| max_custom_workflows | int32 | Maximum number of custom workflows for the organization |  |
| qos_scan | string | The selected scan queue, based on the organization's license type |  |
| sandbox_qos_scan | string | The selected sandbox scan queue, based on the organization's license type |  |
| safe_redirect_options | object | The safe redirect lists for the organization |  |

Expand 404

The requested page was not found

 Response
### Apikey limits

Retrieve information about the consumed limits for an apikey. Every time a request is made to an endpoint that consumes a specific limit, it will be reflected in this endpoint. It is the equivalent of the X-RateLimit-Used from the response headers. Depending on your license, your rate limit will reset daily or monthly.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user. |  |
| --- | --- | --- | --- |

GET /apikey/limitscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| Headers | | | | |
| --- | --- | --- | --- | --- |
| X-Authenticated | string | Indicates the source of authentication. |  |
| X-Response-Time | string | Indicates the response time expressed in milliseconds. |  |
| Body | | | | |
| Apikey usage | object |  |  |
| reputation_api | int32 | The consumed Reputation API limits for the apikey |  |
| threat_intel_search_api | int32 | The consumed Threat Intel Search API limits for the apikey |  |
| prevention_api | int32 | The consumed Prevention API limits for the apikey |  |
| feed_api | int32 | The consumed Feed API limits for the apikey |  |
| download_file | int32 | The consumed limits for file downloads for the apikey |  |
| sandbox_api | int32 | The consumed Dynamic Analysis API limits for the apikey |  |

404

The requested page was not found

 Response
### Apikey scan history

Retrieve a paginated list of files uploaded by the user in reverse chronological order (newest to oldest). The pagination is controlled by the user (how many items per page and which page) by specifying the limit and offset query parameters in the request. The response only contains a summary of the files, with minimum information.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user. |  |
| --- | --- | --- | --- |

Query String

| limit | integer | Pagination - how many entries you want to return. |  |
| --- | --- | --- | --- |
| offset | integer | Pagination - how many entries to skip (sorted chronologically). |  |
| cursor | string | Utilize a string-based cursor for efficient pagination in database queries. This approach enhances performance and should be used in place of the traditional offset parameter. |  |
| search | string | An optional search term to filter results by hash or file display name. Supports the * wildcard for flexible matching. |  |
| start_date | string | Start date for the scan history is in ISO 8601 format (e.g., YYYY-MM-DDTHH:MM:SSZ). |  |
| end_date | string | End date for the scan history is in ISO 8601 format (e.g., YYYY-MM-DDTHH:MM:SSZ). |  |
| sort_by | string | Sort field. |  |
| sort_dir | string | Sort direction.  Enum: `asc`,`desc` |  |
| status | string | Status of the scan history.  Enum: `Allowed`,`Blocked` |  |

GET /apikey/scan-historycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| Scan history | object |  |  |
| --- | --- | --- | --- |
| data10 fields | array[object] | Scan History |  |
| data_id | string | The unique id received by the API for a submitted file |  |
| process_info | object | Information about the analysis process |  |
| progress_percentage | int32 | The progress percentage of the analysis process |  |
| file_info5 fields | object | Information about the file |  |
| md5 | string | The MD5 hash corresponding to the file scanned |  |
| sha1 | string | The SHA1 hash corresponding to the file scanned |  |
| sha256 | string | The SHA256 hash corresponding to the file scanned |  |
| display_name | string | The display name of the file |  |
| file_type_extension | string | The file extension |  |
| scan_results4 fields | object | Scan result |  |
| total_detected_avs | int32 | The number of AVs that detected a threat |  |
| total_avs | int32 | The number of AVs used by the API |  |
| scan_all_result_i | int32 | The flag that specifies if the submitted file is infected |  |
| start_time | string | The date when the scan started |  |
| scan_with | string | The service used by the apikey for scanning |  |
| dlp_info | object | Contains the verdict from Proactive DLP |  |
| verdict | integer | The overall result for the scanned file. Possible values:   - 0 - Clean - 1 - Found matched data - 2 - Suspicious - 3 - Failed - 4 - Not scanned   Enum: `0`,`1`,`2`,`3`,`4` |  |
| sanitized4 fields | object | Represents the sanitization information of an item. |  |
| reason | string | The reason or explanation for the sanitization. |  |
| result | string | The result or outcome of the sanitization process. |  |
| progress_percentage | integer | The progress percentage of the sanitized file. |  |
| failure_reasons1 field | object | The object wrapping the list of files in the archive for which sanitization failed. |  |
| data_id4 fields | object | Sanitization failure reason for file |  |
| display_name | string | The name of the offending file. |  |
| file_path | string | Path to reach the file |  |
| reason | string | Description of the sanitization error |  |
| details | string | Additional details on the sanitization error |  |
| sandbox4 fields | object | Sandbox scan final verdict |  |
| verdict | string | The overall result for the scanned file.  Enum: `UNKNOWN`,`BENIGN`,`NO_THREAT`,`SUSPICIOUS`,`LIKELY_MALICIOUS`,`MALICIOUS` |  |
| threatLevel | number | The infection score indicating the severity of the detected threats. |  |
| confidence | integer | The confidence score when determining the severity of the detected threats. |  |
| blocked | boolean | The indicator whether the file is blocked. |  |
| vulnerability | object | The highest vulnerability based on the CVEs associated with the file |  |
| severity_index | integer | A numerical representation of the severity of the vulnerability |  |
| severity | integer | A textual representation of the severity index of the vulnerability  Enum: `LOW`,`MODERATE`,`IMPORTANT`,`CRITICAL` |  |
| nextCursor | string | A string-based cursor used to retrieve the next page of results, replacing the traditional offset parameter. This parameter is available only on the last element within the results array. |  |

404

The requested page was not found

 Response
### Apikey remaining limits

Retrieve information about the remaining limits for an apikey.

Auth NoneHeaders

| apikey | string | The apikey identifies and authenticates the user. |  |
| --- | --- | --- | --- |

GET /apikey/limits/statuscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json; charset=utf-8 200

The request has succeeded

| Apikey usage | object |  |  |
| --- | --- | --- | --- |
| reputation_api | int32 | The remaining Reputation API limits for the apikey |  |
| threat_intel_search_api | int32 | The remaining Threat Intel Search API limits for the apikey |  |
| prevention_api | int32 | The remaining Prevention API limits for the apikey |  |
| feed_api | int32 | The remaining Feed API limits for the apikey |  |
| download_file | int32 | The remaining limits for file downloads for the apikey |  |
| sandbox_api | int32 | The remaining Dynamic Analysis API limits for the apikey |  |
| throttling_limit | int32 | The remaining Throttling limits for the apikey |  |

404

The requested page was not found

 Response
## File Scanning

Scanning a file starts with uploading the file to MetaDefender Cloud to initiate the scan process. Although we are trying to keep scanning very fast, scanning with more than 30 engines might take from a few seconds to many minutes depending on file type, file size, and current traffic. Also, archives usually take longer when scanning all the files inside. Due to these variables, we are not able to guarantee scanning times.

Free API users are sent to different queues with a lower priority, and MetaDefender Cloud customers' scan requests are prioritized.

Scanning a file consists of the following steps:

1. Initiate scan request by uploading a file
2. Retrieve scan report using unique data_id returned from Scan File API

Notes:

- When both the multiscan and sandbox functionalities are concurrently operational, and specific rate limits have been established for the sandbox, while none exist for multiscan, rather than generating an error, the sandbox process will be executed. Consequently, the associated data_id will return a status code of 253, denoting 'Not Scanned. Rate Limit Exceeded,' within the scan results.
Endpoints[POST/file](/docs/mdcloud/metadefender-cloud-api-v4#file-upload) [GET/file/webhooks/{dataId}](/docs/mdcloud/metadefender-cloud-api-v4#getretrieving-webhook-status) [GET/file/{dataId}](/docs/mdcloud/metadefender-cloud-api-v4#file-lookupbydataid) [POST/repo](/docs/mdcloud/metadefender-cloud-api-v4#repo-scan) [POST/dataIdBulkLookup](/docs/mdcloud/metadefender-cloud-api-v4#dataids-bulklookup) Show 
## Hash Lookups

MetaDefender provides two basic ways of looking up scan results using data hashes, MD5, SHA1, and SHA256:

1. Single hash lookup
2. Multiple hash lookup

   While single hash lookup provides full scan results related to the hash,
   if found, multiple hash lookup will return a list of condensed results with
   links (data_ids) to the full scan results.
Endpoints[GET/hash/{hash}](/docs/mdcloud/metadefender-cloud-api-v4#hash-lookup) [POST/hash](/docs/mdcloud/metadefender-cloud-api-v4#hash-bulklookup) [GET/hash/{hash}/scanhistory](/docs/mdcloud/metadefender-cloud-api-v4#hash-scanhistory) [GET/hash/{hash}/badge](/docs/mdcloud/metadefender-cloud-api-v4#hash-badge) Show 
## Reputation Service

MetaDefender Cloud allows users to check IP addresses, domains, and URLs for malicious behavior using multiple IP & URL reputation sources. This functionality makes it possible to identify threats like botnets that would not be found through scanning files when accessing content. By providing a standardized interface for leading IP & URL reputation sources, MetaDefender Cloud makes it possible to obtain aggregated data on whether an IP address, domain or URL should be trusted, enabling you to monitor your network for possible threats.

MetaDefender Cloud provides two basic ways of verifying reputation for each type:

1. Single scan (Scanning IP / Domain / URL)
2. Bulk scans (Scanning list of IPs / Domains / URLs)
Endpoints[GET/ip/{observable_ip}](/docs/mdcloud/metadefender-cloud-api-v4#ip-lookup) [POST/ip/](/docs/mdcloud/metadefender-cloud-api-v4#ip-bulklookup) [GET/url/{observable_url}](/docs/mdcloud/metadefender-cloud-api-v4#url-lookup) [POST/url/](/docs/mdcloud/metadefender-cloud-api-v4#url-bulklookup) [GET/domain/{observable_domain}](/docs/mdcloud/metadefender-cloud-api-v4#domain-lookup) [POST/domain/](/docs/mdcloud/metadefender-cloud-api-v4#domain-bulklookup) Show 
## Application Information

MetaDefender Cloud allows users to leverage our threat intelligence platform by providing an extensive REST API. The **unique data set** shared through our platform is collected from **millions of live machines**. This data set offers you tremendous insights on the behavior of potential malware, in order of weeks, from endpoints used in live environments by real users. This real-time information is more valuable than information from a sandbox solution, where everything is running in a controlled and simulated environment for approximately 3 minutes.

Through our API, you will be able to retrieve all the applications that the searched hash belongs to, all the network connections made by those applications, and the other loaded components that are used by those applications. You will be able to identify, restrict, or grant access based on the correlations provided.

Endpoints[GET/hash/{exif_hash}/exif](/docs/mdcloud/metadefender-cloud-api-v4#hash-exif) [GET/hash/{peinfo_hash}/peinfo](/docs/mdcloud/metadefender-cloud-api-v4#hash-peinfo) [GET/hash/{apk_hash}/apk-manifest](/docs/mdcloud/metadefender-cloud-api-v4#hash-apkmanifest) Show 
## Data Sanitization Cdr

MetaDefender Cloud allows users to leverage our [Deep CDR (Content Disarm and Reconstruction) technology](https://www.opswat.com/products/metadefender/workflow-engine?__hstc=126361682.95764283e70d2ab6b1ea977785ef0074.1503490400344.1504248455458.1504269918167.15&__hssc=126361682.1.1504269918167&__hsfp=3138280023) by providing an extensive REST API.

Through our API, you will be able to use data sanitization (CDR) to strip out embedded objects in document files. Some targeted attacks may not be detected by traditional anti-malware engines, which is why data sanitization should be performed on document files. The CDR process provides an extra level of insurance against zero-day attacks without affecting the usability of the files. MetaDefender Cloud leverages the MetaDefender Core Deep CDR engine.

Endpoints[GET/file/converted/{dataId}](/docs/mdcloud/metadefender-cloud-api-v4#file-sanitized) [DELETE/file/converted/{dataId}](/docs/mdcloud/metadefender-cloud-api-v4#deletedelete-the-sanitized-version-of-the-file) Show 
## Malware Sample Sharing

The endpoints part of malware sharing program are designed to expose the latest malware identified by OPSWAT, both infected files, and possible false positives.

---

*These endpoints are only available to OPSWAT partners participating in the malware exchange program. If you are an antivirus vendor, or have a malware feed and want to participate in the program, please contact us at [malware-sharing@opswat.com](mailto:malware-sharing@opswat.com).*

---

The lists expose information like the hashes of the files, the engines which detected the file and the download link, so it is easy to parse the feed and identify interesting hashes before starting the download.

MetaDefender Cloud does not store the files in archives separate. So it might be the case that a downloaded file has a different hash than specified in the URL. In this case, the hash can be found inside the archive.

The feed is generated once per day. At the moment, only the current day can be accessed.

Endpoints[GET/feed/hashes](/docs/mdcloud/metadefender-cloud-api-v4#feed-hashes) [GET/feed/false-positives](/docs/mdcloud/metadefender-cloud-api-v4#feed-falsepositives) [GET/feed/false-positives/{engine}](/docs/mdcloud/metadefender-cloud-api-v4#feed-falsepositivesbyengine) [GET/file/{hash}/download](/docs/mdcloud/metadefender-cloud-api-v4#file-downloadlink) Show 
## Threat Intelligence Feed

OPSWAT's threat intelligence feed enables developers to leverage data collected from thousands of MetaDefender Cloud community users and customers. Developers, IT administrators and organizations can easily integrate our up-to-date malware threat intelligence data into their existing tools or solutions to effectively protect their organization against threats.

Use cases for the feed include:

- Organizations that want to be on the lookout for the hottest malware
- IT specialists that implement file denylist based on hashes
- Researchers analyzing trending malware on the market
- Security products that leverage threat intelligence capabilities to
  harden security measures
Endpoints[GET/feed/clean/latest](/docs/mdcloud/metadefender-cloud-api-v4#feed-latestcleanhashes) [GET/feed/infected/latest](/docs/mdcloud/metadefender-cloud-api-v4#feed-latestinfectedhashes) Show 
## Status Endpoints

Various endpoints for querying MetaDefender Cloud.

Endpoints[GET/status/version](/docs/mdcloud/metadefender-cloud-api-v4#status-version) [GET/status/maintenance](/docs/mdcloud/metadefender-cloud-api-v4#status-maintenance-get) [GET/status/enginedef](/docs/mdcloud/metadefender-cloud-api-v4#status-enginedef) Show 
## Dynamic Analysis

API calls for dynamic analysis. General information can be found here: [Dynamic analysis](https://docs.opswat.com/mdcloud/operation/dynamic-analysis)

Endpoints[POST/sandbox](/docs/mdcloud/metadefender-cloud-api-v4#sandbox-url-scan) [GET/sandbox/{sandbox_id}](/docs/mdcloud/metadefender-cloud-api-v4#sandbox-lookup) [GET/hash/{sandbox_hash}/sandbox](/docs/mdcloud/metadefender-cloud-api-v4#hash-sandbox) Show
