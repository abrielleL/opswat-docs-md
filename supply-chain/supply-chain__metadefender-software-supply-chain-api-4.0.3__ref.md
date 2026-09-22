<!-- source: https://www.opswat.com/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3/ref -->

## Authentication

This section of the user guide describes how you can programmatically
interact with the MetaDefender Software Supply Chain REST API. Below are some
common tasks that can be done using the available REST APIs:

- Authenticate to obtain a JSON Web Token(JWT)
- Start or stop a process(scan)
- Add / remove service units

## About this REST API

The exposed endpoint is located by default at **http(s)://mdssc-server/api/** (for example, the authentication endpoint is available at **http(s)://mdssc-server/api/user/authenticate**). All requests are handled by the NGINX web server before being proxied to the backend API Gateway service.

All endpoints perform authentication and authorization checks. For these checks to succeed, a valid token should be presented in the Authorization header in the form of Bearer.

Please note that all issued tokens have a timestamp and signature associated in order to prevent long-term usage without re - authentication. The lifespan of the token is currently set to 60 minutes, meaning you will have to request a new token before it expires in order to avoid error responses.

## Useful links

- [MetaDefender Software Supply Chain Documentation](https://docs.opswat.com/supply-chain)
- [Scalar UI Documentation](https://guides.scalar.com/scalar/scalar-api-references/getting-started)
Serverhttp://localhost:8001Server Variables## Authenticationhttp BearerapiKey ApiKeyFields

| Key | In |
| --- | --- |
| ApiKey | Header |  |

## Monitored Files

Endpoints[POST/api/v1/monitored-files](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postmonitored-files) [GET/api/v1/monitored-files](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getmonitored-files) [GET/api/v1/monitored-files/{id}/history](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#gethistory) [POST/api/v1/monitored-files/{id}/scan-now](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postscan-now) [POST/api/v1/monitored-files/{id}/enabled](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postenabled) [POST/api/v1/monitored-files/{id}/interval](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postinterval) [DELETE/api/v1/monitored-files/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deleteid)
### monitored-files

Auth NoneRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| file | file |  |  |
| workflowId | string | Default: null |  |
| intervalMinutes | int32 | Default: null |  |
| groupId | string | Default: null |  |
| groupName | string | Default: null |  |

POST /api/v1/monitored-filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| originalFileName | string |  |  |
| sha256 | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| enabled | boolean |  |  |
| rescanIntervalMinutes | int32 |  |  |
| newCveCount | int32 |  |  |
| lastRunAt | date-time |  |  |
| nextRunAt | date-time |  |  |
| createdAt | date-time |  |  |

 Response
### monitored-files

Auth NoneGET /api/v1/monitored-filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| originalFileName | string |  |  |
| sha256 | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| enabled | boolean |  |  |
| rescanIntervalMinutes | int32 |  |  |
| newCveCount | int32 |  |  |
| lastRunAt | date-time |  |  |
| nextRunAt | date-time |  |  |
| createdAt | date-time |  |  |

 Response
### history

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/monitored-files/{id}/historycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| scanId | string |  |  |
| runAt | date-time |  |  |
| newCveIds | string |  |  |

 Response
### scan-now

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

POST /api/v1/monitored-files/{id}/scan-nowcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| originalFileName | string |  |  |
| sha256 | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| enabled | boolean |  |  |
| rescanIntervalMinutes | int32 |  |  |
| newCveCount | int32 |  |  |
| lastRunAt | date-time |  |  |
| nextRunAt | date-time |  |  |
| createdAt | date-time |  |  |

 Response
### enabled

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| enabled | boolean |  |  |

POST /api/v1/monitored-files/{id}/enabledcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| originalFileName | string |  |  |
| sha256 | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| enabled | boolean |  |  |
| rescanIntervalMinutes | int32 |  |  |
| newCveCount | int32 |  |  |
| lastRunAt | date-time |  |  |
| nextRunAt | date-time |  |  |
| createdAt | date-time |  |  |

 Response
### interval

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| intervalMinutes | int32 |  |  |

POST /api/v1/monitored-files/{id}/intervalcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| originalFileName | string |  |  |
| sha256 | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| enabled | boolean |  |  |
| rescanIntervalMinutes | int32 |  |  |
| newCveCount | int32 |  |  |
| lastRunAt | date-time |  |  |
| nextRunAt | date-time |  |  |
| createdAt | date-time |  |  |

 Response
### {id}

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/monitored-files/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 204

No Content

| No response body |
| --- |

 Response
## Manage Abac Attribute-based Access Control

Endpoints[GET/api/v1/abac/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-roles) [POST/api/v1/abac/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcreate-role) [GET/api/v1/abac/roles/{roleId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-role-by-id) [PUT/api/v1/abac/roles/{roleId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-role) [DELETE/api/v1/abac/roles/{roleId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-role) [GET/api/v1/abac/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-permissions) [POST/api/v1/abac/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcreate-permission) [DELETE/api/v1/abac/permissions/{permissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-permission) [POST/api/v1/abac/roles/{roleId}/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postassign-permission-to-role) [DELETE/api/v1/abac/roles/{roleId}/permissions/{permissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deleteremove-permission-from-role) [POST/api/v1/abac/users/{userId}/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postassign-role-to-user) [PUT/api/v1/abac/users/{userId}/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putreplace-user-roles) [DELETE/api/v1/abac/users/{userId}/roles/{roleBindingId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deleteremove-role-from-user) [POST/api/v1/abac/users/{userId}/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postassign-permission-to-user) [DELETE/api/v1/abac/users/{userId}/permissions/{userPermissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deleteremove-permission-from-user)
### Get Roles

Auth NoneQuery String

| includePermissions | boolean | Default: true |  |
| --- | --- | --- | --- |

GET /api/v1/abac/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| roles3 fields | array[object] |  |  |
| id | uuid |  |  |
| name | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | uuid |  |  |
| action | string |  |  |
| resource | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Create Role

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 100  minLength: 3 |  |
| permissionIds | array[string] |  |  |
| templateRoleId | uuid |  |  |

POST /api/v1/abac/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| role3 fields | object |  |  |
| id | uuid |  |  |
| name | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | uuid |  |  |
| action | string |  |  |
| resource | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Get Role by ID

Auth NonePath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/abac/roles/{roleId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| role3 fields | object |  |  |
| id | uuid |  |  |
| name | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | uuid |  |  |
| action | string |  |  |
| resource | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Update Role

Auth NonePath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 100  minLength: 3 |  |
| permissionIds | array[string] |  |  |

PUT /api/v1/abac/roles/{roleId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Delete Role

Auth NonePath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/abac/roles/{roleId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Get Permissions

Auth NoneGET /api/v1/abac/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| permissions3 fields | array[object] |  |  |
| id | uuid |  |  |
| action | string |  |  |
| resource | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Create Permission

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| action | string |  |  |
| resource | string |  |  |

POST /api/v1/abac/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| permission3 fields | object |  |  |
| id | uuid |  |  |
| action | string |  |  |
| resource | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Delete Permission

Auth NonePath Params

| permissionId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/abac/permissions/{permissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Assign Permission to Role

Auth NonePath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| permissionId | uuid |  |  |

POST /api/v1/abac/roles/{roleId}/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Remove Permission from Role

Auth NonePath Params

| roleId | string |  |  |
| --- | --- | --- | --- |
| permissionId | string |  |  |

DELETE /api/v1/abac/roles/{roleId}/permissions/{permissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Assign Role to User

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| roleId | uuid |  |  |
| expiresAt | date-time |  |  |

POST /api/v1/abac/users/{userId}/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| roleBindingId | uuid |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Replace User Roles

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| roleIds | array[string] |  |  |

PUT /api/v1/abac/users/{userId}/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Remove Role from User

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |
| roleBindingId | string |  |  |

DELETE /api/v1/abac/users/{userId}/roles/{roleBindingId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Assign Permission to User

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| permissionId | uuid |  |  |
| expiresAt | date-time |  |  |

POST /api/v1/abac/users/{userId}/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| userPermissionId | uuid |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Remove Permission from User

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |
| userPermissionId | string |  |  |

DELETE /api/v1/abac/users/{userId}/permissions/{userPermissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Audit

Endpoints[GET/api/v1/audit](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getlist-audit-events)
### List audit events

Auth NoneQuery String

| Start | string | pattern: `^[0-9]*$` |  |
| --- | --- | --- | --- |
| Count | string | pattern: `^[0-9]*$` |  |
| LogType | array |  |  |
| CategoryType | string | pattern: `^[0-9]*$` |  |
| LogLevel | string | pattern: `^[0-9]*$` |  |
| Search | string | pattern: `^[0-9]*$` |  |

GET /api/v1/auditcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| entries4 fields | array[object] |  |  |
| id | string |  |  |
| level | integer |  |  |
| properties5 fields | object |  |  |
| logType | integer |  |  |
| category | integer |  |  |
| eventTimestamp | date-time |  |  |
| userId | string |  |  |
| userName | string |  |  |
| renderedMessage | string |  |  |
| totalCount | int64 |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
## Manage Configuration

Endpoints[GET/api/v1](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-application-configuration)
### Get application configuration

Auth NoneGET /api/v1cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Cross Domain Transfers

Endpoints[POST/api/v1/cross-domain/file-stream](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postreceive-a-full-file-as-a-single-framed-binary-stream-with-ma) [GET/api/v1/cross-domain/global-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-global-lowside-configuration) [PUT/api/v1/cross-domain/global-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putset-global-lowside-configuration) [POST/api/v1/cross-domain/global-config/lowside/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postdisable-global-lowside-configuration) [GET/api/v1/cross-domain/global-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-global-highside-configuration) [PUT/api/v1/cross-domain/global-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putset-global-highside-configuration) [POST/api/v1/cross-domain/global-config/highside/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postdisable-global-highside-configuration) [GET/api/v1/cross-domain/logs](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-cross-domain-operation-logs) [DELETE/api/v1/cross-domain/logs/{transmissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-cross-domain-activity-log-entry-by-transmission-i) [POST/api/v1/cross-domain/lowside-configuration-notifications](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postreceive-a-lowside-configuration-change-notification) [GET/api/v1/cross-domain/notifications](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-cross-domain-notifications) [GET/api/v1/cross-domain/storage-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-lowside-configuration-by-storage-id) [POST/api/v1/cross-domain/storage-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-lowside-configuration) [PUT/api/v1/cross-domain/storage-config/lowside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-lowside-configuration-by-id) [DELETE/api/v1/cross-domain/storage-config/lowside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-lowside-configuration-by-id) [GET/api/v1/cross-domain/storage-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-highside-storage-configuration-by-storage-id) [POST/api/v1/cross-domain/storage-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-highside-configuration) [PUT/api/v1/cross-domain/storage-config/highside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-highside-configuration-by-id) [DELETE/api/v1/cross-domain/storage-config/highside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-highside-configuration-by-id)
### Receive a full file as a single framed binary stream with manifest in headers

Auth NoneHeaders

| receiveFileStreamDto9 fields | object |  |  |
| --- | --- | --- | --- |
| transmissionId | string |  |  |
| fileName | string |  |  |
| fileSizeBytes | int64 |  |  |
| totalChunks | int64 |  |  |
| chunkSizeBytes | int32 |  |  |
| storageName | string |  |  |
| repositoryName | string |  |  |
| reference | string |  |  |
| organization | string |  |  |

POST /api/v1/cross-domain/file-streamcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

500

Internal Server Error

 Response
### Get global lowside configuration

Auth NoneGET /api/v1/cross-domain/global-config/lowsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| configuration | object |  |  |
| highsideAddress | string |  |  |
| enabled | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Set global lowside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| highsideAddress | string |  |  |
| authorizationToken | string |  |  |
| enabled | boolean |  |  |

PUT /api/v1/cross-domain/global-config/lowsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Disable global lowside configuration

Auth NonePOST /api/v1/cross-domain/global-config/lowside/disablecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Get global highside configuration

Auth NoneGET /api/v1/cross-domain/global-config/highsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| configuration8 fields | object |  |  |
| pushBehaviour | integer |  |  |
| enabled | boolean |  |  |
| scanBeforeImport | boolean |  |  |
| scanWorkflowId | string |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |
| scanTimeoutSeconds | int32 |  |  |
| pollIntervalSeconds | int32 |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Set global highside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| pushBehaviour | integer |  |  |
| enabled | boolean |  |  |
| scanBeforeImport | boolean |  |  |
| scanWorkflowId | string |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |
| scanTimeoutSeconds | int32 |  |  |
| pollIntervalSeconds | int32 |  |  |

PUT /api/v1/cross-domain/global-config/highsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Disable global highside configuration

Auth NonePOST /api/v1/cross-domain/global-config/highside/disablecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Get cross-domain operation logs

Auth NoneQuery String

| page | integer | Default: null |  |
| --- | --- | --- | --- |
| pageSize | integer | Default: null |  |
| sortBy | string | pattern: `^[0-9]*$`  Default: null |  |
| sortOrder | string | pattern: `^[0-9]*$`  Default: null |  |
| filter | string | pattern: `^[0-9]*$`  Default: null |  |
| search | string | pattern: `^[0-9]*$`  Default: null |  |

GET /api/v1/cross-domain/logscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| logs14 fields | array[object] |  |  |
| id | string |  |  |
| transmissionId | string |  |  |
| storageId | string |  |  |
| step | integer |  |  |
| status | integer |  |  |
| timestamp | date-time |  |  |
| storageName | string |  |  |
| storage9 fields | object |  |  |
| id | string |  |  |
| credentialsType | int32 |  |  |
| scanWorkflowId | string |  |  |
| domain | string |  |  |
| realTimeStatus | integer |  |  |
| name | string |  |  |
| vendorType | integer |  |  |
| protocolType | integer |  |  |
| lowsideRepositoryName | string |  |  |
| highsideRepositoryName | string |  |  |
| reference | string |  |  |
| scanId | string |  |  |
| fileId | string |  |  |
| errorMessage | string |  |  |
| hasNextPage | boolean |  |  |
| hasPreviousPage | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Delete a cross-domain activity-log entry by transmission id

Auth NonePath Params

| transmissionId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/cross-domain/logs/{transmissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Receive a lowside configuration change notification

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageName | string |  |  |
| protocolType | integer |  |  |
| changeType | integer |  |  |

POST /api/v1/cross-domain/lowside-configuration-notificationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get all cross-domain notifications

Auth NoneGET /api/v1/cross-domain/notificationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| notifications6 fields | array[object] |  |  |
| id | string |  |  |
| storageName | string |  |  |
| protocolType | integer |  |  |
| changeType | integer |  |  |
| receivedAt | date-time |  |  |
| acknowledged | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Get a lowside configuration by storage ID

Auth NoneGET /api/v1/cross-domain/storage-config/lowsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| configurations5 fields | array[object] |  |  |
| id | string |  |  |
| storageId | string |  |  |
| storageName | string |  |  |
| protocolType | integer |  |  |
| valid | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Add a lowside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |

POST /api/v1/cross-domain/storage-config/lowsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| configurationId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Update a lowside configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |

PUT /api/v1/cross-domain/storage-config/lowside/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Delete a lowside configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/cross-domain/storage-config/lowside/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Get a highside storage configuration by storage ID

Auth NoneGET /api/v1/cross-domain/storage-config/highsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| configurations6 fields | array[object] |  |  |
| id | string |  |  |
| storageId | string |  |  |
| storageName | string |  |  |
| lowsideStorageName | string |  |  |
| lowsideProtocolType | integer |  |  |
| valid | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Add a highside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |
| notificationId | string |  |  |

POST /api/v1/cross-domain/storage-config/highsidecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| configurationId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Update a highside configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |
| storageName | string |  |  |
| lowsideStorageName | string |  |  |

PUT /api/v1/cross-domain/storage-config/highside/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Delete a highside configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/cross-domain/storage-config/highside/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
## Manage Dashboard

Endpoints[GET/api/v1/dashboard](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-the-dashboard-summary-and-trends-time-series) [GET/api/v1/dashboard/top-risky](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-top-risky-repositories-across-all-connections)
### Get the dashboard summary and trends time-series

Auth NoneQuery String

| connection_id | string |  |  |
| --- | --- | --- | --- |
| window | string |  |  |
| timezone | string |  |  |

GET /api/v1/dashboardcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| summary19 fields | object |  |  |
| totalConnections | int32 |  |  |
| totalScannedRepositories | int32 |  |  |
| totalScannedRepositoriesTrend | int32 |  |  |
| totalPackages | int32 |  |  |
| totalPackagesTrend | int32 |  |  |
| riskScore | int32 |  |  |
| riskScoreTrend | int32 |  |  |
| criticalVulnerabilities | int32 |  |  |
| criticalPackages | int32 |  |  |
| criticalRepositories | int32 |  |  |
| totalVulnerabilities | int32 |  |  |
| totalVulnerabilitiesTrend | int32 |  |  |
| totalThreats | int32 |  |  |
| totalThreatsTrend | int32 |  |  |
| totalSecrets | int32 |  |  |
| totalSecretsTrend | int32 |  |  |
| severity5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| topRiskyPackages | array[object] |  |  |
| name | string |  |  |
| criticalCount | int32 |  |  |
| topRiskyRepositories | array[object] |  |  |
| name | string |  |  |
| detectionCount | int32 |  |  |
| trends9 fields | array[object] |  |  |
| periodStart | date-time |  |  |
| periodEnd | date-time |  |  |
| totalVulnerabilities | int32 |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| scansConsidered | int32 |  |  |

400

Bad Request

500

Internal Server Error

 Response
### Get top-risky repositories across all connections

Auth NoneQuery String

| window | string |  |  |
| --- | --- | --- | --- |
| count | integer | Default: null |  |

GET /api/v1/dashboard/top-riskycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| connectionId | string |  |  |
| connectionName | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| riskScore | int32 |  |  |

400

Bad Request

500

Internal Server Error

 Response
## Manage Export

Endpoints[GET/api/v1/export/cyclonedx/{repoId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-cyclonedx-report-for-repository) [GET/api/v1/export/cyclonedx/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-cyclonedx-report-for-a-specific-file-scan) [GET/api/v1/export/spdx/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-an-spdx-report-for-a-specific-scan) [GET/api/v1/export/spdx/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-an-spdx-report-for-a-specific-file-scan) [GET/api/v1/export/pdf/all-scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-pdf-report-for-all-scans) [GET/api/v1/export/pdf/overview/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-pdf-overview-report-for-repository) [GET/api/v1/export/pdf/sbom/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-pdf-sbom-report-for-repository) [GET/api/v1/export/pdf/sbom/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-pdf-sbom-report-for-a-specific-batch-of-files) [GET/api/v1/export/pdf/sbom/dependencies/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-pdf-sbom-report-for-repository-that-lists-every-pack) [GET/api/v1/export/csv/sbom/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-csv-report-for-repository) [GET/api/v1/export/csv/sbom/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-csv-report-for-a-specific-batch-of-files) [GET/api/v1/export/csv/cves](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-csv-report-of-all-cves-from-latest-scans) [GET/api/v1/export/csv/packages](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getexport-a-csv-report-of-all-packages-from-latest-scans)
### Export a CycloneDX report for repository

Auth NonePath Params

| repoId | string |  |  |
| --- | --- | --- | --- |

Query String

| Reference | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |

GET /api/v1/export/cyclonedx/{repoId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a CycloneDX report for a specific file scan

Auth NonePath Params

| fileId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/export/cyclonedx/file/{fileId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export an SPDX report for a specific scan

Auth NonePath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

Query String

| format | string |  |  |
| --- | --- | --- | --- |
| version | string |  |  |

GET /api/v1/export/spdx/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export an SPDX report for a specific file scan

Auth NonePath Params

| fileId | string |  |  |
| --- | --- | --- | --- |

Query String

| format | string |  |  |
| --- | --- | --- | --- |
| version | string |  |  |

GET /api/v1/export/spdx/file/{fileId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a PDF report for all scans

Auth NoneQuery String

| ProductAddress | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |
| Type | array |  |  |
| TimeFrame | string | pattern: `^[0-9]*$`  Default: null |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string | pattern: `^[0-9]*$`  Default: null |  |
| Connection | string | pattern: `^[0-9]*$`  Default: null |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string | pattern: `^[0-9]*$`  Default: null |  |
| ConnectionType | string | pattern: `^[0-9]*$`  Default: null |  |
| RepositoryId | string | pattern: `^[0-9]*$`  Default: null |  |
| Latest | boolean |  |  |

GET /api/v1/export/pdf/all-scanscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a PDF overview report for repository

Auth NonePath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

Query String

| ProductAddress | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |

GET /api/v1/export/pdf/overview/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a PDF SBOM report for repository

Auth NonePath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

Query String

| ProductAddress | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |

GET /api/v1/export/pdf/sbom/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a PDF SBOM report for a specific batch of files

Auth NonePath Params

| fileId | string |  |  |
| --- | --- | --- | --- |

Query String

| ProductAddress | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |

GET /api/v1/export/pdf/sbom/file/{fileId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a PDF SBOM report for repository that lists every package dependency as its own package

Auth NonePath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

Query String

| ProductAddress | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |

GET /api/v1/export/pdf/sbom/dependencies/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a CSV report for repository

Auth NonePath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/export/csv/sbom/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a CSV report for a specific batch of files

Auth NonePath Params

| fileId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/export/csv/sbom/file/{fileId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a CSV report of all CVEs from latest scans

Auth NoneQuery String

| Severity | array |  |  |
| --- | --- | --- | --- |

GET /api/v1/export/csv/cvescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

 Response
### Export a CSV report of all packages from latest scans

Auth NoneGET /api/v1/export/csv/packagescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag2 fields | object |  |  |
| tag5 fields | object |  |  |
| buffer | string |  |  |
| offset | int32 |  |  |
| length | int32 |  |  |
| value | string |  |  |
| hasValue | boolean |  |  |
| isWeak | boolean |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

 Response
## Manage External Loggers

Endpoints[GET/api/v1/externallogger](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-external-loggers) [POST/api/v1/externallogger](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-an-external-logger) [PUT/api/v1/externallogger/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-an-external-logger) [DELETE/api/v1/externallogger/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-an-external-logger)
### Get all external loggers

Auth NoneGET /api/v1/externalloggercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### Add an external logger

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| connectionSettings4 fields | object |  |  |
| serverAddress | string |  |  |
| port | int32 |  |  |
| facility | integer |  |  |
| format | integer |  |  |

POST /api/v1/externalloggercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### Update an external logger

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| connectionSettings4 fields | object |  |  |
| serverAddress | string |  |  |
| port | int32 |  |  |
| facility | integer |  |  |
| format | integer |  |  |

PUT /api/v1/externallogger/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### Delete an external logger

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/externallogger/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
## Manage Global Label Keys

Endpoints[GET/api/v1/global-label-keys](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getreturns-all-global-label-keys) [POST/api/v1/global-label-keys](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadds-a-new-global-label-key) [PUT/api/v1/global-label-keys/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdates-an-global-label-key) [DELETE/api/v1/global-label-keys/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedeletes-an-global-label-key)
### Returns all global label keys

Auth NoneGET /api/v1/global-label-keyscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| globalKeys10 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| valueType | string |  |  |
| options | array[string] |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| tenantId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Adds a new global label key

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| description | string |  |  |
| valueType | string |  |  |
| options | array[string] |  |  |

POST /api/v1/global-label-keyscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| globalKey10 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| valueType | string |  |  |
| options | array[string] |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| tenantId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Updates an global label key

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| description | string |  |  |
| valueType | string |  |  |
| options | array[string] |  |  |

PUT /api/v1/global-label-keys/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| globalKey10 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| valueType | string |  |  |
| options | array[string] |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| tenantId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Deletes an global label key

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/global-label-keys/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Jobs V2

Endpoints[POST/api/v1/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#poststart-a-scan-now-job-over-one-or-more-targets-each-target-ca) [GET/api/v1/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getlist-jobs-paginated-queryable-by-trigger-type) [DELETE/api/v1/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletebulk-delete-jobs-trigger-agnostic) [POST/api/v1/jobs/rtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#poststart-a-real-time-protection-job-over-one-or-more-targets-ea) [POST/api/v1/jobs/scheduled](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcreate-a-scheduled-job-with-a-recurrence-pattern) [DELETE/api/v1/jobs/scheduled](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-all-upcoming-jobs) [POST/api/v1/jobs/{id}/cancel](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcancel-a-job-for-realtime-jobs-this-disables-rtp) [GET/api/v1/jobs/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-single-job-by-id)
### Start a Scan Now job over one or more targets (each target carries its own StorageId, so a single job may mix protocols)

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| priority | integer |  |  |
| workflowId | string |  |  |
| targets9 fields | array[object] |  |  |
| storageId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| connection | string |  |  |
| organization | string |  |  |
| packageType | string |  |  |
| repositoryType | string |  |  |
| references | array[string] |  |  |

POST /api/v1/jobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jobIds | array[string] |  |  |
| priority | integer |  |  |
| enabledRepositories | array[string] |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

207

Multi-Status

400

Bad Request

 Response
### List jobs (paginated, queryable by trigger type)

Auth NoneQuery String

| TriggerType | array | Enum: `ScanNow`,`Scheduled`,`RealTime`,`DirectFile` |  |
| --- | --- | --- | --- |
| Priority | array |  |  |
| Status | array |  |  |
| WorkflowId | array |  |  |
| Search | string | pattern: `^[0-9]*$`  Default: null |  |
| TimeFrame | string | pattern: `^[0-9]*$`  Default: null |  |
| Type | array |  |  |
| ConnectionType | string | pattern: `^[0-9]*$`  Default: null |  |
| Repository | string | pattern: `^[0-9]*$`  Default: null |  |
| Service | string | pattern: `^[0-9]*$`  Default: null |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Threats | boolean |  |  |
| Secrets | boolean |  |  |
| SortBy | string | pattern: `^[0-9]*$`  Default: null |  |
| SortDir | string | pattern: `^[0-9]*$`  Default: null |  |
| Page | integer |  |  |
| PageSize | integer |  |  |

Expand GET /api/v1/jobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page | int32 |  |  |
| pageSize | int32 |  |  |
| totalCount | int32 |  |  |
| hasMoreItems | boolean |  |  |
| jobs9 fields | array[object] |  |  |
| jobId | string |  |  |
| name | string |  |  |
| priority | integer |  |  |
| storage7 fields | object |  |  |
| storageId | string |  |  |
| storageName | string |  |  |
| vendorType | string |  |  |
| protocolType | string |  |  |
| connection | string |  |  |
| packageType | string |  |  |
| organization | string |  |  |
| repository6 fields | object |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryType | string |  |  |
| repositoryUrl | string |  |  |
| repositoryReference | string |  |  |
| repositoryMetadata | string |  |  |
| scanInformation11 fields | object |  |  |
| filesProcessed | int64 |  |  |
| malware | object |  |  |
| infectedFiles | int32 |  |  |
| secrets | object |  |  |
| filesWithSecrets | int32 |  |  |
| vulnerabilities6 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| total | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus4 fields | object |  |  |
| scanningState | integer |  |  |
| discoveryState | integer |  |  |
| scanProgress | int32 |  |  |
| uploadProgress | int32 |  |  |

 Response
### Bulk delete jobs (trigger-agnostic)

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| jobIds | array[string] |  |  |

DELETE /api/v1/jobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| deletedJobIds | array[string] |  |  |
| failedJobIds | array[string] |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
### Start a Real-Time Protection job over one or more targets (each target carries its own StorageId)

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| priority | integer |  |  |
| workflowId | string |  |  |
| targets9 fields | array[object] |  |  |
| storageId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| connection | string |  |  |
| organization | string |  |  |
| packageType | string |  |  |
| repositoryType | string |  |  |
| references | array[string] |  |  |

POST /api/v1/jobs/rtpcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jobIds | array[string] |  |  |
| priority | integer |  |  |
| enabledRepositories | array[string] |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

207

Multi-Status

400

Bad Request

 Response
### Create a scheduled job with a recurrence pattern

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| priority | integer |  |  |
| workflowId | string |  |  |
| recurrencePattern5 fields | object |  |  |
| type | integer |  |  |
| hourlyRecurrence | object |  |  |
| everyNumberOfHours | int32 |  |  |
| dailyRecurrence | object |  |  |
| everyNumberOfDays | int32 |  |  |
| weeklyRecurrence | object |  |  |
| daysOfWeek | array[integer] |  |  |
| everyNumberOfWeeks | int32 |  |  |
| monthlyRecurrence | object |  |  |
| everyNumberOfMonths | int32 |  |  |
| dayOfMonth | int32 |  |  |
| targets9 fields | array[object] |  |  |
| storageId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| connection | string |  |  |
| organization | string |  |  |
| packageType | string |  |  |
| repositoryType | string |  |  |
| references | array[string] |  |  |

POST /api/v1/jobs/scheduledcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jobIds | array[string] |  |  |
| priority | integer |  |  |
| nextRunTime | date-time |  |  |
| failedRepositories | array[string] |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

207

Multi-Status

400

Bad Request

 Response
### Delete all upcoming jobs

Auth NoneDELETE /api/v1/jobs/scheduledcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| deletedJobIds | array[string] |  |  |
| failedJobIds | array[string] |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

207

Multi-Status

400

Bad Request

 Response
### Cancel a job (for RealTime jobs this disables RTP)

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

POST /api/v1/jobs/{id}/cancelcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jobId | string |  |  |
| status | string |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

404

Not Found

 Response
### Get a single job by id

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/jobs/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jobId | string |  |  |
| name | string |  |  |
| priority | integer |  |  |
| storage7 fields | object |  |  |
| storageId | string |  |  |
| storageName | string |  |  |
| vendorType | string |  |  |
| protocolType | string |  |  |
| connection | string |  |  |
| packageType | string |  |  |
| organization | string |  |  |
| repository6 fields | object |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryType | string |  |  |
| repositoryUrl | string |  |  |
| repositoryReference | string |  |  |
| repositoryMetadata | string |  |  |
| scanInformation11 fields | object |  |  |
| filesProcessed | int64 |  |  |
| malware | object |  |  |
| infectedFiles | int32 |  |  |
| secrets | object |  |  |
| filesWithSecrets | int32 |  |  |
| vulnerabilities6 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| total | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus4 fields | object |  |  |
| scanningState | integer |  |  |
| discoveryState | integer |  |  |
| scanProgress | int32 |  |  |
| uploadProgress | int32 |  |  |

404

Not Found

 Response
## Manage Licenses

Endpoints[POST/api/v1/licenses/online](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postactivate-a-license-online) [POST/api/v1/licenses/offline](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postactivate-a-license-offline) [DELETE/api/v1/licenses](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deleteremove-licenses) [GET/api/v1/licenses](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-licenses) [GET/api/v1/licenses/current-deployment-id](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-current-deployment-id-for-offline-license-activation)
### Activate a license online

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| key | string |  |  |

POST /api/v1/licenses/onlinecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Activate a license offline

Auth NoneRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| LicenseContent | file |  |  |

POST /api/v1/licenses/offlinecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Remove licenses

Auth NoneDELETE /api/v1/licensescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseMessage | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get licenses

Auth NoneGET /api/v1/licensescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| license8 fields | object |  |  |
| productId | string |  |  |
| productName | string |  |  |
| expiration | int64 |  |  |
| deploymentId | string |  |  |
| currentDeploymentId | string |  |  |
| activationKey | string |  |  |
| licenseContent | string |  |  |
| maxDevelopers | int32 |  |  |
| responseMessage | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get current deployment Id for offline license activation

Auth NoneGET /api/v1/licenses/current-deployment-idcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| currentDeploymentId | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
## Manage Opswat Central Management Ocm

Endpoints[PUT/api/v1/ocm](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-an-ocm-instance) [DELETE/api/v1/ocm](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-an-ocm-instance) [GET/api/v1/ocm](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-an-ocm-instance)
### Update an OCM instance

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| serverApi | string |  |  |
| regCode | string |  |  |

PUT /api/v1/ocmcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Delete an OCM instance

Auth NoneDELETE /api/v1/ocmcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Get an OCM instance

Auth NoneGET /api/v1/ocmcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| ocmInformation29 fields | object |  |  |
| id | string |  |  |
| apiKey | string |  |  |
| serverApi | string |  |  |
| registrationCode | string |  |  |
| deploymentId | string |  |  |
| cmVersion | string |  |  |
| scanConfigurationHash | string |  |  |
| storageConfigurationHash | string |  |  |
| retentionConfigurationHash | string |  |  |
| externalLoggerConfigurationHash | string |  |  |
| userConfigurationHash | string |  |  |
| licenseConfigurationHash | string |  |  |
| smtpConfigurationHash | string |  |  |
| notificationConfigurationHash | string |  |  |
| agentToken | string |  |  |
| instanceId | string |  |  |
| tokenRefreshedAt | int64 |  |  |
| confHash | string |  |  |
| vpackHash | string |  |  |
| heartbeatIntervalSeconds | int32 |  |  |
| fetchConfigIntervalSeconds | int32 |  |  |
| groupId | string |  |  |
| enrollStatus | integer |  |  |
| lastServerConnection | int64 |  |  |
| lastConfigurationSync | int64 |  |  |
| connectionStatus | integer |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Onboarding

Endpoints[GET/api/v1/onboarding](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-onboarding) [POST/api/v1/onboarding/complete](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcomplete-onboarding) [POST/api/v1/onboarding/accept-eula](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postagree-to-onboarding-eula)
### Get onboarding

Auth NoneGET /api/v1/onboardingcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| hasUserConfigured | boolean |  |  |
| hasLicenseConfigured | boolean |  |  |
| hasScanInstanceConfigured | boolean |  |  |
| hasConnectionConfigured | boolean |  |  |
| isCloudType | boolean |  |  |
| isEulaAgreed | boolean |  |  |
| isOnboardingDone | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Complete onboarding

Auth NonePOST /api/v1/onboarding/completecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### Agree to onboarding EULA

Auth NonePOST /api/v1/onboarding/accept-eulacURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
## Manage Packages

Endpoints[GET/api/v1/packages](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-a-paginated-sortable-list-of-packages) [GET/api/v1/packages/versions](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-all-versions-of-a-specific-package-by-its-name-and-) [GET/api/v1/packages/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-a-package-by-its-internal-database-id) [GET/api/v1/packages/by-uid/{uidInB64}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-a-package-by-its-universal-package-uid) [GET/api/v1/packages/{id}/cves](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-cves-associated-with-a-specific-package) [GET/api/v1/packages/{id}/update-instructions](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-the-ecosystem-specific-upgrade-command-for-a-packag) [GET/api/v1/packages/{id}/labels](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieves-all-labels-for-a-specific-package) [POST/api/v1/packages/{id}/labels](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadds-a-label-to-a-package) [PUT/api/v1/packages/{id}/labels/{key}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdates-a-label-in-a-package) [DELETE/api/v1/packages/{id}/labels/{key}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedeletes-a-label-from-a-package) [GET/api/v1/packages/search/labels](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getsearches-for-packages-by-label-key-and-optionally-value)
### Retrieves a paginated, sortable list of packages

Auth NoneQuery String

| Name | string | pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |
| Ecosystem | string | pattern: `^[0-9]*$`  Default: null |  |
| Version | string | pattern: `^[0-9]*$`  Default: null |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Connection | string | pattern: `^[0-9]*$`  Default: null |  |
| Repository | string | pattern: `^[0-9]*$`  Default: null |  |
| Reference | string | pattern: `^[0-9]*$`  Default: null |  |
| ScanId | string | pattern: `^[0-9]*$`  Default: null |  |
| StepSha256 | string | pattern: `^[0-9]*$`  Default: null |  |
| Search | string | pattern: `^[0-9]*$`  Default: null |  |
| IncludeDirectFiles | boolean |  |  |
| sortBy | string | Default: null |  |
| sortDir | string | Default: null |  |
| page | integer | Default: null |  |
| pageSize | integer | Default: null |  |

Expand GET /api/v1/packagescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page | int32 |  |  |
| pageSize | int32 |  |  |
| totalCount | int32 |  |  |
| hasMoreItems | boolean |  |  |
| packages23 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| version | string |  |  |
| ecosystem | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| packageType | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| repositories7 fields | array[object] |  |  |
| connection | string |  |  |
| repository | string |  |  |
| repositoryId | string |  |  |
| reference | string |  |  |
| scanned | date-time |  |  |
| scanIds | array[string] |  |  |
| stepSha256s | array[string] |  |  |
| directFiles3 fields | array[object] |  |  |
| fileName | string |  |  |
| scanned | date-time |  |  |
| scanResultId | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities8 fields | array[object] |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| dependencies6 fields | array[object] |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings | array |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest | object |  |  |
| version | string |  |  |
| releaseDate | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| impact | integer |  |  |
| dependencyImpact | integer |  |  |
| recommendedVersion | string |  |  |

207

Multi-Status

401

Unauthorized

 Response
### Retrieves all versions of a specific package by its name and ecosystem

Auth NoneQuery String

| ecosystem | string |  |  |
| --- | --- | --- | --- |
| packageName | string |  |  |

GET /api/v1/packages/versionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| packageName | string |  |  |
| ecosystem | string |  |  |
| versions6 fields | array[object] |  |  |
| version | string |  |  |
| vulnerabilities8 fields | array[object] |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| dependencies6 fields | array[object] |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings | array |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Retrieves a package by its internal database ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Query String

| includeDirectFiles | boolean | Default: false |  |
| --- | --- | --- | --- |

GET /api/v1/packages/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| package23 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| version | string |  |  |
| ecosystem | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| packageType | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| repositories7 fields | array[object] |  |  |
| connection | string |  |  |
| repository | string |  |  |
| repositoryId | string |  |  |
| reference | string |  |  |
| scanned | date-time |  |  |
| scanIds | array[string] |  |  |
| stepSha256s | array[string] |  |  |
| directFiles3 fields | array[object] |  |  |
| fileName | string |  |  |
| scanned | date-time |  |  |
| scanResultId | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities8 fields | array[object] |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| dependencies6 fields | array[object] |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings | array |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest | object |  |  |
| version | string |  |  |
| releaseDate | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| impact | integer |  |  |
| dependencyImpact | integer |  |  |
| recommendedVersion | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Retrieves a package by its universal package UID

Auth NonePath Params

| uidInB64 | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/packages/by-uid/{uidInB64}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| package23 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| version | string |  |  |
| ecosystem | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| packageType | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| repositories7 fields | array[object] |  |  |
| connection | string |  |  |
| repository | string |  |  |
| repositoryId | string |  |  |
| reference | string |  |  |
| scanned | date-time |  |  |
| scanIds | array[string] |  |  |
| stepSha256s | array[string] |  |  |
| directFiles3 fields | array[object] |  |  |
| fileName | string |  |  |
| scanned | date-time |  |  |
| scanResultId | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities8 fields | array[object] |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| dependencies6 fields | array[object] |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings | array |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest | object |  |  |
| version | string |  |  |
| releaseDate | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| impact | integer |  |  |
| dependencyImpact | integer |  |  |
| recommendedVersion | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Retrieves CVEs associated with a specific package

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/packages/{id}/cvescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| cves8 fields | array[object] |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Retrieves the ecosystem-specific upgrade command for a package

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/packages/{id}/update-instructionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| packageId | string |  |  |
| ecosystem | string |  |  |
| command | string |  |  |
| message | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

401

Unauthorized

404

Not Found

500

Internal Server Error

 Response
### Retrieves all labels for a specific package

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/packages/{id}/labelscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| labels5 fields | array[object] |  |  |
| Key | string |  |  |
| Value | string |  |  |
| ValueType | string |  |  |
| Created | date-time |  |  |
| Updated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Adds a label to a package

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| Key | string |  |  |
| Value | string |  |  |
| ValueType | string |  |  |
| Created | date-time |  |  |
| Updated | date-time |  |  |

POST /api/v1/packages/{id}/labelscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| label5 fields | object |  |  |
| Key | string |  |  |
| Value | string |  |  |
| ValueType | string |  |  |
| Created | date-time |  |  |
| Updated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Updates a label in a package

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |
| key | string |  |  |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| value | string |  |  |
| valueType | string |  |  |

PUT /api/v1/packages/{id}/labels/{key}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Deletes a label from a package

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |
| key | string |  |  |

DELETE /api/v1/packages/{id}/labels/{key}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Searches for packages by label key and optionally value

Auth NoneQuery String

| key | string |  |  |
| --- | --- | --- | --- |
| value | string | Default: null |  |

GET /api/v1/packages/search/labelscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| packages23 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| version | string |  |  |
| ecosystem | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| packageType | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| repositories7 fields | array[object] |  |  |
| connection | string |  |  |
| repository | string |  |  |
| repositoryId | string |  |  |
| reference | string |  |  |
| scanned | date-time |  |  |
| scanIds | array[string] |  |  |
| stepSha256s | array[string] |  |  |
| directFiles3 fields | array[object] |  |  |
| fileName | string |  |  |
| scanned | date-time |  |  |
| scanResultId | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities8 fields | array[object] |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| dependencies6 fields | array[object] |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings | array |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest | object |  |  |
| version | string |  |  |
| releaseDate | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| impact | integer |  |  |
| dependencyImpact | integer |  |  |
| recommendedVersion | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Projects

Endpoints[POST/api/v1/projects](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcreate-a-project) [GET/api/v1/projects](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getlist-projects) [GET/api/v1/projects/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-project-by-id) [PUT/api/v1/projects/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-project) [DELETE/api/v1/projects/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-project) [POST/api/v1/projects/{id}/workflows/attach](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postattach-workflows-to-a-project) [POST/api/v1/projects/{id}/workflows/detach](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postdetach-workflows-from-a-project) [POST/api/v1/projects/{id}/storages/attach](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postattach-connections-services-to-a-project) [POST/api/v1/projects/{id}/storages/detach](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postdetach-connections-services-from-a-project)
### Create a project

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 50 |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |

POST /api/v1/projectscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### List projects

Auth NoneGET /api/v1/projectscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |

 Response
### Get a project by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/projects/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |

404

Not Found

 Response
### Update a project

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 50 |  |

PUT /api/v1/projects/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Delete a project

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/projects/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Attach workflows to a project

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| ids | array[string] |  |  |

POST /api/v1/projects/{id}/workflows/attachcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Detach workflows from a project

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| ids | array[string] |  |  |

POST /api/v1/projects/{id}/workflows/detachcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Attach connections (services) to a project

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| ids | array[string] |  |  |

POST /api/v1/projects/{id}/storages/attachcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Detach connections (services) from a project

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| ids | array[string] |  |  |

POST /api/v1/projects/{id}/storages/detachcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| project4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowIds | array[string] |  |  |
| storageIds | array[string] |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
## Manage Real-time Protection

Endpoints[POST/api/v1/realtime/{storageId}/enable](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postenable-real-time-protection-for-multiple-repositories) [PATCH/api/v1/realtime/{storageId}/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#patchdisable-real-time-protection-for-connection) [PATCH/api/v1/realtime/{storageId}/{repositoryId}/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#patchdisable-real-time-protection-for-repository) [GET/api/v1/realtime](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getlist-connections-with-real-time-protection-enabled) [GET/api/v1/realtime/{storageId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getlist-ongoing-real-time-protection-scans-for-connection) [DELETE/api/v1/realtime/{storageId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-real-time-scan-protection-for-connection) [DELETE/api/v1/realtime/{storageId}/{repositoryId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-real-time-scan-protection-for-repository)
### Enable real-time protection for multiple repositories

Auth NonePath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| repositories | array[object] |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| connection | string |  |  |
| workflowId | string |  |  |

POST /api/v1/realtime/{storageId}/enablecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 207

Multi-Status

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

409

Conflict

 Response
### Disable real-time protection for connection

Auth NonePath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

PATCH /api/v1/realtime/{storageId}/disablecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### Disable real-time protection for repository

Auth NonePath Params

| storageId | string |  |  |
| --- | --- | --- | --- |
| repositoryId | string |  |  |

PATCH /api/v1/realtime/{storageId}/{repositoryId}/disablecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### List connections with real-time protection enabled

Auth NoneGET /api/v1/realtimecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| storages4 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer |  |  |
| protocolType | integer |  |  |
| vendorType | integer |  |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer |  |  |

 Response
### List ongoing real-time protection scans for connection

Auth NonePath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/realtime/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |
| realTimeScans5 fields | array[object] |  |  |
| scanId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| scanningState | integer |  |  |
| workflowId | string |  |  |
| scanInformation7 fields | object |  |  |
| totalFiles | int32 |  |  |
| malware | int32 |  |  |
| secret | int32 |  |  |
| blockedFiles | int32 |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |

 Response
### Delete real-time scan protection for connection

Auth NonePath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Query String

| forceDelete | boolean | Default: false |  |
| --- | --- | --- | --- |

DELETE /api/v1/realtime/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
### Delete real-time scan protection for repository

Auth NonePath Params

| storageId | string |  |  |
| --- | --- | --- | --- |
| repositoryId | string |  |  |

Query String

| forceDelete | boolean | Default: false |  |
| --- | --- | --- | --- |

DELETE /api/v1/realtime/{storageId}/{repositoryId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

 Response
## Manage Scan Configurations

Endpoints[POST/api/v1/scan-configurations](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-scan-configuration) [GET/api/v1/scan-configurations](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-scan-configurations) [PUT/api/v1/scan-configurations/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-scan-configuration) [DELETE/api/v1/scan-configurations/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-scan-configuration) [GET/api/v1/scan-configurations/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-scan-configuration-by-id) [GET/api/v1/scan-configurations/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-scan-configurations-by-scan-pool-id)
### Add a scan configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 50  minLength: 3 |  |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| userAgent | string |  |  |

POST /api/v1/scan-configurationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| type | integer |  |  |
| name | string |  |  |
| scanPool5 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer |  |  |
| isDefault | boolean |  |  |
| scanInstances5 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| userAgent | string |  |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |

400

Bad Request

502

Bad Gateway

 Response
### Get all scan configurations

Auth NoneGET /api/v1/scan-configurationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| Workflows8 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| type | integer |  |  |
| name | string |  |  |
| scanPool5 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer |  |  |
| isDefault | boolean |  |  |
| scanInstances5 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| userAgent | string |  |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Update a scan configuration

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 50  minLength: 3 |  |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| userAgent | string |  |  |

PUT /api/v1/scan-configurations/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Delete a scan configuration

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/scan-configurations/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get a scan configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-configurations/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| Workflow8 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| type | integer |  |  |
| name | string |  |  |
| scanPool5 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer |  |  |
| isDefault | boolean |  |  |
| scanInstances5 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| userAgent | string |  |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get all scan configurations by scan pool ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-configurations/scan-pools/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| Workflows8 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| type | integer |  |  |
| name | string |  |  |
| scanPool5 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer |  |  |
| isDefault | boolean |  |  |
| scanInstances5 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| userAgent | string |  |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
## Manage Scan Instances

Endpoints[POST/api/v1/scan-instances](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-new-scan-instance) [DELETE/api/v1/scan-instances/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-scan-instance) [GET/api/v1/scan-instances/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-scan-instance-by-id) [PUT/api/v1/scan-instances/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-scan-instance)
### Add a new scan instance

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| scanInstanceType | integer |  |  |

POST /api/v1/scan-instancescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanInstanceId | string |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Delete a scan instance

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/scan-instances/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get a scan instance by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-instances/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanInstance5 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Update a scan instance

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |

PUT /api/v1/scan-instances/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
## Manage Scan Pools

Endpoints[POST/api/v1/scan-pools](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-new-scan-pool) [GET/api/v1/scan-pools](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-scan-pools) [DELETE/api/v1/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-scan-pool) [GET/api/v1/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-scan-pool-by-id) [PUT/api/v1/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-an-existing-scan-pool) [GET/api/v1/scan-pools/{id}/rules](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-rules-from-a-scan-pool)
### Add a new scan pool

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| scanPoolType | integer |  |  |

POST /api/v1/scan-poolscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanPoolId | string |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get scan pools

Auth NoneGET /api/v1/scan-poolscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanPools5 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer |  |  |
| isDefault | boolean |  |  |
| scanInstances5 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Delete a scan pool

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/scan-pools/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get a scan pool by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-pools/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanPool5 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer |  |  |
| isDefault | boolean |  |  |
| scanInstances5 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Update an existing scan pool

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |

PUT /api/v1/scan-pools/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get all rules from a scan pool

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-pools/{id}/rulescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| user_agents | array[string] |  |  |

400

Bad Request

 Response
## Manage Scans

Endpoints[POST/api/v1/scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-or-start-a-scan) [GET/api/v1/scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-scan-results) [DELETE/api/v1/scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-multiple-scans-by-their-scan-ids) [POST/api/v1/scans/direct](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postupload-and-scan-a-file-immediately) [POST/api/v1/scans/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#poststop-a-scan) [GET/api/v1/scans/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-scan-results-by-scan-id) [GET/api/v1/scans/latest](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-all-latest-scan-results) [GET/api/v1/scans/{serviceId}/latest](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-all-latest-scan-results-by-service-id) [GET/api/v1/scans/{id}/overview](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-scan-overview-by-scan-id) [GET/api/v1/scans/{serviceId}/{repositoryId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-all-scan-results-by-repository-id) [GET/api/v1/scans/schedules](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-all-scan-schedules) [GET/api/v1/scans/cves](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-all-cves-across-scanned-packages) [POST/api/v1/scans/cleanup](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postclean-up-historical-scan-results-older-than-the-specified-ti) [GET/api/v1/scans/{scanId}/files](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getenumerate-files-by-scan-id) [GET/api/v1/scans/{scanResultId}/core-result](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-the-core-result-of-a-file-by-its-scan-result-id) [GET/api/v1/scans/{scanResultId}/archive](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-the-core-results-of-files-in-an-archive-by-their-scan-res) [GET/api/v1/scans/vulnerability-trends/details](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-per-cve-newfixed-details-for-each-trend-period)
### Add or start a scan

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |
| storageName | string |  |  |
| scanType | integer |  |  |
| workflowId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| protocolType | integer |  |  |
| repositoryReferences | array[string] |  |  |
| organization | string |  |  |
| connection | string |  |  |
| packageType | string |  |  |
| repositoryType | string |  |  |

POST /api/v1/scanscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanIds | array[string] |  |  |
| referencesUsedForScanning | array[string] |  |  |
| protocolType | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| serviceId | string |  |  |
| storageName | string |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| triggerEvent | string |  |  |
| triggerBy | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Enumerate scan results

Auth NoneQuery String

| Type | array |  |  |
| --- | --- | --- | --- |
| TimeFrame | string | pattern: `^[0-9]*$`  Default: null |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string | pattern: `^[0-9]*$`  Default: null |  |
| Connection | string | pattern: `^[0-9]*$`  Default: null |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string | pattern: `^[0-9]*$`  Default: null |  |
| ConnectionType | string | pattern: `^[0-9]*$`  Default: null |  |
| RepositoryId | string | pattern: `^[0-9]*$`  Default: null |  |
| Latest | boolean |  |  |

GET /api/v1/scanscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Delete multiple scans by their scan IDs

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| array | array[string] |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/scanscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

500

Internal Server Error

 Response
### Upload and scan a file immediately

Uploads and scans files immediately. Optional 'jobName' labels the scan; if omitted, a name is generated automatically.

Auth NoneRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| files | array[string] |  |  |
| workflowId | string |  |  |
| metadata | string |  |  |
| jobName | string |  |  |

POST /api/v1/scans/directcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanIds | array[string] |  |  |
| referencesUsedForScanning | array[string] |  |  |
| protocolType | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| serviceId | string |  |  |
| storageName | string |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| triggerEvent | string |  |  |
| triggerBy | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Stop a scan

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

POST /api/v1/scans/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| statusCode | int32 |  |  |

 Response
### Get scan results by scan ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scans/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| serviceId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryType | string |  |  |
| referenceUsedForScanning | string |  |  |
| scanId | string |  |  |
| protocolType | integer |  |  |
| connection | string |  |  |
| packageType | string |  |  |
| organization | string |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| duration | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| scanStatus | integer |  |  |
| discoveryStatus | integer |  |  |
| errors | array[string] |  |  |
| blockedLicensesCount | int32 |  |  |
| infectedFiles | int32 |  |  |
| filesWithSecrets | int32 |  |  |

404

Not Found

 Response
### Enumerate all latest scan results

Auth NoneQuery String

| Type | array |  |  |
| --- | --- | --- | --- |
| TimeFrame | string | pattern: `^[0-9]*$`  Default: null |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string | pattern: `^[0-9]*$`  Default: null |  |
| Connection | string | pattern: `^[0-9]*$`  Default: null |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string | pattern: `^[0-9]*$`  Default: null |  |
| ConnectionType | string | pattern: `^[0-9]*$`  Default: null |  |
| RepositoryId | string | pattern: `^[0-9]*$`  Default: null |  |
| Latest | boolean |  |  |

GET /api/v1/scans/latestcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |
| repository7 fields | object |  |  |
| connectionId | string |  |  |
| connectionName | string |  |  |
| protocolType | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryReference | string |  |  |
| repositoryMetadata | string |  |  |
| scanInformation12 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |
| riskScore | int32 |  |  |
| riskBreakdown4 fields | object |  |  |
| floor | int32 |  |  |
| floorReason | string |  |  |
| extras | object |  |  |
| * | number |  |  |
| finalScore | int32 |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress | int32 |  |  |
| scanProgress | int32 |  |  |
| metadata | string |  |  |
| sbomDocument3 fields | object |  |  |
| authorName | string |  |  |
| authorTool | string |  |  |
| timestamp | string |  |  |

404

Not Found

 Response
### Enumerate all latest scan results by service ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

Query String

| Type | array |  |  |
| --- | --- | --- | --- |
| TimeFrame | string | pattern: `^[0-9]*$`  Default: null |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string | pattern: `^[0-9]*$`  Default: null |  |
| Connection | string | pattern: `^[0-9]*$`  Default: null |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string | pattern: `^[0-9]*$`  Default: null |  |
| ConnectionType | string | pattern: `^[0-9]*$`  Default: null |  |
| RepositoryId | string | pattern: `^[0-9]*$`  Default: null |  |
| Latest | boolean |  |  |

GET /api/v1/scans/{serviceId}/latestcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |
| repository7 fields | object |  |  |
| connectionId | string |  |  |
| connectionName | string |  |  |
| protocolType | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryReference | string |  |  |
| repositoryMetadata | string |  |  |
| scanInformation12 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |
| riskScore | int32 |  |  |
| riskBreakdown4 fields | object |  |  |
| floor | int32 |  |  |
| floorReason | string |  |  |
| extras | object |  |  |
| * | number |  |  |
| finalScore | int32 |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress | int32 |  |  |
| scanProgress | int32 |  |  |
| metadata | string |  |  |
| sbomDocument3 fields | object |  |  |
| authorName | string |  |  |
| authorTool | string |  |  |
| timestamp | string |  |  |

 Response
### Get scan overview by scan ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scans/{id}/overviewcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |
| repository7 fields | object |  |  |
| connectionId | string |  |  |
| connectionName | string |  |  |
| protocolType | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryReference | string |  |  |
| repositoryMetadata | string |  |  |
| scanInformation12 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |
| riskScore | int32 |  |  |
| riskBreakdown4 fields | object |  |  |
| floor | int32 |  |  |
| floorReason | string |  |  |
| extras | object |  |  |
| * | number |  |  |
| finalScore | int32 |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress | int32 |  |  |
| scanProgress | int32 |  |  |
| metadata | string |  |  |
| sbomDocument3 fields | object |  |  |
| authorName | string |  |  |
| authorTool | string |  |  |
| timestamp | string |  |  |

 Response
### Enumerate all scan results by repository ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |
| repositoryId | string |  |  |

GET /api/v1/scans/{serviceId}/{repositoryId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |
| repository7 fields | object |  |  |
| connectionId | string |  |  |
| connectionName | string |  |  |
| protocolType | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryReference | string |  |  |
| repositoryMetadata | string |  |  |
| scanInformation12 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount | int32 |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| package | object |  |  |
| totalPackages | int32 |  |  |
| vulnerablePackages | int32 |  |  |
| riskScore | int32 |  |  |
| riskBreakdown4 fields | object |  |  |
| floor | int32 |  |  |
| floorReason | string |  |  |
| extras | object |  |  |
| * | number |  |  |
| finalScore | int32 |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress | int32 |  |  |
| scanProgress | int32 |  |  |
| metadata | string |  |  |
| sbomDocument3 fields | object |  |  |
| authorName | string |  |  |
| authorTool | string |  |  |
| timestamp | string |  |  |

 Response
### Enumerate all scan schedules

Auth NoneGET /api/v1/scans/schedulescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| workflowId | string |  |  |
| storageId | string |  |  |
| userId | string |  |  |
| name | string |  |  |
| priority | integer |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| lastScanTime | date-time |  |  |
| nextScanTime | date-time |  |  |
| recurrenceType | integer |  |  |
| startDate | date-time |  |  |
| timeToStart | date-time |  |  |
| everyNumberOfHours | int32 |  |  |
| everyNumberOfDays | int32 |  |  |
| everyNumberOfWeeks | int32 |  |  |
| everyNumberOfMonths | int32 |  |  |
| daysOfWeek | array[integer] |  |  |
| dayOfMonth | int32 |  |  |
| workflow14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| userId | string |  |  |
| scanConfigurationId | string |  |  |
| blockedFileDefinition2 fields | object |  |  |
| mode | string |  |  |
| configuration4 fields | object |  |  |
| blockMaliciousContent | boolean |  |  |
| blockSensitiveData | boolean |  |  |
| blockVulnerabilities | boolean |  |  |
| vulnerabilitySeverities | array[string] |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed | object |  |  |
| keep | boolean |  |  |
| softDelete | boolean |  |  |
| blocked | object |  |  |
| keep | boolean |  |  |
| softDelete | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| keep | boolean |  |  |
| copy2 fields | object |  |  |
| serviceConnections6 fields | array[object] |  |  |
| sourceServiceId | string |  |  |
| destinationServiceId | string |  |  |
| sourceRepositoryId | string |  |  |
| destinationRepositoryId | string |  |  |
| sourceRepositoryPackageType | string |  |  |
| destinationRepositoryPackageType | string |  |  |
| isEnabled | boolean |  |  |
| blocked2 fields | object |  |  |
| keep | boolean |  |  |
| copy2 fields | object |  |  |
| serviceConnections6 fields | array[object] |  |  |
| sourceServiceId | string |  |  |
| destinationServiceId | string |  |  |
| sourceRepositoryId | string |  |  |
| destinationRepositoryId | string |  |  |
| sourceRepositoryPackageType | string |  |  |
| destinationRepositoryPackageType | string |  |  |
| isEnabled | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| keep | boolean |  |  |
| copy2 fields | object |  |  |
| serviceConnections6 fields | array[object] |  |  |
| sourceServiceId | string |  |  |
| destinationServiceId | string |  |  |
| sourceRepositoryId | string |  |  |
| destinationRepositoryId | string |  |  |
| sourceRepositoryPackageType | string |  |  |
| destinationRepositoryPackageType | string |  |  |
| isEnabled | boolean |  |  |
| blocked3 fields | object |  |  |
| keep | boolean |  |  |
| copy2 fields | object |  |  |
| serviceConnections6 fields | array[object] |  |  |
| sourceServiceId | string |  |  |
| destinationServiceId | string |  |  |
| sourceRepositoryId | string |  |  |
| destinationRepositoryId | string |  |  |
| sourceRepositoryPackageType | string |  |  |
| destinationRepositoryPackageType | string |  |  |
| isEnabled | boolean |  |  |
| packageDelete | object |  |  |
| isEnabled | boolean |  |  |
| remediations RemediationEmailRemediationRemediationTeamsRemediationRemediationSoftDeleteRemediationRemediationPackageDeleteRemediationRemediationCopyRemediationRemediationJiraRemediationRemediationBase |  |  |  |
| _t | string | Enum: `EmailRemediation` |  |
| emailRecipients | array[string] |  |  |
| isEnabled | boolean |  |  |
| deleted | boolean |  |  |
| crossDomainTransfer3 fields | object |  |  |
| isEnabled | boolean |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| scans33 fields | array[object] |  |  |
| name | string |  |  |
| discoveryState | integer |  |  |
| scanningState | integer |  |  |
| scanType | integer |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| executionId | string |  |  |
| errors | array[string] |  |  |
| priority | integer |  |  |
| realTimeIsEnabled | boolean |  |  |
| realTimeStartDate | date-time |  |  |
| realTimeHandlingType | integer |  |  |
| storageId | string |  |  |
| scanScheduleId | string |  |  |
| userId | string |  |  |
| tenantId | string |  |  |
| scanSchedule | object |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryReference | string |  |  |
| repositoryRevision | string |  |  |
| repositoryType | string |  |  |
| packageType | string |  |  |
| scanTargetPath | string |  |  |
| organization | string |  |  |
| serviceName | string |  |  |
| protocolType | string |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| scanPartition | string |  |  |
| scanStatistics23 fields | object |  |  |
| totalFiles | int32 |  |  |
| infectedFiles | int32 |  |  |
| filesWithSecrets | int32 |  |  |
| totalVulnerabilities | int32 |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| duration | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |
| appliedRemediations | array[string] |  |  |
| totalPackages | int32 |  |  |
| packagesWithVulnerabilities | int32 |  |  |
| allowedLicenses4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usage_restriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blockedLicenses | array |  |  |
| riskScore | int32 |  |  |
| riskBreakdown4 fields | object |  |  |
| floor | int32 |  |  |
| floorReason | string |  |  |
| extras | object |  |  |
| * | number |  |  |
| finalScore | int32 |  |  |
| scan33 fields | object |  |  |
| name | string |  |  |
| discoveryState | integer |  |  |
| scanningState | integer |  |  |
| scanType | integer |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| executionId | string |  |  |
| priority | integer |  |  |
| realTimeIsEnabled | boolean |  |  |
| realTimeStartDate | date-time |  |  |
| realTimeHandlingType | integer |  |  |
| storageId | string |  |  |
| scanScheduleId | string |  |  |
| userId | string |  |  |
| tenantId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| repositoryReference | string |  |  |
| repositoryRevision | string |  |  |
| repositoryType | string |  |  |
| packageType | string |  |  |
| scanTargetPath | string |  |  |
| organization | string |  |  |
| serviceName | string |  |  |
| protocolType | string |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| scanPartition | string |  |  |
| id | string |  |  |
| rowVersion | uint32 |  |  |
| id | string |  |  |
| tenantId | string |  |  |
| id | string |  |  |

 Response
### Enumerate all CVEs across scanned packages

Auth NoneQuery String

| severities | string | Default: null |  |
| --- | --- | --- | --- |
| search | string | Default: null |  |
| page | integer | Default: null |  |
| pageSize | integer | Default: null |  |

GET /api/v1/scans/cvescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page | int32 |  |  |
| pageSize | int32 |  |  |
| totalCount | int32 |  |  |
| hasMoreItems | boolean |  |  |
| cves6 fields | array[object] |  |  |
| cve8 fields | object |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| packageId | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| ecosystem | string |  |  |
| repositories7 fields | array[object] |  |  |
| connection | string |  |  |
| repository | string |  |  |
| repositoryId | string |  |  |
| reference | string |  |  |
| scanned | date-time |  |  |
| scanIds | array[string] |  |  |
| stepSha256s | array[string] |  |  |

400

Bad Request

401

Unauthorized

500

Internal Server Error

 Response
### Clean up historical scan results older than the specified time frame

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| timeFrame | integer |  |  |

POST /api/v1/scans/cleanupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| deletedScansCount | int32 |  |  |
| totalScansFound | int32 |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

207

Multi-Status

400

Bad Request

500

Internal Server Error

 Response
### Enumerate files by scan ID

Auth NonePath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

Query String

| page | integer | Default: null |  |
| --- | --- | --- | --- |
| pageSize | integer | Default: null |  |
| search | string | Default: null |  |
| includeArchives | boolean | Default: null |  |
| includePackages | boolean | Default: null |  |

GET /api/v1/scans/{scanId}/filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| objectIdentityId | string |  |  |
| objectIdentityHash | string |  |  |
| scanResultId | string |  |  |
| progressUpload | int16 |  |  |
| progressScan | int16 |  |  |
| processingState | integer |  |  |
| exceptionDetails | string |  |  |
| created | date-time |  |  |
| discoveryStarted | date-time |  |  |
| discoveryStartedDaySec | int64 |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| processingFailedTime | date-time |  |  |
| processingRetryCount | int16 |  |  |
| objectTriggeredActions | array[object] |  |  |
| actionStatus | integer |  |  |
| triggeredActionType | integer |  |  |
| skippedScan | boolean |  |  |
| hasAppliedRemediation | boolean |  |  |
| hasAppliedSanitization | boolean |  |  |
| hasFailedSanitization | boolean |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| objectRemediationActions12 fields | array[object] |  |  |
| id | string |  |  |
| objectActionType | integer |  |  |
| objectActionState | integer |  |  |
| cdrObjectState | integer |  |  |
| exceptions | array[string] |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| remediationId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| file | object |  |  |
| versions41 fields | array[object] |  |  |
| url | string |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| scanResultId | string |  |  |
| objectIdentityId | string |  |  |
| objectIdentityHash | string |  |  |
| progressScan | int16 |  |  |
| progressUpload | int16 |  |  |
| processingState | integer |  |  |
| exceptionDetails | string |  |  |
| created | date-time |  |  |
| discoveryStarted | date-time |  |  |
| discoveryStartedDaySec | int64 |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| processingFailedTime | date-time |  |  |
| processingRetryCount | int16 |  |  |
| lastUpdated | date-time |  |  |
| createdAt | date-time |  |  |
| tenantId | string |  |  |
| objectIdentity15 fields | object |  |  |
| id | string |  |  |
| storageId | string |  |  |
| lastModifiedTime | date-time |  |  |
| storageObjectHash | string |  |  |
| path | string |  |  |
| processingType | integer |  |  |
| type | integer |  |  |
| objectIdentityHash | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| objectIdentityActions | array[object] |  |  |
| scanResult21 fields | object |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEnginesHash | string |  |  |
| objectIdentityId | string |  |  |
| objectIdentityHash | string |  |  |
| objectIdentity15 fields | object |  |  |
| id | string |  |  |
| storageId | string |  |  |
| lastModifiedTime | date-time |  |  |
| storageObjectHash | string |  |  |
| path | string |  |  |
| processingType | integer |  |  |
| type | integer |  |  |
| objectIdentityHash | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| objectIdentityActions | array[object] |  |  |
| id | string |  |  |
| coreScanResult | string |  |  |
| resultI | integer |  |  |
| scanAllResultI | int16 |  |  |
| totalDetections | int16 |  |  |
| vulnerabilities | int16 |  |  |
| dlpVerdict | int16 |  |  |
| hasVulnerability | boolean |  |  |
| sandboxVerdict | integer |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| file | object |  |  |
| id | string |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| metaDefenderCoreUrl | string |  |  |
| name | string |  |  |
| path | string |  |  |
| hash | string |  |  |
| objectStorageMetadata | string |  |  |
| size | int64 |  |  |
| lastModified | date-time |  |  |
| storageLocation | string |  |  |
| fileTypeCategory | integer |  |  |
| pathForDisplay | string |  |  |
| extension | string |  |  |
| id | string |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| metaDefenderCoreUrl | string |  |  |
| name | string |  |  |
| path | string |  |  |
| hash | string |  |  |
| objectStorageMetadata | string |  |  |
| size | int64 |  |  |
| lastModified | date-time |  |  |
| storageLocation | string |  |  |
| fileTypeCategory | integer |  |  |
| pathForDisplay | string |  |  |
| extension | string |  |  |

Expand 404

Not Found

 Response
### Get the core result of a file by its scan result ID

Auth NonePath Params

| scanResultId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scans/{scanResultId}/core-resultcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| extracted_files5 fields | object |  |  |
| data_id | string |  |  |
| scan_result_i | int32 |  |  |
| detected_by | int32 |  |  |
| files_in_archive11 fields | array[object] |  |  |
| display_name | string |  |  |
| data_id | string |  |  |
| file_type | string |  |  |
| file_type_description | string |  |  |
| scan_result_i | int32 |  |  |
| scan_all_result_i | int32 |  |  |
| detected_by | int32 |  |  |
| scanned_with | int32 |  |  |
| progress_percentage | int32 |  |  |
| file_size | int64 |  |  |
| process_info9 fields | object |  |  |
| post_processing6 fields | object |  |  |
| actions_ran | string |  |  |
| actions_failed | string |  |  |
| converted_to | string |  |  |
| copy_move_destination | string |  |  |
| converted_destination | string |  |  |
| sanitization_details | object |  |  |
| failure_category | string |  |  |
| progress_percentage | int32 |  |  |
| user_agent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blocked_reason | string |  |  |
| file_type_skipped_scan | boolean |  |  |
| processing_time | number |  |  |
| queue_time | number |  |  |
| files_extracted_count | int32 |  |  |
| scan_results8 fields | object |  |  |
| scan_details | object |  |  |
| *6 fields | object |  |  |
| threat_found | string |  |  |
| scan_result_i | int32 |  |  |
| def_time | string |  |  |
| scan_time | number |  |  |
| wait_time | number |  |  |
| eng_id | string |  |  |
| data_id | string |  |  |
| scan_all_result_i | int32 |  |  |
| start_time | string |  |  |
| total_time | number |  |  |
| total_avs | int32 |  |  |
| progress_percentage | int32 |  |  |
| scan_all_result_a | string |  |  |
| file_info13 fields | object |  |  |
| file_size | int64 |  |  |
| upload_timestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| sha512 | string |  |  |
| file_type | string |  |  |
| file_type_category | string |  |  |
| file_type_description | string |  |  |
| file_type_id | string |  |  |
| file_type_extension | string |  |  |
| display_name | string |  |  |
| original_file_path | string |  |  |
| process_info9 fields | object |  |  |
| post_processing6 fields | object |  |  |
| actions_ran | string |  |  |
| actions_failed | string |  |  |
| converted_to | string |  |  |
| copy_move_destination | string |  |  |
| converted_destination | string |  |  |
| sanitization_details | object |  |  |
| failure_category | string |  |  |
| progress_percentage | int32 |  |  |
| user_agent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blocked_reason | string |  |  |
| file_type_skipped_scan | boolean |  |  |
| processing_time | number |  |  |
| queue_time | number |  |  |
| data_id | string |  |  |
| source | string |  |  |
| scanned_on | string |  |  |
| dlp_info3 fields | object |  |  |
| hits | object |  |  |
| *2 fields | object |  |  |
| display_name | string |  |  |
| hits11 fields | array[object] |  |  |
| after | string |  |  |
| before | string |  |  |
| hit | string |  |  |
| certainty | string |  |  |
| certainty_score | int64 |  |  |
| severity | integer |  |  |
| location | string |  |  |
| line | int32 |  |  |
| column | int32 |  |  |
| tryRedact | boolean |  |  |
| redactionStatus | integer |  |  |
| verdict | int64 |  |  |
| category_counts9 fields | object |  |  |
| credit_cards | int32 |  |  |
| social_security_numbers | int32 |  |  |
| government_ids | int32 |  |  |
| ipv4_addresses | int32 |  |  |
| cidr | int32 |  |  |
| adult_content | int32 |  |  |
| personal_identity_documents | int32 |  |  |
| secrets_in_text_files | int32 |  |  |
| custom_regular_expressions | int32 |  |  |
| sbom_info3 fields | object |  |  |
| final_verdict8 fields | object |  |  |
| blocked | boolean |  |  |
| licensing_package_counts4 fields | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| total_package_count | int32 |  |  |
| verdict | string |  |  |
| verdict_explanation | array[string] |  |  |
| vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerable_package_count | int32 |  |  |
| overview_report17 fields | object |  |  |
| is_partial_report | boolean |  |  |
| os_info | object |  |  |
| os_name | string |  |  |
| os_version | string |  |  |
| scan_mode | string |  |  |
| steps14 fields | array[object] |  |  |
| command | string |  |  |
| license_status | string |  |  |
| licensing_package_counts4 fields | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| packages24 fields | array[object] |  |  |
| authors | string |  |  |
| release_date | string |  |  |
| arch | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| structured | boolean |  |  |
| uid | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usage_restriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| os_name | string |  |  |
| os_version | string |  |  |
| package_name | string |  |  |
| latest | object |  |  |
| version | string |  |  |
| release_date | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| file_name | string |  |  |
| package_version | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| source | string |  |  |
| fixed_versions | string |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies7 fields | array[object] |  |  |
| uid | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| package_name | string |  |  |
| package_version | string |  |  |
| vulnerabilities | array |  |  |
| vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| package_type | string |  |  |
| up_to_date | boolean |  |  |
| labels5 fields | array[object] |  |  |
| Key | string |  |  |
| Value | string |  |  |
| ValueType | string |  |  |
| Created | date-time |  |  |
| Updated | date-time |  |  |
| url | string |  |  |
| update_frequency | object |  |  |
| label | string |  |  |
| step | int32 |  |  |
| vulnerability_count | int32 |  |  |
| vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies_vulnerability_count | int32 |  |  |
| dependencies_vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| sha256 | string |  |  |
| package_count | int32 |  |  |
| vulnerable_dependencies_package_count | int32 |  |  |
| vulnerable_package_count | int32 |  |  |
| packages23 fields | array[object] |  |  |
| authors | string |  |  |
| description | string |  |  |
| release_date | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| structured | boolean |  |  |
| uid | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usage_restriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| package_name | string |  |  |
| package_version | string |  |  |
| target | string |  |  |
| latest | object |  |  |
| version | string |  |  |
| release_date | string |  |  |
| hashes | array |  |  |
| vulnerabilities | array |  |  |
| vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies | array |  |  |
| package_type | string |  |  |
| up_to_date | boolean |  |  |
| labels | array |  |  |
| url | string |  |  |
| update_frequency | object |  |  |
| label | string |  |  |
| SBOM | array |  |  |
| dependencies_package_count | int32 |  |  |
| dependencies_vulnerability_count | int32 |  |  |
| dependencies_vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerability_count | int32 |  |  |
| vulnerability_counts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| has_pe_info | boolean |  |  |
| package_count | int32 |  |  |
| timestamp | string |  |  |
| author | object |  |  |
| name | string |  |  |
| tool | string |  |  |
| vulnerable_dependencies_package_count | int32 |  |  |
| vulnerable_package_count | int32 |  |  |
| result_template_hash | string |  |  |
| vulnerability_info1 field | object |  |  |
| result6 fields | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timestamp | string |  |  |
| timing | int64 |  |  |
| detected_product11 fields | object |  |  |
| has_vulnerability | boolean |  |  |
| is_current | boolean |  |  |
| product | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediation_link | string |  |  |
| severity | string |  |  |
| sig_name | string |  |  |
| signature | int64 |  |  |
| vendor | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| version_data3 fields | object |  |  |
| count_behind | int64 |  |  |
| feed_id | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details8 fields | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss9 fields | object |  |  |
| access-complexity | string |  |  |
| access-vector | string |  |  |
| authentication | string |  |  |
| availability-impact | string |  |  |
| confidentiality-impact | string |  |  |
| generated-on-epoch | string |  |  |
| integrity-impact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss_3_013 fields | object |  |  |
| attack_complexity | string |  |  |
| attack_vector | string |  |  |
| availability_impact | string |  |  |
| base_score | string |  |  |
| base_severity | string |  |  |
| confidentiality_impact | string |  |  |
| exploitability_score | string |  |  |
| impact_score | string |  |  |
| integrity_impact | string |  |  |
| privileges_required | string |  |  |
| scope | string |  |  |
| user_interaction | string |  |  |
| vector_string | string |  |  |
| cwe | string |  |  |
| last-modified-epoch | string |  |  |
| published-epoch | string |  |  |
| references | array[string] |  |  |
| severity | string |  |  |
| severity_index | int32 |  |  |
| static_id | int64 |  |  |
| engine_stat | object |  |  |
| *14 fields | array[object] |  |  |
| abandoned | boolean |  |  |
| active | boolean |  |  |
| def_time | string |  |  |
| download_progress | int32 |  |  |
| download_time | date-time |  |  |
| eng_id | string |  |  |
| eng_name | string |  |  |
| eng_type | string |  |  |
| eng_ver | string |  |  |
| engine_type | string |  |  |
| pinned | boolean |  |  |
| state | string |  |  |
| type | string |  |  |
| db_ver | string |  |  |
| sessionCookie | string |  |  |
| isFailed | boolean |  |  |

 Response
### Get the core results of files in an archive by their scan result ID

Auth NonePath Params

| scanResultId | string |  |  |
| --- | --- | --- | --- |

Query String

| count | integer |  |  |
| --- | --- | --- | --- |
| offset | integer |  |  |

GET /api/v1/scans/{scanResultId}/archivecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| coreScanResults13 fields | array[object] |  |  |
| extractedFiles5 fields | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesInArchive11 fields | array[object] |  |  |
| displayName | string |  |  |
| dataId | string |  |  |
| fileType | string |  |  |
| fileTypeDescription | string |  |  |
| scanResultI | int32 |  |  |
| scanAllResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| scannedWith | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileSize | int64 |  |  |
| processInfo9 fields | object |  |  |
| postProcessing6 fields | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails | object |  |  |
| failureCategory | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults8 fields | object |  |  |
| scanDetails | object |  |  |
| *6 fields | object |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| waitTime | number |  |  |
| engId | string |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| progressPercentage | int32 |  |  |
| scanAllResultA | string |  |  |
| fileInfo12 fields | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeCategoryCloud | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| fileTypeExtensionCloud | string |  |  |
| displayName | string |  |  |
| originalFilePath | string |  |  |
| processInfo9 fields | object |  |  |
| postProcessing6 fields | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails | object |  |  |
| failureCategory | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| dataId | string |  |  |
| source | string |  |  |
| scannedOn | string |  |  |
| dlpInfo2 fields | object |  |  |
| hits2 fields | object |  |  |
| displayName | string |  |  |
| hits6 fields | array[object] |  |  |
| after | string |  |  |
| before | string |  |  |
| hit | string |  |  |
| certainty | string |  |  |
| certaintyScore | int64 |  |  |
| severity | integer |  |  |
| verdict | int64 |  |  |
| sbomInfo2 fields | object |  |  |
| finalVerdict3 fields | object |  |  |
| blocked | boolean |  |  |
| severity | integer |  |  |
| verdict | string |  |  |
| overviewReport6 fields | object |  |  |
| steps5 fields | array[object] |  |  |
| command | string |  |  |
| packages16 fields | array[object] |  |  |
| authors | string |  |  |
| arch | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| osName | string |  |  |
| packageType | string |  |  |
| latest | object |  |  |
| version | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| source | string |  |  |
| severity | integer |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss3 fields | object |  |  |
| date | string |  |  |
| percentile | number |  |  |
| score | number |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score | number |  |  |
| severity | string |  |  |
| source | object |  |  |
| name | string |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies3 fields | array[object] |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| upToDate | boolean |  |  |
| step | int32 |  |  |
| sha256 | string |  |  |
| severity | integer |  |  |
| packages15 fields | array[object] |  |  |
| authors | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses2 fields | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction3 fields | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked | array |  |  |
| target | string |  |  |
| packageType | string |  |  |
| latest | object |  |  |
| version | string |  |  |
| hashes | array |  |  |
| vulnerabilities | array |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies | array |  |  |
| upToDate | boolean |  |  |
| vulnerabilityCount | int32 |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| hasPeInfo | boolean |  |  |
| timestamp | string |  |  |
| vulnerabilityInfo1 field | object |  |  |
| vulnerabilityInfoResult6 fields | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct11 fields | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData3 fields | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details8 fields | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss9 fields | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss313 fields | object |  |  |
| attackComplexity | string |  |  |
| attackVector | string |  |  |
| availabilityImpact | string |  |  |
| baseScore | string |  |  |
| baseSeverity | string |  |  |
| confidentialityImpact | string |  |  |
| exploitabilityScore | string |  |  |
| impactScore | string |  |  |
| integrityImpact | string |  |  |
| privilegesRequired | string |  |  |
| scope | string |  |  |
| userInteraction | string |  |  |
| vectorString | string |  |  |
| cwe | string |  |  |
| lastModifiedEpoch | string |  |  |
| publishedEpoch | string |  |  |
| references | array[string] |  |  |
| severity | string |  |  |
| severityIndex | int32 |  |  |
| staticId | int64 |  |  |
| engines | object |  |  |
| *13 fields | array[object] |  |  |
| abandoned | boolean |  |  |
| active | boolean |  |  |
| defTime | string |  |  |
| downloadProgress | int32 |  |  |
| engId | string |  |  |
| engName | string |  |  |
| engType | string |  |  |
| engineVersion | string |  |  |
| engineType | string |  |  |
| pinned | boolean |  |  |
| state | string |  |  |
| type | string |  |  |
| dbVer | string |  |  |
| sessionCookie | string |  |  |
| isFailed | boolean |  |  |
| hasMore | boolean |  |  |

 Response
### Get per-CVE new/fixed details for each trend period

Auth NoneQuery String

| interval | integer | Default: 1 |  |
| --- | --- | --- | --- |
| periods | integer | Default: 4 |  |

GET /api/v1/scans/vulnerability-trends/detailscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| periodStart | date |  |  |
| periodEnd | date |  |  |
| newCves6 fields | array[object] |  |  |
| cveId | string |  |  |
| severity | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| fixedCves | array |  |  |

500

Internal Server Error

 Response
## Manage Services Connections

Endpoints[POST/api/v1/services](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-service) [GET/api/v1/services](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-services) [PUT/api/v1/services/{serviceId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-service-by-id) [GET/api/v1/services/{serviceId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-service-by-id) [DELETE/api/v1/services/{serviceId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-service-by-id) [GET/api/v1/services/{serviceId}/references](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-service-references-by-service-id) [GET/api/v1/services/{serviceId}/resources](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-service-resources-by-service-id) [GET/api/v1/services/{serviceId}/top-risky](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-top-risky-repositories-for-a-service) [GET/api/v1/services/{serviceId}/{repositoryId}/references](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-service-references-by-service-id-and-repository-id) [POST/api/v1/services/references](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-service-references)
### Add a service

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| credentials | string |  |  |
| name | string |  |  |
| vendorType | integer |  |  |
| protocolType | integer |  |  |

POST /api/v1/servicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| type4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer |  |  |
| protocolType | integer |  |  |
| vendorType | integer |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
### Get all services

Auth NoneQuery String

| content | boolean |  |  |
| --- | --- | --- | --- |
| type | array |  |  |

GET /api/v1/servicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| serviceDtos9 fields | array[object] |  |  |
| id | string |  |  |
| credentialsType | int32 |  |  |
| scanWorkflowId | string |  |  |
| domain | string |  |  |
| realTimeStatus | integer |  |  |
| name | string |  |  |
| vendorType | integer |  |  |
| protocolType | integer |  |  |
| statusMessage | string |  |  |

206

Partial Content

400

Bad Request

 Response
### Update a service by ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| credentials | string |  |  |
| hasNewCredentials | boolean |  |  |

PUT /api/v1/services/{serviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| type4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer |  |  |
| protocolType | integer |  |  |
| vendorType | integer |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
### Get a service by ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

Query String

| content | boolean |  |  |
| --- | --- | --- | --- |
| Search | string | Default: null |  |
| Page | integer | Default: null |  |
| PageSize | integer | Default: null |  |
| FilterValue | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| Cursor | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| Search | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| PrioritizedRepositoriesReference | string | Default: null |  |

GET /api/v1/services/{serviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| credentialsType | int32 |  |  |
| scanWorkflowId | string |  |  |
| domain | string |  |  |
| realTimeStatus | integer |  |  |
| name | string |  |  |
| vendorType | integer |  |  |
| protocolType | integer |  |  |

400

Bad Request

404

Not Found

 Response
### Delete a service by ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/services/{serviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

404

Not Found

 Response
### Get service references by service ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/services/{serviceId}/referencescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| serviceId | string |  |  |
| serviceName | string |  |  |
| repositoryReferenceInfoArray3 fields | array[object] |  |  |
| repositoryId | string |  |  |
| defaultReference | string |  |  |
| references | array[string] |  |  |

404

Not Found

 Response
### Get service resources by service ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/services/{serviceId}/resourcescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| resources | array[string] |  |  |

404

Not Found

 Response
### Get top-risky repositories for a service

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

Query String

| count | integer | Default: null |  |
| --- | --- | --- | --- |

GET /api/v1/services/{serviceId}/top-riskycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| connectionId | string |  |  |
| connectionName | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| riskScore | int32 |  |  |

500

Internal Server Error

 Response
### Get service references by service ID and repository ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |
| repositoryId | string |  |  |

Query String

| Page | integer | Default: null |  |
| --- | --- | --- | --- |
| PageSize | integer | Default: null |  |
| FilterValue | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| Cursor | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| Search | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |

GET /api/v1/services/{serviceId}/{repositoryId}/referencescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| references | array[string] |  |  |
| totalReferences | uint32 |  |  |

404

Not Found

 Response
### Add service references

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| array | array[object] |  |  |
| --- | --- | --- | --- |
| serviceId | string |  |  |
| repositoryIds | array[string] |  |  |

POST /api/v1/services/referencescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| serviceId | string |  |  |
| serviceName | string |  |  |
| repositoryReferenceInfoArray3 fields | array[object] |  |  |
| repositoryId | string |  |  |
| defaultReference | string |  |  |
| references | array[string] |  |  |

204

No Content

404

Not Found

 Response
## Manage Settings

Endpoints[POST/api/v1/smtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-smtp-configuration) [PATCH/api/v1/smtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#patchpartially-update-smtp-configuration) [GET/api/v1/smtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-smtp-configuration) [POST/api/v1/jira](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-jira-configuration) [GET/api/v1/jira](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-jira-configurations) [GET/api/v1/jira/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-jira-configuration-by-id) [PUT/api/v1/jira/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-jira-configuration-by-id) [DELETE/api/v1/jira/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-jira-configuration-by-id) [GET/api/v1/jira/{id}/projects](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-jira-projects) [POST/api/v1/teams](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-teams-configuration) [GET/api/v1/teams](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-all-teams-configurations) [GET/api/v1/teams/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-teams-configuration-by-id) [PUT/api/v1/teams/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-teams-configuration-by-id) [DELETE/api/v1/teams/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-teams-configuration-by-id) [GET/api/v1/telemetry](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#gettelemetry) [PUT/api/v1/telemetry/enabled](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putenabled) [PUT/api/v1/telemetry/opswat](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putopswat) [POST/api/v1/telemetry/collectors](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcollectors) [PUT/api/v1/telemetry/collectors](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putcollectors) [DELETE/api/v1/telemetry/collectors](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletecollectors)
### Add a SMTP configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| host | string |  |  |
| baseUrl | string |  |  |
| port | int32 |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| username | string |  |  |
| password | string |  |  |
| secureSocketOption | integer |  |  |
| ignoreCertWarnings | boolean |  |  |
| isEnabled | boolean |  |  |

POST /api/v1/smtpcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Partially update SMTP configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| host | string |  |  |
| baseUrl | string |  |  |
| port | int32 |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| username | string |  |  |
| password | string |  |  |
| secureSocketOption | integer |  |  |
| ignoreCertWarnings | boolean |  |  |
| isEnabled | boolean |  |  |

PATCH /api/v1/smtpcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get a SMTP configuration

Auth NoneGET /api/v1/smtpcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| smtp15 fields | object |  |  |
| id | string |  |  |
| host | string |  |  |
| port | int32 |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| baseUrl | string |  |  |
| userName | string |  |  |
| password | string |  |  |
| secureSocketOption | integer |  |  |
| ignoreCertWarnings | boolean |  |  |
| isEnabled | boolean |  |  |
| tenantId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Add a Jira configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| apiKey | string |  |  |
| baseAddress | string |  |  |
| productAddress | string |  |  |
| username | string |  |  |

POST /api/v1/jiracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get all Jira configurations

Auth NoneGET /api/v1/jiracURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jiraEntries9 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| apiKey | string |  |  |
| baseAddress | string |  |  |
| productAddress | string |  |  |
| username | string |  |  |
| tenantId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get a Jira configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/jira/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jira9 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| apiKey | string |  |  |
| baseAddress | string |  |  |
| productAddress | string |  |  |
| username | string |  |  |
| tenantId | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Update a Jira configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| apiKey | string |  |  |
| baseAddress | string |  |  |
| productAddress | string |  |  |
| username | string |  |  |

PUT /api/v1/jira/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Delete a Jira configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/jira/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jiraId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Get Jira projects

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/jira/{id}/projectscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| projects | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Add a Teams configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| apiKey | string |  |  |
| webhookUrl | string |  |  |
| productAddress | string |  |  |

POST /api/v1/teamscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 201

Created

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get all Teams configurations

Auth NoneGET /api/v1/teamscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| teamsConnections8 fields | array[object] |  |  |
| name | string |  |  |
| apiKey | string |  |  |
| webhookUrl | string |  |  |
| productAddress | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| id | string |  |  |
| tenantId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get a Teams configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/teams/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| teams8 fields | object |  |  |
| name | string |  |  |
| apiKey | string |  |  |
| webhookUrl | string |  |  |
| productAddress | string |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| id | string |  |  |
| tenantId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Update a Teams configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| apiKey | string |  |  |
| webhookUrl | string |  |  |
| productAddress | string |  |  |

PUT /api/v1/teams/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### Delete a Teams configuration by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/teams/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| teamsId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### telemetry

Auth NoneGET /api/v1/telemetrycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| enabled | boolean |  |  |
| sendToOpswatEnabled | boolean |  |  |
| collectors4 fields | array[object] |  |  |
| endpointUrl | string |  |  |
| metricProtocol | string |  |  |
| hasApiKey | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### enabled

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| enabled | boolean |  |  |

PUT /api/v1/telemetry/enabledcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### opswat

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| sendToOpswatEnabled | boolean |  |  |

PUT /api/v1/telemetry/opswatcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### collectors

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| endpointUrl | string |  |  |
| metricProtocol | string |  |  |
| apiKey | string |  |  |

POST /api/v1/telemetry/collectorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### collectors

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| endpointUrl | string |  |  |
| metricProtocol | string |  |  |
| apiKey | string |  |  |

PUT /api/v1/telemetry/collectorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
### collectors

Auth NoneQuery String

| endpointUrl | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/telemetry/collectorscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
## Manage Users

Endpoints[POST/api/v1/users](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postadd-a-new-user) [GET/api/v1/users](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-users) [PUT/api/v1/users](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putupdate-a-user) [GET/api/v1/user](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-current-user) [DELETE/api/v1/users/{userId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-user) [POST/api/v1/user/login](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postlogin-user) [DELETE/api/v1/user/login/{userId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deleteremove-all-tokens-for-an-user) [PUT/api/v1/user/token](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#putget-a-new-access-token) [POST/api/v1/user/password/request-reset](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postrequest-a-password-reset) [POST/api/v1/user/password/new-password](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postreset-a-user-password)
### Add a new user

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| role | integer |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| password | string |  |  |
| email | string |  |  |

POST /api/v1/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| createUserParameters5 fields | object |  |  |
| role | integer |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| password | string |  |  |
| email | string |  |  |
| currentUserId | string |  |  |

400

Bad Request

 Response
### Get users

Auth NoneQuery String

| Type | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |
| StartIndex | integer | Default: null |  |
| Count | integer | Default: null |  |
| SearchTerm | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |

GET /api/v1/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| enumerateUsersDto2 fields | object |  |  |
| entries6 fields | array[object] |  |  |
| userId | string |  |  |
| username | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role | integer |  |  |
| showTutorial | boolean |  |  |
| totalCount | int64 |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Update a user

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| userId | string |  |  |
| role | integer |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| currentPassword | string |  |  |
| newPassword | string |  |  |
| showTutorial | boolean |  |  |

PUT /api/v1/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get current user

Auth NoneGET /api/v1/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| userDto6 fields | object |  |  |
| userId | string |  |  |
| username | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role | integer |  |  |
| showTutorial | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Delete a user

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/users/{userId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Login user

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| username | string |  |  |
| password | string |  |  |

POST /api/v1/user/logincURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jwtToken | object |  |  |
| token | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Remove all tokens for an user

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/user/login/{userId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get a new Access Token

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| accessToken | string |  |  |

PUT /api/v1/user/tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jwtToken | object |  |  |
| token | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Request a password reset

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| emailInput | string |  |  |

POST /api/v1/user/password/request-resetcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Reset a user password

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| newPassword | string | minLength: 12 |  |
| newPasswordConfirmation | string | minLength: 12 |  |
| secureToken | string |  |  |
| userId | string |  |  |

POST /api/v1/user/password/new-passwordcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| user6 fields | object |  |  |
| userId | string |  |  |
| username | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role | integer |  |  |
| showTutorial | boolean |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Versions

Endpoints[GET/api/version](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-application-version) [GET/api/v1/version](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-application-version-2)
### Get application version

Auth NoneQuery String

| api-version | string | maxLength: 256  minLength: 0  pattern: `^[0-9]*$`  Default: null |  |
| --- | --- | --- | --- |

GET /api/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| version | string |  |  |
| lastSupportedConfigVersion | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Get application version

Auth NoneGET /api/v1/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| version | string |  |  |
| lastSupportedConfigVersion | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Webhooks

Endpoints[POST/api/v1/webhook/hmac/{routeParameter}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#posthandles-a-scan-event-triggered-by-a-webhook-requires-a-custo) [POST/api/v1/webhook/{routeParameter}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#posthandles-a-scan-event-triggered-by-a-webhook-requires-a-custo)
### Handles a scan event triggered by a webhook. Requires a custom header and a body.

Auth NonePath Params

| routeParameter | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| No request body |
| --- |

POST /api/v1/webhook/hmac/{routeParameter}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

500

Internal Server Error

 Response
### Handles a scan event triggered by a webhook. Requires a custom body.

Auth NonePath Params

| routeParameter | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| No request body |
| --- |

POST /api/v1/webhook/{routeParameter}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

500

Internal Server Error

 Response
## Manage Workflows

Endpoints[POST/api/v1/workflows](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#postcreate-a-workflow) [GET/api/v1/workflows](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getlist-workflows-paginated) [PATCH/api/v1/workflows/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#patchpartially-update-a-workflow) [GET/api/v1/workflows/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getget-a-workflow-by-id) [DELETE/api/v1/workflows/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#deletedelete-a-workflow-by-id) [GET/api/v1/workflows/{id}/technologies](/docs/supply-chain/metadefender-software-supply-chain-api-4.0.3#getretrieve-metadefender-core-technology-states-for-a-workflow)
### Create a workflow

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| description | string |  |  |
| scanConfigurationId | string |  |  |
| blockedFileDefinition2 fields | object |  |  |
| mode | string |  |  |
| configuration4 fields | object |  |  |
| blockMaliciousContent | boolean |  |  |
| blockSensitiveData | boolean |  |  |
| blockVulnerabilities | boolean |  |  |
| vulnerabilitySeverities | array[string] |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| blocked | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| packageDelete | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| crossDomainTransfer3 fields | object |  |  |
| isEnabled | boolean |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |

POST /api/v1/workflowscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
### List workflows (paginated)

Auth NoneQuery String

| page | integer | Default: 1 |  |
| --- | --- | --- | --- |
| pageSize | integer | Default: 10 |  |
| includeDeleted | boolean | Default: false |  |

GET /api/v1/workflowscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| entries13 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| userId | string |  |  |
| scanConfigurationId | string |  |  |
| deleted | boolean |  |  |
| blockedFileDefinition2 fields | object |  |  |
| mode | string |  |  |
| configuration4 fields | object |  |  |
| blockMaliciousContent | boolean |  |  |
| blockSensitiveData | boolean |  |  |
| blockVulnerabilities | boolean |  |  |
| vulnerabilitySeverities | array[string] |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| blocked | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| packageDelete | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| crossDomainTransfer3 fields | object |  |  |
| isEnabled | boolean |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |
| security | int32 |  |  |
| scanPool | string |  |  |
| totalCount | int64 |  |  |

 Response
### Partially update a workflow

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| description | string |  |  |
| scanConfigurationId | string |  |  |
| blockedFileDefinition2 fields | object |  |  |
| mode | string |  |  |
| configuration4 fields | object |  |  |
| blockMaliciousContent | boolean |  |  |
| blockSensitiveData | boolean |  |  |
| blockVulnerabilities | boolean |  |  |
| vulnerabilitySeverities | array[string] |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| blocked | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| packageDelete | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| crossDomainTransfer3 fields | object |  |  |
| isEnabled | boolean |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |

PATCH /api/v1/workflows/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
### Get a workflow by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/workflows/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| userId | string |  |  |
| scanConfigurationId | string |  |  |
| deleted | boolean |  |  |
| blockedFileDefinition2 fields | object |  |  |
| mode | string |  |  |
| configuration4 fields | object |  |  |
| blockMaliciousContent | boolean |  |  |
| blockSensitiveData | boolean |  |  |
| blockVulnerabilities | boolean |  |  |
| vulnerabilitySeverities | array[string] |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| blocked | object |  |  |
| softDelete | boolean |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| packageDelete | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| keep | boolean |  |  |
| remediations | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| crossDomainTransfer3 fields | object |  |  |
| isEnabled | boolean |  |  |
| maxAllowedSeverity | integer |  |  |
| blockOnSecrets | boolean |  |  |
| security | int32 |  |  |
| scanPool | string |  |  |

 Response
### Delete a workflow by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/workflows/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
### Retrieve MetaDefender Core technology states for a workflow

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/workflows/{id}/technologiescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| sbom | integer |  |  |
| metaScan | integer |  |  |
| dlp | integer |  |  |
| enabledCount | int32 |  |  |

404

Not Found

500

Internal Server Error

 Response
