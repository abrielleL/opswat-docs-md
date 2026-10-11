<!-- source: https://www.opswat.com/docs/cm/direct-instance-management/ref -->

## Direct Connection Support in CM10

My OPSWAT Central Management (MOCM) supports initiating a direct connection to MetaDefender (MD) product instances, enabling the execution of product-specific APIs and supported commands. The following OPSWAT products currently support this feature:

- MetaDefender CORE (version 5.15.0 and above)
- MetaDefender ICAP (version 5.9.0 and above)

### How it works

MD Core/ICAP must first be registered with the MOCM. Once enrolled, MOCM can effectively manage MD Core/ICAP instances.

When an administrator invokes MOCM APIs, MOCM authenticates the request and then forwards it to the appropriate Product Instance APIs.

Administrators do not need to enable inbound traffic from users to MD instances. All requests are securely routed from MOCM directly to the MD instances.

### Steps to make API requests

Once the product instance is enrolled in CM10, adminstrator can follow these steps to make an api request to the instance

1. **Get `OAuth API Access token` from MOCM**

   Go to MOCM console page and setup application to get an access token:
3. **Obtain the `connectionID`**

   Retrieve the `connectionID` from the relevant product instance.
6. **Construct the API Request**
   - **Build the URL:** Combine the MOCM endpoint URL with the retrieved `connectionID`.
   - **Prepare the Request Body:** Include the required data exactly as specified in the product support documentation.
   - **Set the Required Headers:**
     - `X-App-Method`: Specify the original HTTP method (e.g., `GET`, `POST`).
     - `X-App-Url`: Provide the original request path.
     - Include any optional headers from the original request using the format: `X-App-Header-{headerKey}`.

