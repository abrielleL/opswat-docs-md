<!-- source: https://www.opswat.com/docs/filescan/3.2.0/metadefender-sandbox-api-reference/ref -->

## Developer Guide

This is the API documentation for MetaDefender Sandbox. If you would like to evaluate or have any questions about this documentation, please contact us via our [Contact Us](https://www.opswat.com/contact) form.

## AuthenticationapiKey apiKeyFields

| Key | In |
| --- | --- |
| X-Api-Key | Header |  |

## Scan

Upload file or URL resource for scan

Endpoints[POST/api/scan/file](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#scan-file-api-scan-file-post) [POST/api/scan/url](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#scan-file-api-scan-url-post) [POST/api/scan/profiles](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#save-scan-profile-api-scan-profiles-post) [DELETE/api/scan/profiles/{profile_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-scan-profile-api-scan-profiles--profile-id--delete) [GET/api/scan/{flow_id}/report](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-all-upload-related-reports-api-scan--flow-id--report-get)
### Scan File

Perform scan of uploaded file

Auth apiKeyRequest Body multipart/form-data

| Body_scan_file_api_scan_file_post | object |  |  |
| --- | --- | --- | --- |
| file | file |  |  |
| description | string | Uploaded file/url description |  |
| tags | string | Tags array to propagate |  |
| propagate_tags | boolean | If tags from description should be added to produced report(s)  Default: true |  |
| password | string | Custom password, in case uploaded archive is protected |  |
| is_private | boolean | If file should not be available for download by other users  Default: false |  |
| is_private_report | boolean | If the report should not be available for other users  Default: false |  |
| skip_whitelisted | boolean | If file is detected as whitelisted, report is not created  Default: false |  |
| scan_profile | string | Id of scan profile, or name of preset scan profile |  |
| scan_engine | string | All possible scan engines that can be used  Enum: `internal`,`mdcloud` |  |
| rapid_mode | boolean | Disable some scan long-running features |  |
| early_termination | boolean | Terminates scan execution once a conclusive verdict is detected |  |
| osint | boolean | Enable OSINT (e.g. VirusTotal, ClamAV) lookups |  |
| extended_osint | boolean | Enable OSINT lookups on extracted IOCs |  |
| extracted_files_osint | boolean | Enable OSINT lookups on extracted files |  |
| visualization | boolean | Enable file visualization (e.g. PDF rendering) |  |
| files_download | boolean | Enable download of files from extracted URLs |  |
| resolve_domains | boolean | Enable resolving domains to IPs (DNS) |  |
| input_file_yara | boolean | Enable YARA rule matches on input file |  |
| extracted_files_yara | boolean | Enable YARA rule matches on extracted files |  |
| whois | boolean | Enable WHOIS record lookups |  |
| ips_meta | boolean | Enable meta-data lookups for extracted IPs |  |
| images_ocr | boolean | Enable OCR text recognition on extracted images |  |
| certificates | boolean | Extract certificates |  |
| url_analysis | boolean | Analyse domains and URLs, geolocation |  |
| extract_strings | boolean | Enable strings extraction |  |
| ocr_qr | boolean | Extract string with OCR and process QR codes |  |
| phishing_detection | boolean | Phishing detection for URLs, emails and HTML pages |  |

Expand POST /api/scan/filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScanResponse | object | Model for an initiated scan response |  |
| --- | --- | --- | --- |
| flow_id | string |  |  |
| priority3 fields | object | Priority part of the scan respoms model |  |
| applied | integer |  |  |
| max_posibble | integer |  |  |
| note | string |  |  |

400

Bad request

401

Not authorized

403

Forbidden

413

Content too large

422

Validation Error

429

Too many requests

 Response
### Scan URL

Scan URL resource

Auth apiKeyRequest Body application/x-www-form-urlencoded

| Body_scan_file_api_scan_url_post | object |  |  |
| --- | --- | --- | --- |
| url | string | Url of internet resource to be scanned |  |
| description | string | Uploaded file/url description |  |
| tags | string | Tags array to propagate |  |
| propagate_tags | boolean | If tags from description should be added to produced report(s)  Default: true |  |
| password | string | Custom password, in case uploaded archive is protected |  |
| is_private | boolean | If file should not be available for download by other users  Default: false |  |
| is_private_report | boolean | If the report should not be available for other users  Default: false |  |
| skip_whitelisted | boolean | If file is detected as whitelisted, report is not created  Default: false |  |
| scan_profile | string | Id of scan profile, or name of preset scan profile |  |
| scan_engine | string | All possible scan engines that can be used  Enum: `internal`,`mdcloud` |  |
| rapid_mode | boolean | Disable some scan long-running features |  |
| early_termination | boolean | Terminates scan execution once a conclusive verdict is detected |  |
| osint | boolean | Enable OSINT (e.g. VirusTotal, ClamAV) lookups |  |
| extended_osint | boolean | Enable OSINT lookups on extracted IOCs |  |
| extracted_files_osint | boolean | Enable OSINT lookups on extracted files |  |
| visualization | boolean | Enable file visualization (e.g. PDF rendering) |  |
| files_download | boolean | Enable download of files from extracted URLs |  |
| resolve_domains | boolean | Enable resolving domains to IPs (DNS) |  |
| input_file_yara | boolean | Enable YARA rule matches on input file |  |
| extracted_files_yara | boolean | Enable YARA rule matches on extracted files |  |
| whois | boolean | Enable WHOIS record lookups |  |
| ips_meta | boolean | Enable meta-data lookups for extracted IPs |  |
| images_ocr | boolean | Enable OCR text recognition on extracted images |  |
| certificates | boolean | Extract certificates |  |
| url_analysis | boolean | Analyse domains and URLs, geolocation |  |
| extract_strings | boolean | Enable strings extraction |  |
| ocr_qr | boolean | Extract string with OCR and process QR codes |  |
| phishing_detection | boolean | Phishing detection for URLs, emails and HTML pages |  |

Expand POST /api/scan/urlcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScanResponse | object | Model for an initiated scan response |  |
| --- | --- | --- | --- |
| flow_id | string |  |  |
| priority3 fields | object | Priority part of the scan respoms model |  |
| applied | integer |  |  |
| max_posibble | integer |  |  |
| note | string |  |  |

400

Bad request

401

Not authorized

403

Forbidden

422

Validation Error

429

Too many requests

 Response
### Save Scan Profile

Add/edit scan profile

Auth apiKeyRequest Body application/json

| ScanProfilePayload | object | User provided data to edit scan profile |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| is_default | boolean |  |  |
| options18 fields | object | Options to turn on/off various scan features |  |
| rapid_mode | boolean | Disable some scan long-running features |  |
| early_termination | boolean | Terminates scan execution once a conclusive verdict is detected |  |
| osint | boolean | Enable OSINT (e.g. VirusTotal, ClamAV) lookups |  |
| extended_osint | boolean | Enable OSINT lookups on extracted IOCs |  |
| extracted_files_osint | boolean | Enable OSINT lookups on extracted files |  |
| visualization | boolean | Visualize sample file and render document pages |  |
| files_download | boolean | Download and analyze files from embedded URLs |  |
| resolve_domains | boolean | Enable resolving domains to IPs (DNS) |  |
| input_file_yara | boolean | Enable YARA rule matches on input file |  |
| extracted_files_yara | boolean | Enable YARA rule matches on extracted files |  |
| whois | boolean | Enable WHOIS record lookups |  |
| ips_meta | boolean | Enable meta-data lookups for extracted IPs |  |
| images_ocr | boolean | Enable OCR text recognition on extracted images |  |
| certificates | boolean | Extract certificates |  |
| url_analysis | boolean | Analyse domains and URLs, geolocation |  |
| extract_strings | boolean | Enable strings extraction |  |
| ocr_qr | boolean | Extract string with OCR and process QR codes |  |
| phishing_detection | boolean | Phishing detection for URLs, emails and HTML pages |  |

POST /api/scan/profilescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

422

Validation Error

 Response
### Remove Scan Profile

Remove scan profile

Auth apiKeyPath Params

| profile_id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/scan/profiles/{profile_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

422

Validation Error

 Response
### Get All Upload Related Reports

Obtain all reports for given scan init. By default, if no `filter` parameter is sent, we only return some basic report data, just to see report is there

Auth apiKeyPath Params

| flow_id | string | Flow Id from scan-file |  |
| --- | --- | --- | --- |

Query String

| filter | array | Report fields that should be fetched. |  |
| --- | --- | --- | --- |
| sorting | array | Sort parameters to be applied to fetched report data |  |
| other | array | Extra options to get special data |  |

GET /api/scan/{flow_id}/reportcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AllUploadRelatedReportsResponse | object | Model for get_all_upload_related_reports() endpoint |  |
| --- | --- | --- | --- |
| flowId | string |  |  |
| allFinished | boolean |  |  |
| allFilesDownloadFinished | boolean |  |  |
| allAdditionalStepsDone | boolean |  |  |
| reportsAmount | integer |  |  |
| priority | string |  |  |
| pollPause | integer |  |  |
| state | string | Scan state of ScanInit instance  Enum: `created`,`queued`,`scanning`,`finished` |  |
| scanStartedDate | string |  |  |
| positionInQueue | integer |  |  |
| queueSize | integer |  |  |
| fileSize | integer |  |  |
| job | object | Model for job field in AllUploadRelatedReportsResponse |  |
| error | boolean |  |  |
| reason | string |  |  |
| fileReadProgressBytes | integer |  |  |
| rejected_files | array[object] |  |  |
| name | string |  |  |
| rejected_reason | string |  |  |
| sourceArchive11 fields | object | Model for sourceArchive field in AllUploadRelatedReportsResponse |  |
| scan_task_id | string |  |  |
| name | string |  |  |
| mimeType | string |  |  |
| sha256 | string |  |  |
| private | boolean |  |  |
| is_link_upload | boolean |  |  |
| sha1 | string |  |  |
| sha512 | string |  |  |
| md5 | string |  |  |
| tags2 fields | object | Model for tags field in AllUploadRelatedReportsResponse |  |
| source | string |  |  |
| tag | object | Model for tag field in TagsResponse |  |
| name | string |  |  |
| verdict | string |  |  |
| reports | object |  |  |
| * | object |  |  |

400

Bad request

404

Item not found

422

Validation Error

 Response Basic responseFiltered report
## Reports

Retrieve a variety of report related data

Endpoints[GET/api/reports/{report_id}/chat-gpt](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-chat-gpt-summary-api-reports--report-id--chat-gpt-get) [GET/api/reports/{report_id}/files](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-all-files-api-reports--report-id--files-get) [GET/api/reports/{report_id}/download/start](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#start-report-format-creation-api-reports--report-id--download-st) [GET/api/reports/{report_id}/download](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#download-export-formats-api-reports--report-id--download-get) [GET/api/users/me/downloads](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-downloads-list-api-users-me-downloads-get) [GET/api/reports/{report_id}/{file_hash}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-specific-report-api-reports--report-id---file-hash--get) [GET/api/files/pe-emulation/{report_id}/{file_name}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-pe-emulation-file-api-files-pe-emulation--report-id---file-n) [GET/api/reports/advanced-search](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#search-report-api-reports-advanced-search-get) [GET/api/reports/search](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#search-report-api-reports-search-get) [GET/api/reports](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-public-reports-api-reports-get) [GET/api/me/reports](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-reports-api-me-reports-get) [GET/api/me/reports/links](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-reports-links-api-me-reports-links-get) [GET/api/users/get-frequent-tags](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-frequent-tags-api-users-get-frequent-tags-get) [GET/api/users/most-interesting](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-most-interesting-api-users-most-interesting-get)
### Get Chat Gpt SummaryDeprecated

Request ChatGPT summary on report

Auth apiKeyPath Params

| report_id | string |  |  |
| --- | --- | --- | --- |

GET /api/reports/{report_id}/chat-gptcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ChatGptSummary | object | Summary generated for report by ChatGPT |  |
| --- | --- | --- | --- |
| data | string | Summary itself |  |
| created_date | date-time | Time of summary generation |  |

400

Bad request

404

Item not found

422

Validation Error

 Response
### Get All Files

Obtain all files for given report

Auth apiKeyPath Params

| report_id | string |  |  |
| --- | --- | --- | --- |

Query String

| type |  | Default: all |  |
| --- | --- | --- | --- |
| with_content | boolean | Compressed base64 data  Default: false |  |

GET /api/reports/{report_id}/filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportAllFilesResponse | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| hash | string |  |  |
| size | integer |  |  |
| mediaType | string |  |  |
| type | string | Smaller set of ReportFileType for the get_all_files() endpoint  Enum: `all`,`extracted`,`downloaded` |  |

404

Item not found

422

Validation Error

 Response
### Start Report Format Creation

Start creation of HTML or PDF formated report

Auth apiKeyPath Params

| report_id | string | Report Id |  |
| --- | --- | --- | --- |

Query String

| format | string | Enum: `html`,`pdf` |  |
| --- | --- | --- | --- |

GET /api/reports/{report_id}/download/startcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

404

Item not found

422

Validation Error

 Response
### Download Export Formats

Download the report in HTML, PDF, MISP and STIX format

Auth apiKeyPath Params

| report_id | string | Report Id |  |
| --- | --- | --- | --- |

Query String

| format | string | Enum: `misp`,`stix`,`html`,`pdf` |  |
| --- | --- | --- | --- |
| export_id | string | ID of export record |  |

GET /api/reports/{report_id}/downloadcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

202

Accepted

204

No content

400

Bad request

404

Item not found

408

Request timeout

422

Validation Error

500

Internal server error

 Response
### Get Downloads List

Get list of all reports downloads by current user

Auth apiKeyQuery String

| page | integer | Default: 1 |  |
| --- | --- | --- | --- |
| page_size | integer | Default: 10 |  |

GET /api/users/me/downloadscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportFormatResponse | object |  |  |
| --- | --- | --- | --- |
| items12 fields | array[object] |  |  |
| id | string |  |  |
| flow_id | string |  |  |
| file_name | string |  |  |
| file_sha256 | string |  |  |
| verdict | string |  |  |
| report_id | string |  |  |
| format | string | Formats that can take a lot of time to be generated  Enum: `html`,`pdf` |  |
| state | string | State of report generation  Enum: `created`,`queued`,`in_progress`,`failed`,`success` |  |
| created_date | date-time |  |  |
| started_date | date-time |  |  |
| finished_date | date-time |  |  |
| settings | object | Settings used for exporting report |  |
| strings_limit | integer |  |  |
| strings_mode | string | An enumeration.  Enum: `all`,`interesting`,`prefer_interesting` |  |
| count | integer |  |  |

422

Validation Error

500

Internal server error

 Response
### Get Specific Report

Obtain a report for given report_id.

Auth apiKeyPath Params

| report_id | string | Report Id |  |
| --- | --- | --- | --- |
| file_hash | string | File hash |  |

Query String

| filter | array | Report fields that should be fetched |  |
| --- | --- | --- | --- |
| sorting | array | Sort parameters to be applied to fetched report data |  |
| other | array | Extra options to get special data |  |

GET /api/reports/{report_id}/{file_hash}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AllUploadRelatedReportsResponse | object | Model for get_all_upload_related_reports() endpoint |  |
| --- | --- | --- | --- |
| flowId | string |  |  |
| allFinished | boolean |  |  |
| allFilesDownloadFinished | boolean |  |  |
| allAdditionalStepsDone | boolean |  |  |
| reportsAmount | integer |  |  |
| priority | string |  |  |
| pollPause | integer |  |  |
| state | string | Scan state of ScanInit instance  Enum: `created`,`queued`,`scanning`,`finished` |  |
| scanStartedDate | string |  |  |
| positionInQueue | integer |  |  |
| queueSize | integer |  |  |
| fileSize | integer |  |  |
| job | object | Model for job field in AllUploadRelatedReportsResponse |  |
| error | boolean |  |  |
| reason | string |  |  |
| fileReadProgressBytes | integer |  |  |
| rejected_files | array[object] |  |  |
| name | string |  |  |
| rejected_reason | string |  |  |
| sourceArchive11 fields | object | Model for sourceArchive field in AllUploadRelatedReportsResponse |  |
| scan_task_id | string |  |  |
| name | string |  |  |
| mimeType | string |  |  |
| sha256 | string |  |  |
| private | boolean |  |  |
| is_link_upload | boolean |  |  |
| sha1 | string |  |  |
| sha512 | string |  |  |
| md5 | string |  |  |
| tags2 fields | object | Model for tags field in AllUploadRelatedReportsResponse |  |
| source | string |  |  |
| tag | object | Model for tag field in TagsResponse |  |
| name | string |  |  |
| verdict | string |  |  |
| reports | object |  |  |
| * | object |  |  |

400

Bad request

404

Item not found

422

Validation Error

 Response
### Get Pe Emulation File

Get PE emulation files

Auth apiKeyPath Params

| report_id | string | Report Id |  |
| --- | --- | --- | --- |
| file_name |  | PE emulation file name |  |

GET /api/files/pe-emulation/{report_id}/{file_name}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Successful Response

| No response body |
| --- |

404

Item not found

422

Validation Error

 Response
### Advanced Search

Search for reports and uploaded files by various tokens, like hash, filename, verdict, IOCs etc.

Auth apiKeyQuery String

| age | integer | Search reports with age of "age" days  Default: -1 |  |
| --- | --- | --- | --- |
| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| page_size |  | Page size  Default: 10 |  |
| unique_files | boolean | Default: false |  |
| method |  | Default: and |  |
| derived_files | boolean | Default: true |  |
| no_date_limit | boolean | Default: false |  |
| query | string |  |  |
| verdict | string |  |  |
| source_type | string | Enum: `url`,`url-to-file`,`file` |  |
| filetype | string | Enum: `ace`,`apk`,`bat`,`64bits`,`bmp`,`csv`,`doc`,`docm`,`docx`,`dot`,`dotm`,`dotx`,`elf`,`eml`,`gif`,`hta`,`htm`,`html`,`iso`,`java`,`java-bytecode`,`javascript`,`jpg`,`lnk`,`mbox`,`mhtml`,`msg`,`msi`,`mso`,`odp`,`ods`,`odt`,`odg`,`odf`,`odc`,`odb`,`odi`,`ole`,`one`,`pdf`,`pedll`,`peexe`,`png`,`pot`,`potm`,`potx`,`powershell`,`ppt`,`pptm`,`pptx`,`ps`,`pub`,`rar`,`rfc822`,`rtf`,`svg`,`txt`,`vbs`,`wmv`,`wsf`,`xlm`,`xls`,`xlsb`,`xlsm`,`xlsx`,`xlt`,`xltm`,`xltx`,`xml`,`xsl`,`zip`,`7zip`,`exe`,`mail`,`ms-office`,`script` |  |
| tag | string |  |  |
| tags | string |  |  |
| date_from | string |  |  |
| date_to | string |  |  |
| rate_from | integer |  |  |
| rate_to | integer |  |  |
| uuid | string |  |  |
| email | string |  |  |
| registry_path | string |  |  |
| revision_save_id | string |  |  |
| yara_rule | string |  |  |
| retry_count | integer |  |  |
| scan_init_id | string |  |  |
| report_id | string |  |  |
| country | string |  |  |
| filename | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| sha512 | string |  |  |
| md5 | string |  |  |
| domain | string |  |  |
| ip | string |  |  |
| url | string |  |  |
| media_type | string |  |  |
| imphash | string |  |  |
| ssdeep | string |  |  |
| authentihash | string |  |  |
| fuzzyfsiohash | string |  |  |
| signal_groups | string |  |  |
| mitre_techniques | string |  |  |
| verdict_groups | string |  |  |
| main_task_state |  | Default: success |  |
| exclude | string |  |  |

Expand GET /api/reports/advanced-searchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportSearchResponse | object | Search response returned to user |  |
| --- | --- | --- | --- |
| items | array |  |  |
| count | integer |  |  |
| count_search_params | integer |  |  |
| method | string |  |  |
| dbs_sync | boolean |  |  |

400

Bad request

422

Validation Error

 Response
### Simple Search

Search for reports and uploaded files by various tokens, like hash, filename, verdict, IOCs etc. Simple search only uses the `query` param (and some other defaults), other params are ignored.

Auth apiKeyQuery String

| age | integer | Search reports with age of "age" days  Default: -1 |  |
| --- | --- | --- | --- |
| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| page_size |  | Page size  Default: 10 |  |
| method |  | Default: and |  |
| derived_files | boolean | Default: true |  |
| no_date_limit | boolean | Default: false |  |
| query | string |  |  |
| verdict | string |  |  |
| source_type | string | Enum: `url`,`url-to-file`,`file` |  |
| filetype | string | Enum: `ace`,`apk`,`bat`,`64bits`,`bmp`,`csv`,`doc`,`docm`,`docx`,`dot`,`dotm`,`dotx`,`elf`,`eml`,`gif`,`hta`,`htm`,`html`,`iso`,`java`,`java-bytecode`,`javascript`,`jpg`,`lnk`,`mbox`,`mhtml`,`msg`,`msi`,`mso`,`odp`,`ods`,`odt`,`odg`,`odf`,`odc`,`odb`,`odi`,`ole`,`one`,`pdf`,`pedll`,`peexe`,`png`,`pot`,`potm`,`potx`,`powershell`,`ppt`,`pptm`,`pptx`,`ps`,`pub`,`rar`,`rfc822`,`rtf`,`svg`,`txt`,`vbs`,`wmv`,`wsf`,`xlm`,`xls`,`xlsb`,`xlsm`,`xlsx`,`xlt`,`xltm`,`xltx`,`xml`,`xsl`,`zip`,`7zip`,`exe`,`mail`,`ms-office`,`script` |  |
| tag | string |  |  |
| tags | string |  |  |
| date_from | string |  |  |
| date_to | string |  |  |
| rate_from | integer |  |  |
| rate_to | integer |  |  |
| uuid | string |  |  |
| email | string |  |  |
| registry_path | string |  |  |
| revision_save_id | string |  |  |
| yara_rule | string |  |  |
| retry_count | integer |  |  |
| scan_init_id | string |  |  |
| report_id | string |  |  |
| country | string |  |  |
| filename | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| sha512 | string |  |  |
| md5 | string |  |  |
| domain | string |  |  |
| ip | string |  |  |
| url | string |  |  |
| media_type | string |  |  |
| imphash | string |  |  |
| ssdeep | string |  |  |
| authentihash | string |  |  |
| fuzzyfsiohash | string |  |  |
| signal_groups | string |  |  |
| mitre_techniques | string |  |  |
| verdict_groups | string |  |  |
| main_task_state |  | Default: success |  |
| exclude | string |  |  |

Expand GET /api/reports/searchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportSearchResponse | object | Search response returned to user |  |
| --- | --- | --- | --- |
| items | array |  |  |
| count | integer |  |  |
| count_search_params | integer |  |  |
| method | string |  |  |
| dbs_sync | boolean |  |  |

400

Bad request

422

Validation Error

 Response
### Get Public Reports

Get all public reports

Auth apiKeyQuery String

| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| page_size |  | Page size  Default: 10 |  |

GET /api/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportSearchResponse | object | Search response returned to user |  |
| --- | --- | --- | --- |
| items | array |  |  |
| count | integer |  |  |
| count_search_params | integer |  |  |
| method | string |  |  |
| dbs_sync | boolean |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get User Reports

Get reports of current user

Auth apiKeyQuery String

| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| page_size |  | Page size  Default: 10 |  |
| date_from | string | Results newer then this date (format YYYY-MM-DD) |  |
| verdict | string | Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

GET /api/me/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportSearchResponse | object | Search response returned to user |  |
| --- | --- | --- | --- |
| items | array |  |  |
| count | integer |  |  |
| count_search_params | integer |  |  |
| method | string |  |  |
| dbs_sync | boolean |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get User Reports Links

Get links of all user's reports as a .CSV file.

In case of no reports for selected time frame empty response is returned.

Auth apiKeyQuery String

| date_from | string | Results newer then this date (format YYYY-MM-DD) |  |
| --- | --- | --- | --- |
| date_to | string | Results older then this date (format YYYY-MM-DD) |  |

GET /api/me/reports/linkscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Frequent Tags

Get most frequently seen tags recently

Auth apiKeyGET /api/users/get-frequent-tagscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| FrequentTagsResponse | object |  |  |
| --- | --- | --- | --- |
| tags | array[object] |  |  |
| updated | date-time |  |  |

401

Not authorized

 Response
### Get Most Interesting

Get most interesting report recently

Auth apiKeyGET /api/users/most-interestingcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| MostInterestingResponse | object |  |  |
| --- | --- | --- | --- |
| report | object |  |  |
| updated | date-time |  |  |

401

Not authorized

 Response
## Files

Get a file by its hash or id in various format

Endpoints[GET/api/files/{hash}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-single-file-api-files--hash--get) [GET/api/archives/samples/{publicity}/{type}/{date}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#download-samples-archive-api-archives-samples--publicity---type-) [GET/api/feed/archives/{publicity}/{type}/{date}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#download-samples-archive-api-feed-archives--publicity---type---d)
### Get Single File

Obtain single file for given report by hash

Auth apiKeyPath Params

| hash | string | File hash |  |
| --- | --- | --- | --- |

Query String

| report_id | string | Report Id (only needed if `original_name` is true) |  |
| --- | --- | --- | --- |
| type |  | Default: base64 |  |
| original_name | boolean | (only used if `type` is raw)  Default: false |  |
| password | string | Password to be used on compression (only used if `type` is raw) |  |

GET /api/files/{hash}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

GetSingleFileResponse<unnamed>

| GetSingleFileResponse | object | Model for get_single_file() endpoint |  |
| --- | --- | --- | --- |
| type | string | An enumeration.  Enum: `base64`,`compressedBase64` |  |
| content | string |  |  |

404

Item not found

422

Validation Error

 Response
### Download Samples Archive

Download an archive file

Auth apiKeyPath Params

| publicity | string | Enum: `public`,`private` |  |
| --- | --- | --- | --- |
| type | string | Enum: `doc`,`exec` |  |
| date | string | pattern: `(\d{4})\-(0[1-9]|1[012])\-(0[1-9]|[12][0-9]|3[01])` |  |

GET /api/archives/samples/{publicity}/{type}/{date}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Successful Response

| No response body |
| --- |

401

Not authorized

403

Forbidden

404

Item not found

422

Validation Error

 Response
### Download Samples ArchiveDeprecated

Download an archive file

Auth apiKeyPath Params

| publicity | string | Enum: `public`,`private` |  |
| --- | --- | --- | --- |
| type | string | Enum: `doc`,`exec` |  |
| date | string | pattern: `(\d{4})\-(0[1-9]|1[012])\-(0[1-9]|[12][0-9]|3[01])` |  |

GET /api/feed/archives/{publicity}/{type}/{date}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Successful Response

| No response body |
| --- |

401

Not authorized

403

Forbidden

404

Item not found

422

Validation Error

 Response
## Feed

Atom feed

Endpoints[GET/api/feed/reports](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-feed-api-feed-reports-get) [GET/api/feed/atom](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-feed-api-feed-atom-get) [GET/api/feed/reports/info](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-feed-info-api-feed-reports-info-get) [GET/api/feed/info](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-feed-info-api-feed-info-get) [GET/api/archives/samples](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-daily-samples-archives-api-archives-samples-get) [GET/api/feed/archives](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-daily-samples-archives-api-feed-archives-get) [GET/api/feed/yara](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-yara-feed-api-feed-yara-get) [GET/api/feed/yara/info](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-yara-feed-info-api-feed-yara-info-get) [GET/api/archives/yara](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-daily-yara-archives-api-archives-yara-get) [GET/api/archives/yara/{date}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#download-yara-archive-api-archives-yara--date--get)
### Get Reports Feed

Get reports feed.

For API documentation page we show smaller amount of reports. To get full feed, query feed endpoint directly from browser address bar or from any suitable app.

Auth apiKeyGET /api/feed/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Reports FeedDeprecated

Get reports feed.

For API documentation page we show smaller amount of reports. To get full feed, query feed endpoint directly from browser address bar or from any suitable app.

Auth apiKeyGET /api/feed/atomcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Reports Feed Info

Get reports feed info

Auth apiKeyGET /api/feed/reports/infocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| FeedInfo | object | Response model for get_feed_info endpoint |  |
| --- | --- | --- | --- |
| count | integer |  |  |
| length | integer |  |  |
| updated | number |  |  |
| download_allowed | boolean |  |  |

401

Not authorized

 Response
### Get Reports Feed InfoDeprecated

Get reports feed info

Auth apiKeyGET /api/feed/infocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| FeedInfo | object | Response model for get_feed_info endpoint |  |
| --- | --- | --- | --- |
| count | integer |  |  |
| length | integer |  |  |
| updated | number |  |  |
| download_allowed | boolean |  |  |

401

Not authorized

 Response
### Get Daily Samples Archives

Get daily samples

Auth apiKeyGET /api/archives/samplescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DailySamplesArchiveResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string | Archive file name |  |
| link | string | Link to file download |  |
| reports_date | string | Date of reports creation |  |
| files_count | integer | Amount of files in archive |  |
| files_type | string | An enumeration.  Enum: `doc`,`exec` |  |
| size | integer | Archive size in bytes |  |
| is_public | boolean | If archive contains only public or only private files |  |

401

Not authorized

 Response
### Get Daily Samples ArchivesDeprecated

Get daily samples

Auth apiKeyGET /api/feed/archivescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DailySamplesArchiveResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string | Archive file name |  |
| link | string | Link to file download |  |
| reports_date | string | Date of reports creation |  |
| files_count | integer | Amount of files in archive |  |
| files_type | string | An enumeration.  Enum: `doc`,`exec` |  |
| size | integer | Archive size in bytes |  |
| is_public | boolean | If archive contains only public or only private files |  |

401

Not authorized

 Response
### Get Yara Feed

Get YARA rules feed

Auth apiKeyGET /api/feed/yaracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Yara Feed Info

Get YARA rules feed info

Auth apiKeyGET /api/feed/yara/infocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Daily Yara Archives

Get daily YARA rules, generated for malicious reports

Auth apiKeyGET /api/archives/yaracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DailyYaraArchiveResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string | Archive file name |  |
| link | string | Link to file download |  |
| reports_date | string | Date of reports creation |  |
| rules_count | integer | Amount of rules in archive |  |
| size | integer | Archive size in bytes |  |

401

Not authorized

 Response
### Download Yara Archive

Get daily YARA rules archive

Auth apiKeyPath Params

| date | string |  |  |
| --- | --- | --- | --- |

GET /api/archives/yara/{date}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

403

Forbidden

404

Item not found

422

Validation Error

 Response
## Users

Report-related and other functionality used by ordinary users.

Endpoints[GET/api/users/me](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-current-user-api-users-me-get) [GET/api/users/profile](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-profile-api-users-profile-get) [POST/api/users/profile](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#post-profile-api-users-profile-post) [DELETE/api/users/reset-timezone-locale](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#reset-timezone-locale-api-users-reset-timezone-locale-delete) [GET/api/users/{account_id}/avatar](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-avatar-image-api-users--account-id--avatar-get) [POST/api/users/api-key/create](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#create-api-key-api-users-api-key-create-post) [POST/api/users/api-key/set](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#set-api-key-api-users-api-key-set-post) [POST/api/users/api-key/remove](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-api-key-api-users-api-key-remove-post) [POST/api/users/notifications/{notification}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#mark-notification-viewed-api-users-notifications--notification--) [DELETE/api/users/reports/{report_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#delete-report-api-users-reports--report-id--delete) [GET/api/users/uploads](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-public-reports-api-users-uploads-get) [GET/api/users/me/uploads](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-reports-api-users-me-uploads-get) [GET/api/users/stat](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-stat-api-users-stat-get) [GET/api/users/stat/generic](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-generic-stat-api-users-stat-generic-get) [GET/api/users/stat/reports](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-stat-api-users-stat-reports-get) [POST/api/users/stat/reports/verdicts/amount](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-verdicts-amount-api-users-stat-reports-verdicts-amou) [POST/api/users/stat/reports/verdicts/dates](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reports-verdicts-dates-api-users-stat-reports-verdicts-dates) [GET/api/users/stat/malicious-ips](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-malicious-ips-stat-api-users-stat-malicious-ips-get) [GET/api/users/stat/iocs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-ioc-stat-api-users-stat-iocs-get) [GET/api/users/stat/yara](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-yara-stat-api-users-stat-yara-get) [GET/api/users/stat/mitre](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-mitre-stat-api-users-stat-mitre-get) [GET/api/users/info/yara](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-yara-info-api-users-info-yara-get)
### Get Current User

Get user model of currently authenticated user

Auth apiKeyGET /api/users/mecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| GetCurrentUserResponse | object |  |  |
| --- | --- | --- | --- |
| accountId | string |  |  |
| userId | string |  |  |
| username | string |  |  |
| email | string |  |  |
| avatarLastModified | date-time |  |  |
| allowedFeatures | array |  |  |
| scanProfiles | array |  |  |
| isAdmin | boolean |  |  |
| isAuditor | boolean |  |  |
| isPasswordEmpty | boolean |  |  |
| theme | string |  |  |
| timezone | string |  |  |
| locale | string |  |  |
| externalAuth | object |  |  |
| notifications | array |  |  |

 Response
### Get Profile

Get user profile data

Auth apiKeyGET /api/users/profilecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| UserResponse | object | System user for out |  |
| --- | --- | --- | --- |
| account_id | string |  |  |
| email | string |  |  |
| username | string |  |  |
| pseudoname | string |  |  |
| groups | array[object] |  |  |
| name | string |  |  |
| has_avatar | boolean |  |  |
| profile9 fields | object |  |  |
| first_name | string |  |  |
| last_name | string |  |  |
| phone | string |  |  |
| company | string |  |  |
| job | string |  |  |
| role | string |  |  |
| department | string |  |  |
| industry | string |  |  |
| subscribe | boolean |  |  |
| api_key | string |  |  |
| theme | string |  |  |
| timezone | string | An enumeration.  Enum: `Africa/Abidjan`,`Africa/Accra`,`Africa/Addis_Ababa`,`Africa/Algiers`,`Africa/Asmara`,`Africa/Asmera`,`Africa/Bamako`,`Africa/Bangui`,`Africa/Banjul`,`Africa/Bissau`,`Africa/Blantyre`,`Africa/Brazzaville`,`Africa/Bujumbura`,`Africa/Cairo`,`Africa/Casablanca`,`Africa/Ceuta`,`Africa/Conakry`,`Africa/Dakar`,`Africa/Dar_es_Salaam`,`Africa/Djibouti`,`Africa/Douala`,`Africa/El_Aaiun`,`Africa/Freetown`,`Africa/Gaborone`,`Africa/Harare`,`Africa/Johannesburg`,`Africa/Juba`,`Africa/Kampala`,`Africa/Khartoum`,`Africa/Kigali`,`Africa/Kinshasa`,`Africa/Lagos`,`Africa/Libreville`,`Africa/Lome`,`Africa/Luanda`,`Africa/Lubumbashi`,`Africa/Lusaka`,`Africa/Malabo`,`Africa/Maputo`,`Africa/Maseru`,`Africa/Mbabane`,`Africa/Mogadishu`,`Africa/Monrovia`,`Africa/Nairobi`,`Africa/Ndjamena`,`Africa/Niamey`,`Africa/Nouakchott`,`Africa/Ouagadougou`,`Africa/Porto-Novo`,`Africa/Sao_Tome`,`Africa/Timbuktu`,`Africa/Tripoli`,`Africa/Tunis`,`Africa/Windhoek`,`America/Adak`,`America/Anchorage`,`America/Anguilla`,`America/Antigua`,`America/Araguaina`,`America/Argentina/Buenos_Aires`,`America/Argentina/Catamarca`,`America/Argentina/ComodRivadavia`,`America/Argentina/Cordoba`,`America/Argentina/Jujuy`,`America/Argentina/La_Rioja`,`America/Argentina/Mendoza`,`America/Argentina/Rio_Gallegos`,`America/Argentina/Salta`,`America/Argentina/San_Juan`,`America/Argentina/San_Luis`,`America/Argentina/Tucuman`,`America/Argentina/Ushuaia`,`America/Aruba`,`America/Asuncion`,`America/Atikokan`,`America/Atka`,`America/Bahia`,`America/Bahia_Banderas`,`America/Barbados`,`America/Belem`,`America/Belize`,`America/Blanc-Sablon`,`America/Boa_Vista`,`America/Bogota`,`America/Boise`,`America/Buenos_Aires`,`America/Cambridge_Bay`,`America/Campo_Grande`,`America/Cancun`,`America/Caracas`,`America/Catamarca`,`America/Cayenne`,`America/Cayman`,`America/Chicago`,`America/Chihuahua`,`America/Coral_Harbour`,`America/Cordoba`,`America/Costa_Rica`,`America/Creston`,`America/Cuiaba`,`America/Curacao`,`America/Danmarkshavn`,`America/Dawson`,`America/Dawson_Creek`,`America/Denver`,`America/Detroit`,`America/Dominica`,`America/Edmonton`,`America/Eirunepe`,`America/El_Salvador`,`America/Ensenada`,`America/Fort_Nelson`,`America/Fort_Wayne`,`America/Fortaleza`,`America/Glace_Bay`,`America/Godthab`,`America/Goose_Bay`,`America/Grand_Turk`,`America/Grenada`,`America/Guadeloupe`,`America/Guatemala`,`America/Guayaquil`,`America/Guyana`,`America/Halifax`,`America/Havana`,`America/Hermosillo`,`America/Indiana/Indianapolis`,`America/Indiana/Knox`,`America/Indiana/Marengo`,`America/Indiana/Petersburg`,`America/Indiana/Tell_City`,`America/Indiana/Vevay`,`America/Indiana/Vincennes`,`America/Indiana/Winamac`,`America/Indianapolis`,`America/Inuvik`,`America/Iqaluit`,`America/Jamaica`,`America/Jujuy`,`America/Juneau`,`America/Kentucky/Louisville`,`America/Kentucky/Monticello`,`America/Knox_IN`,`America/Kralendijk`,`America/La_Paz`,`America/Lima`,`America/Los_Angeles`,`America/Louisville`,`America/Lower_Princes`,`America/Maceio`,`America/Managua`,`America/Manaus`,`America/Marigot`,`America/Martinique`,`America/Matamoros`,`America/Mazatlan`,`America/Mendoza`,`America/Menominee`,`America/Merida`,`America/Metlakatla`,`America/Mexico_City`,`America/Miquelon`,`America/Moncton`,`America/Monterrey`,`America/Montevideo`,`America/Montreal`,`America/Montserrat`,`America/Nassau`,`America/New_York`,`America/Nipigon`,`America/Nome`,`America/Noronha`,`America/North_Dakota/Beulah`,`America/North_Dakota/Center`,`America/North_Dakota/New_Salem`,`America/Ojinaga`,`America/Panama`,`America/Pangnirtung`,`America/Paramaribo`,`America/Phoenix`,`America/Port-au-Prince`,`America/Port_of_Spain`,`America/Porto_Acre`,`America/Porto_Velho`,`America/Puerto_Rico`,`America/Punta_Arenas`,`America/Rainy_River`,`America/Rankin_Inlet`,`America/Recife`,`America/Regina`,`America/Resolute`,`America/Rio_Branco`,`America/Rosario`,`America/Santa_Isabel`,`America/Santarem`,`America/Santiago`,`America/Santo_Domingo`,`America/Sao_Paulo`,`America/Scoresbysund`,`America/Shiprock`,`America/Sitka`,`America/St_Barthelemy`,`America/St_Johns`,`America/St_Kitts`,`America/St_Lucia`,`America/St_Thomas`,`America/St_Vincent`,`America/Swift_Current`,`America/Tegucigalpa`,`America/Thule`,`America/Thunder_Bay`,`America/Tijuana`,`America/Toronto`,`America/Tortola`,`America/Vancouver`,`America/Virgin`,`America/Whitehorse`,`America/Winnipeg`,`America/Yakutat`,`America/Yellowknife`,`Antarctica/Casey`,`Antarctica/Davis`,`Antarctica/DumontDUrville`,`Antarctica/Macquarie`,`Antarctica/Mawson`,`Antarctica/McMurdo`,`Antarctica/Palmer`,`Antarctica/Rothera`,`Antarctica/South_Pole`,`Antarctica/Syowa`,`Antarctica/Troll`,`Antarctica/Vostok`,`Arctic/Longyearbyen`,`Asia/Aden`,`Asia/Almaty`,`Asia/Amman`,`Asia/Anadyr`,`Asia/Aqtau`,`Asia/Aqtobe`,`Asia/Ashgabat`,`Asia/Ashkhabad`,`Asia/Atyrau`,`Asia/Baghdad`,`Asia/Bahrain`,`Asia/Baku`,`Asia/Bangkok`,`Asia/Barnaul`,`Asia/Beirut`,`Asia/Bishkek`,`Asia/Brunei`,`Asia/Calcutta`,`Asia/Chita`,`Asia/Choibalsan`,`Asia/Chongqing`,`Asia/Chungking`,`Asia/Colombo`,`Asia/Dacca`,`Asia/Damascus`,`Asia/Dhaka`,`Asia/Dili`,`Asia/Dubai`,`Asia/Dushanbe`,`Asia/Famagusta`,`Asia/Gaza`,`Asia/Harbin`,`Asia/Hebron`,`Asia/Ho_Chi_Minh`,`Asia/Hong_Kong`,`Asia/Hovd`,`Asia/Irkutsk`,`Asia/Istanbul`,`Asia/Jakarta`,`Asia/Jayapura`,`Asia/Jerusalem`,`Asia/Kabul`,`Asia/Kamchatka`,`Asia/Karachi`,`Asia/Kashgar`,`Asia/Kathmandu`,`Asia/Katmandu`,`Asia/Khandyga`,`Asia/Kolkata`,`Asia/Krasnoyarsk`,`Asia/Kuala_Lumpur`,`Asia/Kuching`,`Asia/Kuwait`,`Asia/Macao`,`Asia/Macau`,`Asia/Magadan`,`Asia/Makassar`,`Asia/Manila`,`Asia/Muscat`,`Asia/Nicosia`,`Asia/Novokuznetsk`,`Asia/Novosibirsk`,`Asia/Omsk`,`Asia/Oral`,`Asia/Phnom_Penh`,`Asia/Pontianak`,`Asia/Pyongyang`,`Asia/Qatar`,`Asia/Qostanay`,`Asia/Qyzylorda`,`Asia/Rangoon`,`Asia/Riyadh`,`Asia/Saigon`,`Asia/Sakhalin`,`Asia/Samarkand`,`Asia/Seoul`,`Asia/Shanghai`,`Asia/Singapore`,`Asia/Srednekolymsk`,`Asia/Taipei`,`Asia/Tashkent`,`Asia/Tbilisi`,`Asia/Tehran`,`Asia/Tel_Aviv`,`Asia/Thimbu`,`Asia/Thimphu`,`Asia/Tokyo`,`Asia/Tomsk`,`Asia/Ujung_Pandang`,`Asia/Ulaanbaatar`,`Asia/Ulan_Bator`,`Asia/Urumqi`,`Asia/Ust-Nera`,`Asia/Vientiane`,`Asia/Vladivostok`,`Asia/Yakutsk`,`Asia/Yangon`,`Asia/Yekaterinburg`,`Asia/Yerevan`,`Atlantic/Azores`,`Atlantic/Bermuda`,`Atlantic/Canary`,`Atlantic/Cape_Verde`,`Atlantic/Faeroe`,`Atlantic/Faroe`,`Atlantic/Jan_Mayen`,`Atlantic/Madeira`,`Atlantic/Reykjavik`,`Atlantic/South_Georgia`,`Atlantic/St_Helena`,`Atlantic/Stanley`,`Australia/ACT`,`Australia/Adelaide`,`Australia/Brisbane`,`Australia/Broken_Hill`,`Australia/Canberra`,`Australia/Currie`,`Australia/Darwin`,`Australia/Eucla`,`Australia/Hobart`,`Australia/LHI`,`Australia/Lindeman`,`Australia/Lord_Howe`,`Australia/Melbourne`,`Australia/NSW`,`Australia/North`,`Australia/Perth`,`Australia/Queensland`,`Australia/South`,`Australia/Sydney`,`Australia/Tasmania`,`Australia/Victoria`,`Australia/West`,`Australia/Yancowinna`,`Brazil/Acre`,`Brazil/DeNoronha`,`Brazil/East`,`Brazil/West`,`CET`,`CST6CDT`,`Canada/Atlantic`,`Canada/Central`,`Canada/Eastern`,`Canada/Mountain`,`Canada/Newfoundland`,`Canada/Pacific`,`Canada/Saskatchewan`,`Canada/Yukon`,`Chile/Continental`,`Chile/EasterIsland`,`Cuba`,`EET`,`EST5EDT`,`Egypt`,`Eire`,`Etc/GMT`,`Etc/GMT+0`,`Etc/GMT+1`,`Etc/GMT+10`,`Etc/GMT+11`,`Etc/GMT+12`,`Etc/GMT+2`,`Etc/GMT+3`,`Etc/GMT+4`,`Etc/GMT+5`,`Etc/GMT+6`,`Etc/GMT+7`,`Etc/GMT+8`,`Etc/GMT+9`,`Etc/GMT-0`,`Etc/GMT-1`,`Etc/GMT-10`,`Etc/GMT-11`,`Etc/GMT-12`,`Etc/GMT-13`,`Etc/GMT-14`,`Etc/GMT-2`,`Etc/GMT-3`,`Etc/GMT-4`,`Etc/GMT-5`,`Etc/GMT-6`,`Etc/GMT-7`,`Etc/GMT-8`,`Etc/GMT-9`,`Etc/GMT0`,`Etc/Greenwich`,`Etc/UCT`,`Etc/UTC`,`Etc/Universal`,`Etc/Zulu`,`Europe/Amsterdam`,`Europe/Andorra`,`Europe/Astrakhan`,`Europe/Athens`,`Europe/Belfast`,`Europe/Belgrade`,`Europe/Berlin`,`Europe/Bratislava`,`Europe/Brussels`,`Europe/Bucharest`,`Europe/Budapest`,`Europe/Busingen`,`Europe/Chisinau`,`Europe/Copenhagen`,`Europe/Dublin`,`Europe/Gibraltar`,`Europe/Guernsey`,`Europe/Helsinki`,`Europe/Isle_of_Man`,`Europe/Istanbul`,`Europe/Jersey`,`Europe/Kaliningrad`,`Europe/Kiev`,`Europe/Kirov`,`Europe/Lisbon`,`Europe/Ljubljana`,`Europe/London`,`Europe/Luxembourg`,`Europe/Madrid`,`Europe/Malta`,`Europe/Mariehamn`,`Europe/Minsk`,`Europe/Monaco`,`Europe/Moscow`,`Europe/Nicosia`,`Europe/Oslo`,`Europe/Paris`,`Europe/Podgorica`,`Europe/Prague`,`Europe/Riga`,`Europe/Rome`,`Europe/Samara`,`Europe/San_Marino`,`Europe/Sarajevo`,`Europe/Saratov`,`Europe/Simferopol`,`Europe/Skopje`,`Europe/Sofia`,`Europe/Stockholm`,`Europe/Tallinn`,`Europe/Tirane`,`Europe/Tiraspol`,`Europe/Ulyanovsk`,`Europe/Uzhgorod`,`Europe/Vaduz`,`Europe/Vatican`,`Europe/Vienna`,`Europe/Vilnius`,`Europe/Volgograd`,`Europe/Warsaw`,`Europe/Zagreb`,`Europe/Zaporozhye`,`Europe/Zurich`,`GB`,`GB-Eire`,`GMT`,`GMT0`,`Greenwich`,`Hongkong`,`Iceland`,`Indian/Antananarivo`,`Indian/Chagos`,`Indian/Christmas`,`Indian/Cocos`,`Indian/Comoro`,`Indian/Kerguelen`,`Indian/Mahe`,`Indian/Maldives`,`Indian/Mauritius`,`Indian/Mayotte`,`Indian/Reunion`,`Iran`,`Israel`,`Jamaica`,`Japan`,`Kwajalein`,`Libya`,`MET`,`MST7MDT`,`Mexico/BajaNorte`,`Mexico/BajaSur`,`Mexico/General`,`NZ`,`NZ-CHAT`,`Navajo`,`PRC`,`PST8PDT`,`Pacific/Apia`,`Pacific/Auckland`,`Pacific/Bougainville`,`Pacific/Chatham`,`Pacific/Chuuk`,`Pacific/Easter`,`Pacific/Efate`,`Pacific/Enderbury`,`Pacific/Fakaofo`,`Pacific/Fiji`,`Pacific/Funafuti`,`Pacific/Galapagos`,`Pacific/Gambier`,`Pacific/Guadalcanal`,`Pacific/Guam`,`Pacific/Honolulu`,`Pacific/Johnston`,`Pacific/Kiritimati`,`Pacific/Kosrae`,`Pacific/Kwajalein`,`Pacific/Majuro`,`Pacific/Marquesas`,`Pacific/Midway`,`Pacific/Nauru`,`Pacific/Niue`,`Pacific/Norfolk`,`Pacific/Noumea`,`Pacific/Pago_Pago`,`Pacific/Palau`,`Pacific/Pitcairn`,`Pacific/Pohnpei`,`Pacific/Ponape`,`Pacific/Port_Moresby`,`Pacific/Rarotonga`,`Pacific/Saipan`,`Pacific/Samoa`,`Pacific/Tahiti`,`Pacific/Tarawa`,`Pacific/Tongatapu`,`Pacific/Truk`,`Pacific/Wake`,`Pacific/Wallis`,`Pacific/Yap`,`Poland`,`Portugal`,`ROK`,`Singapore`,`Turkey`,`UCT`,`US/Alaska`,`US/Aleutian`,`US/Arizona`,`US/Central`,`US/East-Indiana`,`US/Eastern`,`US/Hawaii`,`US/Indiana-Starke`,`US/Michigan`,`US/Mountain`,`US/Pacific`,`US/Pacific-New`,`US/Samoa`,`UTC`,`Universal`,`W-SU`,`WET`,`Zulu` |  |
| locale | string | An enumeration.  Enum: `de`,`en`,`hu`,`it`,`nl`,`sv` |  |

Expand 401

Not authorized

 Response
### Post Profile

Update user profile data

Auth apiKeyRequest Body multipart/form-data

| Body_post_profile_api_users_profile_post | object |  |  |
| --- | --- | --- | --- |
| email | string |  |  |
| username | string |  |  |
| old_password | string |  |  |
| new_password | string |  |  |
| password_confirm | string |  |  |
| file | file |  |  |
| first_name | string |  |  |
| last_name | string |  |  |
| phone | string |  |  |
| company | string |  |  |
| job | string |  |  |
| role | string |  |  |
| department | string |  |  |
| industry | string |  |  |
| subscribe | boolean | Default: true |  |
| theme | string |  |  |
| timezone | string | An enumeration.  Enum: `Africa/Abidjan`,`Africa/Accra`,`Africa/Addis_Ababa`,`Africa/Algiers`,`Africa/Asmara`,`Africa/Asmera`,`Africa/Bamako`,`Africa/Bangui`,`Africa/Banjul`,`Africa/Bissau`,`Africa/Blantyre`,`Africa/Brazzaville`,`Africa/Bujumbura`,`Africa/Cairo`,`Africa/Casablanca`,`Africa/Ceuta`,`Africa/Conakry`,`Africa/Dakar`,`Africa/Dar_es_Salaam`,`Africa/Djibouti`,`Africa/Douala`,`Africa/El_Aaiun`,`Africa/Freetown`,`Africa/Gaborone`,`Africa/Harare`,`Africa/Johannesburg`,`Africa/Juba`,`Africa/Kampala`,`Africa/Khartoum`,`Africa/Kigali`,`Africa/Kinshasa`,`Africa/Lagos`,`Africa/Libreville`,`Africa/Lome`,`Africa/Luanda`,`Africa/Lubumbashi`,`Africa/Lusaka`,`Africa/Malabo`,`Africa/Maputo`,`Africa/Maseru`,`Africa/Mbabane`,`Africa/Mogadishu`,`Africa/Monrovia`,`Africa/Nairobi`,`Africa/Ndjamena`,`Africa/Niamey`,`Africa/Nouakchott`,`Africa/Ouagadougou`,`Africa/Porto-Novo`,`Africa/Sao_Tome`,`Africa/Timbuktu`,`Africa/Tripoli`,`Africa/Tunis`,`Africa/Windhoek`,`America/Adak`,`America/Anchorage`,`America/Anguilla`,`America/Antigua`,`America/Araguaina`,`America/Argentina/Buenos_Aires`,`America/Argentina/Catamarca`,`America/Argentina/ComodRivadavia`,`America/Argentina/Cordoba`,`America/Argentina/Jujuy`,`America/Argentina/La_Rioja`,`America/Argentina/Mendoza`,`America/Argentina/Rio_Gallegos`,`America/Argentina/Salta`,`America/Argentina/San_Juan`,`America/Argentina/San_Luis`,`America/Argentina/Tucuman`,`America/Argentina/Ushuaia`,`America/Aruba`,`America/Asuncion`,`America/Atikokan`,`America/Atka`,`America/Bahia`,`America/Bahia_Banderas`,`America/Barbados`,`America/Belem`,`America/Belize`,`America/Blanc-Sablon`,`America/Boa_Vista`,`America/Bogota`,`America/Boise`,`America/Buenos_Aires`,`America/Cambridge_Bay`,`America/Campo_Grande`,`America/Cancun`,`America/Caracas`,`America/Catamarca`,`America/Cayenne`,`America/Cayman`,`America/Chicago`,`America/Chihuahua`,`America/Coral_Harbour`,`America/Cordoba`,`America/Costa_Rica`,`America/Creston`,`America/Cuiaba`,`America/Curacao`,`America/Danmarkshavn`,`America/Dawson`,`America/Dawson_Creek`,`America/Denver`,`America/Detroit`,`America/Dominica`,`America/Edmonton`,`America/Eirunepe`,`America/El_Salvador`,`America/Ensenada`,`America/Fort_Nelson`,`America/Fort_Wayne`,`America/Fortaleza`,`America/Glace_Bay`,`America/Godthab`,`America/Goose_Bay`,`America/Grand_Turk`,`America/Grenada`,`America/Guadeloupe`,`America/Guatemala`,`America/Guayaquil`,`America/Guyana`,`America/Halifax`,`America/Havana`,`America/Hermosillo`,`America/Indiana/Indianapolis`,`America/Indiana/Knox`,`America/Indiana/Marengo`,`America/Indiana/Petersburg`,`America/Indiana/Tell_City`,`America/Indiana/Vevay`,`America/Indiana/Vincennes`,`America/Indiana/Winamac`,`America/Indianapolis`,`America/Inuvik`,`America/Iqaluit`,`America/Jamaica`,`America/Jujuy`,`America/Juneau`,`America/Kentucky/Louisville`,`America/Kentucky/Monticello`,`America/Knox_IN`,`America/Kralendijk`,`America/La_Paz`,`America/Lima`,`America/Los_Angeles`,`America/Louisville`,`America/Lower_Princes`,`America/Maceio`,`America/Managua`,`America/Manaus`,`America/Marigot`,`America/Martinique`,`America/Matamoros`,`America/Mazatlan`,`America/Mendoza`,`America/Menominee`,`America/Merida`,`America/Metlakatla`,`America/Mexico_City`,`America/Miquelon`,`America/Moncton`,`America/Monterrey`,`America/Montevideo`,`America/Montreal`,`America/Montserrat`,`America/Nassau`,`America/New_York`,`America/Nipigon`,`America/Nome`,`America/Noronha`,`America/North_Dakota/Beulah`,`America/North_Dakota/Center`,`America/North_Dakota/New_Salem`,`America/Ojinaga`,`America/Panama`,`America/Pangnirtung`,`America/Paramaribo`,`America/Phoenix`,`America/Port-au-Prince`,`America/Port_of_Spain`,`America/Porto_Acre`,`America/Porto_Velho`,`America/Puerto_Rico`,`America/Punta_Arenas`,`America/Rainy_River`,`America/Rankin_Inlet`,`America/Recife`,`America/Regina`,`America/Resolute`,`America/Rio_Branco`,`America/Rosario`,`America/Santa_Isabel`,`America/Santarem`,`America/Santiago`,`America/Santo_Domingo`,`America/Sao_Paulo`,`America/Scoresbysund`,`America/Shiprock`,`America/Sitka`,`America/St_Barthelemy`,`America/St_Johns`,`America/St_Kitts`,`America/St_Lucia`,`America/St_Thomas`,`America/St_Vincent`,`America/Swift_Current`,`America/Tegucigalpa`,`America/Thule`,`America/Thunder_Bay`,`America/Tijuana`,`America/Toronto`,`America/Tortola`,`America/Vancouver`,`America/Virgin`,`America/Whitehorse`,`America/Winnipeg`,`America/Yakutat`,`America/Yellowknife`,`Antarctica/Casey`,`Antarctica/Davis`,`Antarctica/DumontDUrville`,`Antarctica/Macquarie`,`Antarctica/Mawson`,`Antarctica/McMurdo`,`Antarctica/Palmer`,`Antarctica/Rothera`,`Antarctica/South_Pole`,`Antarctica/Syowa`,`Antarctica/Troll`,`Antarctica/Vostok`,`Arctic/Longyearbyen`,`Asia/Aden`,`Asia/Almaty`,`Asia/Amman`,`Asia/Anadyr`,`Asia/Aqtau`,`Asia/Aqtobe`,`Asia/Ashgabat`,`Asia/Ashkhabad`,`Asia/Atyrau`,`Asia/Baghdad`,`Asia/Bahrain`,`Asia/Baku`,`Asia/Bangkok`,`Asia/Barnaul`,`Asia/Beirut`,`Asia/Bishkek`,`Asia/Brunei`,`Asia/Calcutta`,`Asia/Chita`,`Asia/Choibalsan`,`Asia/Chongqing`,`Asia/Chungking`,`Asia/Colombo`,`Asia/Dacca`,`Asia/Damascus`,`Asia/Dhaka`,`Asia/Dili`,`Asia/Dubai`,`Asia/Dushanbe`,`Asia/Famagusta`,`Asia/Gaza`,`Asia/Harbin`,`Asia/Hebron`,`Asia/Ho_Chi_Minh`,`Asia/Hong_Kong`,`Asia/Hovd`,`Asia/Irkutsk`,`Asia/Istanbul`,`Asia/Jakarta`,`Asia/Jayapura`,`Asia/Jerusalem`,`Asia/Kabul`,`Asia/Kamchatka`,`Asia/Karachi`,`Asia/Kashgar`,`Asia/Kathmandu`,`Asia/Katmandu`,`Asia/Khandyga`,`Asia/Kolkata`,`Asia/Krasnoyarsk`,`Asia/Kuala_Lumpur`,`Asia/Kuching`,`Asia/Kuwait`,`Asia/Macao`,`Asia/Macau`,`Asia/Magadan`,`Asia/Makassar`,`Asia/Manila`,`Asia/Muscat`,`Asia/Nicosia`,`Asia/Novokuznetsk`,`Asia/Novosibirsk`,`Asia/Omsk`,`Asia/Oral`,`Asia/Phnom_Penh`,`Asia/Pontianak`,`Asia/Pyongyang`,`Asia/Qatar`,`Asia/Qostanay`,`Asia/Qyzylorda`,`Asia/Rangoon`,`Asia/Riyadh`,`Asia/Saigon`,`Asia/Sakhalin`,`Asia/Samarkand`,`Asia/Seoul`,`Asia/Shanghai`,`Asia/Singapore`,`Asia/Srednekolymsk`,`Asia/Taipei`,`Asia/Tashkent`,`Asia/Tbilisi`,`Asia/Tehran`,`Asia/Tel_Aviv`,`Asia/Thimbu`,`Asia/Thimphu`,`Asia/Tokyo`,`Asia/Tomsk`,`Asia/Ujung_Pandang`,`Asia/Ulaanbaatar`,`Asia/Ulan_Bator`,`Asia/Urumqi`,`Asia/Ust-Nera`,`Asia/Vientiane`,`Asia/Vladivostok`,`Asia/Yakutsk`,`Asia/Yangon`,`Asia/Yekaterinburg`,`Asia/Yerevan`,`Atlantic/Azores`,`Atlantic/Bermuda`,`Atlantic/Canary`,`Atlantic/Cape_Verde`,`Atlantic/Faeroe`,`Atlantic/Faroe`,`Atlantic/Jan_Mayen`,`Atlantic/Madeira`,`Atlantic/Reykjavik`,`Atlantic/South_Georgia`,`Atlantic/St_Helena`,`Atlantic/Stanley`,`Australia/ACT`,`Australia/Adelaide`,`Australia/Brisbane`,`Australia/Broken_Hill`,`Australia/Canberra`,`Australia/Currie`,`Australia/Darwin`,`Australia/Eucla`,`Australia/Hobart`,`Australia/LHI`,`Australia/Lindeman`,`Australia/Lord_Howe`,`Australia/Melbourne`,`Australia/NSW`,`Australia/North`,`Australia/Perth`,`Australia/Queensland`,`Australia/South`,`Australia/Sydney`,`Australia/Tasmania`,`Australia/Victoria`,`Australia/West`,`Australia/Yancowinna`,`Brazil/Acre`,`Brazil/DeNoronha`,`Brazil/East`,`Brazil/West`,`CET`,`CST6CDT`,`Canada/Atlantic`,`Canada/Central`,`Canada/Eastern`,`Canada/Mountain`,`Canada/Newfoundland`,`Canada/Pacific`,`Canada/Saskatchewan`,`Canada/Yukon`,`Chile/Continental`,`Chile/EasterIsland`,`Cuba`,`EET`,`EST5EDT`,`Egypt`,`Eire`,`Etc/GMT`,`Etc/GMT+0`,`Etc/GMT+1`,`Etc/GMT+10`,`Etc/GMT+11`,`Etc/GMT+12`,`Etc/GMT+2`,`Etc/GMT+3`,`Etc/GMT+4`,`Etc/GMT+5`,`Etc/GMT+6`,`Etc/GMT+7`,`Etc/GMT+8`,`Etc/GMT+9`,`Etc/GMT-0`,`Etc/GMT-1`,`Etc/GMT-10`,`Etc/GMT-11`,`Etc/GMT-12`,`Etc/GMT-13`,`Etc/GMT-14`,`Etc/GMT-2`,`Etc/GMT-3`,`Etc/GMT-4`,`Etc/GMT-5`,`Etc/GMT-6`,`Etc/GMT-7`,`Etc/GMT-8`,`Etc/GMT-9`,`Etc/GMT0`,`Etc/Greenwich`,`Etc/UCT`,`Etc/UTC`,`Etc/Universal`,`Etc/Zulu`,`Europe/Amsterdam`,`Europe/Andorra`,`Europe/Astrakhan`,`Europe/Athens`,`Europe/Belfast`,`Europe/Belgrade`,`Europe/Berlin`,`Europe/Bratislava`,`Europe/Brussels`,`Europe/Bucharest`,`Europe/Budapest`,`Europe/Busingen`,`Europe/Chisinau`,`Europe/Copenhagen`,`Europe/Dublin`,`Europe/Gibraltar`,`Europe/Guernsey`,`Europe/Helsinki`,`Europe/Isle_of_Man`,`Europe/Istanbul`,`Europe/Jersey`,`Europe/Kaliningrad`,`Europe/Kiev`,`Europe/Kirov`,`Europe/Lisbon`,`Europe/Ljubljana`,`Europe/London`,`Europe/Luxembourg`,`Europe/Madrid`,`Europe/Malta`,`Europe/Mariehamn`,`Europe/Minsk`,`Europe/Monaco`,`Europe/Moscow`,`Europe/Nicosia`,`Europe/Oslo`,`Europe/Paris`,`Europe/Podgorica`,`Europe/Prague`,`Europe/Riga`,`Europe/Rome`,`Europe/Samara`,`Europe/San_Marino`,`Europe/Sarajevo`,`Europe/Saratov`,`Europe/Simferopol`,`Europe/Skopje`,`Europe/Sofia`,`Europe/Stockholm`,`Europe/Tallinn`,`Europe/Tirane`,`Europe/Tiraspol`,`Europe/Ulyanovsk`,`Europe/Uzhgorod`,`Europe/Vaduz`,`Europe/Vatican`,`Europe/Vienna`,`Europe/Vilnius`,`Europe/Volgograd`,`Europe/Warsaw`,`Europe/Zagreb`,`Europe/Zaporozhye`,`Europe/Zurich`,`GB`,`GB-Eire`,`GMT`,`GMT0`,`Greenwich`,`Hongkong`,`Iceland`,`Indian/Antananarivo`,`Indian/Chagos`,`Indian/Christmas`,`Indian/Cocos`,`Indian/Comoro`,`Indian/Kerguelen`,`Indian/Mahe`,`Indian/Maldives`,`Indian/Mauritius`,`Indian/Mayotte`,`Indian/Reunion`,`Iran`,`Israel`,`Jamaica`,`Japan`,`Kwajalein`,`Libya`,`MET`,`MST7MDT`,`Mexico/BajaNorte`,`Mexico/BajaSur`,`Mexico/General`,`NZ`,`NZ-CHAT`,`Navajo`,`PRC`,`PST8PDT`,`Pacific/Apia`,`Pacific/Auckland`,`Pacific/Bougainville`,`Pacific/Chatham`,`Pacific/Chuuk`,`Pacific/Easter`,`Pacific/Efate`,`Pacific/Enderbury`,`Pacific/Fakaofo`,`Pacific/Fiji`,`Pacific/Funafuti`,`Pacific/Galapagos`,`Pacific/Gambier`,`Pacific/Guadalcanal`,`Pacific/Guam`,`Pacific/Honolulu`,`Pacific/Johnston`,`Pacific/Kiritimati`,`Pacific/Kosrae`,`Pacific/Kwajalein`,`Pacific/Majuro`,`Pacific/Marquesas`,`Pacific/Midway`,`Pacific/Nauru`,`Pacific/Niue`,`Pacific/Norfolk`,`Pacific/Noumea`,`Pacific/Pago_Pago`,`Pacific/Palau`,`Pacific/Pitcairn`,`Pacific/Pohnpei`,`Pacific/Ponape`,`Pacific/Port_Moresby`,`Pacific/Rarotonga`,`Pacific/Saipan`,`Pacific/Samoa`,`Pacific/Tahiti`,`Pacific/Tarawa`,`Pacific/Tongatapu`,`Pacific/Truk`,`Pacific/Wake`,`Pacific/Wallis`,`Pacific/Yap`,`Poland`,`Portugal`,`ROK`,`Singapore`,`Turkey`,`UCT`,`US/Alaska`,`US/Aleutian`,`US/Arizona`,`US/Central`,`US/East-Indiana`,`US/Eastern`,`US/Hawaii`,`US/Indiana-Starke`,`US/Michigan`,`US/Mountain`,`US/Pacific`,`US/Pacific-New`,`US/Samoa`,`UTC`,`Universal`,`W-SU`,`WET`,`Zulu` |  |
| locale | string | An enumeration.  Enum: `de`,`en`,`hu`,`it`,`nl`,`sv` |  |

Expand POST /api/users/profilecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| UserResponse | object | System user for out |  |
| --- | --- | --- | --- |
| account_id | string |  |  |
| email | string |  |  |
| username | string |  |  |
| pseudoname | string |  |  |
| groups | array[object] |  |  |
| name | string |  |  |
| has_avatar | boolean |  |  |
| profile9 fields | object |  |  |
| first_name | string |  |  |
| last_name | string |  |  |
| phone | string |  |  |
| company | string |  |  |
| job | string |  |  |
| role | string |  |  |
| department | string |  |  |
| industry | string |  |  |
| subscribe | boolean |  |  |
| api_key | string |  |  |
| theme | string |  |  |
| timezone | string | An enumeration.  Enum: `Africa/Abidjan`,`Africa/Accra`,`Africa/Addis_Ababa`,`Africa/Algiers`,`Africa/Asmara`,`Africa/Asmera`,`Africa/Bamako`,`Africa/Bangui`,`Africa/Banjul`,`Africa/Bissau`,`Africa/Blantyre`,`Africa/Brazzaville`,`Africa/Bujumbura`,`Africa/Cairo`,`Africa/Casablanca`,`Africa/Ceuta`,`Africa/Conakry`,`Africa/Dakar`,`Africa/Dar_es_Salaam`,`Africa/Djibouti`,`Africa/Douala`,`Africa/El_Aaiun`,`Africa/Freetown`,`Africa/Gaborone`,`Africa/Harare`,`Africa/Johannesburg`,`Africa/Juba`,`Africa/Kampala`,`Africa/Khartoum`,`Africa/Kigali`,`Africa/Kinshasa`,`Africa/Lagos`,`Africa/Libreville`,`Africa/Lome`,`Africa/Luanda`,`Africa/Lubumbashi`,`Africa/Lusaka`,`Africa/Malabo`,`Africa/Maputo`,`Africa/Maseru`,`Africa/Mbabane`,`Africa/Mogadishu`,`Africa/Monrovia`,`Africa/Nairobi`,`Africa/Ndjamena`,`Africa/Niamey`,`Africa/Nouakchott`,`Africa/Ouagadougou`,`Africa/Porto-Novo`,`Africa/Sao_Tome`,`Africa/Timbuktu`,`Africa/Tripoli`,`Africa/Tunis`,`Africa/Windhoek`,`America/Adak`,`America/Anchorage`,`America/Anguilla`,`America/Antigua`,`America/Araguaina`,`America/Argentina/Buenos_Aires`,`America/Argentina/Catamarca`,`America/Argentina/ComodRivadavia`,`America/Argentina/Cordoba`,`America/Argentina/Jujuy`,`America/Argentina/La_Rioja`,`America/Argentina/Mendoza`,`America/Argentina/Rio_Gallegos`,`America/Argentina/Salta`,`America/Argentina/San_Juan`,`America/Argentina/San_Luis`,`America/Argentina/Tucuman`,`America/Argentina/Ushuaia`,`America/Aruba`,`America/Asuncion`,`America/Atikokan`,`America/Atka`,`America/Bahia`,`America/Bahia_Banderas`,`America/Barbados`,`America/Belem`,`America/Belize`,`America/Blanc-Sablon`,`America/Boa_Vista`,`America/Bogota`,`America/Boise`,`America/Buenos_Aires`,`America/Cambridge_Bay`,`America/Campo_Grande`,`America/Cancun`,`America/Caracas`,`America/Catamarca`,`America/Cayenne`,`America/Cayman`,`America/Chicago`,`America/Chihuahua`,`America/Coral_Harbour`,`America/Cordoba`,`America/Costa_Rica`,`America/Creston`,`America/Cuiaba`,`America/Curacao`,`America/Danmarkshavn`,`America/Dawson`,`America/Dawson_Creek`,`America/Denver`,`America/Detroit`,`America/Dominica`,`America/Edmonton`,`America/Eirunepe`,`America/El_Salvador`,`America/Ensenada`,`America/Fort_Nelson`,`America/Fort_Wayne`,`America/Fortaleza`,`America/Glace_Bay`,`America/Godthab`,`America/Goose_Bay`,`America/Grand_Turk`,`America/Grenada`,`America/Guadeloupe`,`America/Guatemala`,`America/Guayaquil`,`America/Guyana`,`America/Halifax`,`America/Havana`,`America/Hermosillo`,`America/Indiana/Indianapolis`,`America/Indiana/Knox`,`America/Indiana/Marengo`,`America/Indiana/Petersburg`,`America/Indiana/Tell_City`,`America/Indiana/Vevay`,`America/Indiana/Vincennes`,`America/Indiana/Winamac`,`America/Indianapolis`,`America/Inuvik`,`America/Iqaluit`,`America/Jamaica`,`America/Jujuy`,`America/Juneau`,`America/Kentucky/Louisville`,`America/Kentucky/Monticello`,`America/Knox_IN`,`America/Kralendijk`,`America/La_Paz`,`America/Lima`,`America/Los_Angeles`,`America/Louisville`,`America/Lower_Princes`,`America/Maceio`,`America/Managua`,`America/Manaus`,`America/Marigot`,`America/Martinique`,`America/Matamoros`,`America/Mazatlan`,`America/Mendoza`,`America/Menominee`,`America/Merida`,`America/Metlakatla`,`America/Mexico_City`,`America/Miquelon`,`America/Moncton`,`America/Monterrey`,`America/Montevideo`,`America/Montreal`,`America/Montserrat`,`America/Nassau`,`America/New_York`,`America/Nipigon`,`America/Nome`,`America/Noronha`,`America/North_Dakota/Beulah`,`America/North_Dakota/Center`,`America/North_Dakota/New_Salem`,`America/Ojinaga`,`America/Panama`,`America/Pangnirtung`,`America/Paramaribo`,`America/Phoenix`,`America/Port-au-Prince`,`America/Port_of_Spain`,`America/Porto_Acre`,`America/Porto_Velho`,`America/Puerto_Rico`,`America/Punta_Arenas`,`America/Rainy_River`,`America/Rankin_Inlet`,`America/Recife`,`America/Regina`,`America/Resolute`,`America/Rio_Branco`,`America/Rosario`,`America/Santa_Isabel`,`America/Santarem`,`America/Santiago`,`America/Santo_Domingo`,`America/Sao_Paulo`,`America/Scoresbysund`,`America/Shiprock`,`America/Sitka`,`America/St_Barthelemy`,`America/St_Johns`,`America/St_Kitts`,`America/St_Lucia`,`America/St_Thomas`,`America/St_Vincent`,`America/Swift_Current`,`America/Tegucigalpa`,`America/Thule`,`America/Thunder_Bay`,`America/Tijuana`,`America/Toronto`,`America/Tortola`,`America/Vancouver`,`America/Virgin`,`America/Whitehorse`,`America/Winnipeg`,`America/Yakutat`,`America/Yellowknife`,`Antarctica/Casey`,`Antarctica/Davis`,`Antarctica/DumontDUrville`,`Antarctica/Macquarie`,`Antarctica/Mawson`,`Antarctica/McMurdo`,`Antarctica/Palmer`,`Antarctica/Rothera`,`Antarctica/South_Pole`,`Antarctica/Syowa`,`Antarctica/Troll`,`Antarctica/Vostok`,`Arctic/Longyearbyen`,`Asia/Aden`,`Asia/Almaty`,`Asia/Amman`,`Asia/Anadyr`,`Asia/Aqtau`,`Asia/Aqtobe`,`Asia/Ashgabat`,`Asia/Ashkhabad`,`Asia/Atyrau`,`Asia/Baghdad`,`Asia/Bahrain`,`Asia/Baku`,`Asia/Bangkok`,`Asia/Barnaul`,`Asia/Beirut`,`Asia/Bishkek`,`Asia/Brunei`,`Asia/Calcutta`,`Asia/Chita`,`Asia/Choibalsan`,`Asia/Chongqing`,`Asia/Chungking`,`Asia/Colombo`,`Asia/Dacca`,`Asia/Damascus`,`Asia/Dhaka`,`Asia/Dili`,`Asia/Dubai`,`Asia/Dushanbe`,`Asia/Famagusta`,`Asia/Gaza`,`Asia/Harbin`,`Asia/Hebron`,`Asia/Ho_Chi_Minh`,`Asia/Hong_Kong`,`Asia/Hovd`,`Asia/Irkutsk`,`Asia/Istanbul`,`Asia/Jakarta`,`Asia/Jayapura`,`Asia/Jerusalem`,`Asia/Kabul`,`Asia/Kamchatka`,`Asia/Karachi`,`Asia/Kashgar`,`Asia/Kathmandu`,`Asia/Katmandu`,`Asia/Khandyga`,`Asia/Kolkata`,`Asia/Krasnoyarsk`,`Asia/Kuala_Lumpur`,`Asia/Kuching`,`Asia/Kuwait`,`Asia/Macao`,`Asia/Macau`,`Asia/Magadan`,`Asia/Makassar`,`Asia/Manila`,`Asia/Muscat`,`Asia/Nicosia`,`Asia/Novokuznetsk`,`Asia/Novosibirsk`,`Asia/Omsk`,`Asia/Oral`,`Asia/Phnom_Penh`,`Asia/Pontianak`,`Asia/Pyongyang`,`Asia/Qatar`,`Asia/Qostanay`,`Asia/Qyzylorda`,`Asia/Rangoon`,`Asia/Riyadh`,`Asia/Saigon`,`Asia/Sakhalin`,`Asia/Samarkand`,`Asia/Seoul`,`Asia/Shanghai`,`Asia/Singapore`,`Asia/Srednekolymsk`,`Asia/Taipei`,`Asia/Tashkent`,`Asia/Tbilisi`,`Asia/Tehran`,`Asia/Tel_Aviv`,`Asia/Thimbu`,`Asia/Thimphu`,`Asia/Tokyo`,`Asia/Tomsk`,`Asia/Ujung_Pandang`,`Asia/Ulaanbaatar`,`Asia/Ulan_Bator`,`Asia/Urumqi`,`Asia/Ust-Nera`,`Asia/Vientiane`,`Asia/Vladivostok`,`Asia/Yakutsk`,`Asia/Yangon`,`Asia/Yekaterinburg`,`Asia/Yerevan`,`Atlantic/Azores`,`Atlantic/Bermuda`,`Atlantic/Canary`,`Atlantic/Cape_Verde`,`Atlantic/Faeroe`,`Atlantic/Faroe`,`Atlantic/Jan_Mayen`,`Atlantic/Madeira`,`Atlantic/Reykjavik`,`Atlantic/South_Georgia`,`Atlantic/St_Helena`,`Atlantic/Stanley`,`Australia/ACT`,`Australia/Adelaide`,`Australia/Brisbane`,`Australia/Broken_Hill`,`Australia/Canberra`,`Australia/Currie`,`Australia/Darwin`,`Australia/Eucla`,`Australia/Hobart`,`Australia/LHI`,`Australia/Lindeman`,`Australia/Lord_Howe`,`Australia/Melbourne`,`Australia/NSW`,`Australia/North`,`Australia/Perth`,`Australia/Queensland`,`Australia/South`,`Australia/Sydney`,`Australia/Tasmania`,`Australia/Victoria`,`Australia/West`,`Australia/Yancowinna`,`Brazil/Acre`,`Brazil/DeNoronha`,`Brazil/East`,`Brazil/West`,`CET`,`CST6CDT`,`Canada/Atlantic`,`Canada/Central`,`Canada/Eastern`,`Canada/Mountain`,`Canada/Newfoundland`,`Canada/Pacific`,`Canada/Saskatchewan`,`Canada/Yukon`,`Chile/Continental`,`Chile/EasterIsland`,`Cuba`,`EET`,`EST5EDT`,`Egypt`,`Eire`,`Etc/GMT`,`Etc/GMT+0`,`Etc/GMT+1`,`Etc/GMT+10`,`Etc/GMT+11`,`Etc/GMT+12`,`Etc/GMT+2`,`Etc/GMT+3`,`Etc/GMT+4`,`Etc/GMT+5`,`Etc/GMT+6`,`Etc/GMT+7`,`Etc/GMT+8`,`Etc/GMT+9`,`Etc/GMT-0`,`Etc/GMT-1`,`Etc/GMT-10`,`Etc/GMT-11`,`Etc/GMT-12`,`Etc/GMT-13`,`Etc/GMT-14`,`Etc/GMT-2`,`Etc/GMT-3`,`Etc/GMT-4`,`Etc/GMT-5`,`Etc/GMT-6`,`Etc/GMT-7`,`Etc/GMT-8`,`Etc/GMT-9`,`Etc/GMT0`,`Etc/Greenwich`,`Etc/UCT`,`Etc/UTC`,`Etc/Universal`,`Etc/Zulu`,`Europe/Amsterdam`,`Europe/Andorra`,`Europe/Astrakhan`,`Europe/Athens`,`Europe/Belfast`,`Europe/Belgrade`,`Europe/Berlin`,`Europe/Bratislava`,`Europe/Brussels`,`Europe/Bucharest`,`Europe/Budapest`,`Europe/Busingen`,`Europe/Chisinau`,`Europe/Copenhagen`,`Europe/Dublin`,`Europe/Gibraltar`,`Europe/Guernsey`,`Europe/Helsinki`,`Europe/Isle_of_Man`,`Europe/Istanbul`,`Europe/Jersey`,`Europe/Kaliningrad`,`Europe/Kiev`,`Europe/Kirov`,`Europe/Lisbon`,`Europe/Ljubljana`,`Europe/London`,`Europe/Luxembourg`,`Europe/Madrid`,`Europe/Malta`,`Europe/Mariehamn`,`Europe/Minsk`,`Europe/Monaco`,`Europe/Moscow`,`Europe/Nicosia`,`Europe/Oslo`,`Europe/Paris`,`Europe/Podgorica`,`Europe/Prague`,`Europe/Riga`,`Europe/Rome`,`Europe/Samara`,`Europe/San_Marino`,`Europe/Sarajevo`,`Europe/Saratov`,`Europe/Simferopol`,`Europe/Skopje`,`Europe/Sofia`,`Europe/Stockholm`,`Europe/Tallinn`,`Europe/Tirane`,`Europe/Tiraspol`,`Europe/Ulyanovsk`,`Europe/Uzhgorod`,`Europe/Vaduz`,`Europe/Vatican`,`Europe/Vienna`,`Europe/Vilnius`,`Europe/Volgograd`,`Europe/Warsaw`,`Europe/Zagreb`,`Europe/Zaporozhye`,`Europe/Zurich`,`GB`,`GB-Eire`,`GMT`,`GMT0`,`Greenwich`,`Hongkong`,`Iceland`,`Indian/Antananarivo`,`Indian/Chagos`,`Indian/Christmas`,`Indian/Cocos`,`Indian/Comoro`,`Indian/Kerguelen`,`Indian/Mahe`,`Indian/Maldives`,`Indian/Mauritius`,`Indian/Mayotte`,`Indian/Reunion`,`Iran`,`Israel`,`Jamaica`,`Japan`,`Kwajalein`,`Libya`,`MET`,`MST7MDT`,`Mexico/BajaNorte`,`Mexico/BajaSur`,`Mexico/General`,`NZ`,`NZ-CHAT`,`Navajo`,`PRC`,`PST8PDT`,`Pacific/Apia`,`Pacific/Auckland`,`Pacific/Bougainville`,`Pacific/Chatham`,`Pacific/Chuuk`,`Pacific/Easter`,`Pacific/Efate`,`Pacific/Enderbury`,`Pacific/Fakaofo`,`Pacific/Fiji`,`Pacific/Funafuti`,`Pacific/Galapagos`,`Pacific/Gambier`,`Pacific/Guadalcanal`,`Pacific/Guam`,`Pacific/Honolulu`,`Pacific/Johnston`,`Pacific/Kiritimati`,`Pacific/Kosrae`,`Pacific/Kwajalein`,`Pacific/Majuro`,`Pacific/Marquesas`,`Pacific/Midway`,`Pacific/Nauru`,`Pacific/Niue`,`Pacific/Norfolk`,`Pacific/Noumea`,`Pacific/Pago_Pago`,`Pacific/Palau`,`Pacific/Pitcairn`,`Pacific/Pohnpei`,`Pacific/Ponape`,`Pacific/Port_Moresby`,`Pacific/Rarotonga`,`Pacific/Saipan`,`Pacific/Samoa`,`Pacific/Tahiti`,`Pacific/Tarawa`,`Pacific/Tongatapu`,`Pacific/Truk`,`Pacific/Wake`,`Pacific/Wallis`,`Pacific/Yap`,`Poland`,`Portugal`,`ROK`,`Singapore`,`Turkey`,`UCT`,`US/Alaska`,`US/Aleutian`,`US/Arizona`,`US/Central`,`US/East-Indiana`,`US/Eastern`,`US/Hawaii`,`US/Indiana-Starke`,`US/Michigan`,`US/Mountain`,`US/Pacific`,`US/Pacific-New`,`US/Samoa`,`UTC`,`Universal`,`W-SU`,`WET`,`Zulu` |  |
| locale | string | An enumeration.  Enum: `de`,`en`,`hu`,`it`,`nl`,`sv` |  |

Expand 400

Bad request

401

Not authorized

415

Unsupported media type

422

Validation Error

500

Internal server error

 Response
### Reset Timezone Locale

Reset user timezone and locale settings

Auth apiKeyDELETE /api/users/reset-timezone-localecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Avatar Image

Get use avatar image

Auth apiKeyPath Params

| account_id | string |  |  |
| --- | --- | --- | --- |

GET /api/users/{account_id}/avatarcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Create API Key

Create API key for current user

Auth apiKeyPOST /api/users/api-key/createcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| UserApiKey | object | Model for user API key create and set |  |
| --- | --- | --- | --- |
| api_key | string |  |  |

400

Bad request

401

Not authorized

 Response
### Set API key

Set API key for current user

Auth apiKeyRequest Body application/json

| UserApiKey | object | Model for user API key create and set |  |
| --- | --- | --- | --- |
| api_key | string |  |  |

POST /api/users/api-key/setcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Remove API Key

Remove user's API key

Auth apiKeyPOST /api/users/api-key/removecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

404

Item not found

 Response
### Mark notification as viewed by user

Mark notification as viewed by user

Auth apiKeyPath Params

| notification | string | Enum: `dark_theme` |  |
| --- | --- | --- | --- |

POST /api/users/notifications/{notification}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

422

Validation Error

 Response
### Delete Report

Delete a report

Users can only delete their own reports

Auth apiKeyPath Params

| report_id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/users/reports/{report_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

403

Forbidden

404

Item not found

422

Validation Error

 Response
### Get Public ReportsDeprecated

Get all public reports

Auth apiKeyQuery String

| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| page_size |  | Page size  Default: 10 |  |

GET /api/users/uploadscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportSearchResponse | object | Search response returned to user |  |
| --- | --- | --- | --- |
| items | array |  |  |
| count | integer |  |  |
| count_search_params | integer |  |  |
| method | string |  |  |
| dbs_sync | boolean |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get User ReportsDeprecated

Get reports of current user

Auth apiKeyQuery String

| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| page_size |  | Page size  Default: 10 |  |
| date_from | string | Results newer then this date (format YYYY-MM-DD) |  |
| verdict | string | Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

GET /api/users/me/uploadscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReportSearchResponse | object | Search response returned to user |  |
| --- | --- | --- | --- |
| items | array |  |  |
| count | integer |  |  |
| count_search_params | integer |  |  |
| method | string |  |  |
| dbs_sync | boolean |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get User Stat

Get app statistics for current user or for all users

Auth apiKeyQuery String

| types | array | Enum: `count_malicious_ips_by_user`,`count_verdicts_by_user`,`count_reports_by_user`,`count_uploads_by_user` |  |
| --- | --- | --- | --- |
| all_users | boolean | Default: false |  |
| period | string |  |  |

GET /api/users/statcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| UserStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| user3 fields | object |  |  |
| account_id | string |  |  |
| username | string |  |  |
| pseudoname | string |  |  |
| name | string |  |  |
| updated_date | date-time |  |  |

401

Not authorized

403

Forbidden

422

Validation Error

 Response
### Get User Generic Stat

Get app statistics not related to specific user

Auth apiKeyQuery String

| types | array | Enum: `count_reports`,`count_verdicts`,`count_iocs`,`count_iocs_per_period`,`count_yaras`,`count_users`,`count_users_signup_by_day`,`count_users_signin_by_day`,`fix_old_count_users_signin_by_day`,`count_active_users`,`count_users_uploads`,`count_uploads_by_date`,`count_reports_by_extension`,`count_malicious_reports_by_extension`,`count_malicious_reports_by_language`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_by_user`,`count_malicious_ips_ratio`,`count_verdicts_by_date`,`count_verdicts_by_user`,`count_reports_by_date`,`count_reports_by_user`,`count_uploads_by_user`,`count_malicious_signal_groups`,`count_mitre_techniques_by_period`,`count_yaras_per_period`,`count_top_level_domains`,`count_phishing_brands`,`count_api_calls`,`count_ips`,`count_domains`,`count_sha256`,`average_scan_time`,`frequent_tags`,`frequent_yara_tags`,`most_interesting`,`finalize_fakely_hanged_reports`,`system_info`,`clean_storage`,`do_retention`,`do_healthcheck`,`get_fuzzyhashes_verdicts`,`delete_reports`,`postprocess_iocs`,`new_search_fix_search_params`,`count_initial_scan_jobs_by_date`,`count_rescan_jobs_by_date`,`count_mitre_techniques`,`load_mitre_data`,`get_intersting_score`,`collect_daily_reports`,`collect_daily_yara`,`fix_link_mime_type`,`update_sitemap`,`send_emails_queue`,`update_sourcetype_based_on_shorttype`,`copy_app_errors`,`add_country_search_param`,`set_pseudonames`,`normalize_verdict_history`,`delete_search_indexes`,`create_search_indexes`,`count_search_params`,`report_ocm_status`,`set_uploads_date_fields`,`set_auditor_features`,`change_additional_scan_steps`,`set_new_logos`,`count_reports_states_by_date`,`count_reports_extensions_by_date`,`report_usage_to_ocm`,`fix_origins_relations`,`old_errors_cleanup`,`cleanup_report_format_history`,`calculate_storage`,`check_license_scan_limit`,`generate_yara_xml_feed`,`send_report_summary`,`mark_failed_reports_for_deletion`,`engine_database_update`,`frequent_signal_tags`,`frequent_malware_tags` |  |
| --- | --- | --- | --- |
| period | string |  |  |

Expand GET /api/users/stat/genericcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AppStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| value Choice 1Choice 2Choice 3Choice 4Choice 5 |  |  |  |
| boolean | boolean |  |  |
| updated_date | date-time |  |  |

400

Bad request

401

Not authorized

403

Forbidden

422

Validation Error

 Response
### Get Reports Stat

Get app statistics, which is saved per reports verdicts

Auth apiKeyQuery String

| types | array | Statistics types |  |
| --- | --- | --- | --- |
| date_from | string | Start of time period or the only one date to fetch |  |
| date_to | string | End of time period to fetch |  |
| verdicts | array | Reports verdicts filter  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| order |  | Order applied to statistics items  Default: desc |  |
| page | integer | Page number starting from 1  minimum: 1  Default: 1 |  |
| page_size |  | Page size  Default: 20 |  |
| asc_order | array | Statistic types that should be sorted ascending  Default: [] |  |
| desc_order | array | Statistic types that should be sorted descending  Default: [] |  |

GET /api/users/stat/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| VerdictDateStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| stat_name VerdictDateGenericStatNameVerdictDateStandaloneStatName |  |  |  |
| VerdictDateGenericStatName | string | Name of statistics types that should be stored together in a single collection  Enum: `count_malicious_signal_groups`,`count_mitre_techniques_by_period`,`frequent_yara_tags`,`frequent_malware_tags`,`count_yaras_per_period`,`count_malicious_reports_by_extension`,`count_api_calls`,`count_top_level_domains`,`count_malicious_reports_by_language`,`count_phishing_brands`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_ratio`,`count_iocs_per_period`,`average_scan_time` |  |
| items3 fields | array[object] |  |  |
| name | string |  |  |
| value | number |  |  |
| country_name | string |  |  |
| order | string | In case user needs to specify the order of requested items  Enum: `asc`,`desc` |  |

Expand 400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Reports Verdicts Amount

Get amount of reports verdicts for provided IOCs

Auth apiKeyQuery String

| date_from | string | Start of time period or the only one date to fetch |  |
| --- | --- | --- | --- |
| date_to | string | End of time period to fetch |  |
| verdicts | array | Reports verdicts filter  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

Request Body application/json

| VerdictsAmountPayload | object |  |  |
| --- | --- | --- | --- |
| data | array[object] |  |  |
| items | array[string] |  |  |
| stat_name VerdictDateGenericStatNameVerdictDateStandaloneStatName |  |  |  |
| VerdictDateGenericStatName | string | Name of statistics types that should be stored together in a single collection  Enum: `count_malicious_signal_groups`,`count_mitre_techniques_by_period`,`frequent_yara_tags`,`frequent_malware_tags`,`count_yaras_per_period`,`count_malicious_reports_by_extension`,`count_api_calls`,`count_top_level_domains`,`count_malicious_reports_by_language`,`count_phishing_brands`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_ratio`,`count_iocs_per_period`,`average_scan_time` |  |

POST /api/users/stat/reports/verdicts/amountcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| VerdictAmountResponse | array[object] |  |  |
| --- | --- | --- | --- |
| stat_name VerdictDateGenericStatNameVerdictDateStandaloneStatName |  |  |  |
| VerdictDateGenericStatName | string | Name of statistics types that should be stored together in a single collection  Enum: `count_malicious_signal_groups`,`count_mitre_techniques_by_period`,`frequent_yara_tags`,`frequent_malware_tags`,`count_yaras_per_period`,`count_malicious_reports_by_extension`,`count_api_calls`,`count_top_level_domains`,`count_malicious_reports_by_language`,`count_phishing_brands`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_ratio`,`count_iocs_per_period`,`average_scan_time` |  |
| items2 fields | array[object] |  |  |
| item | string |  |  |
| verdicts | object |  |  |
| * | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Reports Verdicts Dates

Get distribution of reports verdicts for provided IOCs by dates

Auth apiKeyQuery String

| date_from | string | Start of time period or the only one date to fetch |  |
| --- | --- | --- | --- |
| date_to | string | End of time period to fetch |  |
| verdicts | array | Reports verdicts filter  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

Request Body application/json

| VerdictsDatesPayload | object |  |  |
| --- | --- | --- | --- |
| data | array[object] |  |  |
| items | array[string] |  |  |
| stat_name VerdictDateGenericStatNameVerdictDateStandaloneStatName |  |  |  |
| VerdictDateGenericStatName | string | Name of statistics types that should be stored together in a single collection  Enum: `count_malicious_signal_groups`,`count_mitre_techniques_by_period`,`frequent_yara_tags`,`frequent_malware_tags`,`count_yaras_per_period`,`count_malicious_reports_by_extension`,`count_api_calls`,`count_top_level_domains`,`count_malicious_reports_by_language`,`count_phishing_brands`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_ratio`,`count_iocs_per_period`,`average_scan_time` |  |

POST /api/users/stat/reports/verdicts/datescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| VerdictDatesResponse | array[object] |  |  |
| --- | --- | --- | --- |
| stat_name VerdictDateGenericStatNameVerdictDateStandaloneStatName |  |  |  |
| VerdictDateGenericStatName | string | Name of statistics types that should be stored together in a single collection  Enum: `count_malicious_signal_groups`,`count_mitre_techniques_by_period`,`frequent_yara_tags`,`frequent_malware_tags`,`count_yaras_per_period`,`count_malicious_reports_by_extension`,`count_api_calls`,`count_top_level_domains`,`count_malicious_reports_by_language`,`count_phishing_brands`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_ratio`,`count_iocs_per_period`,`average_scan_time` |  |
| items3 fields | array[object] |  |  |
| item | string |  |  |
| total_verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| verdicts | object |  |  |
| * | object |  |  |
| * | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Malicious Ips Stat

Get statistics on malicious IPs

Auth apiKeyQuery String

| period | string |  |  |
| --- | --- | --- | --- |
| target | string |  |  |

GET /api/users/stat/malicious-ipscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

AppStat.__pydantic_model__UserStat.__pydantic_model__

| AppStat | object | Generic statistic record.  Can hold statistics of any type. |  |
| --- | --- | --- | --- |
| name | string |  |  |
| period | string |  |  |
| updated_date | date-time |  |  |
| id | string |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Ioc Stat

Get app statistics

Auth apiKeyGET /api/users/stat/iocscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| StatForResponse | object |  |  |
| --- | --- | --- | --- |
| count Choice 1Choice 2 |  |  |  |
| integer | integer |  |  |
| updated | date-time |  |  |

401

Not authorized

 Response
### Get Yara Stat

Get yara statistics

Auth apiKeyGET /api/users/stat/yaracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| StatForYaraResponse | object |  |  |
| --- | --- | --- | --- |
| count Choice 1Choice 2 |  |  |  |
| integer | integer |  |  |
| updated | date-time |  |  |

401

Not authorized

 Response
### Get Mitre Stat

Get statistics on MITRE techniques used in reports

Auth apiKeyGET /api/users/stat/mitrecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| StatForResponse | object |  |  |
| --- | --- | --- | --- |
| count Choice 1Choice 2 |  |  |  |
| integer | integer |  |  |
| updated | date-time |  |  |

401

Not authorized

 Response
### Get Yara Info

Get yara repo info

Auth apiKeyGET /api/users/info/yaracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| YaraInfoResponse | object |  |  |
| --- | --- | --- | --- |
| info | array[object] |  |  |
| revision | string |  |  |
| url | string |  |  |

401

Not authorized

 Response
## System

Various helper and system functionality.

Endpoints[GET/api/system/info](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-default-api-system-info-get) [GET/api/system/version](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-version-api-system-version-get) [GET/api/system/config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-config-api-system-config-get) [GET/api/system/get-terms/{terms_type}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-terms-api-system-get-terms--terms-type--get) [GET/api/system/signal-groups](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-signal-groups-api-system-signal-groups-get) [GET/api/system/mime-types](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-mime-types-api-system-mime-types-get) [GET/api/system/yara](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-yara-rules-api-system-yara-get) [GET/api/system/yara-authors](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-yara-authors-api-system-yara-authors-get) [GET/api/system/translations/{lang}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-translations-api-system-translations--lang--get) [GET/api/system/languages](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-languages-api-system-languages-get) [GET/api/system/countries](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-countries-api-system-countries-get) [GET/api/system/mitre](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-mitre-data-api-system-mitre-get) [POST/api/system/errors/log](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#log-client-error-api-system-errors-log-post) [GET/api/system/logo](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-logo-api-system-logo-get) [GET/api/system/do-healthcheck](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#do-healthcheck-api-system-do-healthcheck-get) [GET/api/system/query-full-healthcheck](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#query-healthcheck-api-system-query-full-healthcheck-get) [GET/api/system/query-healthcheck](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#query-healthcheck-api-system-query-healthcheck-get) [GET/api/system/license](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#check-license-info-api-system-license-get) [POST/api/system/license/activate/online](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#activate-license-online-api-system-license-activate-online-post) [POST/api/system/license/activate/offline](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#activate-license-offline-api-system-license-activate-offline-pos) [DELETE/api/system/license/deactivate](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#deactivate-license-api-system-license-deactivate-delete) [GET/api/system/reputation/check-config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#reputation-check-config-api-system-reputation-check-config-get) [GET/api/system/news](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-news-api-system-news-get)
### Get Default

Return general information about webservice, just to indicate that API is working

Auth apiKeyGET /api/system/infocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| GeneralSystemInfo | object | Response model for /api/system/info endpoint |  |
| --- | --- | --- | --- |
| title | string |  |  |
| description | string |  |  |
| api_version | string |  |  |
| release_version | string |  |  |
| release_date | date-time |  |  |

 Response
### Get Version

Return the version of the webservice

Auth apiKeyGET /api/system/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Version Api System Version Get | string |  |  |
| --- | --- | --- | --- |

 Response
### Get Config

Obtain project configuration to use on front-end

Auth apiKeyGET /api/system/configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| SystemConfig | object | Response model for /api/system/config endpoint |  |
| --- | --- | --- | --- |
| baseUrl | string |  |  |
| allowAnonymousUsers | boolean |  |  |
| appTitle | string |  |  |
| appDescription | string |  |  |
| adFrequency | integer |  |  |
| buildType | string | An enumeration.  Enum: `default`,`community`,`develop`,`onpremise` |  |
| maxUploadSize | integer |  |  |
| maxUploadSizeLimit | integer |  |  |
| username | object | Username config model for SystemConfig response model |  |
| maximum_length | integer |  |  |
| regex | string |  |  |
| password4 fields | object | Password config model for SystemConfig response model |  |
| alpha_numeric | boolean |  |  |
| minimum_length | integer |  |  |
| mixed_case | boolean |  |  |
| special_characters | boolean |  |  |
| tokenExpire3 fields | object | TokenExpire config model for SystemConfig response model |  |
| signupConfirm | integer |  |  |
| passwordReset | integer |  |  |
| invite | integer |  |  |
| reports6 fields | object | Reports config model for SystemConfig response model |  |
| queryInterval | object | QueryInterval config model for ReportsConfig model |  |
| initial | integer |  |  |
| withData | integer |  |  |
| signalTypeUpperLimit | object | SignalTypeUpperLimit config model for ReportsConfig model |  |
| informational | number |  |  |
| suspicious | number |  |  |
| search4 fields | object | Search config model for ReportsConfig model |  |
| page_size | integer |  |  |
| page_size_options | array[integer] |  |  |
| reportsLimit | integer |  |  |
| monthsLimit | integer |  |  |
| maxRetryCount | integer |  |  |
| viewFileContentSizeLimit | integer |  |  |
| keepJobResultSeconds | integer |  |  |
| queueJobTimeout | integer |  |  |
| languages | object | Languages config model for SystemConfig response model |  |
| language | string |  |  |
| code | string |  |  |
| scanFilesPerUpload | integer |  |  |
| googleAnalyticsID | string |  |  |
| googleAnalyticsUA | string |  |  |
| matomoContainerPath | string |  |  |
| supportedTypes | array[string] | Enum: `ace`,`apk`,`bat`,`64bits`,`bmp`,`csv`,`doc`,`docm`,`docx`,`dot`,`dotm`,`dotx`,`elf`,`eml`,`gif`,`hta`,`htm`,`html`,`iso`,`java`,`java-bytecode`,`javascript`,`jpg`,`lnk`,`mbox`,`mhtml`,`msg`,`msi`,`mso`,`odp`,`ods`,`odt`,`odg`,`odf`,`odc`,`odb`,`odi`,`ole`,`one`,`pdf`,`pedll`,`peexe`,`png`,`pot`,`potm`,`potx`,`powershell`,`ppt`,`pptm`,`pptx`,`ps`,`pub`,`rar`,`rfc822`,`rtf`,`svg`,`txt`,`vbs`,`wmv`,`wsf`,`xlm`,`xls`,`xlsb`,`xlsm`,`xlsx`,`xlt`,`xltm`,`xltx`,`xml`,`xsl`,`zip`,`7zip`,`exe`,`mail`,`ms-office`,`script` |  |
| fileCategories | object |  |  |
| * | array[string] |  |  |
| fileGeneralTypes | object |  |  |
| * | array[string] |  |  |
| constantStrings | array[string] |  |  |
| defaultTheme | string |  |  |
| iocs3 fields | object | IOCs config model for SystemConfig response model |  |
| prevalenceExceptWhitelists | boolean |  |  |
| genQueryExceptWhitelists | boolean |  |  |
| prevalenceDayOptions | array[integer] | Enum: `7`,`14`,`30`,`-1` |  |
| admin | object | Admin config model for SystemConfig response model |  |
| pageSize | integer |  |  |
| logoSelectedTime2 fields | object | LogoSelectedTime config model for SystemConfig response model |  |
| light3 fields | object | LogoTypeSelectedTime config model for LogoSelectedTimeConfig model |  |
| main | integer |  |  |
| top_menu | integer |  |  |
| footer | integer |  |  |
| dark3 fields | object | LogoTypeSelectedTime config model for LogoSelectedTimeConfig model |  |
| main | integer |  |  |
| top_menu | integer |  |  |
| footer | integer |  |  |
| askTermsConsent | boolean |  |  |
| scanBigFileSize | integer |  |  |
| statOverview3 fields | object | StatOverview config model for SystemConfig response model |  |
| timelineMonths | array[string] |  |  |
| topItemsLimit | integer |  |  |
| leaderboardItemsLimit | integer |  |  |
| jobs3 fields | object | Jobs config model for SystemConfig response model |  |
| memoryLimit | integer |  |  |
| chartControlTime | integer |  |  |
| memoryUsageTop | integer |  |  |
| similaritySearchEnabled | boolean |  |  |
| TLDTypes | array[string] | Enum: `com`,`org`,`edu`,`gov`,`uk`,`net`,`ca`,`de`,`jp`,`fr`,`au`,`us`,`ru`,`ch`,`it`,`nl`,`se`,`no`,`es`,`mil`,`aero`,`biz`,`coop`,`info`,`museum`,`name`,`pro`,`ac`,`ad`,`ae`,`af`,`ag`,`al`,`ai`,`am`,`ao`,`aq`,`ar`,`as`,`at`,`az`,`ba`,`bb`,`be`,`bf`,`bg`,`bh`,`bm`,`bn`,`bo`,`br`,`bt`,`bw`,`by`,`bz`,`cc`,`cd`,`cg`,`cl`,`cm`,`co`,`cr`,`cu`,`cx`,`cy`,`cz`,`dj`,`dk`,`do`,`dz`,`ec`,`ee`,`eg`,`et`,`fi`,`fj`,`fm`,`fo`,`ga`,`ge`,`gg`,`gh`,`gi`,`gl`,`gr`,`gs`,`gt`,`hk`,`hm`,`hn`,`hr`,`hu`,`id`,`ie`,`il`,`im`,`io`,`ir`,`je`,`jm`,`jo`,`ke`,`kg`,`kh`,`ki`,`kr`,`kw`,`ky`,`kz`,`la`,`lb`,`li`,`lk`,`lt`,`lu`,`lv`,`ly`,`ma`,`mc`,`md`,`mg`,`mk`,`mm`,`mn`,`mo`,`mp`,`mr`,`ms`,`mt`,`mu`,`mv`,`mx`,`my`,`mz`,`na`,`nc`,`ne`,`ng`,`ni`,`np`,`nr`,`nu`,`nz`,`om`,`pa`,`pe`,`pf`,`pg`,`ph`,`pk`,`pl`,`pr`,`pt`,`pw`,`qa`,`re`,`ro`,`rw`,`sa`,`sc`,`sg`,`sh`,`si`,`sk`,`sm`,`sn`,`sr`,`st`,`sv`,`sy`,`tc`,`tf`,`th`,`tj`,`tk`,`tm`,`tn`,`to`,`tp`,`tr`,`tt`,`tv`,`tw`,`tz`,`ua`,`ug`,`uy`,`uz`,`va`,`vc`,`ve`,`vg`,`vi`,`vn`,`vu`,`ws`,`ye`,`yu`,`za`,`zm`,`zw` |  |
| showFooter | boolean |  |  |
| maintenance4 fields | object | Maintenance config model for SystemConfig response model |  |
| blockScan | boolean |  |  |
| blockScanNotification | string |  |  |
| blockSearch | boolean |  |  |
| blockSearchNotification | string |  |  |
| allowedFeatures | array[string] |  |  |
| ocm | object | OCM config model for SystemConfig response model |  |
| clientUrl | string |  |  |
| extraButton3 fields | object | ExtraButton config model for SystemConfig response model |  |
| text | string |  |  |
| link | string |  |  |
| active | boolean |  |  |
| newsLimit | integer |  |  |
| automaticReportFilesDownload | boolean |  |  |

Expand  Response
### Get Terms

Obtain privacy policy and terms & conditions

Auth apiKeyPath Params

| terms_type | string | Enum: `privacy-policy`,`terms-condition`,`cookie-policy` |  |
| --- | --- | --- | --- |

GET /api/system/get-terms/{terms_type}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Terms Api System Get Terms Terms Type Get | string |  |  |
| --- | --- | --- | --- |

404

Item not found

422

Validation Error

 Response
### Get Signal Groups

Obtain signal groups list

Auth apiKeyGET /api/system/signal-groupscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| SignalGroupsResponse | array[object] |  |  |
| --- | --- | --- | --- |
| type | string |  |  |
| name | string |  |  |
| category | string |  |  |
| groups5 fields | array[object] |  |  |
| id | string |  |  |
| description | string |  |  |
| mime_type | string |  |  |
| mitre_technique_ids | string |  |  |
| strength | string |  |  |

401

Not authorized

 Response
### Get Mime Types

Obtain mime type list

Auth apiKeyGET /api/system/mime-typescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| array | array[string] |  |  |
| --- | --- | --- | --- |

401

Not authorized

 Response
### Get Yara Rules

Get extended data of yara rules

If the `name` parameter is left empty, it returns the list of yara rules that already has a match in the system.
Otherwise it will return a list of yara rules where the yara rule name matches the `name` parameter even if the yara rule has no match in the system.

Auth apiKeyQuery String

| name | array | Name of the YARA rule  Default: [] |  |
| --- | --- | --- | --- |

GET /api/system/yaracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| YaraRuleResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| author | string |  |  |
| strength | number |  |  |
| created_date | date-time |  |  |
| description | string |  |  |
| other_data | object |  |  |
| content | string |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Yara Authors

Get yara rules authors

If the `name` parameter is left empty, it returns the list of yara rule authors that already has a match in the system.
Otherwise it will return a list of yara rule authors where the yara rule name matches the `name` parameter even if the yara rule has no match in the system.

Auth apiKeyQuery String

| name | array | Name of the YARA rule  Default: [] |  |
| --- | --- | --- | --- |

GET /api/system/yara-authorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| array | array[string] |  |  |
| --- | --- | --- | --- |

401

Not authorized

422

Validation Error

 Response
### Get Translations

Obtain translations for specific language

Auth apiKeyPath Params

| lang | string | Enum: `en`,`de`,`zh`,`es`,`hi`,`ar`,`pt`,`bn`,`ru`,`ja`,`ko`,`fr`,`te`,`mr`,`tr`,`ta`,`vi`,`ur` |  |
| --- | --- | --- | --- |

GET /api/system/translations/{lang}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Translations Api System Translations Lang Get | object |  |  |
| --- | --- | --- | --- |
| * | string |  |  |

422

Validation Error

 Response
### Get Languages

Obtain list of all detectable (and probably even more) languages

Auth apiKeyGET /api/system/languagescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Languages Api System Languages Get | object |  |  |
| --- | --- | --- | --- |
| * | string |  |  |

404

Item not found

 Response
### Get Countries

Obtain list of all countries

Auth apiKeyGET /api/system/countriescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Countries Api System Countries Get | object |  |  |
| --- | --- | --- | --- |
| * | string |  |  |

404

Item not found

 Response
### Get Mitre Data

Obtain MITRE tactics and techniques

Auth apiKeyGET /api/system/mitrecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Mitre Data Api System Mitre Get | object |  |  |
| --- | --- | --- | --- |
| *4 fields | object | Response model for /api/system/mitre endpoint |  |
| techniques | object |  |  |
| *3 fields | object | MitreTechnique model for MitreDataResponse model |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |

404

Item not found

 Response
### Log Client Error

Log frontend cliend errors

Auth apiKeyPOST /api/system/errors/logcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

 Response
### Get Logo

Get logo image

Auth apiKeyQuery String

| type |  | Default: main |  |
| --- | --- | --- | --- |
| theme |  | Default: light |  |
| name | string |  |  |

GET /api/system/logocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Successful Response

| No response body |
| --- |

404

Item not found

422

Validation Error

 Response
### Do Healthcheck

Do an immediate healthcheck and return the state

Auth apiKeyGET /api/system/do-healthcheckcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DoHealthcheckOutput | object |  |  |
| --- | --- | --- | --- |
| created_date | date-time |  |  |
| frontend_health2 fields | object | Frontent health log |  |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| calculated_health | boolean | Default: false |  |
| webservice_health8 fields | object | Webservice health log |  |
| http_info_direct3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response_direct | object |  |  |
| http_info_nginx3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response_nginx | object |  |  |
| number_of_all_users | integer |  |  |
| number_of_active_users | integer |  |  |
| tasks_queues2 fields | object |  |  |
| total_healthy | boolean | Health verdict |  |
| queues5 fields | array[object] | Details about each queue health verdict |  |
| queue_name | string | Name of tasks queue |  |
| check_type | string | Type of health check we have verdict for  Enum: `long_run`,`new_run`,`all` |  |
| healthy | boolean | Health verdict |  |
| last_date_healthy | date-time | Last time queue was reported as working |  |
| data | object | Arbitrary data we can save as health state |  |
| calculated_health | boolean | Default: false |  |
| fstransform_health3 fields | array[object] |  |  |
| response | object |  |  |
| instance_id | string |  |  |
| calculated_health | boolean | Default: false |  |
| fsbroker_health3 fields | object | Fsbroker health log |  |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response | object |  |  |
| calculated_health | boolean | Default: false |  |

401

Not authorized

 Response
### Query Healthcheck

Query past healthcheck logs

Auth apiKeyQuery String

| days | integer | Default: 90 |  |
| --- | --- | --- | --- |
| days_from | integer | Default: 0 |  |

GET /api/system/query-full-healthcheckcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DoHealthcheckOutput | array[object] |  |  |
| --- | --- | --- | --- |
| created_date | date-time |  |  |
| frontend_health2 fields | object | Frontent health log |  |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| calculated_health | boolean | Default: false |  |
| webservice_health8 fields | object | Webservice health log |  |
| http_info_direct3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response_direct | object |  |  |
| http_info_nginx3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response_nginx | object |  |  |
| number_of_all_users | integer |  |  |
| number_of_active_users | integer |  |  |
| tasks_queues2 fields | object |  |  |
| total_healthy | boolean | Health verdict |  |
| queues5 fields | array[object] | Details about each queue health verdict |  |
| queue_name | string | Name of tasks queue |  |
| check_type | string | Type of health check we have verdict for  Enum: `long_run`,`new_run`,`all` |  |
| healthy | boolean | Health verdict |  |
| last_date_healthy | date-time | Last time queue was reported as working |  |
| data | object | Arbitrary data we can save as health state |  |
| calculated_health | boolean | Default: false |  |
| fstransform_health3 fields | array[object] |  |  |
| response | object |  |  |
| instance_id | string |  |  |
| calculated_health | boolean | Default: false |  |
| fsbroker_health3 fields | object | Fsbroker health log |  |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response | object |  |  |
| calculated_health | boolean | Default: false |  |

401

Not authorized

422

Validation Error

 Response
### Query Healthcheck

Query sanitized past healthcheck logs

Auth apiKeyQuery String

| days | integer | Default: 90 |  |
| --- | --- | --- | --- |
| days_from | integer | Default: 0 |  |

GET /api/system/query-healthcheckcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| SanitizedHealthCheckOutput | array[object] |  |  |
| --- | --- | --- | --- |
| created_date | date-time |  |  |
| frontend_health | object |  |  |
| webservice_health | object |  |  |
| fstransform_health | array[object] |  |  |
| fsbroker_health | object |  |  |

422

Validation Error

 Response
### Check License Info

Get license information

Auth apiKeyGET /api/system/licensecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| LicenseResponse | object | Fsbroker health log |  |
| --- | --- | --- | --- |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response Choice 1LicenseInfoFstransformDict.__pydantic_model__ |  |  |  |
| object | object |  |  |
| message | string |  |  |
| calculated_health | boolean | Default: false |  |

401

Not authorized

 Response
### Activate License Online

Activate license online, using license key

Auth apiKeyRequest Body application/json

| LicenseActivateOnlinePayload | object |  |  |
| --- | --- | --- | --- |
| app_server | string |  |  |
| license_key | string |  |  |

POST /api/system/license/activate/onlinecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| LicenseResponse | object | Fsbroker health log |  |
| --- | --- | --- | --- |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response Choice 1LicenseInfoFstransformDict.__pydantic_model__ |  |  |  |
| object | object |  |  |
| message | string |  |  |
| calculated_health | boolean | Default: false |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Activate License Offline

Activate license, using license file

Auth apiKeyRequest Body application/x-www-form-urlencoded

| Body_activate_license_offline_api_system_license_activate_offline_post | object |  |  |
| --- | --- | --- | --- |
| app_server | string |  |  |

POST /api/system/license/activate/offlinecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| LicenseResponse | object | Fsbroker health log |  |
| --- | --- | --- | --- |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response Choice 1LicenseInfoFstransformDict.__pydantic_model__ |  |  |  |
| object | object |  |  |
| message | string |  |  |
| calculated_health | boolean | Default: false |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Deactivate License

Deactivate license

Auth apiKeyQuery String

| app_server | string |  |  |
| --- | --- | --- | --- |

DELETE /api/system/license/deactivatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| LicenseResponse | object | Fsbroker health log |  |
| --- | --- | --- | --- |
| http_info3 fields | object | HTTP health log |  |
| response_time_ms | integer |  |  |
| response_code_http | integer |  |  |
| request_success | boolean |  |  |
| response Choice 1LicenseInfoFstransformDict.__pydantic_model__ |  |  |  |
| object | object |  |  |
| message | string |  |  |
| calculated_health | boolean | Default: false |  |

401

Not authorized

404

Item not found

422

Validation Error

500

Internal server error

 Response
### Reputation Check Config

Check if MD Cloud Reputation is enabled

If in the /config `opswatReputationAPIKeySource` value `FALLBACK`, it returns `False`.
If `opswatReputationAPIKeySource` is `LICENSE` or `USER`, it returns `True`

Auth apiKeyGET /api/system/reputation/check-configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReputationCheckConfigResponse | object |  |  |
| --- | --- | --- | --- |
| reputation_enabled | boolean |  |  |

 Response
### Get News

Get news

Auth apiKeyGET /api/system/newscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| NewsItemResponse | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| link | string |  |  |
| date | string | Represenation of news date, is shown as is |  |
| text | string |  |  |
| images | string | Comma separated list of images URLs |  |
| order | integer | In what order news should be shown |  |
| active | boolean | If this news item should be shown |  |

 Response
## Admin

Functionality for site admins.

Endpoints[GET/api/debug/reports](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-report-api-debug-reports-get) [POST/api/system/news](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#save-news-item-api-system-news-post) [DELETE/api/system/news](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-news-item-api-system-news-delete) [DELETE/api/admin/reports/{report_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#delete-report-api-admin-reports--report-id--delete) [GET/api/admin/access-groups](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-access-groups-api-admin-access-groups-get) [POST/api/admin/access-groups](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#save-access-group-api-admin-access-groups-post) [POST/api/admin/access-groups/{group_id}/remove](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-access-group-api-admin-access-groups--group-id--remove-po) [GET/api/admin/settings/api-quota](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-api-quota-api-admin-settings-api-quota-get) [POST/api/admin/settings/api-quota](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#save-api-quota-api-admin-settings-api-quota-post) [POST/api/admin/settings/api-quota/{quota_id}/remove](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-api-quota-api-admin-settings-api-quota--quota-id--remove-) [GET/api/admin/settings/{group}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-settings-group-api-admin-settings--group--get) [POST/api/admin/settings/{group}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#save-settings-group-api-admin-settings--group--post) [GET/api/admin/auth-services](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-auth-services-api-admin-auth-services-get) [POST/api/admin/auth-services](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#save-auth-service-api-admin-auth-services-post) [POST/api/admin/auth-services/{service}/remove](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-auth-service-api-admin-auth-services--service--remove-pos) [GET/api/admin/users](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-users-api-admin-users-get) [GET/api/admin/users/import](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-users-overview-api-admin-users-import-get) [GET/api/admin/users/{user_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-api-admin-users--user-id--get) [POST/api/admin/users/{user_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#edit-user-api-admin-users--user-id--post) [DELETE/api/admin/users/{user_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#delete-user-api-admin-users--user-id--delete) [GET/api/admin/users/{user_id}/uploads](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-uploads-api-admin-users--user-id--uploads-get) [GET/api/admin/users/{user_id}/reset-password](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-reset-password-link-api-admin-users--user-id--reset-pas) [GET/api/admin/app-config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-app-config-api-admin-app-config-get) [GET/api/admin/stat/services](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-services-stat-api-admin-stat-services-get) [POST/api/admin/invite](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#generate-invite-token-api-admin-invite-post) [GET/api/admin/generate-external-tokens-secret](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#generate-external-tokens-secret-api-admin-generate-external-toke) [GET/api/admin/errors](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-app-errors-api-admin-errors-get) [DELETE/api/admin/errors](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-app-errors-api-admin-errors-delete) [DELETE/api/admin/errors/{error_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#app-error-api-admin-errors--error-id--delete) [POST/api/admin/errors/{error_id}/note](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#edit-app-error-note-api-admin-errors--error-id--note-post) [GET/api/admin/errors/export](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#export-errors-api-admin-errors-export-get) [GET/api/admin/logs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-generic-logs-api-admin-logs-get) [DELETE/api/admin/logs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-generic-logs-api-admin-logs-delete) [GET/api/admin/retention-calculation](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#calculate-retention-api-admin-retention-calculation-get) [GET/api/admin/logs/{log_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-full-generic-log-api-admin-logs--log-id--get) [DELETE/api/admin/logs/{log_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-generic-log-api-admin-logs--log-id--delete) [POST/api/admin/logs/{log_id}/note](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#edit-generic-log-note-api-admin-logs--log-id--note-post) [GET/api/admin/logos](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-logos-list-api-admin-logos-get) [POST/api/admin/logos/select](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#select-logo-api-admin-logos-select-post) [GET/api/admin/stat](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-stat-api-admin-stat-get) [GET/api/admin/stat/daily](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-daily-stat-api-admin-stat-daily-get) [GET/api/admin/jobs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-jobs-api-admin-jobs-get) [GET/api/admin/jobs/config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-jobs-config-api-admin-jobs-config-get) [GET/api/admin/jobs/memory/peaks](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-jobs-memory-peaks-api-admin-jobs-memory-peaks-get) [GET/api/admin/jobs/memory](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-job-memory-details-api-admin-jobs-memory-get) [POST/api/admin/jobs/{job_name}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#edit-job-config-api-admin-jobs--job-name--post) [GET/api/admin/jobs/{job_name}/log](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-job-log-api-admin-jobs--job-name--log-get) [POST/api/admin/jobs/stop/all](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#stop-all-jobs-api-admin-jobs-stop-all-post) [POST/api/admin/jobs/enable/all](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#enable-all-jobs-api-admin-jobs-enable-all-post) [GET/api/admin/stat/scan/health](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-scan-jobs-health-api-admin-stat-scan-health-get) [GET/api/admin/stat/scan/states](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-scans-states-api-admin-stat-scan-states-get) [GET/api/users/stat/daily](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-user-daily-stat-api-users-stat-daily-get) [GET/api/admin/emails](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-emails-history-api-admin-emails-get) [POST/api/admin/emails](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#add-email-queue-item-api-admin-emails-post) [GET/api/admin/emails/templates](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-emails-templates-api-admin-emails-templates-get) [GET/api/admin/scan-sources/files](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-files-api-admin-scan-sources-files-get) [GET/api/admin/scan-sources/config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-scan-sources-configs-api-admin-scan-sources-config-get) [POST/api/admin/scan-sources/config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#edit-scan-source-config-api-admin-scan-sources-config-post) [DELETE/api/admin/scan-sources/config](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#remove-scan-sources-config-api-admin-scan-sources-config-delete) [GET/api/admin/scan-sources/{config_id}/check-connection](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#check-scan-source-connection-api-admin-scan-sources--config-id--) [GET/api/admin/scan-sources/subjobs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-scan-sources-jobs-state-api-admin-scan-sources-subjobs-get) [GET/api/admin/scan-sources/subjobs/{job_id}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-full-scan-source-subjob-state-api-admin-scan-sources-subjobs)
### Get Report

Get reports in raw format

Auth apiKeyQuery String

| scan_init_id | string |  |  |
| --- | --- | --- | --- |
| report_id | string |  |  |

GET /api/debug/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| RawReportResponse | object | Model for report raw format |  |
| --- | --- | --- | --- |
| scan_init | object |  |  |
| reports | array[object] |  |  |

400

Bad request

404

Item not found

422

Validation Error

 Response
### Save News Item

Save news item data

Auth apiKeyRequest Body application/json

| AdminNewsPayload | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| link | string |  |  |
| date | string |  |  |
| text | string |  |  |
| images | string |  |  |
| order | integer |  |  |
| active | boolean |  |  |

POST /api/system/newscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Remove News Item

Remove news item

Auth apiKeyQuery String

| news_id |  |  |  |
| --- | --- | --- | --- |

DELETE /api/system/newscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Delete ReportDeprecated

Delete a report

Users can only delete their own reports

Auth apiKeyPath Params

| report_id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/admin/reports/{report_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

403

Forbidden

404

Item not found

422

Validation Error

 Response
### Get Access Groups

Get a list of all access groups

Auth apiKeyGET /api/admin/access-groupscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminGroupResponse | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string | maxLength: 100 |  |
| description | string | maxLength: 300 |  |
| default | boolean | If group is provided by app by default |  |

401

Not authorized

 Response
### Save Access Group

Add or edit group.

**Note**: ID is a required parameter to modify a group

Auth apiKeyRequest Body application/json

| SaveAccessGroupRequest | object | Request model to save access groups |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |

POST /api/admin/access-groupscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Remove Access Group

Remove group

Auth apiKeyPath Params

| group_id | string |  |  |
| --- | --- | --- | --- |

POST /api/admin/access-groups/{group_id}/removecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Get Api Quota

Get all api quota settings

Auth apiKeyGET /api/admin/settings/api-quotacURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ApiQuotaSetting | array[object] |  |  |
| --- | --- | --- | --- |
| route_id | string |  |  |
| groups | array[string] | User groups to apply quota settings to |  |
| time_settings6 fields | object |  |  |
| seconds | object |  |  |
| seconds_amount | integer | Seconds period to count requests |  |
| requests | integer | Requests amount per seconds period |  |
| minute | integer | Max requests amount per minute |  |
| hour | integer | Max requests amount per hour |  |
| day | integer | Max requests amount per day |  |
| week | integer | Max requests amount per week |  |
| month | integer | Max requests amount per month |  |
| credits_settings | object |  |  |
| request_cost | integer | Credits cost for single request |  |
| total_credits | integer | Total credits available per month |  |
| id | string |  |  |

401

Not authorized

 Response
### Save Api Quota

Save single API quota setting

Auth apiKeyRequest Body application/json

| SaveApiQuotaSettingRequest | object | Request model to save api quota setting |  |
| --- | --- | --- | --- |
| route_id | string |  |  |
| groups | array[string] |  |  |
| time_settings6 fields | object |  |  |
| seconds | object |  |  |
| seconds_amount | integer | Seconds period to count requests |  |
| requests | integer | Requests amount per seconds period |  |
| minute | integer | Max requests amount per minute |  |
| hour | integer | Max requests amount per hour |  |
| day | integer | Max requests amount per day |  |
| week | integer | Max requests amount per week |  |
| month | integer | Max requests amount per month |  |
| credits_settings | object |  |  |
| request_cost | integer | Credits cost for single request |  |
| total_credits | integer | Total credits available per month |  |

POST /api/admin/settings/api-quotacURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Remove Api Quota

Remove single api quota setting

Auth apiKeyPath Params

| quota_id | string |  |  |
| --- | --- | --- | --- |

POST /api/admin/settings/api-quota/{quota_id}/removecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Get Settings Group

Get a group of admin settings

Auth apiKeyPath Params

| group | string | Enum: `access`,`auth`,`environment` |  |
| --- | --- | --- | --- |

GET /api/admin/settings/{group}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminSettingOutput | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| group | string | An enumeration.  Enum: `access`,`auth`,`environment` |  |
| subgroup | string |  |  |
| value Choice 1Choice 2Choice 3Choice 4 |  |  |  |
| integer | integer |  |  |

401

Not authorized

422

Validation Error

 Response Access exampleAuth exampleEnvironment exampleOauth_services example
### Save Settings Group

Update group of admin settings

Auth apiKeyPath Params

| group | string | Enum: `access`,`auth`,`environment` |  |
| --- | --- | --- | --- |

Request Body application/json

| Data | object |  |  |
| --- | --- | --- | --- |
| * | object |  |  |

POST /api/admin/settings/{group}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Auth Services

Get all external auth services settings

Auth apiKeyGET /api/admin/auth-servicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Save Auth Service

Update settings of external auth service

Auth apiKeyRequest Body SaveOAuthServicePayloadSaveSamlServicePayloadapplication/json

| SaveOAuthServicePayload | object | Request model to save OAuth service |  |
| --- | --- | --- | --- |
| active | boolean |  |  |
| client_id | string |  |  |
| discovery_base_url | string |  |  |
| discovery_path | string |  |  |
| home_page | string |  |  |
| key | string |  |  |
| name | string |  |  |
| order | string |  |  |
| secret | string |  |  |
| auth_type | string | An enumeration.  Enum: `oauth`,`saml` |  |
| use_state | boolean |  |  |
| api_base_url | string |  |  |
| api_type | string | Supported APIs for OAuth providers  Enum: `microsoft_graph` |  |
| should_map_groups | boolean |  |  |
| groups_map | array[object] |  |  |
| local_group_id | string |  |  |
| external_groups | array[string] |  |  |

POST /api/admin/auth-servicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Remove Auth Service

Remove external auth service settings

Auth apiKeyPath Params

| service | string |  |  |
| --- | --- | --- | --- |

POST /api/admin/auth-services/{service}/removecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

422

Validation Error

 Response
### Get Users

Get list of users.

Use `filter` parameter to find users by email or username. It will match in any part of a word.
If `ids` parameter is specified, `filter` is ignored.

Auth apiKeyQuery String

| page |  | Default: 1 |  |
| --- | --- | --- | --- |
| ids | array |  |  |
| filter | string |  |  |
| group | string |  |  |

GET /api/admin/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminUsersResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| items11 fields | array[object] |  |  |
| id | string |  |  |
| account_id | string | Permanent id to use, say, in urls |  |
| email | string |  |  |
| username | string | User nickname in system |  |
| groups | array[string] | Groups user is a member of |  |
| confirmed | boolean | Default: false |  |
| active | boolean | Default: false |  |
| created_date | date-time |  |  |
| last_login_date | date-time |  |  |
| count_uploads | integer | Amount of user uploads  Default: 0 |  |
| is_service_account | boolean | The account is used for automated services  Default: false |  |
| total_count | integer |  |  |
| matched_count | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Users Overview

Download basic users info as csv file

Auth apiKeyGET /api/admin/users/importcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json text/plain 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get User

Get user by user id

Auth apiKeyPath Params

| user_id | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/users/{user_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminUserResponse | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| account_id | string | Permanent id to use, say, in urls |  |
| email | string |  |  |
| username | string | User nickname in system |  |
| groups | array[string] | Groups user is a member of |  |
| confirmed | boolean | Default: false |  |
| active | boolean | Default: false |  |
| created_date | date-time |  |  |
| last_login_date | date-time |  |  |
| count_uploads | integer | Amount of user uploads  Default: 0 |  |
| is_service_account | boolean | The account is used for automated services  Default: false |  |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Edit User

Edit user

Auth apiKeyPath Params

| user_id | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| EditUserRequest | object | Request model to edit user |  |
| --- | --- | --- | --- |
| active | boolean |  |  |
| confirmed | boolean |  |  |
| groups | array[string] |  |  |
| is_service_account | boolean |  |  |

POST /api/admin/users/{user_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Delete User

Delete a user

Auth apiKeyPath Params

| user_id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/admin/users/{user_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Get User Uploads

Get user's uploads

Auth apiKeyPath Params

| user_id | string |  |  |
| --- | --- | --- | --- |

Query String

| page | integer | minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| page_size |  | Default: 10 |  |

GET /api/admin/users/{user_id}/uploadscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| UserUploadsResponse | object |  |  |
| --- | --- | --- | --- |
| items | array[object] |  |  |
| count | integer |  |  |
| timing | array[object] |  |  |
| method | string | An enumeration.  Enum: `or`,`and` |  |
| count_search_params | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Get User Reset Password Link

Generate user's reset-password link

Auth apiKeyPath Params

| user_id | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/users/{user_id}/reset-passwordcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| UserResetPasswordResponse | object |  |  |
| --- | --- | --- | --- |
| token | string |  |  |

401

Not authorized

422

Validation Error

 Response
### Get App Config

Get app basic config values

Auth apiKeyGET /api/admin/app-configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get App Config Api Admin App Config Get | object |  |  |
| --- | --- | --- | --- |

401

Not authorized

 Response
### Get Services Stat

Get statistics of various running services

Auth apiKeyGET /api/admin/stat/servicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ServicesStatResponse | object |  |  |
| --- | --- | --- | --- |
| queues | object | Service Stat Response nested model |  |
| scan | object |  |  |
| redis | object | Service Stat Response nested model |  |
| info | object |  |  |

401

Not authorized

 Response
### Generate Invite Token

Generate invitation token for user

Auth apiKeyRequest Body application/json

| AdminGenerateInviteLinkResponse | object |  |  |
| --- | --- | --- | --- |
| groups | array[string] |  |  |

POST /api/admin/invitecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| GenerateInviteTokenResponse | object |  |  |
| --- | --- | --- | --- |
| token | string |  |  |

401

Not authorized

422

Validation Error

 Response
### Generate External Tokens Secret

Generate secret key to encript external auth tokens

Auth apiKeyGET /api/admin/generate-external-tokens-secretcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json text/plain 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get App Errors

Obtain saved errors

Params:

- type - can be 'server' or 'client'
- page - (default: 1)
- filter - match the given string to error message
- sort - can be 'date', 'count' or 'note'
Auth apiKeyQuery String

| type |  | Default: client |  |
| --- | --- | --- | --- |
| page | integer | minimum: 1  Default: 1 |  |
| filter | string |  |  |
| sort | string | Enum: `date`,`count`,`note` |  |

GET /api/admin/errorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminAppErrorsResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| items15 fields | array[object] |  |  |
| id | string |  |  |
| type | string | Type of application error that we can save  Enum: `server`,`client` |  |
| message | string |  |  |
| url | string |  |  |
| context | string | Short description of error context  Enum: `Scanning job`,`HTML/PDF report job`,`Scheduled job`,`Signin using external auth provider` |  |
| trace | string |  |  |
| first_occurance_date | date-time |  |  |
| last_occurance_date | date-time |  |  |
| occurance_count | integer | How often error was noticed  Default: 1 |  |
| is_signed_in | boolean | If user was signed in during error |  |
| report_flow_id | string |  |  |
| report_flow_file_sha256 | string |  |  |
| report_id | string |  |  |
| report_file_sha256 | string |  |  |
| note | string |  |  |
| total_count | integer |  |  |
| matched_count | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Remove App Errors

Remove saved errors matching filter

Params:

- type - can be 'server' or 'client'
- filter - match the given string to error message
Auth apiKeyQuery String

| type |  | Default: client |  |
| --- | --- | --- | --- |
| filter | string |  |  |

DELETE /api/admin/errorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminAppErrorsRemovedResponse | object |  |  |
| --- | --- | --- | --- |
| removed_count | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### App Error

Remove single saved error

Auth apiKeyPath Params

| error_id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/admin/errors/{error_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Edit App Error Note

Edit saved error note, to help memorize it's specifics

Auth apiKeyPath Params

| error_id | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| AdminAppErrorNotePayload | object |  |  |
| --- | --- | --- | --- |
| note | string |  |  |

POST /api/admin/errors/{error_id}/notecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Export Errors

Export application errors in a .csv format

Auth apiKeyGET /api/admin/errors/exportcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json text/plain 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Generic Logs

Obtain custom logs, usually aimed to trace problems

Params:

- page - (default: 1)
- filter - match the given string to the 'key' and the beginning of the 'related_url' and 'note' fields
- sort - can be 'date' or 'note'
Auth apiKeyQuery String

| page | integer | minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| filter | string |  |  |
| sort | string | Enum: `date`,`note` |  |

GET /api/admin/logscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminGenericLogsResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| items7 fields | array[object] |  |  |
| id | string |  |  |
| key | string |  |  |
| key_type | string | Type of key attribute for logging record  Enum: `scan_init_id`,`new_search` |  |
| note | string | Note describing log specifics |  |
| related_url | string | Related site page, if it exists |  |
| saved_date | date-time | Date when logging record was created |  |
| total_count | integer |  |  |
| matched_count | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Remove Generic Logs

Remove custom logs matching filter

Params:

- filter - match the given string to the 'key' and the beginning of the 'related_url' and 'note' fields
Auth apiKeyQuery String

| filter | string |  |  |
| --- | --- | --- | --- |

DELETE /api/admin/logscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminGenericLogsRemovedResponse | object |  |  |
| --- | --- | --- | --- |
| removed_count | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Calculate Retention

Calculate affected number of reports by retention config changes

Auth apiKeyQuery String

| retention_period_malicious | integer |  |  |
| --- | --- | --- | --- |
| retention_period_suspicious | integer |  |  |
| retention_period_informational | integer |  |  |
| retention_period_unknown | integer |  |  |
| retention_period_benign | integer |  |  |

GET /api/admin/retention-calculationcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminRetentionCalculationResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| total_number_of_reports | integer |  |  |
| affected_number_of_reports | object |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Full Generic Log

Obtain full log record data

Auth apiKeyPath Params

| log_id | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/logs/{log_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminGenericLogResponse | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| key | string |  |  |
| key_type | string | Type of key attribute for logging record  Enum: `scan_init_id`,`new_search` |  |
| note | string | Note describing log specifics |  |
| related_url | string | Related site page, if it exists |  |
| saved_date | date-time | Date when logging record was created |  |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Remove Generic Log

Remove single log record

Auth apiKeyPath Params

| log_id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/admin/logs/{log_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Edit Generic Log Note

Edit log note, to help memorize it's specifics

Auth apiKeyPath Params

| log_id | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| AdminGenericLogNotePayload | object |  |  |
| --- | --- | --- | --- |
| note | string |  |  |

POST /api/admin/logs/{log_id}/notecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Logos List

Get list of all available logos

Auth apiKeyGET /api/admin/logoscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| array | array[string] |  |  |
| --- | --- | --- | --- |

401

Not authorized

 Response
### Select Logo

Select new logo

Auth apiKeyRequest Body application/x-www-form-urlencoded

| Body_select_logo_api_admin_logos_select_post | object |  |  |
| --- | --- | --- | --- |
| file | file |  |  |
| name | string |  |  |
| type | string | Type of logo, representing it's usecase  Enum: `main`,`top_menu`,`footer` |  |
| theme | string | All available themes  Enum: `light`,`dark` |  |

POST /api/admin/logos/selectcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

422

Validation Error

 Response
### Get Stat

Get app statistics

Auth apiKeyQuery String

| types | array | Enum: `count_reports`,`count_verdicts`,`count_iocs`,`count_yaras`,`count_users`,`count_active_users`,`count_users_uploads`,`count_reports_by_extension`,`count_malicious_reports_by_extension`,`count_malicious_reports_by_language`,`count_malicious_reports_by_country`,`count_malicious_ips`,`count_malicious_ips_ratio`,`frequent_tags`,`frequent_yara_tags`,`most_interesting`,`system_info`,`count_mitre_techniques`,`frequent_malware_tags` |  |
| --- | --- | --- | --- |

GET /api/admin/statcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AppStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| value Choice 1Choice 2Choice 3Choice 4Choice 5 |  |  |  |
| boolean | boolean |  |  |
| updated_date | date-time |  |  |

400

Bad request

401

Not authorized

403

Forbidden

422

Validation Error

 Response
### Get Daily Stat

Get app statistics, which is saved separately in daily stat collection

Auth apiKeyQuery String

| types | array | Enum: `count_verdicts_by_date`,`count_reports_by_date`,`count_uploads_by_date`,`count_initial_scan_jobs_by_date`,`count_rescan_jobs_by_date`,`count_reports_states_by_date`,`count_reports_extensions_by_date`,`count_users_signup_by_day`,`count_users_signin_by_day` |  |
| --- | --- | --- | --- |
| date_from | string |  |  |
| date_to | string |  |  |

GET /api/admin/stat/dailycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DateStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| date | string |  |  |
| name | string |  |  |
| value Choice 1Choice 2Choice 3Choice 4Choice 5 |  |  |  |
| boolean | boolean |  |  |
| updated_date | date-time |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Jobs

Get all available jobs with some additional information

Auth apiKeyQuery String

| category | string | Enum: `statistics`,`scan`,`system`,`reports`,`patches` |  |
| --- | --- | --- | --- |

GET /api/admin/jobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScheduleTaskResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| category | string | Job categories  Enum: `statistics`,`scan`,`system`,`reports`,`patches` |  |
| description | string |  |  |
| config6 fields | object | Return job config to user |  |
| name | string |  |  |
| trigger | string | All available trigger types  Enum: `once`,`date`,`interval`,`cron`,`calendarinterval` |  |
| trigger_config | object |  |  |
| runtime_config | object |  |  |
| is_active | boolean |  |  |
| is_editable | boolean |  |  |
| state6 fields | object | Return job state to user |  |
| name | string |  |  |
| state | string |  |  |
| data | object |  |  |
| updated_date | date-time |  |  |
| public_log | array |  |  |
| has_public_log | boolean |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Jobs Config

Get jobs launch and runtime config

Auth apiKeyQuery String

| jobs | array |  |  |
| --- | --- | --- | --- |

GET /api/admin/jobs/configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScheduleTaskConfig | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| trigger | string | All available trigger types  Enum: `once`,`date`,`interval`,`cron`,`calendarinterval` |  |
| trigger_config | object |  |  |
| runtime_config | object |  |  |
| is_subprocess | boolean | Field to differ real scheduled jobs from custom ones  Default: false |  |
| is_active | boolean | If job is available for running  Default: true |  |
| is_editable | boolean | If user is allowed to edit this settings  Default: true |  |
| updated_date | date-time | Last time when schedual was updated by user |  |
| update_applied_date | date-time | Last date when updated schedual was applied to job |  |
| id | string |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Jobs Memory Peaks

Get peak jobs memory usage

Auth apiKeyGET /api/admin/jobs/memory/peakscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScheduleTaskPeakMemoryResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| description | string |  |  |
| memory | number |  |  |
| is_killed | boolean |  |  |
| is_unresponsive | boolean |  |  |

401

Not authorized

 Response
### Get Job Memory Details

Get job memory usage details

Auth apiKeyQuery String

| job_name | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/jobs/memorycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScheduleTaskMemoryResponse | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| resident_memory | number |  |  |
| date | date-time |  |  |
| is_killed | boolean |  |  |

401

Not authorized

422

Validation Error

 Response
### Edit Job Config

Edit job config

Auth apiKeyPath Params

| job_name | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| ScheduleTaskConfigEdit | object | Job edit input model |  |
| --- | --- | --- | --- |
| trigger | string | All available trigger types  Enum: `once`,`date`,`interval`,`cron`,`calendarinterval` |  |
| trigger_config | object |  |  |
| runtime_config | object |  |  |
| is_active | boolean |  |  |

POST /api/admin/jobs/{job_name}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

403

Forbidden

404

Item not found

422

Validation Error

 Response
### Get Job Log

Get job public log

Auth apiKeyPath Params

| job_name | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/jobs/{job_name}/logcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScheduleTaskLogResponse | object | Job log response |  |
| --- | --- | --- | --- |
| state | string | Name of job state  Enum: `succeeded`,`succeeded_with_errors`,`failed`,`running` |  |
| log | array |  |  |

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Stop All Jobs

Stop all existing jobs

Auth apiKeyPOST /api/admin/jobs/stop/allcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Enable All Jobs

Enable all existing jobs

Auth apiKeyPOST /api/admin/jobs/enable/allcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Get Scan Jobs Health

Get health statistics about scan jobs queues

Auth apiKeyQuery String

| queue_name | string |  |  |
| --- | --- | --- | --- |
| check_type | string | Enum: `long_run`,`new_run` |  |
| date_from | string |  |  |

GET /api/admin/stat/scan/healthcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScanHealthResponse | array[object] |  |  |
| --- | --- | --- | --- |
| date | date-time |  |  |
| value | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Scans States

Get statistics on scans progress

Auth apiKeyQuery String

| queue_name | string |  |  |
| --- | --- | --- | --- |
| state | array | Enum: `created`,`queued`,`scanning`,`queued_cancelled`,`changed_priority`,`failed`,`running_timedout` |  |
| date_from | string |  |  |

GET /api/admin/stat/scan/statescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ScanStateStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| count_created | integer |  |  |
| count_queued | integer |  |  |
| count_scanning | integer |  |  |
| count_failed | integer |  |  |
| count_queued_cancelled | integer |  |  |
| count_changed_priority | integer |  |  |
| count_running_timedout | integer |  |  |
| date | date-time |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get User Daily Stat

Get app statistics, which is saved separately in daily stat collection, available for ordinary users

Auth apiKeyQuery String

| types | array | Enum: `count_verdicts_by_date`,`count_reports_by_date`,`count_uploads_by_date` |  |
| --- | --- | --- | --- |
| date_from | string |  |  |
| date_to | string |  |  |

GET /api/users/stat/dailycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| DateStatResponse | array[object] |  |  |
| --- | --- | --- | --- |
| date | string |  |  |
| name | string |  |  |
| value Choice 1Choice 2Choice 3Choice 4Choice 5 |  |  |  |
| boolean | boolean |  |  |
| updated_date | date-time |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get Emails History

Get history of sending mass emails

Auth apiKeyQuery String

| page | integer | minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |

GET /api/admin/emailscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| EmailHistoryResponse | object |  |  |
| --- | --- | --- | --- |
| items10 fields | array[object] |  |  |
| id | string |  |  |
| recipient_type | string | Recipient types of mass email sending  Enum: `all_users`,`admins`,`selected_users` |  |
| recipient_emails | array[string] |  |  |
| subject | string |  |  |
| content | string |  |  |
| state | string | State of email queue item processing  Enum: `created`,`queued`,`sending`,`succeeded`,`failed` |  |
| created_date | date-time |  |  |
| completed_date | date-time |  |  |
| count_emails_sent | integer |  |  |
| error | object |  |  |
| total_count | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Add Email Queue Item

Add record to emails queue

Auth apiKeyRequest Body application/json

| EmailQueueRequest | object | Email queue input model |  |
| --- | --- | --- | --- |
| recipient_type | string | Recipient types of mass email sending  Enum: `all_users`,`admins`,`selected_users` |  |
| recipient_emails | array[string] |  |  |
| subject | string |  |  |
| content | string |  |  |

POST /api/admin/emailscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

422

Validation Error

 Response
### Get Emails Templates

Get predefined email templates

Auth apiKeyGET /api/admin/emails/templatescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| EmailTemplatesResponse | object |  |  |
| --- | --- | --- | --- |
| terms_change Choice 1Choice 2 |  |  |  |
| string | string |  |  |

401

Not authorized

 Response
### Get Files

Get list of files obtained from scan sources

Auth apiKeyQuery String

| page | integer | minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| config | string |  |  |
| state | string | Enum: `queued_for_download`,`downloading`,`queued_for_scan`,`scanning`,`scan_completed` |  |
| verdict | string | Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

GET /api/admin/scan-sources/filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminScanSourcesFilesResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| items10 fields | array[object] |  |  |
| config4 fields | object |  |  |
| id | string |  |  |
| provider | string |  |  |
| name | string |  |  |
| source_type | string | An enumeration.  Enum: `email:IMAP`,`s3` |  |
| file3 fields | object |  |  |
| name | string |  |  |
| hash | string |  |  |
| mime_type | string |  |  |
| state | string | All possible states of processing of file from remote scan source  Enum: `queued_for_download`,`downloading`,`queued_for_scan`,`scanning`,`scan_completed` |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| folder | string | Unique path to file on source |  |
| id_on_source | integer | Unique id of file in its folder on source |  |
| flow_id | string | Id of scan flow record |  |
| created_date | date-time | Time of file record creation |  |
| created_date_on_source | date-time | Date of file creation on source |  |
| downloaded_date | date-time |  |  |
| total_count | integer |  |  |
| matched_count | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Scan Sources Configs

Obtain scan sources config records

Auth apiKeyQuery String

| page | integer | minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |

GET /api/admin/scan-sources/configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminScanSourcesConfigsResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| items16 fields | array[object] |  |  |
| id | string |  |  |
| provider | string |  |  |
| name | string |  |  |
| source_type | string | An enumeration.  Enum: `email:IMAP`,`s3` |  |
| host | string |  |  |
| port | string |  |  |
| connection_security | string | An enumeration.  Enum: `ssl_tls`,`start_tls` |  |
| folders | array[string] |  |  |
| remove_files_on_source | boolean | If we should remove files on source after scanning  Default: false |  |
| credentials AdminLoginPasswordCredentialsResponseS3Credentials.__pydantic_model__ |  | Can have various fields depending on scan source |  |
| AdminLoginPasswordCredentialsResponse | object |  |  |
| login | string |  |  |
| is_active | boolean | If config is activated for usage |  |
| source_type_specific3 fields | object | Options specific to email sources |  |
| mark_as_seen | boolean | If we should mark downloaded emails as seen on email service  Default: false |  |
| append_scanned_flag | boolean | If we should add flag with scan result to email on service  Default: false |  |
| first_fetch_mode | string | What emails to fetch on first time accessing account  Enum: `all`,`recent`,`unseen` |  |
| files_are_private | boolean | If all downloaded files should be scanned as private |  |
| description | string | Description field that should be added to all downloaded files |  |
| propagate_tags | boolean | If tags should be extracted from description and added to reports |  |
| schedule6 fields | object | Return job config to user |  |
| name | string |  |  |
| trigger | string | All available trigger types  Enum: `once`,`date`,`interval`,`cron`,`calendarinterval` |  |
| trigger_config | object |  |  |
| runtime_config | object |  |  |
| is_active | boolean |  |  |
| is_editable | boolean |  |  |
| total_count | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Edit Scan Source Config

Add or edit scan source config record

Auth apiKeyRequest Body application/json

| EmailSourceConfigRequest | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| provider | string |  |  |
| name | string |  |  |
| source_type | string | An enumeration.  Enum: `email:IMAP`,`s3` |  |
| host | string |  |  |
| port | string |  |  |
| connection_security | string | An enumeration.  Enum: `ssl_tls`,`start_tls` |  |
| folders | array[string] |  |  |
| remove_files_on_source | boolean |  |  |
| credentials LoginPasswordCredentials.__pydantic_model__S3Credentials.__pydantic_model__ |  |  |  |
| LoginPasswordCredentials | object | Standard credentials with login/password |  |
| login | string |  |  |
| password | string |  |  |
| is_active | boolean |  |  |
| source_type_specific3 fields | object | Options specific to email sources |  |
| mark_as_seen | boolean | If we should mark downloaded emails as seen on email service  Default: false |  |
| append_scanned_flag | boolean | If we should add flag with scan result to email on service  Default: false |  |
| first_fetch_mode | string | What emails to fetch on first time accessing account  Enum: `all`,`recent`,`unseen` |  |
| files_are_private | boolean |  |  |
| description | string |  |  |
| propagate_tags | boolean |  |  |
| schedule4 fields | object |  |  |
| trigger | string | Available tirgger types when adding scan source from clientside  Enum: `once`,`interval`,`cron` |  |
| trigger_config3 fields | object |  |  |
| time | string |  |  |
| unit | string | An enumeration.  Enum: `minutes`,`hours`,`days`,`each_day`,`week_day` |  |
| value Choice 1Choice 2 |  |  |  |
| integer | integer |  |  |
| runtime_config | object |  |  |
| run_once | boolean |  |  |
| is_active | boolean |  |  |

POST /api/admin/scan-sources/configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Remove Scan Sources Config

Remove scan sources configs records by id

Note: This will also remove scan source files from the database.
The quick overview and verdicts of these files won't be available in the Admin Panel anymore.
The scan results will only remain accessible from standard reports search.

Auth apiKeyRequest Body application/json

| ScanSourcesConfigIds | object |  |  |
| --- | --- | --- | --- |
| config_ids Choice 1Choice 2 |  |  |  |
| string | string |  |  |

DELETE /api/admin/scan-sources/configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminScanSourcesRemoveResponse | object |  |  |
| --- | --- | --- | --- |
| remove_count | integer |  |  |

422

Validation Error

 Response
### Check Scan Source Connection

Verify if scan source credentials are working ok

Auth apiKeyPath Params

| config_id | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/scan-sources/{config_id}/check-connectioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| array | array[string] |  |  |
| --- | --- | --- | --- |

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Get Scan Sources Jobs State

Get state of scan sources handlers

Auth apiKeyQuery String

| page | integer | minimum: 1  Default: 1 |  |
| --- | --- | --- | --- |
| config | string |  |  |

GET /api/admin/scan-sources/subjobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminScanSourcesSubjobsResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| items3 fields | array[object] |  |  |
| scan_source_config4 fields | object |  |  |
| id | string |  |  |
| provider | string |  |  |
| name | string |  |  |
| source_type | string | An enumeration.  Enum: `email:IMAP`,`s3` |  |
| config6 fields | object | Return job config to user |  |
| name | string |  |  |
| trigger | string | All available trigger types  Enum: `once`,`date`,`interval`,`cron`,`calendarinterval` |  |
| trigger_config | object |  |  |
| runtime_config | object |  |  |
| is_active | boolean |  |  |
| is_editable | boolean |  |  |
| state6 fields | object | Return job state to user |  |
| name | string |  |  |
| state | string |  |  |
| data | object |  |  |
| updated_date | date-time |  |  |
| public_log | array |  |  |
| has_public_log | boolean |  |  |
| total_count | integer |  |  |
| matched_count | integer |  |  |

401

Not authorized

422

Validation Error

 Response
### Get Full Scan Source Subjob State

Obtain full scan source job record data

Auth apiKeyPath Params

| job_id | string |  |  |
| --- | --- | --- | --- |

GET /api/admin/scan-sources/subjobs/{job_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AdminScanSourceSubjobResponse | object | Customize admin response models |  |
| --- | --- | --- | --- |
| scan_source_config4 fields | object |  |  |
| id | string |  |  |
| provider | string |  |  |
| name | string |  |  |
| source_type | string | An enumeration.  Enum: `email:IMAP`,`s3` |  |
| config6 fields | object | Return job config to user |  |
| name | string |  |  |
| trigger | string | All available trigger types  Enum: `once`,`date`,`interval`,`cron`,`calendarinterval` |  |
| trigger_config | object |  |  |
| runtime_config | object |  |  |
| is_active | boolean |  |  |
| is_editable | boolean |  |  |
| state6 fields | object | Return job state to user |  |
| name | string |  |  |
| state | string |  |  |
| data | object |  |  |
| updated_date | date-time |  |  |
| public_log | array |  |  |
| has_public_log | boolean |  |  |

400

Bad request

401

Not authorized

404

Item not found

422

Validation Error

 Response
## Audit-logger

Audit Logger

Endpoints[GET/api/admin/audit-logs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-audit-logs-api-admin-audit-logs-get)
### Get Audit Logs

Obtain saved audit logs

Auth apiKeyQuery String

| logger_type | string | Enum: `admin`,`auth` |  |
| --- | --- | --- | --- |
| log_level_filter |  | Default: all |  |
| page | integer | minimum: 1  Default: 1 |  |
| filter | string |  |  |

GET /api/admin/audit-logscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AuditLogsResponse | object | Response model for getting audit logs |  |
| --- | --- | --- | --- |
| items | array[object] |  |  |
| total_count | integer |  |  |
| matched_count | integer |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
## Threatintel

Threat Intelligence

Endpoints[POST/api/threatintel/get-prevalence](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-ioc-prevalences-api-threatintel-get-prevalence-post) [POST/api/threatintel/modify-verdict](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#modify-verdict-api-threatintel-modify-verdict-post) [GET/api/threatintel/get-similars](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-similar-reports-api-threatintel-get-similars-get) [GET/api/threatintel/feed](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-advanced-feed-api-threatintel-feed-get) [GET/api/threatintel/download-iocs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#download-iocs-api-threatintel-download-iocs-get)
### Get prevalence of IOCs

Get prevalences of IOCs

Auth apiKeyQuery String

| exclude_report_ids | array |  |  |
| --- | --- | --- | --- |

Request Body application/json

| IOCsPrevalenceSearchParams | object | Params for IOCs' prevalence search |  |
| --- | --- | --- | --- |
| domain | array[string] | Default: [] |  |
| ip | array[string] | Default: [] |  |
| url | array[string] | Default: [] |  |
| uuid | array[string] | Default: [] |  |
| email | array[string] | Default: [] |  |
| registry_path | array[string] | Default: [] |  |
| revision_save_id | array[string] | Default: [] |  |
| sha1 | array[string] | Default: [] |  |
| sha256 | array[string] | Default: [] |  |
| sha512 | array[string] | Default: [] |  |
| md5 | array[string] | Default: [] |  |
| imphash | array[string] | Default: [] |  |
| ssdeep | array[string] | Default: [] |  |
| authentihash | array[string] | Default: [] |  |
| fuzzyfsiohash | array[string] | Default: [] |  |
| unc_path | array[string] | Default: [] |  |
| days | integer | Default: -1 |  |

Expand POST /api/threatintel/get-prevalencecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Ioc Prevalences Api Threatintel Get Prevalence Post | object |  |  |
| --- | --- | --- | --- |
| * | object |  |  |
| *3 fields | object | Prevalence response model |  |
| counts | object |  |  |
| * | integer |  |  |
| reports5 fields | array[object] |  |  |
| flow_id | string |  |  |
| report_id | string |  |  |
| file | object | File name and hash |  |
| name | string |  |  |
| sha256 | string |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| created_date | date-time |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Modify verdict for a given report

Modify verdict for a given report

Auth apiKeyRequest Body application/json

| ModifyVerdictPayload | object | New verdict and report id |  |
| --- | --- | --- | --- |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| report_id | string |  |  |

POST /api/threatintel/modify-verdictcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

404

Item not found

422

Validation Error

 Response
### Get reports with the same special hashes (fuzzyfsio, imphash, ssdeep, authentihash)

Get reports with the same special hashes

Auth apiKeyQuery String

| exclude_report_ids | array |  |  |
| --- | --- | --- | --- |
| imphash | string |  |  |
| ssdeep | string |  |  |
| fuzzyfsiohash | string |  |  |
| authentihash | string |  |  |
| days | integer | Default: -1 |  |

GET /api/threatintel/get-similarscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Similar Reports Api Threatintel Get Similars Get | object |  |  |
| --- | --- | --- | --- |
| * | object |  |  |
| *3 fields | object | Prevalence response model |  |
| counts | object |  |  |
| * | integer |  |  |
| reports5 fields | array[object] |  |  |
| flow_id | string |  |  |
| report_id | string |  |  |
| file | object | File name and hash |  |
| name | string |  |  |
| sha256 | string |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| created_date | date-time |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Get feeds with more data

Get advanced feed containing all IOCs and signatures compared to the basic feed

Auth apiKeyGET /api/threatintel/feedcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json text/plain 200

Successful Response

| No response body |
| --- |

401

Not authorized

 Response
### Download iocs of reports in csv format

Download iocs of all reports

Auth apiKeyHeaders

| page | integer | minimum: 0  Default: 0 |  |
| --- | --- | --- | --- |
| pageSize | integer | minimum: 0  Default: 0 |  |

Query String

| unique_files | boolean | Default: false |  |
| --- | --- | --- | --- |
| method |  | Default: and |  |
| derived_files | boolean | Default: true |  |
| no_date_limit | boolean | Default: false |  |
| query | string |  |  |
| verdict | string |  |  |
| source_type | string | Enum: `url`,`url-to-file`,`file` |  |
| filetype | string | Enum: `ace`,`apk`,`bat`,`64bits`,`bmp`,`csv`,`doc`,`docm`,`docx`,`dot`,`dotm`,`dotx`,`elf`,`eml`,`gif`,`hta`,`htm`,`html`,`iso`,`java`,`java-bytecode`,`javascript`,`jpg`,`lnk`,`mbox`,`mhtml`,`msg`,`msi`,`mso`,`odp`,`ods`,`odt`,`odg`,`odf`,`odc`,`odb`,`odi`,`ole`,`one`,`pdf`,`pedll`,`peexe`,`png`,`pot`,`potm`,`potx`,`powershell`,`ppt`,`pptm`,`pptx`,`ps`,`pub`,`rar`,`rfc822`,`rtf`,`svg`,`txt`,`vbs`,`wmv`,`wsf`,`xlm`,`xls`,`xlsb`,`xlsm`,`xlsx`,`xlt`,`xltm`,`xltx`,`xml`,`xsl`,`zip`,`7zip`,`exe`,`mail`,`ms-office`,`script` |  |
| tag | string |  |  |
| tags | string |  |  |
| date_from | string |  |  |
| date_to | string |  |  |
| rate_from | integer |  |  |
| rate_to | integer |  |  |
| uuid | string |  |  |
| email | string |  |  |
| registry_path | string |  |  |
| revision_save_id | string |  |  |
| yara_rule | string |  |  |
| retry_count | integer |  |  |
| scan_init_id | string |  |  |
| report_id | string |  |  |
| country | string |  |  |
| filename | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| sha512 | string |  |  |
| md5 | string |  |  |
| domain | string |  |  |
| ip | string |  |  |
| url | string |  |  |
| media_type | string |  |  |
| imphash | string |  |  |
| ssdeep | string |  |  |
| authentihash | string |  |  |
| fuzzyfsiohash | string |  |  |
| signal_groups | string |  |  |
| mitre_techniques | string |  |  |
| verdict_groups | string |  |  |
| main_task_state |  | Default: success |  |
| exclude | string |  |  |

Expand GET /api/threatintel/download-iocscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses text/plain 200

Successful Response

| No response body |
| --- |

401

Not authorized

422

Validation Error

 Response
## Similarity-search

Similarity Search

Endpoints[GET/api/similarity-search/similarity](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#similarity-api-similarity-search-similarity-get)
### Get similar reports based on the SHA256 hash, tags, threshold and verdict

Get similar reports

Auth apiKeyQuery String

| hash | string |  |  |
| --- | --- | --- | --- |
| min_similarity | integer | maximum: 100  minimum: 0  Default: 0 |  |
| verdict | string | Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| tags | array |  |  |

GET /api/similarity-search/similaritycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| SimilaritiesResponse | object |  |  |
| --- | --- | --- | --- |
| note | string | Optinal notification about demo data |  |
| most_similar4 fields | array[object] | Default: [] |  |
| sha256 | string |  |  |
| overall_similarity | number |  |  |
| similarities32 fields | object |  |  |
| extracted | number |  |  |
| threat_indicators | number |  |  |
| sections | number |  |  |
| mitre_techniques | number |  |  |
| binary_metadata | number |  |  |
| certificates | number |  |  |
| characteristic | number |  |  |
| disassembly_sections | number |  |  |
| dotnet_info | number |  |  |
| header_info | number |  |  |
| imports | number |  |  |
| pdb_guid | number |  |  |
| resources | number |  |  |
| rich_header_compiler_ids | number |  |  |
| strings | number |  |  |
| version_info | number |  |  |
| apk | number |  |  |
| biffopcodes | number |  |  |
| emulation | number |  |  |
| extendeddata | number |  |  |
| metadata | number |  |  |
| segments | number |  |  |
| content_parse | number |  |  |
| image_ocr | number |  |  |
| binary_internal | number |  |  |
| strings_input_file | number |  |  |
| triggeredconsumerids | number |  |  |
| vba_emulation | number |  |  |
| yara | number |  |  |
| signal_ids | number |  |  |
| certifications | number |  |  |
| weighted_numerics | number |  |  |
| details7 fields | object |  |  |
| start_date | date-time |  |  |
| file_size | number |  |  |
| tags | array[string] |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| is_dotnet | integer |  |  |
| architecture | string |  |  |
| entropy | number |  |  |
| most_recent4 fields | array[object] | Default: [] |  |
| sha256 | string |  |  |
| overall_similarity | number |  |  |
| similarities32 fields | object |  |  |
| extracted | number |  |  |
| threat_indicators | number |  |  |
| sections | number |  |  |
| mitre_techniques | number |  |  |
| binary_metadata | number |  |  |
| certificates | number |  |  |
| characteristic | number |  |  |
| disassembly_sections | number |  |  |
| dotnet_info | number |  |  |
| header_info | number |  |  |
| imports | number |  |  |
| pdb_guid | number |  |  |
| resources | number |  |  |
| rich_header_compiler_ids | number |  |  |
| strings | number |  |  |
| version_info | number |  |  |
| apk | number |  |  |
| biffopcodes | number |  |  |
| emulation | number |  |  |
| extendeddata | number |  |  |
| metadata | number |  |  |
| segments | number |  |  |
| content_parse | number |  |  |
| image_ocr | number |  |  |
| binary_internal | number |  |  |
| strings_input_file | number |  |  |
| triggeredconsumerids | number |  |  |
| vba_emulation | number |  |  |
| yara | number |  |  |
| signal_ids | number |  |  |
| certifications | number |  |  |
| weighted_numerics | number |  |  |
| details7 fields | object |  |  |
| start_date | date-time |  |  |
| file_size | number |  |  |
| tags | array[string] |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| is_dotnet | integer |  |  |
| architecture | string |  |  |
| entropy | number |  |  |

400

Bad request

401

Not authorized

422

Validation Error

 Response
## Backend

Backend wrapper

Endpoints[GET/api/backend/reputation](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reputation-api-backend-reputation-get)
### Get ReputationDeprecated

Wrapper for reputation api

Auth apiKeyQuery String

| sha256 | string | SHA256 digest as found in the response of submit or extracted resource in the report. |  |
| --- | --- | --- | --- |
| hashes | array | Array of one or more hashes |  |

GET /api/backend/reputationcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReputationResponse | object | Response model for get_reputation() |  |
| --- | --- | --- | --- |
| processTime | integer |  |  |
| reputationResults1 field | object | Model for reputationResults field |  |
| INTERNAL3 fields | object | Model for INTERNAL field |  |
| processTime | integer |  |  |
| whitelistedHashes | array |  |  |
| invalidHashes | array |  |  |

422

Validation Error

500

Internal server error

 Response
## Reputation

Reputation

Endpoints[GET/api/reputation/hash](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reputation-hash-api-reputation-hash-get) [POST/api/reputation/hash](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reputation-hash-bulk-api-reputation-hash-post) [GET/api/reputation/{ioc_type}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reputation-ioc-api-reputation--ioc-type--get) [POST/api/reputation/{ioc_type}](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-reputation-ioc-bulk-api-reputation--ioc-type--post)
### Get Reputation Hash

Get the reputation for one given hash

Auth apiKeyQuery String

| sha256 | string |  |  |
| --- | --- | --- | --- |

GET /api/reputation/hashcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReputationResultHash | object |  |  |
| --- | --- | --- | --- |
| sha256 | string |  |  |
| overall_verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| fuzzyhash | object | Fuzzy hash verdict |  |
| hash | string |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| mdcloud3 fields | object | Result of one multiscan |  |
| total_av_engines | integer |  |  |
| detected_av_engines | integer |  |  |
| scan_time | date-time |  |  |
| filescan_reports4 fields | array[object] |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| report_date | string |  |  |
| report_id | string |  |  |
| flow_id | string |  |  |

400

Bad request

401

Not authorized

415

Unsupported media type

422

Validation Error

 Response
### Get Reputation Hash Bulk

Get the reputation for more hashes

Auth apiKeyRequest Body application/json

| array | array[string] |  |  |
| --- | --- | --- | --- |

POST /api/reputation/hashcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReputationResultHash | array[object] |  |  |
| --- | --- | --- | --- |
| sha256 | string |  |  |
| overall_verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| fuzzyhash | object | Fuzzy hash verdict |  |
| hash | string |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| mdcloud3 fields | object | Result of one multiscan |  |
| total_av_engines | integer |  |  |
| detected_av_engines | integer |  |  |
| scan_time | date-time |  |  |
| filescan_reports4 fields | array[object] |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| report_date | string |  |  |
| report_id | string |  |  |
| flow_id | string |  |  |

400

Bad request

401

Not authorized

415

Unsupported media type

422

Validation Error

 Response
### Get Reputation Ioc

Get the reputation for one given IOC

Auth apiKeyPath Params

| ioc_type | string | Enum: `domain`,`ip`,`url` |  |
| --- | --- | --- | --- |

Query String

| ioc_value | string |  |  |
| --- | --- | --- | --- |

GET /api/reputation/{ioc_type}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReputationResultIoc | object |  |  |
| --- | --- | --- | --- |
| ioc_type | string |  |  |
| ioc_value | string |  |  |
| overall_verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| mdcloud | object | Result of one lookup for IP, domain or URL |  |
| scan_time | date-time |  |  |
| detected | integer |  |  |
| community | object |  |  |
| vote_malicious | integer |  |  |
| vote_benign | integer |  |  |
| filescan_reports4 fields | array[object] |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| report_date | string |  |  |
| report_id | string |  |  |
| flow_id | string |  |  |

400

Bad request

401

Not authorized

415

Unsupported media type

422

Validation Error

 Response
### Get Reputation Ioc Bulk

Get the reputation for more IOCs

Auth apiKeyPath Params

| ioc_type | string | Enum: `domain`,`ip`,`url` |  |
| --- | --- | --- | --- |

Request Body application/json

| array | array[string] |  |  |
| --- | --- | --- | --- |

POST /api/reputation/{ioc_type}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| ReputationResultIoc | array[object] |  |  |
| --- | --- | --- | --- |
| ioc_type | string |  |  |
| ioc_value | string |  |  |
| overall_verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| mdcloud | object | Result of one lookup for IP, domain or URL |  |
| scan_time | date-time |  |  |
| detected | integer |  |  |
| community | object |  |  |
| vote_malicious | integer |  |  |
| vote_benign | integer |  |  |
| filescan_reports4 fields | array[object] |  |  |
| verdict | string | An enumeration.  Enum: `unknown`,`benign`,`informational`,`no_threat`,`suspicious`,`likely_malicious`,`malicious` |  |
| report_date | string |  |  |
| report_id | string |  |  |
| flow_id | string |  |  |

400

Bad request

401

Not authorized

415

Unsupported media type

422

Validation Error

 Response
## Docs

API documentation related

Endpoints[GET/api/docs](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-api-docs-api-docs-get) [GET/openapi.json](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-open-api-endpoint-openapi-json-get) [GET/api/docs/styles](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-api-docs-styles-api-docs-styles-get) [GET/api/docs/sitemap](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-sitemap-api-docs-sitemap-get)
### Get API Docs

Return API docs UI

Auth apiKeyGET /api/docscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json text/plain 200

Successful Response

| Response Get Api Docs Api Docs Get | string |  |  |
| --- | --- | --- | --- |

 Response
### Get OpenAPI Endpoint

Return API json data to be used by docs UI

Auth apiKeyGET /openapi.jsoncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| GetOpenApiJsonResponse | object | Response model for get_open_api_endpoint() |  |
| --- | --- | --- | --- |
| openapi | string |  |  |
| info | object |  |  |
| title | string |  |  |
| version | string |  |  |
| paths | object |  |  |
| * | object |  |  |
| components2 fields | object |  |  |
| schemas | object |  |  |
| * | object |  |  |
| securitySchemes1 field | object |  |  |
| apiKey3 fields | object |  |  |
| type | string |  |  |
| in | string |  |  |
| name | string |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| description | string |  |  |

 Response
### Get API Doc Styles

Return styles for api docs

Auth apiKeyGET /api/docs/stylescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| Response Get Api Docs Styles Api Docs Styles Get | string |  |  |
| --- | --- | --- | --- |

 Response
### Get Sitemap

Get sitemap xml

Auth apiKeyGET /api/docs/sitemapcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

 Response
## Ocm

OPSWAT Central Management (OCM)

Endpoints[GET/api/ocm/state](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-integration-state-api-ocm-state-get) [POST/api/ocm/enroll](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#enroll-api-ocm-enroll-post) [POST/api/ocm/unenroll](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#unenroll-api-ocm-unenroll-post)
### Get Integration State

Get current state of OCM integration

Auth apiKeyGET /api/ocm/statecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| OcmIntegrationStateResponse | object |  |  |
| --- | --- | --- | --- |
| server_url | string | Base url of OCM server |  |
| registration_code | string | Code used for obtaining API key for interaction with OCM |  |
| state | string | An enumeration.  Enum: `not_enrolled`,`enrolled`,`unenrolled` |  |
| disconnected | boolean | If we failed to establish connection with OCM |  |
| last_connection_date | date-time | Last time connection was done to OCM |  |
| last_connection_attempt_date | date-time | Last time we tried to edtablish connection with OCM |  |

401

Not authorized

404

Item not found

 Response
### Enroll

Register product at OPSWAT Central Management

Auth apiKeyRequest Body application/json

| OcmEnrollPayload | object |  |  |
| --- | --- | --- | --- |
| server_url | string | Base URL of OCM server |  |
| registration_code | string | Code to reveice API key to interact with OCM |  |

POST /api/ocm/enrollcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

401

Not authorized

422

Validation Error

 Response
### Unenroll

Unregister product at OPSWAT Central Management

Auth apiKeyRequest Body application/json

| OcmUnenrollPayload | object |  |  |
| --- | --- | --- | --- |
| force | boolean | Clear local enrollment data  Default: false |  |

POST /api/ocm/unenrollcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

401

Not authorized

422

Validation Error

 Response
## Ai

AI powered actions

Endpoints[GET/api/ai/report/summary](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#get-ai-summary-api-ai-report-summary-get) [GET/api/ai/report/decompile](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#decompile-disassembly-section-api-ai-report-decompile-get)
### Get Ai Summary

Request AI summary for report

Auth apiKeyQuery String

| report_id | string |  |  |
| --- | --- | --- | --- |

GET /api/ai/report/summarycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AiReportData | object | AI data, provided on some request to analyze some report data |  |
| --- | --- | --- | --- |
| source_id | string | Id of analyzed portion of report. Usually - the `dataUUID` property |  |
| data_type | string | Type of data we request from AI for report  Enum: `summary`,`decompiled_disassembly_section` |  |
| data AiReportDecompiledData.__pydantic_model__Choice 2 |  | Data provided by AI. Not all data, but only portion of it that we need |  |
| AiReportDecompiledData | object | Parsed data of decompiled disassembly section |  |
| functions | array[string] | Extracted names of decompiled functions |  |
| summary | string | Generic summary on all functions |  |
| content | string | Either only all functions with comments, or whole response if we failed to parse it |  |
| created_date | date-time | Date when AI data was received |  |

Expand 400

Bad request

404

Item not found

422

Validation Error

 Response
### Decompile Disassembly Section

Request AI summary for report

Auth apiKeyQuery String

| report_id | string |  |  |
| --- | --- | --- | --- |
| section_id |  |  |  |

GET /api/ai/report/decompilecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| AiReportData | object | AI data, provided on some request to analyze some report data |  |
| --- | --- | --- | --- |
| source_id | string | Id of analyzed portion of report. Usually - the `dataUUID` property |  |
| data_type | string | Type of data we request from AI for report  Enum: `summary`,`decompiled_disassembly_section` |  |
| data AiReportDecompiledData.__pydantic_model__Choice 2 |  | Data provided by AI. Not all data, but only portion of it that we need |  |
| AiReportDecompiledData | object | Parsed data of decompiled disassembly section |  |
| functions | array[string] | Extracted names of decompiled functions |  |
| summary | string | Generic summary on all functions |  |
| content | string | Either only all functions with comments, or whole response if we failed to parse it |  |
| created_date | date-time | Date when AI data was received |  |

Expand 400

Bad request

404

Item not found

422

Validation Error

 Response
## Engine-database-update

Engine database update management

Endpoints[GET/api/updates/engine/database/check](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#check-engine-database-update-api-updates-engine-database-check-g) [POST/api/updates/engine/database/run](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#run-engine-database-update-api-updates-engine-database-run-post) [POST/api/updates/engine/database/run-manual](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#run-manual-engine-database-update-api-updates-engine-database-ru) [POST/api/updates/engine/database/revert](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#revert-engine-database-update-api-updates-engine-database-revert) [GET/api/updates/engine/database/status](/docs/filescan/3.2.0/metadefender-sandbox-api-reference#status-engine-database-update-api-updates-engine-database-status)
### Check Engine Database Update

Check for engine database update for all engines or for specific one

Auth apiKeyQuery String

| app_server | string |  |  |
| --- | --- | --- | --- |

GET /api/updates/engine/database/checkcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| EngineDatabaseUpdateInfo | array[object] |  |  |
| --- | --- | --- | --- |
| app_server | string |  |  |
| status | string | Status of the engine database update  Enum: `active`,`in_progress`,`failed` |  |
| error | string |  |  |
| active_package_version | string |  |  |
| is_fallback_active | boolean | Default: false |  |
| active_database_api_version | string |  |  |
| available_package_version | string |  |  |
| update_available | boolean | Default: false |  |
| last_update | date-time |  |  |
| modified_date | date-time |  |  |
| id | string |  |  |

204

No content

404

Item not found

422

Validation Error

 Response
### Run Engine Database Update

Perform online engine database update for all engines or for specific one

Auth apiKeyQuery String

| app_server | string |  |  |
| --- | --- | --- | --- |

POST /api/updates/engine/database/runcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

204

No content

400

Bad request

404

Item not found

409

Conflict

422

Validation Error

 Response
### Run Manual Engine Database Update

Perform manual engine database update for all engines or for specific engine

Auth apiKeyRequest Body application/x-www-form-urlencoded

| Body_run_manual_engine_database_update_api_updates_engine_database_run_manual_post | object |  |  |
| --- | --- | --- | --- |
| app_server | string |  |  |
| descriptor | file |  |  |
| database_package | file |  |  |

POST /api/updates/engine/database/run-manualcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

400

Bad request

404

Item not found

409

Conflict

422

Validation Error

 Response
### Revert Engine Database Update

Revert engine database to fallback version for all engines or for specific engine

Auth apiKeyQuery String

| app_server | string |  |  |
| --- | --- | --- | --- |

POST /api/updates/engine/database/revertcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| No response body |
| --- |

404

Item not found

409

Conflict

422

Validation Error

 Response
### Status Engine Database Update

Get engine database status for all engines

Auth apiKeyGET /api/updates/engine/database/statuscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful Response

| EngineDatabaseUpdateInfo | array[object] |  |  |
| --- | --- | --- | --- |
| app_server | string |  |  |
| status | string | Status of the engine database update  Enum: `active`,`in_progress`,`failed` |  |
| error | string |  |  |
| active_package_version | string |  |  |
| is_fallback_active | boolean | Default: false |  |
| active_database_api_version | string |  |  |
| available_package_version | string |  |  |
| update_available | boolean | Default: false |  |
| last_update | date-time |  |  |
| modified_date | date-time |  |  |
| id | string |  |  |

 Response
