<!-- source: https://www.opswat.com/docs/product-management/developer-guide/ref -->

Example: <https://192.168.100.251>

My OPSWAT Cloud: https://product.my.opswat.comServer Variables## Authenticationhttp BearerToken

A token can be generated from a secret key that is managed on My OPSWAT console. This can be used as an API Key for API calls that require authentication. This token has expiration time, your application needs to re-generate a new token when it's expired.

## Auth

BearerToken

Endpoints[POST/api/console/get-token](/docs/product-management/developer-guide#gettoken)
### Obtain an access token for API authentication

Obtain an access token for API authentication. This is required for accessing all APIs. Please note that an old access token will become invalid when a new access token is issued for a secret key.

Auth NoneRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| key | string | a secret key that can be obtained from the My OPSWAT console |  |

POST /api/console/get-tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| accessToken | string | an access token for API authentication |  |
| expiredIn | integer | the duration until the access token expires in seconds |  |

400

Bad Request

 Response
## Account

Endpoints[POST/api/console/public/v1/account/inventory](/docs/product-management/developer-guide#postretrieve-account-inventory-or-a-specific-product-inventory)
### Retrieve account inventory or a specific product inventory

Retrieve account inventory or a specific product inventory based on filter criteria.

| Product Type | Product Name |
| --- | --- |
| MK5 | MetaDefender Kiosk L-Series |
| VAULT | MetaDefender Managed File Transfer |
| MDICAP | MetaDefender ICAP Server |
| MDCORE | MetaDefender Core |
| UF3 | MetaDefender Media Firewall |
| MDD | MetaDefender Drive |
| FSCAN | MetaDefender Sandbox |
| NEURALYZER | MetaDefender OT Security |
| OTFUSE | MetaDefender Industrial Firewall & IPS |
| MDSS | MetaDefender Storage Security |
| MDEMAIL | MetaDefender Email Gateway Security |
| NWUSGBLUE | MetaDefender Unidirectional Security Gateway Blue |
| NWUSGRED | MetaDefender Unidirectional Security Gateway Red |
| NWBSGBLUE | MetaDefender Bilateral Security Gateway Blue |
| NWBSGRED | MetaDefender Bilateral Security Gateway Red |
| NWTPBLUE | MetaDefender Transfer Guard Blue |
| NWTPRED | MetaDefender Transfer Guard Red |
| NWODBLUE | MetaDefender Optical Diode Blue |
| NWODRED | MetaDefender Optical Diode Red |
| MDSSC | MetaDefender Software Supply Chain |
| KIOSK | MetaDefender Kiosk K-Series |

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters | object | Filter data |  |
| productTypes | array[string] |  |  |

POST /api/console/public/v1/account/inventorycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| productName | string |  |  |
| productType | string | Enum: `MDCORE` |  |
| totalInstances | integer | total instances |  |
| connectivity4 fields | object |  |  |
| noLicense | integer |  |  |
| disconnected | integer |  |  |
| pending | integer |  |  |
| connected | integer |  |  |
| health5 fields | object |  |  |
| operational | integer |  |  |
| minorIssues | integer |  |  |
| criticalIssues | integer |  |  |
| unknown | integer |  |  |
| significantIssues | integer |  |  |
| version3 fields | array[object] |  |  |
| value | string |  |  |
| total | integer |  |  |
| status | string |  |  |
| license5 fields | object |  |  |
| expiredIn30Days | integer |  |  |
| expiredIn90Days | integer |  |  |
| expiredIn90PlusDays | integer |  |  |
| expired | integer |  |  |
| noLicense | integer |  |  |
| storageCapacity | object |  |  |

401

Unauthorized

403

Forbdden

429

Rate limit

 Response
## Product

Endpoints[POST/api/console/public/v1/mdcore/processing-overview](/docs/product-management/developer-guide#postretrieve-processing-overview-from-metadefender-core-instance) [POST/api/console/public/v1/kiosks/processing-overview](/docs/product-management/developer-guide#postprocessing-overview-from-metadefender-kiosk-instances) [PUT/api/console/public/v1/mdcore/updateModuleSource](/docs/product-management/developer-guide#putchange-module-update-settings-for-metadefender-core-instances) [POST/api/console/public/v1/mdcore/blocked-files](/docs/product-management/developer-guide#postretrieve-details-of-blocked-files) [POST/api/console/public/v1/kiosks/scan-reports/search](/docs/product-management/developer-guide#postretrieve-metadefender-kiosk-scan-sessions) [POST/api/console/public/v1/mdcore/process-history-files/search](/docs/product-management/developer-guide#postretrieve-processing-history-of-metadefender-core-instances) [POST/api/console/public/v2/mdcore/process-history-files/search](/docs/product-management/developer-guide#postretrieve-processing-history-of-metadefender-core-instances-2)
### Retrieve processing overview from MetaDefender Core instances

Retrieve processing overview from MetaDefender Core instances based on filter criteria over a specified time period.
To optimize query time, calculate result is cached by day.
Recommendation: run queries for the full day (00:00–24:00 UTC) to take advantage of the caching mechanism.

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters | object | Filter criteria |  |
| instanceIds | array[string] |  |  |
| groupIds | array[string] |  |  |
| startTime | integer |  |  |
| endTime | integer |  |  |
| groupBy | string | Enum: `groups`,`instances` |  |

POST /api/console/public/v1/mdcore/processing-overviewcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpGroup by groupsGroup by instancesResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| totalProcessedFiles | integer |  |  |
| totalProcessedObjects | integer |  |  |
| totalBlockedFiles | integer |  |  |
| totalBlockedObjects | integer |  |  |
| totalObjectsWithThreats | integer |  |  |
| totalFilesWithThreats | integer |  |  |
| totalUsersSubmittedScans | integer |  |  |
| totalUniqueUsersSubmittedScans | integer |  |  |
| avgScanTimePerObject | integer |  |  |
| avgScanTimePerFile | integer |  |  |
| groups12 fields | array[object] |  |  |
| groupName | string |  |  |
| groupId | string |  |  |
| totalProcessedFiles | integer |  |  |
| totalProcessedObjects | integer |  |  |
| totalBlockedFiles | integer |  |  |
| totalBlockedObjects | integer |  |  |
| totalObjectsWithThreats | integer |  |  |
| totalFilesWithThreats | integer |  |  |
| totalUsersSubmittedScans | integer |  |  |
| totalUniqueUsersSubmittedScans | integer |  |  |
| avgScanTimePerObject | integer |  |  |
| avgScanTimePerFile | integer |  |  |

400

Bad Request

401

Unauthorized

403

Forbdden

429

Rate limit

 Response Group by groupsGroup by instances
### Processing Overview from MetaDefender Kiosk instances

Retrieve processing overview from MetaDefender Kiosk K-Series and L-Series instances based on filter criteria over a specified time period

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters | object | Filter criteria |  |
| instanceIds | array[string] |  |  |
| groupIds | array[string] |  |  |
| startTime | integer | timestamp in miliseconds |  |
| endTime | integer | timestamp in miliseconds |  |
| groupBy | string | Enum: `groups`,`instances` |  |

POST /api/console/public/v1/kiosks/processing-overviewcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpGroup by groupsGroup by instancesResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| numberOfSessions | integer | total number of scan sessions during the selected time period and based on the applied filters |  |
| numberOfFilesProcessed | integer |  |  |
| numberOfSessionsWithThreatsDetected | integer |  |  |
| numberOfThreatsFound | integer |  |  |
| numberOfFilesSanitized | integer |  |  |
| numberOfFilesMovedToMFT | integer |  |  |
| avgTimeOfASessionInMinutes | integer |  |  |
| groups9 fields | array[object] | this array will be returned when groupBy is set to 'groups' |  |
| id | string |  |  |
| name | string |  |  |
| numberOfSessions | integer |  |  |
| numberOfFilesProcessed | integer |  |  |
| numberOfSessionsWithThreatsDetected | integer |  |  |
| numberOfThreatsFound | integer |  |  |
| numberOfFilesSanitized | integer |  |  |
| numberOfFilesMovedToMFT | integer |  |  |
| avgTimeOfASessionInMinutes | integer |  |  |

400

Bad Request

401

Unauthorized

403

Forbdden

429

Rate limit

 Response Group by groupsGroup by instances
### Change module update settings for MetaDefender Core instances

Allow users to change module update settings for MetaDefender Core instances

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| deploymentId | string |  |  |
| source | string | Enum: `internet`,`folder`,`manually` |  |

PUT /api/console/public/v1/mdcore/updateModuleSourcecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

OK

| No response body |
| --- |

400

Bad Request

401

Unauthorized

403

Forbdden

429

Rate limit

 Response
### Retrieve details of blocked files

Retrieve details of blocked files from MetaDefencer Core instances based on filter criteria over a specified time period

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters | object | Filter criteria |  |
| instanceIds | array[string] |  |  |
| groupIds | array[string] |  |  |
| startTime | integer | timestamp in miliseconds |  |
| endTime | integer | timestamp in miliseconds |  |
| page | integer |  |  |
| limit | integer |  |  |

POST /api/console/public/v1/mdcore/blocked-filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| fileName | string |  |  |
| fileType | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeId | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| numberOfEngineUsed | integer |  |  |
| blockReason | string |  |  |
| detectedMalwares | object | List malware names engines detected. Note that only list engines detected a file as threat so that this list can be empty. |  |
| enginename | string |  |  |
| coreId | string |  |  |
| coreInstanceName | string |  |  |
| groupName | string |  |  |
| groupId | string |  |  |
| workflow | string | workflow a Core used to process the file |  |
| user | string | a user who uploaded the file to Core to process |  |
| startedTime | integer | in miliseconds |  |
| durationInSeconds | number |  |  |
| clients6 fields | array[object] | records the file's transfer log, showing who (clients.user_name) uploaded it to which product instance (clients.deployment_id, clients.product_type), and when (clients.timestamp). |  |
| deployment_id | string |  |  |
| user_name | string |  |  |
| product_type | string | prefer the product type definition in the Inventory API's description |  |
| version | string |  |  |
| host | string |  |  |
| timestamp | integer |  |  |

Expand 400

Bad Request

401

Unauthorized

403

Forbdden

429

Rate limit

 Response
### Retrieve MetaDefender Kiosk scan sessions

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters | object | Filter criteria |  |
| instanceIds | array[string] |  |  |
| groupIds | array[string] |  |  |
| startTime | integer | timestamp in miliseconds |  |
| endTime | integer | timestamp in miliseconds |  |
| page | integer |  |  |
| limit | integer |  |  |

POST /api/console/public/v1/kiosks/scan-reports/searchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| instanceId | string |  |  |
| instanceName | string |  |  |
| deploymentId | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| sessionStart | integer |  |  |
| sessionEnd | integer |  |  |
| reportTime | integer |  |  |
| productType | string |  |  |
| userInfo4 fields | object |  |  |
| profileID | string |  |  |
| userName | string |  |  |
| vault_id | object |  |  |
| * | string |  |  |
| user_question_answer | array[object] |  |  |
| * | string |  |  |

400

Bad Request

401

Unauthorized

403

Forbidden

429

Rate limit

 Response
### Retrieve processing history of MetaDefender Core instances

Retrieve details of blocked files from MetaDefencer Core instances based on filter criteria over a specified time period

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters3 fields | object | Filter criteria |  |
| instanceIds | array[string] |  |  |
| groupIds | array[string] |  |  |
| status | array[string] | Enum: `Blocked`,`Allowed`,`Processing` |  |
| startTime | integer | timestamp in miliseconds |  |
| endTime | integer | timestamp in miliseconds |  |
| page | integer |  |  |
| limit | integer |  |  |

POST /api/console/public/v1/mdcore/process-history-files/searchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| fileName | string |  |  |
| fileType | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeId | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| numberOfEngineUsed | integer |  |  |
| blockReason | string |  |  |
| detectedMalwares | object | List malware names engines detected. Note that only list engines detected a file as threat so that this list can be empty. |  |
| enginename | string |  |  |
| coreId | string |  |  |
| coreInstanceName | string |  |  |
| groupName | string |  |  |
| groupId | string |  |  |
| workflow | string | workflow a Core used to process the file |  |
| user | string | a user who uploaded the file to Core to process |  |
| startedTime | integer | in miliseconds |  |
| durationInSeconds | number |  |  |
| clients6 fields | array[object] | records the file's transfer log, showing who (clients.user_name) uploaded it to which product instance (clients.deployment_id, clients.product_type), and when (clients.timestamp). |  |
| deployment_id | string |  |  |
| user_name | string |  |  |
| product_type | string | prefer the product type definition in the Inventory API's description |  |
| version | string |  |  |
| host | string |  |  |
| timestamp | integer |  |  |

Expand 400

Bad Request

401

Unauthorized

403

Forbdden

429

Rate limit

 Response
### Retrieve processing history of MetaDefender Core instances

Retrieve details of processing history from MetaDefender Core instances based on filter criteria over a specified time period

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| filters4 fields | object | Default: {} |  |
| instanceIds | array[string] | Default: [] |  |
| groupIds | array[string] | Default: [] |  |
| requestTypes | array[string] | rest - all files which are not batch, extracted - all objects in a file, batch - all scan sessions, batched - all files in a batch, non-batch can be filtered by [ rest, extracted, batched]  Enum: `rest`,`extracted`,`batch`,`batched`  Default: [] |  |
| statuses | array[string] | Enum: `Allowed`,`Blocked`  Default: [] |  |
| startTime | int64 |  |  |
| endTime | int64 |  |  |
| limit | integer | maximum: 100  minimum: 1 |  |
| nextToken | string |  |  |

POST /api/console/public/v2/mdcore/process-history-files/searchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttprequest bodyrequest body with next tokenrequest with filtersResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| data27 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| status | string |  |  |
| sessionId | string |  |  |
| accountId | string |  |  |
| instanceId | string |  |  |
| instanceName | string |  |  |
| fileName | string |  |  |
| result | string |  |  |
| workflow | string |  |  |
| username | string |  |  |
| source | string |  |  |
| startTime | int64 |  |  |
| endTime | int64 |  |  |
| totalTime | integer |  |  |
| sha256 | string |  |  |
| fileType | object |  |  |
| key | string |  |  |
| description | string |  |  |
| fileSize | integer |  |  |
| actions | array[string] |  |  |
| reportTime | int64 |  |  |
| parentSessionIds | array[string] |  |  |
| numberOfEngineUsed | integer |  |  |
| requestType | string |  |  |
| processingTimeDetails9 fields | object |  |  |
| avScanTime | integer |  |  |
| avWaitTime | integer |  |  |
| cloudLookupTime | integer |  |  |
| dlpTime | integer |  |  |
| othersTime | integer |  |  |
| yaraTime | integer |  |  |
| filetypeTime | integer |  |  |
| reputationTime | integer |  |  |
| vulTime | integer |  |  |
| progressPercentage | integer |  |  |
| verdicts | array[string] |  |  |
| clients6 fields | array[object] |  |  |
| deployment_id | string |  |  |
| user_name | string |  |  |
| product_type | string |  |  |
| version | string |  |  |
| host | string |  |  |
| timestamp | int64 |  |  |
| nextToken | string |  |  |

400

Bad Request

401

Unauthorized

403

Forbidden

429

Rate limit

 Response Response body
