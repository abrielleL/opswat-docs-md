<!-- source: https://www.opswat.com/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1/ref -->

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
Serverhttp://10.30.160.70:8001Server Variables## Authenticationhttp BearerapiKey ApiKeyFields

| Key | In |
| --- | --- |
| ApiKey | Header |  |

## Monitored Files

Endpoints[POST/api/v1/monitored-files](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postmonitored-files) [GET/api/v1/monitored-files](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getmonitored-files) [GET/api/v1/monitored-files/{id}/history](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#gethistory) [POST/api/v1/monitored-files/{id}/scan-now](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postscan-now) [POST/api/v1/monitored-files/{id}/enabled](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postenabled) [POST/api/v1/monitored-files/{id}/interval](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postinterval) [DELETE/api/v1/monitored-files/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deleteid)
### monitored-files

Auth NoneRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| file | file |  |  |
| workflowId | string |  |  |
| intervalMinutes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| groupId | string |  |  |
| groupName | string |  |  |

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
| rescanIntervalMinutes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| newCveCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| rescanIntervalMinutes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| newCveCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| rescanIntervalMinutes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| newCveCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| rescanIntervalMinutes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| newCveCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| intervalMinutes Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

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
| rescanIntervalMinutes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| newCveCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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

Endpoints[GET/api/v1/abac/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-roles) [POST/api/v1/abac/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcreate-role) [GET/api/v1/abac/roles/{roleId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-role-by-id) [PUT/api/v1/abac/roles/{roleId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-role) [DELETE/api/v1/abac/roles/{roleId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-role) [GET/api/v1/abac/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-permissions) [POST/api/v1/abac/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcreate-permission) [DELETE/api/v1/abac/permissions/{permissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-permission) [POST/api/v1/abac/roles/{roleId}/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postassign-permission-to-role) [DELETE/api/v1/abac/roles/{roleId}/permissions/{permissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deleteremove-permission-from-role) [POST/api/v1/abac/users/{userId}/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postassign-role-to-user) [PUT/api/v1/abac/users/{userId}/roles](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putreplace-user-roles) [DELETE/api/v1/abac/users/{userId}/roles/{roleBindingId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deleteremove-role-from-user) [POST/api/v1/abac/users/{userId}/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postassign-permission-to-user) [DELETE/api/v1/abac/users/{userId}/permissions/{userPermissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deleteremove-permission-from-user)
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
| role Choice 1RoleDto |  |  |  |
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
| role Choice 1RoleDto |  |  |  |
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
| permission Choice 1PermissionDto |  |  |  |
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

Endpoints[GET/api/v1/audit](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-audit-events)
### List audit events

Auth NoneQuery String

| Start | string | pattern: `^[0-9]*$` |  |
| --- | --- | --- | --- |
| Count | string | pattern: `^[0-9]*$` |  |
| LogType | array |  |  |
| CategoryType | integer |  |  |
| LogLevel | integer |  |  |
| Search | string |  |  |

GET /api/v1/auditcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| entries4 fields | array[object] | Because it belongs to a response, if RetrieveLogs breaks, we won't have Entries and TotalCount. |  |
| id | string |  |  |
| level | integer |  |  |
| properties5 fields | object |  |  |
| logType | integer |  |  |
| category | integer |  |  |
| eventTimestamp | date-time |  |  |
| userId | string |  |  |
| userName | string |  |  |
| renderedMessage | string |  |  |
| totalCount Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

 Response
## Manage Password Encryption

Endpoints[GET/api/v1/auth/public-key](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-public-key-used-to-encrypt-passwords)
### Get the public key used to encrypt passwords

Auth NoneGET /api/v1/auth/public-keycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| mode | integer |  |  |
| serverTime Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| keys6 fields | array[object] |  |  |
| kty | string |  |  |
| kid | string |  |  |
| use | string |  |  |
| alg | string |  |  |
| n | string |  |  |
| e | string |  |  |

 Response
## Manage Configuration

Endpoints[GET/api/v1](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-application-configuration)
### Get application configuration

Auth NoneGET /api/v1cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Cross Domain Transfers

Endpoints[POST/api/v1/cross-domain/file-stream](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postreceive-a-full-file-as-a-single-framed-binary-stream-with-ma) [GET/api/v1/cross-domain/global-config](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-global-cross-domain-configuration-for-both-sides) [PUT/api/v1/cross-domain/global-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putset-global-lowside-configuration) [POST/api/v1/cross-domain/global-config/lowside/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postdisable-global-lowside-configuration) [PUT/api/v1/cross-domain/global-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putset-global-highside-configuration) [POST/api/v1/cross-domain/global-config/highside/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postdisable-global-highside-configuration) [POST/api/v1/cross-domain/global-config/highside/pairing-secret](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postgenerate-a-pairing-secret-for-the-global-highside-configurat) [GET/api/v1/cross-domain/logs](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-cross-domain-operation-logs) [DELETE/api/v1/cross-domain/logs/{transmissionId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-cross-domain-activity-log-entry-by-transmission-i) [POST/api/v1/cross-domain/lowside-configuration-notifications](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postreceive-a-lowside-configuration-change-notification) [GET/api/v1/cross-domain/notifications](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-cross-domain-notifications) [GET/api/v1/cross-domain/storage-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-lowside-configuration-by-storage-id) [POST/api/v1/cross-domain/storage-config/lowside](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-lowside-configuration) [PUT/api/v1/cross-domain/storage-config/lowside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-lowside-configuration-by-id) [DELETE/api/v1/cross-domain/storage-config/lowside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-lowside-configuration-by-id) [GET/api/v1/cross-domain/storage-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-highside-storage-configuration-by-storage-id) [POST/api/v1/cross-domain/storage-config/highside](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-highside-configuration) [PUT/api/v1/cross-domain/storage-config/highside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-highside-configuration-by-id) [DELETE/api/v1/cross-domain/storage-config/highside/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-highside-configuration-by-id)
### Receive a full file as a single framed binary stream with manifest in headers

Auth NoneHeaders

| receiveFileStreamDto11 fields | object |  |  |
| --- | --- | --- | --- |
| transmissionId | string |  |  |
| fileName | string |  |  |
| fileSizeBytes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalChunks Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| chunkSizeBytes Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| storageName | string |  |  |
| repositoryName | string |  |  |
| reference | string |  |  |
| organization | string |  |  |
| transferTimestamp Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| transferSignature | string |  |  |

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
### Get the global cross-domain configuration for both sides

Auth NoneGET /api/v1/cross-domain/global-configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| lowside Choice 1GetGlobalLowsideConfigurationDto |  |  |  |
| highside Choice 1GlobalHighsideConfigurationDto |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Set global lowside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| highsideAddress | string |  |  |
| authorizationToken | string |  |  |
| pairingSecret | string |  |  |
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
### Set global highside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| pushBehaviour | integer |  |  |
| enabled | boolean |  |  |
| scanTimeoutSeconds Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pollIntervalSeconds Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasPairingSecret | boolean |  |  |
| pairingSecretIssuedAt | date-time |  |  |

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
### Generate a pairing secret for the global highside configuration

Auth NonePOST /api/v1/cross-domain/global-config/highside/pairing-secretcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| pairingSecret Choice 1PairingSecretDto |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

404

Not Found

 Response
### Get cross-domain operation logs

Auth NoneQuery String

| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| --- | --- | --- | --- |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| sortBy | string |  |  |
| sortOrder | integer |  |  |
| filter | string |  |  |
| search | string |  |  |

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
| storage Choice 1GetServiceDto |  |  |  |
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

Auth NoneHeaders

| X-Transfer-Timestamp |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| --- | --- | --- | --- |
| X-Transfer-Signature | string |  |  |

Request Body application/*+jsonapplication/jsontext/json

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
| configurations8 fields | array[object] |  |  |
| id | string |  |  |
| storageId | string |  |  |
| storageName | string |  |  |
| lowsideStorageName | string |  |  |
| lowsideProtocolType | integer |  |  |
| valid | boolean |  |  |
| scanBeforeImport | boolean |  |  |
| scanWorkflowId | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Add a highside configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string |  |  |
| notificationId | string |  |  |
| scanBeforeImport | boolean |  |  |
| scanWorkflowId | string |  |  |

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
| scanBeforeImport | boolean |  |  |
| scanWorkflowId | string |  |  |

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
## Crypto Assets

Endpoints[GET/api/v1/crypto-assets](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlists-the-crypto-assets-one-entry-per-asset-type-and-identity) [GET/api/v1/crypto-assets/summary](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getcounts-the-crypto-assets-by-nist-level-classical-risk-and-ass) [GET/api/v1/crypto-assets/{assetType}/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlists-the-jobs-that-report-one-crypto-asset-newest-first-put-) [GET/api/v1/crypto-assets/{assetType}/files](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlists-the-files-that-report-one-crypto-asset-by-path-put-the-) [GET/api/v1/crypto-assets/{assetType}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getreads-one-crypto-asset-the-same-entry-the-list-returns-put-th)
### Lists the crypto assets, one entry per asset type and identity. ScanId scopes the result to one job; without it the result covers every job. Pass IdentityKey as key to the detail, jobs and files endpoints. QuantumLevels filters on 0 to 6, unknown and not-applicable. Another level value returns 400. An unknown ScanId returns an empty page.

Auth NoneQuery String

| ScanId | string |  |  |
| --- | --- | --- | --- |
| Search | string |  |  |
| QuantumLevels | array |  |  |
| AssetTypes | array |  |  |
| ClassicalRisks | array |  |  |
| sortBy | integer |  |  |
| sortDir | integer |  |  |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/crypto-assetscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| items18 fields | array[object] |  |  |
| bomRef | string |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| quantumLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isInherited | boolean |  |  |
| classicalRisk | string |  |  |
| quantumRisk | string |  |  |
| overallRisk | string |  |  |
| classicalSecurityLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isPqc | boolean |  |  |
| recommendedReplacements3 fields | array[object] |  |  |
| algorithm | string |  |  |
| appliesTo | string |  |  |
| nistStandard | string |  |  |
| inheritedFrom3 fields | array[object] |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| description | string |  |  |
| quantumRationale | string |  |  |
| evidences | array[object] |  |  |
| line Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| match | string |  |  |
| fileCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| jobCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

401

Unauthorized

 Response
### Counts the crypto assets by NIST level, classical risk and asset type. ScanId scopes the result to one job; without it the result covers every job. An asset is not quantum safe when Core does not mark it quantum-safe. WorstFiles lists the top 5 files by not quantum safe assets. Without ScanId, WorstFiles uses only the newest completed job of each repository and reference. An unknown ScanId returns every count at 0.

Auth NoneQuery String

| ScanId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/crypto-assets/summarycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| totalFiles Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| filesWithNotQuantumSafeAssets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalAssets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| quantumLevels8 fields | object |  |  |
| level0 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level1 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level2 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level3 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level4 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level5 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level6 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| classicalRisks | object |  |  |
| assetTypes | object |  |  |
| worstFiles4 fields | array[object] |  |  |
| scanId | string |  |  |
| scanResultId | string |  |  |
| path | string |  |  |
| notQuantumSafeCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

401

Unauthorized

 Response
### Lists the jobs that report one crypto asset, newest first. Put the list entry AssetType in the path and its IdentityKey in key. A missing key returns 400. ScanId scopes the result to one job; without it the result covers every job. An unknown key or ScanId returns an empty page.

Auth NonePath Params

| assetType | string |  |  |
| --- | --- | --- | --- |

Query String

| key | string |  |  |
| --- | --- | --- | --- |
| ScanId | string |  |  |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/crypto-assets/{assetType}/jobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| items4 fields | array[object] |  |  |
| jobId | string |  |  |
| name | string |  |  |
| scannedOn | date-time |  |  |
| fileCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

401

Unauthorized

 Response
### Lists the files that report one crypto asset, by path. Put the list entry AssetType in the path and its IdentityKey in key. A missing key returns 400. ScanId scopes the result to one job; without it the result covers every job. An asset inside an archive counts against the archive. An unknown key or ScanId returns an empty page.

Auth NonePath Params

| assetType | string |  |  |
| --- | --- | --- | --- |

Query String

| key | string |  |  |
| --- | --- | --- | --- |
| ScanId | string |  |  |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/crypto-assets/{assetType}/filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| items4 fields | array[object] |  |  |
| scanId | string |  |  |
| scanResultId | string |  |  |
| path | string |  |  |
| quantumLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

401

Unauthorized

 Response
### Reads one crypto asset, the same entry the list returns. Put the list entry AssetType in the path and its IdentityKey in key. A missing key returns 400. ScanId scopes the result to one job; without it the result covers every job. An unknown key or ScanId returns 404.

Auth NonePath Params

| assetType | string |  |  |
| --- | --- | --- | --- |

Query String

| key | string |  |  |
| --- | --- | --- | --- |
| ScanId | string |  |  |

GET /api/v1/crypto-assets/{assetType}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| bomRef | string |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| quantumLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isInherited | boolean |  |  |
| classicalRisk | string |  |  |
| quantumRisk | string |  |  |
| overallRisk | string |  |  |
| classicalSecurityLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isPqc | boolean |  |  |
| recommendedReplacements3 fields | array[object] |  |  |
| algorithm | string |  |  |
| appliesTo | string |  |  |
| nistStandard | string |  |  |
| inheritedFrom3 fields | array[object] |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| description | string |  |  |
| quantumRationale | string |  |  |
| evidences | array[object] |  |  |
| line Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| match | string |  |  |
| fileCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| jobCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

Expand 400

Bad Request

401

Unauthorized

404

Not Found

 Response
## Manage Dashboard

Endpoints[GET/api/v1/dashboard](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-dashboard-summary-and-trends-time-series) [GET/api/v1/dashboard/top-risky](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-top-risky-repositories-across-all-connections)
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
| totalConnections Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalScannedRepositories Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalScannedRepositoriesTrend Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalPackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalPackagesTrend Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| riskScoreTrend Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| criticalVulnerabilities Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| criticalPackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| criticalRepositories Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalVulnerabilities Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalVulnerabilitiesTrend Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalThreats Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalThreatsTrend Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalSecrets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalSecretsTrend Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| severity5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| topRiskyPackages | array[object] |  |  |
| name | string |  |  |
| criticalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| topRiskyRepositories | array[object] |  |  |
| name | string |  |  |
| detectionCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| trends9 fields | array[object] |  |  |
| periodStart | date-time |  |  |
| periodEnd | date-time |  |  |
| totalVulnerabilities Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scansConsidered Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

500

Internal Server Error

 Response
### Get top-risky repositories across all connections

Auth NoneQuery String

| window | string |  |  |
| --- | --- | --- | --- |
| count |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/dashboard/top-riskycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| connectionId | string |  |  |
| connectionName | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

500

Internal Server Error

 Response
## Manage Export

Endpoints[GET/api/v1/export/cyclonedx/{repoId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-cyclonedx-report-for-repository) [GET/api/v1/export/cyclonedx/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-cyclonedx-report-for-a-specific-file-scan) [GET/api/v1/export/spdx/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-an-spdx-report-for-a-specific-scan) [GET/api/v1/export/spdx/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-an-spdx-report-for-a-specific-file-scan) [GET/api/v1/export/pdf/all-scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-pdf-report-for-all-scans) [GET/api/v1/export/pdf/overview/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-pdf-overview-report-for-repository) [GET/api/v1/export/pdf/sbom/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-pdf-sbom-report-for-repository) [GET/api/v1/export/pdf/sbom/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-pdf-sbom-report-for-a-specific-batch-of-files) [GET/api/v1/export/pdf/sbom/dependencies/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-pdf-sbom-report-for-repository-that-lists-every-pack) [GET/api/v1/export/csv/sbom/{scanId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-csv-report-for-repository) [GET/api/v1/export/csv/sbom/file/{fileId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-csv-report-for-a-specific-batch-of-files) [GET/api/v1/export/csv/cves](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-csv-report-of-all-cves-from-latest-scans) [GET/api/v1/export/csv/packages](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getexport-a-csv-report-of-all-packages-from-latest-scans)
### Export a CycloneDX report for repository

Auth NonePath Params

| repoId | string |  |  |
| --- | --- | --- | --- |

Query String

| Reference | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/export/cyclonedx/{repoId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

404

Not Found

 Response
### Export a PDF report for all scans

Auth NoneQuery String

| Type | array |  |  |
| --- | --- | --- | --- |
| TimeFrame | integer |  |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string |  |  |
| Connection | string |  |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string |  |  |
| ConnectionType | integer |  |  |
| RepositoryId | string |  |  |
| Latest | boolean |  |  |

GET /api/v1/export/pdf/all-scanscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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

GET /api/v1/export/pdf/overview/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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

GET /api/v1/export/pdf/sbom/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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

GET /api/v1/export/pdf/sbom/file/{fileId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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

GET /api/v1/export/pdf/sbom/dependencies/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileStream | file |  |  |
| contentType | string |  |  |
| fileDownloadName | string |  |  |
| lastModified | date-time |  |  |
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
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
| entityTag Choice 1EntityTagHeaderValue |  |  |  |
| enableRangeProcessing | boolean |  |  |

400

Bad Request

 Response
## Manage External Loggers

Endpoints[GET/api/v1/externallogger](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-external-loggers) [POST/api/v1/externallogger](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-an-external-logger) [PUT/api/v1/externallogger/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-an-external-logger) [DELETE/api/v1/externallogger/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-an-external-logger)
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
| port Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| port Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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

Endpoints[GET/api/v1/global-label-keys](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getreturns-all-global-label-keys) [POST/api/v1/global-label-keys](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadds-a-new-global-label-key) [PUT/api/v1/global-label-keys/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdates-an-global-label-key) [DELETE/api/v1/global-label-keys/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedeletes-an-global-label-key)
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
| globalKey Choice 1GlobalLabelKey |  |  |  |
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
| globalKey Choice 1GlobalLabelKey |  |  |  |
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

Endpoints[POST/api/v1/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#poststart-a-scan-now-job-over-one-or-more-targets-each-target-ca) [GET/api/v1/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-jobs-paginated-queryable-by-trigger-type) [DELETE/api/v1/jobs](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletebulk-delete-jobs-trigger-agnostic) [POST/api/v1/jobs/rtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#poststart-a-real-time-protection-job-over-one-or-more-targets-ea) [POST/api/v1/jobs/scheduled](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcreate-a-scheduled-job-with-a-recurrence-pattern) [DELETE/api/v1/jobs/scheduled](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-all-upcoming-jobs) [POST/api/v1/jobs/{id}/cancel](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcancel-a-job-for-realtime-jobs-this-disables-rtp) [GET/api/v1/jobs/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-single-job-by-id)
### Start a Scan Now job over one or more targets (each target carries its own StorageId, so a single job may mix protocols)

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| priority Choice 1MessagePriority |  |  |  |
| workflowId | string |  |  |
| referenceSelectionMode Choice 1ReferenceSelectionMode |  |  |  |
| targets4 fields | array[object] |  |  |
| protocolType | integer |  |  |
| storageId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |

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
| Search | string |  |  |
| TimeFrame | integer |  |  |
| Type | array |  |  |
| ConnectionType | integer |  |  |
| Repository | string |  |  |
| Service | string |  |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| QuantumVerdict | array | Enum: `Safe`,`Unsafe`,`Unknown`,`None` |  |
| Threats | boolean |  |  |
| Secrets | boolean |  |  |
| SortBy | string |  |  |
| SortDir | string |  |  |
| Page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| PageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/jobscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| jobs10 fields | array[object] |  |  |
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
| scanInformation Choice 1JobScanInformationDto |  |  |  |
| scanStatus Choice 1JobScanStatusDto |  |  |  |
| importVerdict | string |  |  |

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
| priority Choice 1MessagePriority |  |  |  |
| workflowId | string |  |  |
| targets4 fields | array[object] |  |  |
| protocolType | integer |  |  |
| storageId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |

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
| priority Choice 1MessagePriority |  |  |  |
| workflowId | string |  |  |
| referenceSelectionMode Choice 1ReferenceSelectionMode |  |  |  |
| recurrencePattern5 fields | object |  |  |
| type | integer |  |  |
| hourlyRecurrence Choice 1HourlyRecurrenceDto |  |  |  |
| dailyRecurrence Choice 1DailyRecurrenceDto |  |  |  |
| weeklyRecurrence Choice 1WeeklyRecurrenceDto |  |  |  |
| monthlyRecurrence Choice 1MonthlyRecurrenceDto |  |  |  |
| targets4 fields | array[object] |  |  |
| protocolType | integer |  |  |
| storageId | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |

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
| scanInformation Choice 1JobScanInformationDto |  |  |  |
| scanStatus Choice 1JobScanStatusDto |  |  |  |
| importVerdict | string |  |  |

404

Not Found

 Response
## Manage Licenses

Endpoints[POST/api/v1/licenses/online](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postactivate-a-license-online) [POST/api/v1/licenses/offline](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postactivate-a-license-offline) [DELETE/api/v1/licenses](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deleteremove-licenses) [GET/api/v1/licenses](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-licenses) [GET/api/v1/licenses/current-deployment-id](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-current-deployment-id-for-offline-license-activation)
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
| license Choice 1LicenseDto |  |  |  |
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

Endpoints[PUT/api/v1/ocm](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-an-ocm-instance) [DELETE/api/v1/ocm](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-an-ocm-instance) [GET/api/v1/ocm](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-an-ocm-instance)
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
| ocmInformation Choice 1OcmInformation |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Onboarding

Endpoints[GET/api/v1/onboarding](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-onboarding) [POST/api/v1/onboarding/complete](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcomplete-onboarding) [POST/api/v1/onboarding/accept-eula](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postagree-to-onboarding-eula)
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

Endpoints[GET/api/v1/packages](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-a-paginated-sortable-list-of-packages) [GET/api/v1/packages/versions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-all-versions-of-a-specific-package-by-its-name-and-) [GET/api/v1/packages/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-a-package-by-its-internal-database-id) [GET/api/v1/packages/by-uid/{uidInB64}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-a-package-by-its-universal-package-uid) [GET/api/v1/packages/{id}/cves](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-cves-associated-with-a-specific-package) [GET/api/v1/packages/{id}/update-instructions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-the-ecosystem-specific-upgrade-command-for-a-packag) [GET/api/v1/packages/{id}/labels](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieves-all-labels-for-a-specific-package) [POST/api/v1/packages/{id}/labels](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadds-a-label-to-a-package) [PUT/api/v1/packages/{id}/labels/{key}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdates-a-label-in-a-package) [DELETE/api/v1/packages/{id}/labels/{key}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedeletes-a-label-from-a-package) [GET/api/v1/packages/search/labels](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getsearches-for-packages-by-label-key-and-optionally-value)
### Retrieves a paginated, sortable list of packages

Auth NoneQuery String

| Name | string |  |  |
| --- | --- | --- | --- |
| Ecosystem | string |  |  |
| Version | string |  |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Connection | string |  |  |
| Repository | string |  |  |
| Reference | string |  |  |
| ScanId | string |  |  |
| StepSha256 | string |  |  |
| Search | string |  |  |
| IncludeDirectFiles | boolean |  |  |
| sortBy | integer |  |  |
| sortDir | integer |  |  |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/packagescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| licenses Choice 1LicensesDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest Choice 1LatestPackageInfoDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| licenses Choice 1LicensesDto |  |  |  |
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
| package Choice 1PackageDto |  |  |  |
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
| package Choice 1PackageDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
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
| label Choice 1PackageLabel |  |  |  |
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
| value | string |  |  |

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
| licenses Choice 1LicensesDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| supplierName | string |  |  |
| releaseDate | date-time |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest Choice 1LatestPackageInfoDto |  |  |  |
| createdAt | date-time |  |  |
| lastUpdated | date-time |  |  |
| impact | integer |  |  |
| dependencyImpact | integer |  |  |
| recommendedVersion | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Projects

Endpoints[POST/api/v1/projects](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcreate-a-project) [GET/api/v1/projects](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-projects) [GET/api/v1/projects/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-project-by-id) [PUT/api/v1/projects/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-project) [DELETE/api/v1/projects/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-project) [POST/api/v1/projects/{id}/workflows/attach](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postattach-workflows-to-a-project) [POST/api/v1/projects/{id}/workflows/detach](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postdetach-workflows-from-a-project) [POST/api/v1/projects/{id}/storages/attach](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postattach-connections-services-to-a-project) [POST/api/v1/projects/{id}/storages/detach](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postdetach-connections-services-from-a-project)
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
| project Choice 1ProjectDto |  |  |  |
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
| project Choice 1ProjectDto |  |  |  |
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
| project Choice 1ProjectDto |  |  |  |
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
| project Choice 1ProjectDto |  |  |  |
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
| project Choice 1ProjectDto |  |  |  |
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
| project Choice 1ProjectDto |  |  |  |
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
| project Choice 1ProjectDto |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

404

Not Found

 Response
## Manage Real-time Protection

Endpoints[POST/api/v1/realtime/{storageId}/enable](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postenable-real-time-protection-for-multiple-repositories) [PATCH/api/v1/realtime/{storageId}/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#patchdisable-real-time-protection-for-connection) [PATCH/api/v1/realtime/{storageId}/{repositoryId}/disable](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#patchdisable-real-time-protection-for-repository) [GET/api/v1/realtime](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-connections-with-real-time-protection-enabled) [GET/api/v1/realtime/{storageId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-ongoing-real-time-protection-scans-for-connection) [DELETE/api/v1/realtime/{storageId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-real-time-scan-protection-for-connection) [DELETE/api/v1/realtime/{storageId}/{repositoryId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-real-time-scan-protection-for-repository)
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
| scanInformation Choice 1RealTimeScanInformationDto |  |  |  |

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

Endpoints[POST/api/v1/scan-configurations](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-scan-configuration) [GET/api/v1/scan-configurations](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-scan-configurations) [PUT/api/v1/scan-configurations/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-scan-configuration) [DELETE/api/v1/scan-configurations/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-scan-configuration) [GET/api/v1/scan-configurations/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-scan-configuration-by-id) [GET/api/v1/scan-configurations/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-scan-configurations-by-scan-pool-id)
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
| minimumSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| maximumSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| Workflows8 fields | array[object] | Because it belongs to a response, if GetMultipleScanConfiguration breaks, we won't have ScanConfigurations. |  |
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
| minimumSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| maximumSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| Workflow Choice 1ScanConfigurationDto |  |  |  |
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
| Workflows8 fields | array[object] | Because it belongs to a response, if GetMultipleScanConfiguration breaks, we won't have ScanConfigurations. |  |
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
| minimumSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| maximumSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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

Endpoints[POST/api/v1/scan-instances](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-new-scan-instance) [DELETE/api/v1/scan-instances/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-scan-instance) [GET/api/v1/scan-instances/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-scan-instance-by-id) [PUT/api/v1/scan-instances/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-scan-instance)
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

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
### Delete a scan instance

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/scan-instances/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
### Get a scan instance by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-instances/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^-?(\d+\.)?\d{2}:\d{2}:\d{2}(\.\d{1,7})?$` |  |

400

Bad Request

404

Not Found

500

Internal Server Error

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

| No response body |
| --- |

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
## Manage Scan Pools

Endpoints[POST/api/v1/scan-pools](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-new-scan-pool) [GET/api/v1/scan-pools](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-scan-pools) [DELETE/api/v1/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-scan-pool) [GET/api/v1/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-scan-pool-by-id) [PUT/api/v1/scan-pools/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-an-existing-scan-pool) [GET/api/v1/scan-pools/{id}/rules](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-rules-from-a-scan-pool)
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

| No response body |
| --- |

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
### Get a scan pool by ID

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scan-pools/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| scanPool Choice 1ScanPoolDto |  |  |  |
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

Endpoints[POST/api/v1/scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-or-start-a-scan) [GET/api/v1/scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-scan-results) [DELETE/api/v1/scans](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-multiple-scans-by-their-scan-ids) [POST/api/v1/scans/direct](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postupload-and-scan-a-file-immediately) [POST/api/v1/scans/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#poststop-a-scan) [GET/api/v1/scans/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-scan-results-by-scan-id) [GET/api/v1/scans/latest](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-all-latest-scan-results) [GET/api/v1/scans/{serviceId}/latest](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-all-latest-scan-results-by-service-id) [GET/api/v1/scans/{id}/overview](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-scan-overview-by-scan-id) [GET/api/v1/scans/{serviceId}/{repositoryId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-all-scan-results-by-repository-id) [GET/api/v1/scans/schedules](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-all-scan-schedules) [GET/api/v1/scans/cves](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-all-cves-across-scanned-packages) [POST/api/v1/scans/cleanup](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postclean-up-historical-scan-results-older-than-the-specified-ti) [GET/api/v1/scans/{scanId}/files](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getenumerate-files-by-scan-id) [GET/api/v1/scans/{scanResultId}/details](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-file-details-view-of-a-file-by-its-scan-result-id) [GET/api/v1/scans/{scanResultId}/children](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-archive-entries-of-a-file-by-its-scan-result-id) [GET/api/v1/scans/{scanResultId}/dependencies](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-dependencies-of-a-file-and-its-archive-entries-by-its) [GET/api/v1/scans/{scanResultId}/archive/{childDataId}/dependencies](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-dependencies-of-one-archive-entry-including-nested-en) [GET/api/v1/scans/vulnerability-trends/details](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-per-cve-newfixed-details-for-each-trend-period)
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
| protocolType Choice 1ProtocolType |  |  |  |
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
| protocolType Choice 1ProtocolType |  |  |  |
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
| TimeFrame | integer |  |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string |  |  |
| Connection | string |  |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string |  |  |
| ConnectionType | integer |  |  |
| RepositoryId | string |  |  |
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

| object | object |  |  |
| --- | --- | --- | --- |
| notFoundScanIds | array[string] |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

207

Multi-Status

400

Bad Request

404

Not Found

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
| protocolType Choice 1ProtocolType |  |  |  |
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
| statusCode Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

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
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanStatus | integer |  |  |
| discoveryStatus | integer |  |  |
| errors | array[string] |  |  |
| blockedLicensesCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| infectedFiles Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| filesWithSecrets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

404

Not Found

 Response
### Enumerate all latest scan results

Auth NoneQuery String

| Type | array |  |  |
| --- | --- | --- | --- |
| TimeFrame | integer |  |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string |  |  |
| Connection | string |  |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string |  |  |
| ConnectionType | integer |  |  |
| RepositoryId | string |  |  |
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
| scanInformation13 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| package | object |  |  |
| totalPackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| vulnerablePackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| cryptography5 fields | object |  |  |
| totalCryptoAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| notQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| filesWithNotQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| status Choice 1CryptoAnalysisStatus |  |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| riskBreakdown Choice 1RiskBreakdownDto |  |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| metadata | string |  |  |
| importVerdict | string |  |  |

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
| TimeFrame | integer |  |  |
| Vulnerabilities | array |  |  |
| LicenseRisks | array |  |  |
| Status | array |  |  |
| TriggerEvent | array |  |  |
| Workflow | string |  |  |
| Connection | string |  |  |
| Secrets | boolean |  |  |
| Threats | boolean |  |  |
| Search | string |  |  |
| ConnectionType | integer |  |  |
| RepositoryId | string |  |  |
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
| scanInformation13 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| package | object |  |  |
| totalPackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| vulnerablePackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| cryptography5 fields | object |  |  |
| totalCryptoAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| notQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| filesWithNotQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| status Choice 1CryptoAnalysisStatus |  |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| riskBreakdown Choice 1RiskBreakdownDto |  |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| metadata | string |  |  |
| importVerdict | string |  |  |

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
| scanInformation13 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| package | object |  |  |
| totalPackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| vulnerablePackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| cryptography5 fields | object |  |  |
| totalCryptoAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| notQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| filesWithNotQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| status Choice 1CryptoAnalysisStatus |  |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| riskBreakdown Choice 1RiskBreakdownDto |  |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| metadata | string |  |  |
| importVerdict | string |  |  |

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
| scanInformation13 fields | object |  |  |
| malware | boolean |  |  |
| secret | boolean |  |  |
| vulnerabilityIssues5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| licenses3 fields | object |  |  |
| blockedLicensesCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction Choice 1UsageRestrictionDto |  |  |  |
| workflow4 fields | object |  |  |
| workflowId | string |  |  |
| workflowName | string |  |  |
| workflowIsDeleted | boolean |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| package | object |  |  |
| totalPackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| vulnerablePackages Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| cryptography5 fields | object |  |  |
| totalCryptoAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| notQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| filesWithNotQuantumSafeAssets Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| status Choice 1CryptoAnalysisStatus |  |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| riskBreakdown Choice 1RiskBreakdownDto |  |  |  |
| scannedOn | date-time |  |  |
| stopTime | date-time |  |  |
| triggerEvent | string |  |  |
| errors | array[string] |  |  |
| scanStatus3 fields | object |  |  |
| scanningState | string |  |  |
| uploadProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanProgress Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| metadata | string |  |  |
| importVerdict | string |  |  |

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
| everyNumberOfHours Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| everyNumberOfDays Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| everyNumberOfWeeks Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| everyNumberOfMonths Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| daysOfWeek | array[integer] |  |  |
| dayOfMonth Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| workflow Choice 1Workflow |  |  |  |
| scans | array[object] |  |  |

Expand  Response
### Enumerate all CVEs across scanned packages

Auth NoneQuery String

| severities | string |  |  |
| --- | --- | --- | --- |
| search | string |  |  |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/scans/cvescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| cves6 fields | array[object] |  |  |
| cve8 fields | object |  |  |
| id | string |  |  |
| fixedVersions | array[string] |  |  |
| severity | integer |  |  |
| source | string |  |  |
| cwes | array[string] |  |  |
| aliases | array[string] |  |  |
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
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
| deletedScansCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalScansFound Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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

| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| --- | --- | --- | --- |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| search | string |  |  |
| includeArchives | boolean |  |  |
| includePackages | boolean |  |  |

GET /api/v1/scans/{scanId}/filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| objectIdentityId | string |  |  |
| objectIdentityHash | string |  |  |
| scanResultId | string |  |  |
| progressUpload Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| progressScan Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| processingState | integer |  |  |
| exceptionDetails | string |  |  |
| created | date-time |  |  |
| discoveryStarted | date-time |  |  |
| discoveryStartedDaySec Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| processingFailedTime | date-time |  |  |
| processingRetryCount Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| objectRemediationActions | array[object] |  |  |
| scanResult Choice 1CoreScanResult |  |  |  |
| objectIdentity Choice 1ObjectIdentity |  |  |  |
| versions | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| metaDefenderCoreUrl | string |  |  |
| name | string |  |  |
| path | string |  |  |
| hash | string |  |  |
| objectStorageMetadata | string |  |  |
| size Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| lastModified | date-time |  |  |
| storageLocation | string |  |  |
| fileTypeCategory Choice 1FileTypeCategory |  |  |  |
| pathForDisplay | string |  |  |
| extension | string |  |  |

Expand 404

Not Found

 Response
### Get the file details view of a file by its scan result ID

Auth NonePath Params

| scanResultId | string |  |  |
| --- | --- | --- | --- |

Query String

| scanId | string |  |  |
| --- | --- | --- | --- |

GET /api/v1/scans/{scanResultId}/detailscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| fileId | string |  |  |
| scanResultId | string |  |  |
| parentId | string |  |  |
| displayName | string |  |  |
| filePath | string |  |  |
| fileType | string |  |  |
| size Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scannedOn | string |  |  |
| startTime | date-time |  |  |
| isArchive | boolean |  |  |
| isBlocked | boolean |  |  |
| blockedReason | string |  |  |
| isMalware | boolean |  |  |
| hasSecrets | boolean |  |  |
| isVulnerable | boolean |  |  |
| dlp Choice 1DlpDto |  |  |  |
| metascan Choice 1MetascanDto |  |  |  |
| sbom5 fields | object |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| dependencyVulnerabilityCounts5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| licenses Choice 1LicensesDto |  |  |  |
| packages12 fields | array[object] |  |  |
| packageId | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| licenses Choice 1LicensesDto |  |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest Choice 1LatestPackageInfoDto |  |  |  |
| steps3 fields | array[object] |  |  |
| step Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| command | string |  |  |
| sha256 | string |  |  |
| cbom4 fields | object |  |  |
| totalAssets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| notQuantumSafeAssets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| quantumLevels8 fields | object |  |  |
| level0 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level1 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level2 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level3 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level4 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level5 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level6 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| assets16 fields | array[object] |  |  |
| bomRef | string |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| quantumLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isInherited | boolean |  |  |
| classicalRisk | string |  |  |
| quantumRisk | string |  |  |
| overallRisk | string |  |  |
| classicalSecurityLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isPqc | boolean |  |  |
| recommendedReplacements3 fields | array[object] |  |  |
| algorithm | string |  |  |
| appliesTo | string |  |  |
| nistStandard | string |  |  |
| inheritedFrom3 fields | array[object] |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| description | string |  |  |
| quantumRationale | string |  |  |
| evidences | array[object] |  |  |
| line Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| match | string |  |  |

 Response
### Get the archive entries of a file by its scan result ID

Auth NonePath Params

| scanResultId | string |  |  |
| --- | --- | --- | --- |

Query String

| scanId | string |  |  |
| --- | --- | --- | --- |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/scans/{scanResultId}/childrencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| children19 fields | array[object] |  |  |
| fileId | string |  |  |
| scanResultId | string |  |  |
| parentId | string |  |  |
| displayName | string |  |  |
| filePath | string |  |  |
| fileType | string |  |  |
| size Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scannedOn | string |  |  |
| startTime | date-time |  |  |
| isArchive | boolean |  |  |
| isBlocked | boolean |  |  |
| blockedReason | string |  |  |
| isMalware | boolean |  |  |
| hasSecrets | boolean |  |  |
| isVulnerable | boolean |  |  |
| dlp Choice 1DlpDto |  |  |  |
| metascan Choice 1MetascanDto |  |  |  |
| sbom5 fields | object |  |  |
| vulnerabilityCounts5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| dependencyVulnerabilityCounts5 fields | object |  |  |
| critical Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| high Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| medium Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| low Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| licenses Choice 1LicensesDto |  |  |  |
| packages12 fields | array[object] |  |  |
| packageId | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| licenses Choice 1LicensesDto |  |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
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
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| labels5 fields | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| valueType | string |  |  |
| created | date-time |  |  |
| updated | date-time |  |  |
| latest Choice 1LatestPackageInfoDto |  |  |  |
| steps3 fields | array[object] |  |  |
| step Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| command | string |  |  |
| sha256 | string |  |  |
| cbom4 fields | object |  |  |
| totalAssets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| notQuantumSafeAssets Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| quantumLevels8 fields | object |  |  |
| level0 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level1 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level2 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level3 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level4 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level5 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| level6 Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| unknown Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| assets16 fields | array[object] |  |  |
| bomRef | string |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| quantumLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isInherited | boolean |  |  |
| classicalRisk | string |  |  |
| quantumRisk | string |  |  |
| overallRisk | string |  |  |
| classicalSecurityLevel Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| isPqc | boolean |  |  |
| recommendedReplacements3 fields | array[object] |  |  |
| algorithm | string |  |  |
| appliesTo | string |  |  |
| nistStandard | string |  |  |
| inheritedFrom3 fields | array[object] |  |  |
| name | string |  |  |
| assetType | string |  |  |
| identityKey | string |  |  |
| description | string |  |  |
| quantumRationale | string |  |  |
| evidences | array[object] |  |  |
| line Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| match | string |  |  |

 Response
### Get the dependencies of a file and its archive entries by its scan result ID

Rolls up the transitive dependencies reported for a file and every entry inside it when it is an archive. ReportedDependencyCount is what the scan engine reported; ItemizedDependencyCount is how many it itemized and therefore how many rows this endpoint can return.

Auth NonePath Params

| scanResultId | string |  |  |
| --- | --- | --- | --- |

Query String

| scanId | string |  |  |
| --- | --- | --- | --- |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| search | string |  |  |

GET /api/v1/scans/{scanResultId}/dependenciescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| directPackageCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalPackageCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| reportedDependencyCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| itemizedDependencyCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| distinctDependencyCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| dependencies9 fields | array[object] |  |  |
| uid | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| parentPackageName | string |  |  |
| parentPackageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |

Expand  Response
### Get the dependencies of one archive entry, including nested entries, by its child data ID

Same rollup as the file dependencies endpoint, scoped to one extracted file and any archive entries nested under it. ReportedDependencyCount is what the scan engine reported; ItemizedDependencyCount is how many it itemized and therefore how many rows this endpoint can return.

Auth NonePath Params

| scanResultId | string |  |  |
| --- | --- | --- | --- |
| childDataId | string |  |  |

Query String

| scanId | string |  |  |
| --- | --- | --- | --- |
| page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| search | string |  |  |

GET /api/v1/scans/{scanResultId}/archive/{childDataId}/dependenciescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| page Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| pageSize Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| hasMoreItems | boolean |  |  |
| directPackageCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalPackageCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| reportedDependencyCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| itemizedDependencyCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| distinctDependencyCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |
| dependencies9 fields | array[object] |  |  |
| uid | string |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| parentPackageName | string |  |  |
| parentPackageVersion | string |  |  |
| vulnerabilities9 fields | array[object] |  |  |
| id | string |  |  |
| severity | string |  |  |
| source | string |  |  |
| fixedVersions | array[string] |  |  |
| cwes | array[string] |  |  |
| type | string |  |  |
| aliases | array[string] |  |  |
| epss Choice 1EpssDto |  |  |  |
| ratings4 fields | array[object] |  |  |
| method | string |  |  |
| score Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)(?:\.\d+)?(?:[eE][+-]?\d+)?$` |  |
| number | number |  |  |
| severity | string |  |  |
| source Choice 1CveRatingSourceDto |  |  |  |
| vulnerabilityCounts Choice 1VulnerabilityCountsDto |  |  |  |

Expand  Response
### Get per-CVE new/fixed details for each trend period

Auth NoneQuery String

| interval | integer |  |  |
| --- | --- | --- | --- |
| periods |  | pattern: `^-?(?:0|[1-9]\d*)$`  Default: 4 |  |

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
| fixedCves6 fields | array[object] |  |  |
| cveId | string |  |  |
| severity | integer |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |

500

Internal Server Error

 Response
## Manage Services Connections

Endpoints[GET/api/v1/services/{serviceId}/references](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-service-references-by-service-id) [GET/api/v1/services/{serviceId}/{repositoryId}/references](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-service-references-by-service-id-and-repository-id) [POST/api/v1/services/references](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-service-references) [GET/api/v1/services/{serviceId}/resources](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-service-resources-by-service-id) [POST/api/v1/services](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-service) [GET/api/v1/services](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-services) [PUT/api/v1/services/{serviceId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-service-by-id) [GET/api/v1/services/{serviceId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-service-by-id) [DELETE/api/v1/services/{serviceId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-service-by-id) [GET/api/v1/services/{serviceId}/top-risky](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-top-risky-repositories-for-a-service)
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
### Get service references by service ID and repository ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |
| repositoryId | string |  |  |

Query String

| Page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| --- | --- | --- | --- |
| PageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| FilterValue | string |  |  |
| Cursor | string |  |  |
| Search | string | maxLength: 256  minLength: 0 |  |

GET /api/v1/services/{serviceId}/{repositoryId}/referencescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| references | array[string] |  |  |
| totalReferences Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

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
### Add a service

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| vendorType | integer |  |  |
| protocolType | integer |  |  |

POST /api/v1/servicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| type Choice 1NewStorageType |  |  |  |
| details Choice 1JsonNode |  |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

409

Conflict

500

Internal Server Error

503

Service Unavailable

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
| credentialsType Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| hasNewCredentials | boolean |  |  |

PUT /api/v1/services/{serviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| type Choice 1NewStorageType |  |  |  |
| details Choice 1JsonNode |  |  |  |
| result | integer |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

400

Bad Request

404

Not Found

409

Conflict

500

Internal Server Error

503

Service Unavailable

 Response
### Get a service by ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

Query String

| content | boolean |  |  |
| --- | --- | --- | --- |
| Search | string |  |  |
| Page |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| PageSize |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| FilterValue | string |  |  |
| Cursor | string |  |  |
| Search | string | maxLength: 256  minLength: 0 |  |
| PrioritizedRepositoriesReference | string |  |  |

GET /api/v1/services/{serviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| credentialsType Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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

500

Internal Server Error

 Response
### Delete a service by ID

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/v1/services/{serviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
### Get top-risky repositories for a service

Auth NonePath Params

| serviceId | string |  |  |
| --- | --- | --- | --- |

Query String

| window | string |  |  |
| --- | --- | --- | --- |
| count |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |

GET /api/v1/services/{serviceId}/top-riskycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| connectionId | string |  |  |
| connectionName | string |  |  |
| repositoryId | string |  |  |
| repositoryName | string |  |  |
| riskScore Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

400

Bad Request

500

Internal Server Error

 Response
## Manage Settings

Endpoints[GET/api/v1/network](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-base-url) [PUT/api/v1/network](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putset-the-base-url) [POST/api/v1/smtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-smtp-configuration) [PATCH/api/v1/smtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#patchpartially-update-smtp-configuration) [GET/api/v1/smtp](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-smtp-configuration) [POST/api/v1/jira](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-jira-configuration) [GET/api/v1/jira](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-jira-configurations) [GET/api/v1/jira/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-jira-configuration-by-id) [PUT/api/v1/jira/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-jira-configuration-by-id) [DELETE/api/v1/jira/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-jira-configuration-by-id) [GET/api/v1/jira/{id}/projects](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-jira-projects) [POST/api/v1/teams](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-teams-configuration) [GET/api/v1/teams](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-all-teams-configurations) [GET/api/v1/teams/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-teams-configuration-by-id) [PUT/api/v1/teams/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-teams-configuration-by-id) [DELETE/api/v1/teams/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-teams-configuration-by-id) [GET/api/v1/sso](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-sso-configuration) [PUT/api/v1/sso](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putcreate-or-update-the-sso-configuration) [GET/api/v1/sso/enabled](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getanonymous-by-design-the-login-page-must-decide-whether-to-off) [GET/api/v1/telemetry](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#gettelemetry) [PUT/api/v1/telemetry/enabled](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putenabled) [PUT/api/v1/telemetry/opswat](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putopswat) [POST/api/v1/telemetry/collectors](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcollectors) [PUT/api/v1/telemetry/collectors](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putcollectors) [DELETE/api/v1/telemetry/collectors](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletecollectors)
### Get the base URL

Auth NoneGET /api/v1/networkcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| baseUrl | string |  |  |

500

Internal Server Error

 Response
### Set the base URL

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| baseUrl | string |  |  |

PUT /api/v1/networkcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

409

Conflict

500

Internal Server Error

 Response
### Add a SMTP configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| host | string |  |  |
| port Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| port Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| username | string |  |  |
| password | string |  |  |
| secureSocketOption Choice 1SecureSocketOption |  |  |  |
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
| smtp Choice 1Smtp |  |  |  |
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
| jiraEntries8 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| apiKey | string |  |  |
| baseAddress | string |  |  |
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
| jira Choice 1Jira |  |  |  |
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
| teamsConnections7 fields | array[object] |  |  |
| name | string |  |  |
| apiKey | string |  |  |
| webhookUrl | string |  |  |
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
| teams Choice 1Teams |  |  |  |
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
### Get the SSO configuration

Auth NoneGET /api/v1/ssocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| ssoType | integer |  |  |
| ssoProvider | integer |  |  |
| baseUrl | string |  |  |
| clientId | string |  |  |
| authority | string |  |  |
| identityProviderIssuer | string |  |  |
| identityProviderLoginUrl | string |  |  |
| identityProviderLogoutUrl | string |  |  |
| administratorRoleName | string |  |  |
| readonlyRoleName | string |  |  |
| roleMappings | array[object] |  |  |
| roleId | uuid |  |  |
| idpRoleName | string |  |  |
| hasClientSecret | boolean |  |  |
| hasIdentityProviderCertificate | boolean |  |  |

404

Not Found

500

Internal Server Error

 Response
### Create or update the SSO configuration

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| ssoType | integer |  |  |
| ssoProvider | integer |  |  |
| baseUrl | string |  |  |
| clientId | string |  |  |
| clientSecret | string |  |  |
| authority | string |  |  |
| identityProviderIssuer | string |  |  |
| identityProviderLoginUrl | string |  |  |
| identityProviderLogoutUrl | string |  |  |
| administratorRoleName | string |  |  |
| readonlyRoleName | string |  |  |
| roleMappings | array[object] |  |  |
| roleId | uuid |  |  |
| idpRoleName | string |  |  |

PUT /api/v1/ssocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
### Anonymous by design: the login page must decide whether to offer the SSO button before a session exists. It returns only a boolean — never provider, authority, or secret presence.

Auth NoneGET /api/v1/sso/enabledcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |

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

Endpoints[POST/api/v1/users](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postadd-a-new-user) [GET/api/v1/users](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-users) [PUT/api/v1/users](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-a-user) [POST/api/v1/users/register](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postregister-a-new-pending-user) [POST/api/v1/users/{userId}/approve](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postapprove-a-pending-user) [POST/api/v1/users/{userId}/reject](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postreject-a-pending-user) [GET/api/v1/user](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-current-user) [PUT/api/v1/user](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putupdate-the-current-users-own-profile) [GET/api/v1/user/permissions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-the-calling-principals-permission-claims) [DELETE/api/v1/users/{userId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-user) [POST/api/v1/user/login](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postlogin-user) [POST/api/v1/user/sso/session](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postturns-an-identity-service-session-into-an-mdssc-one-the-sso-) [DELETE/api/v1/user/login/{userId}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deleteremove-all-tokens-for-an-user) [PUT/api/v1/user/token](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#putget-a-new-access-token) [POST/api/v1/user/password/request-reset](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postrequest-a-password-reset) [POST/api/v1/user/password/new-password](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postreset-a-user-password) [GET/api/v1/user/sessions](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-the-current-users-active-sessions) [POST/api/v1/user/sessions/terminate](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postterminate-the-current-users-sessions)
### Add a new user

The new password must meet the password policy. A rejected password returns 400 stating the exact limit.

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| role Choice 1UserRole |  |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| email | string |  |  |

POST /api/v1/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| createUserParameters5 fields | object |  |  |
| role Choice 1UserRole |  |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| email | string |  |  |
| currentUserId | string |  |  |

400

Bad Request

 Response
### Get users

Auth NoneQuery String

| Type | integer |  |  |
| --- | --- | --- | --- |
| StartIndex |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| Count |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| SearchTerm | string |  |  |

GET /api/v1/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| enumerateUsersDto2 fields | object |  |  |
| entries7 fields | array[object] |  |  |
| userId | string |  |  |
| username | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role Choice 1UserRole |  |  |  |
| showTutorial | boolean |  |  |
| tablePreferences2 fields | array[object] |  |  |
| tableId | string |  |  |
| columns3 fields | array[object] |  |  |
| columnKey | string |  |  |
| isVisible | boolean |  |  |
| order Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| totalCount Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| role Choice 1UserRole |  |  |  |
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
### Register a new pending user

The new password must meet the password policy. A rejected password returns 400 stating the exact limit.

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| fullName | string |  |  |
| userName | string |  |  |
| email | string |  |  |

POST /api/v1/users/registercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| userDto Choice 1UserDto |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Approve a pending user

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| role | integer |  |  |

POST /api/v1/users/{userId}/approvecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

403

Forbidden

404

Not Found

409

Conflict

 Response
### Reject a pending user

Auth NonePath Params

| userId | string |  |  |
| --- | --- | --- | --- |

POST /api/v1/users/{userId}/rejectcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

400

Bad Request

404

Not Found

409

Conflict

 Response
### Get current user

Auth NoneGET /api/v1/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| userDto Choice 1UserDto |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Update the current user's own profile

The new password must meet the password policy. A rejected password returns 400 stating the exact limit.

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| fullName | string |  |  |
| email | string |  |  |
| showTutorial | boolean |  |  |
| tablePreferences2 fields | array[object] |  |  |
| tableId | string |  |  |
| columns3 fields | array[object] |  |  |
| columnKey | string |  |  |
| isVisible | boolean |  |  |
| order Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

PUT /api/v1/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

 Response
### Get the calling principal's permission claims

Auth NoneGET /api/v1/user/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[string] |  |  |
| --- | --- | --- | --- |

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

POST /api/v1/user/logincURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jwtToken Choice 1JwtToken |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

400

Bad Request

429

Too Many Requests

 Response
### Turns an identity-service session into an MDSSC one. The SSO callback leaves the platform token readable by the page, but MDSSC's own session lives in an HttpOnly cookie that script cannot write, so the exchange has to happen here.

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /api/v1/user/sso/sessioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| No response body |
| --- |

403

Forbidden

404

Not Found

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

Auth NonePUT /api/v1/user/tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| jwtToken Choice 1JwtToken |  |  |  |
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

The new password must meet the password policy. A rejected password returns 400 stating the exact limit.

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| newPassword | string |  |  |
| newPasswordConfirmation | string |  |  |
| secureToken | string |  |  |
| userId | string |  |  |

POST /api/v1/user/password/new-passwordcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| user Choice 1UserDto |  |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### List the current user's active sessions

Auth NoneGET /api/v1/user/sessionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| signedInAt | date-time |  |  |
| lastActiveAt | date-time |  |  |
| expiresAt | date-time |  |  |
| isCurrent | boolean |  |  |

403

Forbidden

 Response
### Terminate the current user's sessions

Supply CurrentPassword to confirm the request.

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| sessionId | string |  |  |
| includeCurrent | boolean |  |  |

POST /api/v1/user/sessions/terminatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| terminatedCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| currentSessionEnded | boolean |  |  |

400

Bad Request

403

Forbidden

404

Not Found

429

Too Many Requests

 Response
## Manage Versions

Endpoints[GET/api/version](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-application-version) [GET/api/v1/version](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-application-version-2)
### Get application version

Auth NoneQuery String

| api-version | string |  |  |
| --- | --- | --- | --- |

GET /api/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| version | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
### Get application version

Auth NoneGET /api/v1/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| version | string |  |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |

 Response
## Manage Webhooks

Endpoints[POST/api/v1/webhook/hmac/{routeParameter}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#posthandles-a-scan-event-triggered-by-a-webhook-requires-a-custo) [POST/api/v1/webhook/{routeParameter}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#posthandles-a-scan-event-triggered-by-a-webhook-requires-a-custo)
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

Endpoints[POST/api/v1/workflows](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#postcreate-a-workflow) [GET/api/v1/workflows](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getlist-workflows-paginated) [PATCH/api/v1/workflows/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#patchpartially-update-a-workflow) [GET/api/v1/workflows/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getget-a-workflow-by-id) [DELETE/api/v1/workflows/{id}](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#deletedelete-a-workflow-by-id) [GET/api/v1/workflows/{id}/technologies](/docs/supply-chain/metadefender-software-supply-chain-api-4.1.1#getretrieve-metadefender-core-technology-states-for-a-workflow)
### Create a workflow

Auth NoneRequest Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| scanConfigurationId | string |  |  |
| blockedFileDefinition | object |  |  |
| mode | string |  |  |
| configuration Choice 1ConfigurableBlockedFileSettingsDto |  |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed3 fields | object |  |  |
| softDelete | boolean |  |  |
| copy Choice 1RemediationDto |  |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| softDelete | boolean |  |  |
| copy Choice 1RemediationDto |  |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| packageDelete3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| fileDiscoveryFilterConfiguration Choice 1FileDiscoveryFilterConfiguration |  |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| crossDomainTransfer Choice 1CrossDomainTransfer |  |  |  |

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

| page |  | pattern: `^-?(?:0|[1-9]\d*)$`  Default: 1 |  |
| --- | --- | --- | --- |
| pageSize |  | pattern: `^-?(?:0|[1-9]\d*)$`  Default: 10 |  |
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
| blockedFileDefinition | object |  |  |
| mode | string |  |  |
| configuration Choice 1ConfigurableBlockedFileSettingsDto |  |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed3 fields | object |  |  |
| softDelete | boolean |  |  |
| copy Choice 1RemediationDto |  |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| softDelete | boolean |  |  |
| copy Choice 1RemediationDto |  |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| packageDelete3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| fileDiscoveryFilterConfiguration Choice 1FileDiscoveryFilterConfiguration |  |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| crossDomainTransfer Choice 1CrossDomainTransfer |  |  |  |
| security Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
| scanPool | string |  |  |
| totalCount Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

 Response
### Partially update a workflow

Auth NonePath Params

| id | string |  |  |
| --- | --- | --- | --- |

Request Body application/*+jsonapplication/jsontext/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| scanConfigurationId | string |  |  |
| blockedFileDefinition Choice 1BlockedFileDefinitionDto |  |  |  |
| fileRemediations Choice 1FileRemediationsDto |  |  |  |
| fileDiscoveryFilterConfiguration Choice 1FileDiscoveryFilterConfiguration |  |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| crossDomainTransfer Choice 1CrossDomainTransfer |  |  |  |

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
| blockedFileDefinition | object |  |  |
| mode | string |  |  |
| configuration Choice 1ConfigurableBlockedFileSettingsDto |  |  |  |
| fileRemediations3 fields | object |  |  |
| sourceCode2 fields | object |  |  |
| allowed3 fields | object |  |  |
| softDelete | boolean |  |  |
| copy Choice 1RemediationDto |  |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| softDelete | boolean |  |  |
| copy Choice 1RemediationDto |  |  |  |
| keep | boolean |  |  |
| container2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| blocked2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| binary2 fields | object |  |  |
| allowed2 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| blocked3 fields | object |  |  |
| copy3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| packageDelete3 fields | object |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| keep | boolean |  |  |
| fileDiscoveryFilterConfiguration Choice 1FileDiscoveryFilterConfiguration |  |  |  |
| remediations3 fields | array[object] |  |  |
| isEnabled | boolean |  |  |
| type | string |  |  |
| config Choice 1JsonNode |  |  |  |
| crossDomainTransfer Choice 1CrossDomainTransfer |  |  |  |
| security Choice 1Choice 2Choice 3 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |
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
| enabledCount Choice 1Choice 2 |  | pattern: `^-?(?:0|[1-9]\d*)$` |  |
| integer | integer |  |  |

404

Not Found

500

Internal Server Error

 Response
