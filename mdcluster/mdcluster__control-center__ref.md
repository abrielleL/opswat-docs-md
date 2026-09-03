<!-- source: https://www.opswat.com/docs/mdcluster/control-center/ref -->

## Developer Guide

---

This is the API documentation for *MetaDefender Cluster Control Center Public API*. If you
would like to evaluate or have any questions about this documentation,
please contact us via our [Contact Us](https://www.opswat.com/contact) form.

---

## How to Interact with MetaDefender Cluster Control Center using REST API

The MetaDefender Cluster Control Center empowers administrators and system engineers to efficiently manage system operations, including:

1. Establishing and maintaining essential service connections.
2. Deploying and managing MetaDefender Core, MetaDefender Cluster API Gateway instances.
3. Managing licenses.
4. Administering user accounts and access controls.
5. Configuring and enforcing security protocols.
6. Monitoring the overall system health and system performance.

OPSWAT recommends using the JSON-based REST API. The available methods are documented below.

---

OPSWAT provides some sample codes on [GitHub](https://github.com/OPSWAT) to make it easier to understand how the MetaDefender REST API works.

Serverhttp://localhost:8892Server Variables## AuthenticationapiKey apikey

Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication.

Fields

| Key | In |
| --- | --- |
| apikey | Header |  |

## Auth

### Authentication APIs

User authentication is done via username & password.

Endpoints[POST/login](/docs/mdcluster/control-center#userlogin) [POST/logout](/docs/mdcluster/control-center#userlogout)
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
## User Management

### User management APIs

The APIs for manage users and user directories.

Endpoints[POST/admin/user](/docs/mdcluster/control-center#usercreate) [GET/admin/user](/docs/mdcluster/control-center#userlist) [DELETE/admin/user/{user_id}](/docs/mdcluster/control-center#userdelete) [POST/user/changepassword](/docs/mdcluster/control-center#userchangepass)
### Create user

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object | User object in MetaDefender. |  |
| --- | --- | --- | --- |
| api_key | string | Associated apikey with this user |  |
| directory_id | integer | To which User Directories belongs to (LOCAL/System/etc.) |  |
| display_name | string | Which is the name showed in the Management Console |  |
| email | string | User's email address |  |
| name | string | User's full name |  |
| description | string | User's description, 256 characters maximum |  |
| roles | array[string] | A list of roles attached to this user |  |
| ui_settings | object | Configuration of Management Console for this user.   - `refresh_rate` the refresh rate of the Management Console in seconds. Must not be negative. - `engine_time_period` the time period for Technology results on the Usage page, in hours. Must be non-negative. - `processing_chart_time_period` the time period for the Processing chart on the Usage page, in hours. Must be non-negative. - `summary_time_period` the time period for the Summary data on the Usage page, in hours. Must be non-negative. |  |
| password | string | The user's password |  |

Expand POST /admin/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully.

| object | object | User object in MetaDefender. |  |
| --- | --- | --- | --- |
| api_key | string | Associated apikey with this user |  |
| directory_id | integer | To which User Directories belongs to (LOCAL/System/etc.) |  |
| display_name | string | Which is the name showed in the Management Console |  |
| email | string | User's email address |  |
| name | string | User's full name |  |
| description | string | User's description, 256 characters maximum |  |
| roles | array[string] | A list of roles attached to this user |  |
| ui_settings | object | Configuration of Management Console for this user. |  |

400

Bad Request (e.g. invalid header, invalid request body).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### List all users

Returns a list of all users in the server.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/usercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

List of users retrieved successfully.

| array | array[object] |  |  |
| --- | --- | --- | --- |
| api_key | string | Associated apikey with this user |  |
| directory_id | integer | To which User Directories belongs to (LOCAL/System/etc.) |  |
| display_name | string | Which is the name showed in the Management Console |  |
| email | string | User's email address |  |
| id | integer | User's unique identifier |  |
| name | string | User's full name |  |
| description | string | User's description, 256 characters maximum |  |
| roles | array[string] | A list of roles attached to this user |  |
| ui_settings | object | Configuration of Management Console for this user. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Delete a user

Delete a user by id from the system.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

DELETE /admin/user/{user_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully.

| object | object |  |  |
| --- | --- | --- | --- |

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Change Password for local user

Modify the current password for the user identified by apikey

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| old_password | string | The current password in plain text |  |
| new_password | string | The new password in plain text |  |

POST /user/changepasswordcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| result | string |  |  |

400

Bad Request (e.g. invalid header, invalid request body).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
## Admin

Admin specific API requests.

Endpoints[GET/admin/userdirectory](/docs/mdcluster/control-center#userdirectorylist) [POST/admin/role](/docs/mdcluster/control-center#rolecreate) [DELETE/admin/role/{role_id}](/docs/mdcluster/control-center#roledelete)
### List all user directories

Retrieve a list of all user directories configured in the system.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/userdirectorycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

List of user directories retrieved successfully.

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | integer | Internal used identifier |  |
| name | string | Name of the user directory |  |
| type | string | Type of the user directory (e.g., LDAP, Local, etc.) |  |
| enabled | boolean | If the user directory is enabled or not |  |
| lockout_attempts | integer | Number of failed login attempts before the user is locked out |  |
| lockout_timeout | integer | Time in seconds before the user can try to log in again after being locked out |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Create new role

Add a new user role to the system.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object | MetaDefender user role describing object. |  |
| --- | --- | --- | --- |
| name | string | The name identifier of the role |  |
| display_name | string | The extended name showed in the Management Console. |  |
| rights18 fields | object | A list of rights for each permission |  |
| cert | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| configlog | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| engines | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| license | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| retention | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| rule | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| scanlog | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| update | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| updatelog | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| users | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| workflow | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| zone | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| healthcheck | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| fetch | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| download | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| deployment | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| service | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| packageupload | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |

POST /admin/rolecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object | MetaDefender user role describing object. |  |
| --- | --- | --- | --- |
| name | string | The name identifier of the role |  |
| display_name | string | The extended name showed in the Management Console. |  |
| rights18 fields | object | A list of rights for each permission |  |
| cert | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| configlog | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| engines | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| license | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| retention | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| rule | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| scanlog | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| update | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| updatelog | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| users | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| workflow | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| zone | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| healthcheck | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| fetch | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| download | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| deployment | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| service | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| packageupload | array[string] | An object defining the permission set allowed on MetaDefender individual role.  Enum: `read`,`write` |  |
| editable | boolean | If the role can be altered or not. |  |
| id | integer | Internal used identifier |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Delete a role

Delete a role by id from the system.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

DELETE /admin/role/{role_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully.

| object | object |  |  |
| --- | --- | --- | --- |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
## Config

Configure the product through APIs (especially the Settings). Will require admin apikey..

Endpoints[PUT/admin/config/auditlog/cleanup](/docs/mdcluster/control-center#configauditlog) [PUT/admin/config/filestorage/cleanup](/docs/mdcluster/control-center#configfilestorage) [PUT/admin/config/warehouse/cleanup](/docs/mdcluster/control-center#configexecutivereport) [PUT/admin/config/scanhistory/cleanup](/docs/mdcluster/control-center#configscanhistory) [GET/admin/config/healthcheck](/docs/mdcluster/control-center#configgethealthcheck) [POST/admin/config/healthcheck](/docs/mdcluster/control-center#configposthealthcheck) [PUT/admin/config/session](/docs/mdcluster/control-center#configsession) [GET/admin/config/sessioncookie](/docs/mdcluster/control-center#configgetsessioncookie) [PUT/admin/config/sessioncookie](/docs/mdcluster/control-center#configputsessioncookie)
### Audit clean up

Setting audit record cleanup time ( cleanup records older than).

> ***Note***: The cleanup range is defined in `hours`.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. ***Note***: If `cleanuprange` is `0`, the cleanup functionality will be disabled. |  |

PUT /admin/config/auditlog/cleanupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### File storage clean up

Setting file storage clean up time (clean up records older than).

> ***Note***:The clean up range is defined in `hours`.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. ***Note***: If `cleanuprange` is `0`, the cleanup functionality will be disabled. |  |

PUT /admin/config/filestorage/cleanupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Executive report clean up

Setting executive report clean up time (clean up records older than).

> ***Note***:The clean up range is defined in `hours`.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. ***Note***: If `cleanuprange` is `0`, the cleanup functionality will be disabled. |  |

PUT /admin/config/warehouse/cleanupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Processing history clean up

Setting processing history clean up time (clean up records older than).

> ***Note***:The clean up range is defined in `hours`.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. ***Note***: If `cleanuprange` is `0`, the cleanup functionality will be disabled. |  |

PUT /admin/config/scanhistory/cleanupcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| cleanuprange | integer | The number of hours of data retention. Anything older than this number will be deleted. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Fetch Health Check Setting

Retrieves the current health check configuration, including the number of active MetaDefender Core (ometascan) instances required and the list of engines available together with their selection state.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/config/healthcheckcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully.

| object | object |  |  |
| --- | --- | --- | --- |
| number_active_ometascan | integer | Minimum number of active MetaDefender Core (ometascan) instances required to be considered healthy. Must be at least 1.  minimum: 1 |  |
| number_active_av_engines | integer | Minimum number of active anti-virus engines required to be considered healthy. Must be at least 1.  minimum: 1 |  |
| engines3 fields | array[object] | List of engines available in the system together with their selection state. The `7z` (Archive Extraction) and `filetype` (FileType) engines are always required and will always be returned with `is_selected: true`. |  |
| display_name | string | Human readable name of the engine. |  |
| id | string | Internal engine identifier. |  |
| is_selected | boolean | Whether the engine is selected as required for the health check. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response sample
### Configure Health Check Setting

Updates the health check configuration. The required engines listed in the request body will be marked as selected; all other engines will be de-selected.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| number_active_ometascan | integer | Minimum number of active MetaDefender Core (ometascan) instances required to be considered healthy. Must be at least 1.  minimum: 1 |  |
| number_active_av_engines | integer | Minimum number of active anti-virus engines required to be considered healthy. Must be at least 1.  minimum: 1 |  |
| required_engines | array[string] | List of engine identifiers that must be active for the system to be considered healthy. The `7z` (Archive Extraction) and `filetype` (FileType) engines are always required and will be included regardless of whether they are present in this list. |  |

POST /admin/config/healthcheckcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpsampleResponses application/json 200

Request processed successfully. Returns the updated health check configuration.

| object | object |  |  |
| --- | --- | --- | --- |
| number_active_ometascan | integer | Minimum number of active MetaDefender Core (ometascan) instances required to be considered healthy. Must be at least 1.  minimum: 1 |  |
| number_active_av_engines | integer | Minimum number of active anti-virus engines required to be considered healthy. Must be at least 1.  minimum: 1 |  |
| engines3 fields | array[object] | List of engines available in the system together with their selection state. The `7z` (Archive Extraction) and `filetype` (FileType) engines are always required and will always be returned with `is_selected: true`. |  |
| display_name | string | Human readable name of the engine. |  |
| id | string | Internal engine identifier. |  |
| is_selected | boolean | Whether the engine is selected as required for the health check. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response sample
### Session settings

Configure settings for session generated upon a successful login
See more at [Login](/docs/mdcore/metadefender-core/ref#userlogin)

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object | API object for /admin/config/session |  |
| --- | --- | --- | --- |
| absoluteSessionTimeout | integer | The interval (in milliseconds) for overall session length timeout (regardless of activity). |  |
| allowCrossIpSessions | boolean | Allow requests from the same user to come from different IPs. |  |
| allowDuplicateSession | boolean | Allow same user to have multiple active sessions. |  |
| sessionTimeout | integer | The interval (in milliseconds) for the user's session timeout, based on last activity. Timer starts after the last activity for the apikey. |  |

PUT /admin/config/sessioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object | API object for /admin/config/session |  |
| --- | --- | --- | --- |
| absoluteSessionTimeout | integer | The interval (in milliseconds) for overall session length timeout (regardless of activity). |  |
| allowCrossIpSessions | boolean | Allow requests from the same user to come from different IPs. |  |
| allowDuplicateSession | boolean | Allow same user to have multiple active sessions. |  |
| sessionTimeout | integer | The interval (in milliseconds) for the user's session timeout, based on last activity. Timer starts after the last activity for the apikey. |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get session cookie attributes

Getting session cookie attributes

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/config/sessioncookiecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully.

| object | object | Session cookie configuration details. |  |
| --- | --- | --- | --- |
| samesite | number | SameSite attribute accepts three values:   - `Strict` - cookies will only be sent in a first-party context, not be sent along with requests initiated by third party websites. - `Lax` - cookies are not sent on normal cross-site subrequests, but are sent when a user is navigating to the origin site. - `None` - cookies will be sent in all contexts.   Default value: `Lax` |  |

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Update session cookie attributes

Modifying session cookie attributes

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object | Session cookie configuration details. |  |
| --- | --- | --- | --- |
| samesite | number | SameSite attribute accepts three values:   - `Strict` - cookies will only be sent in a first-party context, not be sent along with requests initiated by third party websites. - `Lax` - cookies are not sent on normal cross-site subrequests, but are sent when a user is navigating to the origin site. - `None` - cookies will be sent in all contexts.   Default value: `Lax` |  |

PUT /admin/config/sessioncookiecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully.

| object | object | Session cookie configuration details. |  |
| --- | --- | --- | --- |
| samesite | number | SameSite attribute accepts three values:   - `Strict` - cookies will only be sent in a first-party context, not be sent along with requests initiated by third party websites. - `Lax` - cookies are not sent on normal cross-site subrequests, but are sent when a user is navigating to the origin site. - `None` - cookies will be sent in all contexts.   Default value: `Lax` |  |

403

Invalid user information or Not Allowed

404

Requests resource was not found.

500

Unexpected event on server.

 Response
## Workers

Connect, deploy, undeploy and manage workers.

Endpoints[POST/admin/worker](/docs/mdcluster/control-center#postconnect-to-workers) [GET/admin/worker](/docs/mdcluster/control-center#getlist-connected-workers) [DELETE/admin/worker](/docs/mdcluster/control-center#deletedisconnect-from-workers) [GET/admin/worker/instance/deploy/available/{installer_id}](/docs/mdcluster/control-center#getget-available-workers-by-installer-id) [POST/admin/worker/instance/deploy](/docs/mdcluster/control-center#postdeploy-workers) [DELETE/admin/worker/instance/deploy](/docs/mdcluster/control-center#deleteundeploy-workers) [POST/admin/worker/instance/upgrade](/docs/mdcluster/control-center#postupgrade-deployed-instances) [GET/admin/worker/instance/upgrade/version](/docs/mdcluster/control-center#getget-upgradable-instance-version)
### Connect to workers

Connect to MetaDefender Cluster Worker services.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| array | array[object] | A list of workers and their connection details. |  |
| --- | --- | --- | --- |
| display_name | string | Display name for the worker. |  |
| host | string | The address of the worker. |  |
| port | number | The port on which the worker is listening. |  |
| connection_key | string | The connection key for the worker. |  |

POST /admin/workercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to add service was successful

| array | array[object] | list of worker status. |  |
| --- | --- | --- | --- |
| display_name | string | Display name for the worker. |  |
| host | string | The address of the worker. |  |
| port | number | The port on which the worker is listening. |  |
| result | string | Connection attempt result.  Enum: `ok`,`failed` |  |
| worker_id | string | Present only when result = ok. Unique identifier of the worker. |  |
| error | string | Present only when result = failed. Error message. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### List connected workers

Retrieve a list of currently connected MetaDefender Cluster Worker services.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/workercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

A list of connected workers.

| array | array[object] | A list of connected workers and their details. |  |
| --- | --- | --- | --- |
| worker_id | string | Unique identifier of the worker. |  |
| display_name | string | Display name for the worker. |  |
| platform | string | Operating system / platform of the worker. |  |
| os | string | Operating system details of the worker. |  |
| package_type | string | The deployment package type. |  |
| hardware3 fields | object | Hardware information. |  |
| cpu3 fields | object |  |  |
| count | integer | Number of CPU cores. |  |
| model | string | CPU model name. |  |
| usage | number | CPU usage percentage. |  |
| disk | object |  |  |
| available_bytes | integer | Available disk space in bytes. |  |
| total_bytes | integer | Total disk space in bytes. |  |
| memory | object |  |  |
| available_bytes | integer | Available memory in bytes. |  |
| total_bytes | integer | Total memory in bytes. |  |
| user_name | string | Name of the user who added the worker. |  |
| host | string | The address (IP or hostname) of the worker. |  |
| port | integer | Port on which the worker is listening. |  |
| status | string | Current status of worker. |  |
| status_description | string | The description of worker's status |  |
| version | string | The version of the worker. |  |
| deployment_info5 fields | object | Deployment related information. This field is only available when instance is deployed. |  |
| type | string | Deployment type, can be `ometascan` or `api-gateway`. |  |
| installer_id | string | Identifier of the installer. |  |
| version | string | The instance version. |  |
| user_name | string | Name of the user who deployed the instance. |  |
| custom_config | object | Custom configuration for deployed instance. |  |

Expand 400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Disconnect from workers

Disconnect from specified MetaDefender Cluster Worker services.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| array | array[string] | A list of worker IDs to disconnect. |  |
| --- | --- | --- | --- |

DELETE /admin/workercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to disconnect workers was successful

| object | object | Map of worker IDs to disconnection (deletion) status. |  |
| --- | --- | --- | --- |
| worker_id | string | Disconnection status of the worker.  Enum: `Deleted` |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get available workers by installer_id.

Retrieve the list of available workers eligible for deployment for the specified installer ID.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/worker/instance/deploy/available/{installer_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to get available workers was successful

| array | array[object] | A list of connected workers and their details. |  |
| --- | --- | --- | --- |
| worker_id | string | Unique identifier of the worker. |  |
| display_name | string | Display name for the worker. |  |
| platform | string | Operating system / platform of the worker. |  |
| os | string | Operating system details of the worker. |  |
| package_type | string | The deployment package type. |  |
| hardware3 fields | object | Hardware information. |  |
| cpu3 fields | object |  |  |
| count | integer | Number of CPU cores. |  |
| model | string | CPU model name. |  |
| usage | number | CPU usage percentage. |  |
| disk | object |  |  |
| available_bytes | integer | Available disk space in bytes. |  |
| total_bytes | integer | Total disk space in bytes. |  |
| memory | object |  |  |
| available_bytes | integer | Available memory in bytes. |  |
| total_bytes | integer | Total memory in bytes. |  |
| user_name | string | Name of the user who added the worker. |  |
| host | string | The address (IP or hostname) of the worker. |  |
| port | integer | Port on which the worker is listening. |  |
| status | string | Current status of worker. |  |
| status_description | string | The description of worker's status |  |
| version | string | The version of the worker. |  |
| deployment_info5 fields | object | Deployment related information. This field is only available when instance is deployed. |  |
| type | string | Deployment type, can be `ometascan` or `api-gateway`. |  |
| installer_id | string | Identifier of the installer. |  |
| version | string | The instance version. |  |
| user_name | string | Name of the user who deployed the instance. |  |
| custom_config | object | Custom configuration for deployed instance. |  |

Expand 400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Deploy workers

Deploy the selected installer on one or more selected workers.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body Deploy MetaDefender CoreDeploy MetaDefender Cluster API GatewayDeploy MetaDefender Cluster Callback Serviceapplication/json

| object | object |  |  |
| --- | --- | --- | --- |
| type | string | Enum: `ometascan` |  |
| installer_id | string | Identifier of the installer. |  |
| worker | array[string] | List of worker IDs to deploy to. |  |
| config | object | Optional configuration for ometascan worker. |  |
| log_level | string | Enum: `debug`,`info`,`warning`,`error`  Default: info |  |
| connection_per_file_service | integer | minimum: 1  Default: 4 |  |

POST /admin/worker/instance/deploycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to add service was successful

| object | object | Map of worker IDs to deployment status ("Deploying") or an error message. |  |
| --- | --- | --- | --- |
| * | string | "Deploying" if deployment initiated successfully; otherwise an error message. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Undeploy workers

Undeploy the specified workers.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| array | array[string] |  |  |
| --- | --- | --- | --- |

DELETE /admin/worker/instance/deploycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to undeploy workers was successful

| object | object | Map of worker IDs to undeployment status ("Undeploying") or an error message. |  |
| --- | --- | --- | --- |
| * | string | "Undeploying" if undeployment initiated successfully; otherwise an error message. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Upgrade deployed instances

Upgrade the deployed instances managed by the worker to a newer version

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object | Parameters to upgrade deployed worker instances. |  |
| --- | --- | --- | --- |
| version | string | Target version to upgrade to. |  |
| type | string | Worker deployment type.  Enum: `ometascan`,`api-gateway`,`callback-service` |  |

POST /admin/worker/instance/upgradecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to upgrade workers was successful

| object | object | Upgrade request accepted. |  |
| --- | --- | --- | --- |
| result | string |  |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get upgradable instance version

Retrieve a list of available versions of MetaDefender Core and MetaDefender Cluster API Gateway for upgrading.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/worker/instance/upgrade/versioncURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

A list of available versions for upgrading.

| object | object |  |  |
| --- | --- | --- | --- |
| ometascan | array[string] |  |  |
| api-gateway | array[string] |  |  |
| callback-service | array[string] |  |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
## Services

Add essential services and view connection status.

Endpoints[POST/admin/service](/docs/mdcluster/control-center#postconnect-and-check-essential-services-status) [GET/admin/service](/docs/mdcluster/control-center#getget-the-status-of-all-essential-services) [PUT/admin/service/{service_id}](/docs/mdcluster/control-center#putedit-service-details) [DELETE/admin/service/{service_id}](/docs/mdcluster/control-center#deletedisconnect-to-service-and-remove-their-configurations) [GET/admin/service/{service_type}](/docs/mdcluster/control-center#getget-status-for-a-specific-service) [PUT/admin/service/{service_type}/setting](/docs/mdcluster/control-center#putedit-setting-of-service) [GET/admin/service/{service_type}/setting](/docs/mdcluster/control-center#getget-service-settings)
### Connect and check essential services status.

Establish connections and retrieve the status of essential services within the MetaDefender Cluster system.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body File Storage ConfigurationDataLake, DataWarehouse or Broker ConfigurationCaching Configurationapplication/json

| object | object | service type `filestorage` configuration details |  |
| --- | --- | --- | --- |
| host | string | the host address of the service. |  |
| port | integer | the port number of the service. |  |
| connection_key | string | the connection key for the service. |  |

POST /admin/servicecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to add service was successful

| array | array[object] | A list of service id and their status. |  |
| --- | --- | --- | --- |
| result | string | the result of the service addition, can be either "ok" or "error" |  |
| service_id | string | The unique identifier of the service if result is "ok" |  |
| detail | string | The error details if result is "error" |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get the status of all essential services.

Retrieve the status of all added services within the MetaDefender Cluster system.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/servicecURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Details of all added services and their status.

| object | object | Keyed by service type (e.g. broker, caching, datalake, filestorage, warehouse). |  |
| --- | --- | --- | --- |
| service_type4 fields | object | service type (e.g. broker, caching, datalake, filestorage, warehouse) |  |
| healthy_instances | number | Number of healthy instances for the service. |  |
| overall_status | string | Aggregated status across all instances of the service. |  |
| overall_status_description | string | Description of the overall status. |  |
| instances11 fields | array[object] | List of all replicated instances for the service. |  |
| service_id | string | Unique service identifier. |  |
| message | string | Optional status/message. |  |
| display_name | string | Human friendly name. Defaults to "host:port" if absent. |  |
| status_description | string | Human readable status explanation. |  |
| host | string | Hostname or IP. |  |
| port | number | Service's port. |  |
| version | string | Service version (semantic or other). |  |
| added_by | string | User or system that registered the service. |  |
| last_update | number | Unix epoch milliseconds of last update. |  |
| last_healthy | number | Unix epoch milliseconds of last confirmed healthy state. |  |
| detail6 fields | object | Service specific diagnostic details (structure varies by service). |  |
| cpu_usage | number | CPU usage (implementation specific units). |  |
| platform | string | Operating system/platform the service is running on. |  |
| role | string | Service role (e.g. primary, secondary). |  |
| db_size | number | Database size in bytes. |  |
| ram | object | Memory usage details. |  |
| total_bytes | number | Total RAM available. |  |
| used_bytes | number | RAM currently in use. |  |
| disk | object | Disk usage details. |  |
| total_bytes | number | Total disk space available. |  |
| used_bytes | number | Disk space currently in use. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Edit service details.

Update the display name and/or configuration details for a specific service.
**Note**: Service configuration cannot be modified after instances have been deployed.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object | Request payload to connect a service and optionally set display name and configuration. |  |
| --- | --- | --- | --- |
| display_name | string | Display name for the service. |  |
| config5 fields | object | service configuration details |  |
| host | string | the host address of the service |  |
| port | integer | the port number of the service |  |
| user | string | the user name for the service. Applicable for type `caching`, `broker`, `datalake`, and `warehouse` |  |
| password | string | the password for the service. Applicable for type `caching`, `broker`, `datalake`, and `warehouse` |  |
| connection_key | string | the connection key for the service. Applicable for type `filestorage` |  |

PUT /admin/service/{service_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to add service was successful

| object | object | Service record plus last known health/status info. |  |
| --- | --- | --- | --- |
| service_id | string | Unique service identifier. |  |
| message | string | Optional status/message. |  |
| display_name | string | Human friendly name. Defaults to "host:port" if absent. |  |
| status_description | string | Human readable status explanation. |  |
| host | string | Hostname or IP. |  |
| port | number | Service's port. |  |
| version | string | Service version (semantic or other). |  |
| added_by | string | User or system that registered the service. |  |
| last_update | number | Unix epoch milliseconds of last update. |  |
| last_healthy | number | Unix epoch milliseconds of last confirmed healthy state. |  |
| detail6 fields | object | Service specific diagnostic details (structure varies by service). |  |
| cpu_usage | number | CPU usage (implementation specific units). |  |
| platform | string | Operating system/platform the service is running on. |  |
| role | string | Service role (e.g. primary, secondary). |  |
| db_size | number | Database size in bytes. |  |
| ram | object | Memory usage details. |  |
| total_bytes | number | Total RAM available. |  |
| used_bytes | number | RAM currently in use. |  |
| disk | object | Disk usage details. |  |
| total_bytes | number | Total disk space available. |  |
| used_bytes | number | Disk space currently in use. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Disconnect to service and remove their configurations.

Remove the connection and configuration details for a specific service.
**Note**: Service configuration cannot be deleted after instances have been deployed.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

DELETE /admin/service/{service_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to remove service was successful

| object | object | Response indicating the service has been removed. |  |
| --- | --- | --- | --- |
| service_id | string |  |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get status for a specific service.

Retrieve the current status of a specific service, including all instance details.
**Note**: The `service_type` must be one of: `datalake`, `warehouse`, `caching`, `broker`, `filestorage`.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/service/{service_type}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to get service type was successful

| object | object | Status information for a specific service type including instance details. |  |
| --- | --- | --- | --- |
| overall_status | string | Aggregated status for the service type (e.g. healthy, degraded, down) |  |
| overall_status_description | string | Human readable description of the aggregated status |  |
| healthy_instances | number | Count of instances currently considered healthy |  |
| instances11 fields | array[object] | List of discovered service instances |  |
| service_id | string | Unique service identifier. |  |
| message | string | Optional status/message. |  |
| display_name | string | Human friendly name. Defaults to "host:port" if absent. |  |
| status_description | string | Human readable status explanation. |  |
| host | string | Hostname or IP. |  |
| port | number | Service's port. |  |
| version | string | Service version (semantic or other). |  |
| added_by | string | User or system that registered the service. |  |
| last_update | number | Unix epoch milliseconds of last update. |  |
| last_healthy | number | Unix epoch milliseconds of last confirmed healthy state. |  |
| detail6 fields | object | Service specific diagnostic details (structure varies by service). |  |
| cpu_usage | number | CPU usage (implementation specific units). |  |
| platform | string | Operating system/platform the service is running on. |  |
| role | string | Service role (e.g. primary, secondary). |  |
| db_size | number | Database size in bytes. |  |
| ram | object | Memory usage details. |  |
| total_bytes | number | Total RAM available. |  |
| used_bytes | number | RAM currently in use. |  |
| disk | object | Disk usage details. |  |
| total_bytes | number | Total disk space available. |  |
| used_bytes | number | Disk space currently in use. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Edit setting of service

Update the configuration settings for a specific service.
**Note**: Supported only for the `filestorage` service type.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| max_replica | number | Maximum number of replicas, default is 1 |  |
| min_replica | number | Minimum number of replicas, default is 1 |  |
| cleanuprange | number | Cleanup interval in hours, default is 0 |  |
| storage | object | At-rest data protection |  |
| type | string | Storage backend type, can be `salt` or `none` |  |
| config | object | Backend specific configuration |  |

PUT /admin/service/{service_type}/settingcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to add service was successful

| object | object | Response schema for successful service setting update |  |
| --- | --- | --- | --- |
| result | string | Success message |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get service settings

Retrieve the current configuration settings for a specific service.
**Note**: Supported only for the `filestorage` service type.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/service/{service_type}/settingcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request to retrieve service settings was successful

| object | object |  |  |
| --- | --- | --- | --- |
| max_replica | number | Maximum number of replicas, default is 1 |  |
| min_replica | number | Minimum number of replicas, default is 1 |  |
| cleanuprange | number | Cleanup interval in hours, default is 0 |  |
| storage | object | At-rest data protection |  |
| type | string | Storage backend type, can be `salt` or `none` |  |
| config | object | Backend specific configuration |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
## Installers

Upload and manage installers for the MetaDefender Core and MetaDefender Cluster API Gateway.

Endpoints[POST/admin/installer](/docs/mdcluster/control-center#postupload-installer) [GET/admin/installer](/docs/mdcluster/control-center#getget-uploaded-installers) [DELETE/admin/installer/{installer_id}](/docs/mdcluster/control-center#deletedelete-an-uploaded-installer)
### Upload installer

Upload installers for the MetaDefender Core, MetaDefender Cluster API Gateway and MetaDefender Cluster Callback Service.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |
| filename | string | The name of the installer file to upload. **Note**: Ensure the filename remains same with the original MY OPSWAT download (e.g: ometascan-5.15.0-1-x64.msi) |  |

Request Body application/octet-stream

| file | file | Optional installer file content (binary). Send raw bytes of the installer. |  |
| --- | --- | --- | --- |

POST /admin/installercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| installer_id | string | Unique identifier of the uploaded installer. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
### Get uploaded installers

Retrieve information about an uploaded installer.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

GET /admin/installercURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object | Map of installer IDs to installer details. |  |
| --- | --- | --- | --- |
| *8 fields | object |  |  |
| checksum | string | SHA256 checksum of the installer file. |  |
| name | string | Original file name of the installer. |  |
| platform | string | Target platform / package type. |  |
| size | number | Size of the installer file in bytes. |  |
| type | string | Product type of the installer. |  |
| upload_by | string | Identifier of the user or node that uploaded the installer. |  |
| upload_timestamp | number | Upload time as Unix epoch milliseconds. |  |
| version | string | Version extracted from the installer. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

500

Unexpected event on server.

 Response
### Delete an uploaded installer

Delete an uploaded installer.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-distributed-cluster/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
| --- | --- | --- | --- |

DELETE /admin/installer/{installer_id}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Request processed successfully

| object | object |  |  |
| --- | --- | --- | --- |
| result | string | Success message. |  |

400

Bad Request (e.g. header is invalid, apikey is missing or invalid, parameter value is invalid or out of range, etc).

403

Invalid user information or Not Allowed

404

Requests resource was not found.

405

The user has no rights for this operation.

500

Unexpected event on server.

 Response
## Stats

Readiness probing for the MetaDefender Cluster Control Center.

Endpoints[GET/readyz](/docs/mdcluster/control-center#controlcenterreadyz)
### Get readiness status

Report whether the MetaDefender Cluster Control Center is ready to accept administrative operations such as uploading installers, deploying instances and managing MetaDefender Cluster Workers. Intended as a readiness probe, so it requires no authentication. Returns `200` when every backing service is healthy, and `503` when at least one is not, meaning those operations may fail or be rejected until it recovers. The response body is empty unless `verbose=true` is supplied.

Auth NoneQuery String

| verbose | boolean | Optional. Return the per-component readiness detail instead of an empty body. |  |
| --- | --- | --- | --- |

GET /readyzcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

The MetaDefender Cluster Control Center is ready; every backing service is healthy.

| object | object | MetaDefender Cluster Control Center readiness status. Returned only when the request carries `verbose=true`; otherwise the response body is empty. |  |
| --- | --- | --- | --- |
| status | boolean | Overall readiness. `true` only when every component below is healthy. |  |
| components8 fields | object | Per-dependency readiness detail. |  |
| status | boolean | Aggregate component status, identical to the top-level `status`. |  |
| clusterdb | object | MetaDefender Cluster Control Center configuration database status. |  |
| status | boolean | Configuration database overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |
| caching | object | Caching service status. |  |
| status | boolean | Caching service overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |
| broker | object | Message broker status. |  |
| status | boolean | Message broker overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |
| filestorage | object | MetaDefender Cluster File Storage service status. |  |
| status | boolean | MetaDefender Cluster File Storage overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |
| datalake | object | Data lake database status. |  |
| status | boolean | Data lake overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |
| datawarehouse | object | Data warehouse database status. |  |
| status | boolean | Data warehouse overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |
| identity | object | MetaDefender Cluster Identity Service status. |  |
| status | boolean | MetaDefender Cluster Identity Service overall status. |  |
| detail | string | Reason the component is unhealthy. Empty when healthy. |  |

503

The MetaDefender Cluster Control Center is not ready; at least one backing service is unhealthy. Administrative operations may fail until it recovers.

 Response
