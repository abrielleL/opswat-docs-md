<!-- source: https://www.opswat.com/docs/mdcluster/api-gateway/ref -->

## Developer Guide

---

This is the API documentation for *MetaDefender Cluster API Gateway Public API*. If you
would like to evaluate or have any questions about this documentation,
please contact us via our [Contact Us](https://www.opswat.com/contact) form.

---

## How to Interact with MetaDefender Cluster API Gateway using REST API

MetaDefender Cluster API Gateway is used to submit files for analysis, retrieve scan results,
manage file processing, download processed files, and manage file batches.
OPSWAT recommends using the JSON-based REST API. The available methods are documented below.

> ***Note**:* MetaDefender Cluster API doesn't support chunk upload, however is
> recommended to stream the files to MetaDefender Cluster API Gateway as part of the upload
> process.

---

## File Analysis Process

MetaDefender Cluster is a system with multiple components that work together to utilize the power of multiple MetaDefender Core instances.
The system is designed to handle large volumes of files and provide high throughput for file analysis. The system can be deployed in a distributed manner, allowing for horizontal scaling and load balancing across multiple MetaDefender Core instances.

Below is a brief description of the API integration flow:

1. Upload a file for analysis to MetaDefender Cluster API Gateway (`POST /file`), which returns the `data_id`: [File Analysis](/docs/mdcore/metadefender-distributed-cluster/ref#fileanalysispost).
2. The following method can be used to retrieve the analysis report:

   - **Polling**: Fetch the result with previously received data_id (`GET /file/{data_id}` resource) until scan result belonging to data_id doesn't reach the 100 percent progress_percentage: ([Fetch analysis result](/docs/mdcore/metadefender-distributed-cluster/ref#fileanalysisget))
   > ***Note**:* Too many data_id requests can reduce performance. It is enough to just check every few hundred milliseconds.
3. Retrieve the analysis results anytime after the analysis is completed with hash for files (md5, sha1, sha256, sha512) by calling [Fetch analysis result by hash](/docs/mdcore/metadefender-distributed-cluster/ref#hashget).

   - The hash can be found in the scan results
4. Retrieve processed file (sanitized, redacted, watermarked, etc.) after the analysis is complete.

   > ***Note**:* Based on the configured retention policy, the files might be available for retrieval at a later time.

---

OPSWAT provides some sample codes on [GitHub](https://github.com/OPSWAT) to
make it easier to understand how the MetaDefender REST API works.

Serverhttp://localhost:8899Server Variables## AuthenticationapiKey apikey

Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication.

Fields

| Key | In |
| --- | --- |
| apikey | Header |  |

## Auth

### Authentication APIs

User authentication is done via username & password.

Endpoints[POST/login](/docs/mdcluster/api-gateway#userlogin) [POST/logout](/docs/mdcluster/api-gateway#userlogout)
### Login

Initiate a new session. Required for using protected REST APIs.

Auth NoneRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| user | string | Username |  |
| password | string | User's password |  |

POST /logincURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| oms-csrf-token | string | The randomly generated token used to prevent CSRF attacks |  |
| session_id | string | The apikey used to make API calls which requires authentication |  |

403

Invalid credentials

500

Unexpected event on server.

 Response
### Logout

Destroy session for not using protected REST APIs.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

POST /logoutcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| response | string |  |  |

400

Bad Request.

403

Invalid user information.

500

Unexpected event on server.

 Response
## Analysis

### File analysis APIs

Submit each file to MetaDefender Cluster API Gateway individually or group them in batches. Each file submission will return a `data_id` which will be the unique identifier used to retrieve the analysis results.

> ***Note**:* MetaDefender API doesn't support chunk upload. You shouldn't load the file in memory, is recommended to stream the files to MetaDefender Cluster API Gateway as part of the upload process.

Endpoints[POST/file](/docs/mdcluster/api-gateway#fileanalysispost) [GET/file/{data_id}](/docs/mdcluster/api-gateway#fileanalysisget) [GET/hash/{md5|sha1|sha256|sha512}](/docs/mdcluster/api-gateway#hashget) [GET/hash/{md5|sha1|sha256|sha512}/blocked-leaves](/docs/mdcluster/api-gateway#retrieveblockedleaffilebyhash) [GET/file/rules](/docs/mdcluster/api-gateway#analysisrules) [GET/file/converted/{data_id}](/docs/mdcluster/api-gateway#sanitizedfile) [GET/file/download/{data_id}](/docs/mdcluster/api-gateway#downloadfile) [POST/file/{data_id}/cancel](/docs/mdcluster/api-gateway#fileanalysiscancel) [GET/file/{data_id}/blocked-leaves](/docs/mdcluster/api-gateway#retrieveblockedleaffile) [GET/file/{data_id}/extraction-errors](/docs/mdcluster/api-gateway#retrieveextractionerrors) [GET/file/webhook/{data_id}](/docs/mdcluster/api-gateway#webhookstatus)
### Analyze File (Asynchronous mode)

**Scanning a file using a specified workflow.**
Scan is done asynchronously and each scan request is tracked by data id of which result can be retrieved by API Fetch Scan Result.

> ***Note***: Chunked transfer encoding (applying header Transfer-Encoding: Chunked) is **not supported** on `/file` API. API Gateway **only accepts** file uploads with a known content length and a content type of `application/octet-stream`

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| filename | string | The name of the submitted file |  |
| user_agent | string | user_agent header used to identify (and limit) access to a particular rule. For rule selection, `rule` header should be used. |  |
| rule | string | Select rule for the analysis, if no header given the default rule will be selected (URL encoded UTF-8 string of rule name) |  |
| batch | string | Batch id to scan with, coming from `Initiate Batch` (If it is not given, it will be a single file scan.) |  |
| archivepwd | string | Password for archive ( URL encoded UTF-8 string) Multiple passwords is also supported, format: archivepwdX   - X: Could be empty - When having value, X must be a number >= 1   For example:   - archivepwd1: "fox" - archivepwd2: "cow" - archivepwd3: "bear" |  |
| content-encoding | string | Content encoding of the file. This header is used to specify the encoding of the file content. The value should be a valid content encoding type, such as "base64", "gzip". This header is optional and can be omitted if the encoding is not applicable. |  |
| metadata | string | Could be utilized for:   - Additional parameter for pre-defined post actions and external scanners   (as a part of STDIN input). - Customized macro variable for watermarking text (Proactive DLP engine   feature). - Additional context / verbose information for each file submission   (appended into JSON response scan result).   It is strongly recommended to apply URL encoding before sending `metadata` to Metadefender Core to prevent unexpected issues related to encoding errors or unsafe characters. |  |
| engines-metadata | string | Since MetaDefender Core 5.0.0, preferred context / verbose information can be sent to the engines.  Please see the below pages for the details:   - [File Type engine](https://docs.opswat.com/mdcore/utilities-engines/supported-engines-metadata) (supported since Core 5.2.1) - [Archive engine](https://docs.opswat.com/mdcore/utilities-engines/supported-engines-metadata-header) (supported since Core 5.4.1) - [Deep CDR](https://docs.opswat.com/mdcore/deep-cdr/supported-engines-metadata-json) - [Proactive DLP](https://docs.opswat.com/mdcore/proactive-dlp/supported-engines-metadata-json) |  |
| callbackurl | string | Client's URL where MetaDefender Cluster Callback Service will notify scan result back to whenever scan is finished (webhook model). * Format: <protocol://><ip | domain>: * Example: <http://10.0.1.100:8081/listenback> * Supported protocol: HTTP / HTTPS * Supported host types: domain name, IPv4 (IPv6 not supported) * Method: POST  ***Note***: The Callback URL is only supported when MetaDefender Cluster Callback Service is deployed, and MetaDefender Core version must be 5.16.1 or higher. |  |
| downloadfrom | string | Format: <protocol://><ip | domain>:<port></path>  Scan a file from a download link, instead of uploading the file in the request body. MetaDefender Cluster Download Service downloads the file from the link, then sends it for scanning.  ***Note***: To use this header, you need:   - MetaDefender Cluster Download Service deployed. - MetaDefender Cluster version 2.10.0 or later. - MetaDefender Core version 5.23.0 or later.   If no Download Service instance is available, the request fails with HTTP 503.  How it works:   - Do not send a request body. `Content-Length` must be `0` or not set. If you send a body, the request fails with HTTP 400. - The response returns a `data_id` right away. The download continues in the background. - To see the download progress and result, check `download_info` in [Fetch Analysis Result](/docs/mdcore/metadefender-distributed-cluster/ref#fileanalysisget). - If you do not set the `filename` header, the file name is the last part of the link path.   Supported:   - Protocols: HTTP and HTTPS. - Single file scan, with or without webhook. - Batch scan: add the `downloadfrom` header to each file request in the batch. The batch request itself needs nothing extra.   - If you cancel the batch, all files in the batch that are still downloading are also cancelled. - Settings in the workflow ("General" tab):   - Max sizes > URL file download   - Timeouts > File download - Settings in Settings > Scan From Link:   - Max download queue: the number of downloads that run at once. Other links wait their turn.   - Idle timeout: a download fails if it receives no data for this long.   - Enforce scan from link validation: allow or block links that match the given patterns. - Size check before download: MetaDefender Cluster sends an HTTP `HEAD` request to the link.   If the file is larger than the max URL file download size or the max file scan size, the download is refused.   To skip this check, use the `skip-head-request` header. |  |
| redirect-support | boolean | Use only with the `downloadfrom` header.  Follow redirects of the download link.   - Default: `false`. If the link redirects, the request fails with HTTP 400 (`Redirect link not supported.`). - `true`: Follow up to 5 redirects.   Default: false |  |
| skip-head-request | boolean | Use only with the `downloadfrom` header.  Skip the HTTP `HEAD` request that checks the file size before the download. Use it when the download server does not support `HEAD` requests.   - Default: `false`. Send the `HEAD` request first, then download. - `true`: Download the file directly. The size limits are still checked during the download.   Default: false |  |
| global-timeout | integer | This custom global timeout (in seconds) will override the global timeout predefined in corresponding workflow rule. |  |
| client-identity | string | The `client-identity` header identifies the clients involved in processing a file, providing greater visibility into its processing stages. The header value is a JSON object containing a clients array. Each `client` object supports the following fields:   - `deployment_id`: *REQUIRED*. Unique identifier of the deployment. - `user_name`: *REQUIRED*. Name of the user or system that initiated the scan. - `product_type`: *REQUIRED*. Type of product or system performing the scan. - `version`: *OPTIONAL*. Version of the product or system. - `host`: *OPTIONAL*. Hostname or IP address of the client machine. - `timestamp`: *REQUIRED*. Time at which the scan was initiated, expressed in milliseconds since the Unix epoch.   Example:   ```   {   "clients":    [   {     "deployment_id": "abcdef1234567890",     "user_name": "Gemini",     "product_type": "MetaDefender Kiosk",     "version": "1.0.0",     "host": "client.example.com",     "timestamp": 1744949754890   }   ]   }   ```   URL-encode the JSON value before sending the header to MetaDefender Cluster to avoid issues caused by unsafe characters or incorrect encoding. Omit the header when client identity tracking is not required. |  |

Expand Request Body application/octet-stream

| file | file |  |  |
| --- | --- | --- | --- |

POST /filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful file submission

| object | object |  |  |
| --- | --- | --- | --- |
| data_id | string | Unique submission identifier. Use this value to reference the submission. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or
out of range, etc). The request is rejected before the file is processed, so no `data_id` is
created.

When the `client-identity` header is present but its value is invalid, `err` is one of:

| `err` | Cause |
| --- | --- |
| `Header 'client-identity' is empty` | The header was sent without a value. |
| `Header 'client-identity' must be less than or equal 4096 characters` | The header value is longer than 4096 characters. |
| `Header 'client-identity' contains non-printable character` | The value contains an ASCII control character, either directly or through an escape. |
| `Header 'client-identity' is not in JSON format` | The value could not be URL-decoded, is not valid JSON, or is not a JSON object. |
| `Header 'client-identity' does not contain a 'clients' key or empty 'clients'` | `clients` is missing, is not an array, or is an empty array. |
| `Header 'client-identity' contains an invalid data` | An entry of `clients` is not a JSON object. |
| `Header 'client-identity' does not contain required key '<key>'` | An entry is missing `deployment_id`, `user_name`, `product_type` or `timestamp`. |
| `Header 'client-identity' contains a non-string '<key>'` | `deployment_id`, `user_name` or `product_type` is not a string. |
| `Header 'client-identity' contains an empty '<key>'` | `deployment_id`, `user_name` or `product_type` is blank. |
| `Header 'client-identity' contains an invalid 'deployment_id'` | `deployment_id` holds anything other than letters and digits. |
| `Header 'client-identity' contains a non-integer 'timestamp'` | `timestamp` is not an integer. |
| `Header 'client-identity' contains a negative 'timestamp'` | `timestamp` is zero or negative. |

Every entry of `clients` is checked, not only the first one, and the first rule that fails is the
one reported.

403

Invalid user information or Not Allowed

411

Content-Length header is missing from the request.

422

Body input is empty.

500

Unexpected event on server.

503

Service is unavailable, `err` is one of:

- `Server is too busy. Try again later.`
- `Failed to request because no MetaDefender Cluster Download Service instance is available` - the `downloadfrom` header was given but no Download Service instance is healthy.
 Response
### Fetch Analysis Result

Retrieve scan results.

Scan is done asynchronously and each scan request is tracked by a data ID.

Initiating file scans and retrieving the results need to be done using two separate API calls.
This request needs to be made multiple times until the scan is complete.
Scan completion can be traced using `scan_results.progress_percentage` value from the response.

> ***Note**:* The REST API also supports pagination for archive file result. A completed response description with archive detection:
>
> - extracted_files: information about extracted files
>   - files_extracted_count: the number of extracted files
>   - files_in_archive: array of files in archive
>     - detected_by: number of engines reported threat
>     - scanned_with: number of engines used for scanning the file
>   - first_index: it tells that from which file (index of the file, 0 is the first) the result JSON contains information about extracted files. (default=0, min=0)
>   - page_size: it tells how many files the result JSON contains information about (default=50, min=0, max=2000). So by default, the result JSON contains information about the first 50 extracted files.
>   - worst_data_id: data id of the file that has the worst result in the archive
>   - total_reused_files: Indicates how many extracted files reused results from a previous analysis instead of being processed again. This field is available starting with MetaDefender Cluster 2.10.0. A value of `0` means no extracted files were reused. If the entire archive is reused, `original_data_id` is set and `files_in_archive` is empty, while the archive totals are still included in the response.
> - scan_results
>   - last_file_scanned (stored only in memory, not in database): If available, the name of the most recent processed file

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| user_agent | string | user_agent header used to identify (and limit) access to a particular rule. For rule selection, `rule` header should be used. |  |

Path Params

| data_id | string | Unique submission identifier. Use this value to reference the submission. |  |
| --- | --- | --- | --- |

Query String

| first | integer | The `first` item order in the list child files of archive file  minimum: 0  Default: 0 |  |
| --- | --- | --- | --- |
| size | integer | The number of items to be fetched next, counting from the item order indicated in `first` header. The default value is 50, and the maximum value is 2000.  maximum: 2000  minimum: 0  Default: 50 |  |

GET /file/{data_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Entire analysis report generated by MetaDefender Core

| object | object |  |  |
| --- | --- | --- | --- |
| data_id | string | data identifier of the requested file |  |
| deflected_engines | array[string] | Engines skipped (deflected) for this file based on the OPSWAT Alin AI Deflection verdict (available starting with MetaDefender Cluster 2.10.0). Returned only when at least one engine was deflected. Each item is an engine identifier, e.g. `extraction`, `metascan`, `ds`, `oesis`, `dlp`, `yara`, `filescanio`, `sbom`, `coo`, `reputation`, `ti`, `aigcd`, `fsv`. |  |
| deflection_info5 fields | object | Report from the OPSWAT Alin AI Deflection engine (available starting with MetaDefender Cluster 2.10.0). Deflection produces an early verdict on a file that can be used to skip (deflect) other engines in the workflow. The object is empty when Deflection did not run on the file. |  |
| final_verdict3 fields | object | Overall Deflection verdict and supporting details. |  |
| verdict | string | Deflection engine verdict. Values:   - clean: the file is considered clean. - malicious: the file is considered malicious. - unknown: the engine could not confidently classify the file. - Cancelled: processing was cancelled before a verdict was produced.   Enum: `clean`,`malicious`,`unknown`,`Cancelled` |  |
| confidence | integer | Confidence of the verdict, as a percentage (0-100).  maximum: 100  minimum: 0 |  |
| detail | object | Additional details about the analyzed file. |  |
| data_id | string | data identifier of the analyzed file. |  |
| file_type | string | Detected file type of the analyzed file. |  |
| result_template_hash | string | Hash of the result template used internally for Deflection rendering and coordination. |  |
| err_code | integer | Returned only when Deflection failed to produce a verdict (`final_verdict` is then absent). Common values:   - 1: Deflection failed. - 5: Deflection timed out. - 6: The file type is not supported by Deflection. - 9: The global processing timeout was exceeded. |  |
| err_details | string | Returned only when Deflection failed. Human-readable reason of the failure. |  |
| err_category | string | Returned only when Deflection failed and the engine reported a failure category. |  |
| dlp_info9 fields | object | Full report from Proactive DLP |  |
| certainty | string | Describes how certain the hit is, possible values:   - `Very Low` - `Low` - `Medium` - `High` - `Very High`   Enum: `Very Low`,`Low`,`Medium`,`High`,`Very High` |  |
| errors | object | A list of error objects (empty if no errors happened), each error object contains following keys:   - `scan`: scan related error description - `redact`: redaction related error description - `watermark`: watermark related error description - `metadata_removal`: metadata removal related error description |  |
| filename | string | Output processed file name (pre-configured on engine settings under Core's worflow rule) |  |
| hits1 field | object | Detailed results that contains as key the type of matched rule:   - ccn (credit card number), - ssn (social security number), - regex_ (regular expression with an index in order to differentiate the RegEx rules if there are more.) |  |
| ccn2 fields | object |  |  |
| display_name | string | Credit Card Number, Social Security Number, or in case of RegEx, the name of the rule that has been given by the user |  |
| hits | array[object] | A list of detections that matched this rule/pattern. |  |
| after | string | The context after the matched data. |  |
| before | string | The context before the matched data. |  |
| certainty | string | The text version of "certainty_score", possible values:   - `Very Low` - `Low` - `Medium` - `High` - `Very High`   Enum: `Very Low`,`Low`,`Medium`,`High`,`Very High` |  |
| certainty_score | integer | Is defined by the relevance of the given hit in its context. It is calculated based on multiple factors such as the number of digits, possible values: [0-100] |  |
| hit | string | The matched data. |  |
| location | string | The location of the hit that is found in a file. |  |
| severity | integer | (NOTE: this field is deprecated): can be 0 (detected) or 1 (suspicious).  Enum: `0`,`1` |  |
| tryRedact | boolean | If file was redacted or not. |  |
| metadata_removal | object | Result of metadata removal. |  |
| result | string | Result of the metadata removal process, possible values:   - `removed` - `not removed` - `failed to remove`   Enum: `removed`,`not removed`,`failed to remove` |  |
| redact | object | Result of redaction process. |  |
| result | string | Result of the redaction process, possible values:   - `redacted` - `not redacted` - `failed to redact`   Enum: `redacted`,`not redacted`,`failed to redact` |  |
| severity | integer | (NOTE: this field is deprecated): represents the severity of the data loss, possible values:   - `0` - Certainly is data loss - `1` - Might be data loss   Enum: `0`,`1` |  |
| verdict | integer | The overall result for the scanned file. Possible values:   - `0` - Clean - `1` - Found matched data - `2` - Suspicious - `3` - Failed - `4` - Not scanned   Enum: `0`,`1`,`2`,`3`,`4` |  |
| watermark | object | Result of watermarking process. |  |
| result | string | Result of the watermarking process, possible values:   - `added` - `not added` - `failed to add`   Enum: `added`,`not added`,`failed to add` |  |
| download_info5 fields | object | The downloading status. Only present when the file was submitted with the `downloadfrom` header (scan from link), in which case MetaDefender Cluster Download Service downloads the file before it is scanned. |  |
| error_detail | string | Revealed detailed reason why the download failed. Only present when the download did not succeed. |  |
| progress | number | Only applicable when "status" is `Downloading`, indicates download finished percentage, in a range of [0, 99].   - Once hitting 100, the status will be changed to `Download Success`. - or other problematic status (`Download Cancelled`, `Download Failed`, `Download Timeout`) if the download stopped unexpectedly. - Stays at 0 when the download server does not declare the file size (no `Content-Length`); check `downloaded` instead. |  |
| downloaded | int64 | Only applicable when "status" is `Downloading`, indicates the number of bytes downloaded so far. |  |
| status | string | Indicates download status, which could be either   - `Downloading`   - Check `progress` and `downloaded` key values for actual download progress     ```     "download_info": {         "downloaded": 268435456,         "progress": 5,         "status": "Downloading",         "url": "http://192.168.200.97:8080/5gb.zip"     }     ``` - `Download Success`   ```     "download_info": {         "status": "Download Success",         "url": "https://secure.eicar.org/eicar.com"     }   ``` - `Download Failed`   - Check `error_detail` key value for an error explanation   - The scan result is `Download Failed`     ```     "download_info": {         "error_detail": "Connection error",         "status": "Download Failed",         "url": "http://192.168.200.97:8080/2gb.zip"     }     ``` - `Download Timeout`   - Expecting to occur when the download takes longer than the file download timeout configured in the workflow (General tab > Timeouts > File download)   - The scan result is `Download Timeout`     ```     "download_info": {         "status": "Download Timeout",         "url": "http://192.168.200.97:8080/2gb.zip"     }     ``` - `Download Cancelled`   - Expecting to occur when user explicitly cancelled that file scan request, or batch request that the scan belongs to     ```     "download_info": {         "status": "Download Cancelled",         "url": "http://192.168.200.97:8080/5gb.zip"     }     ```   Enum: `Downloading`,`Download Success`,`Download Failed`,`Download Timeout`,`Download Cancelled` |  |
| url | string | Original download link which was specified in HTTP(S) request's `downloadfrom` header |  |
| extraction_info6 fields | object | Details for archive extraction. |  |
| decrypted_status | string | Indicate that decryption phase is successful or not.  Enum: `Success`,`Failed` |  |
| err_category | string | Error category |  |
| err_code | integer | Error code |  |
| err_details | string | Error message |  |
| is_encrypted_file | boolean | Indicate if file is password-protected or not. |  |
| total_reused_extraction_errors | integer | Indicates how many extraction errors were reused from a previous analysis instead of being detected during the current analysis. This can include errors from the archive itself or from nested archives. A value of 0 means no extraction errors were reused. This field is available starting with MetaDefender Cluster 2.10.0. |  |
| file_info13 fields | object | basic information of the scanned file |  |
| display_name | string | The filename reported via `filename` header. |  |
| file_size | integer | Total file size in bytes. |  |
| file_type | string | The filetype using mimetype. |  |
| file_type_description | string | The filetype in human readable format. |  |
| md5 | string | File's MD5 hash. |  |
| sha1 | string | File's SHA1 hash. |  |
| sha256 | string | File's SHA256 Hash. |  |
| sha512 | string | File's SHA512 Hash. |  |
| signer_infos6 fields | array[object] | Digital signature information of the scanned file. |  |
| digest_algorithm | string | Digest algorithm. |  |
| digest_encryption_algorithm | string | Encryption algorithm. |  |
| issuer | string | Entity that develops and registers the certificate. |  |
| serial_number | string | Serial number of the certificate. |  |
| vendor_name | string | Entity that is issued a certificate and utilize it for creating a digital signature. |  |
| version | string | Version of X.509 that is used in the certificate. This version field is zero-based.   - 0: v1 - 1: v2 - 2: v3 |  |
| type_category | array[string] | File type category.   - `A` - Archive files - `AP` - Application - `D` - Document (Microsoft Office) - `D_ENC` - Encrypted Documents - `E` - Executables - `G` - Graphical format (JPG, PNG, GIF, etc.) - `I` - Disk image - `M` - Audio or video format - `OPENSSL_ENC` - OpenSSL Encrypted Files - `P` - PDF format - `T` - Text - `Z` - Mail messages - `O` - Other (anything that is not recognized as one of the above)   Enum: `A`,`D`,`E`,`G`,`I`,`M`,`P`,`T`,`Z`,`O` |  |
| receive_data_timestamp | string | The timestamp when upload progress started (first byte received) (in milliseconds) |  |
| upload_time | integer | Total time elapsed for upload process (in milliseconds). |  |
| upload_timestamp | string | The timestamp when upload progress finished (all bytes received) (in milliseconds) |  |
| filetype_info6 fields | object | response information from FileType engine |  |
| file_info11 fields | object |  |  |
| description | string | File type description |  |
| detected_by | string | Analyzer that detected the file type |  |
| encrypted | boolean | File is password-protected or not |  |
| extensions | string | File type extension |  |
| groupID | string | File type category |  |
| groupIDs | array[string] | File type category.   - `A` - Archive files - `AP` - Application - `D` - Document (Microsoft Office) - `D_ENC` - Encrypted Documents - `E` - Executables - `G` - Graphical format (JPG, PNG, GIF, etc.) - `I` - Disk image - `M` - Audio or video format - `OPENSSL_ENC` - OpenSSL Encrypted Files - `P` - PDF format - `T` - Text - `Z` - Mail messages - `O` - Other (anything that is not recognized as one of the above)   Enum: `A`,`D`,`E`,`G`,`I`,`M`,`P`,`T`,`Z`,`O` |  |
| group_description | string | File type category description |  |
| likely_type_ids | array[object] | A list of likely file type IDs |  |
| score | integer | Likelihood score of the file type |  |
| typeID | string | File type ID |  |
| type | string | MIME type |  |
| typeID | string | File type ID |  |
| type_ids | array[string] | A list of file type IDs |  |
| final_verdict | object | Final verdict of the file type analysis. |  |
| verdict | string | Final verdict of the file type analysis.  Enum: `allowed`,`blocked` |  |
| verdict_explanation | string | Explanation of the final verdict. |  |
| is_file_type_mismatch | boolean | Indicates if the file type does not match the expected type. |  |
| result_template_hash | string | SHA256 Hash of user-interface template. For web console only. |  |
| spoofing_info3 fields | object | Spoofing information. |  |
| detection_result | string | Result of the spoofing detection. |  |
| result_explanation | string | Explanation of the spoofing detection result. |  |
| result_overview | string | Overview of the spoofing detection result. |  |
| opswatfilescan_info | object | response information from OPSWAT Filescan engine |  |
| original_data_id | string | The data ID of the previous analysis whose result was reused. This field is present only when the result was returned from an earlier analysis through the workflow rule's Reuse processing result option (`process_info.reuse_processing_result`) instead of being processed again. For archive files, archive result reuse must also be enabled with `process_info.reuse_processing_result.include_archive`. Available starting with MetaDefender Cluster 2.10.0. |  |
| process_info16 fields | object | Processing information |  |
| blocked_reason | string | Provides the reason why the file is blocked (if so). |  |
| blocked_reasons | array[string] | Provides the reason why the file is blocked in an array (if so). |  |
| file_type_skipped_scan | boolean | Indicates if the input file's detected type was configured to skip scanning. |  |
| hash_time | integer | Total time elapsed for computing hashes (in milliseconds). |  |
| outdated_data | array[string] | array of flags - if occur - describing outdated data in the result, these can be   - engineconfigurations: the configuration of any AV engine in Inventory > Modules has been modified since the item was processed - enginedefinitions: at least one of the AV engines the item was scanned with has a newer definition database - configuration: the process' rule - or any item used by the rule - was modified since the item was processed - sanitization: if item was sanitized this flag notifies that the sanitization information regarding this result is outdated, meaning the sanitized item is no longer available   Enum: `engineconfigurations`,`enginedefinitions`,`configuration`,`sanitization` |  |
| processing_time | integer | Total time elapsed during processing file (in milliseconds). |  |
| processing_time_details11 fields | object | Processing time on each major workflow processing step. |  |
| av_scan_time | integer | AV engines' processing time. |  |
| cdr_time | integer | Deep CDR engine's sanitization time. |  |
| dlp_time | integer | Proactive DLP engine's processing time. |  |
| extraction_time | integer | Archive extraction engine's processing time. |  |
| filetype_time | integer | FileType engine's processing time. |  |
| opswatfilescan_time | integer | OPSWAT Filescan engine's processing time. |  |
| others_time | integer | Total time elapsed for following processing tasks in the product (in milliseconds):   - Decryption time (if receiving an encrypted file) - External scanner (if configured) - Post action (if configured) - Other internal processing time among components in the product |  |
| parse_dgsg_time | integer | Digital signature analyzing time. |  |
| vul_time | integer | Vulnerability engine's lookup time. |  |
| yara_time | integer | YARA engine's processing time. |  |
| filetype_wait_time | integer | FileType engine's wait time. |  |
| profile | string | The used rule name. |  |
| progress_percentage | integer | Percentage of processing completed (from 1-100). |  |
| queue_time | integer | Total time elapsed for file processing task was waiting in MetaDefender Core’s queue until being picked up (queue_time = start_time - upload_timestamp) (in milliseconds). |  |
| result | string | The final result of processing the file (Allowed / Blocked / Processing). |  |
| user_agent | string | Identifier for the REST Client that calls the API. |  |
| username | string | User identifier who submitted scan request earlier. |  |
| verdicts | array[string] | Aggregated list of potential issues. |  |
| post_processing6 fields | object | Contains information about result of sanitization process and any action done after finalizing the process using Post Actions. |  |
| actions_failed | string | Empty string if no action failed or list of failed actions, separated by "|". |  |
| actions_ran | string | List of successful actions, separated by "|". Empty string if otherwise. |  |
| converted_destination | string | Contains the name of the sanitized file. |  |
| converted_to | string | Contains target type name of sanitization. |  |
| copy_move_destination | string | Contains target type name of sanitization. |  |
| sanitization_details9 fields | object | Deep CDR module returns forensic info to describe what happened during the process in the case file was successfully sanitized. |  |
| cdr_wait_time | integer | The time in milliseconds that the CDR process took to complete. |  |
| description | string | Action was successful or not. |  |
| details7 fields | array[object] | List of all sanitized objects |  |
| action | string | The type of action that was performed  Enum: `sanitized`,`removed` |  |
| count | integer | The number of objects that were sanitized/removed. |  |
| details4 fields | object | List of all sanitized objects of a sanitized embedded file |  |
| action | string | The type of action that was performed  Enum: `sanitized`,`removed` |  |
| count | integer | The number of objects that were sanitized/removed. |  |
| object_details | array[string] | Additional information about the sanitized object |  |
| object_name | string | The object type that was sanitized/removed. |  |
| description | string | Action was successful or not. |  |
| file_name | string | If an embedded file was sanitized. |  |
| object_details | array[string] | Additional information about the sanitized object |  |
| object_name | string | The object type that was sanitized/removed. |  |
| failure_category | string | Deep CDR errors are classified into different categories.  For more details, please find [Troubleshooting sanitization failures](https://docs.opswat.com/mdcore/deep-cdr/troubleshooting-sanitization-failures) |  |
| result | string | The result of the CDR process.   - **Sanitized**: the file was successfully sanitized. - **Sanitized failed**: the file could not be sanitized due to an error during the process. - **Sanitized skipped**: the file was skipped from sanitization. Common reasons include the file being digitally signed or other policy-based exclusions.   Enum: `Sanitized`,`Sanitized failed`,`Sanitized skipped` |  |
| result_template_hash | string | The hash value of the result template, which is used for displaying results on the Core UI and for internal communication between MetaDefender Core and the Deep CDR engine. This value is intended for system use only and is not required for external integration. |  |
| sanitized_file_info | object | Information of sanitized file. Only applicable to individual file sanitization, or original archive document sanitization level. |  |
| file_size | integer | Size of sanitized file in bytes. |  |
| sha256 | string | SHA256 hash of sanitized file. |  |
| verdict | string | The verdict of the CDR process.   - **blocked**: the file is recommended for blocking by Deep CDR. - **allowed**: the file is recommended for allowing by Deep CDR as it found no reason to recommend blocking it.   Enum: `blocked`,`allowed` |  |
| verdict_explanations | array[string] | The explanations for the verdict of the CDR process. |  |
| client_identity1 field | object | The `client-identity` helps track and understand the workflow that a file passes through clients, offering greater visibility into the processing stages and the clients involved. |  |
| clients6 fields | array[object] | Array of client identity objects. |  |
| deployment_id | string | Unique identifier for the deployment. |  |
| user_name | string | Name of the user or system that initiated the scan. |  |
| product_type | string | Type of product or system that is performing the scan. |  |
| version | string | Version of the product or system. |  |
| host | string | Hostname or IP address of the client machine. |  |
| timestamp | integer | Timestamp of when the scan was initiated, in milliseconds since epoch. |  |
| scan_results8 fields | object | Result of the scanning process. |  |
| data_id | string | Data ID of the requested file |  |
| progress_percentage | integer | Track analysis progress until reaches 100. |  |
| scan_all_result_a | string | Processing result and its index   - `No Threat Detected`: 0 - `Infected`: 1 - `Suspicious`: 2 - `Failed`: 3 - `Whitelisted`: 7 - `Blacklisted`: 8 - `Exceeded Archive Depth`: 9 - `Not Scanned`: 10 - `Encrypted Archive`: 12 - `Exceeded Archive Size`: 13 - `Exceeded Archive File Number`: 14 - `Password Protected Document`: 15 - `Exceeded Archive Timeout`: 16 - `Mismatch`: 17 - `Potentially Vulnerable File`: 18 - `Cancelled`: 19 - `Sensitive Data Found`: 20 - `Yara Rule Matched`: 21 - `Potentially Unwanted`: 22 - `Unsupported File Type`: 23 - `Extraction Failed`: 24 - `Scan Failed`: 25 - `Suspicious Verdict by Sandbox`: 26 - `Likely Malicious Verdict by Sandbox`: 27 - `Malicious Verdict by Sandbox`: 28 - `Blocked Verdict by Sandbox`: 29 - `Blocked Verdict by Deep CDR`: 30 - `Global Timeout Exceeded`: 31 - `Vulnerable Verdict by SBOM`: 32 - `Non-vulnerable Verdict by SBOM`: 33 - `Blocked Verdict by SBOM`: 34 - `Blocked by Post Action`: 36 - `Known Bad`: 38 - `Known Good`: 39 - `Unknown`: 40 - `Allowed Verdict by COO`: 41 - `Blocked Verdict by COO`: 42 - `Unknown Verdict by COO`: 43 - `OPSWAT AI Confidently Clean`: 67 - `OPSWAT AI Confidently Malicious`: 68 - `OPSWAT AI Undetermined`: 69 - `Download Timeout`: 70 - `Download Failed`: 71 - `In Progress`: 255 - `Skip Processing Fast Symlink`: 1014   Enum: `No Threat Detected`,`Infected`,`Suspicious`,`Failed`,`Whitelisted`,`Blacklisted`,`Exceeded Archive Depth`,`Not Scanned`,`Encrypted Archive`,`Exceeded Archive Size`,`Exceeded Archive File Number`,`Password Protected Document`,`Exceeded Archive Timeout`,`Mismatch`,`Potentially Vulnerable File`,`Cancelled`,`Sensitive Data Found`,`Yara Rule Matched`,`Potentially Unwanted`,`Unsupported File Type`,`Extraction Failed`,`Scan Failed`,`Suspicious Verdict by Sandbox`,`Likely Malicious Verdict by Sandbox`,`Malicious Verdict by Sandbox`,`Blocked Verdict by Sandbox`,`Blocked Verdict by Deep CDR`,`Global Timeout Exceeded`,`Vulnerable Verdict by SBOM`,`Non-vulnerable Verdict by SBOM`,`Blocked Verdict by SBOM`,`Blocked by Post Action`,`Known Bad`,`Known Good`,`Unknown`,`Allowed Verdict by COO`,`Blocked Verdict by COO`,`Unknown Verdict by COO`,`OPSWAT AI Confidently Clean`,`OPSWAT AI Confidently Malicious`,`OPSWAT AI Undetermined`,`Download Timeout`,`Download Failed`,`In Progress`,`Skip Processing Fast Symlink` |  |
| scan_all_result_i | integer | Scan result as index in the Processing Results table above  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`67`,`68`,`69`,`70`,`71`,`255`,`1014` |  |
| start_time | string | Timestamp when the scanning process starts. |  |
| total_avs | integer | Total number of scanning engines used as part of this analysis. |  |
| total_time | integer | Total time elapsed during scan (in milliseconds). |  |
| scan_details1 field | object | Scan results for each antivirus engine. The key is the name of the antivirus engine and the value is the result of the antivirus engine |  |
| ClamAV7 fields | object | Scan report per each engine. |  |
| def_time | string | The database definition time for this engine |  |
| eng_id | string | The unique identification string for the engine |  |
| location | string | Where this engine is deployed (local/remote). |  |
| scan_result_i | integer | Scan result as index in the Processing Results table |  |
| scan_time | integer | The time elapsed during scan with this engine (in milliseconds). |  |
| threat_found | string | The threat name, IF scan result is Infected or Suspicious. Otherwise empty string or error message from the engine. |  |
| wait_time | integer | Time elapsed between sending file to Core and receiving the result from the engine (in milliseconds). |  |
| vulnerability_info2 fields | object | Contains all vulnerability information of the analysis result |  |
| result6 fields | object | The result information provided by the OESIS Framework |  |
| code | integer | The result code for vulnerability check, 0 means a successful check |  |
| hash | string | The file's SHA1 hash value |  |
| method | integer | The method used by OESIS Framework, it should be 50700 every time.  Enum: `50700` |  |
| timestamp | string | Timestamp of the request issued |  |
| timing | integer | The vulnerability check's duration in milliseconds |  |
| detected_product12 fields | object | Detected products object is present if input hash has been found to correspond to verified product |  |
| has_kb | boolean | Indicates whether any KBs or MSBs exist for this hash |  |
| has_vulnerability | boolean | Indicates whether any vulnerabilities have been associated with the particular product |  |
| is_current | boolean | True if this product's patch level is current, defaults to true |  |
| product | object | Product data object |  |
| id | integer | The OPSWAT product id |  |
| name | string | The product name |  |
| remediation_link | string | A link where product updates or patches can be obtained |  |
| severity | string | String description of Severity level:   - `LOW` - `MODERATE` - `IMPORTANT` - `CRITICAL` - `NOT_AVAILABLE` - `UNKNOWN`   Enum: `LOW`,`MODERATE`,`IMPORTANT`,`CRITICAL`,`NOT_AVAILABLE`,`UNKNOWN` |  |
| sig_name | string | Product signature descriptor |  |
| signature | integer | OPSWAT signature id |  |
| vendor | object | Vendor data object |  |
| id | integer | The OPSWAT vendor id |  |
| name | string | The vendor name |  |
| version | string | The installed product version |  |
| version_data3 fields | object | Object containing detailed patch information |  |
| count_behind | integer | The number of patches behind of the installed product |  |
| feed_id | integer | The remote feed ID used to determine patch level |  |
| version | string | The current version of the product in the remote feed |  |
| vulnerabilites5 fields | array[object] | A list of specific vulnerabilities |  |
| description | string | A text description of the specific vulnerability |  |
| details7 fields | object | A set of optional vulnerability details |  |
| cpe | string | A CPE product reference |  |
| cve | string | A CVE identification string |  |
| cvss9 fields | object | A set of cvss severity information |  |
| access-complexity | string | A CVSS access-complexity descriptor |  |
| access-vector | string | A CVSS access-vector descriptor |  |
| authentication | string | A CVSS authentication descriptor |  |
| availability-impact | string | A CVSS availability impact descriptor |  |
| confidentiality-impact | string | A CVSS confidentiality impact descriptor |  |
| generated-on-epoch | string | An epoch timestamp indicating CVSS generation time |  |
| integrity-impact | string | A CVSS integrity impact descriptor |  |
| score | string | A CVSS 10-point severity score |  |
| source | string | A CVSS source descriptor |  |
| cwe | string | A CWE group identification string |  |
| last_modified_epoch | string | An epoch timestamp indicating source last update time |  |
| published-epoch | string | An epoch timestamp indicating source publishing time |  |
| references | array[string] | An array of external reference links |  |
| severity | string | String description of Severity level:   - `LOW` - `MODERATE` - `IMPORTANT` - `CRITICAL` - `NOT_AVAILABLE` - `UNKNOWN`   Enum: `LOW`,`MODERATE`,`IMPORTANT`,`CRITICAL`,`NOT_AVAILABLE`,`UNKNOWN` |  |
| severity_index | integer | A 5 point scale numerical description of Severity level with 5 being greatest and 0 being unknown |  |
| static_id | integer | An OPSWAT identifier for the vulnerability |  |
| verdict | integer | The vulnerability check's duration in milliseconds   - `0` - No Vulnerability Found - `1` - Vulnerability Found - `3` - Failed - `16` - Processing Timed Out |  |
| yara | object | Information on data that matched YARA rules |  |
| hits | object | detailed results that contains the name of the matched rules and a description for each. |  |
| verdict | integer | The overall result for the analyzed file. Value will be one of the following: | index | status | |---------------|------------------------------| | 0 | Clean | | 1 | Found matched data | | 2 | Suspicious | | 3 | Failed | | 4 | Not scanned |  Enum: `0`,`1`,`2`,`3`,`4` |  |

Expand 400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Fetch Analysis Result By Hash

Retrieve analysis result by hash

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| rule | string | Select rule for the analysis, if no header given the default rule will be selected (URL encoded UTF-8 string of rule name) |  |
| selfonly | boolean | Useful to archive hash lookup.  Allow specifying to only perform hash lookup against the original archive file self only, and skip searching all child files result within the original archive.  Default value is false. |  |
| timerange | integer | Scoping down the recent number of hours that hash lookup task should start from till now, instead of searching the entire scan history in MetaDefender Cluster database.  Default value is 0. That means no time scope. |  |
| include-inprogress | boolean | False (default): API will return "Not Found" if the verdict is in progress.  True: If the queried hash has a completed processing result before, API will return the completed processing result. If this hash doesn't have any completed processing result, API will return this In-progress result. |  |

Path Params

| md5|sha1|sha256|sha512 | string | Hash value to search. This can be md5, sha1, sha256, sha512 |  |
| --- | --- | --- | --- |

Query String

| first | integer | The `first` item order in the list child files of archive file  minimum: 0  Default: 0 |  |
| --- | --- | --- | --- |
| size | integer | The number of items to be fetched next, counting from the item order indicated in `first` header. The default value is 50, and the maximum value is 2000.  maximum: 2000  minimum: 0  Default: 50 |  |

GET /hash/{md5|sha1|sha256|sha512}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Get information of file

| object | object |  |  |
| --- | --- | --- | --- |
| data_id | string | data identifier of the requested file |  |
| deflected_engines | array[string] | Engines skipped (deflected) for this file based on the OPSWAT Alin AI Deflection verdict (available starting with MetaDefender Cluster 2.10.0). Returned only when at least one engine was deflected. Each item is an engine identifier, e.g. `extraction`, `metascan`, `ds`, `oesis`, `dlp`, `yara`, `filescanio`, `sbom`, `coo`, `reputation`, `ti`, `aigcd`, `fsv`. |  |
| deflection_info5 fields | object | Report from the OPSWAT Alin AI Deflection engine (available starting with MetaDefender Cluster 2.10.0). Deflection produces an early verdict on a file that can be used to skip (deflect) other engines in the workflow. The object is empty when Deflection did not run on the file. |  |
| final_verdict3 fields | object | Overall Deflection verdict and supporting details. |  |
| verdict | string | Deflection engine verdict. Values:   - clean: the file is considered clean. - malicious: the file is considered malicious. - unknown: the engine could not confidently classify the file. - Cancelled: processing was cancelled before a verdict was produced.   Enum: `clean`,`malicious`,`unknown`,`Cancelled` |  |
| confidence | integer | Confidence of the verdict, as a percentage (0-100).  maximum: 100  minimum: 0 |  |
| detail | object | Additional details about the analyzed file. |  |
| data_id | string | data identifier of the analyzed file. |  |
| file_type | string | Detected file type of the analyzed file. |  |
| result_template_hash | string | Hash of the result template used internally for Deflection rendering and coordination. |  |
| err_code | integer | Returned only when Deflection failed to produce a verdict (`final_verdict` is then absent). Common values:   - 1: Deflection failed. - 5: Deflection timed out. - 6: The file type is not supported by Deflection. - 9: The global processing timeout was exceeded. |  |
| err_details | string | Returned only when Deflection failed. Human-readable reason of the failure. |  |
| err_category | string | Returned only when Deflection failed and the engine reported a failure category. |  |
| dlp_info9 fields | object | Full report from Proactive DLP |  |
| certainty | string | Describes how certain the hit is, possible values:   - `Very Low` - `Low` - `Medium` - `High` - `Very High`   Enum: `Very Low`,`Low`,`Medium`,`High`,`Very High` |  |
| errors | object | A list of error objects (empty if no errors happened), each error object contains following keys:   - `scan`: scan related error description - `redact`: redaction related error description - `watermark`: watermark related error description - `metadata_removal`: metadata removal related error description |  |
| filename | string | Output processed file name (pre-configured on engine settings under Core's worflow rule) |  |
| hits1 field | object | Detailed results that contains as key the type of matched rule:   - ccn (credit card number), - ssn (social security number), - regex_ (regular expression with an index in order to differentiate the RegEx rules if there are more.) |  |
| ccn2 fields | object |  |  |
| display_name | string | Credit Card Number, Social Security Number, or in case of RegEx, the name of the rule that has been given by the user |  |
| hits | array[object] | A list of detections that matched this rule/pattern. |  |
| after | string | The context after the matched data. |  |
| before | string | The context before the matched data. |  |
| certainty | string | The text version of "certainty_score", possible values:   - `Very Low` - `Low` - `Medium` - `High` - `Very High`   Enum: `Very Low`,`Low`,`Medium`,`High`,`Very High` |  |
| certainty_score | integer | Is defined by the relevance of the given hit in its context. It is calculated based on multiple factors such as the number of digits, possible values: [0-100] |  |
| hit | string | The matched data. |  |
| location | string | The location of the hit that is found in a file. |  |
| severity | integer | (NOTE: this field is deprecated): can be 0 (detected) or 1 (suspicious).  Enum: `0`,`1` |  |
| tryRedact | boolean | If file was redacted or not. |  |
| metadata_removal | object | Result of metadata removal. |  |
| result | string | Result of the metadata removal process, possible values:   - `removed` - `not removed` - `failed to remove`   Enum: `removed`,`not removed`,`failed to remove` |  |
| redact | object | Result of redaction process. |  |
| result | string | Result of the redaction process, possible values:   - `redacted` - `not redacted` - `failed to redact`   Enum: `redacted`,`not redacted`,`failed to redact` |  |
| severity | integer | (NOTE: this field is deprecated): represents the severity of the data loss, possible values:   - `0` - Certainly is data loss - `1` - Might be data loss   Enum: `0`,`1` |  |
| verdict | integer | The overall result for the scanned file. Possible values:   - `0` - Clean - `1` - Found matched data - `2` - Suspicious - `3` - Failed - `4` - Not scanned   Enum: `0`,`1`,`2`,`3`,`4` |  |
| watermark | object | Result of watermarking process. |  |
| result | string | Result of the watermarking process, possible values:   - `added` - `not added` - `failed to add`   Enum: `added`,`not added`,`failed to add` |  |
| download_info5 fields | object | The downloading status. Only present when the file was submitted with the `downloadfrom` header (scan from link), in which case MetaDefender Cluster Download Service downloads the file before it is scanned. |  |
| error_detail | string | Revealed detailed reason why the download failed. Only present when the download did not succeed. |  |
| progress | number | Only applicable when "status" is `Downloading`, indicates download finished percentage, in a range of [0, 99].   - Once hitting 100, the status will be changed to `Download Success`. - or other problematic status (`Download Cancelled`, `Download Failed`, `Download Timeout`) if the download stopped unexpectedly. - Stays at 0 when the download server does not declare the file size (no `Content-Length`); check `downloaded` instead. |  |
| downloaded | int64 | Only applicable when "status" is `Downloading`, indicates the number of bytes downloaded so far. |  |
| status | string | Indicates download status, which could be either   - `Downloading`   - Check `progress` and `downloaded` key values for actual download progress     ```     "download_info": {         "downloaded": 268435456,         "progress": 5,         "status": "Downloading",         "url": "http://192.168.200.97:8080/5gb.zip"     }     ``` - `Download Success`   ```     "download_info": {         "status": "Download Success",         "url": "https://secure.eicar.org/eicar.com"     }   ``` - `Download Failed`   - Check `error_detail` key value for an error explanation   - The scan result is `Download Failed`     ```     "download_info": {         "error_detail": "Connection error",         "status": "Download Failed",         "url": "http://192.168.200.97:8080/2gb.zip"     }     ``` - `Download Timeout`   - Expecting to occur when the download takes longer than the file download timeout configured in the workflow (General tab > Timeouts > File download)   - The scan result is `Download Timeout`     ```     "download_info": {         "status": "Download Timeout",         "url": "http://192.168.200.97:8080/2gb.zip"     }     ``` - `Download Cancelled`   - Expecting to occur when user explicitly cancelled that file scan request, or batch request that the scan belongs to     ```     "download_info": {         "status": "Download Cancelled",         "url": "http://192.168.200.97:8080/5gb.zip"     }     ```   Enum: `Downloading`,`Download Success`,`Download Failed`,`Download Timeout`,`Download Cancelled` |  |
| url | string | Original download link which was specified in HTTP(S) request's `downloadfrom` header |  |
| extraction_info6 fields | object | Details for archive extraction. |  |
| decrypted_status | string | Indicate that decryption phase is successful or not.  Enum: `Success`,`Failed` |  |
| err_category | string | Error category |  |
| err_code | integer | Error code |  |
| err_details | string | Error message |  |
| is_encrypted_file | boolean | Indicate if file is password-protected or not. |  |
| total_reused_extraction_errors | integer | Indicates how many extraction errors were reused from a previous analysis instead of being detected during the current analysis. This can include errors from the archive itself or from nested archives. A value of 0 means no extraction errors were reused. This field is available starting with MetaDefender Cluster 2.10.0. |  |
| file_info13 fields | object | basic information of the scanned file |  |
| display_name | string | The filename reported via `filename` header. |  |
| file_size | integer | Total file size in bytes. |  |
| file_type | string | The filetype using mimetype. |  |
| file_type_description | string | The filetype in human readable format. |  |
| md5 | string | File's MD5 hash. |  |
| sha1 | string | File's SHA1 hash. |  |
| sha256 | string | File's SHA256 Hash. |  |
| sha512 | string | File's SHA512 Hash. |  |
| signer_infos6 fields | array[object] | Digital signature information of the scanned file. |  |
| digest_algorithm | string | Digest algorithm. |  |
| digest_encryption_algorithm | string | Encryption algorithm. |  |
| issuer | string | Entity that develops and registers the certificate. |  |
| serial_number | string | Serial number of the certificate. |  |
| vendor_name | string | Entity that is issued a certificate and utilize it for creating a digital signature. |  |
| version | string | Version of X.509 that is used in the certificate. This version field is zero-based.   - 0: v1 - 1: v2 - 2: v3 |  |
| type_category | array[string] | File type category.   - `A` - Archive files - `AP` - Application - `D` - Document (Microsoft Office) - `D_ENC` - Encrypted Documents - `E` - Executables - `G` - Graphical format (JPG, PNG, GIF, etc.) - `I` - Disk image - `M` - Audio or video format - `OPENSSL_ENC` - OpenSSL Encrypted Files - `P` - PDF format - `T` - Text - `Z` - Mail messages - `O` - Other (anything that is not recognized as one of the above)   Enum: `A`,`D`,`E`,`G`,`I`,`M`,`P`,`T`,`Z`,`O` |  |
| receive_data_timestamp | string | The timestamp when upload progress started (first byte received) (in milliseconds) |  |
| upload_time | integer | Total time elapsed for upload process (in milliseconds). |  |
| upload_timestamp | string | The timestamp when upload progress finished (all bytes received) (in milliseconds) |  |
| filetype_info6 fields | object | response information from FileType engine |  |
| file_info11 fields | object |  |  |
| description | string | File type description |  |
| detected_by | string | Analyzer that detected the file type |  |
| encrypted | boolean | File is password-protected or not |  |
| extensions | string | File type extension |  |
| groupID | string | File type category |  |
| groupIDs | array[string] | File type category.   - `A` - Archive files - `AP` - Application - `D` - Document (Microsoft Office) - `D_ENC` - Encrypted Documents - `E` - Executables - `G` - Graphical format (JPG, PNG, GIF, etc.) - `I` - Disk image - `M` - Audio or video format - `OPENSSL_ENC` - OpenSSL Encrypted Files - `P` - PDF format - `T` - Text - `Z` - Mail messages - `O` - Other (anything that is not recognized as one of the above)   Enum: `A`,`D`,`E`,`G`,`I`,`M`,`P`,`T`,`Z`,`O` |  |
| group_description | string | File type category description |  |
| likely_type_ids | array[object] | A list of likely file type IDs |  |
| score | integer | Likelihood score of the file type |  |
| typeID | string | File type ID |  |
| type | string | MIME type |  |
| typeID | string | File type ID |  |
| type_ids | array[string] | A list of file type IDs |  |
| final_verdict | object | Final verdict of the file type analysis. |  |
| verdict | string | Final verdict of the file type analysis.  Enum: `allowed`,`blocked` |  |
| verdict_explanation | string | Explanation of the final verdict. |  |
| is_file_type_mismatch | boolean | Indicates if the file type does not match the expected type. |  |
| result_template_hash | string | SHA256 Hash of user-interface template. For web console only. |  |
| spoofing_info3 fields | object | Spoofing information. |  |
| detection_result | string | Result of the spoofing detection. |  |
| result_explanation | string | Explanation of the spoofing detection result. |  |
| result_overview | string | Overview of the spoofing detection result. |  |
| opswatfilescan_info | object | response information from OPSWAT Filescan engine |  |
| original_data_id | string | The data ID of the previous analysis whose result was reused. This field is present only when the result was returned from an earlier analysis through the workflow rule's Reuse processing result option (`process_info.reuse_processing_result`) instead of being processed again. For archive files, archive result reuse must also be enabled with `process_info.reuse_processing_result.include_archive`. Available starting with MetaDefender Cluster 2.10.0. |  |
| process_info16 fields | object | Processing information |  |
| blocked_reason | string | Provides the reason why the file is blocked (if so). |  |
| blocked_reasons | array[string] | Provides the reason why the file is blocked in an array (if so). |  |
| file_type_skipped_scan | boolean | Indicates if the input file's detected type was configured to skip scanning. |  |
| hash_time | integer | Total time elapsed for computing hashes (in milliseconds). |  |
| outdated_data | array[string] | array of flags - if occur - describing outdated data in the result, these can be   - engineconfigurations: the configuration of any AV engine in Inventory > Modules has been modified since the item was processed - enginedefinitions: at least one of the AV engines the item was scanned with has a newer definition database - configuration: the process' rule - or any item used by the rule - was modified since the item was processed - sanitization: if item was sanitized this flag notifies that the sanitization information regarding this result is outdated, meaning the sanitized item is no longer available   Enum: `engineconfigurations`,`enginedefinitions`,`configuration`,`sanitization` |  |
| processing_time | integer | Total time elapsed during processing file (in milliseconds). |  |
| processing_time_details11 fields | object | Processing time on each major workflow processing step. |  |
| av_scan_time | integer | AV engines' processing time. |  |
| cdr_time | integer | Deep CDR engine's sanitization time. |  |
| dlp_time | integer | Proactive DLP engine's processing time. |  |
| extraction_time | integer | Archive extraction engine's processing time. |  |
| filetype_time | integer | FileType engine's processing time. |  |
| opswatfilescan_time | integer | OPSWAT Filescan engine's processing time. |  |
| others_time | integer | Total time elapsed for following processing tasks in the product (in milliseconds):   - Decryption time (if receiving an encrypted file) - External scanner (if configured) - Post action (if configured) - Other internal processing time among components in the product |  |
| parse_dgsg_time | integer | Digital signature analyzing time. |  |
| vul_time | integer | Vulnerability engine's lookup time. |  |
| yara_time | integer | YARA engine's processing time. |  |
| filetype_wait_time | integer | FileType engine's wait time. |  |
| profile | string | The used rule name. |  |
| progress_percentage | integer | Percentage of processing completed (from 1-100). |  |
| queue_time | integer | Total time elapsed for file processing task was waiting in MetaDefender Core’s queue until being picked up (queue_time = start_time - upload_timestamp) (in milliseconds). |  |
| result | string | The final result of processing the file (Allowed / Blocked / Processing). |  |
| user_agent | string | Identifier for the REST Client that calls the API. |  |
| username | string | User identifier who submitted scan request earlier. |  |
| verdicts | array[string] | Aggregated list of potential issues. |  |
| post_processing6 fields | object | Contains information about result of sanitization process and any action done after finalizing the process using Post Actions. |  |
| actions_failed | string | Empty string if no action failed or list of failed actions, separated by "|". |  |
| actions_ran | string | List of successful actions, separated by "|". Empty string if otherwise. |  |
| converted_destination | string | Contains the name of the sanitized file. |  |
| converted_to | string | Contains target type name of sanitization. |  |
| copy_move_destination | string | Contains target type name of sanitization. |  |
| sanitization_details9 fields | object | Deep CDR module returns forensic info to describe what happened during the process in the case file was successfully sanitized. |  |
| cdr_wait_time | integer | The time in milliseconds that the CDR process took to complete. |  |
| description | string | Action was successful or not. |  |
| details7 fields | array[object] | List of all sanitized objects |  |
| action | string | The type of action that was performed  Enum: `sanitized`,`removed` |  |
| count | integer | The number of objects that were sanitized/removed. |  |
| details4 fields | object | List of all sanitized objects of a sanitized embedded file |  |
| action | string | The type of action that was performed  Enum: `sanitized`,`removed` |  |
| count | integer | The number of objects that were sanitized/removed. |  |
| object_details | array[string] | Additional information about the sanitized object |  |
| object_name | string | The object type that was sanitized/removed. |  |
| description | string | Action was successful or not. |  |
| file_name | string | If an embedded file was sanitized. |  |
| object_details | array[string] | Additional information about the sanitized object |  |
| object_name | string | The object type that was sanitized/removed. |  |
| failure_category | string | Deep CDR errors are classified into different categories.  For more details, please find [Troubleshooting sanitization failures](https://docs.opswat.com/mdcore/deep-cdr/troubleshooting-sanitization-failures) |  |
| result | string | The result of the CDR process.   - **Sanitized**: the file was successfully sanitized. - **Sanitized failed**: the file could not be sanitized due to an error during the process. - **Sanitized skipped**: the file was skipped from sanitization. Common reasons include the file being digitally signed or other policy-based exclusions.   Enum: `Sanitized`,`Sanitized failed`,`Sanitized skipped` |  |
| result_template_hash | string | The hash value of the result template, which is used for displaying results on the Core UI and for internal communication between MetaDefender Core and the Deep CDR engine. This value is intended for system use only and is not required for external integration. |  |
| sanitized_file_info | object | Information of sanitized file. Only applicable to individual file sanitization, or original archive document sanitization level. |  |
| file_size | integer | Size of sanitized file in bytes. |  |
| sha256 | string | SHA256 hash of sanitized file. |  |
| verdict | string | The verdict of the CDR process.   - **blocked**: the file is recommended for blocking by Deep CDR. - **allowed**: the file is recommended for allowing by Deep CDR as it found no reason to recommend blocking it.   Enum: `blocked`,`allowed` |  |
| verdict_explanations | array[string] | The explanations for the verdict of the CDR process. |  |
| client_identity1 field | object | The `client-identity` helps track and understand the workflow that a file passes through clients, offering greater visibility into the processing stages and the clients involved. |  |
| clients6 fields | array[object] | Array of client identity objects. |  |
| deployment_id | string | Unique identifier for the deployment. |  |
| user_name | string | Name of the user or system that initiated the scan. |  |
| product_type | string | Type of product or system that is performing the scan. |  |
| version | string | Version of the product or system. |  |
| host | string | Hostname or IP address of the client machine. |  |
| timestamp | integer | Timestamp of when the scan was initiated, in milliseconds since epoch. |  |
| scan_results8 fields | object | Result of the scanning process. |  |
| data_id | string | Data ID of the requested file |  |
| progress_percentage | integer | Track analysis progress until reaches 100. |  |
| scan_all_result_a | string | Processing result and its index   - `No Threat Detected`: 0 - `Infected`: 1 - `Suspicious`: 2 - `Failed`: 3 - `Whitelisted`: 7 - `Blacklisted`: 8 - `Exceeded Archive Depth`: 9 - `Not Scanned`: 10 - `Encrypted Archive`: 12 - `Exceeded Archive Size`: 13 - `Exceeded Archive File Number`: 14 - `Password Protected Document`: 15 - `Exceeded Archive Timeout`: 16 - `Mismatch`: 17 - `Potentially Vulnerable File`: 18 - `Cancelled`: 19 - `Sensitive Data Found`: 20 - `Yara Rule Matched`: 21 - `Potentially Unwanted`: 22 - `Unsupported File Type`: 23 - `Extraction Failed`: 24 - `Scan Failed`: 25 - `Suspicious Verdict by Sandbox`: 26 - `Likely Malicious Verdict by Sandbox`: 27 - `Malicious Verdict by Sandbox`: 28 - `Blocked Verdict by Sandbox`: 29 - `Blocked Verdict by Deep CDR`: 30 - `Global Timeout Exceeded`: 31 - `Vulnerable Verdict by SBOM`: 32 - `Non-vulnerable Verdict by SBOM`: 33 - `Blocked Verdict by SBOM`: 34 - `Blocked by Post Action`: 36 - `Known Bad`: 38 - `Known Good`: 39 - `Unknown`: 40 - `Allowed Verdict by COO`: 41 - `Blocked Verdict by COO`: 42 - `Unknown Verdict by COO`: 43 - `OPSWAT AI Confidently Clean`: 67 - `OPSWAT AI Confidently Malicious`: 68 - `OPSWAT AI Undetermined`: 69 - `Download Timeout`: 70 - `Download Failed`: 71 - `In Progress`: 255 - `Skip Processing Fast Symlink`: 1014   Enum: `No Threat Detected`,`Infected`,`Suspicious`,`Failed`,`Whitelisted`,`Blacklisted`,`Exceeded Archive Depth`,`Not Scanned`,`Encrypted Archive`,`Exceeded Archive Size`,`Exceeded Archive File Number`,`Password Protected Document`,`Exceeded Archive Timeout`,`Mismatch`,`Potentially Vulnerable File`,`Cancelled`,`Sensitive Data Found`,`Yara Rule Matched`,`Potentially Unwanted`,`Unsupported File Type`,`Extraction Failed`,`Scan Failed`,`Suspicious Verdict by Sandbox`,`Likely Malicious Verdict by Sandbox`,`Malicious Verdict by Sandbox`,`Blocked Verdict by Sandbox`,`Blocked Verdict by Deep CDR`,`Global Timeout Exceeded`,`Vulnerable Verdict by SBOM`,`Non-vulnerable Verdict by SBOM`,`Blocked Verdict by SBOM`,`Blocked by Post Action`,`Known Bad`,`Known Good`,`Unknown`,`Allowed Verdict by COO`,`Blocked Verdict by COO`,`Unknown Verdict by COO`,`OPSWAT AI Confidently Clean`,`OPSWAT AI Confidently Malicious`,`OPSWAT AI Undetermined`,`Download Timeout`,`Download Failed`,`In Progress`,`Skip Processing Fast Symlink` |  |
| scan_all_result_i | integer | Scan result as index in the Processing Results table above  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`67`,`68`,`69`,`70`,`71`,`255`,`1014` |  |
| start_time | string | Timestamp when the scanning process starts. |  |
| total_avs | integer | Total number of scanning engines used as part of this analysis. |  |
| total_time | integer | Total time elapsed during scan (in milliseconds). |  |
| scan_details1 field | object | Scan results for each antivirus engine. The key is the name of the antivirus engine and the value is the result of the antivirus engine |  |
| ClamAV7 fields | object | Scan report per each engine. |  |
| def_time | string | The database definition time for this engine |  |
| eng_id | string | The unique identification string for the engine |  |
| location | string | Where this engine is deployed (local/remote). |  |
| scan_result_i | integer | Scan result as index in the Processing Results table |  |
| scan_time | integer | The time elapsed during scan with this engine (in milliseconds). |  |
| threat_found | string | The threat name, IF scan result is Infected or Suspicious. Otherwise empty string or error message from the engine. |  |
| wait_time | integer | Time elapsed between sending file to Core and receiving the result from the engine (in milliseconds). |  |
| vulnerability_info2 fields | object | Contains all vulnerability information of the analysis result |  |
| result6 fields | object | The result information provided by the OESIS Framework |  |
| code | integer | The result code for vulnerability check, 0 means a successful check |  |
| hash | string | The file's SHA1 hash value |  |
| method | integer | The method used by OESIS Framework, it should be 50700 every time.  Enum: `50700` |  |
| timestamp | string | Timestamp of the request issued |  |
| timing | integer | The vulnerability check's duration in milliseconds |  |
| detected_product12 fields | object | Detected products object is present if input hash has been found to correspond to verified product |  |
| has_kb | boolean | Indicates whether any KBs or MSBs exist for this hash |  |
| has_vulnerability | boolean | Indicates whether any vulnerabilities have been associated with the particular product |  |
| is_current | boolean | True if this product's patch level is current, defaults to true |  |
| product | object | Product data object |  |
| id | integer | The OPSWAT product id |  |
| name | string | The product name |  |
| remediation_link | string | A link where product updates or patches can be obtained |  |
| severity | string | String description of Severity level:   - `LOW` - `MODERATE` - `IMPORTANT` - `CRITICAL` - `NOT_AVAILABLE` - `UNKNOWN`   Enum: `LOW`,`MODERATE`,`IMPORTANT`,`CRITICAL`,`NOT_AVAILABLE`,`UNKNOWN` |  |
| sig_name | string | Product signature descriptor |  |
| signature | integer | OPSWAT signature id |  |
| vendor | object | Vendor data object |  |
| id | integer | The OPSWAT vendor id |  |
| name | string | The vendor name |  |
| version | string | The installed product version |  |
| version_data3 fields | object | Object containing detailed patch information |  |
| count_behind | integer | The number of patches behind of the installed product |  |
| feed_id | integer | The remote feed ID used to determine patch level |  |
| version | string | The current version of the product in the remote feed |  |
| vulnerabilites5 fields | array[object] | A list of specific vulnerabilities |  |
| description | string | A text description of the specific vulnerability |  |
| details7 fields | object | A set of optional vulnerability details |  |
| cpe | string | A CPE product reference |  |
| cve | string | A CVE identification string |  |
| cvss9 fields | object | A set of cvss severity information |  |
| access-complexity | string | A CVSS access-complexity descriptor |  |
| access-vector | string | A CVSS access-vector descriptor |  |
| authentication | string | A CVSS authentication descriptor |  |
| availability-impact | string | A CVSS availability impact descriptor |  |
| confidentiality-impact | string | A CVSS confidentiality impact descriptor |  |
| generated-on-epoch | string | An epoch timestamp indicating CVSS generation time |  |
| integrity-impact | string | A CVSS integrity impact descriptor |  |
| score | string | A CVSS 10-point severity score |  |
| source | string | A CVSS source descriptor |  |
| cwe | string | A CWE group identification string |  |
| last_modified_epoch | string | An epoch timestamp indicating source last update time |  |
| published-epoch | string | An epoch timestamp indicating source publishing time |  |
| references | array[string] | An array of external reference links |  |
| severity | string | String description of Severity level:   - `LOW` - `MODERATE` - `IMPORTANT` - `CRITICAL` - `NOT_AVAILABLE` - `UNKNOWN`   Enum: `LOW`,`MODERATE`,`IMPORTANT`,`CRITICAL`,`NOT_AVAILABLE`,`UNKNOWN` |  |
| severity_index | integer | A 5 point scale numerical description of Severity level with 5 being greatest and 0 being unknown |  |
| static_id | integer | An OPSWAT identifier for the vulnerability |  |
| verdict | integer | The vulnerability check's duration in milliseconds   - `0` - No Vulnerability Found - `1` - Vulnerability Found - `3` - Failed - `16` - Processing Timed Out |  |
| yara | object | Information on data that matched YARA rules |  |
| hits | object | detailed results that contains the name of the matched rules and a description for each. |  |
| verdict | integer | The overall result for the analyzed file. Value will be one of the following: | index | status | |---------------|------------------------------| | 0 | Clean | | 1 | Found matched data | | 2 | Suspicious | | 3 | Failed | | 4 | Not scanned |  Enum: `0`,`1`,`2`,`3`,`4` |  |

Expand 404

Invalid hash format

 Response
### Retrieve blocked leaf files from an archive by hash

Returns the deepest blocked files found within an original archive, identified by the archive's hash value.
A leaf file is a file that has no successfully extracted child files.
If no blocked leaf files are found, the response returns an empty array.
A maximum of 100 blocked leaf files is returned in a single request.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| rule | string | Select rule for the analysis, if no header given the default rule will be selected (URL encoded UTF-8 string of rule name) |  |
| timerange | integer | Limits the hash lookup to files analyzed within the specified number of hours.  A value of `0` (default) searches the entire analysis history. |  |

Path Params

| md5|sha1|sha256|sha512 | string | Hash value of the archive. Supported hash types are MD5, SHA-1, SHA-256, and SHA-512. |  |
| --- | --- | --- | --- |

GET /hash/{md5|sha1|sha256|sha512}/blocked-leavescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successfully retrieved the list of blocked leaf files.

| object | object |  |  |
| --- | --- | --- | --- |
| details10 fields | array[object] | List of blocked leaf files. |  |
| blocked_reasons | array[string] | Reasons why the file was blocked. |  |
| engines | array[object] | Detection results reported by individual engines. |  |
| engine | string | Name of the scanning engine. |  |
| threat_name | string | Threat detected by the engine. |  |
| data_id | string | Unique identifier of the blocked leaf file. |  |
| display_name | string | Name of the blocked leaf file. |  |
| file_type | string | MIME type of the file. |  |
| parent_id | string | Data identifier of the original archive. |  |
| path | string | Full path of the blocked leaf file within the archive. |  |
| process_info1 field | object | Processing information. |  |
| post_processing | object | Details of post-processing actions. |  |
| actions_failed | string | Failed post-processing actions, separated by `|`. Empty if none. |  |
| actions_ran | string | Successful post-processing actions, separated by `|`. Empty if none. |  |
| verdicts | array[string] | Aggregated verdicts for the blocked leaf file. |  |
| yara_info | object | YARA scan results for the blocked leaf file. |  |
| hits | array[string] | Matched YARA rules. |  |
| limit_reached | boolean | Indicates whether more than 100 blocked leaf files were found. |  |
| total | integer | Number of blocked leaf files returned in the `details` array. |  |

400

The `timerange` header value is invalid.

404

The specified hash was not found, or the file is still being processed.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response sample
### Fetching Available Analysis Rules

Retrieve all available rules with their custom configurations.
Fetching available processing rules.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. Only those rules are returned, that:   - Match the apikey's role sent using the apikey header, or - Are not restricted to a specific role. |  |
| --- | --- | --- | --- |
| user_agent | string | The user agent string value sent in the header (specified by the client).  Only those rules are returned, that:   - Match the client's user agent sent using the user_agent header, or - Are not restricted to a specific user agent.   For details see KB article [What are Security Policies and how do I use them?](https://onlinehelp.opswat.com/corev4/What_are_Security_Policies_and_how_do_I_use_them_.html). |  |

GET /file/rulescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Returns the list of available rules.

| array | array[object] |  |  |
| --- | --- | --- | --- |
| max_file_size | integer | The maximum allowed file size (in bytes) for this rule. |  |
| name | string | A unique identifier for identify in the used rule for a scan.. |  |
| global_timeout | object | The global timeout for the rule in seconds. If the rule takes longer than this time, it will be stopped. |  |
| value | integer | The timeout value in seconds. |  |
| enabled | boolean | Indicates whether the global timeout is enabled. |  |

500

Unexpected event on server.

 Response
### Download Sanitized Files

Retrieve sanitized file based on the `data_id`

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| data_id | string | The data_id comes from the result of `Analyze a file`. In case of sanitizing the content of an archive, the data_id of contained file can be found in `Fetch analysis result`. |  |
| --- | --- | --- | --- |

GET /file/converted/{data_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

Returns the sanitized content.

| file | file |  |  |
| --- | --- | --- | --- |

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Download either sanitized files or DLP processed files

Retrieve sanitized file based on the `data_id`.
In case there's no sanitized file, and DLP processed file is available, user will retrieve DLP processed file.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| data_id | string | The data_id comes from the result of `Analyze a file`. In case of sanitizing the content of an archive, the data_id of contained file can be found in `Fetch analysis result`. |  |
| --- | --- | --- | --- |

GET /file/download/{data_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

Returns the sanitized or DLP processed content.

| file | file |  |  |
| --- | --- | --- | --- |

404

File could not be found

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Cancel File Analysis

When cancelling a file analysis, the connected analysis (e.g. files in an archive) that are still in progress will be cancelled also.

The cancelled analysis will be automatically closed.

When the file was submitted with the `downloadfrom` header and is still being downloaded, the download is stopped and `download_info.status` becomes `Download Cancelled`.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| data_id | string | Unique submission identifier. Use this value to reference the submission. |  |
| --- | --- | --- | --- |

POST /file/{data_id}/cancelcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Analysis was sucessfully cancelled.

| object | object |  |  |
| --- | --- | --- | --- |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Data ID not found (invalid id) or Requests resource was not found

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Retrieve blocked leaf files from an archive

Returns the deepest blocked files found within an original archive, identified by the archive's `data_id`.
A leaf file is a file that has no successfully extracted child files.
If no blocked leaf files are found, the response returns an empty array.
A maximum of 100 blocked leaf files is returned in a single request.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| data_id | string | The `data_id` returned by the **Analyze a file** API. When analyzing or sanitizing an archive, the `data_id` of files contained within the archive can be obtained from the **Fetch analysis result** API. |  |
| --- | --- | --- | --- |

GET /file/{data_id}/blocked-leavescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successfully retrieved the list of blocked leaf files.

| object | object |  |  |
| --- | --- | --- | --- |
| details10 fields | array[object] | List of blocked leaf files. |  |
| blocked_reasons | array[string] | Reasons why the file was blocked. |  |
| engines | array[object] | Detection results reported by individual engines. |  |
| engine | string | Name of the scanning engine. |  |
| threat_name | string | Threat detected by the engine. |  |
| data_id | string | Unique identifier of the blocked leaf file. |  |
| display_name | string | Name of the blocked leaf file. |  |
| file_type | string | MIME type of the file. |  |
| parent_id | string | Data identifier of the original archive. |  |
| path | string | Full path of the blocked leaf file within the archive. |  |
| process_info1 field | object | Processing information. |  |
| post_processing | object | Details of post-processing actions. |  |
| actions_failed | string | Failed post-processing actions, separated by `|`. Empty if none. |  |
| actions_ran | string | Successful post-processing actions, separated by `|`. Empty if none. |  |
| verdicts | array[string] | Aggregated verdicts for the blocked leaf file. |  |
| yara_info | object | YARA scan results for the blocked leaf file. |  |
| hits | array[string] | Matched YARA rules. |  |
| limit_reached | boolean | Indicates whether more than 100 blocked leaf files were found. |  |
| total | integer | Number of blocked leaf files returned in the `details` array. |  |

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response sample
### Fetch the Top 100 Extraction Errors in an Archive

Returns up to 100 extraction errors found while processing the archive identified by `data_id`, including errors from nested archives.
The response includes:

- `total`: Number of archives (root and nested) that reported extraction errors.
- `root_archive`: Extraction error details for the top-level archive. Omitted if no root-level errors exist.
- `nested_archives`: Extraction error details for nested archives.

If no extraction errors are found:

- `total` is 0.
- `nested_archives` may be empty.
- `root_archive` may be omitted.

If the archive result was reused from a previous analysis, the API returns the extraction errors from that analysis. You can identify this case when `original_data_id` is set in the `GET /file/{data_id}` response. The first segment of each `archive_path` is updated to use the name of the requested file. This behavior is available starting with MetaDefender Cluster 2.10.0.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| data_id | string | Data identifier of the original (root) archive file. |  |
| --- | --- | --- | --- |

GET /file/{data_id}/extraction-errorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Extraction error information for the specified archive.

| object | object |  |  |
| --- | --- | --- | --- |
| total | integer | Total count of archives (root and nested) that have extraction errors. |  |
| root_archive3 fields | object | Error details for the root archive (present only if the root archive has an error). |  |
| err_category | string | High-level error category. |  |
| err_details | string | Detailed diagnostic message. |  |
| err_description | string | Human-readable description of the error. |  |
| nested_archives5 fields | array[object] | List of nested archives that encountered extraction errors. |  |
| data_id | string | Data identifier of the nested archive. |  |
| archive_path | array[string] | Ordered path segments from the root archive to this nested archive. |  |
| err_category | string | High-level error category. |  |
| err_details | string | Detailed diagnostic message. |  |
| err_description | string | Human-readable description of the nested archive issue. |  |

400

Invalid request (e.g. malformed data_id or bad query parameters).

404

Requests resource was not found.

405

The user has no rights for this operation.

423

The file is still being processed; extraction errors not finalized yet.

500

Unexpected event on server.

 Response sample
### Query webhook status

Prior to being notified when webhook mode is enabled, the client can request MetaDefender Cluster API Gateway for the file processing webhook status at any time.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| data_id | string | The `data_id` of the file to query. |  |
| --- | --- | --- | --- |

GET /file/webhook/{data_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Webhook status is fetched successfully.

| object | object |  |  |
| --- | --- | --- | --- |
| data_id | string | The file submission identifier |  |
| request_time | string | A timestamp when the request has been made. |  |
| status_code | integer | What was the returned HTTP status code.   - `200` - Callback was sent successfully - `403` - ContentAccessDenied. The access to the remote content was denied (similar to HTTP(S) error 401). - `404` - ContentNotFoundError. The remote content was not found at the server (similar to HTTP(S) error 404). - `408` - TimeoutError. The connection to the remote server timed out. - `503` - HostNotFoundError. The remote host name was not found (invalid hostname). - `520` - RemoteHostClosedError. The remote server closed the connection prematurely, before the entire reply was received and processed. - `444` - Other error types. |  |
| url | string | What was the called URL (should match the `callbackurl` header). |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

500

Unexpected event on server.

 Response
## Batch

Group the analysis requests in batches.
Supported with endpoints: MetaDefender Cluster API Gateway.

Endpoints[POST/file/batch](/docs/mdcluster/api-gateway#batchcreate) [POST/file/batch/{batchId}/close](/docs/mdcluster/api-gateway#batchclose) [GET/file/batch/{batchId}](/docs/mdcluster/api-gateway#batchstatus) [GET/file/batch/{batchId}/certificate](/docs/mdcluster/api-gateway#batchsignedresult) [POST/file/batch/{batchId}/cancel](/docs/mdcluster/api-gateway#batchcancel)
### Initiate Batch

Create a new batch and retrieve the batch_id

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| rule | string | Select rule for the analysis, if no header given the default rule will be selected (URL encoded UTF-8 string of rule name) |  |
| user_agent | string | user_agent header used to identify (and limit) access to a particular rule. For rule selection, `rule` header should be used. |  |
| user-data | string | Name of the batch (max 1024 bytes, URL encoded UTF-8 string). |  |
| client-identity | string | The `client-identity` header identifies the clients involved in processing a file, providing greater visibility into its processing stages. The header value is a JSON object containing a clients array. Each `client` object supports the following fields:   - `deployment_id`: *REQUIRED*. Unique identifier of the deployment. - `user_name`: *REQUIRED*. Name of the user or system that initiated the scan. - `product_type`: *REQUIRED*. Type of product or system performing the scan. - `version`: *OPTIONAL*. Version of the product or system. - `host`: *OPTIONAL*. Hostname or IP address of the client machine. - `timestamp`: *REQUIRED*. Time at which the scan was initiated, expressed in milliseconds since the Unix epoch.   Example:   ```   {   "clients":    [   {     "deployment_id": "abcdef1234567890",     "user_name": "Gemini",     "product_type": "MetaDefender Kiosk",     "version": "1.0.0",     "host": "client.example.com",     "timestamp": 1744949754890   }   ]   }   ```   URL-encode the JSON value before sending the header to MetaDefender Cluster to avoid issues caused by unsafe characters or incorrect encoding. Omit the header when client identity tracking is not required. |  |

Expand POST /file/batchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Batch created successfully.

| object | object |  |  |
| --- | --- | --- | --- |
| batch_id | string | The batch identifier used to submit files in the batch and to close the batch. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or
out of range, etc). The request is rejected before the file is processed, so no `data_id` is
created.

When the `client-identity` header is present but its value is invalid, `err` is one of:

| `err` | Cause |
| --- | --- |
| `Header 'client-identity' is empty` | The header was sent without a value. |
| `Header 'client-identity' must be less than or equal 4096 characters` | The header value is longer than 4096 characters. |
| `Header 'client-identity' contains non-printable character` | The value contains an ASCII control character, either directly or through an escape. |
| `Header 'client-identity' is not in JSON format` | The value could not be URL-decoded, is not valid JSON, or is not a JSON object. |
| `Header 'client-identity' does not contain a 'clients' key or empty 'clients'` | `clients` is missing, is not an array, or is an empty array. |
| `Header 'client-identity' contains an invalid data` | An entry of `clients` is not a JSON object. |
| `Header 'client-identity' does not contain required key '<key>'` | An entry is missing `deployment_id`, `user_name`, `product_type` or `timestamp`. |
| `Header 'client-identity' contains a non-string '<key>'` | `deployment_id`, `user_name` or `product_type` is not a string. |
| `Header 'client-identity' contains an empty '<key>'` | `deployment_id`, `user_name` or `product_type` is blank. |
| `Header 'client-identity' contains an invalid 'deployment_id'` | `deployment_id` holds anything other than letters and digits. |
| `Header 'client-identity' contains a non-integer 'timestamp'` | `timestamp` is not an integer. |
| `Header 'client-identity' contains a negative 'timestamp'` | `timestamp` is zero or negative. |

Every entry of `clients` is checked, not only the first one, and the first rule that fails is the
one reported.

403

Invalid user information or Not Allowed

500

Unexpected event on server.

 Response
### Close Batch

The batch will be closed and files can no longer be added to the current batch.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| batchId | string | The batch identifier used to submit files in the batch and to close the batch. |  |
| --- | --- | --- | --- |

POST /file/batch/{batchId}/closecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Batch successfully closed.

| object | object | The response for a Batch status request. |  |
| --- | --- | --- | --- |
| batch_files5 fields | object | Information about the files included in this batch. |  |
| batch_count | integer | The total number of files/entries in the batch. |  |
| current_finished_files | integer | The total number of files/entries that have been fully processed in the batch. |  |
| files_in_batch11 fields | array[object] | The list of files in the batch. |  |
| data_id | string | Unique identifer for the file. |  |
| detected_by | integer | Total number of engines that detected this file. |  |
| display_name | string | The filename reported via `filename` header. |  |
| file_size | integer | Total file size in bytes. |  |
| file_type | string | The filetype using mimetype. |  |
| file_type_description | string | The filetype in human readable format. |  |
| process_info5 fields | object | The analysis summary |  |
| blocked_reason | string | Provides the reason why the file is blocked (if so). |  |
| progress_percentage | integer | Percentage of processing completed (from 1-100). |  |
| result | string | The final result of processing the file (Allowed / Blocked / Processing). |  |
| verdicts | array[string] | Aggregated list of potential issues. |  |
| client_identity1 field | object | The `client-identity` helps track and understand the workflow that a file passes through clients, offering greater visibility into the processing stages and the clients involved. |  |
| clients6 fields | array[object] | Array of client identity objects. |  |
| deployment_id | string | Unique identifier for the deployment. |  |
| user_name | string | Name of the user or system that initiated the scan. |  |
| product_type | string | Type of product or system that is performing the scan. |  |
| version | string | Version of the product or system. |  |
| host | string | Hostname or IP address of the client machine. |  |
| timestamp | integer | Timestamp of when the scan was initiated, in milliseconds since epoch. |  |
| progress_percentage | integer | Track analysis progress until reaches 100. |  |
| scan_all_result_a | string | Processing result and its index   - `No Threat Detected`: 0 - `Infected`: 1 - `Suspicious`: 2 - `Failed`: 3 - `Whitelisted`: 7 - `Blacklisted`: 8 - `Exceeded Archive Depth`: 9 - `Not Scanned`: 10 - `Encrypted Archive`: 12 - `Exceeded Archive Size`: 13 - `Exceeded Archive File Number`: 14 - `Password Protected Document`: 15 - `Exceeded Archive Timeout`: 16 - `Mismatch`: 17 - `Potentially Vulnerable File`: 18 - `Cancelled`: 19 - `Sensitive Data Found`: 20 - `Yara Rule Matched`: 21 - `Potentially Unwanted`: 22 - `Unsupported File Type`: 23 - `Extraction Failed`: 24 - `Scan Failed`: 25 - `Suspicious Verdict by Sandbox`: 26 - `Likely Malicious Verdict by Sandbox`: 27 - `Malicious Verdict by Sandbox`: 28 - `Blocked Verdict by Sandbox`: 29 - `Blocked Verdict by Deep CDR`: 30 - `Global Timeout Exceeded`: 31 - `Vulnerable Verdict by SBOM`: 32 - `Non-vulnerable Verdict by SBOM`: 33 - `Blocked Verdict by SBOM`: 34 - `Blocked by Post Action`: 36 - `Known Bad`: 38 - `Known Good`: 39 - `Unknown`: 40 - `Allowed Verdict by COO`: 41 - `Blocked Verdict by COO`: 42 - `Unknown Verdict by COO`: 43 - `OPSWAT AI Confidently Clean`: 67 - `OPSWAT AI Confidently Malicious`: 68 - `OPSWAT AI Undetermined`: 69 - `Download Timeout`: 70 - `Download Failed`: 71 - `In Progress`: 255 - `Skip Processing Fast Symlink`: 1014   Enum: `No Threat Detected`,`Infected`,`Suspicious`,`Failed`,`Whitelisted`,`Blacklisted`,`Exceeded Archive Depth`,`Not Scanned`,`Encrypted Archive`,`Exceeded Archive Size`,`Exceeded Archive File Number`,`Password Protected Document`,`Exceeded Archive Timeout`,`Mismatch`,`Potentially Vulnerable File`,`Cancelled`,`Sensitive Data Found`,`Yara Rule Matched`,`Potentially Unwanted`,`Unsupported File Type`,`Extraction Failed`,`Scan Failed`,`Suspicious Verdict by Sandbox`,`Likely Malicious Verdict by Sandbox`,`Malicious Verdict by Sandbox`,`Blocked Verdict by Sandbox`,`Blocked Verdict by Deep CDR`,`Global Timeout Exceeded`,`Vulnerable Verdict by SBOM`,`Non-vulnerable Verdict by SBOM`,`Blocked Verdict by SBOM`,`Blocked by Post Action`,`Known Bad`,`Known Good`,`Unknown`,`Allowed Verdict by COO`,`Blocked Verdict by COO`,`Unknown Verdict by COO`,`OPSWAT AI Confidently Clean`,`OPSWAT AI Confidently Malicious`,`OPSWAT AI Undetermined`,`Download Timeout`,`Download Failed`,`In Progress`,`Skip Processing Fast Symlink` |  |
| scan_all_result_i | integer | Scan result as index in the Processing Results table above  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`67`,`68`,`69`,`70`,`71`,`255`,`1014` |  |
| scanned_with | integer | The total number of engines used to analyze this file. |  |
| first_index | integer | The starting index in the batch. Used for pagination. |  |
| page_size | integer | The number of entries per page. |  |
| batch_id | string | The batch unique identifer |  |
| is_closed | boolean | The batch status (open/close). |  |
| process_info7 fields | object | Overall batch process result |  |
| blocked_reason | string | Provides the reason why the file is blocked (if so). |  |
| file_type_skipped_scan | boolean | Indicates if the input file's detected type was configured to skip scanning. |  |
| profile | string | The used rule name. |  |
| result | string | The final result of processing the file (Allowed / Blocked / Processing). |  |
| user_agent | string | Identifier for the REST Client that calls the API. |  |
| username | string | User identifier who submitted scan request earlier. |  |
| client_identity1 field | object | The `client-identity` helps track and understand the workflow that a file passes through clients, offering greater visibility into the processing stages and the clients involved. |  |
| clients6 fields | array[object] | Array of client identity objects. |  |
| deployment_id | string | Unique identifier for the deployment. |  |
| user_name | string | Name of the user or system that initiated the scan. |  |
| product_type | string | Type of product or system that is performing the scan. |  |
| version | string | Version of the product or system. |  |
| host | string | Hostname or IP address of the client machine. |  |
| timestamp | integer | Timestamp of when the scan was initiated, in milliseconds since epoch. |  |
| scan_results6 fields | object | Metascan analysis result. |  |
| batch_id | string | The batch unique identifer |  |
| scan_all_result_a | string | Processing result and its index   - `No Threat Detected`: 0 - `Infected`: 1 - `Suspicious`: 2 - `Failed`: 3 - `Whitelisted`: 7 - `Blacklisted`: 8 - `Exceeded Archive Depth`: 9 - `Not Scanned`: 10 - `Encrypted Archive`: 12 - `Exceeded Archive Size`: 13 - `Exceeded Archive File Number`: 14 - `Password Protected Document`: 15 - `Exceeded Archive Timeout`: 16 - `Mismatch`: 17 - `Potentially Vulnerable File`: 18 - `Cancelled`: 19 - `Sensitive Data Found`: 20 - `Yara Rule Matched`: 21 - `Potentially Unwanted`: 22 - `Unsupported File Type`: 23 - `Extraction Failed`: 24 - `Scan Failed`: 25 - `Suspicious Verdict by Sandbox`: 26 - `Likely Malicious Verdict by Sandbox`: 27 - `Malicious Verdict by Sandbox`: 28 - `Blocked Verdict by Sandbox`: 29 - `Blocked Verdict by Deep CDR`: 30 - `Global Timeout Exceeded`: 31 - `Vulnerable Verdict by SBOM`: 32 - `Non-vulnerable Verdict by SBOM`: 33 - `Blocked Verdict by SBOM`: 34 - `Blocked by Post Action`: 36 - `Known Bad`: 38 - `Known Good`: 39 - `Unknown`: 40 - `Allowed Verdict by COO`: 41 - `Blocked Verdict by COO`: 42 - `Unknown Verdict by COO`: 43 - `OPSWAT AI Confidently Clean`: 67 - `OPSWAT AI Confidently Malicious`: 68 - `OPSWAT AI Undetermined`: 69 - `Download Timeout`: 70 - `Download Failed`: 71 - `In Progress`: 255 - `Skip Processing Fast Symlink`: 1014   Enum: `No Threat Detected`,`Infected`,`Suspicious`,`Failed`,`Whitelisted`,`Blacklisted`,`Exceeded Archive Depth`,`Not Scanned`,`Encrypted Archive`,`Exceeded Archive Size`,`Exceeded Archive File Number`,`Password Protected Document`,`Exceeded Archive Timeout`,`Mismatch`,`Potentially Vulnerable File`,`Cancelled`,`Sensitive Data Found`,`Yara Rule Matched`,`Potentially Unwanted`,`Unsupported File Type`,`Extraction Failed`,`Scan Failed`,`Suspicious Verdict by Sandbox`,`Likely Malicious Verdict by Sandbox`,`Malicious Verdict by Sandbox`,`Blocked Verdict by Sandbox`,`Blocked Verdict by Deep CDR`,`Global Timeout Exceeded`,`Vulnerable Verdict by SBOM`,`Non-vulnerable Verdict by SBOM`,`Blocked Verdict by SBOM`,`Blocked by Post Action`,`Known Bad`,`Known Good`,`Unknown`,`Allowed Verdict by COO`,`Blocked Verdict by COO`,`Unknown Verdict by COO`,`OPSWAT AI Confidently Clean`,`OPSWAT AI Confidently Malicious`,`OPSWAT AI Undetermined`,`Download Timeout`,`Download Failed`,`In Progress`,`Skip Processing Fast Symlink` |  |
| scan_all_result_i | integer | Scan result as index in the Processing Results table above  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`67`,`68`,`69`,`70`,`71`,`255`,`1014` |  |
| start_time | string | Timestamp when the scanning process starts. |  |
| total_avs | integer | Total number of scanning engines used as part of this analysis. Not like files, batch is not processed by engine, so this value is always 0. |  |
| total_time | integer | Total time elapsed during scan (in milliseconds). |  |
| user_data | string | Metadata submitted at batch creation. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

500

Unexpected event on server.

 Response
### Status of Batch Analysis

Retrieve status report for the entire batch

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| batchId | string | The batch identifier used to submit files in the batch and to close the batch. |  |
| --- | --- | --- | --- |

Query String

| first | integer | The first item order in the list of files in this batch  minimum: 0  Default: 0 |  |
| --- | --- | --- | --- |
| size | integer | The number of items to be fetched next, counting from the item order indicated in `first` header. The default value is 50, and the maximum value is 2000.  maximum: 2000  minimum: 0  Default: 50 |  |

GET /file/batch/{batchId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Batch progress paginated report (50 entries/page).

| object | object | The response for a Batch status request. |  |
| --- | --- | --- | --- |
| batch_files5 fields | object | Information about the files included in this batch. |  |
| batch_count | integer | The total number of files/entries in the batch. |  |
| current_finished_files | integer | The total number of files/entries that have been fully processed in the batch. |  |
| files_in_batch11 fields | array[object] | The list of files in the batch. |  |
| data_id | string | Unique identifer for the file. |  |
| detected_by | integer | Total number of engines that detected this file. |  |
| display_name | string | The filename reported via `filename` header. |  |
| file_size | integer | Total file size in bytes. |  |
| file_type | string | The filetype using mimetype. |  |
| file_type_description | string | The filetype in human readable format. |  |
| process_info5 fields | object | The analysis summary |  |
| blocked_reason | string | Provides the reason why the file is blocked (if so). |  |
| progress_percentage | integer | Percentage of processing completed (from 1-100). |  |
| result | string | The final result of processing the file (Allowed / Blocked / Processing). |  |
| verdicts | array[string] | Aggregated list of potential issues. |  |
| client_identity1 field | object | The `client-identity` helps track and understand the workflow that a file passes through clients, offering greater visibility into the processing stages and the clients involved. |  |
| clients6 fields | array[object] | Array of client identity objects. |  |
| deployment_id | string | Unique identifier for the deployment. |  |
| user_name | string | Name of the user or system that initiated the scan. |  |
| product_type | string | Type of product or system that is performing the scan. |  |
| version | string | Version of the product or system. |  |
| host | string | Hostname or IP address of the client machine. |  |
| timestamp | integer | Timestamp of when the scan was initiated, in milliseconds since epoch. |  |
| progress_percentage | integer | Track analysis progress until reaches 100. |  |
| scan_all_result_a | string | Processing result and its index   - `No Threat Detected`: 0 - `Infected`: 1 - `Suspicious`: 2 - `Failed`: 3 - `Whitelisted`: 7 - `Blacklisted`: 8 - `Exceeded Archive Depth`: 9 - `Not Scanned`: 10 - `Encrypted Archive`: 12 - `Exceeded Archive Size`: 13 - `Exceeded Archive File Number`: 14 - `Password Protected Document`: 15 - `Exceeded Archive Timeout`: 16 - `Mismatch`: 17 - `Potentially Vulnerable File`: 18 - `Cancelled`: 19 - `Sensitive Data Found`: 20 - `Yara Rule Matched`: 21 - `Potentially Unwanted`: 22 - `Unsupported File Type`: 23 - `Extraction Failed`: 24 - `Scan Failed`: 25 - `Suspicious Verdict by Sandbox`: 26 - `Likely Malicious Verdict by Sandbox`: 27 - `Malicious Verdict by Sandbox`: 28 - `Blocked Verdict by Sandbox`: 29 - `Blocked Verdict by Deep CDR`: 30 - `Global Timeout Exceeded`: 31 - `Vulnerable Verdict by SBOM`: 32 - `Non-vulnerable Verdict by SBOM`: 33 - `Blocked Verdict by SBOM`: 34 - `Blocked by Post Action`: 36 - `Known Bad`: 38 - `Known Good`: 39 - `Unknown`: 40 - `Allowed Verdict by COO`: 41 - `Blocked Verdict by COO`: 42 - `Unknown Verdict by COO`: 43 - `OPSWAT AI Confidently Clean`: 67 - `OPSWAT AI Confidently Malicious`: 68 - `OPSWAT AI Undetermined`: 69 - `Download Timeout`: 70 - `Download Failed`: 71 - `In Progress`: 255 - `Skip Processing Fast Symlink`: 1014   Enum: `No Threat Detected`,`Infected`,`Suspicious`,`Failed`,`Whitelisted`,`Blacklisted`,`Exceeded Archive Depth`,`Not Scanned`,`Encrypted Archive`,`Exceeded Archive Size`,`Exceeded Archive File Number`,`Password Protected Document`,`Exceeded Archive Timeout`,`Mismatch`,`Potentially Vulnerable File`,`Cancelled`,`Sensitive Data Found`,`Yara Rule Matched`,`Potentially Unwanted`,`Unsupported File Type`,`Extraction Failed`,`Scan Failed`,`Suspicious Verdict by Sandbox`,`Likely Malicious Verdict by Sandbox`,`Malicious Verdict by Sandbox`,`Blocked Verdict by Sandbox`,`Blocked Verdict by Deep CDR`,`Global Timeout Exceeded`,`Vulnerable Verdict by SBOM`,`Non-vulnerable Verdict by SBOM`,`Blocked Verdict by SBOM`,`Blocked by Post Action`,`Known Bad`,`Known Good`,`Unknown`,`Allowed Verdict by COO`,`Blocked Verdict by COO`,`Unknown Verdict by COO`,`OPSWAT AI Confidently Clean`,`OPSWAT AI Confidently Malicious`,`OPSWAT AI Undetermined`,`Download Timeout`,`Download Failed`,`In Progress`,`Skip Processing Fast Symlink` |  |
| scan_all_result_i | integer | Scan result as index in the Processing Results table above  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`67`,`68`,`69`,`70`,`71`,`255`,`1014` |  |
| scanned_with | integer | The total number of engines used to analyze this file. |  |
| first_index | integer | The starting index in the batch. Used for pagination. |  |
| page_size | integer | The number of entries per page. |  |
| batch_id | string | The batch unique identifer |  |
| is_closed | boolean | The batch status (open/close). |  |
| process_info7 fields | object | Overall batch process result |  |
| blocked_reason | string | Provides the reason why the file is blocked (if so). |  |
| file_type_skipped_scan | boolean | Indicates if the input file's detected type was configured to skip scanning. |  |
| profile | string | The used rule name. |  |
| result | string | The final result of processing the file (Allowed / Blocked / Processing). |  |
| user_agent | string | Identifier for the REST Client that calls the API. |  |
| username | string | User identifier who submitted scan request earlier. |  |
| client_identity1 field | object | The `client-identity` helps track and understand the workflow that a file passes through clients, offering greater visibility into the processing stages and the clients involved. |  |
| clients6 fields | array[object] | Array of client identity objects. |  |
| deployment_id | string | Unique identifier for the deployment. |  |
| user_name | string | Name of the user or system that initiated the scan. |  |
| product_type | string | Type of product or system that is performing the scan. |  |
| version | string | Version of the product or system. |  |
| host | string | Hostname or IP address of the client machine. |  |
| timestamp | integer | Timestamp of when the scan was initiated, in milliseconds since epoch. |  |
| scan_results6 fields | object | Metascan analysis result. |  |
| batch_id | string | The batch unique identifer |  |
| scan_all_result_a | string | Processing result and its index   - `No Threat Detected`: 0 - `Infected`: 1 - `Suspicious`: 2 - `Failed`: 3 - `Whitelisted`: 7 - `Blacklisted`: 8 - `Exceeded Archive Depth`: 9 - `Not Scanned`: 10 - `Encrypted Archive`: 12 - `Exceeded Archive Size`: 13 - `Exceeded Archive File Number`: 14 - `Password Protected Document`: 15 - `Exceeded Archive Timeout`: 16 - `Mismatch`: 17 - `Potentially Vulnerable File`: 18 - `Cancelled`: 19 - `Sensitive Data Found`: 20 - `Yara Rule Matched`: 21 - `Potentially Unwanted`: 22 - `Unsupported File Type`: 23 - `Extraction Failed`: 24 - `Scan Failed`: 25 - `Suspicious Verdict by Sandbox`: 26 - `Likely Malicious Verdict by Sandbox`: 27 - `Malicious Verdict by Sandbox`: 28 - `Blocked Verdict by Sandbox`: 29 - `Blocked Verdict by Deep CDR`: 30 - `Global Timeout Exceeded`: 31 - `Vulnerable Verdict by SBOM`: 32 - `Non-vulnerable Verdict by SBOM`: 33 - `Blocked Verdict by SBOM`: 34 - `Blocked by Post Action`: 36 - `Known Bad`: 38 - `Known Good`: 39 - `Unknown`: 40 - `Allowed Verdict by COO`: 41 - `Blocked Verdict by COO`: 42 - `Unknown Verdict by COO`: 43 - `OPSWAT AI Confidently Clean`: 67 - `OPSWAT AI Confidently Malicious`: 68 - `OPSWAT AI Undetermined`: 69 - `Download Timeout`: 70 - `Download Failed`: 71 - `In Progress`: 255 - `Skip Processing Fast Symlink`: 1014   Enum: `No Threat Detected`,`Infected`,`Suspicious`,`Failed`,`Whitelisted`,`Blacklisted`,`Exceeded Archive Depth`,`Not Scanned`,`Encrypted Archive`,`Exceeded Archive Size`,`Exceeded Archive File Number`,`Password Protected Document`,`Exceeded Archive Timeout`,`Mismatch`,`Potentially Vulnerable File`,`Cancelled`,`Sensitive Data Found`,`Yara Rule Matched`,`Potentially Unwanted`,`Unsupported File Type`,`Extraction Failed`,`Scan Failed`,`Suspicious Verdict by Sandbox`,`Likely Malicious Verdict by Sandbox`,`Malicious Verdict by Sandbox`,`Blocked Verdict by Sandbox`,`Blocked Verdict by Deep CDR`,`Global Timeout Exceeded`,`Vulnerable Verdict by SBOM`,`Non-vulnerable Verdict by SBOM`,`Blocked Verdict by SBOM`,`Blocked by Post Action`,`Known Bad`,`Known Good`,`Unknown`,`Allowed Verdict by COO`,`Blocked Verdict by COO`,`Unknown Verdict by COO`,`OPSWAT AI Confidently Clean`,`OPSWAT AI Confidently Malicious`,`OPSWAT AI Undetermined`,`Download Timeout`,`Download Failed`,`In Progress`,`Skip Processing Fast Symlink` |  |
| scan_all_result_i | integer | Scan result as index in the Processing Results table above  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`67`,`68`,`69`,`70`,`71`,`255`,`1014` |  |
| start_time | string | Timestamp when the scanning process starts. |  |
| total_avs | integer | Total number of scanning engines used as part of this analysis. Not like files, batch is not processed by engine, so this value is always 0. |  |
| total_time | integer | Total time elapsed during scan (in milliseconds). |  |
| user_data | string | Metadata submitted at batch creation. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

500

Unexpected event on server.

 Response
### Download Signed Batch Result

Download digitally signed status report for the entire batch

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| metadata | string | In JSON format, this can be used to:  Include additional information in the response YML. Currently, one supported field in the metadata is `include_vul_info`, which can be set to `true` or `false` to indicate whether vulnerability processing information should be included or not. It is strongly recommended to apply URL encoding before sending `metadata` to Metadefender Cluster API Gateway to prevent unexpected issues related to encoding errors or unsafe characters. |  |

Path Params

| batchId | string | The batch identifier used to submit files in the batch and to close the batch. |  |
| --- | --- | --- | --- |

GET /file/batch/{batchId}/certificatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/x-yaml 200

Signed batch result and certificate are sent back in response body (YAML format).

| No response body |
| --- |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

500

Unexpected event on server.

 Response
### Cancel Batch

When cancelling a batch, the connected analysis that are still in progress will be cancelled also.

The cancelled batch will be closed.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Path Params

| batchId | string | The batch identifier used to submit files in the batch and to close the batch. |  |
| --- | --- | --- | --- |

POST /file/batch/{batchId}/cancelcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Batch cancelled.

| object | object |  |  |
| --- | --- | --- | --- |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Batch not found (invalid id)

500

Unexpected event on server.

 Response
## License

Retrieve the current license information.

Endpoints[GET/admin/license](/docs/mdcluster/api-gateway#licenseget)
### Get current license information

Fetch details about the longest expiry active license among all activated licenses.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/licensecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Information about the licensed product (product type, number of activations, deploymentId, expiration date and days left)

| object | object | Information about the licensed product (product type, number of activations, deploymentId, expiration date and days left) |  |
| --- | --- | --- | --- |
| days_left | integer | Number of days left before expiration |  |
| expiration | string | Expiration date in MM/DD/YYYY format. |  |
| licensed_engines | array[string] | List of engine/module identifiers that have been licensed |  |
| licensed_to | string | Name of the entity to which the license is issued. |  |
| max_agent_count | string | Total number of deployed MetaDefender Agents attached to this MetaDefender Core instance. |  |
| online_activated | boolean | Track online/offline activation mode |  |
| product_id | string | Official MetaDefender base SKU licensed. |  |
| product_name | string | Official MetaDefender base product name licensed. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
## Stats

Health check and statistics about MetaDefender Core instance usage.

Endpoints[GET/stat/engines](/docs/mdcluster/api-gateway#enginesstatus) [GET/stat/nodes](/docs/mdcluster/api-gateway#nodesstatus) [GET/readyz](/docs/mdcluster/api-gateway#healthcheck)
### Engine Status

Return the status of the latest engines between the MetaDefender Core instances.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /stat/enginescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

An array with all the engines and their details.

| array | array[object] |  |  |
| --- | --- | --- | --- |
| abandoned | boolean | Indicates if this engine is abandoned. |  |
| active | boolean | If used by at least one engine |  |
| def_time | string | The database definition time for this engine |  |
| download_progress | integer | The percentage progress of download |  |
| download_time | string | When this engine downloaded from the update server. |  |
| eng_id | string | Engine internal ID |  |
| eng_name | string | Engine name |  |
| eng_type | string | Engine type in human readable form |  |
| eng_ver | string | Engine's version (format differs from one engine to another). |  |
| engine_type | string | Engine's type:   - av - archive - filetype   Enum: `av`,`archive`,`filetype` |  |
| pinned | boolean | Indicate if this engine is pinned. |  |
| state | string | Status of the engine:   - downloading - downloaded - staging - production - removed - temporary failed - permanently failed - content invalid - download failed   Enum: `downloading`,`downloaded`,`staging`,`production`,`removed`,`temporary failed`,`permanently failed`,`content invalid`,`download failed` |  |
| type | string | The type of information, whether it is engine or engine's database. |  |

Expand  Response
### Instance Status Overview

Retrieve status details of all available MetaDefender Core instances.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /stat/nodescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Status details of MetaDefender Core instances.

| object | object |  |  |
| --- | --- | --- | --- |
| external_nodes_allowed | boolean | Indicates whether external nodes can connect; always true. |  |
| max_node_count | integer | Total number of available MetaDefender Core instances. |  |
| statuses18 fields | array[object] | List of MetaDefender Core instance status details. |  |
| address | string | Location of the Core instance; currently always return empty string. |  |
| available_mem | integer | The number of available RAM in this system. |  |
| cpu_cores | integer | The number of CPU Cores allocated to this Core instance. |  |
| current_processing_files | integer | Number of objects currently being processed by the Core instance. |  |
| engines9 fields | array[object] | Summary of each engine status deployed on this Core. |  |
| active | boolean | If used by at least one engine |  |
| db_ver | string | The database version for this engine |  |
| def_time | string | The database definition time for this engine |  |
| download_time | string | The database download time for this engine |  |
| eng_name | string | Engine name |  |
| eng_ver | string | Engine's version (format differs from one engine to another). |  |
| engine_type | string | Engine's type:   - av - archive - filetype   Enum: `av`,`archive`,`filetype` |  |
| id | string | Engine internal ID |  |
| free_disk_space | integer | Reported available disk on Core instance (in bytes). |  |
| id | string | Identifier of the worker that deployed this Core instance. |  |
| info_disk_space4 fields | array[object] | Report disk space usage from the host where the MetaDefender Core instance is installed. |  |
| free | integer | Free space on the disk (in bytes). |  |
| location | string | Disk location. |  |
| total | integer | Total space on the disk (in bytes). |  |
| issues | array[object] | A list of all potential problems on Core instance. |  |
| description | string | Text detailing the issue. |  |
| severity | string | How important is the reported issue. |  |
| load | integer | Current CPU utilization on Core instance (in percentage). |  |
| os | string | Current used OS |  |
| scan_queue | integer | Number of objects currently being processed by the Core instance. |  |
| scan_queue_details5 fields | object | Current load of scan queue in details |  |
| archive_scan_queue_ratio | number | Ratio of archive scan queue, always -1 for Core in Cluster mode. |  |
| available_slots | integer | The number of slots is available, always -1 for Core in Cluster mode. |  |
| extracted_file_slots | integer | Number of child files being processing |  |
| file_slots | integer | Number of files taken from REST by the current Core instance |  |
| total_scan_queue | integer | Total scan queue, always -1 for Core in Cluster mode. |  |
| total_disk_space | integer | The amount of disk space is allocated on Core instance (in Byte). |  |
| total_mem | integer | How much memory is allocated on Core instance (in MB). |  |
| total_scan_queue | integer | The maximum queue size is allowed, always -1 for Core in Cluster mode. |  |
| uptime | integer | How long this Core is in operation (in second). |  |
| version | string | Product version |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

 Response
### Get health check status

Fetch current status of system health.

Auth NoneQuery String

| verbose | boolean | Optional. Show detailed result of system health. |  |
| --- | --- | --- | --- |

GET /readyzcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

System is currently healthy.

| object | object | System readiness / health status. |  |
| --- | --- | --- | --- |
| status | boolean | System-wide status, indicate if all components are healthy. |  |
| scan_queue | object | Scan queue status. |  |
| number_in_queue | integer | Number of objects being processed by the system. |  |
| status | boolean | The operational status of the scan process; true if the system contains the required minimum of healthy MetaDefender Core instances. |  |
| license | object | License status. |  |
| status | string | License status.  Enum: `expired`,`invalid`,`ok` |  |
| components7 fields | object | Core component statuses. |  |
| status | boolean | Aggregate component status. |  |
| clusterdb | object | Configuration database status. |  |
| status | boolean | Configuration database overall status. |  |
| detail | string | Status detail message. |  |
| datalake | object | DataLake status. |  |
| status | boolean | DataLake overall status. |  |
| detail | string | Status detail message |  |
| caching | object | Caching status. |  |
| status | boolean | Caching overall status. |  |
| detail | string | Status detail message. |  |
| broker | object | Broker status. |  |
| status | boolean | Broker overall status. |  |
| detail | string | Status detail message. |  |
| filestorage | object | MetaDefender Cluster File storage status. |  |
| status | boolean | MetaDefender Cluster File storage overall status. |  |
| detail | string | Status detail message. |  |
| identity | object | MetaDefender Cluster Identity service status. |  |
| status | boolean | MetaDefender Cluster Identity service overall status. |  |
| detail | string | Status detail message. |  |
| ometascan3 fields | object | Status of MetaDefender Core instances |  |
| status | boolean | MetaDefender Core overall status. |  |
| detail | string | Detail message. |  |
| instance | array[string] | List of instance status. |  |
| callback-service | object | Webhook callback service status. |  |
| status | boolean | Callback service overall status. |  |
| instance | array[string] | List of instance status. |  |
| download-service | object | MetaDefender Cluster Download Service status (scan from link). This status does not affect the overall system `status`: when it is unhealthy, only file submissions with the `downloadfrom` header are refused. |  |
| status | boolean | Download Service overall status. `true` when at least one instance is healthy, or when no instance is deployed. |  |
| instance | array[string] | List of instance status. |  |

Expand 500

Unexpected event on server.

503

System is currently unhealthy.

 Response
