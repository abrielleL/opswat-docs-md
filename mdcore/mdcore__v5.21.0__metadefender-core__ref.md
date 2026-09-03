<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/metadefender-core/ref -->

## Developer Guide

---

This is the API documentation for *MetaDefender Core Public API*. If you
would like to evaluate or have any questions about this documentation,
please contact us via our [Contact Us](https://www.opswat.com/contact) form.

---

## How to Interact with MetaDefender Core using REST

Beginning with MetaDefender Core 4.x, OPSWAT recommends using the JSON-based
REST API. The available methods are documented below.

> ***Note**:* MetaDefender API doesn't support chunk upload, however is
> recommended to stream the files to MetaDefender Core as part of the upload
> process.

---

## File Analysis Process

MetaDefender's main functionality is to analyze large volumes with a high throughput. Depending on the configuration and licensed technologies, the analysis times can vary.
Below is a brief description of the API integration flow:

1. Upload a file for analysis (`POST /file`), which returns the `data_id` or `batch_id`: [File Analysis](/docs/mdcore/metadefender-core/ref#fileanalysispost)).

   > ***Note**:* The performance depends on:
   >
   > - number of engines
   > - type of file to be scanned
   > - MetaDefender Core's hardware

   **Batch Upload with multipart/form-data**:

   - When the request uses `Content-Type: multipart/form-data`, MetaDefender Core treats the entire submission as a batch.
   - A new batch is automatically created for this media type.
   - Each part in the request body is processed as an individual file within the batch.
   - The API returns a `batch_id` instead of a `data_id`.
   - All individual file scans are linked to the created batch.
2. You have 2 ways to retrieve the analysis report:

   - **Polling**: Fetch the result with previously received data_id or batch_id (`GET /file/{data_id}` or `GET /file/{batch_id}` resource) until scan result belonging to data_id/batch_id doesn't reach the 100 percent progress_percentage: ([Fetch analysis result](/docs/mdcore/metadefender-core/ref#fileanalysisget))
   > ***Note**:* Too many data_id/batch_id requests can reduce performance. It is enough to just check every few hundred milliseconds.

   - **Callbackurl**: Specify a callbackurl that will be called once the analysis is complete.
3. Retrieve the analysis results anytime after the analysis is completed with hash for files (md5, sha1, sha256, sha512) by calling [Fetch analysis result by hash](/docs/mdcore/metadefender-core/ref#hashget).

   - The hash can be found in the scan results
4. Retrieve processed file (sanitized, redacted, watermarked, etc.) after the analysis is complete.

   > ***Note**:* Based on the configured retention policy, the files might be available for retrieval at a later time.

---

OPSWAT provides some sample codes on [GitHub](https://github.com/OPSWAT) to
make it easier to understand how the MetaDefender REST API works.

Serverhttp://localhost:8008Server Variables## AuthenticationapiKey apikey

Generated `session_id` from [Login](/docs/mdcore/metadefender-core/ref#userlogin) call can be used as an `apikey` for API calls that require authentication.

Fields

| Key | In |
| --- | --- |
| apikey | Header |  |

## Auth

### Authentication APIs

User authentication is done via username & password.
Additional integrations are available within the product:

- **LDAP** integration
- **Active Directory** integration
- **SAML** integration (starting with v4.18.0)

Endpoints[POST/login](/docs/mdcore/v5.21.0/metadefender-core#userlogin) [POST/logout](/docs/mdcore/v5.21.0/metadefender-core#userlogout)
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

Unexpected event on server

 Response
### Logout

Destroy session for not using protected REST APIs.

Auth NoneHeaders

| apikey | string | Generated `session_id` from [Login](/docs/mdcore/metadefender-core/ref#userlogin) call can be used as an `apikey` for API calls that require authentication. |  |
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

Unexpected event on server

 Response
## User Management

### User management APIs

The APIs for manage users and user directories.

Endpoints[POST/admin/user](/docs/mdcore/v5.21.0/metadefender-core#usercreate) [GET/admin/user](/docs/mdcore/v5.21.0/metadefender-core#userlist) [DELETE/admin/user/{user_id}](/docs/mdcore/v5.21.0/metadefender-core#userdelete) [PUT/admin/user/{user_id}/apikey](/docs/mdcore/v5.21.0/metadefender-core#changeuserapikey) [GET/admin/exportusers](/docs/mdcore/v5.21.0/metadefender-core#exportusers) [PUT/admin/userdirectory/changepassword](/docs/mdcore/v5.21.0/metadefender-core#userdirectorychangepass) [POST/user/changepassword](/docs/mdcore/v5.21.0/metadefender-core#userchangepass) Show 
## Analysis

### File analysis APIs

Submit each file to MetaDefender Core individually or group them in batches. Each file submission will return a `data_id` which will be the unique identifier used to retrieve the analysis results.
When `Content-Type: multipart/form-data` is used, the entire request is treated as a batch. A `batch_id` is created automatically, and each part in the multipart body is processed as an individual file within that batch.
**Important**: Even though one file is being submitted, if MetaDefender Core is configured to extract the files, all compound file types (archives, Office documents, etc.) will be extracted and each file within will be analyzed as a separate entry.

- This means that if you submit an archive with 100 files in it, MetaDefender Core will process 101 files: original file as it is and each of the 100 child files
  - Note that by opening the files, detection ratio can increase even by 30%.

> ***Note**:* MetaDefender API doesn't support chunk upload. You shouldn't load the file in memory, is recommended to stream the files to MetaDefender Core as part of the upload process.

Endpoints[POST/file](/docs/mdcore/v5.21.0/metadefender-core#fileanalysispost) [POST/file/sync](/docs/mdcore/v5.21.0/metadefender-core#fileanalysissyncpost) [GET/file/last](/docs/mdcore/v5.21.0/metadefender-core#getlastprocessedfile) [GET/file/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#fileanalysisget) [GET/file/{data_id}/blocked-leaves](/docs/mdcore/v5.21.0/metadefender-core#retrieveblockedleaffile) [GET/file/{data_id}/extraction-errors](/docs/mdcore/v5.21.0/metadefender-core#retrieveextractionerrors) [GET/archive/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#fileanalysisgetallchildfiles) [GET/hash/{md5|sha1|sha256|sha512}](/docs/mdcore/v5.21.0/metadefender-core#hashget) [GET/hash/{md5|sha1|sha256|sha512}/blocked-leaves](/docs/mdcore/v5.21.0/metadefender-core#retrieveblockedleaffilebyhash) [GET/file/webhook/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#webhookstatus) [GET/file/rules](/docs/mdcore/v5.21.0/metadefender-core#analysisrules) [HEAD/file/converted/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#headsanitizedfile) [GET/file/converted/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#sanitizedfile) [GET/file/download/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#downloadfile) [GET/file/{data_id}/export](/docs/mdcore/v5.21.0/metadefender-core#resultexportedfile) [GET/quarantine/{sha256}/download](/docs/mdcore/v5.21.0/metadefender-core#downloadquarantinedfile) [GET/file/{dataid}/sbom/report](/docs/mdcore/v5.21.0/metadefender-core#downloadsbomreport) [POST/file/{data_id}/cancel](/docs/mdcore/v5.21.0/metadefender-core#fileanalysiscancel) Show 
## Batch

Group the analysis requests in batches.

Endpoints[POST/file/batch](/docs/mdcore/v5.21.0/metadefender-core#batchcreate) [POST/file/batch/{batchId}/close](/docs/mdcore/v5.21.0/metadefender-core#batchclose) [POST/file/batch/{batchId}/close/callback](/docs/mdcore/v5.21.0/metadefender-core#batchclosecallback) [GET/file/batch/{batchId}](/docs/mdcore/v5.21.0/metadefender-core#batchstatus) [GET/file/batch/{batchId}/certificate](/docs/mdcore/v5.21.0/metadefender-core#batchsignedresult) [POST/file/batch/{batchId}/cancel](/docs/mdcore/v5.21.0/metadefender-core#batchcancel) Show 
## Multipart

Upload a file for scan by multiple parts.

Endpoints[POST/file/multipart](/docs/mdcore/v5.21.0/metadefender-core#createmultipartuploadpost) [POST/file/multipart/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#uploadpartpost) [GET/file/multipart/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#uploadpartget) [DELETE/file/multipart/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#uploadpartdelete) Show 
## Splitarchive

Processes a split archive uploaded in multiple parts. Only the extracted files from the reassembled split archive are processed; the combined archive file itself is not supported. Therefore, Quarantine and PostAction do not apply.

Endpoints[POST/file/splitarchive](/docs/mdcore/v5.21.0/metadefender-core#createsplitarchiveuploadpost) [POST/file/splitarchive/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#uploadsplitarchivepartpost) [GET/file/splitarchive/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#getsplitarchivestatusget) [DELETE/file/splitarchive/{data_id}](/docs/mdcore/v5.21.0/metadefender-core#abortsplitarchiveuploaddelete) Show 
## Admin

Admin specific API requests.

Endpoints[GET/admin/export](/docs/mdcore/v5.21.0/metadefender-core#adminexport) [GET/admin/export/v2](/docs/mdcore/v5.21.0/metadefender-core#adminexportv2) [POST/admin/import](/docs/mdcore/v5.21.0/metadefender-core#adminimport) [POST/admin/import/v2](/docs/mdcore/v5.21.0/metadefender-core#adminimportv2) [POST/admin/role](/docs/mdcore/v5.21.0/metadefender-core#rolecreate) [GET/admin/role](/docs/mdcore/v5.21.0/metadefender-core#rolelist) [DELETE/admin/role/{role_id}](/docs/mdcore/v5.21.0/metadefender-core#roledelete) [GET/admin/userdirectory](/docs/mdcore/v5.21.0/metadefender-core#userdirectorylist) [GET/admin/license/backup](/docs/mdcore/v5.21.0/metadefender-core#getlicensebackup) [POST/admin/license/backup](/docs/mdcore/v5.21.0/metadefender-core#postlicensebackup) [DELETE/admin/license/backup](/docs/mdcore/v5.21.0/metadefender-core#removebackupinstance) [POST/admin/license/backup/nomination](/docs/mdcore/v5.21.0/metadefender-core#licensebackupnomination) Show 
## License

Activate the product or get licensing information. Will require admin apikey.

Endpoints[POST/admin/license/activation](/docs/mdcore/v5.21.0/metadefender-core#licenseactivation) [POST/admin/license](/docs/mdcore/v5.21.0/metadefender-core#licenseupload) [GET/admin/license](/docs/mdcore/v5.21.0/metadefender-core#licenseget) [POST/admin/license/deactivation](/docs/mdcore/v5.21.0/metadefender-core#licensedeactivation) Show 
## Config

Configure the product through APIs (especially the Settings). Will require admin apikey.

Endpoints[PUT/admin/config/auditlog](/docs/mdcore/v5.21.0/metadefender-core#configauditlog) [PUT/admin/config/quarantine](/docs/mdcore/v5.21.0/metadefender-core#configquarantine) [PUT/admin/config/sanitize](/docs/mdcore/v5.21.0/metadefender-core#configsanitizedrepo) [PUT/admin/config/scanhistory](/docs/mdcore/v5.21.0/metadefender-core#configscanhistory) [PUT/admin/config/session](/docs/mdcore/v5.21.0/metadefender-core#configsession) [PUT/admin/config/update](/docs/mdcore/v5.21.0/metadefender-core#configupdate) [GET/config/skip/{skip_type}/template](/docs/mdcore/v5.21.0/metadefender-core#configgetskiphashtemplate) [POST/admin/config/skip/{skip_type}](/docs/mdcore/v5.21.0/metadefender-core#configpostskiphashcsv) [POST/admin/config/skip](/docs/mdcore/v5.21.0/metadefender-core#configpostskiphash) [GET/admin/config/skip](/docs/mdcore/v5.21.0/metadefender-core#configgetskiphash) [PUT/admin/config/skip](/docs/mdcore/v5.21.0/metadefender-core#putmodify-skip-by-hash-list) [DELETE/admin/config/skip](/docs/mdcore/v5.21.0/metadefender-core#configdeleteskiphash) [GET/admin/config/webhook](/docs/mdcore/v5.21.0/metadefender-core#configwebhook) [PUT/admin/config/webhook](/docs/mdcore/v5.21.0/metadefender-core#configupdatewebhook) [GET/admin/config/proxy](/docs/mdcore/v5.21.0/metadefender-core#configgetproxy) [PUT/admin/config/proxy](/docs/mdcore/v5.21.0/metadefender-core#configupdateproxy) [POST/admin/config/proxy/testconnection](/docs/mdcore/v5.21.0/metadefender-core#configpostproxytestconnection) [GET/admin/config/file/sync](/docs/mdcore/v5.21.0/metadefender-core#configgetsyncscantimeout) [PUT/admin/config/file/sync](/docs/mdcore/v5.21.0/metadefender-core#configupdatesyncscantimeout) [GET/admin/config/sessioncookie](/docs/mdcore/v5.21.0/metadefender-core#configgetsessioncookie) [PUT/admin/config/sessioncookie](/docs/mdcore/v5.21.0/metadefender-core#configputsessioncookie) [GET/admin/config/cacheuser](/docs/mdcore/v5.21.0/metadefender-core#configgetcacheuser) [PUT/admin/config/cacheuser](/docs/mdcore/v5.21.0/metadefender-core#configputcacheuser) [GET/admin/config/customresponseheader](/docs/mdcore/v5.21.0/metadefender-core#configgetcustomresponseheader) [PUT/admin/config/customresponseheader](/docs/mdcore/v5.21.0/metadefender-core#configputcustomresponseheader) [GET/admin/config/healthcheck](/docs/mdcore/v5.21.0/metadefender-core#configgethealthcheck) [POST/admin/config/healthcheck](/docs/mdcore/v5.21.0/metadefender-core#configupdatehealthcheck) [GET/admin/config/logger/logfile](/docs/mdcore/v5.21.0/metadefender-core#getlogfileconfig) [PUT/admin/config/logger/logfile](/docs/mdcore/v5.21.0/metadefender-core#putlogfileconfig) [GET/admin/config/logger/syslog](/docs/mdcore/v5.21.0/metadefender-core#getsyslogconfig) [POST/admin/config/logger/syslog](/docs/mdcore/v5.21.0/metadefender-core#postsyslogconfig) [PUT/admin/config/logger/syslog](/docs/mdcore/v5.21.0/metadefender-core#putsyslogconfig) [DELETE/admin/config/logger/syslog](/docs/mdcore/v5.21.0/metadefender-core#removesyslogconfig) [GET/admin/config/logger/general](/docs/mdcore/v5.21.0/metadefender-core#getgeneralloggerconfig) [PUT/admin/config/logger/general](/docs/mdcore/v5.21.0/metadefender-core#putgeneralloggerconfig) Show 
## Yara

YARA engine configuration and source management APIs.

Endpoints[GET/admin/config/yara/sources](/docs/mdcore/v5.21.0/metadefender-core#yarasourcesget) [PUT/admin/config/yara/sources](/docs/mdcore/v5.21.0/metadefender-core#yarasourcesput) [GET/yara/package](/docs/mdcore/v5.21.0/metadefender-core#yarapackagestatus) [POST/yara/generate](/docs/mdcore/v5.21.0/metadefender-core#yarapackagegenerate) Show 
## Engines

Enable/disable or pin/unpin the engines through API.

Endpoints[POST/admin/engine/{engineId}/pin](/docs/mdcore/v5.21.0/metadefender-core#enginepin) [POST/admin/engine/{engineId}/unpin](/docs/mdcore/v5.21.0/metadefender-core#engineunpin) [POST/admin/engine/{engineId}/enable](/docs/mdcore/v5.21.0/metadefender-core#engineenable) [POST/admin/engine/{engineId}/disable](/docs/mdcore/v5.21.0/metadefender-core#enginedisable) [GET/admin/engine/{engineId}/config](/docs/mdcore/v5.21.0/metadefender-core#engineconfigget) [PUT/admin/engine/{engineId}/config](/docs/mdcore/v5.21.0/metadefender-core#engineconfigput) [DELETE/admin/engine/{engineId}](/docs/mdcore/v5.21.0/metadefender-core#deletedelete-an-engine-or-database-package) Show 
## Stats

Health check and statistics about MetaDefender Core usage.

Endpoints[GET/admin/stat/server](/docs/mdcore/v5.21.0/metadefender-core#getserverstats) [GET/version](/docs/mdcore/v5.21.0/metadefender-core#productversion) [GET/stat/engines](/docs/mdcore/v5.21.0/metadefender-core#enginesstatus) [GET/stat/nodes](/docs/mdcore/v5.21.0/metadefender-core#nodesstatus) [GET/stat/activeperformance](/docs/mdcore/v5.21.0/metadefender-core#activeperformance) [GET/stat/user/totalprocess](/docs/mdcore/v5.21.0/metadefender-core#getusertotalprocess) [GET/readyz](/docs/mdcore/v5.21.0/metadefender-core#healthcheck) Show 
## Management

Endpoints[POST/admin/update/folder](/docs/mdcore/v5.21.0/metadefender-core#postforce-update-folder-trigger) [PUT/pincode](/docs/mdcore/v5.21.0/metadefender-core#updatepincode) [HEAD/pincode](/docs/mdcore/v5.21.0/metadefender-core#checkpincodeexists) [POST/admin/pincode/validate](/docs/mdcore/v5.21.0/metadefender-core#validatepincode) Show 
## Database

Endpoints[POST/dbconfig/changepasswdpgconnection](/docs/mdcore/v5.21.0/metadefender-core#dbconfigchangepgpassword) Show
