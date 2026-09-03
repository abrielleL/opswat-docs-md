<!-- source: https://www.opswat.com/docs/mdss/metadefender-storage-security-api/ref -->

This section of the user guide describes how you can programmatically
interact with the MetaDefender Storage Security REST API. Below are some
common tasks that can be done using the available REST APIs:

- Authenticate to obtain a JSON Web Token(JWT)
- Start or stop a process(scan)
- Add / remove storage units

## About this REST API

The exposed endpoint is located by default at `http(s)://md-storage-server/api/` (for example, the authentication endpoint is available at `http(s)://md-storage-server/api/user/authenticate`). All requests are handled by the NGINX web server before being proxied to the backend API Gateway service.

All endpoints perform authentication and authorization checks. For these checks to succeed, a valid token should be presented in the Authorization header in the form of Bearer.

Please note that all issued tokens have a timestamp and signature associated in order to prevent long-term usage without re - authentication. The lifespan of the token is currently set to 60 minutes, meaning you will have to request a new token before it expires in order to avoid error responses.

## Useful links

- <https://swagger.io/tools/swagger-ui/>

Server<MDSS_HOST>Server Variables## Authenticationhttp Bearer

As mentioned earlier, all endpoints perform authentication and authorization checks. In order for these checks to succeed, a valid token should be presented in the Authorization header in the form of `Bearer <JWT>`.

### Suggested application logic

If you plan to integrate **MetaDefender Storage Security** in your custom application or workflow, please consider the following scenarios for successfully making REST API requests:

| Scenario | Possible use cases |
| --- | --- |
| Short-lived integration | You are building or enhancing an application that requires sporadic or on-demand access to **MetaDefender Storage Security** REST APIs. |
|  | The application is not expected to make more than a few REST API calls per hour. |
|  | The application does not need to preserve a session. |
| Long-lived integration | You are building or enhancing an application that requires continuous, uninterrupted, or hard to predict access to **MetaDefender Storage Security** REST APIs. |
|  | Requests are being triggered based on external factors and your application should maintain connectivity with **MetaDefender Storage Security** REST API. |
|  | Session preserving is necessary and authentication should happen without user-interaction. |
|  | Your application will make a significant number of REST API requests and you need increased performance |
| API Key integration | You are building or enhancing an application that requires continuous, uninterrupted, or hard to predict access to **MetaDefender Storage Security** REST APIs. |
|  | Requests are being triggered based on external factors and your application should maintain connectivity with **MetaDefender Storage Security** REST API. |
|  | Authentication should happen without user-interaction. |
|  | Your application will make a significant number of REST API requests and you need increased performance. |

### Short-lived integration

- Obtain a signed accessToken by calling `/api/user/authenticate` API
- Use this token to call your desired REST API by providing it in the Authorization header
- Expire the token by calling `/api/user/logout`
- Repeat steps 1-3 the next time your application needs to call a REST API

### Long-lived integration

- Obtain a signed token by calling `/api/user/authenticate` API
- Securely save the received accessToken and the refreshToken
- Use the accessToken to call your desired REST API by providing it in the Authorization header
- Add an exception handler in case you receive a 401 Unauthorized response because the JWT has expired call `/api/user/refreshToken` to obtain a new accessToken by providing the saved refreshToken.

  > a) the accessToken expires after an hour of creation; the expiry time is represented in UTC format by the accessTokenExpiryTime value.
  > b) the refreshToken expires after an hour of creation; the expiry time is represented in UTC format by the refreshTokenExpiryTime value.
  > c) if the refreshToken has expired as well, obtain a signed token by calling `/api/user/authenticate` API
- Use the newly issued accessToken to call your desired REST API by providing it in the Authorization header

### API Key integration

- In the **MetaDefender Storage Security** interface, navigate to Settings → Profile → Configure API Key
- Generate the key, copy it, and store it somewhere safe
- Use the API Key to call your desired REST API by providing it as a header with the Key: `ApiKey` and Value: `<the value of your API Key>`

### General considerations

- The access token expiration date cannot be extended. By default, the access token is valid for an hour after calling `/api/user/authenticate` API to obtain it. The refresh token is also valid for an hour but can be extended by calling `/api/user/refreshToken` and it is also automatically extended with an hour with each non-GET request.
- A refresh token is used to request a new access token when the current one expires without requiring re-authentication using a username and password.
- The refresh token is used to forcibly expire any previously issued JWT when the refresh token expires or is removed by calling `/api/user/logout`.
- A 3rd party application that needs persistent connectivity with **MetaDefender Storage Security** should implement a timeout mechanism to ensure that the refresh token is renewed before it expires by calling `/api/user/refreshToken` whenever the JWT (access token) is expired but before the refresh token expires as well.
- API Keys cannot be used to authenticate requests to the `/api/user` and `/api/apikey` endpoints.

---

## Abac

Attribute-Based Access Control management endpoints