For detailed examples, please refer to the documentation:
[View Documentation](https://www.opswat.com/_permalink/367527)

Serverhttps://product.my.us.opswat.com

My OPSWAT Central Management US tenant

https://product.my.eu.opswat.com

My OPSWAT Central Management EU tenant

Server Variables## Authenticationhttp BearerToken

Users authenticate using a Client ID and Client Secret, which can be obtained from My OPSWAT Central Management.

## Auth

BearerToken

Endpoints[POST/o/oauth2/token](/docs/cm/direct-instance-management#postget-oauth-api-token)
### Get Oauth API Token

To retrieve your Client ID and Client Secret, please follow this link:
<https://www.opswat.com/docs/cm/developer-guidelines/how-to-work-with-apis>

Auth NoneRequest Body application/x-www-form-urlencoded

Required information to generate token

| object | object |  |  |
| --- | --- | --- | --- |
| client_id | string | Client Id of MyOpswat Central Management Account |  |
| client_secret | string | Client Secret of MyOpswat Central Management Account |  |
| grant_type | string | client_credentials |  |

POST /o/oauth2/tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

response

| Root Type for Oauth_reponse_data | object |  |  |
| --- | --- | --- | --- |
| access_token | string |  |  |
| token_type | string |  |  |
| expires_in | int32 |  |  |

 Response
## Connection_management

Manage direct connection from product instances to MyOpswat Central Management

Endpoints[GET/fusion/console/services/connection/{connectionId}](/docs/cm/direct-instance-management#getgetconnection-status) [DELETE/fusion/console/services/connection/{connectionId}](/docs/cm/direct-instance-management#deleteclose-connection) [POST/fusion/console/services/connection/request/{productType}](/docs/cm/direct-instance-management#postinitiate-direct-instance-connection)
### GetConnection status

Get Connection status by Connection ID

Auth BearerTokenGET /fusion/console/services/connection/{connectionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Get Connection Status successfully

| Root Type for InitConnectionData_reponse_success | object |  |  |
| --- | --- | --- | --- |
| connId | string |  |  |
| status | string |  |  |

400

Invalid ConnectionId

 Response
### Close connection

Close a direct connection

Auth NoneDELETE /fusion/console/services/connection/{connectionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

desc

| No response body |
| --- |

 Response
### Initiate Direct Instance Connection

Initiate a direct communication channel from CM10 to the product instance.

Auth BearerTokenPath Params

| productType | string | OPSWAT product types  Enum: `mdcore`,`mdicap` |  |
| --- | --- | --- | --- |

Request Body application/json

| Root Type for InitConnectionData | object | Data for initiating a connection from MyOpswat Central Management |  |
| --- | --- | --- | --- |
| deploymentId | string |  |  |
| Purpose | string |  |  |

POST /fusion/console/services/connection/request/{productType}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpInit connection ExampleResponses application/json 200

Init Connection successfull

| Root Type for InitConnectionData_reponse_success | object |  |  |
| --- | --- | --- | --- |
| connId | string |  |  |
| status | string |  |  |

404

Incorrect DeploymentId

 Response
## Sending_requests

Sending requests directly from My OPSWAT Central Management to product instances.

Endpoints[POST/fusion/console/services/connection/{connectionId}](/docs/cm/direct-instance-management#postsending-requestscommands)
### Sending Requests/Commands

#### Sending Requests or Commands to Product Instances

Auth NoneHeaders

| X-App-Method | string |  |  |
| --- | --- | --- | --- |
| X-App-URL | string |  |  |

Request Body application/json

| string | string |  |  |
| --- | --- | --- | --- |

POST /fusion/console/services/connection/{connectionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpDataBodyCreate CORE USer sampleResponses application/json 200

| string | string |  |  |
| --- | --- | --- | --- |

 Response Example
## Pmp

Endpoints[POST/o/pmp/v1/reports/details](/docs/cm/direct-instance-management#getpmpreportdetails) [POST/o/pmp/v1/reports](/docs/cm/direct-instance-management#getpmpreports) [POST/o/pmp/v1/kiosk/configuration](/docs/cm/direct-instance-management#updateruleskiosk)
### Get PMP Report Details

Retrieve the details of a PMP report - including MetaDefender Kiosk, MetaDefender Drive - using the report's session ID. This API returns data as a stream.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| session_id | string | session ID. |  |
| filter | object |  |  |
| issue_type | array[string] | Specify what issue type used to filter along with the field.  Enum: `VUL(vulnerability)`,`COO`,`SENSITIVE`,`SKIPPED`,`INFECTED` |  |

POST /o/pmp/v1/reports/detailscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| id | string | ID |  |
| timestamp | long | timestamp when the report occurs |  |
| sync_time | long | timestamp when the report sent to My Opswat Central Management |  |
| session_id | string | session id of the report |  |
| file_name | string | file name |  |
| file_path | string | file path |  |
| pmp_type | string | issue type |  |
| device_id | string | Device id of a device that the report occurred on |  |
| device_type | string | Device type of a device that the event occurred on |  |
| device_name | string | Device name of a device that the report occurred on |  |
| md5 | string | md5 of the file |  |
| sha1 | string | sha1 of the file |  |
| sha256 | string | sha256 of the file |  |

 Response
### Get PMP Reports

Retrieve reports of PMP devices - including MetaDefender Kiosk, MetaDefender Endpoint - in the cursor fashion, sorted by reported time in ascending order.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| token | string | Pagination token to retrieve the next set of items. |  |
| limit | integer | Maximum number of devices to return. The value should be in [1,100].  Default: 20 |  |
| start_time | long | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds The value must be greater than zero, and it must not be more than 30 days from the current date. |  |
| end_time | long | Specify an end time of the query's duration. The format should be Unix epoch time in milliseconds. |  |
| filter3 fields | object |  |  |
| device_type | array[string] | Specify what device type used to filter along with the field.  Enum: `EM`,`KIOSK`,`MK5` |  |
| media_type | array[string] | Specify what media type used to filter along with the field. |  |
| issue_type | array[string] | Specify what issue type used to filter along with the field.  Enum: `VUL(vulnerability)`,`COO`,`SENSITIVE`,`SKIPPED`,`INFECTED` |  |

POST /o/pmp/v1/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| token | string | Pagination token |  |
| data18 fields | array[object] |  |  |
| timestamp | long | timestamp when the report occurs |  |
| sync_time | long | timestamp when the report sent to My Opswat Central Management |  |
| session_id | string | session id of the report |  |
| report_id | string | report id of the report |  |
| user_name | string | User logged-in ID who logged into a device when the report occurred |  |
| device_name | string | Device name that the report occurred on |  |
| device_id | string | Device id of a device that the report occurred on |  |
| device_type | string | Device type of a device that the event occurred on |  |
| device_group | string | A device's group name |  |
| media_type | string | media type |  |
| total_infected | integer | total infected files in the report |  |
| total_vulnerability | integer | total vulnerable files in the report |  |
| total_sensitive | integer | total sensitive files in the report |  |
| total_coo | integer | total coo detection files in the report |  |
| total_skipped | integer | total skipped files in the report |  |
| total_files_scanned | integer | total scanned files in the report |  |
| total_sanitized | integer | total sanitized files in the report |  |
| total_threat | integer | total issued files in the report |  |

 Response
### Update Yara rules and file hashes for MetaDefender Kiosk

Update Yara rules and file hashes for MetaDefender Kiosk

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| apply_type | string | Values: - all: apply for all instances - instances: apply for specific instances in |  |
| apply_to | array[string] | The list of instance IDs will be updated the file hashes and Yara rules. |  |
| yara_sources | object |  |  |
| type | string | Possible values: - append: will append to existing yara rules - overwrite: will overwrite all yara rules |  |
| skip_by_hash | object |  |  |
| type | string | Possible values: - append: will append to existing yara rules - overwrite: will overwrite all yara rules |  |

POST /o/pmp/v1/kiosk/configurationcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| total_applied | integer | The number of instances will be applied the Yara rules and file hashes. Note that My OPSWAT Central Management will save this change and will send to MetaDefender Kiosk next time it checks in with My OPSWAT Central Management. |  |

 Response
## Meta Defender Drive

MetaDefender Drive.

Endpoints[POST/o/mdd/v1/reports](/docs/cm/direct-instance-management#getdrivereports) [POST/o/mdd/v1/reports/details](/docs/cm/direct-instance-management#getdrivereportdetails) [POST/o/mdd/v1/reports/scanned-hosts](/docs/cm/direct-instance-management#get-metadefender-drive-scanned-host-list) [GET/o/mdd/v1/reports/scanned-hosts/{serial_number}](/docs/cm/direct-instance-management#get-metadefender-drive-scanned-host-detail)
### Get MetaDefender Drive Reports

Receive MetaDefender Drive's reports in the cursor fashion, sorted by reported time in ascending order.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| token | string | Pagination token to retrieve the next set of items. |  |
| limit | integer | Maximum number of devices to return. The value should be in [1,100].  Default: 20 |  |
| start_time | long | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds The value must be greater than zero, and it must not be more than 30 days from the current date. |  |
| end_time | long | Specify an end time of the query's duration. The format should be Unix epoch time in milliseconds. |  |
| filter3 fields | object |  |  |
| scanned_host | array[string] |  |  |
| scanned_by | array[string] |  |  |
| issue_type | array[string] | Specify what issue type used to filter along with the field.  Enum: `VUL(vulnerability)`,`COO`,`SENSITIVE`,`SKIPPED`,`INFECTED` |  |

POST /o/mdd/v1/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| token | string | Pagination token |  |
| data16 fields | array[object] |  |  |
| timestamp | long | timestamp when the report occurs |  |
| sync_time | long | timestamp when the report sent to My Opswat Central Management |  |
| session_id | string | session id of the report |  |
| hardware_model | string | hardware model of a device that the report occurred on |  |
| scan_profile | string | scanning profile |  |
| scanned_host | string |  |  |
| scanned_by | string |  |  |
| device_group | string | A device's group name |  |
| total_infected | integer | total infected files in the report |  |
| total_vulnerability | integer | total vulnerable files in the report |  |
| total_sensitive | integer | total sensitive files in the report |  |
| total_coo | integer | total coo detection files in the report |  |
| total_skipped | integer | total skipped files in the report |  |
| total_files_scanned | integer | total scanned files in the report |  |
| total_sanitized | integer | total sanitized files in the report |  |
| total_threat | integer | total issued files in the report |  |

 Response
### Get MetaDefender Drive Report Details

Retrieve the MetaDefender Drive report details by using the report ID and device ID. This API returns data as a stream.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| device_id | string | the device ID |  |
| report_id | string | the report ID |  |
| filter | object |  |  |
| issue_type | array[string] | Specify what issue type used to filter along with the field.  Enum: `VUL(vulnerability)`,`COO`,`SENSITIVE`,`SKIPPED`,`INFECTED` |  |

POST /o/mdd/v1/reports/detailscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| id | string | ID |  |
| timestamp | long | timestamp when the report occurs |  |
| sync_time | long | timestamp when the report sent to My Opswat Central Management |  |
| session_id | string | session id of the report |  |
| file_path | string | file path |  |
| threat_type | string | issue type |  |
| device_id | string | Device id of a device that the report occurred on |  |
| device_group | string | Device group of a device that the report occurred on |  |
| sha256 | string | sha256 of the file |  |

 Response
### Get MetaDefender Drive Scanned Host List

Returns a paginated list of scanned hosts for the account, with one entry per host serial number. Each entry includes the user who scanned the host, its vendor, model, operating system, total scan sessions, and the last reported time.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| limit | integer | Number of items to return per page. If the value is less than or equal to 0, the default page size of 25 is used. Values greater than 100 are not allowed.  Default: 25 |  |
| start_time | integer | Only include hosts that reported on or after the specified time. Enter 0 to include all hosts. |  |
| end_time | integer | The latest report time to include in the results, in epoch milliseconds. Set this value to 0 to include all reports with no upper time limit. If specified, it must be greater than or equal to start_time. |  |
| page | integer | The page number to retrieve, starting from 1. Values less than 1 are automatically treated as 1.  Default: 1 |  |
| sort | string | Specify one of the following values: hostName, lastReport, vendor, model, or sessions. If an invalid value is provided, the results will be sorted by lastReport by default.  Enum: `hostName`,`lastReport`,`vendor`,`model`,`sessions`  Default: lastReport |  |
| order | string | Choose to sort in ascending or descending order.  Enum: `desc`,`asc` |  |
| search | string | Search by hostname or host serial number. The search is case-insensitive and matches any part of the text. |  |

Expand POST /o/mdd/v1/reports/scanned-hostscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| total | integer | The total number of distinct hosts matching the filter before pagination. Use this value to implement pagination |  |
| data9 fields | array[object] | the page of host rows; always present ([] when nothing matches, never null) |  |
| scanned_host | string | Host name, taken from the host's most recent report |  |
| scanned_host_serial | string | The serial number of the scan host |  |
| scanned_by3 fields | array[object] | The number of unique drives that have reported this host across all sources. |  |
| id | string | Metadefender Drive Identifier |  |
| name | string | Metadefender Drive serial number |  |
| device_type | string | The type of MetaDefender Drive device (eg: MetaDefender Drive USB). |  |
| vendor | string | The device manufacturer. This information is only available for host-only reports. If the device has only been detected through regular scans, this field will be empty. |  |
| model | string | The device model from the latest host report. If unavailable, the model from the latest scan report is used instead. |  |
| device_type | string | The operating system running on the host (for example, Windows or Linux). |  |
| scan_profile | string | The scan profiles used to scan this host. |  |
| sessions | integer | The number of completed scan sessions for the host. |  |
| last_report | integer | The timestamp (in epoch milliseconds) of the host's most recent scan report. Returns 0 if the host has no scan reports. |  |

400

Bad Request

500

Internal Server Error

 Response
### Get MetaDefender Drive Scanned Host Detail

Returns detailed information about a specific host in your account, including its network addresses, hardware, disks and volumes, operating system, BIOS, logged-in user, and the drive that most recently reported it.

Auth BearerTokenGET /o/mdd/v1/reports/scanned-hosts/{serial_number}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| object | object |  |  |
| --- | --- | --- | --- |
| created_at | integer | Time when the host was first discovered (Unix epoch milliseconds). |  |
| serial_number | string | Unique serial number of the host. |  |
| host_name | string | Host name of the device. |  |
| ip | string | Primary IP address of the host. |  |
| mac | string | Primary MAC address of the host. |  |
| ip_addresses | array[string] | All detected IP addresses. |  |
| mac_addresses | array[string] | All detected MAC addresses. |  |
| public_ip_address | string | Public IP address, if available. |  |
| cpu | string | CPU model. |  |
| cpu_cores | string | Number of CPU cores. |  |
| memory | string | Total system memory in a human-readable format. |  |
| memory_total_mb | integer | Total system memory in MB. |  |
| brand_name | string | Device manufacturer and model. |  |
| vendor | string | Device manufacturer. |  |
| model | string | Device model. |  |
| firmware_version | string | BIOS or firmware version. |  |
| host_os | string | Operating system reported by the host. |  |
| os_name | string | Operating system name. |  |
| os_version | string | Operating system version or build number. |  |
| os_architecture | string | Operating system architecture (for example, 64-bit). |  |
| os_type | string | Operating system family (such as Windows or Linux). |  |
| machine_uuid | string | Unique hardware UUID of the host. |  |
| logged_in_user | string | User logged in when the device was scanned. |  |
| domain_name | string | Active Directory domain or workgroup name. |  |
| bios_info3 fields | object | BIOS information, including name, version, and release_date. |  |
| name | string |  |  |
| version | string |  |  |
| release_date | string |  |  |
| location8 fields | object | Geographic location information, when available. |  |
| country | string |  |  |
| country_code | string |  |  |
| region | string |  |  |
| region_name | string |  |  |
| city | string |  |  |
| longitude | string |  |  |
| latitude | string |  |  |
| zip | string |  |  |
| drive_info3 fields | object | Information about the drive that most recently reported this host. |  |
| device_id | string |  |  |
| device_name | string |  |  |
| physical_disks10 fields | array[object] | List of physical storage devices detected on the host. |  |
| friendly_name | string | Display name of the disk. |  |
| model | string | Disk model. |  |
| serial_number | string | Disk serial number. |  |
| size | integer | Total disk capacity in bytes. |  |
| bus_type | integer | Storage bus type (for example, 17 = NVMe). |  |
| media_type | integer | Storage media type (for example, 4 = SSD). |  |
| health_status | integer | Current health status of the disk (for example, 0 = Healthy). |  |
| free_percentage | integer | Percentage of free space available (for example, 0.64 = 64%). |  |
| operational_status | array[integer] | Current operational status of the disk (for example, 2 = OK). |  |
| volumes6 fields | array[object] | Volumes available on the disk. |  |
| drive_letter | string | Drive letter (for example, C:). |  |
| file_system | string | File system type (such as NTFS). |  |
| size | integer | Volume size in bytes. |  |
| health_status | integer | Current health status of the volume (for example, 0 = Healthy). |  |
| operational_status | array[integer] | Current operational status of the volume (for example, 2 = OK). |  |
| volume_id | string | Unique volume identifier. |  |
| port_services | string | Reported network services, when available |  |
| remote_connections | string | Reported remote connections, when available. |  |
| role | string | Device role, if reported. |  |
| site_zone | string | Site or zone associated with the device, if available. |  |
| last_scanned | integer | Time when the host was last scanned (Unix epoch milliseconds). |  |
| protocol_usage | string | Reported network protocol usage, when available. |  |
| bios_release_date | integer | The date and time when the computer’s BIOS was released. A value of 0 means this information is not available |  |
| bios_type | string | The type of firmware your computer uses, such as UEFI or BIOS |  |
| secure_boot | string | Whether Secure Boot is turned on or off, as reported by the computer (e.g., enabled or disabled). The value is stored as text and may vary depending on the computer, so it is not limited to a fixed set of values |  |
| cpu_architecture | string | Processor architecture, e.g. x64. |  |
| processor_count | integer | The number of physical processors installed on your computer |  |
| core_count | integer | The total number of processor cores available on the device. |  |
| memory_available_bytes | number | The amount of memory available for use when the information was collected, measured in bytes. Note that memory_total_mb represents total memory in megabytes (MB). Since these fields use different units, convert them to the same unit before comparing them |  |
| os_service_pack | string | The service pack version of the operating system, if applicable (e.g: 0.0) |  |
| os_product_id | string | The operating system's product id |  |
| os_language | string | Shows the language and region currently set on the operating system, e.g: English (United States) |  |
| os_install_time | integer | The date and time when the operating system was installed on the device. 0 means this information is not available |  |
| ie_version | string | The version of Internet Explorer installed on the device, if available |  |
| ie_service_pack | string | The service pack version of Internet Explorer installed on the device, if available |  |
| ie_update_version | string | The version number of Internet Explorer installed on the device, if available |  |
| windows_directory | string | The Windows folder path (e.g: C:\WINDOWS) where Windows is installed. Backslashes are displayed as entered |  |
| system_directory | string | The system folder (e.g: C:\WINDOWS\system32) |  |
| system_drive_total_bytes | integer | The total capacity of the drive where the operating system is installed, measured in bytes |  |
| system_drive_free_bytes | integer | Free space available on the same drive, measured in bytes |  |
| boot_device | string | Identifies the device or disk volume that the computer started from, such as \Device\HarddiskVolume1 |  |
| timezone | string | The computer’s local time zone, including its UTC offset (e.g: UTC+07:00 for Vietnam) |  |
| system_date_time | integer | The timestamp when the information was collected, based on the computer's system clock, in epoch milliseconds. It may differ from last_scanned if the computer's clock is inaccurate |  |

Expand 201

OK

400

Bad Request

404

Not Found

500

Internal Server Error

 Response
## Meta Defender Core

Endpoints[POST/o/core/v1/instances](/docs/cm/direct-instance-management#getcoreinstances) [POST/o/core/v1.1/reports](/docs/cm/direct-instance-management#getcorereports) [POST/o/core/v1.1/reports/processing-overview](/docs/cm/direct-instance-management#getprocessingoverview) [PUT/o/core/v1/instances/module-update-settings](/docs/cm/direct-instance-management#updatemoduleupdatesettings)
### Get MetaDefender Core Instances

Retrieve MetaDefender Core instances.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| limit | integer | Maximum number of devices to return. The value should be in [1,100]. |  |
| page | integer | The specific page number from which instances will be returned |  |
| verbose3 fields | object |  |  |
| enabled | boolean | If verbose is set to true, the system returns statistical data about the processing history within the specified start_time and end_time  Default: false |  |
| start_date | long | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds.The value must be greater than zero, and it must not exceed one year from the current date. |  |
| end_date | long | Specify an end time of the query's duration. The value must be a Unix epoch timestamp in milliseconds, greater than zero, and no more than 90 days after the start_date. |  |
| filter3 fields | object |  |  |
| deployment_ids | array[string] | List of deployment ID |  |
| group_ids | array[string] | List of group ID |  |
| tags | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |

POST /o/core/v1/instancescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| array | array[object] |  |  |
| --- | --- | --- | --- |
| id | string |  |  |
| name | string |  |  |
| deployment_id | string |  |  |
| status | string |  |  |
| health_status | string |  |  |
| version | string |  |  |
| group_id | string |  |  |
| group_name | string |  |  |
| public_ip | string |  |  |
| last_seen | string |  |  |
| last_reported | string |  |  |
| license | object |  |  |
| expiration | integer |  |  |
| type | string |  |  |
| tags | array[object] |  |  |
| key | string |  |  |
| value | string |  |  |
| verbose14 fields | object |  |  |
| total_processed_files | integer |  |  |
| total_blocked_files | integer |  |  |
| total_sanitized_files | integer |  |  |
| total_quarantined_files | integer |  |  |
| coo_detection | integer |  |  |
| spoofing | integer |  |  |
| vulnerabilities | integer |  |  |
| sensitive_data | integer |  |  |
| zero_day_protection | integer |  |  |
| threat_analysis | integer |  |  |
| oss_vulnerabilities | integer |  |  |
| insights_threat_intelligence | integer |  |  |
| known_good_bad | integer |  |  |
| threat_detection | integer |  |  |

 Response
### Get MetaDefender Core Reports

Retrieve MetaDefender Core's processing history reports using cursor-based pagination, sorted by report time in ascending order.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| token | string | Pagination token to retrieve the next set of items. |  |
| limit | integer | Maximum number of devices to return. The value should be in [1,100].  Default: 20 |  |
| start_time | long | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds.The value must be greater than zero, and it must not exceed one year from the current date. |  |
| end_time | long | Specify an end time of the query's duration. The value must be a Unix epoch timestamp in milliseconds, greater than zero, and no more than 30 days after the start_date. |  |
| filter4 fields | object |  |  |
| deployment_ids | array[string] | List of deployment ID |  |
| group_ids | array[string] | List of group ID |  |
| status | array[string] | Enum: `Blocked`,`Allowed` |  |
| request_type | array[string] | Enum: `batch`,`batched`,`extracted`,`rest` |  |

POST /o/core/v1.1/reportscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| token | string | Pagination token |  |
| data23 fields | array[object] |  |  |
| timestamp | long | timestamp when the report occurs |  |
| user | string | MD Core's user associated with an API Key used to scan the file |  |
| file_name | string | file name |  |
| status | string | status |  |
| result | string | result |  |
| data_id | string |  |  |
| parent_data_id | string |  |  |
| workflow | string | workflow |  |
| sha256 | string | sha256 of the file |  |
| deployment_id | string | deployment ID |  |
| request_type | string |  |  |
| progress_percent | integer |  |  |
| start_time | integer |  |  |
| file_size | integer |  |  |
| upload_time_ms | integer |  |  |
| processing_time_ms | integer |  |  |
| incident_types | array[string] | Security incident categories detected during the scan |  |
| verdicts | array[string] |  |  |
| actions | array[string] | Post-processing actions applied during the scan (e.g., "sanitize", "quarantine") |  |
| parent_session_ids | array[string] | dataIds of all ancestors from root to direct parent |  |
| instance_id | string | The ObjectId of the Instance that processed this scan request. |  |
| clients | array[object] | records the file's transfer log, showing who (clients.user_name) uploaded it to which product instance (clients.deployment_id, clients.product_type), and when (clients.timestamp). |  |
| file_type | object |  |  |

 Response
### Get Processing Overview

Retrieve aggregated processing statistics for MetaDefender Core instances over a specified time range. Results can optionally be broken down by groups or instances using the `group_by` field.

If both `filters.group_ids` and `filters.instance_ids` are provided, `instance_ids` is ignored.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| start_time | long | Unix epoch milliseconds. Defaults to 24h before end_time. Must be within one year from now. |  |
| end_time | long | Unix epoch milliseconds. Defaults to current time. |  |
| filters | object |  |  |
| instance_ids | array[string] | Filter by instance IDs. Ignored if group_ids is provided. |  |
| group_ids | array[string] | Filter by group IDs. Takes precedence over instance_ids. |  |
| group_by | string | Break down results by groups or instances. Omit for top-level stats only.  Enum: `groups`,`instances` |  |

POST /o/core/v1.1/reports/processing-overviewcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successful response

| object | object |  |  |
| --- | --- | --- | --- |
| total_processed_files | integer |  |  |
| total_processed_objects | integer |  |  |
| total_blocked_files | integer |  |  |
| total_blocked_objects | integer |  |  |
| total_objects_with_threats | integer |  |  |
| total_files_with_threats | integer |  |  |
| total_users_submitted_scans | integer |  |  |
| total_unique_users_submitted_scans | integer |  |  |
| avg_scan_time_per_object | integer | Avg scan time per object (ms). |  |
| avg_scan_time_per_file | integer | Avg scan time per file (ms). |  |
| groups12 fields | array[object] | Present only when group_by=groups. |  |
| group_id | string |  |  |
| group_name | string |  |  |
| total_processed_files | integer |  |  |
| total_processed_objects | integer |  |  |
| total_blocked_files | integer |  |  |
| total_blocked_objects | integer |  |  |
| total_objects_with_threats | integer |  |  |
| total_files_with_threats | integer |  |  |
| total_users_submitted_scans | integer |  |  |
| total_unique_users_submitted_scans | integer |  |  |
| avg_scan_time_per_object | integer |  |  |
| avg_scan_time_per_file | integer |  |  |
| instances12 fields | array[object] | Present only when group_by=instances. |  |
| instance_id | string |  |  |
| instance_name | string |  |  |
| total_processed_files | integer |  |  |
| total_processed_objects | integer |  |  |
| total_blocked_files | integer |  |  |
| total_blocked_objects | integer |  |  |
| total_objects_with_threats | integer |  |  |
| total_files_with_threats | integer |  |  |
| total_users_submitted_scans | integer |  |  |
| total_unique_users_submitted_scans | integer |  |  |
| avg_scan_time_per_object | integer |  |  |
| avg_scan_time_per_file | integer |  |  |

400

Bad Request – validation failure.

 Response No group_bygroup_by=instances
### Update Module Update Settings

Update the module update settings for a specific MetaDefender Core instance. Only the `source` field is modified; all other existing settings are preserved.

Auth BearerTokenRequest Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| deployment_id | string | deploymentId of the target instance. |  |
| source | string | The update source for modules.  Enum: `internet`,`folder`,`manual` |  |

PUT /o/core/v1/instances/module-update-settingscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses 200

Module update settings updated successfully. No response body.

| No response body |
| --- |

400

Bad Request – validation failure or group auto-sync policy conflict.

404

Instance not found for the given deployment_id.

500

Internal Server Error

 Response
## Account

Endpoints[POST/o/fusion/v1/account/inventory](/docs/cm/direct-instance-management#postretrieve-account-inventory-or-a-specific-product-inventory)
### Retrieve account inventory or a specific product inventory

Retrieve account inventory or a specific product inventory based on filter criteria.
productTypes: MDD (MetaDefender Drive), KIOSK (MetaDefender Kiosk K-Series), MK5 (MetaDefender Kiosk L-Series), MDCORE (MetaDefender Core), MDICAP (MetaDefender ICAP Server)

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| Root Type for filterProductTypes | object |  |  |
| --- | --- | --- | --- |
| filters | object |  |  |
| productTypes | array[string] |  |  |

POST /o/fusion/v1/account/inventorycURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| Root Type for RetrieveAccountObj | array[object] |  |  |
| --- | --- | --- | --- |
| productName | string |  |  |
| productType | string | Enum: `MDCORE` |  |
| totalInstances | int32 |  |  |
| connectivity3 fields | object |  |  |
| connected | int32 |  |  |
| nolicense | int32 |  |  |
| disconnected | int32 |  |  |
| health6 fields | object |  |  |
| operational | int32 |  |  |
| minorIssues | int32 |  |  |
| criticalIssues | int32 |  |  |
| unknown | int32 |  |  |
| significantIssues | int32 |  |  |
| blockerIssues | int32 |  |  |
| version3 fields | array[object] |  |  |
| value | string |  |  |
| total | int32 |  |  |
| status | string |  |  |
| license5 fields | object |  |  |
| expiredIn30Days | int32 |  |  |
| expiredIn90Days | int32 |  |  |
| expiredIn90PlusDays | int32 |  |  |
| expired | int32 |  |  |
| nolicense | int32 |  |  |

400

Bad Request

401

Unauthorized

500

Internal Server Error

 Response
## Meta Defender Kiosk

Endpoints[POST/o/pmp/v1/scan-report/overview](/docs/cm/direct-instance-management#postprocessing-overview-from-metadefender-kiosk-instances) [GET/o/pmp/v1/devices/{deviceId}/report/scan/{sessionId}](/docs/cm/direct-instance-management#getget-kiosk-session-detail) [GET/o/pmp/v1/kiosk/devices/{deviceId}](/docs/cm/direct-instance-management#getget-kiosk-detail) [GET/o/pmp/v1/kiosk/devices](/docs/cm/direct-instance-management#getget-kiosk-list)
### Processing Overview from MetaDefender Kiosk instances

Retrieve processing overview from MetaDefender Kiosk K-Series and L-Series instances based on filter criteria over a specified time period

Auth BearerTokenHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| Root Type for KioskOverviewReq | object |  |  |
| --- | --- | --- | --- |
| endTime | int32 | timestamp in miliseconds |  |
| startTime | int32 | timestamp in miliseconds |  |
| filters | object |  |  |
| instanceIds | array |  |  |
| groupIds | array |  |  |
| groupBy | string | Enum: `groups`,`instances` |  |

POST /o/pmp/v1/scan-report/overviewcURLRequestRequestsnet/httpGuzzleHttpClientOkHttpkioskOverviewReqResponses application/json 200

OK

| Root Type for KioskResObj | object |  |  |
| --- | --- | --- | --- |
| numberOfSessions | int32 | total number of scan sessions during the selected time period and based on the applied filters |  |
| numberOfFilesProcessed | int32 |  |  |
| numberOfSessionsWithThreatsDetected | int32 |  |  |
| numberOfThreatsFound | int32 |  |  |
| numberOfFilesSanitized | int32 |  |  |
| instances7 fields | array[object] | this array will be returned when groupBy is set to 'instances' |  |
| id | string |  |  |
| name | string |  |  |
| numberOfSessions | int32 |  |  |
| numberOfFilesProcessed | int32 |  |  |
| numberOfSessionsWithThreatsDetected | int32 |  |  |
| numberOfThreatsFound | int32 |  |  |
| numberOfFilesSanitized | int32 |  |  |

400

Bad Request

401

Unauthorized

500

Internal Server Error

 Response
### Get Kiosk session detail

Auth BearerTokenGET /o/pmp/v1/devices/{deviceId}/report/scan/{sessionId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| Root Type for GetKioskSessionDetailReq | object |  |  |
| --- | --- | --- | --- |
| deviceId | string |  |  |
| sessionId | string |  |  |
| malwareInfected | int32 |  |  |
| vulnerableApp | int32 |  |  |
| exploitProtection | int32 |  |  |
| malwareSandbox | int32 |  |  |
| cooViolation | int32 |  |  |
| privacyViolation | int32 |  |  |
| skippedFile | int32 |  |  |

401

Unauthorized

500

Internal Server Error

 Response
### Get Kiosk Detail

Auth BearerTokenGET /o/pmp/v1/kiosk/devices/{deviceId}cURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| Root Type for GetKioskDetailRes | object |  |  |
| --- | --- | --- | --- |
| deviceId | string |  |  |
| productType | string |  |  |
| deviceName | string |  |  |
| healthStatus | string |  |  |
| statusMessages | array[string] |  |  |
| modelId | string |  |  |
| hardwareVersionId | string |  |  |
| deviceType | string |  |  |
| agentVersion | string |  |  |
| isRequired | boolean |  |  |
| publicIp | string |  |  |
| location | string |  |  |
| groupId | string |  |  |
| groupName | string |  |  |
| policyId | string |  |  |
| groupPolicyId | string |  |  |
| groupPolicyName | string |  |  |
| lastSeen | int32 |  |  |
| enrolledAt | int32 |  |  |
| lastReport | int32 |  |  |
| tags | array |  |  |
| coreInfo5 fields | object |  |  |
| coreDeploymentId | string |  |  |
| coreVersion | string |  |  |
| coreId | string |  |  |
| coreName | string |  |  |
| isCoreEnrolled | boolean |  |  |
| geolocation2 fields | object |  |  |
| coordinates | object |  |  |
| latitude | string |  |  |
| longitude | string |  |  |
| country | object |  |  |
| friendlyName | string |  |  |
| iso2Code | string |  |  |
| properties7 fields | object |  |  |
| biosVersion | string |  |  |
| hardware3 fields | object |  |  |
| manufacturer | string |  |  |
| model | string |  |  |
| serialNumber | string |  |  |
| network3 fields | array[object] |  |  |
| adapterName | string |  |  |
| ipv4 | string |  |  |
| macAddress | string |  |  |
| hostName | string |  |  |
| kioskVersion | string |  |  |
| osInfo | string |  |  |
| hardenedImageVersion | string |  |  |
| configurationStatus | object |  |  |
| status | string |  |  |
| lastFetched | int32 |  |  |

401

Unauthorized

404

Not Found

500

Internal Server Error

 Response
### Get Kiosk List

Auth BearerTokenGET /o/pmp/v1/kiosk/devicescURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

OK

| Root Type for GetKioskListRes | object |  |  |
| --- | --- | --- | --- |
| total | int32 |  |  |
| items26 fields | array[object] |  |  |
| deviceID | string |  |  |
| deviceName | string |  |  |
| modelID | string |  |  |
| HardwareVersionID | string |  |  |
| deviceType | string |  |  |
| productType | string |  |  |
| os | string |  |  |
| username | string |  |  |
| groupName | string |  |  |
| location | string |  |  |
| version | string |  |  |
| localIP | string |  |  |
| lastSeen | int32 |  |  |
| isRequired | boolean |  |  |
| healthStatus | string |  |  |
| statusMessages | array[string] |  |  |
| productStatus | string |  |  |
| scanSession | int32 |  |  |
| tags | array |  |  |
| configurationStatus | object |  |  |
| status | string |  |  |
| lastFetched | int32 |  |  |
| hardwareName | string |  |  |
| hardenedImageVersion | string |  |  |
| hardwareModel | string |  |  |
| hardwareSerialNumber | string |  |  |
| coreName | string |  |  |
| biosVersion | string |  |  |

401

Unauthorized

500

Internal Server Error

 Response
