<!-- source: https://www.opswat.com/docs/mdmft/metadefender-mft/ref -->

This chapter describes the REST API calls that can be used with MetaDefender Vault. Through the Application’s Interface, any 3rd party application can interact and communicate directly with MetaDefender Vault. This allows you to add MetaDefender Vault to your automated workflow. Each call should include an authentication key or user credentials (username and password) or use 8.4 API Keys.

## About this REST API

The exposed endpoint is located by default at **http://localhost:8010/vault_rest/** (i.e. for **Initialize Group Transfer** the endpoint is **http://localhost:8010/vault_rest/transfer**).

All endpoints require you to provide the Authorization header. The value for this header should be obtained by calling **Request An API Key**. Please note that an authentication key has a limited lifetime and it should be refreshed to avoid expiration policy.

In order to change the URL it is recommended to use the **Protocol Configuration Tool**(located by default in *C:\Program Files\OPSWAT\MetaDefender Vault\Tools*).

This URL can also be changed directly from the configuration file by following these steps:

1. Go to the installation directory (by default *C:\Program Files\OPSWAT\MetaDefender Vault*)
2. Navigate to the *WebServer/conf* folder
3. Open the file called *dynamic.conf* using administrative privileges
4. Edit the following section of the configuration file as you wish:

   ```
   listen <ip_address>:<port>;
   server_name "<machine_name>";
   ```

   Or, in case of TLS/SSL:

   ```
   listen <ip_address>:<port> ssl;
   server_name "<machine_name>";
   ssl_certificate "<certificate_path>";
   ssl_certificate_key "<certificate_key_path>";
   ssl_password_file "<password_file_path>";
   ```
5. Restart MetaDefender Vault Helper Service (vaultHelper) for changes to apply.
Serverhttp://localhost:8010Server Variables## Authenticationhttp basicAuthhttp bearerAuth
## Authentication Management

## Overview

These APIs provide functionality to create, update and delete API keys.
The first step should be to **Request an API key** before continuing with other API calls.