Endpoints[GET/api/abac/roles](/docs/mdss/metadefender-storage-security-api#abac-getroles) [POST/api/abac/roles](/docs/mdss/metadefender-storage-security-api#abac-createrole) [GET/api/abac/roles/{roleId}](/docs/mdss/metadefender-storage-security-api#abac-getrolebyid) [PUT/api/abac/roles/{roleId}](/docs/mdss/metadefender-storage-security-api#abac-updaterole) [DELETE/api/abac/roles/{roleId}](/docs/mdss/metadefender-storage-security-api#abac-deleterole) [GET/api/abac/permissions](/docs/mdss/metadefender-storage-security-api#abac-getpermissions) [POST/api/abac/permissions](/docs/mdss/metadefender-storage-security-api#abac-createpermission) [DELETE/api/abac/permissions/{permissionId}](/docs/mdss/metadefender-storage-security-api#abac-deletepermission) [POST/api/abac/roles/{roleId}/permissions](/docs/mdss/metadefender-storage-security-api#abac-assignpermissiontorole) [DELETE/api/abac/roles/{roleId}/permissions/{permissionId}](/docs/mdss/metadefender-storage-security-api#abac-removepermissionfromrole) [POST/api/abac/users/{userId}/roles](/docs/mdss/metadefender-storage-security-api#abac-assignroletouser) [PUT/api/abac/users/{userId}/roles](/docs/mdss/metadefender-storage-security-api#abac-replaceuserroles) [DELETE/api/abac/users/{userId}/roles/{roleBindingId}](/docs/mdss/metadefender-storage-security-api#abac-removerolefromuser) [POST/api/abac/users/{userId}/permissions](/docs/mdss/metadefender-storage-security-api#abac-assignpermissiontouser) [DELETE/api/abac/users/{userId}/permissions/{userPermissionId}](/docs/mdss/metadefender-storage-security-api#abac-removepermissionfromuser)
### Get Roles

Retrieve all ABAC roles. Set includePermissions to true to include the full permission list for each role.

Auth BearerQuery String

| includePermissions | boolean | Default: true |  |
| --- | --- | --- | --- |

GET /api/abac/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| roles3 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | string |  |  |
| action | string |  |  |
| resource | string |  |  |

 Response
### Create Role

Create a new ABAC role. Provide an optional templateRoleId to inherit all permissions from an existing role; any IDs in permissionIds are merged on top of the template.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 100  minLength: 3 |  |
| permissionIds | array[string] |  |  |
| templateRoleId | string |  |  |

POST /api/abac/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| role Role |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | string |  |  |
| action | string |  |  |
| resource | string |  |  |

 Response
### Get Role by ID

Retrieve a single role and its associated permissions by role ID.

Auth BearerPath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

GET /api/abac/roles/{roleId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| role Role |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | string |  |  |
| action | string |  |  |
| resource | string |  |  |

 Response
### Update Role

Replace an existing role's name and full permission set in a single operation. The supplied permissionIds become the role's complete permission list (previously assigned permissions not in the list are removed). Predefined system roles cannot be updated.

Auth BearerPath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 100  minLength: 3 |  |
| permissionIds | array[string] |  |  |

PUT /api/abac/roles/{roleId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Delete Role

Permanently delete a role. Predefined system roles cannot be deleted.

Auth BearerPath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/abac/roles/{roleId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get Permissions

Retrieve all available ABAC permissions (action + resource pairs).

Auth BearerGET /api/abac/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| permissions3 fields | array[object] |  |  |
| id | string |  |  |
| action | string |  |  |
| resource | string |  |  |

 Response
### Create Permission

Create a new ABAC permission defined by an action and a resource.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| action | string | minLength: 1 |  |
| resource | string | minLength: 1 |  |

POST /api/abac/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| permission Permission |  |  |  |
| object | object |  |  |
| id | string |  |  |
| action | string |  |  |
| resource | string |  |  |

 Response
### Delete Permission

Permanently delete a permission by ID. Predefined base permissions cannot be deleted.

Auth BearerPath Params

| permissionId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/abac/permissions/{permissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Assign Permission to Role

Assign a permission to the specified role.

Auth BearerPath Params

| roleId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| permissionId | string | minLength: 1 |  |

POST /api/abac/roles/{roleId}/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Remove Permission from Role

Remove a permission from the specified role. Permissions that were assigned to a predefined role during initialization cannot be removed.

Auth BearerPath Params

| roleId | string |  |  |
| --- | --- | --- | --- |
| permissionId | string |  |  |

DELETE /api/abac/roles/{roleId}/permissions/{permissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Assign Role to User

Assign a role to a user, optionally with an expiry date after which the assignment is no longer valid.

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| roleId | string | minLength: 1 |  |
| expiresAt | date-time |  |  |

POST /api/abac/users/{userId}/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| roleBindingId | string |  |  |

 Response
### Replace User Roles

Atomically replace all role assignments for a user with the provided set of role IDs. All existing role bindings are removed and new ones are created in a single transaction.

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| roleIds | array[string] |  |  |

PUT /api/abac/users/{userId}/rolescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Remove Role from User

Remove a role binding from a user using the role binding ID.

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |
| roleBindingId | string |  |  |

DELETE /api/abac/users/{userId}/roles/{roleBindingId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Assign Permission to User

Assign a permission directly to a user, optionally with an expiry date.

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| permissionId | string | minLength: 1 |  |
| expiresAt | date-time |  |  |

POST /api/abac/users/{userId}/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| userPermissionId | string |  |  |

 Response
### Remove Permission from User

Remove a directly assigned permission from a user using the user permission ID.

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |
| userPermissionId | string |  |  |

DELETE /api/abac/users/{userId}/permissions/{userPermissionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
## Account

Manage your accounts

Endpoints[POST/api/account](/docs/mdss/metadefender-storage-security-api#account-addaccount) [DELETE/api/account](/docs/mdss/metadefender-storage-security-api#account-bulkdeleteaccounts) [GET/api/account](/docs/mdss/metadefender-storage-security-api#account-getaccounts) [PATCH/api/account](/docs/mdss/metadefender-storage-security-api#account-updateaccount) [DELETE/api/account/{accountId}](/docs/mdss/metadefender-storage-security-api#account-deleteaccount) [GET/api/account/{accountId}](/docs/mdss/metadefender-storage-security-api#account-getaccount) [GET/api/account/{accountId}/storages](/docs/mdss/metadefender-storage-security-api#account-enumerateaccountstorages) [GET/api/account/{accountId}/sources](/docs/mdss/metadefender-storage-security-api#account-enumerateaccountsources)
### Add an account

Add a new storage account to the system

Auth BearerQuery String

| Name | string | display name for the account |  |
| --- | --- | --- | --- |
| Description | string | description of the account purpose or scope |  |
| Credentials | string | access credentials for the storage service |  |
| ProtocolType |  | type of protocol (0 = SMB, 1 = S3, etc.) |  |
| VendorType |  | vendor type of storage (0 = AmazonS3, 1 = OneDrive, etc.) |  |
| AutoDiscovery | boolean | if true, enables automatic storage detection |  |
| GroupId | string | id of the group account storages should be added to by default |  |
| StorageIds | array | id's of specific storage units under this account |  |

Request Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| CredentialsFile | file |  |  |

POST /api/accountcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |

Expand  Response
### Bulk delete accounts

Deletes up to 100 accounts in a single request. Per-account ABAC (Accounts.Delete) plus per-cascaded-storage ABAC (Storages.Delete) are enforced. When forceDelete=true, child storages are cascade-deleted along with their scans. If any cascaded storage has a running scan, the request is rejected with HTTP 409. When forceDelete=false, accounts with children are returned in the failed list with localized reason; only empty accounts are deleted.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| accountIds | array[string] |  |  |
| forceDelete | boolean |  |  |

DELETE /api/accountcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| confirmationRequired | boolean |  |  |
| preview | array[object] |  |  |
| accountId | string |  |  |
| memberStorageIds | array[string] |  |  |
| scansRunning | boolean |  |  |
| runningScans4 fields | array[object] |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| accountId | string |  |  |
| groupId | string |  |  |

 Response
### List accounts (paginated, filtered, sorted)

Returns a paginated, filtered, and sorted list of accounts. Supports multi-value filters: vendorType (StorageVendorType) and protocolType (StorageProtocolType). The autodiscoveryEnabled boolean filter restricts results to accounts with auto-discovery enabled or disabled. The includeStorages flag (default true) controls whether associated storage units are loaded per account; set to false to skip the per-account N+1 storage scan RPC calls. Default Count is 100 (maximum 100). Returns an IPagedResponse containing Items, TotalCount, StartIndex, and Count.

Auth BearerQuery String

| Name | string |  |  |
| --- | --- | --- | --- |
| VendorType | array |  |  |
| ProtocolType | array |  |  |
| AutodiscoveryEnabled | boolean |  |  |
| IncludeStorages | boolean |  |  |
| StartIndex | integer | maximum: 2147483647  minimum: 0 |  |
| Count | integer | maximum: 100  minimum: 1 |  |
| SortBy | array | Enum: `0`,`1` |  |
| SortOrder | array | Enum: `0`,`1` |  |

GET /api/accountcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| items10 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| credentials | string |  |  |
| autoDiscovery | boolean |  |  |
| groupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| protocolType | int32 |  |  |
| vendorType | int32 |  |  |
| accounts10 fields | array[object] | Deprecated |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| credentials | string |  |  |
| autoDiscovery | boolean |  |  |
| groupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| protocolType | int32 |  |  |
| vendorType | int32 |  |  |
| totalCount | int32 |  |  |
| startIndex | int32 |  |  |
| count | int32 |  |  |

 Response
### Update an account

Update an existing account's configuration

Auth BearerQuery String

| AccountId | string | id of the account to update |  |
| --- | --- | --- | --- |
| Name | string | display name for the account |  |
| Description | string | description of the account purpose or scope |  |
| Credentials | string | access credentials for the storage service |  |
| ProtocolType |  | type of protocol (0 = SMB, 1 = S3, etc.) |  |
| VendorType |  | vendor type of storage (0 = AmazonS3, 1 = OneDrive, etc.) |  |
| AutoDiscovery | boolean | if true, enables automatic storage detection |  |
| GroupId | string | id of the group account storages should be added to by default |  |

Request Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| CredentialsFile | file |  |  |

PATCH /api/accountcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| accountId | string |  |  |

 Response
### Delete an account

Permanently delete an account and its storage references

Auth BearerPath Params

| accountId | string | id of the account to delete |  |
| --- | --- | --- | --- |

Query String

| forceDelete | boolean | Default: false |  |
| --- | --- | --- | --- |

DELETE /api/account/{accountId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| confirmationRequired | boolean |  |  |
| preview | array[object] |  |  |
| accountId | string |  |  |
| memberStorageIds | array[string] |  |  |
| scansRunning | boolean |  |  |
| runningScans4 fields | array[object] |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| accountId | string |  |  |
| groupId | string |  |  |

 Response
### Fetch account by ID

Retrieve a single account's details by ID

Auth BearerPath Params

| accountId | string | id of the account to get |  |
| --- | --- | --- | --- |

GET /api/account/{accountId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| account10 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| credentials | string |  |  |
| autoDiscovery | boolean |  |  |
| groupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| protocolType | int32 |  |  |
| vendorType | int32 |  |  |

 Response
### Fetch available storage units for an account

List all storage units linked to a particular account

Auth BearerPath Params

| accountId | string | ID of the account |  |
| --- | --- | --- | --- |

GET /api/account/{accountId}/storagescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries | array[object] |  |  |
| autodiscoverySource | string |  |  |
| autodiscoverySourceUrl | string |  |  |
| protocolType | int32 |  |  |
| vendorType | int32 |  |  |

 Response
### Fetch account sources

Fetch account sources

Auth BearerPath Params

| accountId | string |  |  |
| --- | --- | --- | --- |

Query String

| filter | string |  |  |
| --- | --- | --- | --- |

GET /api/account/{accountId}/sourcescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries | array[string] |  |  |

 Response
## Audit

List audit information

Endpoints[GET/api/audit/{startIndex}/{count}](/docs/mdss/metadefender-storage-security-api#audit-enumerateauditlogs)
### Fetch audit logs

Auth BearerPath Params

| startIndex | string |  |  |
| --- | --- | --- | --- |
| count | string |  |  |

Query String

| logType | string |  |  |
| --- | --- | --- | --- |
| categoryType | string |  |  |
| logLevel | string |  |  |
| searchText | string |  |  |

GET /api/audit/{startIndex}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`0`,`1`,`2` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries8 fields | array[object] |  |  |
| id | string |  |  |
| logLevel | integer | - 0: Debug - 1: Info - 2: Warn - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| details | string |  |  |
| logType LogType |  |  |  |
| integer | integer | - 0: FileDiscovered - 1: FileScanned - 2: FileDiscoveryFailed - 3: FileCancelled - 100: ProcessStarted - 101: ProcessCompleted - 102: ProcessCancelled - 103: ProcessFailed - 200: FileTagged - 201: FileSanitizedKeptOriginal - 203: FileSanitizedDeletedOriginal - 204: FileDecryption - 205: BlockedFileMoved - 206: BlockedFileDeleted - 207: SanitizedFileMoved - 208: AllowedFileMoved - 209: BlockedFileCopied - 210: SanitizedFileCopied - 211: AllowedFileCopied - 212: BlockedFileKept - 213: AllowedFileKept - 214: SanitizedFileKept - 215: AllowedFileDeleted - 216: FileVersionsScanned - 217: DiscoveredFileDeleted - 218: DiscoveredFileMoved - 219: DiscoveredFileCopied - 220: DiscoveredFileKept - 221: SanitizedFileDeleted - 222: CdrUnsupportedFileMoved - 223: CdrUnsupportedFileCopied - 224: CdrUnsupportedFileDeleted - 225: CdrUnsupportedFileKept - 300: StorageAdded - 301: StorageUpdated - 302: StorageRemoved - 320: GroupAdded - 321: GroupUpdated - 322: GroupRemoved - 330: AccountAdded - 331: AccountUpdated - 332: AccountRemoved - 350: SecurityChecklistItem - 351: SecurityChecklistVerified - 400: Rtp - 410: FileTagging - 411: DeepCdrRemediation - 412: SanitizedFilesRemediation - 413: BlockedFilesRemediation - 414: TreatFilesWithSensitiveDataAsBlocked - 415: TreatFilesWithVulnerabilitiesAsBlocked - 416: AllowedFilesRemediation - 417: StrictBlockFilesStrategy - 418: ConfigurableBlockFilesStrategy - 419: DeletedEmptyFolders - 600: LoggedIn - 601: LoggedOut - 602: UserCreated - 603: UserRegistered - 604: UserRoleUpdated - 605: UserUpdated - 606: UserRemoved - 700: ScanInstanceAdd - 701: ScanInstanceUpdate - 702: ScanInstanceDelete - 703: ScanInstanceImport - 750: ScanPoolAdd - 751: ScanPoolUpdate - 752: ScanPoolDelete - 753: ScanPoolImport - 800: OnlineLicenseActivated - 801: OfflineLicenseActivated - 802: LicenseDeactivated - 900: ConfigurationImported - 901: ConfigurationExported - 950: Notifications - 975: Smtp - 1000: ExternalLoggerAdd - 1001: ExternalLoggerUpdate - 1002: ExternalLoggerDelete - 1100: DataRetention - 1200: ApiKeyAdd - 1201: ApiKeyUpdate - 1202: ApiKeyDelete - 1300: SsoConfiguration - 1400: WorkflowAdd - 1401: WorkflowUpdate - 1402: WorkflowDelete - 1403: WorkflowSetDefault - 1404: WorkflowImport - 1410: WorkflowTechnologies - 1500: ScanAdd - 1501: ScanUpdate - 1502: ScanDelete - 1503: ScanImport - 1600: OnDemandScanRequest - 1700: ReportGenerated - 1800: TourFinalized - 1900: ScanScheduleAdd - 1901: ScanScheduleUpdate - 1902: ScanScheduleDelete - 1903: ScanScheduleImport - 1904: ScanScheduleSkip - 2000: Encryption - 2101: RemediationAdd - 2102: RemediationUpdate - 2103: RemediationDelete - 2200: Certificates - 2300: Telemetry - 2400: AbacRoleAssigned - 2401: AbacRoleRemoved - 2402: AbacRoleCreated - 2403: AbacRoleDeleted - 2410: AbacPermissionAssigned - 2411: AbacPermissionRemoved - 2412: AbacRolesReplaced - 10105: ScanScheduleStart   Enum: `0`,`1`,`2`,`3`,`100`,`101`,`102`,`103`,`200`,`201`,`203`,`204`,`205`,`206`,`207`,`208`,`209`,`210`,`211`,`212`,`213`,`214`,`215`,`216`,`217`,`218`,`219`,`220`,`221`,`222`,`223`,`224`,`225`,`300`,`301`,`302`,`320`,`321`,`322`,`330`,`331`,`332`,`350`,`351`,`400`,`410`,`411`,`412`,`413`,`414`,`415`,`416`,`417`,`418`,`419`,`600`,`601`,`602`,`603`,`604`,`605`,`606`,`700`,`701`,`702`,`703`,`750`,`751`,`752`,`753`,`800`,`801`,`802`,`900`,`901`,`950`,`975`,`1000`,`1001`,`1002`,`1100`,`1200`,`1201`,`1202`,`1300`,`1400`,`1401`,`1402`,`1403`,`1404`,`1410`,`1500`,`1501`,`1502`,`1503`,`1600`,`1700`,`1800`,`1900`,`1901`,`1902`,`1903`,`1904`,`2000`,`2101`,`2102`,`2103`,`2200`,`2300`,`2400`,`2401`,`2402`,`2403`,`2410`,`2411`,`2412`,`10105` |  |
| userId | string |  |  |
| category | integer | - 0: Processes - 1: PostActions - 2: StorageUnits - 3: Authentication - 4: Settings - 6: Users - 8: Notifications - 9: GroupUnits - 10: AccountUnits   Enum: `0`,`1`,`2`,`3`,`4`,`6`,`8`,`9`,`10` |  |
| timeStamp | date-time |  |  |
| userName | string |  |  |
| filterCount | int64 |  |  |
| totalCount | int64 |  |  |

 Response
## Configuration

Import or export configuration file

Endpoints[GET/api/configuration/export](/docs/mdss/metadefender-storage-security-api#configuration-exportsettings) [POST/api/configuration/import](/docs/mdss/metadefender-storage-security-api#configuration-importsettings) [GET/api/configuration/enabledModules](/docs/mdss/metadefender-storage-security-api#configuration-getenabledmodules)
### Export configuration file

Export the current configuration settings to an archive. The file will be encrypted using the provided password.

Auth BearerQuery String

| exportLicense | boolean |  |  |
| --- | --- | --- | --- |
| exportSmtp | boolean |  |  |
| exportNotifications | boolean |  |  |
| exportRetention | boolean |  |  |
| exportUsers | boolean |  |  |
| password | string |  |  |

GET /api/configuration/exportcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Import configuration file

Auth BearerRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| ConfigurationFile | file |  |  |
| password | string |  |  |

POST /api/configuration/importcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: FailedToUpgradeConfigFile - 2: FailedRequestBodyIsEmpty - 3: FailedToActivateLicense - 4: FailedToDeserializeConfigFile - 5: FailedOutdatedVersion - 6: FailedInvalidConfigFile - 7: FailedMissingPassword - 8: FailedWrongPassword   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| areSmtpSettingsImported | boolean |  |  |
| isLicenseImported | boolean |  |  |
| isRetentionImported | boolean |  |  |
| areNotificationsImported | boolean |  |  |
| hasNotificationsPartialFailure | boolean |  |  |
| activationDto Activation |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| newLocalUserId | string |  |  |
| areUsersImported | boolean |  |  |

Expand  Response
### Get enabled modules

Auth NoneGET /api/configuration/enabledModulescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| enabledModules | array[integer] |  |  |

 Response
## External Logger

Manage external loggers

Endpoints[GET/api/externallogger](/docs/mdss/metadefender-storage-security-api#externallogger-enumerateexternalloggers) [PUT/api/externallogger/status](/docs/mdss/metadefender-storage-security-api#externallogger-updateexternalloggerstatus) [POST/api/externallogger/udpSyslog](/docs/mdss/metadefender-storage-security-api#externallogger-addsyslogserver) [PUT/api/externallogger/udpSyslog](/docs/mdss/metadefender-storage-security-api#externallogger-updatesyslogserver) [POST/api/externallogger/kafka](/docs/mdss/metadefender-storage-security-api#externallogger-addkafkaserver) [PUT/api/externallogger/kafka](/docs/mdss/metadefender-storage-security-api#externallogger-updatekafkaserver) [DELETE/api/externallogger/{id}](/docs/mdss/metadefender-storage-security-api#externallogger-deleteexternalloggerconfigurationbyid)
### Retrieve external loggers

Auth BearerGET /api/externalloggercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`0`,`1`,`2` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries4 fields | array[object] |  |  |
| id | string |  |  |
| isEnabled | boolean |  |  |
| loggerType | integer | - 0: SyslogUdp - 1: Kafka - 2: TcpSyslog - 3: TcpSyslogWithTls   Enum: `0`,`1`,`2`,`3` |  |
| connectionSettings ExternalLoggerConnectionSettings |  |  |  |
| object | object |  |  |
| $type | string |  |  |

 Response
### Update external logger state

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| id | string | minLength: 1 |  |
| isEnabled | boolean |  |  |

PUT /api/externallogger/statuscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Add a new Syslog server configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| serverAddress | string | minLength: 1  pattern: `^(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9]))$|^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$|^(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z]|[A-Za-z][A-Za-z0-9\-]*[A-Za-z0-9])$` |  |
| port | int32 | pattern: `^()(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})$` |  |
| loggerType | integer | - 0: SyslogUdp - 1: Kafka - 2: TcpSyslog - 3: TcpSyslogWithTls   Enum: `0`,`1`,`2`,`3` |  |
| facility | integer | - 0: KernelMessages - 1: UserLevelMessages - 2: MailSystem - 3: SystemDaemons - 4: SecurityOrAuthorizationMessages1 - 5: InternalMessages - 6: LinePrinterSubsystem - 7: NetworkNewsSubsystem - 8: UUCPSubsystem - 9: ClockDaemon1 - 10: SecurityOrAuthorizationMessages2 - 11: FTPDaemon - 12: NTPSubsystem - 13: LogAudit - 14: LogAlert - 15: ClockDaemon2 - 16: LocalUse0 - 17: LocalUse1 - 18: LocalUse2 - 19: LocalUse3 - 20: LocalUse4 - 21: LocalUse5 - 22: LocalUse6 - 23: LocalUse7   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23` |  |
| format | integer | - 0: RFC5424   Enum: `0` |  |
| $type | string |  |  |

Expand POST /api/externallogger/udpSyslogcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Update a Syslog server configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| serverAddress | string | minLength: 1  pattern: `^(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9]))$|^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$|^(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z]|[A-Za-z][A-Za-z0-9\-]*[A-Za-z0-9])$` |  |
| port | int32 | pattern: `^()(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})$` |  |
| loggerType | integer | - 0: SyslogUdp - 1: Kafka - 2: TcpSyslog - 3: TcpSyslogWithTls   Enum: `0`,`1`,`2`,`3` |  |
| facility | integer | - 0: KernelMessages - 1: UserLevelMessages - 2: MailSystem - 3: SystemDaemons - 4: SecurityOrAuthorizationMessages1 - 5: InternalMessages - 6: LinePrinterSubsystem - 7: NetworkNewsSubsystem - 8: UUCPSubsystem - 9: ClockDaemon1 - 10: SecurityOrAuthorizationMessages2 - 11: FTPDaemon - 12: NTPSubsystem - 13: LogAudit - 14: LogAlert - 15: ClockDaemon2 - 16: LocalUse0 - 17: LocalUse1 - 18: LocalUse2 - 19: LocalUse3 - 20: LocalUse4 - 21: LocalUse5 - 22: LocalUse6 - 23: LocalUse7   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23` |  |
| format | integer | - 0: RFC5424   Enum: `0` |  |
| $type | string |  |  |
| id | string | minLength: 1 |  |

Expand PUT /api/externallogger/udpSyslogcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Add a new Kafka server configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| serverAddressWithPortList | string | minLength: 1  pattern: `^(?:(?:(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z]|[A-Za-z][A-Za-z0-9\-]*[A-Za-z0-9]):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})))(?:,(?:(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z]|[A-Za-z][A-Za-z0-9\-]*[A-Za-z0-9]):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})))*?$` |  |
| loggerType | integer | - 0: SyslogUdp - 1: Kafka - 2: TcpSyslog - 3: TcpSyslogWithTls   Enum: `0`,`1`,`2`,`3` |  |
| topic | string | minLength: 1 |  |
| configuration | string | minLength: 1 |  |
| $type | string |  |  |

Expand POST /api/externallogger/kafkacURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Update a Kafka server configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| serverAddressWithPortList | string | minLength: 1  pattern: `^(?:(?:(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z]|[A-Za-z][A-Za-z0-9\-]*[A-Za-z0-9]):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})))(?:,(?:(([0-9a-fA-F]{1,4}:){7,7}[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,7}:|([0-9a-fA-F]{1,4}:){1,6}:[0-9a-fA-F]{1,4}|([0-9a-fA-F]{1,4}:){1,5}(:[0-9a-fA-F]{1,4}){1,2}|([0-9a-fA-F]{1,4}:){1,4}(:[0-9a-fA-F]{1,4}){1,3}|([0-9a-fA-F]{1,4}:){1,3}(:[0-9a-fA-F]{1,4}){1,4}|([0-9a-fA-F]{1,4}:){1,2}(:[0-9a-fA-F]{1,4}){1,5}|[0-9a-fA-F]{1,4}:((:[0-9a-fA-F]{1,4}){1,6})|:((:[0-9a-fA-F]{1,4}){1,7}|:)|fe80:(:[0-9a-fA-F]{0,4}){0,4}%[0-9a-zA-Z]{1,}|::(ffff(:0{1,4}){0,1}:){0,1}((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])|([0-9a-fA-F]{1,4}:){1,4}:((25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])\.){3,3}(25[0-5]|(2[0-4]|1{0,1}[0-9]){0,1}[0-9])):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})|(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z]|[A-Za-z][A-Za-z0-9\-]*[A-Za-z0-9]):(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})))*?$` |  |
| loggerType | integer | - 0: SyslogUdp - 1: Kafka - 2: TcpSyslog - 3: TcpSyslogWithTls   Enum: `0`,`1`,`2`,`3` |  |
| topic | string | minLength: 1 |  |
| configuration | string | minLength: 1 |  |
| $type | string |  |  |
| id | string | minLength: 1 |  |

Expand PUT /api/externallogger/kafkacURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Delete external logger

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/externallogger/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
## File

Retrieve processed files information

Endpoints[PUT/api/file](/docs/mdss/metadefender-storage-security-api#file-ondemandscan) [GET/api/file](/docs/mdss/metadefender-storage-security-api#file-enumeratefiles) [PUT/api/file/rescan](/docs/mdss/metadefender-storage-security-api#file-ondemandfilteredscan) [GET/api/file/{fileId}](/docs/mdss/metadefender-storage-security-api#file-getfile) [GET/api/file/archive](/docs/mdss/metadefender-storage-security-api#file-getarchiveresult) [POST/api/file/cancel](/docs/mdss/metadefender-storage-security-api#file-cancelfile)
### Rescan a file on demand

This request is used to update a scanned file with passwords, in case it is an encrypted archive andit could not be scanned because the passwords to decrypt it were not provided. It can also be used withoutproviding any passwords to simply rescan a specific file from a finished scan.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| fileId | string | ID of the file to rescan |  |
| fileIds | array[string] | IDs of the files to rescan |  |
| scanId | string | scan ID associated with the file  minLength: 1 |  |
| storageProtocolType | int32 | protocol used by the storage (e.g., SMB, S3) |  |
| passwords | array[string] | optional passwords for encrypted file scanning |  |
| workflowId | string | workflow ID to be used for the on-demand scan  minLength: 1 |  |
| mdssBaseUrl | string | base URL for MDSS, if not provided will use Request.Host |  |

PUT /api/filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Enumerate processed files

Auth BearerQuery String

| StartIndex | integer | starting position for pagination (0-based index)  maximum: 2147483647  minimum: 0 |  |
| --- | --- | --- | --- |
| Count | integer | maximum: 10000  minimum: 1 |  |
| StartDate | string | filter files by scan date |  |
| EndDate | string | filter files by scan date |  |
| Search | string | text filter |  |
| ScanType | array | scan type such as (on-demand, scheduled, real time)  Enum: `0`,`1`,`2` |  |
| StorageId | array | filter based on a list of possible storage id |  |
| ScanId | array | filter based on a list of possible scan id |  |
| ScanWorkflowSnapshotId | array | filter based on a list of possible scan workflow snapshot id |  |
| ProcessingState | array | Enum: `0`,`1`,`2`,`3`,`4` |  |
| Result | array | filter by scan result (0 = Clean, 1 = Blocked, 2 = Processing)  Enum: `0`,`1`,`2` |  |
| ScanAllResultI | array | filter by MD Core scan result (0 = NoThreatDetected, 1 = Infected, 2 = Suspicious, etc.)  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`255`,`1014`,`9999` |  |
| ScanResultICount | array | the number of engine results that are not "No threat detected" |  |
| SandboxVerdict | array | filter by Sandbox verdict (0 = NoThreat, 1 = Malicious, 2 = Suspicious)  Enum: `0`,`1`,`2`,`3`,`4`,`5`,`999` |  |
| VulnerabilityCount | array | the number of vulnerabilities detected |  |
| HasVulnerabilities | boolean | filter by presence of vulnerabilities |  |
| DlpDetection | boolean | DLP detection |  |
| HasBlockedFileVersions | boolean | filter by presence of blocked file versions |  |
| Remediations | array | filter by remediation performed on the file  Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| SkippedScan | boolean | filter by whether the scan was skipped |  |
| SortBy | array | Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8` |  |
| SortOrder | array | Enum: `0`,`1` |  |
| Expand | array | Possible values for expand: workflow_snapshot |  |

Expand GET /api/filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries | array |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| scanId | string |  |  |
| name | string |  |  |
| path | string |  |  |
| hash | string |  |  |
| fileOwner4 fields | object |  |  |
| userId | string |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| emailAddress | string |  |  |
| size | int64 |  |  |
| fileTypeCategory FileTypeCategory |  |  |  |
| integer | integer | - 0: Other - 1: Archive - 2: Application - 3: Document - 4: EncryptedDocument - 5: Executable - 6: Graphical - 7: DiskImage - 8: AudioVideo - 9: OpenSslEncrypted - 10: Pdf - 11: Text - 12: MailMessage   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12` |  |
| extension | string |  |  |
| storageType StorageType |  |  |  |
| object | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageName | string |  |  |
| storageLocation | string |  |  |
| scanName | string |  |  |
| progress Progress |  |  |  |
| object | object |  |  |
| upload | integer |  |  |
| scan | integer |  |  |
| archiveExtraction | integer |  |  |
| scanResult CoreScanResult |  |  |  |
| object | object |  |  |
| extractedFiles ExtractedFiles |  |  |  |
| object | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults ScanResults |  |  |  |
| object | object |  |  |
| scanDetails7 fields | array[object] |  |  |
| engineName | string |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| engId | string |  |  |
| waitTime | number |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| scanAllResultA | string |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| totalDetections | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileInfo FileInfo |  |  |  |
| object | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| displayName | string |  |  |
| fileTypeId | string |  |  |
| fileScanInfo FileScanInfo |  |  |  |
| object | object |  |  |
| finalVerdict FileScanInfoFinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| verdict | string |  |  |
| confidence | number |  |  |
| threatLevel | number |  |  |
| overviewReport FileScanInfoOverviewReport |  |  |  |
| object | object |  |  |
| analysisState | string |  |  |
| signalGroups4 fields | array[object] |  |  |
| description | string |  |  |
| verdict | string |  |  |
| signals3 fields | array[object] |  |  |
| originType | string |  |  |
| signalReadable | string |  |  |
| strength | number |  |  |
| mitreTechniques | array[object] |  |  |
| name | string |  |  |
| tacticName | string |  |  |
| iocs4 fields | array[object] |  |  |
| data | string |  |  |
| type | string |  |  |
| origin | string |  |  |
| verdict | string |  |  |
| yaraMatches9 fields | array[object] |  |  |
| ruleName | string |  |  |
| ruleDescription | string |  |  |
| verdict | string |  |  |
| matchedStrings | array[string] |  |  |
| author | string |  |  |
| version | string |  |  |
| threatLevel | number |  |  |
| confidence | number |  |  |
| strength | number |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| verdict | string |  |  |
| metaData FileScanInfoMetaData |  |  |  |
| object | object |  |  |
| entropy | number |  |  |
| forensicAnalysisRecommended | boolean |  |  |
| fuzzyFsioHash | string |  |  |
| errorCategory | string |  |  |
| errorCode | int32 |  |  |
| errorDetails | string |  |  |
| processInfo ProcessInfo |  |  |  |
| object | object |  |  |
| postProcessing PostProcessing |  |  |  |
| object | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| resultI | integer | - 0: Allowed - 1: Blocked - 2: Processing   Enum: `0`,`1`,`2` |  |
| dataId | string |  |  |
| dlpInfo DlpInfo |  |  |  |
| object | object |  |  |
| verdict | int64 |  |  |
| sbomInfo SbomInfo |  |  |  |
| object | object |  |  |
| finalVerdict FinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| totalPackageCount | int32 |  |  |
| verdict | string |  |  |
| vulnerabilityCounts VulnerabilityIssues |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| overviewReport OverviewReport |  |  |  |
| object | object |  |  |
| isPartialReport | boolean |  |  |
| osInfo OsInfo |  |  |  |
| object | object |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| scanMode | string |  |  |
| steps SbomStep |  |  |  |
| object | object |  |  |
| command | string |  |  |
| packages ContainerPackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| arch | string |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenseStatus | string |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| step | int32 |  |  |
| vulnerabilityCount | int32 |  |  |
| sha256 | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| packages SourceCodePackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependenciesPackageCount | int32 |  |  |
| dependenciesVulnerabilityTotal | int32 |  |  |
| dependenciesVulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| resultTemplateHash | string |  |  |
| vulnerabilityInfo VulnerabilityInfo |  |  |  |
| object | object |  |  |
| vulnerabilityInfoResult VulnerabilityInfoResult |  |  |  |
| object | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct DetectedProduct |  |  |  |
| object | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product Product |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor Vendor |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData VersionData |  |  |  |
| object | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details VulnerabilityDetails |  |  |  |
| object | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss Cvss |  |  |  |
| object | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss3 Cvss3 |  |  |  |
| object | object |  |  |
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
| sessionCookie | string |  |  |
| fileTypeInfo FileTypeInfo |  |  |  |
| object | object |  |  |
| fileInfoExtended FileInfoExtended |  |  |  |
| object | object |  |  |
| extensions | string |  |  |
| groupId | string |  |  |
| typeId | string |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| processingState | integer | - 0: InProgress - 1: Failed - 2: Canceled - 3: Available - 4: FailedRemediation   Enum: `0`,`1`,`2`,`3`,`4` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| created | date-time |  |  |
| lastModified | date-time |  |  |
| discoveryStarted | date-time |  |  |
| fileProcessingDetails FileProcessingDetails |  |  |  |
| object | object |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| remediation FileRemediation |  |  |  |
| object | object |  |  |
| deepCdr DeepCdr |  |  |  |
| object | object |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| fileWasReplaced | boolean |  |  |
| postActionFailedInformation | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| objectRemediationActions10 fields | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| objectActionState | integer | - 0: NotApplied - 1: Applied - 3: CannotBeApplied - 4: Error - 5: SanitizationSkipped   Enum: `0`,`1`,`3`,`4`,`5` |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| exceptions | array[string] |  |  |
| id | string |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| remediationId | string |  |  |
| tenantId | string |  |  |
| lastUpdated | date-time |  |  |
| metaDefenderCoreUrl | string |  |  |
| discoveryStartedDaySec | int64 |  |  |
| objectStorageMetadata | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| scanWorkflowSnapshot ScanWorkflowSnapshot |  |  |  |
| object | object |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| versions | array[object] |  |  |
| hasBlockedVersions | boolean |  |  |
| versionsCount | int32 |  |  |
| objectType | integer | - 0: File - 1: FileVersion   Enum: `0`,`1` |  |
| skippedScan | boolean |  |  |
| $type | string |  |  |
| filterCount | int64 |  |  |
| totalCount | int64 |  |  |

 Response
### Rescan multiple files on demand

This request is used to rescan and update existing files from a scan based on a filter.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| scanId | string | scan ID associated with the file  minLength: 1 |  |
| workflowId | string | workflow ID to use when re-scanning  minLength: 1 |  |
| passwords | array[string] | optional passwords for encrypted file scanning |  |
| filterParameters FileFilterSortParameters |  | Filters to select files to be re-scanned |  |
| object | object |  |  |
| expand | array[string] | Possible values for expand: workflow_snapshot |  |
| startDate | date-time | filter files by scan date |  |
| endDate | date-time | filter files by scan date |  |
| search | string | text filter |  |
| scanType | array[integer] | scan type such as (on-demand, scheduled, real time)  Enum: `0`,`1`,`2` |  |
| storageId | array[string] | filter based on a list of possible storage id |  |
| scanId | array[string] | filter based on a list of possible scan id |  |
| scanWorkflowSnapshotId | array[string] | filter based on a list of possible scan workflow snapshot id |  |
| processingState | array[integer] | Enum: `0`,`1`,`2`,`3`,`4` |  |
| result | array[integer] | filter by scan result (0 = Clean, 1 = Blocked, 2 = Processing)  Enum: `0`,`1`,`2` |  |
| scanAllResultI | array[integer] | filter by MD Core scan result (0 = NoThreatDetected, 1 = Infected, 2 = Suspicious, etc.)  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`255`,`1014`,`9999` |  |
| scanResultICount | array[integer] | the number of engine results that are not "No threat detected" |  |
| sandboxVerdict | array[integer] | filter by Sandbox verdict (0 = NoThreat, 1 = Malicious, 2 = Suspicious)  Enum: `0`,`1`,`2`,`3`,`4`,`5`,`999` |  |
| vulnerabilityCount | array[integer] | the number of vulnerabilities detected |  |
| hasVulnerabilities | boolean | filter by presence of vulnerabilities |  |
| dlpDetection | boolean | DLP detection |  |
| hasBlockedFileVersions | boolean | filter by presence of blocked file versions |  |
| remediations | array[integer] | filter by remediation performed on the file  Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| skippedScan | boolean | filter by whether the scan was skipped |  |
| sortBy | array[integer] | Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8` |  |
| sortOrder | array[integer] | Enum: `0`,`1` |  |
| storageProtocolType | int32 | storage protocol type to use when re-scanning |  |
| mdssBaseUrl | string | base URL for MDSS, if not provided will use Request.Host |  |

Expand PUT /api/file/rescancURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Fetch processing results for a file

File processing is done asynchronously and each analysis request is tracked by a file ID. Because processing a file is a potentially time-consuming operation, scheduling a file for processing and retrieving the results needs to be done using two separate API calls.

This request needs to be made multiple times until the analysis is complete. Analysis completion can be tracked using the processingState and the progress values from the response..

Auth BearerPath Params

| fileId | string |  |  |
| --- | --- | --- | --- |

Query String

| expand | array | Possible values for expand: workflow_snapshot |  |
| --- | --- | --- | --- |

GET /api/file/{fileId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string | Deprecated |  |
| scanId | string | Deprecated |  |
| name | string | Deprecated |  |
| path | string | Deprecated |  |
| hash | string | Deprecated |  |
| fileOwner FileOwner |  | Deprecated |  |
| object | object |  |  |
| userId | string |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| emailAddress | string |  |  |
| size | int64 | Deprecated |  |
| storageType StorageType |  | Deprecated |  |
| object | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageName | string | Deprecated |  |
| storageLocation | string | Deprecated |  |
| scanName | string | Deprecated |  |
| progress Progress |  | Deprecated |  |
| object | object |  |  |
| upload | integer |  |  |
| scan | integer |  |  |
| archiveExtraction | integer |  |  |
| scanResult CoreScanResult |  | Deprecated |  |
| object | object |  |  |
| extractedFiles ExtractedFiles |  |  |  |
| object | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults ScanResults |  |  |  |
| object | object |  |  |
| scanDetails7 fields | array[object] |  |  |
| engineName | string |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| engId | string |  |  |
| waitTime | number |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| scanAllResultA | string |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| totalDetections | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileInfo FileInfo |  |  |  |
| object | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| displayName | string |  |  |
| fileTypeId | string |  |  |
| fileScanInfo FileScanInfo |  |  |  |
| object | object |  |  |
| finalVerdict FileScanInfoFinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| verdict | string |  |  |
| confidence | number |  |  |
| threatLevel | number |  |  |
| overviewReport FileScanInfoOverviewReport |  |  |  |
| object | object |  |  |
| analysisState | string |  |  |
| signalGroups4 fields | array[object] |  |  |
| description | string |  |  |
| verdict | string |  |  |
| signals3 fields | array[object] |  |  |
| originType | string |  |  |
| signalReadable | string |  |  |
| strength | number |  |  |
| mitreTechniques | array[object] |  |  |
| name | string |  |  |
| tacticName | string |  |  |
| iocs4 fields | array[object] |  |  |
| data | string |  |  |
| type | string |  |  |
| origin | string |  |  |
| verdict | string |  |  |
| yaraMatches9 fields | array[object] |  |  |
| ruleName | string |  |  |
| ruleDescription | string |  |  |
| verdict | string |  |  |
| matchedStrings | array[string] |  |  |
| author | string |  |  |
| version | string |  |  |
| threatLevel | number |  |  |
| confidence | number |  |  |
| strength | number |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| verdict | string |  |  |
| metaData FileScanInfoMetaData |  |  |  |
| object | object |  |  |
| entropy | number |  |  |
| forensicAnalysisRecommended | boolean |  |  |
| fuzzyFsioHash | string |  |  |
| errorCategory | string |  |  |
| errorCode | int32 |  |  |
| errorDetails | string |  |  |
| processInfo ProcessInfo |  |  |  |
| object | object |  |  |
| postProcessing PostProcessing |  |  |  |
| object | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| resultI | integer | - 0: Allowed - 1: Blocked - 2: Processing   Enum: `0`,`1`,`2` |  |
| dataId | string |  |  |
| dlpInfo DlpInfo |  |  |  |
| object | object |  |  |
| verdict | int64 |  |  |
| sbomInfo SbomInfo |  |  |  |
| object | object |  |  |
| finalVerdict FinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| totalPackageCount | int32 |  |  |
| verdict | string |  |  |
| vulnerabilityCounts VulnerabilityIssues |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| overviewReport OverviewReport |  |  |  |
| object | object |  |  |
| isPartialReport | boolean |  |  |
| osInfo OsInfo |  |  |  |
| object | object |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| scanMode | string |  |  |
| steps SbomStep |  |  |  |
| object | object |  |  |
| command | string |  |  |
| packages ContainerPackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| arch | string |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenseStatus | string |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| step | int32 |  |  |
| vulnerabilityCount | int32 |  |  |
| sha256 | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| packages SourceCodePackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependenciesPackageCount | int32 |  |  |
| dependenciesVulnerabilityTotal | int32 |  |  |
| dependenciesVulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| resultTemplateHash | string |  |  |
| vulnerabilityInfo VulnerabilityInfo |  |  |  |
| object | object |  |  |
| vulnerabilityInfoResult VulnerabilityInfoResult |  |  |  |
| object | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct DetectedProduct |  |  |  |
| object | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product Product |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor Vendor |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData VersionData |  |  |  |
| object | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details VulnerabilityDetails |  |  |  |
| object | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss Cvss |  |  |  |
| object | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss3 Cvss3 |  |  |  |
| object | object |  |  |
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
| sessionCookie | string |  |  |
| fileTypeInfo FileTypeInfo |  |  |  |
| object | object |  |  |
| fileInfoExtended FileInfoExtended |  |  |  |
| object | object |  |  |
| extensions | string |  |  |
| groupId | string |  |  |
| typeId | string |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| processingState ProcessingState2 |  | Deprecated |  |
| integer | integer | - 0: InProgress - 1: Failed - 2: Canceled - 3: Available - 4: FailedRemediation   Enum: `0`,`1`,`2`,`3`,`4` |  |
| exception Exception |  | Deprecated |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| created | date-time | Deprecated |  |
| lastModified | date-time | Deprecated |  |
| discoveryStarted | date-time | Deprecated |  |
| fileProcessingDetails FileProcessingDetails |  | Deprecated |  |
| object | object |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| coreEngines5 fields | array[object] | Deprecated |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| remediation FileRemediation |  | Deprecated |  |
| object | object |  |  |
| deepCdr DeepCdr |  |  |  |
| object | object |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| fileWasReplaced | boolean |  |  |
| postActionFailedInformation | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| objectRemediationActions10 fields | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| objectActionState | integer | - 0: NotApplied - 1: Applied - 3: CannotBeApplied - 4: Error - 5: SanitizationSkipped   Enum: `0`,`1`,`3`,`4`,`5` |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| exceptions | array[string] |  |  |
| id | string |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| remediationId | string |  |  |
| tenantId | string |  |  |
| lastUpdated | date-time |  |  |
| metaDefenderCoreUrl | string | Deprecated |  |
| discoveryStartedDaySec | int64 | Deprecated |  |
| fileDto File |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| scanId | string |  |  |
| name | string |  |  |
| path | string |  |  |
| hash | string |  |  |
| fileOwner4 fields | object |  |  |
| userId | string |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| emailAddress | string |  |  |
| size | int64 |  |  |
| fileTypeCategory FileTypeCategory |  |  |  |
| integer | integer | - 0: Other - 1: Archive - 2: Application - 3: Document - 4: EncryptedDocument - 5: Executable - 6: Graphical - 7: DiskImage - 8: AudioVideo - 9: OpenSslEncrypted - 10: Pdf - 11: Text - 12: MailMessage   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12` |  |
| extension | string |  |  |
| storageType StorageType |  |  |  |
| object | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageName | string |  |  |
| storageLocation | string |  |  |
| scanName | string |  |  |
| progress Progress |  |  |  |
| object | object |  |  |
| upload | integer |  |  |
| scan | integer |  |  |
| archiveExtraction | integer |  |  |
| scanResult CoreScanResult |  |  |  |
| object | object |  |  |
| extractedFiles ExtractedFiles |  |  |  |
| object | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults ScanResults |  |  |  |
| object | object |  |  |
| scanDetails7 fields | array[object] |  |  |
| engineName | string |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| engId | string |  |  |
| waitTime | number |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| scanAllResultA | string |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| totalDetections | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileInfo FileInfo |  |  |  |
| object | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| displayName | string |  |  |
| fileTypeId | string |  |  |
| fileScanInfo FileScanInfo |  |  |  |
| object | object |  |  |
| finalVerdict FileScanInfoFinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| verdict | string |  |  |
| confidence | number |  |  |
| threatLevel | number |  |  |
| overviewReport FileScanInfoOverviewReport |  |  |  |
| object | object |  |  |
| analysisState | string |  |  |
| signalGroups4 fields | array[object] |  |  |
| description | string |  |  |
| verdict | string |  |  |
| signals3 fields | array[object] |  |  |
| originType | string |  |  |
| signalReadable | string |  |  |
| strength | number |  |  |
| mitreTechniques | array[object] |  |  |
| name | string |  |  |
| tacticName | string |  |  |
| iocs4 fields | array[object] |  |  |
| data | string |  |  |
| type | string |  |  |
| origin | string |  |  |
| verdict | string |  |  |
| yaraMatches9 fields | array[object] |  |  |
| ruleName | string |  |  |
| ruleDescription | string |  |  |
| verdict | string |  |  |
| matchedStrings | array[string] |  |  |
| author | string |  |  |
| version | string |  |  |
| threatLevel | number |  |  |
| confidence | number |  |  |
| strength | number |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| verdict | string |  |  |
| metaData FileScanInfoMetaData |  |  |  |
| object | object |  |  |
| entropy | number |  |  |
| forensicAnalysisRecommended | boolean |  |  |
| fuzzyFsioHash | string |  |  |
| errorCategory | string |  |  |
| errorCode | int32 |  |  |
| errorDetails | string |  |  |
| processInfo ProcessInfo |  |  |  |
| object | object |  |  |
| postProcessing PostProcessing |  |  |  |
| object | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| resultI | integer | - 0: Allowed - 1: Blocked - 2: Processing   Enum: `0`,`1`,`2` |  |
| dataId | string |  |  |
| dlpInfo DlpInfo |  |  |  |
| object | object |  |  |
| verdict | int64 |  |  |
| sbomInfo SbomInfo |  |  |  |
| object | object |  |  |
| finalVerdict FinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| totalPackageCount | int32 |  |  |
| verdict | string |  |  |
| vulnerabilityCounts VulnerabilityIssues |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| overviewReport OverviewReport |  |  |  |
| object | object |  |  |
| isPartialReport | boolean |  |  |
| osInfo OsInfo |  |  |  |
| object | object |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| scanMode | string |  |  |
| steps SbomStep |  |  |  |
| object | object |  |  |
| command | string |  |  |
| packages ContainerPackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| arch | string |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenseStatus | string |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| step | int32 |  |  |
| vulnerabilityCount | int32 |  |  |
| sha256 | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| packages SourceCodePackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependenciesPackageCount | int32 |  |  |
| dependenciesVulnerabilityTotal | int32 |  |  |
| dependenciesVulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| resultTemplateHash | string |  |  |
| vulnerabilityInfo VulnerabilityInfo |  |  |  |
| object | object |  |  |
| vulnerabilityInfoResult VulnerabilityInfoResult |  |  |  |
| object | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct DetectedProduct |  |  |  |
| object | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product Product |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor Vendor |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData VersionData |  |  |  |
| object | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details VulnerabilityDetails |  |  |  |
| object | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss Cvss |  |  |  |
| object | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss3 Cvss3 |  |  |  |
| object | object |  |  |
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
| sessionCookie | string |  |  |
| fileTypeInfo FileTypeInfo |  |  |  |
| object | object |  |  |
| fileInfoExtended FileInfoExtended |  |  |  |
| object | object |  |  |
| extensions | string |  |  |
| groupId | string |  |  |
| typeId | string |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| processingState | integer | - 0: InProgress - 1: Failed - 2: Canceled - 3: Available - 4: FailedRemediation   Enum: `0`,`1`,`2`,`3`,`4` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| created | date-time |  |  |
| lastModified | date-time |  |  |
| discoveryStarted | date-time |  |  |
| fileProcessingDetails FileProcessingDetails |  |  |  |
| object | object |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| remediation FileRemediation |  |  |  |
| object | object |  |  |
| deepCdr DeepCdr |  |  |  |
| object | object |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| fileWasReplaced | boolean |  |  |
| postActionFailedInformation | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| objectRemediationActions10 fields | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| objectActionState | integer | - 0: NotApplied - 1: Applied - 3: CannotBeApplied - 4: Error - 5: SanitizationSkipped   Enum: `0`,`1`,`3`,`4`,`5` |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| exceptions | array[string] |  |  |
| id | string |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| remediationId | string |  |  |
| tenantId | string |  |  |
| lastUpdated | date-time |  |  |
| metaDefenderCoreUrl | string |  |  |
| discoveryStartedDaySec | int64 |  |  |
| objectStorageMetadata | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| scanWorkflowSnapshot ScanWorkflowSnapshot |  |  |  |
| object | object |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| versions | array[object] |  |  |
| hasBlockedVersions | boolean |  |  |
| versionsCount | int32 |  |  |
| objectType | integer | - 0: File - 1: FileVersion   Enum: `0`,`1` |  |
| skippedScan | boolean |  |  |
| $type | string |  |  |

Expand  Response
### Retrieve archive scan results

Retrieve the archive scan results using either the scanResultId or the parentId

Auth BearerQuery String

| scanResultId | string |  |  |
| --- | --- | --- | --- |
| parentId | string |  |  |
| start | integer | Default: 0 |  |
| count | integer | Default: 1000 |  |

GET /api/file/archivecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| archiveScanResults14 fields | array[object] |  |  |
| extractedFiles ExtractedFiles |  |  |  |
| object | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults ScanResults |  |  |  |
| object | object |  |  |
| scanDetails7 fields | array[object] |  |  |
| engineName | string |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| engId | string |  |  |
| waitTime | number |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| scanAllResultA | string |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| totalDetections | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileInfo FileInfo |  |  |  |
| object | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| displayName | string |  |  |
| fileTypeId | string |  |  |
| fileScanInfo FileScanInfo |  |  |  |
| object | object |  |  |
| finalVerdict FileScanInfoFinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| verdict | string |  |  |
| confidence | number |  |  |
| threatLevel | number |  |  |
| overviewReport FileScanInfoOverviewReport |  |  |  |
| object | object |  |  |
| analysisState | string |  |  |
| signalGroups4 fields | array[object] |  |  |
| description | string |  |  |
| verdict | string |  |  |
| signals3 fields | array[object] |  |  |
| originType | string |  |  |
| signalReadable | string |  |  |
| strength | number |  |  |
| mitreTechniques | array[object] |  |  |
| name | string |  |  |
| tacticName | string |  |  |
| iocs4 fields | array[object] |  |  |
| data | string |  |  |
| type | string |  |  |
| origin | string |  |  |
| verdict | string |  |  |
| yaraMatches9 fields | array[object] |  |  |
| ruleName | string |  |  |
| ruleDescription | string |  |  |
| verdict | string |  |  |
| matchedStrings | array[string] |  |  |
| author | string |  |  |
| version | string |  |  |
| threatLevel | number |  |  |
| confidence | number |  |  |
| strength | number |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| verdict | string |  |  |
| metaData FileScanInfoMetaData |  |  |  |
| object | object |  |  |
| entropy | number |  |  |
| forensicAnalysisRecommended | boolean |  |  |
| fuzzyFsioHash | string |  |  |
| errorCategory | string |  |  |
| errorCode | int32 |  |  |
| errorDetails | string |  |  |
| processInfo ProcessInfo |  |  |  |
| object | object |  |  |
| postProcessing PostProcessing |  |  |  |
| object | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| resultI | integer | - 0: Allowed - 1: Blocked - 2: Processing   Enum: `0`,`1`,`2` |  |
| dataId | string |  |  |
| dlpInfo DlpInfo |  |  |  |
| object | object |  |  |
| verdict | int64 |  |  |
| sbomInfo SbomInfo |  |  |  |
| object | object |  |  |
| finalVerdict FinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| totalPackageCount | int32 |  |  |
| verdict | string |  |  |
| vulnerabilityCounts VulnerabilityIssues |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| overviewReport OverviewReport |  |  |  |
| object | object |  |  |
| isPartialReport | boolean |  |  |
| osInfo OsInfo |  |  |  |
| object | object |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| scanMode | string |  |  |
| steps SbomStep |  |  |  |
| object | object |  |  |
| command | string |  |  |
| packages ContainerPackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| arch | string |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenseStatus | string |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| step | int32 |  |  |
| vulnerabilityCount | int32 |  |  |
| sha256 | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| packages SourceCodePackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependenciesPackageCount | int32 |  |  |
| dependenciesVulnerabilityTotal | int32 |  |  |
| dependenciesVulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| resultTemplateHash | string |  |  |
| vulnerabilityInfo VulnerabilityInfo |  |  |  |
| object | object |  |  |
| vulnerabilityInfoResult VulnerabilityInfoResult |  |  |  |
| object | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct DetectedProduct |  |  |  |
| object | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product Product |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor Vendor |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData VersionData |  |  |  |
| object | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details VulnerabilityDetails |  |  |  |
| object | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss Cvss |  |  |  |
| object | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss3 Cvss3 |  |  |  |
| object | object |  |  |
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
| sessionCookie | string |  |  |
| fileTypeInfo FileTypeInfo |  |  |  |
| object | object |  |  |
| fileInfoExtended FileInfoExtended |  |  |  |
| object | object |  |  |
| extensions | string |  |  |
| groupId | string |  |  |
| typeId | string |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |

 Response
### Cancel a file in an ongoing scan

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| fileIds | array[string] |  |  |

POST /api/file/cancelcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string | Deprecated |  |
| scanId | string | Deprecated |  |
| name | string | Deprecated |  |
| path | string | Deprecated |  |
| hash | string | Deprecated |  |
| fileOwner FileOwner |  | Deprecated |  |
| object | object |  |  |
| userId | string |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| emailAddress | string |  |  |
| size | int64 | Deprecated |  |
| storageType StorageType |  | Deprecated |  |
| object | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageName | string | Deprecated |  |
| storageLocation | string | Deprecated |  |
| scanName | string | Deprecated |  |
| progress Progress |  | Deprecated |  |
| object | object |  |  |
| upload | integer |  |  |
| scan | integer |  |  |
| archiveExtraction | integer |  |  |
| scanResult CoreScanResult |  | Deprecated |  |
| object | object |  |  |
| extractedFiles ExtractedFiles |  |  |  |
| object | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults ScanResults |  |  |  |
| object | object |  |  |
| scanDetails7 fields | array[object] |  |  |
| engineName | string |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| engId | string |  |  |
| waitTime | number |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| scanAllResultA | string |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| totalDetections | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileInfo FileInfo |  |  |  |
| object | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| displayName | string |  |  |
| fileTypeId | string |  |  |
| fileScanInfo FileScanInfo |  |  |  |
| object | object |  |  |
| finalVerdict FileScanInfoFinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| verdict | string |  |  |
| confidence | number |  |  |
| threatLevel | number |  |  |
| overviewReport FileScanInfoOverviewReport |  |  |  |
| object | object |  |  |
| analysisState | string |  |  |
| signalGroups4 fields | array[object] |  |  |
| description | string |  |  |
| verdict | string |  |  |
| signals3 fields | array[object] |  |  |
| originType | string |  |  |
| signalReadable | string |  |  |
| strength | number |  |  |
| mitreTechniques | array[object] |  |  |
| name | string |  |  |
| tacticName | string |  |  |
| iocs4 fields | array[object] |  |  |
| data | string |  |  |
| type | string |  |  |
| origin | string |  |  |
| verdict | string |  |  |
| yaraMatches9 fields | array[object] |  |  |
| ruleName | string |  |  |
| ruleDescription | string |  |  |
| verdict | string |  |  |
| matchedStrings | array[string] |  |  |
| author | string |  |  |
| version | string |  |  |
| threatLevel | number |  |  |
| confidence | number |  |  |
| strength | number |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| verdict | string |  |  |
| metaData FileScanInfoMetaData |  |  |  |
| object | object |  |  |
| entropy | number |  |  |
| forensicAnalysisRecommended | boolean |  |  |
| fuzzyFsioHash | string |  |  |
| errorCategory | string |  |  |
| errorCode | int32 |  |  |
| errorDetails | string |  |  |
| processInfo ProcessInfo |  |  |  |
| object | object |  |  |
| postProcessing PostProcessing |  |  |  |
| object | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| resultI | integer | - 0: Allowed - 1: Blocked - 2: Processing   Enum: `0`,`1`,`2` |  |
| dataId | string |  |  |
| dlpInfo DlpInfo |  |  |  |
| object | object |  |  |
| verdict | int64 |  |  |
| sbomInfo SbomInfo |  |  |  |
| object | object |  |  |
| finalVerdict FinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| totalPackageCount | int32 |  |  |
| verdict | string |  |  |
| vulnerabilityCounts VulnerabilityIssues |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| overviewReport OverviewReport |  |  |  |
| object | object |  |  |
| isPartialReport | boolean |  |  |
| osInfo OsInfo |  |  |  |
| object | object |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| scanMode | string |  |  |
| steps SbomStep |  |  |  |
| object | object |  |  |
| command | string |  |  |
| packages ContainerPackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| arch | string |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenseStatus | string |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| step | int32 |  |  |
| vulnerabilityCount | int32 |  |  |
| sha256 | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| packages SourceCodePackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependenciesPackageCount | int32 |  |  |
| dependenciesVulnerabilityTotal | int32 |  |  |
| dependenciesVulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| resultTemplateHash | string |  |  |
| vulnerabilityInfo VulnerabilityInfo |  |  |  |
| object | object |  |  |
| vulnerabilityInfoResult VulnerabilityInfoResult |  |  |  |
| object | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct DetectedProduct |  |  |  |
| object | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product Product |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor Vendor |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData VersionData |  |  |  |
| object | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details VulnerabilityDetails |  |  |  |
| object | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss Cvss |  |  |  |
| object | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss3 Cvss3 |  |  |  |
| object | object |  |  |
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
| sessionCookie | string |  |  |
| fileTypeInfo FileTypeInfo |  |  |  |
| object | object |  |  |
| fileInfoExtended FileInfoExtended |  |  |  |
| object | object |  |  |
| extensions | string |  |  |
| groupId | string |  |  |
| typeId | string |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| processingState ProcessingState2 |  | Deprecated |  |
| integer | integer | - 0: InProgress - 1: Failed - 2: Canceled - 3: Available - 4: FailedRemediation   Enum: `0`,`1`,`2`,`3`,`4` |  |
| exception Exception |  | Deprecated |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| created | date-time | Deprecated |  |
| lastModified | date-time | Deprecated |  |
| discoveryStarted | date-time | Deprecated |  |
| fileProcessingDetails FileProcessingDetails |  | Deprecated |  |
| object | object |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| coreEngines5 fields | array[object] | Deprecated |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| remediation FileRemediation |  | Deprecated |  |
| object | object |  |  |
| deepCdr DeepCdr |  |  |  |
| object | object |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| fileWasReplaced | boolean |  |  |
| postActionFailedInformation | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| objectRemediationActions10 fields | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| objectActionState | integer | - 0: NotApplied - 1: Applied - 3: CannotBeApplied - 4: Error - 5: SanitizationSkipped   Enum: `0`,`1`,`3`,`4`,`5` |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| exceptions | array[string] |  |  |
| id | string |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| remediationId | string |  |  |
| tenantId | string |  |  |
| lastUpdated | date-time |  |  |
| metaDefenderCoreUrl | string | Deprecated |  |
| discoveryStartedDaySec | int64 | Deprecated |  |
| fileDto File |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| scanId | string |  |  |
| name | string |  |  |
| path | string |  |  |
| hash | string |  |  |
| fileOwner4 fields | object |  |  |
| userId | string |  |  |
| fullName | string |  |  |
| userName | string |  |  |
| emailAddress | string |  |  |
| size | int64 |  |  |
| fileTypeCategory FileTypeCategory |  |  |  |
| integer | integer | - 0: Other - 1: Archive - 2: Application - 3: Document - 4: EncryptedDocument - 5: Executable - 6: Graphical - 7: DiskImage - 8: AudioVideo - 9: OpenSslEncrypted - 10: Pdf - 11: Text - 12: MailMessage   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12` |  |
| extension | string |  |  |
| storageType StorageType |  |  |  |
| object | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageName | string |  |  |
| storageLocation | string |  |  |
| scanName | string |  |  |
| progress Progress |  |  |  |
| object | object |  |  |
| upload | integer |  |  |
| scan | integer |  |  |
| archiveExtraction | integer |  |  |
| scanResult CoreScanResult |  |  |  |
| object | object |  |  |
| extractedFiles ExtractedFiles |  |  |  |
| object | object |  |  |
| dataId | string |  |  |
| scanResultI | int32 |  |  |
| detectedBy | int32 |  |  |
| filesExtractedCount | int32 |  |  |
| scanResults ScanResults |  |  |  |
| object | object |  |  |
| scanDetails7 fields | array[object] |  |  |
| engineName | string |  |  |
| threatFound | string |  |  |
| scanResultI | int32 |  |  |
| defTime | string |  |  |
| scanTime | number |  |  |
| engId | string |  |  |
| waitTime | number |  |  |
| dataId | string |  |  |
| scanAllResultI | int32 |  |  |
| scanAllResultA | string |  |  |
| startTime | string |  |  |
| totalTime | number |  |  |
| totalAvs | int32 |  |  |
| totalDetections | int32 |  |  |
| progressPercentage | int32 |  |  |
| fileInfo FileInfo |  |  |  |
| object | object |  |  |
| fileSize | int64 |  |  |
| uploadTimestamp | string |  |  |
| md5 | string |  |  |
| sha1 | string |  |  |
| sha256 | string |  |  |
| fileTypeCategory | string |  |  |
| fileTypeDescription | string |  |  |
| fileTypeExtension | string |  |  |
| displayName | string |  |  |
| fileTypeId | string |  |  |
| fileScanInfo FileScanInfo |  |  |  |
| object | object |  |  |
| finalVerdict FileScanInfoFinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| verdict | string |  |  |
| confidence | number |  |  |
| threatLevel | number |  |  |
| overviewReport FileScanInfoOverviewReport |  |  |  |
| object | object |  |  |
| analysisState | string |  |  |
| signalGroups4 fields | array[object] |  |  |
| description | string |  |  |
| verdict | string |  |  |
| signals3 fields | array[object] |  |  |
| originType | string |  |  |
| signalReadable | string |  |  |
| strength | number |  |  |
| mitreTechniques | array[object] |  |  |
| name | string |  |  |
| tacticName | string |  |  |
| iocs4 fields | array[object] |  |  |
| data | string |  |  |
| type | string |  |  |
| origin | string |  |  |
| verdict | string |  |  |
| yaraMatches9 fields | array[object] |  |  |
| ruleName | string |  |  |
| ruleDescription | string |  |  |
| verdict | string |  |  |
| matchedStrings | array[string] |  |  |
| author | string |  |  |
| version | string |  |  |
| threatLevel | number |  |  |
| confidence | number |  |  |
| strength | number |  |  |
| tags | array[object] |  |  |
| name | string |  |  |
| verdict | string |  |  |
| metaData FileScanInfoMetaData |  |  |  |
| object | object |  |  |
| entropy | number |  |  |
| forensicAnalysisRecommended | boolean |  |  |
| fuzzyFsioHash | string |  |  |
| errorCategory | string |  |  |
| errorCode | int32 |  |  |
| errorDetails | string |  |  |
| processInfo ProcessInfo |  |  |  |
| object | object |  |  |
| postProcessing PostProcessing |  |  |  |
| object | object |  |  |
| actionsRan | string |  |  |
| actionsFailed | string |  |  |
| convertedTo | string |  |  |
| copyMoveDestination | string |  |  |
| convertedDestination | string |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| progressPercentage | int32 |  |  |
| userAgent | string |  |  |
| profile | string |  |  |
| result | string |  |  |
| blockedReason | string |  |  |
| fileTypeSkippedScan | boolean |  |  |
| processingTime | number |  |  |
| queueTime | number |  |  |
| resultI | integer | - 0: Allowed - 1: Blocked - 2: Processing   Enum: `0`,`1`,`2` |  |
| dataId | string |  |  |
| dlpInfo DlpInfo |  |  |  |
| object | object |  |  |
| verdict | int64 |  |  |
| sbomInfo SbomInfo |  |  |  |
| object | object |  |  |
| finalVerdict FinalVerdict |  |  |  |
| object | object |  |  |
| blocked | boolean |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| totalPackageCount | int32 |  |  |
| verdict | string |  |  |
| vulnerabilityCounts VulnerabilityIssues |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| overviewReport OverviewReport |  |  |  |
| object | object |  |  |
| isPartialReport | boolean |  |  |
| osInfo OsInfo |  |  |  |
| object | object |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| scanMode | string |  |  |
| steps SbomStep |  |  |  |
| object | object |  |  |
| command | string |  |  |
| packages ContainerPackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| arch | string |  |  |
| osName | string |  |  |
| osVersion | string |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| licenseStatus | string |  |  |
| licensingPackageCounts LicensingIssues |  |  |  |
| object | object |  |  |
| allowed | int32 |  |  |
| blocked | int32 |  |  |
| unknown | int32 |  |  |
| unsupported | int32 |  |  |
| step | int32 |  |  |
| vulnerabilityCount | int32 |  |  |
| sha256 | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| packages SourceCodePackage |  |  |  |
| object | object |  |  |
| authors | string |  |  |
| releaseDate | date-time |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| archive | boolean |  |  |
| executable | boolean |  |  |
| uid | string |  |  |
| licenses Licenses |  |  |  |
| object | object |  |  |
| allowed4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| blocked4 fields | array[object] |  |  |
| id | string |  |  |
| url | string |  |  |
| category | string |  |  |
| usageRestriction UsageRestriction |  |  |  |
| object | object |  |  |
| permissions | array[string] |  |  |
| conditions | array[string] |  |  |
| limitations | array[string] |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| target | string |  |  |
| hashes | array[object] |  |  |
| sha256 | string |  |  |
| fileName | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependencies Dependency |  |  |  |
| object | object |  |  |
| ecosystem | string |  |  |
| group | string |  |  |
| packageName | string |  |  |
| packageVersion | string |  |  |
| vulnerabilities SbomVulnerability |  |  |  |
| object | object |  |  |
| id | string |  |  |
| severity | integer | - 0: None - 1: Critical - 2: High - 3: Medium - 4: Low - 5: Unknown   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| source | string |  |  |
| fixedVersions | string |  |  |
| cwes | array[string] |  |  |
| vulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| dependenciesPackageCount | int32 |  |  |
| dependenciesVulnerabilityTotal | int32 |  |  |
| dependenciesVulnerabilityCounts VulnerabilityCounts |  |  |  |
| object | object |  |  |
| critical | int32 |  |  |
| high | int32 |  |  |
| medium | int32 |  |  |
| low | int32 |  |  |
| unknown | int32 |  |  |
| resultTemplateHash | string |  |  |
| vulnerabilityInfo VulnerabilityInfo |  |  |  |
| object | object |  |  |
| vulnerabilityInfoResult VulnerabilityInfoResult |  |  |  |
| object | object |  |  |
| code | int64 |  |  |
| hash | string |  |  |
| method | int64 |  |  |
| timeStamp | string |  |  |
| timing | int64 |  |  |
| detectedProduct DetectedProduct |  |  |  |
| object | object |  |  |
| hasVulnerability | boolean |  |  |
| isCurrent | boolean |  |  |
| product Product |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| remediationLink | string |  |  |
| severity | string |  |  |
| sigName | string |  |  |
| signature | int64 |  |  |
| vendor Vendor |  |  |  |
| object | object |  |  |
| id | int64 |  |  |
| name | string |  |  |
| version | string |  |  |
| versionData VersionData |  |  |  |
| object | object |  |  |
| countBehind | int64 |  |  |
| feedId | int64 |  |  |
| version | string |  |  |
| vulnerabilities5 fields | array[object] |  |  |
| description | string |  |  |
| details VulnerabilityDetails |  |  |  |
| object | object |  |  |
| cpe | string |  |  |
| cve | string |  |  |
| cvss Cvss |  |  |  |
| object | object |  |  |
| accessComplexity | string |  |  |
| accessVector | string |  |  |
| authentication | string |  |  |
| availabilityImpact | string |  |  |
| confidentialityImpact | string |  |  |
| generatedOnEpoch | string |  |  |
| integrityImpact | string |  |  |
| score | string |  |  |
| source | string |  |  |
| cvss3 Cvss3 |  |  |  |
| object | object |  |  |
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
| sessionCookie | string |  |  |
| fileTypeInfo FileTypeInfo |  |  |  |
| object | object |  |  |
| fileInfoExtended FileInfoExtended |  |  |  |
| object | object |  |  |
| extensions | string |  |  |
| groupId | string |  |  |
| typeId | string |  |  |
| scanInstanceUrl | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| processingState | integer | - 0: InProgress - 1: Failed - 2: Canceled - 3: Available - 4: FailedRemediation   Enum: `0`,`1`,`2`,`3`,`4` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| created | date-time |  |  |
| lastModified | date-time |  |  |
| discoveryStarted | date-time |  |  |
| fileProcessingDetails FileProcessingDetails |  |  |  |
| object | object |  |  |
| streamingStartedTime | date-time |  |  |
| streamingCompletedTime | date-time |  |  |
| streamingTimeSpanMs | int64 |  |  |
| scanCompletedTime | date-time |  |  |
| processingTimeSpanMs | int64 |  |  |
| coreEngines5 fields | array[object] |  |  |
| engineId | string |  |  |
| engineName | string |  |  |
| engineVersion | string |  |  |
| dbVersion | string |  |  |
| definitionTime | string |  |  |
| remediation FileRemediation |  |  |  |
| object | object |  |  |
| deepCdr DeepCdr |  |  |  |
| object | object |  |  |
| sanitizationDetails SanitizationDetails |  |  |  |
| object | object |  |  |
| failureCategory | string |  |  |
| description | string |  |  |
| details | string |  |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| fileWasReplaced | boolean |  |  |
| postActionFailedInformation | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| exception Exception |  |  |  |
| object | object |  |  |
| exceptionDetails | string |  |  |
| exceptionMessage | string |  |  |
| objectRemediationActions10 fields | array[object] |  |  |
| objectActionType | integer | - 0: Tagging - 5: AllowedMoved - 6: BlockedMoved - 7: BlockedDelete - 8: AllowedSanitizedMoved - 9: AllowedCopied - 10: BlockedCopied - 11: AllowedSanitizedCopied - 12: AllowedSanitizedDeleted - 13: AllowedDeleted - 14: AllowedKept - 15: BlockedKept - 16: AllowedSanitizedKept - 17: BlockedSanitizedCopied - 18: BlockedSanitizedMoved - 19: BlockedSanitizedDeleted - 20: BlockedSanitizedKept - 21: ScanFileVersions - 22: DiscoveredMoved - 23: DiscoveredCopied - 24: DiscoveredKept - 25: DiscoveredDelete - 26: AllowedCdrUnsupportedKept - 27: AllowedCdrUnsupportedMoved - 28: AllowedCdrUnsupportedCopied - 29: AllowedCdrUnsupportedDeleted - 30: BlockedCdrUnsupportedKept - 31: BlockedCdrUnsupportedMoved - 32: BlockedCdrUnsupportedCopied - 33: BlockedCdrUnsupportedDeleted - 100: SoftDelete - 101: PackageDelete - 102: Copy   Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| objectActionState | integer | - 0: NotApplied - 1: Applied - 3: CannotBeApplied - 4: Error - 5: SanitizationSkipped   Enum: `0`,`1`,`3`,`4`,`5` |  |
| cdrObjectState CdrObjectState |  |  |  |
| integer | integer | - 0: Original - 1: CdrOriginal - 2: CdrSanitized   Enum: `0`,`1`,`2` |  |
| exceptions | array[string] |  |  |
| id | string |  |  |
| fileId | string |  |  |
| fileScanCompletedTime | date-time |  |  |
| remediationId | string |  |  |
| tenantId | string |  |  |
| lastUpdated | date-time |  |  |
| metaDefenderCoreUrl | string |  |  |
| discoveryStartedDaySec | int64 |  |  |
| objectStorageMetadata | string |  |  |
| scanWorkflowSnapshotId | string |  |  |
| scanWorkflowSnapshot ScanWorkflowSnapshot |  |  |  |
| object | object |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| versions | array[object] |  |  |
| hasBlockedVersions | boolean |  |  |
| versionsCount | int32 |  |  |
| objectType | integer | - 0: File - 1: FileVersion   Enum: `0`,`1` |  |
| skippedScan | boolean |  |  |
| $type | string |  |  |

Expand  Response
## Group

Manage your groups

Endpoints[POST/api/group](/docs/mdss/metadefender-storage-security-api#group-addgroup) [DELETE/api/group](/docs/mdss/metadefender-storage-security-api#group-bulkdeletegroups) [GET/api/group](/docs/mdss/metadefender-storage-security-api#group-getgroups) [PATCH/api/group](/docs/mdss/metadefender-storage-security-api#group-updategroup) [DELETE/api/group/{groupId}](/docs/mdss/metadefender-storage-security-api#group-deletegroup) [GET/api/group/{groupId}](/docs/mdss/metadefender-storage-security-api#group-getgroup) [GET/api/group/count](/docs/mdss/metadefender-storage-security-api#group-getgroupcount)
### Add a group

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | group name  minLength: 1 |  |
| description | string | description of the group |  |
| storageIds | array[string] | associated storages |  |

POST /api/groupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| group Group |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |

 Response
### Bulk delete groups

Deletes up to 100 groups in a single request. Per-group ABAC (Groups.Delete) plus per-cascaded-storage ABAC (Storages.Delete) are enforced. When forceDelete=true, child accounts and storages are cascade-deleted along with their scans. If any cascaded storage has a running scan, the request is rejected with HTTP 409. When forceDelete=false, groups with children are returned in the failed list with localized reason; only empty groups are deleted.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| groupIds | array[string] |  |  |
| forceDelete | boolean |  |  |

DELETE /api/groupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| confirmationRequired | boolean |  |  |
| preview | array[object] |  |  |
| groupId | string |  |  |
| memberStorageIds | array[string] |  |  |
| scansRunning | boolean |  |  |
| runningScans4 fields | array[object] |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| accountId | string |  |  |
| groupId | string |  |  |

 Response
### List groups (paginated, filtered, sorted)

Returns a paginated, filtered, and sorted list of groups. The name filter performs a case-insensitive substring (ILIKE) match. The includeStorages flag (default true) controls whether associated storage units are loaded per group; set to false to skip the per-group N+1 storage scan RPC calls. Default Count is 100 (maximum 100). Returns an IPagedResponse containing Items, TotalCount, StartIndex, and Count.

Auth BearerQuery String

| Name | string |  |  |
| --- | --- | --- | --- |
| IncludeStorages | boolean |  |  |
| StartIndex | integer | maximum: 2147483647  minimum: 0 |  |
| Count | integer | maximum: 100  minimum: 1 |  |
| SortBy | array | Enum: `0`,`1` |  |
| SortOrder | array | Enum: `0`,`1` |  |

GET /api/groupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| items4 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| groups4 fields | array[object] | Deprecated |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| totalCount | int32 |  |  |
| startIndex | int32 |  |  |
| count | int32 |  |  |

 Response
### Update a group

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | group name |  |
| description | string | description of the group |  |
| groupId | string | group id to update  minLength: 1 |  |

PATCH /api/groupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| updatedGroup Group |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |

 Response
### Delete a group

Auth BearerPath Params

| groupId | string |  |  |
| --- | --- | --- | --- |

Query String

| forceDelete | boolean | Default: false |  |
| --- | --- | --- | --- |

DELETE /api/group/{groupId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| confirmationRequired | boolean |  |  |
| preview | array[object] |  |  |
| groupId | string |  |  |
| memberStorageIds | array[string] |  |  |
| scansRunning | boolean |  |  |
| runningScans4 fields | array[object] |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| accountId | string |  |  |
| groupId | string |  |  |

 Response
### Fetch group by ID

Auth BearerPath Params

| groupId | string |  |  |
| --- | --- | --- | --- |

GET /api/group/{groupId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| group4 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| storages14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |

 Response
### Fetch the number of groups

Auth BearerGET /api/group/countcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| groupCount | object |  |  |
| count | int64 |  |  |

 Response
## Health Status

API that responds with 200 OK if application is running.

Endpoints[GET/api/health](/docs/mdss/metadefender-storage-security-api#health-checkhealth)
### Get health status

Auth NoneQuery String

| verbose | boolean | whether to include extra details  Default: false |  |
| --- | --- | --- | --- |

GET /api/healthcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| apiStatus | string |  |  |

 Response
## Onboarding

Manage onboarding

Endpoints[GET/api/onboarding](/docs/mdss/metadefender-storage-security-api#onboarding-getonboardingconfig) [POST/api/onboarding](/docs/mdss/metadefender-storage-security-api#onboarding-finishonboarding) [POST/api/onboarding/eula](/docs/mdss/metadefender-storage-security-api#onboarding-agreeeulaonboarding)
### Fetch onboarding configuration

Auth NoneQuery String

| newConfigSetup | boolean |  |  |
| --- | --- | --- | --- |
| newDefaultWorkflow | boolean |  |  |

GET /api/onboardingcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| hasUserConfigured | boolean |  |  |
| hasAccountConfigured | boolean |  |  |
| hasStorageConfigured | boolean |  |  |
| hasScanInstanceConfigured | boolean |  |  |
| isOnboardingDone | boolean |  |  |
| isEulaAgreed | boolean |  |  |
| isCloudType | boolean |  |  |

 Response
### Finish onboarding

Auth BearerPOST /api/onboardingcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Accept Eula

Auth BearerPOST /api/onboarding/eulacURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
## Remediations

Remediations information

Endpoints[GET/api/remediations/workflow/{id}](/docs/mdss/metadefender-storage-security-api#remediations-getremediationsbyworkflowid) [GET/api/remediations/{id}](/docs/mdss/metadefender-storage-security-api#remediations-getremediationbyid) [DELETE/api/remediations/{id}](/docs/mdss/metadefender-storage-security-api#remediations-deleteremediationbyid) [POST/api/remediations](/docs/mdss/metadefender-storage-security-api#remediations-addremediation) [PATCH/api/remediations](/docs/mdss/metadefender-storage-security-api#remediations-updateremediation) [DELETE/api/remediations](/docs/mdss/metadefender-storage-security-api#remediations-bulkdeleteremediations)
### Get Remediations by workflow id

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/remediations/workflow/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |

 Response
### Get Remediation by id

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/remediations/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entry Remediation |  |  |  |
| object | object |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |

Expand  Response
### Delete Remediation

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/remediations/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Add Remediation

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |

POST /api/remediationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Update Remediation

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type RemediationType |  |  |  |
| integer | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType RemediationHandlingType |  |  |  |
| integer | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |

PATCH /api/remediationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Bulk delete remediations

Deletes multiple remediations in a single request. Returns per-id succeeded/failed results; a non-existent id is reported as failed (not found).

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| remediationIds | array[string] |  |  |

DELETE /api/remediationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
## Report

Generate reports

Endpoints[GET/api/report](/docs/mdss/metadefender-storage-security-api#report-getscansreport) [GET/api/report/download/{scanId}](/docs/mdss/metadefender-storage-security-api#report-getpdfdownload)
### Get scans report

Auth BearerQuery String

| storageId | string |  |  |
| --- | --- | --- | --- |
| name | string |  |  |
| scanTypesFilter | array | Enum: `0`,`1`,`2` |  |
| scanStatesFilter | array | Enum: `0`,`1`,`2`,`3`,`4` |  |
| realTimeHandlingType |  |  |  |
| startDate | string |  |  |
| endDate | string |  |  |
| sortBy | array | Enum: `0`,`1`,`2` |  |
| sortOrder | array | Enum: `0`,`1` |  |
| startIndex | integer |  |  |
| count | integer |  |  |
| workflowId | string |  |  |
| dateField |  | Default: 0 |  |

GET /api/reportcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: StorageNotFound - 2: Error   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`0`,`1`,`2` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries | array |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| name | string |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| scanType | string |  |  |
| scanningState | integer | - 0: NotStarted - 1: Running - 2: Cancelled - 3: Failed - 4: Completed   Enum: `0`,`1`,`2`,`3`,`4` |  |
| scanStatusDto18 fields | object |  |  |
| pendingFilesCount | int64 |  |  |
| pendingFilesSize | int64 |  |  |
| allowedFilesCount | int64 |  |  |
| allowedFilesSize | int64 |  |  |
| blockedFilesCount | int64 |  |  |
| blockedFilesSize | int64 |  |  |
| sanitizedFilesCount | int64 |  |  |
| failedSanitizedFilesCount | int64 |  |  |
| remediatedFilesCount | int64 |  |  |
| totalFilesCount | int64 |  |  |
| totalFilesSize | int64 |  |  |
| processingFailedCount | int64 |  |  |
| processingFailedSize | int64 |  |  |
| processingFailedRemediationCount | int64 |  |  |
| processedFilesCount | int64 |  |  |
| processedFilesSize | int64 |  |  |
| canceledFilesCount | int64 |  |  |
| canceledFilesSize | int64 |  |  |
| scanStatsDto8 fields | object |  |  |
| infectedFilesCount | int64 |  |  |
| threatTotalFilesCount | int64 |  |  |
| filesWithVulnerabilitiesCount | int64 |  |  |
| filesWithSensitiveDataCount | int64 |  |  |
| filesBlockedBySandboxCount | int64 |  |  |
| scannedFilesCount | int64 |  |  |
| skippedFilesScanCount | int64 |  |  |
| scanFilesDistribution ScanFilesDistribution |  |  |  |
| object | object |  |  |
| documentsEncryptedFilesCount | int64 |  |  |
| executablesFilesCount | int64 |  |  |
| audioVideoFilesCount | int64 |  |  |
| openSSlEncryptedFilesCount | int64 |  |  |
| pdfFilesCount | int64 |  |  |
| graphicalFilesCount | int64 |  |  |
| diskImageFilesCount | int64 |  |  |
| textFilesCount | int64 |  |  |
| mailFilesCount | int64 |  |  |
| applicationFilesCount | int64 |  |  |
| documentsFilesCount | int64 |  |  |
| otherFilesCount | int64 |  |  |
| archivesFilesCount | int64 |  |  |
| realTimeStartDate | date-time |  |  |
| scanSequenceDto ScanSequence |  |  |  |
| object | object |  |  |
| previousScanId | string |  |  |
| nextScanId | string |  |  |
| scanPartition | string |  |  |
| workflowId | string | WorkflowId required if ScanConfigurationId is null  minLength: 1 |  |
| scanConfigurationId | string | This property is obsolete and will be removed in the future. Use WorkflowId instead. |  |
| errors | array[string] |  |  |
| priority | integer | - 0: Low - 1: Medium - 2: High   Enum: `0`,`1`,`2` |  |
| scanWorkflowSnapshotDtos13 fields | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| storageId | string |  |  |
| discoveryCycleTiming DiscoveryCycleTimingResponse |  |  |  |
| object | object |  |  |
| currentCycleStartedAt | date-time |  |  |
| lastCycleStartedAt | date-time |  |  |
| lastCycleFinishedAt | date-time |  |  |
| lastCycleDurationSeconds | number |  |  |
| $type | string |  |  |
| totalCount | int64 |  |  |

 Response
### Download PDF Report

Auth BearerPath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

Query String

| TypeOfReport | integer | Enum: `0`,`1` |  |
| --- | --- | --- | --- |
| StartIndex | integer | starting position for pagination (0-based index)  maximum: 2147483647  minimum: 0 |  |
| Count | integer | maximum: 10000  minimum: 1 |  |
| StartDate | string | filter files by scan date |  |
| EndDate | string | filter files by scan date |  |
| Search | string | text filter |  |
| ScanType | array | scan type such as (on-demand, scheduled, real time)  Enum: `0`,`1`,`2` |  |
| StorageId | array | filter based on a list of possible storage id |  |
| ScanId | array | filter based on a list of possible scan id |  |
| ScanWorkflowSnapshotId | array | filter based on a list of possible scan workflow snapshot id |  |
| ProcessingState | array | Enum: `0`,`1`,`2`,`3`,`4` |  |
| Result | array | filter by scan result (0 = Clean, 1 = Blocked, 2 = Processing)  Enum: `0`,`1`,`2` |  |
| ScanAllResultI | array | filter by MD Core scan result (0 = NoThreatDetected, 1 = Infected, 2 = Suspicious, etc.)  Enum: `0`,`1`,`2`,`3`,`7`,`8`,`9`,`10`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`34`,`36`,`38`,`39`,`40`,`41`,`42`,`43`,`255`,`1014`,`9999` |  |
| ScanResultICount | array | the number of engine results that are not "No threat detected" |  |
| SandboxVerdict | array | filter by Sandbox verdict (0 = NoThreat, 1 = Malicious, 2 = Suspicious)  Enum: `0`,`1`,`2`,`3`,`4`,`5`,`999` |  |
| VulnerabilityCount | array | the number of vulnerabilities detected |  |
| HasVulnerabilities | boolean | filter by presence of vulnerabilities |  |
| DlpDetection | boolean | DLP detection |  |
| HasBlockedFileVersions | boolean | filter by presence of blocked file versions |  |
| Remediations | array | filter by remediation performed on the file  Enum: `0`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`23`,`24`,`25`,`26`,`27`,`28`,`29`,`30`,`31`,`32`,`33`,`100`,`101`,`102` |  |
| SkippedScan | boolean | filter by whether the scan was skipped |  |
| SortBy | array | Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8` |  |
| SortOrder | array | Enum: `0`,`1` |  |
| Expand | array | Possible values for expand: workflow_snapshot |  |

Expand GET /api/report/download/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
## Scan

Manage your scans

Endpoints[GET/api/scan/{scanId}](/docs/mdss/metadefender-storage-security-api#scan-getscanbyid) [POST/api/scan/start](/docs/mdss/metadefender-storage-security-api#scan-startscan) [POST/api/scan/stop/{scanId}](/docs/mdss/metadefender-storage-security-api#scan-stopscan) [DELETE/api/scan](/docs/mdss/metadefender-storage-security-api#scan-bulkdeletescans) [POST/api/scan/stop](/docs/mdss/metadefender-storage-security-api#scan-bulkstopscans) [DELETE/api/scan/{storageId}](/docs/mdss/metadefender-storage-security-api#scan-deletescans) [GET/api/scan/last_completed/{storageId}](/docs/mdss/metadefender-storage-security-api#scan-getlastcompletedscan) [GET/api/scan/active/{scanId}](/docs/mdss/metadefender-storage-security-api#scan-getactivescanbyid) [GET/api/scan/realtime/{storageId}](/docs/mdss/metadefender-storage-security-api#scan-getrealtimeprocessingscan)
### Get scan by ID

Auth BearerPath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

GET /api/scan/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scan ScanResponse |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| name | string |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| scanType | string |  |  |
| scanningState | integer | - 0: NotStarted - 1: Running - 2: Cancelled - 3: Failed - 4: Completed   Enum: `0`,`1`,`2`,`3`,`4` |  |
| scanStatusDto18 fields | object |  |  |
| pendingFilesCount | int64 |  |  |
| pendingFilesSize | int64 |  |  |
| allowedFilesCount | int64 |  |  |
| allowedFilesSize | int64 |  |  |
| blockedFilesCount | int64 |  |  |
| blockedFilesSize | int64 |  |  |
| sanitizedFilesCount | int64 |  |  |
| failedSanitizedFilesCount | int64 |  |  |
| remediatedFilesCount | int64 |  |  |
| totalFilesCount | int64 |  |  |
| totalFilesSize | int64 |  |  |
| processingFailedCount | int64 |  |  |
| processingFailedSize | int64 |  |  |
| processingFailedRemediationCount | int64 |  |  |
| processedFilesCount | int64 |  |  |
| processedFilesSize | int64 |  |  |
| canceledFilesCount | int64 |  |  |
| canceledFilesSize | int64 |  |  |
| scanStatsDto8 fields | object |  |  |
| infectedFilesCount | int64 |  |  |
| threatTotalFilesCount | int64 |  |  |
| filesWithVulnerabilitiesCount | int64 |  |  |
| filesWithSensitiveDataCount | int64 |  |  |
| filesBlockedBySandboxCount | int64 |  |  |
| scannedFilesCount | int64 |  |  |
| skippedFilesScanCount | int64 |  |  |
| scanFilesDistribution ScanFilesDistribution |  |  |  |
| object | object |  |  |
| documentsEncryptedFilesCount | int64 |  |  |
| executablesFilesCount | int64 |  |  |
| audioVideoFilesCount | int64 |  |  |
| openSSlEncryptedFilesCount | int64 |  |  |
| pdfFilesCount | int64 |  |  |
| graphicalFilesCount | int64 |  |  |
| diskImageFilesCount | int64 |  |  |
| textFilesCount | int64 |  |  |
| mailFilesCount | int64 |  |  |
| applicationFilesCount | int64 |  |  |
| documentsFilesCount | int64 |  |  |
| otherFilesCount | int64 |  |  |
| archivesFilesCount | int64 |  |  |
| realTimeStartDate | date-time |  |  |
| scanSequenceDto ScanSequence |  |  |  |
| object | object |  |  |
| previousScanId | string |  |  |
| nextScanId | string |  |  |
| scanPartition | string |  |  |
| workflowId | string | WorkflowId required if ScanConfigurationId is null  minLength: 1 |  |
| scanConfigurationId | string | This property is obsolete and will be removed in the future. Use WorkflowId instead. |  |
| errors | array[string] |  |  |
| priority | integer | - 0: Low - 1: Medium - 2: High   Enum: `0`,`1`,`2` |  |
| scanWorkflowSnapshotDtos13 fields | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| storageId | string |  |  |
| discoveryCycleTiming DiscoveryCycleTimingResponse |  |  |  |
| object | object |  |  |
| currentCycleStartedAt | date-time |  |  |
| lastCycleStartedAt | date-time |  |  |
| lastCycleFinishedAt | date-time |  |  |
| lastCycleDurationSeconds | number |  |  |
| $type | string |  |  |

Expand  Response
### Start a scan

To scan a specific folder using the optional Folder parameter, provide the absolute folder path:
For Amazon S3 / S3 Compatible Types, Azure Blob, Azure Files, Google Cloud, Alibaba Cloud and Oracle Native: Including the Folder Location integrated in MDSS and excluding the Bucket Name, Container, etc.
For Box: With or without the "All Files" folder
For Sharepoint and Onedrive: Excluding the Document Library, Site, or Group
For OPSWAT MFT Storage: The desired Folder Path when integrating with user
For NFS / SMB / SFTP / FTP / SharePoint OnPrem: Only the folder path beyond your configured storage root (do not include the base path set during integration)
Provide the absolute folder path in the following format "{"Folder":"PATH_TO_SCAN"}

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageId | string | This property is obsolete and will be removed in the future. Use StorageIds instead.  Deprecated |  |
| name | string | user-defined name for the scan  pattern: `^[^@#$%&*"';:.|,{}?+=><`~^[]!\]+$` |  |
| folder | string | This property is obsolete and will be removed in the future. Use ScanPartition instead.  Deprecated |  |
| scanPartition | string | partiton of storage where the scan will run |  |
| priority | int32 | priority such as (low, medium, high) |  |
| storageIds | array[string] | id's of storages to be scanned |  |
| workflowId | string | associated workflow to be executed  minLength: 1 |  |
| mdssBaseUrl | string | base URL for MDSS, if not provided will use Request.Host |  |
| scanConfigDto ScanConfig |  |  |  |
| object | object |  |  |
| realTimeScanConfig RealTimeScanConfig |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| startDate | date-time |  |  |
| handlingType | integer | - 0: Polling - 1: EventBased   Enum: `0`,`1` |  |

Expand POST /api/scan/startcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scanId | string |  |  |
| scanIds | array[string] |  |  |
| failedStorages4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Stop a scan

Auth BearerPath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

POST /api/scan/stop/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| dispatched | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Bulk delete scans

Deletes up to 100 scan records across any storages the caller can access. Per-scan ABAC is enforced and inaccessible scan IDs are returned in the failed list with a localized reason. Partial-delete model — running scans are NOT a hard block: they are returned in the failed list with reasonKey BULK_OPERATION_SCAN_RUNNING while the rest of the batch is deleted normally.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| scanIds | array[string] |  |  |
| forceDeleteRtp | boolean |  |  |

DELETE /api/scancURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Bulk stop scans

Dispatches stop signals for up to 100 scans in a single request. Per-scan ABAC is enforced and inaccessible scan IDs are returned in the failed list with a localized reason. Stop is fire-and-forget — the response field 'dispatched' contains the scan IDs for which a stop signal was queued; the actual transition to Cancelled happens asynchronously.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| scanIds | array[string] |  |  |

POST /api/scan/stopcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| dispatched | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Delete scans

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Query String

| forceDeleteRtp | boolean | Default: true |  |
| --- | --- | --- | --- |

Request Body application/json

| array | array[string] |  |  |
| --- | --- | --- | --- |

DELETE /api/scan/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Fetch last completed scan

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

GET /api/scan/last_completed/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scan ScanResponse |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| name | string |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| scanType | string |  |  |
| scanningState | integer | - 0: NotStarted - 1: Running - 2: Cancelled - 3: Failed - 4: Completed   Enum: `0`,`1`,`2`,`3`,`4` |  |
| scanStatusDto18 fields | object |  |  |
| pendingFilesCount | int64 |  |  |
| pendingFilesSize | int64 |  |  |
| allowedFilesCount | int64 |  |  |
| allowedFilesSize | int64 |  |  |
| blockedFilesCount | int64 |  |  |
| blockedFilesSize | int64 |  |  |
| sanitizedFilesCount | int64 |  |  |
| failedSanitizedFilesCount | int64 |  |  |
| remediatedFilesCount | int64 |  |  |
| totalFilesCount | int64 |  |  |
| totalFilesSize | int64 |  |  |
| processingFailedCount | int64 |  |  |
| processingFailedSize | int64 |  |  |
| processingFailedRemediationCount | int64 |  |  |
| processedFilesCount | int64 |  |  |
| processedFilesSize | int64 |  |  |
| canceledFilesCount | int64 |  |  |
| canceledFilesSize | int64 |  |  |
| scanStatsDto8 fields | object |  |  |
| infectedFilesCount | int64 |  |  |
| threatTotalFilesCount | int64 |  |  |
| filesWithVulnerabilitiesCount | int64 |  |  |
| filesWithSensitiveDataCount | int64 |  |  |
| filesBlockedBySandboxCount | int64 |  |  |
| scannedFilesCount | int64 |  |  |
| skippedFilesScanCount | int64 |  |  |
| scanFilesDistribution ScanFilesDistribution |  |  |  |
| object | object |  |  |
| documentsEncryptedFilesCount | int64 |  |  |
| executablesFilesCount | int64 |  |  |
| audioVideoFilesCount | int64 |  |  |
| openSSlEncryptedFilesCount | int64 |  |  |
| pdfFilesCount | int64 |  |  |
| graphicalFilesCount | int64 |  |  |
| diskImageFilesCount | int64 |  |  |
| textFilesCount | int64 |  |  |
| mailFilesCount | int64 |  |  |
| applicationFilesCount | int64 |  |  |
| documentsFilesCount | int64 |  |  |
| otherFilesCount | int64 |  |  |
| archivesFilesCount | int64 |  |  |
| realTimeStartDate | date-time |  |  |
| scanSequenceDto ScanSequence |  |  |  |
| object | object |  |  |
| previousScanId | string |  |  |
| nextScanId | string |  |  |
| scanPartition | string |  |  |
| workflowId | string | WorkflowId required if ScanConfigurationId is null  minLength: 1 |  |
| scanConfigurationId | string | This property is obsolete and will be removed in the future. Use WorkflowId instead. |  |
| errors | array[string] |  |  |
| priority | integer | - 0: Low - 1: Medium - 2: High   Enum: `0`,`1`,`2` |  |
| scanWorkflowSnapshotDtos13 fields | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| storageId | string |  |  |
| discoveryCycleTiming DiscoveryCycleTimingResponse |  |  |  |
| object | object |  |  |
| currentCycleStartedAt | date-time |  |  |
| lastCycleStartedAt | date-time |  |  |
| lastCycleFinishedAt | date-time |  |  |
| lastCycleDurationSeconds | number |  |  |
| $type | string |  |  |

Expand  Response
### Get an active scan by scan ID

Auth BearerPath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

GET /api/scan/active/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scan ActiveScanResponse |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| name | string |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| scanType | string |  |  |
| scanningState | integer | - 0: NotStarted - 1: Running - 2: Cancelled - 3: Failed - 4: Completed   Enum: `0`,`1`,`2`,`3`,`4` |  |
| scanStatusDto18 fields | object |  |  |
| pendingFilesCount | int64 |  |  |
| pendingFilesSize | int64 |  |  |
| allowedFilesCount | int64 |  |  |
| allowedFilesSize | int64 |  |  |
| blockedFilesCount | int64 |  |  |
| blockedFilesSize | int64 |  |  |
| sanitizedFilesCount | int64 |  |  |
| failedSanitizedFilesCount | int64 |  |  |
| remediatedFilesCount | int64 |  |  |
| totalFilesCount | int64 |  |  |
| totalFilesSize | int64 |  |  |
| processingFailedCount | int64 |  |  |
| processingFailedSize | int64 |  |  |
| processingFailedRemediationCount | int64 |  |  |
| processedFilesCount | int64 |  |  |
| processedFilesSize | int64 |  |  |
| canceledFilesCount | int64 |  |  |
| canceledFilesSize | int64 |  |  |
| scanStatsDto8 fields | object |  |  |
| infectedFilesCount | int64 |  |  |
| threatTotalFilesCount | int64 |  |  |
| filesWithVulnerabilitiesCount | int64 |  |  |
| filesWithSensitiveDataCount | int64 |  |  |
| filesBlockedBySandboxCount | int64 |  |  |
| scannedFilesCount | int64 |  |  |
| skippedFilesScanCount | int64 |  |  |
| scanFilesDistribution ScanFilesDistribution |  |  |  |
| object | object |  |  |
| documentsEncryptedFilesCount | int64 |  |  |
| executablesFilesCount | int64 |  |  |
| audioVideoFilesCount | int64 |  |  |
| openSSlEncryptedFilesCount | int64 |  |  |
| pdfFilesCount | int64 |  |  |
| graphicalFilesCount | int64 |  |  |
| diskImageFilesCount | int64 |  |  |
| textFilesCount | int64 |  |  |
| mailFilesCount | int64 |  |  |
| applicationFilesCount | int64 |  |  |
| documentsFilesCount | int64 |  |  |
| otherFilesCount | int64 |  |  |
| archivesFilesCount | int64 |  |  |
| realTimeStartDate | date-time |  |  |
| scanSequenceDto ScanSequence |  |  |  |
| object | object |  |  |
| previousScanId | string |  |  |
| nextScanId | string |  |  |
| scanPartition | string |  |  |
| workflowId | string | WorkflowId required if ScanConfigurationId is null  minLength: 1 |  |
| scanConfigurationId | string | This property is obsolete and will be removed in the future. Use WorkflowId instead. |  |
| errors | array[string] |  |  |
| priority | integer | - 0: Low - 1: Medium - 2: High   Enum: `0`,`1`,`2` |  |
| scanWorkflowSnapshotDtos13 fields | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| storageId | string |  |  |
| discoveryCycleTiming DiscoveryCycleTimingResponse |  |  |  |
| object | object |  |  |
| currentCycleStartedAt | date-time |  |  |
| lastCycleStartedAt | date-time |  |  |
| lastCycleFinishedAt | date-time |  |  |
| lastCycleDurationSeconds | number |  |  |
| $type | string |  |  |
| serviceName | string |  |  |
| storageName | string |  |  |
| currentProcessingFilePath | string |  |  |
| currentProcessingFileProgress | string |  |  |
| discoveryState | integer | - 0: NotStarted - 1: Running - 2: Cancelled - 3: Failed - 4: Completed   Enum: `0`,`1`,`2`,`3`,`4` |  |
| statusMessages3 fields | array[object] |  |  |
| message | string |  |  |
| severity | integer | - 0: Information - 1: Warning - 2: Error   Enum: `0`,`1`,`2` |  |
| params | object |  |  |
| * | string |  |  |

Expand  Response
### Get Real-Time scan by storage Id

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Query String

| scanPartition | string |  |  |
| --- | --- | --- | --- |

GET /api/scan/realtime/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scan RealTimeScanResponse |  |  |  |
| object | object |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| id | string |  |  |
| name | string |  |  |
| startTime | date-time |  |  |
| stopTime | date-time |  |  |
| scanType | string |  |  |
| scanningState | integer | - 0: NotStarted - 1: Running - 2: Cancelled - 3: Failed - 4: Completed   Enum: `0`,`1`,`2`,`3`,`4` |  |
| scanStatusDto18 fields | object |  |  |
| pendingFilesCount | int64 |  |  |
| pendingFilesSize | int64 |  |  |
| allowedFilesCount | int64 |  |  |
| allowedFilesSize | int64 |  |  |
| blockedFilesCount | int64 |  |  |
| blockedFilesSize | int64 |  |  |
| sanitizedFilesCount | int64 |  |  |
| failedSanitizedFilesCount | int64 |  |  |
| remediatedFilesCount | int64 |  |  |
| totalFilesCount | int64 |  |  |
| totalFilesSize | int64 |  |  |
| processingFailedCount | int64 |  |  |
| processingFailedSize | int64 |  |  |
| processingFailedRemediationCount | int64 |  |  |
| processedFilesCount | int64 |  |  |
| processedFilesSize | int64 |  |  |
| canceledFilesCount | int64 |  |  |
| canceledFilesSize | int64 |  |  |
| scanStatsDto8 fields | object |  |  |
| infectedFilesCount | int64 |  |  |
| threatTotalFilesCount | int64 |  |  |
| filesWithVulnerabilitiesCount | int64 |  |  |
| filesWithSensitiveDataCount | int64 |  |  |
| filesBlockedBySandboxCount | int64 |  |  |
| scannedFilesCount | int64 |  |  |
| skippedFilesScanCount | int64 |  |  |
| scanFilesDistribution ScanFilesDistribution |  |  |  |
| object | object |  |  |
| documentsEncryptedFilesCount | int64 |  |  |
| executablesFilesCount | int64 |  |  |
| audioVideoFilesCount | int64 |  |  |
| openSSlEncryptedFilesCount | int64 |  |  |
| pdfFilesCount | int64 |  |  |
| graphicalFilesCount | int64 |  |  |
| diskImageFilesCount | int64 |  |  |
| textFilesCount | int64 |  |  |
| mailFilesCount | int64 |  |  |
| applicationFilesCount | int64 |  |  |
| documentsFilesCount | int64 |  |  |
| otherFilesCount | int64 |  |  |
| archivesFilesCount | int64 |  |  |
| realTimeStartDate | date-time |  |  |
| scanSequenceDto ScanSequence |  |  |  |
| object | object |  |  |
| previousScanId | string |  |  |
| nextScanId | string |  |  |
| scanPartition | string |  |  |
| workflowId | string | WorkflowId required if ScanConfigurationId is null  minLength: 1 |  |
| scanConfigurationId | string | This property is obsolete and will be removed in the future. Use WorkflowId instead. |  |
| errors | array[string] |  |  |
| priority | integer | - 0: Low - 1: Medium - 2: High   Enum: `0`,`1`,`2` |  |
| scanWorkflowSnapshotDtos13 fields | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |
| storageId | string |  |  |
| discoveryCycleTiming DiscoveryCycleTimingResponse |  |  |  |
| object | object |  |  |
| currentCycleStartedAt | date-time |  |  |
| lastCycleStartedAt | date-time |  |  |
| lastCycleFinishedAt | date-time |  |  |
| lastCycleDurationSeconds | number |  |  |
| $type | string |  |  |
| isRealTimeEnabled | boolean |  |  |
| handlingType | integer | - 0: Polling - 1: EventBased   Enum: `0`,`1` |  |

Expand  Response
## Scan Instance

List, add, update and delete Scan Instances

Endpoints[GET/api/scaninstance](/docs/mdss/metadefender-storage-security-api#scaninstance-getscaninstances) [POST/api/scaninstance](/docs/mdss/metadefender-storage-security-api#scaninstance-addscaninstance) [PUT/api/scaninstance](/docs/mdss/metadefender-storage-security-api#scaninstance-updatescaninstance) [GET/api/scaninstance/{id}](/docs/mdss/metadefender-storage-security-api#scaninstance-getscaninstancebyid) [DELETE/api/scaninstance/{id}](/docs/mdss/metadefender-storage-security-api#scaninstance-deletescaninstancebyid) [POST/api/scaninstance/Test](/docs/mdss/metadefender-storage-security-api#scaninstance-testscaninstance)
### Get Scan Instances

Auth BearerQuery String

| scanPoolId | string |  |  |
| --- | --- | --- | --- |

GET /api/scaninstancecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |

 Response
### Add a new Scan Instance

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| scanPoolId | string | minLength: 1 |  |
| url | string | minLength: 1  pattern: `^((?!(^((https?):\/\/)?127(?:\.[0-9]+){0,2}\.[0-9]+(:(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})?)?$)|(^((https?):\/\/)?\[(?:0*\:)*?:?0*1\](:(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})?)?$)).)*$` |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^([0-9]|[01][0-9]|2[0-3]):[0-5][0-9]:[0-5][0-9]$` |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |

POST /api/scaninstancecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scanInstanceId | string |  |  |

 Response
### Update an existing Scan Instance

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| id | string | minLength: 1 |  |
| url | string | pattern: `^((?!(^((https?):\/\/)?127(?:\.[0-9]+){0,2}\.[0-9]+(:(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})?)?$)|(^((https?):\/\/)?\[(?:0*\:)*?:?0*1\](:(6[0-4][0-9]{3}|65[0-4][0-9]{2}|655[0-2][0-9]|6553[0-5]|[1-5][0-9]{4}|[1-9][0-9]{0,3})?)?$)).)*$` |  |
| apiKey | string |  |  |
| timeout | string | pattern: `^([0-9]|[01][0-9]|2[0-3]):[0-5][0-9]:[0-5][0-9]$` |  |

PUT /api/scaninstancecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get Scan Instance by ID

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/scaninstance/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entry ScanInstance |  |  |  |
| object | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |

 Response
### Delete a Scan Instance

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/scaninstance/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Test

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| url | string | minLength: 1 |  |
| rules | array[string] |  |  |
| apiKey | string |  |  |
| userAgent | string |  |  |
| isCloudInstance | boolean |  |  |

POST /api/scaninstance/TestcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
## Scan Pool

List, add, update and delete Scan Pools

Endpoints[GET/api/scanpool](/docs/mdss/metadefender-storage-security-api#scanpool-getscanpools) [POST/api/scanpool](/docs/mdss/metadefender-storage-security-api#scanpool-addscanpool) [PUT/api/scanpool](/docs/mdss/metadefender-storage-security-api#scanpool-updatescanpool) [GET/api/scanpool/{id}](/docs/mdss/metadefender-storage-security-api#scanpool-getscanpoolbyid) [DELETE/api/scanpool/{id}](/docs/mdss/metadefender-storage-security-api#scanpool-deletescanpoolbyid)
### Get Scan Pools

Auth BearerGET /api/scanpoolcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries5 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |

 Response
### Add a new Scan Pool

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | maxLength: 30  minLength: 3 |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |

POST /api/scanpoolcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scanPoolId | string |  |  |

 Response
### Update an existing Scan Pool

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| id | string | minLength: 1 |  |
| name | string | maxLength: 30  minLength: 3 |  |

PUT /api/scanpoolcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get Scan Pool by ID

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/scanpool/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entry ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |

 Response
### Delete a Scan Pool

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/scanpool/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
## Scan Workflow Snapshot

List scan workflow snapshots

Endpoints[GET/api/scanworkflowsnapshot/getAllFromScan/{scanId}](/docs/mdss/metadefender-storage-security-api#scanworkflowsnapshot-getworkflowsusedbyscan)
### Get all scan workflow snapshots by scan ID

Auth BearerPath Params

| scanId | string |  |  |
| --- | --- | --- | --- |

GET /api/scanworkflowsnapshot/getAllFromScan/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| scanWorkflowSnapshots13 fields | array[object] |  |  |
| id | string |  |  |
| scanId | string |  |  |
| workflow17 fields | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| startTimestamp | int64 |  |  |
| stopTimestamp | int64 |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| storage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| workflowStatistics12 fields | object |  |  |
| taggingStatistics TaggingStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepAllowedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepBlockedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| keepSanitizedStatistics KeepStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| movedAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedSanitizedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| movedBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyAllowedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| copyBlockedStatistics MovedStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| destinationStorageInformation14 fields | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |
| deleteAllowedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| deleteBlockedStatistics DeleteStatistics |  |  |  |
| object | object |  |  |
| total | int64 |  |  |
| lastCalculatedStatisticsTime | date-time |  |  |
| account Account |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| description | string |  |  |
| credentials | string |  |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType StorageVendorType |  |  |  |
| integer | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| autoDiscovery | boolean |  |  |
| autodiscoveryDestinationGroupId | string |  |  |
| destinationGroup GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| realTimeStartDate | date-time |  |  |

 Response
## Settings

List or update your settings

Endpoints[PUT/api/settings/notifications](/docs/mdss/metadefender-storage-security-api#settings-updatenotificationsconfig) [GET/api/settings/notifications](/docs/mdss/metadefender-storage-security-api#settings-getnotificationsconfig) [PATCH/api/settings/smtp](/docs/mdss/metadefender-storage-security-api#settings-updatesmtpconfig) [GET/api/settings/smtp](/docs/mdss/metadefender-storage-security-api#settings-getsmtpconfig) [POST/api/settings/admin/license/activate/online](/docs/mdss/metadefender-storage-security-api#settings-activateonline) [POST/api/settings/admin/license/activate/offline](/docs/mdss/metadefender-storage-security-api#settings-activateoffline) [GET/api/settings/admin/license](/docs/mdss/metadefender-storage-security-api#settings-getlicense) [POST/api/settings/admin/license/deactivate](/docs/mdss/metadefender-storage-security-api#settings-deactivate) [PUT/api/settings/retention](/docs/mdss/metadefender-storage-security-api#settings-updateretentionsconfig) [GET/api/settings/retention](/docs/mdss/metadefender-storage-security-api#settings-getretentionsconfig) [POST/api/settings/encryption/generate](/docs/mdss/metadefender-storage-security-api#settings-generateencryptionkey) [GET/api/settings/encryption/creation-date](/docs/mdss/metadefender-storage-security-api#settings-getencryptionkeycreationdate) [POST/api/settings/ssl](/docs/mdss/metadefender-storage-security-api#settings-updatesslconfiguration) [GET/api/settings/ssl](/docs/mdss/metadefender-storage-security-api#settings-getsslconfiguration) [POST/api/settings/single-user-session](/docs/mdss/metadefender-storage-security-api#settings-updatesingleusersessionconfiguration) [GET/api/settings/single-user-session](/docs/mdss/metadefender-storage-security-api#settings-getsingleusersession) [GET/api/settings/telemetry](/docs/mdss/metadefender-storage-security-api#settings-getoptelconfiguration) [POST/api/settings/telemetry](/docs/mdss/metadefender-storage-security-api#settings-updateoptelconfiguration)
### Update notifications configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| emailNotificationsConfig EmailNotificationsConfig2 |  |  |  |
| object | object |  |  |
| generatedReportNotificationsConfig GeneratedReportNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: OwnerOnly - 1: AllRegisteredUsers   Enum: `0`,`1` |  |
| userRequestNotificationsConfig UserRequestNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| blockedFileNotificationsConfig BlockedFileNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: AllRegisteredUsers - 1: FileOwner - 2: FileOwnerAndAllRegisteredUsers   Enum: `0`,`1`,`2` |  |
| webhookNotificationsConfig WebhookNotificationsConfig2 |  |  |  |
| object | object |  |  |
| scanCompletedNotificationsConfig ScanCompletedNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| fileScannedNotificationConfig FileScannedNotificationConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| destinationAddress | string |  |  |
| headers | object |  |  |
| * | string |  |  |
| requestType RequestType |  |  |  |
| integer | integer | - 0: Post - 1: Put   Enum: `0`,`1` |  |
| rabbitMqNotificationsConfig RabbitMqNotificationsConfig2 |  |  |  |
| object | object |  |  |
| fileScannedNotificationConfig FileScannedNotificationConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| rabbitMqUrl | string |  |  |
| headers | object |  |  |
| * | string |  |  |

Expand PUT /api/settings/notificationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| newNotificationsConfig NotificationsConfig |  |  |  |
| object | object |  |  |
| id | string |  |  |
| emailNotificationsConfig3 fields | object |  |  |
| userRequestNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| generatedReportNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: OwnerOnly - 1: AllRegisteredUsers   Enum: `0`,`1` |  |
| blockedFileNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: AllRegisteredUsers - 1: FileOwner - 2: FileOwnerAndAllRegisteredUsers   Enum: `0`,`1`,`2` |  |
| webhookNotificationsConfig5 fields | object |  |  |
| scanCompletedNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| fileScannedNotificationConfig | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| destinationAddress | string |  |  |
| headers | object |  |  |
| * | string |  |  |
| requestType | integer | - 0: Post - 1: Put   Enum: `0`,`1` |  |
| rabbitMqNotificationsConfig3 fields | object |  |  |
| fileScannedNotificationConfig | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| rabbitMqUrl | string |  |  |
| headers | object |  |  |
| * | string |  |  |
| initialNotificationsConfig NotificationsConfig |  |  |  |
| object | object |  |  |
| id | string |  |  |
| emailNotificationsConfig3 fields | object |  |  |
| userRequestNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| generatedReportNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: OwnerOnly - 1: AllRegisteredUsers   Enum: `0`,`1` |  |
| blockedFileNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: AllRegisteredUsers - 1: FileOwner - 2: FileOwnerAndAllRegisteredUsers   Enum: `0`,`1`,`2` |  |
| webhookNotificationsConfig5 fields | object |  |  |
| scanCompletedNotificationsConfig | object |  |  |
| isEnabled | boolean |  |  |
| fileScannedNotificationConfig | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| destinationAddress | string |  |  |
| headers | object |  |  |
| * | string |  |  |
| requestType | integer | - 0: Post - 1: Put   Enum: `0`,`1` |  |
| rabbitMqNotificationsConfig3 fields | object |  |  |
| fileScannedNotificationConfig | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| rabbitMqUrl | string |  |  |
| headers | object |  |  |
| * | string |  |  |
| typeResults4 fields | array[object] |  |  |
| type | integer | - 0: Email - 1: Webhook - 2: RabbitMq   Enum: `0`,`1`,`2` |  |
| status | integer | - 0: Success - 1: Failed - 2: Skipped   Enum: `0`,`1`,`2` |  |
| errorKey | string |  |  |
| errorMessage | string |  |  |

Expand  Response
### Get notifications configuration

Auth BearerGET /api/settings/notificationscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| emailNotificationsConfig EmailNotificationsConfig2 |  |  |  |
| object | object |  |  |
| generatedReportNotificationsConfig GeneratedReportNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: OwnerOnly - 1: AllRegisteredUsers   Enum: `0`,`1` |  |
| userRequestNotificationsConfig UserRequestNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| blockedFileNotificationsConfig BlockedFileNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| recipientsType | integer | - 0: AllRegisteredUsers - 1: FileOwner - 2: FileOwnerAndAllRegisteredUsers   Enum: `0`,`1`,`2` |  |
| webhookNotificationsConfig WebhookNotificationsConfig2 |  |  |  |
| object | object |  |  |
| scanCompletedNotificationsConfig ScanCompletedNotificationsConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| fileScannedNotificationConfig FileScannedNotificationConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| destinationAddress | string |  |  |
| headers | object |  |  |
| * | string |  |  |
| requestType RequestType |  |  |  |
| integer | integer | - 0: Post - 1: Put   Enum: `0`,`1` |  |
| rabbitMqNotificationsConfig RabbitMqNotificationsConfig2 |  |  |  |
| object | object |  |  |
| fileScannedNotificationConfig FileScannedNotificationConfig2 |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| notificationScope | integer | - 0: BlockedFilesOnly - 1: AllFiles   Enum: `0`,`1` |  |
| rabbitMqUrl | string |  |  |
| headers | object |  |  |
| * | string |  |  |

Expand  Response
### Update SMTP configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| host | string |  |  |
| port | int32 |  |  |
| baseUrl | string |  |  |
| senderAddress | string |  |  |
| senderName | string | maxLength: 320 |  |
| domain | string |  |  |
| username | string |  |  |
| password | string |  |  |
| secureSocketOption SecureSocketOption |  |  |  |
| integer | integer | - 0: None - 1: Auto - 2: SslOnConnect - 3: StartTls - 4: StartTlsWhenAvailable   Enum: `0`,`1`,`2`,`3`,`4` |  |
| ignoreCertWarnings | boolean |  |  |
| isSmtpEnabled | boolean |  |  |

PATCH /api/settings/smtpcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| newSmtpConfig SmtpConfig |  |  |  |
| object | object |  |  |
| host | string |  |  |
| baseUrl | string |  |  |
| port | int32 |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| username | string |  |  |
| secureSocketOption | integer | - 0: None - 1: Auto - 2: SslOnConnect - 3: StartTls - 4: StartTlsWhenAvailable   Enum: `0`,`1`,`2`,`3`,`4` |  |
| ignoreCertWarnings | boolean |  |  |
| isSmtpEnabled | boolean |  |  |
| replyTo | string |  |  |
| oldSmtpConfig SmtpConfig |  |  |  |
| object | object |  |  |
| host | string |  |  |
| baseUrl | string |  |  |
| port | int32 |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| username | string |  |  |
| secureSocketOption | integer | - 0: None - 1: Auto - 2: SslOnConnect - 3: StartTls - 4: StartTlsWhenAvailable   Enum: `0`,`1`,`2`,`3`,`4` |  |
| ignoreCertWarnings | boolean |  |  |
| isSmtpEnabled | boolean |  |  |
| replyTo | string |  |  |

Expand  Response
### Fetch SMTP configuration

Auth BearerGET /api/settings/smtpcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| host | string |  |  |
| port | int32 |  |  |
| baseUrl | string |  |  |
| senderAddress | string |  |  |
| senderName | string |  |  |
| domain | string |  |  |
| username | string |  |  |
| secureSocketOption | integer | - 0: None - 1: Auto - 2: SslOnConnect - 3: StartTls - 4: StartTlsWhenAvailable   Enum: `0`,`1`,`2`,`3`,`4` |  |
| ignoreCertWarnings | boolean |  |  |
| isSmtpEnabled | boolean |  |  |

 Response
### Online license activation

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| key | string | minLength: 1 |  |

POST /api/settings/admin/license/activate/onlinecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Offline license activation

Auth BearerRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| LicenseContent | file |  |  |

POST /api/settings/admin/license/activate/offlinecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get license details

Auth BearerGET /api/settings/admin/licensecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| apiStatus | string |  |  |

 Response
### Deactivate license

Auth BearerPOST /api/settings/admin/license/deactivatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Update retention configuration

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| retentionAuditDays | int32 | maximum: 50000  minimum: 1 |  |
| reportRetention | object |  |  |
| isEnabled | boolean |  |  |
| retentionDays | int32 | maximum: 50000  minimum: 1 |  |
| rtpHistoryRetention | object |  |  |
| isEnabled | boolean |  |  |
| retentionDays | int32 | maximum: 50000  minimum: 1 |  |

PUT /api/settings/retentioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Fetch retention configuration

Auth BearerGET /api/settings/retentioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| retentionAuditDays | int32 |  |  |
| reportRetentionConfiguration ReportRetention |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| retentionDays | int32 |  |  |
| rtpHistoryRetentionConfiguration ReportRetention |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| retentionDays | int32 |  |  |

 Response
### Generate encryption key

Generate a new encryption key, replacing the old one if it exists.

Auth BearerPOST /api/settings/encryption/generatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get encryption key creation date

Get the creation date of the encryption key.

Auth BearerGET /api/settings/encryption/creation-datecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| creationDate | date-time |  |  |

 Response
### Update SSL configuration

Update SSL configuration of MDSS by uploading a certificate and a key to enable SSL.

Auth BearerRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| SslCertificate | file |  |  |
| SslKey | file |  |  |
| IsEnabled | boolean |  |  |

POST /api/settings/sslcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get SSL configuration

Get current SSL configuration status.

Auth BearerGET /api/settings/sslcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| creationDate | date-time |  |  |

 Response
### Update Single User Session

Update Simultaneous Sessions allowed for a Single User.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| isSingleUserSession | boolean |  |  |

POST /api/settings/single-user-sessioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get Single User Session

Get Simultaneous Sessions allowed for a Single User.

Auth BearerGET /api/settings/single-user-sessioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| creationDate | date-time |  |  |

 Response
### Get Telemetry configuration

Get MDSS Open Telemetry configuration.

Auth BearerGET /api/settings/telemetrycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| telemetryConfig4 fields | object |  |  |
| isEnabled | boolean |  |  |
| sendTelemetryToOpswat | boolean |  |  |
| autoInstrumentation | boolean |  |  |
| optelCollectors3 fields | array[object] |  |  |
| metricEndpoint3 fields | object |  |  |
| endpointUrl | string |  |  |
| endpointApiKey | string |  |  |
| protocol | integer | - 0: GRPC - 1: HTTP   Enum: `0`,`1` |  |
| traceEndpoint3 fields | object |  |  |
| endpointUrl | string |  |  |
| endpointApiKey | string |  |  |
| protocol | integer | - 0: GRPC - 1: HTTP   Enum: `0`,`1` |  |
| isOpswatCollector | boolean |  |  |

 Response
### Update Telemetry configuration

Update MDSS Open Telemetry configuration.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| telemetryConfig4 fields | object |  |  |
| isEnabled | boolean |  |  |
| sendTelemetryToOpswat | boolean |  |  |
| autoInstrumentation | boolean |  |  |
| optelCollectors3 fields | array[object] |  |  |
| metricEndpoint3 fields | object |  |  |
| endpointUrl | string |  |  |
| endpointApiKey | string |  |  |
| protocol | integer | - 0: GRPC - 1: HTTP   Enum: `0`,`1` |  |
| traceEndpoint3 fields | object |  |  |
| endpointUrl | string |  |  |
| endpointApiKey | string |  |  |
| protocol | integer | - 0: GRPC - 1: HTTP   Enum: `0`,`1` |  |
| isOpswatCollector | boolean |  |  |
| userInfo UserInfo |  |  |  |
| object | object |  |  |
| userId | string |  |  |
| userName | string |  |  |

POST /api/settings/telemetrycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
## Sso

Sso Authentication and Sso configuration update

Endpoints[GET/api/sso/config](/docs/mdss/metadefender-storage-security-api#sso-getssoconfiguration) [PATCH/api/sso](/docs/mdss/metadefender-storage-security-api#sso-update)
### Get Sso Configuration

Allows retrieval of the current SSO configuration.

Auth BearerGET /api/sso/configcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| isEnabled | boolean |  |  |
| ssoProvider | integer | - 0: Azure - 1: Okta - 2: Auth0 - 3: Adfs - 4: PingFederate - 5: Opswat   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| ssoType | integer | - 0: OpenIdConnect - 1: Saml2   Enum: `0`,`1` |  |
| baseUrl | string |  |  |
| clientId | string |  |  |
| clientSecret | string |  |  |
| authority | string |  |  |
| identityProviderCertificate | string |  |  |
| identityProviderIssuer | string |  |  |
| loginUrl | string |  |  |
| logoutUrl | string |  |  |
| administratorRoleName | string |  |  |
| readonlyRoleName | string |  |  |

 Response
### Update Sso Configuration

Allows updating the current Sso Configuration.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| clientId | string | maxLength: 255 |  |
| clientSecret | string | maxLength: 255 |  |
| authority | string | maxLength: 255 |  |
| baseUrl | string | maxLength: 255 |  |
| identityProviderIssuer | string | maxLength: 255 |  |
| identityProviderLoginUrl | string | maxLength: 255 |  |
| identityProviderLogoutUrl | string | maxLength: 255 |  |
| identityProviderCertificate | object |  |  |
| content | string |  |  |
| isEnabled | boolean |  |  |
| ssoType | integer | - 0: OpenIdConnect - 1: Saml2   Enum: `0`,`1` |  |
| ssoProvider | integer | - 0: Azure - 1: Okta - 2: Auth0 - 3: Adfs - 4: PingFederate - 5: Opswat   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| administratorRoleName | string | maxLength: 63 |  |
| readonlyRoleName | string | maxLength: 63 |  |

Expand PATCH /api/ssocURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| clientId | string |  |  |
| authority | string |  |  |
| baseUrl | string |  |  |
| isEnabled | boolean |  |  |
| ssoType | integer | - 0: OpenIdConnect   Enum: `0` |  |
| ssoProvider | integer | - 0: Azure - 1: Okta - 2: Auth0 - 3: Adfs - 4: PingFederate   Enum: `0`,`1`,`2`,`3`,`4` |  |
| identityProviderIssuer | string |  |  |
| identityProviderLoginUrl | string |  |  |
| identityProviderLogoutUrl | string |  |  |
| administratorRoleName | string |  |  |
| readonlyRoleName | string |  |  |
| ssoConfig SsoConfig |  |  |  |
| object | object |  |  |
| isEnabled | boolean |  |  |
| ssoProvider | integer | - 0: Azure - 1: Okta - 2: Auth0 - 3: Adfs - 4: PingFederate - 5: Opswat   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| ssoType | integer | - 0: OpenIdConnect - 1: Saml2   Enum: `0`,`1` |  |
| baseUrl | string |  |  |
| clientId | string |  |  |
| clientSecret | string |  |  |
| authority | string |  |  |
| identityProviderCertificate | string |  |  |
| identityProviderIssuer | string |  |  |
| loginUrl | string |  |  |
| logoutUrl | string |  |  |
| administratorRoleName | string |  |  |
| readonlyRoleName | string |  |  |

Expand  Response
## Storage

Manage your storage units

Endpoints[GET/api/storage/{storageId}](/docs/mdss/metadefender-storage-security-api#storage-getstoragebyid) [PATCH/api/storage/{storageId}](/docs/mdss/metadefender-storage-security-api#storage-updatestorage) [DELETE/api/storage/{storageId}](/docs/mdss/metadefender-storage-security-api#storage-deletestorage) [GET/api/storage](/docs/mdss/metadefender-storage-security-api#storage-getstorages) [POST/api/storage](/docs/mdss/metadefender-storage-security-api#storage-addstorage) [PATCH/api/storage](/docs/mdss/metadefender-storage-security-api#storage-movestorages) [DELETE/api/storage](/docs/mdss/metadefender-storage-security-api#storage-bulkdeletestorages) [GET/api/storage/{storageId}/users](/docs/mdss/metadefender-storage-security-api#storage-enumeratestorageusers) [POST/api/storage/batch](/docs/mdss/metadefender-storage-security-api#storage-addstorage2) [GET/api/storage/results](/docs/mdss/metadefender-storage-security-api#storage-getbatchresults) [PUT/api/storage/{storageId}/scan_schedule](/docs/mdss/metadefender-storage-security-api#storage-addscanschedule) [PUT/api/storage/scan_schedule/update/{storageId}](/docs/mdss/metadefender-storage-security-api#storage-updatescanschedule) [GET/api/storage/scan_schedules/{sortDirection}/{startIndex}/{count}](/docs/mdss/metadefender-storage-security-api#storage-enumeratescanschedules) [DELETE/api/storage/scan_schedule](/docs/mdss/metadefender-storage-security-api#storage-deletescanschedules) [GET/api/storage/{storageId}/user](/docs/mdss/metadefender-storage-security-api#storage-retrieveusernamefromstoragewithuseridparam) [GET/api/storage/{storageId}/{userId}](/docs/mdss/metadefender-storage-security-api#storage-retrieveusernamefromstorage)
### Fetch storage by ID

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

GET /api/storage/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| storage Storage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |

Expand  Response
### Update a storage

**Note! The following are templates for what is expected in the Credentials, CredentialsFile and Source fields. Please provide the correct values for your storage integration instead of null/false**

**Alibaba Cloud storage units:**
Credentials: "{"Endpoint":null,"AccessKeyId":null,"AccessKeySecret":null,"UseRamRole":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Amazon S3 / S3 Compatible storage units:**
Credentials: "{"ServiceUrl":null,"AccessKeyId":null,"SecretAccessKey":null,"RegionEndpoint":null,"AssumeRoleArn":null,"UseIamRole":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Azure Blob storage units:**
Credentials: "{"TenantId":null,"ClientId":null,"ClientSecret":null,"StorageAccount":null}"
Source: "{"Container":null}"

**Azure Files storage units:**
Credentials: "{"AccountName":null,"AccountKey":null,"ShareName":null}"
Source: "{"FolderLocation":null}"

**Box storage units:**
CredentialsFile: upload the credentials file
Source: "{"FolderLocation":null}"

**Dell Isilon / SMB Compatible storage units:**
Credentials: "{"User":null,"Password":null,"Server":null}"
Source: "{"SharePath":null}"

**Google Cloud storage units:**
CredentialsFile: upload the credentials file
Credentials: "{"UseAdc":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Graph storage units:**
Credentials: "{"TenantId":null,"ClientId":null,"ClientSecret":null}"
Source: "{"Group":null}"

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Request Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| Name | string |  |  |
| StorageVendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| StorageProtocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| CredentialsFile | file |  |  |
| Credentials | string |  |  |
| Source | string |  |  |
| GroupId | string |  |  |
| AccountId | string |  |  |
| WorkflowId | string |  |  |
| TransferMetadataAndChecksum | boolean |  |  |

Expand PATCH /api/storage/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| updatedStorage NewStorage |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| groupId | string |  |  |
| clientId | string |  |  |
| accountId | string |  |  |
| source | string |  |  |
| storageFunctionality | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk - 100: GitHubSdk - 101: DockerHubSdk - 102: BitbucketSdk - 103: AmazonEcrSdk - 104: QuaySdk - 105: JFrogContainerSdk - 106: JFrogBinarySdk - 107: AzureAcrSdk - 108: GitLabSourceSdk - 109: GitLabContainerSdk - 110: SvnSdk - 111: AzureDevOpsSourceSdk - 112: AzureDevOpsBinarySdk - 113: DirectFile - 114: NexusBinarySdk - 115: GiteaSdk - 116: HarborSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing - 100: GitHub - 101: DockerHub - 102: Bitbucket - 103: AmazonEcr - 104: Quay - 105: JFrogContainer - 106: JFrogBinary - 107: AzureAcr - 108: GitLabSource - 109: GitLabContainer - 110: Svn - 111: AzureDevOpsSource - 112: AzureDevOpsBinary - 113: DirectFile - 114: NexusBinary - 115: Gitea - 116: Harbor   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22`,`100`,`101`,`102`,`103`,`104`,`105`,`106`,`107`,`108`,`109`,`110`,`111`,`112`,`113`,`114`,`115`,`116` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | integer | - 0: NotTested - 1: Testing - 2: Operational - 3: Error   Enum: `0`,`1`,`2`,`3` |  |
| workflowId | string |  |  |
| lastUpdated | date-time |  |  |
| tenantId | string |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| isAutodiscovered | boolean |  |  |

Expand  Response
### Delete a storage

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/storage/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| scansRunning | boolean |  |  |
| runningScans4 fields | array[object] |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| accountId | string |  |  |
| groupId | string |  |  |

 Response
### List storage units (paginated, filtered, sorted)

Returns a paginated, filtered, and sorted list of storage units. Supports multi-value comma-separated filters: status (StorageStatusType), vendorType (StorageVendorType), protocolType (StorageProtocolType), accountId, and groupId. The name filter performs a case-insensitive substring (ILIKE) match. Sorting is configurable by id or name. Default Count is 100 (maximum 100). Returns an IPagedResponse containing Items, TotalCount, StartIndex, and Count.

Auth BearerQuery String

| Name | string |  |  |
| --- | --- | --- | --- |
| Status | array |  |  |
| VendorType | array |  |  |
| ProtocolType | array |  |  |
| AccountId | array |  |  |
| GroupId | array |  |  |
| StartIndex | integer | maximum: 2147483647  minimum: 0 |  |
| Count | integer | maximum: 100  minimum: 1 |  |
| SortBy | array | Enum: `0`,`1` |  |
| SortOrder | array | Enum: `0`,`1` |  |

GET /api/storagecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| items14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| entries14 fields | array[object] | Deprecated |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |
| totalCount | int32 |  |  |
| startIndex | int32 |  |  |
| count | int32 |  |  |

 Response
### Add a storage

**Note! The following are templates for what is expected in the Credentials, CredentialsFile and Source fields. Please provide the correct values for your storage integration instead of null/false**

**Alibaba Cloud storage units:**
Credentials: "{"Endpoint":null,"AccessKeyId":null,"AccessKeySecret":null,"UseRamRole":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Amazon S3 / S3 Compatible storage units:**
Credentials: "{"ServiceUrl":null,"AccessKeyId":null,"SecretAccessKey":null,"RegionEndpoint":null,"AssumeRoleArn":null,"UseIamRole":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Azure Blob storage units:**
Credentials: "{"TenantId":null,"ClientId":null,"ClientSecret":null,"StorageAccount":null}"
Source: "{"Container":null}"

**Azure Files storage units:**
Credentials: "{"AccountName":null,"AccountKey":null,"ShareName":null}"
Source: "{"FolderLocation":null}"

**Box storage units:**
CredentialsFile: upload the credentials file
Source: "{"FolderLocation":null}"

**Dell Isilon / SMB Compatible storage units:**
Credentials: "{"User":null,"Password":null,"Server":null}"
Source: "{"SharePath":null}"

**Google Cloud storage units:**
CredentialsFile: upload the credentials file
Credentials: "{"UseAdc":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Graph storage units:**
Credentials: "{"TenantId":null,"ClientId":null,"ClientSecret":null}"
Source: "{"Group":null}"

Auth BearerRequest Body multipart/form-data

| object | object |  |  |
| --- | --- | --- | --- |
| Id | string |  |  |
| StorageClientId | string |  |  |
| Name | string |  |  |
| StorageVendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| StorageProtocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| CredentialsFile | file |  |  |
| Credentials | string |  |  |
| Source | string |  |  |
| GroupId | string |  |  |
| AccountId | string |  |  |
| WorkflowId | string |  |  |
| TransferMetadataAndChecksum | boolean |  |  |

Expand POST /api/storagecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| storageId | string |  |  |

 Response
### Bulk move storages to a target group

Moves up to 100 storages to a target group in a single request. Per-storage ABAC (Write) is enforced — inaccessible storage IDs are returned in the failed list with a localized reason. The target group must exist and be accessible; otherwise the entire request fails with a localized 'target group not found' response.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageIds | array[string] |  |  |
| targetGroupId | string |  |  |

PATCH /api/storagecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| targetGroupId | string |  |  |

 Response
### Bulk delete storages

Deletes up to 100 storages in a single request. Per-storage ABAC is enforced — inaccessible storage IDs are returned in the failed list with a localized reason. If any of the target storages has a running scan, the request is rejected with HTTP 409 and the runningScans list. Otherwise, all scans associated with the target storages are deleted as part of the cascade before the storage rows are removed.

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| storageIds | array[string] |  |  |

DELETE /api/storagecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |
| scansRunning | boolean |  |  |
| runningScans4 fields | array[object] |  |  |
| scanId | string |  |  |
| storageId | string |  |  |
| accountId | string |  |  |
| groupId | string |  |  |

 Response
### Fetch storage users

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Query String

| filter | string |  |  |
| --- | --- | --- | --- |

GET /api/storage/{storageId}/userscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries | array[object] |  |  |
| id | string |  |  |
| fullName | string |  |  |

 Response
### Add batch of storages

**Note! The following are templates for what is expected in the Credentials, CredentialsFile and Source fields. Please provide the correct values for your storage integration instead of null/false**

**Alibaba Cloud storage units:**
Credentials: "{"Endpoint":null,"AccessKeyId":null,"AccessKeySecret":null,"UseRamRole":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Amazon S3 / S3 Compatible storage units:**
Credentials: "{"ServiceUrl":null,"AccessKeyId":null,"SecretAccessKey":null,"RegionEndpoint":null,"AssumeRoleArn":null,"UseIamRole":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Azure Blob storage units:**
Credentials: "{"TenantId":null,"ClientId":null,"ClientSecret":null,"StorageAccount":null}"
Source: "{"Container":null}"

**Azure Files storage units:**
Credentials: "{"AccountName":null,"AccountKey":null,"ShareName":null}"
Source: "{"FolderLocation":null}"

**Box storage units:**
CredentialsFile: upload the credentials file
Source: "{"FolderLocation":null}"

**Dell Isilon / SMB Compatible storage units:**
Credentials: "{"User":null,"Password":null,"Server":null}"
Source: "{"SharePath":null}"

**Google Cloud storage units:**
CredentialsFile: upload the credentials file
Credentials: "{"UseAdc":false}"
Source: "{"BucketName":null,"FolderLocation":null}"

**Graph storage units:**
Credentials: "{"TenantId":null,"ClientId":null,"ClientSecret":null}"
Source: "{"Group":null}"

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| addStorageParametersList12 fields | array[object] |  |  |
| id | string |  |  |
| storageClientId | string |  |  |
| name | string | maxLength: 60  minLength: 3  pattern: `^[^@#$%&*"';:.|,{}?+=><`~^[]!\]+$` |  |
| storageVendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageProtocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| credentialsFile | file |  |  |
| credentials | string |  |  |
| source | string | minLength: 1 |  |
| groupId | string | minLength: 1 |  |
| accountId | string |  |  |
| workflowId | string |  |  |
| transferMetadataAndChecksum | boolean |  |  |

POST /api/storage/batchcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| storageId | string |  |  |

 Response
### Get batch of add storages results

Auth BearerQuery String

| token | string |  |  |
| --- | --- | --- | --- |

GET /api/storage/resultscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| addStorageResultInfos | array |  |  |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| source | string |  |  |
| name | string |  |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| isCompleted | boolean |  |  |

 Response
### Add a scan schedule

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | minLength: 1  pattern: `^[^@#$%&*"';:.|,{}?+=><`~^[]!\]+$` |  |
| workflowId | string | minLength: 1 |  |
| recurrencePattern9 fields | object |  |  |
| type | string |  |  |
| minutelyRecurrence MinutelyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfMinutes | int32 | maximum: 60  minimum: 5 |  |
| hourlyRecurrence HourlyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfHours | int32 | maximum: 24  minimum: 1 |  |
| dailyRecurrence DailyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfDays | int32 | maximum: 365  minimum: 1 |  |
| weeklyRecurrence WeeklyRecurrenceParameters |  |  |  |
| object | object |  |  |
| daysOfWeek | array[integer] | Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6` |  |
| everyNumberOfWeeks | int32 |  |  |
| monthlyRecurrence MonthlyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfMonths | int32 | maximum: 12  minimum: 1 |  |
| dayOfMonth | int32 | maximum: 30  minimum: 1 |  |
| startDate | date-time |  |  |
| timeToStart | date-time |  |  |
| avoidConcurrentScheduleRuns | boolean |  |  |
| scanPartition | string |  |  |
| priority | int32 |  |  |
| $type | string |  |  |

PUT /api/storage/{storageId}/scan_schedulecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Update a scan schedule

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| name | string | minLength: 1  pattern: `^[^@#$%&*"';:.|,{}?+=><`~^[]!\]+$` |  |
| workflowId | string | minLength: 1 |  |
| recurrencePattern9 fields | object |  |  |
| type | string |  |  |
| minutelyRecurrence MinutelyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfMinutes | int32 | maximum: 60  minimum: 5 |  |
| hourlyRecurrence HourlyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfHours | int32 | maximum: 24  minimum: 1 |  |
| dailyRecurrence DailyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfDays | int32 | maximum: 365  minimum: 1 |  |
| weeklyRecurrence WeeklyRecurrenceParameters |  |  |  |
| object | object |  |  |
| daysOfWeek | array[integer] | Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6` |  |
| everyNumberOfWeeks | int32 |  |  |
| monthlyRecurrence MonthlyRecurrenceParameters |  |  |  |
| object | object |  |  |
| everyNumberOfMonths | int32 | maximum: 12  minimum: 1 |  |
| dayOfMonth | int32 | maximum: 30  minimum: 1 |  |
| startDate | date-time |  |  |
| timeToStart | date-time |  |  |
| avoidConcurrentScheduleRuns | boolean |  |  |
| scanPartition | string |  |  |
| priority | int32 |  |  |
| $type | string |  |  |
| id | string |  |  |

PUT /api/storage/scan_schedule/update/{storageId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Fetch scan schedules

Auth BearerPath Params

| sortDirection | integer | Enum: `0`,`1` |  |
| --- | --- | --- | --- |
| startIndex | integer | maximum: 2147483647  minimum: 0 |  |
| count | integer | maximum: 2147483647  minimum: 1 |  |

Query String

| name | string | pattern: `^[^@#$%&*"';:.|,{}?+=><`~^[]!\]+$` |  |
| --- | --- | --- | --- |
| user | string | pattern: `^[\p{L}\p{M} ',.-]+$` |  |
| type | string |  |  |
| storageId | string |  |  |

GET /api/storage/scan_schedules/{sortDirection}/{startIndex}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries13 fields | array[object] |  |  |
| id | string |  |  |
| name | string |  |  |
| workflowId | string | WorkflowId required if ScanConfigurationId is null  minLength: 1 |  |
| scanConfigurationId | string | This property is obsolete and will be removed in the future. Use WorkflowId instead. |  |
| type | string |  |  |
| scanPartition | string |  |  |
| createdAt | date-time |  |  |
| lastScanTime | date-time |  |  |
| nextScanTime | date-time |  |  |
| recurrencePatternDto RecurrencePattern |  |  |  |
| object | object |  |  |
| type | integer | - 0: Hourly - 1: Daily - 2: Weekly - 3: Monthly - 4: Minutely   Enum: `0`,`1`,`2`,`3`,`4` |  |
| minutelyRecurrence MinutelyRecurrence |  |  |  |
| object | object |  |  |
| everyNumberOfMinutes | int32 |  |  |
| hourlyRecurrence HourlyRecurrence |  |  |  |
| object | object |  |  |
| everyNumberOfHours | int32 |  |  |
| dailyRecurrence DailyRecurrence |  |  |  |
| object | object |  |  |
| everyNumberOfDays | int32 |  |  |
| weeklyRecurrence WeeklyRecurrence |  |  |  |
| object | object |  |  |
| daysOfWeek | array[integer] | Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6` |  |
| everyNumberOfWeeks | int32 |  |  |
| monthlyRecurrence MonthlyRecurrence |  |  |  |
| object | object |  |  |
| everyNumberOfMonths | int32 |  |  |
| dayOfMonth | int32 |  |  |
| startDate | date-time |  |  |
| timeToStart | date-time |  |  |
| avoidConcurrentScheduleRuns | boolean |  |  |
| createdBy | string |  |  |
| priority | integer | - 0: Low - 1: Medium - 2: High   Enum: `0`,`1`,`2` |  |
| storageId | string |  |  |
| totalCount | int64 |  |  |

 Response
### Delete scan schedules

Deletes up to 100 scan schedule records in a single request. Per-schedule ABAC (Storages.Delete on the schedule's storage) is enforced — inaccessible IDs are returned in the failed list with a localized reason. Schedules that don't exist are also returned in the failed list with reasonKey BULK_OPERATION_ITEM_NOT_FOUND.

Auth BearerRequest Body application/json

| array | array[string] |  |  |
| --- | --- | --- | --- |

DELETE /api/storage/scan_schedulecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| succeeded | array[string] |  |  |
| failed4 fields | array[object] |  |  |
| id | string |  |  |
| reasonKey | string |  |  |
| reason | string |  |  |
| childFailures | array[object] |  |  |

 Response
### Retrieve storage user name

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |

Query String

| userId | string |  |  |
| --- | --- | --- | --- |

GET /api/storage/{storageId}/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| userName | string |  |  |

 Response
### Retrieve storage user name

Auth BearerPath Params

| storageId | string |  |  |
| --- | --- | --- | --- |
| userId | string |  |  |

GET /api/storage/{storageId}/{userId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| userName | string |  |  |

 Response
## User

Create, list and update user accounts

Endpoints[GET/api/user/active/{startIndex}/{count}](/docs/mdss/metadefender-storage-security-api#user-enumerateactiveusers) [POST/api/user/register](/docs/mdss/metadefender-storage-security-api#user-register) [POST/api/user/create](/docs/mdss/metadefender-storage-security-api#user-create) [POST/api/user/authenticate](/docs/mdss/metadefender-storage-security-api#user-authenticate) [GET/api/user/me](/docs/mdss/metadefender-storage-security-api#user-getcurrentuserinfo) [POST/api/user/refreshToken](/docs/mdss/metadefender-storage-security-api#user-refresh) [POST/api/user/logout](/docs/mdss/metadefender-storage-security-api#user-logout) [PUT/api/user/role](/docs/mdss/metadefender-storage-security-api#user-updateuserrole) [GET/api/user/requests](/docs/mdss/metadefender-storage-security-api#user-enumerateuserrequests) [DELETE/api/user/{userId}](/docs/mdss/metadefender-storage-security-api#user-delete) [PUT/api/user](/docs/mdss/metadefender-storage-security-api#user-update) [POST/api/user/password/reset](/docs/mdss/metadefender-storage-security-api#user-requestpasswordreset) [POST/api/user/password](/docs/mdss/metadefender-storage-security-api#user-passwordreset) [GET/api/user/{userId}/permissions](/docs/mdss/metadefender-storage-security-api#user-getuserpermissions)
### Fetch active users

Auth BearerPath Params

| startIndex | string |  |  |
| --- | --- | --- | --- |
| count | string |  |  |

Query String

| searchTerm | string | pattern: `^[\p{L}\p{M} ',.-]+$` |  |
| --- | --- | --- | --- |
| orderType |  |  |  |
| orderBy |  |  |  |
| searchText | string | pattern: `^[\p{L}\p{M} ',.-]+$` |  |

GET /api/user/active/{startIndex}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| entries6 fields | array[object] |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| roles4 fields | array[object] |  |  |
| bindingId | string |  |  |
| roleId | string |  |  |
| roleName | string |  |  |
| expiresAt | date-time |  |  |
| directPermissions3 fields | array[object] |  |  |
| id | string |  |  |
| permissionName | string |  |  |
| expiresAt | date-time |  |  |
| totalCount | int64 |  |  |

 Response
### Register a user

Auth NoneRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| fullName | string | minLength: 1 |  |
| userName | string | minLength: 1 |  |
| password | string |  |  |
| email | string | minLength: 1 |  |
| ssoUserId | string |  |  |

POST /api/user/registercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Create a user

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| fullName | string | minLength: 1 |  |
| userName | string | minLength: 1 |  |
| password | string |  |  |
| email | string | minLength: 1 |  |
| ssoUserId | string |  |  |
| role | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |

POST /api/user/createcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Authenticate with a username and password

Authenticate with a username and password to obtain a JWT token,Most of the APIs require authentication in the form of providing a JWT token. Call this API in order to receive a token but please note that it's only valid for an hour so it should be periodically refreshed.

Auth NoneRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| userName | string | login name of the user  minLength: 1 |  |
| password | string | password  minLength: 1 |  |

POST /api/user/authenticatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| userName | string |  |  |
| role UserRole |  |  |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| user UserDto |  |  |  |
| object | object |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role UserRole |  | Deprecated |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| roles | array[string] |  |  |
| tenantId | string |  |  |
| ssoUserId | string |  |  |
| passwordHash | string |  |  |
| passwordSalt | string |  |  |
| passwordHashAlgorithm | int32 |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |
| userId | string |  |  |

Expand  Response
### Fetch current user information

Retrieve information about the currently authenticated user.

Auth BearerGET /api/user/mecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| username | string |  |  |
| email | string |  |  |
| authProvider | string |  |  |
| role | string |  |  |
| id | string |  |  |
| roles4 fields | array[object] |  |  |
| bindingId | string |  |  |
| roleId | string |  |  |
| roleName | string |  |  |
| expiresAt | date-time |  |  |
| directPermissions3 fields | array[object] |  |  |
| id | string |  |  |
| permissionName | string |  |  |
| expiresAt | date-time |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |

 Response
### Refresh user token

Refresh an expired accessToken using a valid refreshToken

Auth NonePOST /api/user/refreshTokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Logout

Auth BearerPOST /api/user/logoutcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### Update user role

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| userId | string | minLength: 1 |  |
| role | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |

PUT /api/user/rolecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| user UserDto |  |  |  |
| object | object |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role UserRole |  | Deprecated |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| roles | array[string] |  |  |
| tenantId | string |  |  |
| ssoUserId | string |  |  |
| passwordHash | string |  |  |
| passwordSalt | string |  |  |
| passwordHashAlgorithm | int32 |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |

Expand  Response
### Fetch users

Auth BearerQuery String

| startIndex | integer | maximum: 2147483647  minimum: 0 |  |
| --- | --- | --- | --- |
| count | integer | maximum: 2147483647  minimum: 1 |  |
| orderType |  |  |  |
| orderBy |  |  |  |
| searchText | string | pattern: `^[\p{L}\p{M} ',.-]+$` |  |

GET /api/user/requestscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| entries12 fields | array[object] |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role UserRole |  | Deprecated |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| roles | array[string] |  |  |
| tenantId | string |  |  |
| ssoUserId | string |  |  |
| passwordHash | string |  |  |
| passwordSalt | string |  |  |
| passwordHashAlgorithm | int32 |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |
| totalCount | int64 |  |  |

 Response
### Delete a user

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |

DELETE /api/user/{userId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| user UserDto |  |  |  |
| object | object |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role UserRole |  | Deprecated |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| roles | array[string] |  |  |
| tenantId | string |  |  |
| ssoUserId | string |  |  |
| passwordHash | string |  |  |
| passwordSalt | string |  |  |
| passwordHashAlgorithm | int32 |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |

Expand  Response
### Update current user

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| userId | string |  |  |
| role | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| userName | string |  |  |
| fullName | string |  |  |
| currentPassword | string |  |  |
| newPassword | string |  |  |
| email | string |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |

PUT /api/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| user UserDto |  |  |  |
| object | object |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role UserRole |  | Deprecated |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| roles | array[string] |  |  |
| tenantId | string |  |  |
| ssoUserId | string |  |  |
| passwordHash | string |  |  |
| passwordSalt | string |  |  |
| passwordHashAlgorithm | int32 |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |

Expand  Response
### Request password reset

Auth NoneRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| userInput | string | minLength: 1 |  |

POST /api/user/password/resetcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Reset user password

Auth NoneRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| newPassword | string | minLength: 12 |  |
| newPasswordConfirmation | string | minLength: 12 |  |
| secureToken | string |  |  |

POST /api/user/passwordcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| user UserDto |  |  |  |
| object | object |  |  |
| id | string |  |  |
| userName | string |  |  |
| fullName | string |  |  |
| email | string |  |  |
| role UserRole |  | Deprecated |  |
| integer | integer | - 0: None - 1: ReadOnlyAdministrator - 2: Administrator - 4: SsoAdministrator - 5: SsoReadOnlyAdministrator - 6: TenantAdministrator - 999: Invalid   Enum: `0`,`1`,`2`,`4`,`5`,`6`,`999` |  |
| roles | array[string] |  |  |
| tenantId | string |  |  |
| ssoUserId | string |  |  |
| passwordHash | string |  |  |
| passwordSalt | string |  |  |
| passwordHashAlgorithm | int32 |  |  |
| preferences UserPreferences |  |  |  |
| object | object |  |  |
| theme | integer | - 0: Light - 1: Dark - 2: System - 3: Company   Enum: `0`,`1`,`2`,`3` |  |
| language | integer | - 0: En - 1: Jp   Enum: `0`,`1` |  |

Expand  Response
### Get User Permissions

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |

GET /api/user/{userId}/permissionscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| roles4 fields | array[object] |  |  |
| bindingId | string |  |  |
| roleId | string |  |  |
| roleName | string |  |  |
| expiresAt | date-time |  |  |
| directPermissions3 fields | array[object] |  |  |
| id | string |  |  |
| permissionName | string |  |  |
| expiresAt | date-time |  |  |

 Response
## User Tour

Finalize and list user tours

Endpoints[GET/api/usertour/{userId}](/docs/mdss/metadefender-storage-security-api#usertour-getusertours) [POST/api/usertour/finalizeUserTour](/docs/mdss/metadefender-storage-security-api#usertour-finalizeusertour)
### Fetch tours completed by a user

Auth BearerPath Params

| userId | string |  |  |
| --- | --- | --- | --- |

GET /api/usertour/{userId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| userId | string |  |  |
| userTours | array[object] |  |  |
| tourType | integer | - 0: OnboardingUi - 1: WorkflowUi - 2: StorageUnits   Enum: `0`,`1`,`2` |  |
| finalizedDate | date-time |  |  |

 Response
### Mark a specific Tour as completed by a user

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| userId | string | minLength: 1 |  |
| userTourType | integer | - 0: OnboardingUi - 1: WorkflowUi - 2: StorageUnits   Enum: `0`,`1`,`2` |  |

POST /api/usertour/finalizeUserTourcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
## Webhook

Endpoints[POST/api/webhook/realtime](/docs/mdss/metadefender-storage-security-api#webhook-eventhandler) [POST/api/webhook/realtime/{storageClientId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlerbystorageclientid) [POST/api/webhook/realtime/{storageClientId}/{scanId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlerbystorageclientid2) [POST/api/webhook/realtime/public/{storageClientId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlerbystorageclientidpublic) [POST/api/webhook/realtime/public/{storageClientId}/{scanId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlerbystorageclientidpublic2) [POST/api/webhook/realtime/public/{tenantId}/{storageClientId}/{scanId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlerbystorageclientidpublic3) [POST/api/webhook/realtime/graph/{storageClientId}/{scanId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlergraphnotification) [POST/api/webhook/realtime/graph/{tenantId}/{storageClientId}/{scanId}](/docs/mdss/metadefender-storage-security-api#webhook-eventhandlergraphnotification2)
### File event trigger of real time processing

This endpoint takes the parameters and tries to find the file in the specified storage and applies the workflow for the specified file

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| metadata | string | minLength: 1 |  |
| storageClientId | string | minLength: 1 |  |
| scanId | string |  |  |

POST /api/webhook/realtimecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| correlationId | string |  |  |

400404 Response
### File event trigger of real time processing by storage client ID

This endpoint takes the parameter and tries to find the file in the specified storage and applies the workflow for the specified file

Auth BearerPath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/{storageClientId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| correlationId | string |  |  |

400404 Response
### File event trigger of real time processing by storage client ID

This endpoint takes the parameter and tries to find the file in the specified storage and applies the workflow for the specified file

Auth BearerPath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/{storageClientId}/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| correlationId | string |  |  |

400404 Response
### File event trigger of real time processing for Box

This endpoint takes the parameter and tries to find the file in the specified Box storage and applies the workflow for the specified file

Auth NonePath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/public/{storageClientId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| correlationId | string |  |  |

400404 Response
### File event trigger of real time processing for Box

This endpoint takes the parameter and tries to find the file in the specified Box storage and applies the workflow for the specified file

Auth NonePath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/public/{storageClientId}/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| correlationId | string |  |  |

400404 Response
### File event trigger of real time processing for Box

This endpoint takes the parameter and tries to find the file in the specified Box storage and applies the workflow for the specified file

Auth NonePath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |
| tenantId | string |  |  |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/public/{tenantId}/{storageClientId}/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| correlationId | string |  |  |

400404 Response
### {scanId}

Auth NonePath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |

Query String

| validationToken | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/graph/{storageClientId}/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
### {scanId}

Auth NonePath Params

| storageClientId | string |  |  |
| --- | --- | --- | --- |
| scanId | string |  |  |
| tenantId | string |  |  |

Query String

| validationToken | string |  |  |
| --- | --- | --- | --- |

Request Body application/json

| No request body |
| --- |

POST /api/webhook/realtime/graph/{tenantId}/{storageClientId}/{scanId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

| file | file |  |  |
| --- | --- | --- | --- |

 Response
## Workflow

List, add, update and delete Workflows

Endpoints[GET/api/workflow](/docs/mdss/metadefender-storage-security-api#workflow-getworkflows) [POST/api/workflow](/docs/mdss/metadefender-storage-security-api#workflow-addworkflow) [PATCH/api/workflow](/docs/mdss/metadefender-storage-security-api#workflow-updateworkflow) [GET/api/workflow/{id}](/docs/mdss/metadefender-storage-security-api#workflow-getworkflowbyid) [DELETE/api/workflow/{id}](/docs/mdss/metadefender-storage-security-api#workflow-deleteworkflowbyid) [POST/api/workflow/setDefault/{id}](/docs/mdss/metadefender-storage-security-api#workflow-setdefaultworkflow) [POST/api/workflow/enabledTechnologies](/docs/mdss/metadefender-storage-security-api#workflow-enabledtechnologies)
### Get Workflows

Auth BearerGET /api/workflowcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries17 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| scanPoolHasApiKey | object |  |  |
| * | boolean |  |  |

 Response
### Add a new Workflow

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| scanPoolId | string |  |  |
| rules | array[string] |  |  |
| name | string | maxLength: 60  minLength: 3 |  |
| userAgent | string |  |  |
| failOverScanPoolId | string |  |  |
| filters AddFilters |  |  |  |
| object | object |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | integer | maximum: 365  minimum: 1 |  |

POST /api/workflowcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| workflowId | string |  |  |

 Response
### Update an existing Workflow

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| id | string | minLength: 1 |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| rules | array[string] |  |  |
| name | string | maxLength: 60  minLength: 3 |  |
| userAgent | string |  |  |
| failOverScanPoolId | string |  |  |
| failOverDisabled | boolean |  |  |
| filters UpdateFilters |  |  |  |
| object | object |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | integer | maximum: 365  minimum: 1 |  |

Expand PATCH /api/workflowcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Get Workflow by ID

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

GET /api/workflow/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entry Workflow |  |  |  |
| object | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |
| scanPoolHasApiKey | object |  |  |
| * | boolean |  |  |

Expand  Response
### Delete a Workflow

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

DELETE /api/workflow/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Set a Workflow as default

Auth BearerPath Params

| id | string |  |  |
| --- | --- | --- | --- |

POST /api/workflow/setDefault/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |

 Response
### Refresh supported technologies for a Workflow and return updated Workflow

Auth BearerRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| workflowId | string |  |  |

POST /api/workflow/enabledTechnologiescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| workflowDto Workflow |  |  |  |
| object | object |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| scanProcessFlow ScanProcessFlow |  |  |  |
| integer | integer | - 0: WithScanning - 1: WithoutScanning   Enum: `0`,`1` |  |
| isIdentityScanningEnabled | boolean |  |  |
| scanIntervalDays | int32 |  |  |
| rules | array[string] |  |  |
| type | integer | - 0: Default - 1: Basic   Enum: `0`,`1` |  |
| workflowSupportedTechnologies WorkflowSupportedTechnologies |  |  |  |
| object | object |  |  |
| dlp | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| deepCdr | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| sandBox | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| metascan | object |  |  |
| status | integer | - 0: Unknown - 1: Disabled - 2: Enabled   Enum: `0`,`1`,`2` |  |
| name | string |  |  |
| userAgent | string |  |  |
| scanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| failOverScanPoolId | string |  |  |
| failOverScanPool ScanPool |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| scanPoolType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| isDefault | boolean |  |  |
| scanInstances6 fields | array[object] |  |  |
| id | string |  |  |
| scanPoolId | string |  |  |
| url | string |  |  |
| apiKey | string |  |  |
| timeout | string |  |  |
| scanInstanceType | integer | - 0: MdCore - 1: MdCloud   Enum: `0`,`1` |  |
| filters5 fields | object |  |  |
| id | string |  |  |
| minimumSize | int64 |  |  |
| maximumSize | int64 |  |  |
| minimumDateTime | date-time |  |  |
| maximumDateTime | date-time |  |  |
| fileDefinition FileDefinition |  |  |  |
| object | object |  |  |
| blockingStrategy | integer | - 0: Strict - 1: Configurable   Enum: `0`,`1` |  |
| configurableBlockingStrategy | object |  |  |
| shouldTreatFilesWithSensitiveDataAsBlocked | boolean |  |  |
| shouldTreatFilesWithVulnerabilitiesAsBlocked | boolean |  |  |
| remediations6 fields | array[object] |  |  |
| id | string |  |  |
| workflowId | string |  |  |
| isEnabled | boolean |  |  |
| configuration | string |  |  |
| type | integer | - 0: FileTagging - 1: DeepCdr - 2: BlockedFileRemediation - 3: AllowedSanitizedFileRemediation - 4: AllowedFileRemediation - 5: BlockedSanitizedFileRemediation - 6: DeleteEmptyFoldersRemediation - 7: ScanFileVersions - 8: DiscoveredFileRemediation - 9: AllowedCdrUnsupportedFileRemediation - 10: BlockedCdrUnsupportedFileRemediation   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10` |  |
| handlingType | integer | - 0: Delete - 1: Move - 2: Copy - 3: Keep - 999: NotApplicable   Enum: `0`,`1`,`2`,`3`,`999` |  |
| tenantId | string |  |  |

Expand  Response
## Deprecated Soon To Be Removed

Endpoints[GET/api/account/count](/docs/mdss/metadefender-storage-security-api#account-getaccountcount) [GET/api/storage/all](/docs/mdss/metadefender-storage-security-api#storage-enumeratestorages) [GET/api/storage/enumerate/{startIndex}/{count}](/docs/mdss/metadefender-storage-security-api#storage-enumeratestorageswithfilters)
### Fetch the number of accountsDeprecated

Get the total number of accounts in the system

Auth BearerGET /api/account/countcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| accountCount | object |  |  |
| count | int64 |  |  |

 Response
### Fetch all storage unitsDeprecated

Auth BearerGET /api/storage/allcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |

 Response
### Fetch all storage units by filters (storage type or status)Deprecated

Auth BearerPath Params

| startIndex | string |  |  |
| --- | --- | --- | --- |
| count | string |  |  |

Query String

| sortingOrder | string |  |  |
| --- | --- | --- | --- |
| search | string |  |  |
| storageType | integer |  |  |
| storageStatus | integer |  |  |

GET /api/storage/enumerate/{startIndex}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

| object | object |  |  |
| --- | --- | --- | --- |
| result | integer | - 0: Success - 1: Error - 2: InternalError - 3: NotFound - 4: Forbidden - 5: Conflict   Enum: `0`,`1`,`2`,`3`,`4`,`5` |  |
| responseKey | string |  |  |
| responseMessage | string |  |  |
| responseMessageParams | object |  |  |
| * | string |  |  |
| entries14 fields | array[object] |  |  |
| id | string |  |  |
| groupId | string |  |  |
| accountId | string |  |  |
| name | string |  |  |
| storageClientId | string |  |  |
| storageType4 fields | object |  |  |
| name | string |  |  |
| categoryType | integer | - 0: Local - 1: Cloud - 2: Object   Enum: `0`,`1`,`2` |  |
| protocolType | integer | - 0: Smb - 1: GraphSdk - 2: BoxSdk - 3: AwsSdk - 4: AzureBlobSdk - 5: AlibabaCloudSdk - 6: GoogleCloudSdk - 7: AzureFilesSdk - 8: Sftp - 9: Nfs - 10: Mft - 11: SharepointOnPrem - 12: Ftp - 13: OracleSdk   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13` |  |
| vendorType | integer | - 0: AmazonS3 - 1: OneDrive - 2: Box - 3: DellIsilon - 4: AzureFiles - 5: SmbCompatible - 6: S3Compatible - 7: AzureBlob - 8: AlibabaCloud - 9: GoogleCloud - 10: Sftp - 11: SharePoint - 12: Nfs - 13: Wasabi - 14: OracleCloud - 15: NetAppOntap - 16: Cubbit - 17: Mft - 18: SharepointOnPrem - 19: Ftp - 20: Oracle - 21: NfsSisl - 22: ScalityRing   Enum: `0`,`1`,`2`,`3`,`4`,`5`,`6`,`7`,`8`,`9`,`10`,`11`,`12`,`13`,`14`,`15`,`16`,`17`,`18`,`19`,`20`,`21`,`22` |  |
| storageStatus | object |  |  |
| message | string |  |  |
| statusType | int32 |  |  |
| scansInProgress | boolean |  |  |
| isRtpInProgress | boolean |  |  |
| isScheduledScanInProgress | boolean |  |  |
| storageFunctionality | string |  |  |
| isAutodiscovered | boolean |  |  |
| groupRef GroupReference |  |  |  |
| object | object |  |  |
| id | string |  |  |
| name | string |  |  |
| $type | string |  |  |

 Response