Endpoints[GET/vault_rest/authenticate](/docs/mdmft/metadefender-mft#getrequest-an-api-key) [DELETE/vault_rest/authenticate](/docs/mdmft/metadefender-mft#deletecancel-or-expire-an-api-key) [PUT/vault_rest/token](/docs/mdmft/metadefender-mft#putextend-api-key) [POST/vault_rest/token](/docs/mdmft/metadefender-mft#postcreate-a-3rd-party-api-key) [GET/vault_rest/tokens/{start}/{count}](/docs/mdmft/metadefender-mft#getenumerate-api-keys)
### Request An API Key

## Summary

This API allows a user to sign in and obtain an API key to use in subsequent API requests.

## Use Cases (used by)

All clients accessing MetaDefender Vault REST must call this API first to obtain an API key.

The token required in the Authorization header is formed by joining the account's username and password, using the windows newline
separator (CRLF - \r\n) as delimiter.

## Example

Username: JohnDoe

Password: SecretPassword

Token: encodeBase64("JohnDoe\r\nSecretPassword")

Authorization: Basic Sm9obkRvZQ0KU2VjcmV0UGFzc3dvcmQ=

Auth basicAuthGET /vault_rest/authenticatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Cancel Or Expire An API Key

## Use Cases (used by)

Used by the user interface when the user logs out.

Auth bearerAuthDELETE /vault_rest/authenticatecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Extend API Key

## Summary

This API allows a user to extend an API key.

## Use Cases (used by)

Used by clients that want to prevent an API to expire due to inactivity or change the expiration of an existing generated API key.

Auth bearerAuthHeaders

| Token | string | The API key that you wish to extend. *Note: If this header is not present the API key from Authorization header will be used instead |  |
| --- | --- | --- | --- |
| ExtendBy | string | Parameter value must be a time span (hh:mm:ss) value how long to extend the API key. If this parameter is not specified a default server value is used. Max value is 24h: 23:59:59 |  |
| ExtendUntil | number | Used to adjust 3rd party API key expiration date. Date should be specified in UTC, for example: 2016-01-02T12:00:00.0000000Z |  |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Create A 3rd Party API Key

## Summary

This API allows you to create API keys to be used by 3rd party applications.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Enumerate API Keys

## Summary

Returns a list of API keys generated by this user to allow 3rd party applications to connect to MetaDefender Vault .

## Use Cases

Used by the web user interface to display generated API keys.

Auth bearerAuthHeaders

| sort_column | string | Possible values: Token, Created, Expires, Description, Role |  |
| --- | --- | --- | --- |
| sort_direction | string | Possible values, asc, desc |  |
| find | string | Searches Token & Description |  |
| findB64 | string | Free text search string (Base64 encoded to support all charsets). Will override any value specified in 'find' header. |  |

Path Params

| start | integer | [required] Zero based position in list from where to start returning data |  |
| --- | --- | --- | --- |
| count | integer | [required] Maximum number of list entries to return |  |

GET /vault_rest/tokens/{start}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response
## File Management

## Overview

These APIs enable developers to check information about files uploaded in MetaDefender Vault.

Endpoints[GET/vault_rest/file/{file_id}](/docs/mdmft/metadefender-mft#getdownload-a-file) [DELETE/vault_rest/file/{file_id}](/docs/mdmft/metadefender-mft#deletedelete-a-file) [PUT/vault_rest/v2/move_files](/docs/mdmft/metadefender-mft#putmove-a--file) [PUT/vault_rest/rename_file](/docs/mdmft/metadefender-mft#putrename-a-file) [POST/vault_rest/update_file_share](/docs/mdmft/metadefender-mft#postshare-a-file) [GET/vault_rest/file/status/{file_id}](/docs/mdmft/metadefender-mft#getquery-file-status) [GET/vault_rest/files/{type}/{start}/{count}](/docs/mdmft/metadefender-mft#getenumerate-files) [DELETE/vault_rest/files](/docs/mdmft/metadefender-mft#deletedelete-multiple-files) [GET/vault_rest/file_tags/{file_id}](/docs/mdmft/metadefender-mft#getget-file-tags) [PUT/vault_rest/file_tags](/docs/mdmft/metadefender-mft#putaddmodify-file-tags)
### Download a file

## Summary

This API call allows you to download the files stored in MetaDefender Vault.

The call should be made to vault_rest/file/{file_id} through a GET request. Please note that you need to obtain {file_id} in order to retrieve the file.

Auth bearerAuthPath Params

| file_id | string | [required] Id of the file you wish to download |  |
| --- | --- | --- | --- |

GET /vault_rest/file/{file_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/octet-stream 200

Successful response

| file | file |  |  |
| --- | --- | --- | --- |

 Response File Content
### Delete A File

## Summary

Delete a file from the MetaDefender Vault storage. This API will only mark the file for deletion. The file will be physically deleted by the background worker.

## Permissions Restrictions

Administrators can delete any file, including other user's files.
Users can only delete their own files.

Auth bearerAuthPath Params

| file_id | string | [required] ID of file to delete |  |
| --- | --- | --- | --- |

DELETE /vault_rest/file/{file_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Move A File

## Summary

This API allows moving one or multiple files in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/v2/move_filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Rename A File

## Summary

This API allows renaming a file in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/rename_filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Share A File

## Summary

This API allows sharing a file in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/update_file_sharecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Query File status

## Summary

This API lets you query the current status of a file in MetaDefender Vault.

Auth bearerAuthPath Params

| file_id | string | [required] File ID of MetaDefender Vault file returned by Upload file call. |  |
| --- | --- | --- | --- |

GET /vault_rest/file/status/{file_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response File Status
### Enumerate Files

## Summary

Retrieve a list of the user's files.

Auth bearerAuthHeaders

| sort_column | string | Possible values: expires, name, size |  |
| --- | --- | --- | --- |
| sort_direction | string | Possible values: asc, desc |  |
| find | string | Free text search string (Use only with English characters) |  |
| findB64 | string | Free text search string (Base64 encoded to support all charsets). Will override any value specified in 'find' header. |  |
| columns | string | Possible values: SearchId, FileTransferId, Subject, Body, Sender, Recepiet, FileName |  |
| AvailabilityState | string | By default Files of all availability states are returned. To return files of certain states, specify them in the header (separate multiple states with a , (comma)) Possible states:  Composing QueuedForProcessing BeingProcessed Available Expired Deleted Blocked BlockedNoSanitization ProcessingFailed |  |

Path Params

| type | string | [required] Return entries of this specific type. Possible values: my, all |  |
| --- | --- | --- | --- |
| start | string | [required] Zero based position in list from where to start returning data |  |
| count | string | [required] Maximum number of list entries to return |  |

GET /vault_rest/files/{type}/{start}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response Enumerate Files Result
### Delete Multiple Files

## Summary

Delete a group of files from the MetaDefender Managed File Transfer storage. This API will only mark the files for deletion. The files will be physically removed by a background worker.

## Permissions Restrictions

Administrators can delete any file, including other user's files.
Users can only delete their own files.

Auth bearerAuthRequest Body application/json

DELETE /vault_rest/filescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |

 Response Delete Files Result
### Get file tags

This API endpoint, provides a list of {file_id} file's tags

Auth bearerAuthGET /vault_rest/file_tags/{file_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| string | string |  |  |
| --- | --- | --- | --- |

 Response Tags response
### Add/Modify file tags

This API endpoint, allows user to modify file tags

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/file_tagscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpTag requestResponses application/json 200

Successful response

| No response body |
| --- |

 Response
## User Management

## Overview

Manage users inside MetaDefender Vault.

Endpoints[PUT/vault_rest/guest](/docs/mdmft/metadefender-mft#putmodify-a-guest-account) [POST/vault_rest/guest](/docs/mdmft/metadefender-mft#postcreate-a-guest-account) [GET/vault_rest/accounts/{type}/{start}/{count}](/docs/mdmft/metadefender-mft#getenumerate-accounts) [POST/vault_rest/account](/docs/mdmft/metadefender-mft#postcreate-an-account) [PUT/vault_rest/accounts/{id}](/docs/mdmft/metadefender-mft#putmodify-an-account) [DELETE/vault_rest/accounts](/docs/mdmft/metadefender-mft#deletedelete-accounts) [GET/vault_rest/account/{id}](/docs/mdmft/metadefender-mft#getget-account-details)
### Modify a guest account

This API endpoint, allows the user to remove guest account.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/guestcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpguestResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response Successful response
### Create a guest account

This API endpoint, allows user to create guest account

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/guestcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpguest_dataResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Enumerate accounts

This API endpoint, with the {type} parameter supporting options like local, external, guest, or active directory, provides a response containing a list of accounts.

Auth bearerAuthHeaders

| find | string | Free text search string |  |
| --- | --- | --- | --- |
| findB64 | string | Free text search string (Base64 encoded to support all charsets). Will override any value specified in 'find' header. |  |
| sort_column | string | Allows users to specify the column by which the query results should be sorted. |  |
| sort_direction | string | Allows them to specify whether the results should be in ascending or descending order. |  |

Path Params

| start | string | [required] Zero based position in list from where to start returning data |  |
| --- | --- | --- | --- |
| count | string | [required] Maximum number of list entries to return |  |
| type | string | [required] Account type |  |

GET /vault_rest/accounts/{type}/{start}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| string | string |  |  |
| --- | --- | --- | --- |

 Response LocalUserGuestExternalUserActiveDirectory
### Create an account

This API endpoint, allows user to create an account

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/accountcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response Response
### Modify an account

This API endpoint, allows user to modify an account

Auth bearerAuthPath Params

| id | string | Account id |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/accounts/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpModify AccountResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response Response
### Delete account(s)

This API endpoint, allows the removal of a user account, permanently erasing associated data and terminating access.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

DELETE /vault_rest/accountscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpDelete account(s)Responses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response Successful response
### Get account details

This API endpoint, allows user to get an account's detailed info

Auth bearerAuthGET /vault_rest/account/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response Account detail
## Archive Download

## Overview

These APIs enable downloading of multiple files or folders as an archive from MetaDefender Vault.

## Workflow

In order to start the process please follow these steps:

1. Create an archive by calling Create Archive
2. Wait until the archive is created by polling Get Archive Status
3. Once the archive is available, you can obtain it by calling Download Archive

## Error Handling

If an error prevents you from downloading the archive or you simply wish to stop the process or discard the archive, you can call Cancel Archive Download. Please note that it’s not mandatory to call this endpoint after a successful download because there is an automatic cleanup mechanism that will remove archives after they are downloaded.

Endpoints[PUT/vault_rest/cancel_archive_download/{id}](/docs/mdmft/metadefender-mft#putcancel-archive-download) [POST/vault_rest/create_archive_download](/docs/mdmft/metadefender-mft#postcreate-archive) [GET/vault_rest/archive_download/{id}](/docs/mdmft/metadefender-mft#getdownload-archive) [GET/vault_rest/archive_download_status/{id}](/docs/mdmft/metadefender-mft#getget-archive-status)
### Cancel Archive Download

## Summary

This API allows the cancelation of a previously created archive.

Auth bearerAuthPath Params

| id | string | [required] Unique identifier of the archive to be canceled |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/cancel_archive_download/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Create Archive

## Summary

This API allows creating an archive containing multiple folders and files from MetaDefender Vault. This API will only initiate the archiving process, you need to use Get Archive Status to obtain the status of the archiving process and then download it.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/create_archive_downloadcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses text/plain 200

OK

| string | string |  |  |
| --- | --- | --- | --- |

 Response
### Download Archive

## Summary

This API downloads an archive from MetaDefender Vault.

Auth bearerAuthPath Params

| id | string | [required] Unique identifier of the public archive. |  |
| --- | --- | --- | --- |

GET /vault_rest/archive_download/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Get Archive Status

Auth bearerAuthPath Params

| id | string | [required] Unique identifier of the archive. |  |
| --- | --- | --- | --- |

GET /vault_rest/archive_download_status/{id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
## Audit Events

## Overview

View and export audit events.

Endpoints[GET/vault_rest/audit/{start}/{count}](/docs/mdmft/metadefender-mft#getenumerate-audit-events) [GET/vault_rest/audit/export](/docs/mdmft/metadefender-mft#getexport-audit-events)
### Enumerate Audit Events

Auth NoneHeaders

| sort_column | string | Possible values: date, description, event, location, status, user |  |
| --- | --- | --- | --- |
| sort_direction | string | Possible values: asc, desc |  |
| find | string | Free text search string |  |
| findB64 | string | Free text search string (Base64 encoded to support all charsets). Will override any value specified in 'find' header. |  |

Path Params

| start | string | [required] Zero based position in list from where to start returning data |  |
| --- | --- | --- | --- |
| count | string | [required] Maximum number of list entries to return |  |

GET /vault_rest/audit/{start}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Export Audit Events

Auth bearerAuthQuery String

| locale | string |  |  |
| --- | --- | --- | --- |

GET /vault_rest/audit/exportcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
## File Upload

## Workflow

To upload one or more files in chunks to MetaDefender Vault , follow the workflow below:

1. Create a transfer group by calling **Initialize Group Transfer**
2. Create a file transfer by calling **Initialize File Transfer**
3. Upload file chunks by calling **Upload file chunk** until the complete file is uploaded
4. Call **Complete File Transfer** to commit the uploaded file in MetaDefender Vault .
5. Repeat step 2 - 4 to upload additional files in the same group.
6. Call **Complete Group Transfer** to commit the transfer in MetaDefender Vault and make it available for download.

## Error Handling

During steps 3 to 5, it is possible to delete a partially/completely uploaded file by calling Delete File From File Transfer

During steps 2 to 5, it is possible to delete a group transfer (including any uploaded files) by calling Delete Group Transfer

Endpoints[GET/vault_rest/transfer](/docs/mdmft/metadefender-mft#getinitialize-group-transfer) [POST/vault_rest/transfer](/docs/mdmft/metadefender-mft#postcomplete-group-transfer) [DELETE/vault_rest/transfer](/docs/mdmft/metadefender-mft#deletedelete-group-transfer) [GET/vault_rest/transfer_file](/docs/mdmft/metadefender-mft#getinitialize-file-transfer) [POST/vault_rest/transfer_file](/docs/mdmft/metadefender-mft#postcomplete-file-transfer) [DELETE/vault_rest/transfer_file](/docs/mdmft/metadefender-mft#deletedelete-file-from-file-transfer) [PATCH/vault_rest/transfer_file](/docs/mdmft/metadefender-mft#patchupload-file-chunk)
### Initialize group transfer

## Permissions Restrictions

Even if the current API method is open to multiple user roles (i.e. Administrator and User), only the Administrator has a full set of permissions.

Administrators can impersonate users, or even other administrators.

For the User role, the permissions apply an even more strict rules set: they can only upload files in their own account - they don't have any impersonation rights.
Although it's not something that applies directly to the current API method, it is worth mentioning that after a transfer has been started (i.e. this method has been called successfully), the other transfer methods (e.g. Init file transfer, Patch file, Complete File, etc.) will only be accessible to the user that has initiated the transfer (the one who's API key was used to make this request). No other user can alter a transfer that's in progress.

Auth bearerAuthHeaders

| group_id | string | A unique transfer group id can be transmitted to support Diode scenarios. If no id has been specified MetaDefender Vault will generate a unique id. Must be a valid v4 UUID (RFC4122 standard). |  |
| --- | --- | --- | --- |
| impersonate_as | string | Must be a valid user or email address Note: please use impersonate_as header because send_as will be deprecated. |  |
| share_with | string | Must be one or more valid users or email addresses. Separate multiple entries with a comma (,). Note: please use share_with header because recipients will be deprecated. |  |
| subject | string |  |  |
| message | string |  |  |
| source | string | 0 = REST (default) 1 = Kiosk 2 = WebUI |  |

GET /vault_rest/transfercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Complete group transfer

## Permissions Restrictions

The API is limited to the user roles listed above (i.e. CO, Administrator, User), but assuming that a valid set of parameters is provided, including a group_id, only the transfer owner will be able alter the transfer.

Example:

The user test1 initiates a group transfer (i.e. calls /transfer successfully) and it receives a transfer group ID - group_id.

The user test2 tries to append a file to transfer with ID group_id. A 403 - Forbidden error will be returned stating that the user that has made the request is not authorized to alter the transfer.

The user test1 tries to append a file to the transfer - operation successful.

The user test1 completes the transfer by calling POST /transfer - operation successful.

Transfer with ID group_id will be accessible to the user until its expiration date.

Auth bearerAuthHeaders

| group_id | string | A transfer group id obtained from the Initialize Group Transfer call. |  |
| --- | --- | --- | --- |
| expires_after | string | Specify in DD:HH:MM:SS. Cannot be combined with 'expires' property.  The value ranges are the following:   - Days, ranging from 1 to 9999; - Hours, ranging from 0 to 23; - Minutes, ranging from 0 to 59; - Optional seconds, ranging from 0 to 59. |  |
| file_name_duplicate_handling_strategy | string | Specifies how to handle file name duplications.   - "None" - Allow file name duplication - "Deny" - Don't allow file name duplication - "Overwrite" - Overwrite file with existing name - "RenameIncrement" - Increment file name, like "filename(1).txt" |  |

POST /vault_rest/transfercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Delete Group Transfer

## Permissions Restrictions

The API is limited to the user roles listed above (i.e. CO, Administrator, User), but assuming that a valid set of parameters is provided, including a group_id, only the transfer owner will be able alter the transfer.

Example:

The user test1 initiates a group transfer (i.e. calls /transfer successfully) and it receives a transfer group ID - group_id.

The user test2 tries to append a file to transfer with ID group_id. A 403 - Forbidden error will be returned stating that the user that has made the request is not authorized to alter the transfer.

The user test1 tries to append a file to the transfer - operation successful.

The user test1 completes the transfer by calling POST /transfer - operation successful.

Transfer with ID group_id will be accessible to the user until its expiration date.

Auth bearerAuthHeaders

| group_id | string | A transfer group id obtains from the Initialize Group Transfer call. |  |
| --- | --- | --- | --- |

DELETE /vault_rest/transfercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Initialize File Transfer

## Permissions Restrictions

The API is limited to the user roles listed above (i.e. CO, Administrator, User), but assuming that a valid set of parameters is provided, including a group_id, only the transfer owner will be able alter the transfer.

Example:

The user test1 initiates a group transfer (i.e. calls /transfer successfully) and it receives a transfer group ID - group_id.

The user test2 tries to append a file to transfer with ID group_id. A 403 - Forbidden error will be returned stating that the user that has made the request is not authorized to alter the transfer.

The user test1 tries to append a file to the transfer - operation successful.

The user test1 completes the transfer by calling POST /transfer - operation successful.

Transfer with ID group_id will be accessible to the user until its expiration date.

Auth bearerAuthHeaders

| transfer_method | string | Specify the method of transferring file chunks. Possible values are:  Stream - chunks are submitted in a synchronous orderly fashion  Chunk - multiple chunks can be transferred simultaneously; does not require any specific ordering of data |  |
| --- | --- | --- | --- |
| group_id | string | A transfer group id obtains from the 1. Initialize Group Transfer call. |  |
| file_size | string | The size in bytes of the complete file to be transferred. |  |
| file_name | string | The name of the file to be transferred. The file name can't contain special characters such as / or \. |  |
| path | string | The full path to the folder where you wish to upload this file. Leave it empty if you wish to upload it in the root directory. Example: my documents\images\phone |  |
| file_id | string | A unique file_id can be transmitted to support Diode scenarios. If no file id has been specified MetaDefender Vault will generate a unique id. Must be a valid v4 UUID (RFC4122 standard). |  |
| file_checksum | string | Used to verify data integrity when upload has been completed. The hashing algorithm used is SHA256. |  |
| user_agent | string | See <https://onlinehelp.opswat.com/corev4/8.1.3.1._Process_a_file.html> for more details. Leave this field empty in order to use the user_agent defined in Core Integration settings. |  |
| core_rule | string | See <https://onlinehelp.opswat.com/corev4/8.1.3.1._Process_a_file.html> for more details. |  |
| archivepwdX | string | Multiple passwords is also supported, format: archivepwd  X: Could be empty  When having value, X must be a number >= 1  archivepwd1: <password 1> archivepwd2: <password 2> archivepwd3: <password 3> ... archivepwdN: Each archivepwd is a separate header. You can use N headers in order to set multiple password for nested encrypted archive which contains encrypted files inside.  Set only archivepwd if the file is encrypted with password or leave this field empty when the file is not password protected. |  |

Expand GET /vault_rest/transfer_filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Complete file transfer

## Permissions Restrictions

The API is limited to the user roles listed above (i.e. CO, Administrator, User), but assuming that a valid set of parameters is provided, including a group_id, only the transfer owner will be able alter the transfer.

Example:

The user test1 initiates a group transfer (i.e. calls /transfer successfully) and it receives a transfer group ID - group_id.

The user test2 tries to append a file to transfer with ID group_id. A 403 - Forbidden error will be returned stating that the user that has made the request is not authorized to alter the transfer.

The user test1 tries to append a file to the transfer - operation successful.

The user test1 completes the transfer by calling POST /transfer - operation successful.

Transfer with ID group_id will be accessible to the user until its expiration date.

Auth bearerAuthHeaders

| group_id | string | A transfer group id obtained from the Initialize Group Transfer call. |  |
| --- | --- | --- | --- |
| file_id | string | A file ID obtained from the Initialize File Transfer call. |  |

POST /vault_rest/transfer_filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Delete File From File Transfer

## Permissions Restrictions

The API is limited to the user roles listed above (i.e. CO, Administrator, User), but assuming that a valid set of parameters is provided, including a group_id, only the transfer owner will be able alter the transfer.

Example:

The user test1 initiates a group transfer (i.e. calls /transfer successfully) and it receives a transfer group ID - group_id.

The user test2 tries to append a file to transfer with ID group_id. A 403 - Forbidden error will be returned stating that the user that has made the request is not authorized to alter the transfer.

The user test1 tries to append a file to the transfer - operation successful.

The user test1 completes the transfer by calling POST /transfer - operation successful.

Transfer with ID group_id will be accessible to the user until its expiration date.

Auth bearerAuthHeaders

| group_id | string | A transfer group id obtains from the Initialize Group Transfer call. |  |
| --- | --- | --- | --- |
| file_id | string | A file id obtained from the Initialize File Transfer call. |  |

DELETE /vault_rest/transfer_filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Upload File Chunk

## Permissions Restrictions

The API is limited to the user roles listed above (i.e. CO, Administrator, User), but assuming that a valid set of parameters is provided, including a group_id, only the transfer owner will be able alter the transfer.

Example:

The user test1 initiates a group transfer (i.e. calls /transfer successfully) and it receives a transfer group ID - group_id.

The user test2 tries to append a file to transfer with ID group_id. A 403 - Forbidden error will be returned stating that the user that has made the request is not authorized to alter the transfer.

The user test1 tries to append a file to the transfer - operation successful.

The user test1 completes the transfer by calling POST /transfer - operation successful.

Transfer with ID group_id will be accessible to the user until its expiration date.

Auth bearerAuthHeaders

| group_id | string | A transfer group id obtained from the 1. Initialize Group Transfer call. |  |
| --- | --- | --- | --- |
| file_id | string | A file ID obtained from a call to "Initialize File Transfer". |  |
| chunk_offset | string | The offset (location) of the chunk in the reassembled file. |  |
| chunk_checksum | string | Used to verify data integrity when chunk has been received. If no value is provided no checksum will be performed. |  |

Request Body application/octet-stream

| object | object |  |  |
| --- | --- | --- | --- |

PATCH /vault_rest/transfer_filecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
## Folder Management

## Overview

These APIs enable developers to check information about folders in MetaDefender Vault.

Endpoints[DELETE/vault_rest/folder/{folder_id}](/docs/mdmft/metadefender-mft#deletedelete-a-folder) [DELETE/vault_rest/folders](/docs/mdmft/metadefender-mft#deletedelete-multiple-folders) [GET/vault_rest/folder_content/{id}/{start}/{count}](/docs/mdmft/metadefender-mft#getenumerate-folder-content) [GET/vault_rest/folder_search/{id}/{start}/{count}](/docs/mdmft/metadefender-mft#getfolder-search) [GET/vault_rest/root_folder](/docs/mdmft/metadefender-mft#getget-root-folder) [PUT/vault_rest/v2/move_folders](/docs/mdmft/metadefender-mft#putmove-folders) [PUT/vault_rest/rename_folder](/docs/mdmft/metadefender-mft#putrename-a-folder) [POST/vault_rest/update_folder_share](/docs/mdmft/metadefender-mft#postshare-a-folder) [POST/vault_rest/folder](/docs/mdmft/metadefender-mft#postcreate-a-folder)
### Delete A Folder

## Summary

Delete a folder from the MetaDefender Vault storage. This API will only mark the folder for deletion. The folder will be physically deleted by the background worker.

## Permissions Restrictions

Administrators can delete any folder, including other user's folders.
Users can only delete their own folders.

Auth bearerAuthPath Params

| folder_id | string | [required] |  |
| --- | --- | --- | --- |

DELETE /vault_rest/folder/{folder_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Delete Multiple Folders

## Summary

Delete a group of folders from the MetaDefender Vault storage. This API will only mark the folders for deletion. The folders will be physically removed by a background worker.

## Permissions Restrictions

Administrators can delete any folder, including other user's folders.
Users can only delete their own folders.

Auth bearerAuthDELETE /vault_rest/folderscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Enumerate Folder Content

## Summary

Retrieve a list of the user's files.

Auth bearerAuthHeaders

| sort_column | string | Possible values: name, size, datecreated. |  |
| --- | --- | --- | --- |
| sort_direction | string | Possible values: asc, desc. |  |
| find | string | Free text search string (Use only with English characters). |  |
| findB64 | string | Free text search string (Base64 encoded to support all charsets). Will override any value specified in 'find' header. |  |

Path Params

| id | string | [required] |  |
| --- | --- | --- | --- |
| start | string | [required] |  |
| count | string | [required] |  |

GET /vault_rest/folder_content/{id}/{start}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Folder Search

## Summary

Retrieve a list of the user's folders and files starting from a specified folder and filtered by a search string.

Auth bearerAuthHeaders

| sort_column | string | Possible values: name, size, datecreated. |  |
| --- | --- | --- | --- |
| sort_direction | string | Possible values: asc, desc. |  |
| find | string | Free text search string (Use only with English characters). |  |
| findB64 | string | Free text search string (Base64 encoded to support all charsets). Will override any value specified in 'find' header. |  |

Path Params

| id | string | [required] |  |
| --- | --- | --- | --- |
| start | string | [required] |  |
| count | string | [required] |  |

GET /vault_rest/folder_search/{id}/{start}/{count}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Get Root Folder

## Summary

List information about the 'root' folder.

Auth bearerAuthGET /vault_rest/root_foldercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Move Folders

## Summary

This API allows moving one or multiple folders in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/v2/move_folderscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
### Rename A Folder

## Summary

This API allows renaming a folder in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

PUT /vault_rest/rename_foldercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

409

Conflict

 Response
### Share A Folder

## Summary

This API allows sharing a folder in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/update_folder_sharecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| No response body |
| --- |

 Response
### Create A Folder

## Summary

This API allows creating a folder in MetaDefender Vault.

Auth bearerAuthRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |

POST /vault_rest/foldercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

400

Bad Request

409

Conflict

 Response
## Default

Endpoints[GET/vault_rest/version](/docs/mdmft/metadefender-mft#getversion)
### Version

Auth NoneHeaders

| Authorization | string |  |  |
| --- | --- | --- | --- |

GET /vault_rest/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |

 Response
