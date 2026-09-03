<!-- source: https://www.opswat.com/docs/mdcore/configuration/external-scanners-and-post-actions -->

# External Scanners and Post Actions

Under **Library** menu it is possible to configure custom **External Scanners** and custom **Post Actions**.

For both these options we must enter two fields:

- a unique name (maximum 16 character ASCII only text)
- a full path to your executable/interpreter, that will be called by the processing node

**Note:** Since MetaDefender Core 5.2.2, External Scanner and Post Action no longer apply to all the requests. It now binds to Workflow. Therefore, after creating either External Scanner or Post Action, we need to add them into our desired Workflow Rules or Workflow Templates.

## [External Scanners](/docs/mdcore/configuration/external-scanners-and-post-actions#external-scanners)

External Scanners are handled as scan engines from product side but are not updatable through the product.

**Specification for external scanner process**

- **INPUT**

  - On standard input it gets the currently available scan result JSON without the `extracted_files` field
  - As last argument on the command line it gets the absolute path for the file to scan
  - If the command path contains space character, then must nest the command path into double quote. For example: "C:\Test Space\Hello.exe"
- **OUTPUT**

  - If everything goes well, the return value must be 0; otherwise, to indicate that the scanner has **Failed**, a value in the range of 1 to 255 on Linux and 1 to 2,147,483,647 on Windows should be returned.
  - Scan result must be put on standard output in JSON format with the following fields

    - **def_time**: the definition time of this scanner in milliseconds since epoch that will be displayed by Metadefender Core
    - **scan_result_i**: the scan verdict for the file, see the [GET Fetch Analysis Result](/docs/mdcore/metadefender-core#fileanalysisget) > scan_all_result_i
    - **threat_found**: the found threat's description if any
    - If any of the above fields is missing or invalid, the result will automatically be **Failed** for this scanner

Info

Number of External Scanners is a separately licensed feature. If you plan to use this feature please contact your OPSWAT reseller.

### [Example for a Custom Scanner](/docs/mdcore/configuration/external-scanners-and-post-actions#example-for-a-custom-scanner)

#### [Example input for a Custom Scanner](/docs/mdcore/configuration/external-scanners-and-post-actions#example-input-for-a-custom-scanner)

response.jsonCopy{
"data_id": "091c07fe6203479983682f3b4a491ee6",
"file_info": {
"display_name": "archive.zip",
"file_size": 2123967,
"file_type": "application\/zip",
"file_type_description": "ZIP compressed archive",
"md5": "ec8fa3c2897c0956f0e9ed5c092310b9",
"sha1": "0027fc18ed97063387bca9c518a02a6faba85c38",
"sha256": "4fb0083cd3cd966817c1ee4fa3f02519d05eca0b57c2bf71109d3bd69acebd41",
"upload_timestamp": "2017-04-27T13:05:20.435Z"
},
"process_info": {
"blocked_reason": "Infected",
"file_type_skipped_scan": false,
"post_processing": {
"actions_failed": "",
"actions_ran": "",
"converted_destination": "",
"converted_to": "",
"copy_move_destination": ""
},
"profile": "File scan",
"progress_percentage": 100,
"result": "Blocked",
"user_agent": "webscan"
},
"scan_results": {
"data_id": "091c07fe6203479983682f3b4a491ee6",
"progress_percentage": 100,
"scan_all_result_a": "Infected",
"scan_all_result_i": 1,
"scan_details": {
"ClamAV": {
"def_time": "2017-04-27T06:59:21.000Z",
"location": "local",
"scan_result_i": 1,
"scan_time": 51,
"threat_found": "Win.Trojan.Trojan-1082 FOUND"
}
},
"start_time": "2017-04-27T13:05:20.471Z",
"total_avs": 1,
"total_time": 1444
},
"vulnerability_info": {}
}
#### [Example valid output of a Custom Scanner](/docs/mdcore/configuration/external-scanners-and-post-actions#example-valid-output-of-a-custom-scanner)

JsonCopy{
"def_time": 1491288912392,
"scan_result_i": 0,
"threat_found": ""
}
#### [Example scan result where External Scanner found the file to be clean](/docs/mdcore/configuration/external-scanners-and-post-actions#example-scan-result-where-external-scanner-found-the-file-to-be-clean)

JsonCopy...
"scan_results": {
"data_id": "091c07fe6203479983682f3b4a491ee6",
"progress_percentage": 100,
"scan_all_result_a": "Infected",
"scan_all_result_i": 1,
"scan_details": {
"ClamAV": {
"def_time": "2017-04-27T06:59:21.000Z",
"location": "local",
"scan_result_i": 1,
"scan_time": 51,
"threat_found": "Win.Trojan.Trojan-1082 FOUND"
},
"ExtScn_01": {
"def_time": "2017-02-27T05:19:11.000Z",
"location": "local",
"scan_result_i": 0,
"scan_time": 10,
"threat_found": ""
}
},
"start_time": "2017-04-27T13:05:20.471Z",
"total_avs": 1,
"total_time": 1444
...
## [Post Actions](/docs/mdcore/configuration/external-scanners-and-post-actions#post-actions)

Post Actions (PA) run after the scan of the file for any post functionality such as copying the file etc...

**Specification for post action process**

- **INPUT**

  - On standard input it gets the currently available scan result JSON without the `extracted_files` field
  - As last argument on the command line it gets the absolute path for the file
- **OUTPUT**

  - If everything goes well, the return value must be 0; otherwise, to indicate that the action has **Failed**, a value in the range of 1 to 255 on Linux and 1 to 2,147,483,647 on Windows should be returned**.**

Adding a Post Action is the same as in case of an External Scanner. The only difference is in the result handling.

All executed Post Action's result will be on the **process_info.post_processing** object of the scan result JSON. If the return value of an action is zero it will be shown in the **actions_ran** field, if the return value of the action is non-zero then it will be listed in the **actions_failed** field.

### [Two types of Post Action](/docs/mdcore/configuration/external-scanners-and-post-actions#two-types-of-post-action)

Currently, MetaDefender Core supports two types of Post Action: Sub-process and Webhook.

- Sub-process: MetaDefender Core will call the PA as a sub-process
- Webhook: MetaDefender Core will call a `POST` request to customers' self-hosted server (customers needs to deploy and maintain this server)

### [Example of a Sub-process Post Action](/docs/mdcore/configuration/external-scanners-and-post-actions#example-of-a-sub-process-post-action)

#### [The scan result JSON if the Post Action returns 0](/docs/mdcore/configuration/external-scanners-and-post-actions#the-scan-result-json-if-the-post-action-returns-0)

The field `post_action` will look like this

JsonCopy"post_action": {
"details": [
{
"duration": 6,
"name": "Test PA",
"return_value": 0,
"verdict": 35
}
]JsonCopy{
"data_id": "cf24c1b6a14b418eae59b0cc1db1a9d9",
"dlp_info": {},
"extracted_files": {
"files_extracted_count": 2,
"total_extracted_files": 5,
"worst_data_id": "975d30e24c4243bb9d27645eb1dcd2b8"
},
"file_info": {
"display_name": "test.zip",
"file_size": 564,
"file_type": "application/zip",
"file_type_description": "ZIP Archive",
"is_skip_hash": false,
"md5": "eb63b20d6df576dd753da3312e71ae46",
"receive_data_timestamp": "2021-12-31T06:56:22.104Z",
"sha1": "77ec04c7190a7aa04a9c0666359bedddafada05e",
"sha256": "9b98873f15075fe24ccc6ddc22058d8b6415a03f1349e688adcd19192c5a834f",
"type_category": [
"A"
],
"upload_time": 2,
"upload_timestamp": "2021-12-31T06:56:22.106Z"
},
"post_action": {
"details": [
{
"duration": 6,
"name": "Test PA",
"return_value": 0,
"verdict": 35
}
],
"total_blocked": 0,
"total_executed": 1,
"total_failed": 0,
"total_post_action": 1,
"total_success": 1
},
"process_info": {
"blocked_reason": "",
"blocked_reasons": [],
"file_type_skipped_scan": false,
"post_processing": {
"actions_failed": "",
"actions_ran": "Test PA",
"converted_destination": "",
"converted_to": "",
"copy_move_destination": ""
},
"processing_time": 10,
"profile": "File process",
"progress_percentage": 100,
"queue_time": 15,
"result": "Allowed",
"user_agent": "webscan",
"username": "LOCAL/admin",
"verdicts": [
"No Threat Detected"
]
},
"scan_results": {
"current_av_result_a": "No Threat Detected",
"current_av_result_i": 0,
"data_id": "cf24c1b6a14b418eae59b0cc1db1a9d9",
"last_file_scanned": "test.zip",
"progress_percentage": 95,
"scan_all_result_a": "No Threat Detected",
"scan_all_result_i": 0,
"scan_details": {
"Avira": {
"def_time": "2020-09-13T00:00:00.000Z",
"eng_id": "avira_1_windows",
"location": "local",
"scan_result_i": 0,
"scan_time": 0,
"threat_found": "",
"wait_time": 1
}
},
"start_time": "2021-12-31T06:56:22.121Z",
"total_avs": 1,
"total_time": 10
},
"vulnerability_info": {
"verdict": 3
},
"yara_info": {}
}
#### [The scan result JSON if the Post Action returns non-zero](/docs/mdcore/configuration/external-scanners-and-post-actions#the-scan-result-json-if-the-post-action-returns-non-zero)

JsonCopy...
"post_action": {
"details": [
{
"duration": 6,
"name": "Pst_Act_01",
"return_value": 1,
"verdict": 37
}
],
"total_blocked": 0,
"total_executed": 1,
"total_failed": 1,
"total_post_action": 1,
"total_success": 0
},
"process_info": {
"blocked_reason": "Infected",
"file_type_skipped_scan": false,
"post_processing": {
"actions_failed": "Pst_Act_01 failed",
"actions_ran": "",
"converted_destination": "",
"converted_to": "",
"copy_move_destination": ""
},
"profile": "File scan",
"progress_percentage": 100,
"result": "Blocked",
"user_agent": "webscan"
},
...
### [Example of a Webhook Post Action](/docs/mdcore/configuration/external-scanners-and-post-actions#example-of-a-webhook-post-action)

When a file is done, MetaDefender Core will call a `POST` request to the Callback URL, in this case `http://mypaserver.com:8888`

MetaDefender Core will wait for a timeout, that can easily configure via each workflow settings, under the tab "Post Action"

#### [Specification for post action webhook](/docs/mdcore/configuration/external-scanners-and-post-actions#specification-for-post-action-webhook)

**INPUT**

MetaDefender Core will send this body (json) to PA webhook server

JsonCopy{
"processing_result": "current_processing_result_of_file",
"resource_path": "absolute_file_path"
}

Please note that `current_processing_result_of_file` (that webhook server received) is just the current result of the file (has not done yet), so the `processing_time` will be -1

**If you want to read the file in resource_path the webhook server need to be on the same machine of MetaDefender Core**

**OUTPUT**

If everything goes well, the return value must be 200 HTTP status code; other status code rather than 200 will be consider at Failed.

The value of `post_action.details.return_value` will be the status of return code of webhook server.

For example: MetaDefender Core call `POST`[http://mypaserver.com:8888``](http://mypaserver.com:8888%60%60) the server return 200 -> `post_action.details.return_value` = 200

Example details of a file when run with PA - webhook

JsonCopy{
"coo_info": {},
"data_id": "414c854742bf40aab6e597a655fadd3f",
"dlp_info": {},
"extraction_info": {
"is_encrypted_file": false
},
"file_info": {
"display_name": "abc.log",
"file_size": 1236169,
"file_type": "text/plain",
"file_type_description": "ASCII Text",
"file_type_id": "TXT",
"is_skip_hash": false,
"md5": "b886c7dd2b11cea526aa30669d9505a0",
"receive_data_timestamp": "2025-08-01T08:20:34.582Z",
"sha1": "ebc763f5562d9008ba424aa4b51a0249b3b49ef9",
"sha256": "9478e713eda06b654084f846735d7f6486fb737afa2d46a49b438efdbaf4c78a",
"sha512": "",
"signer_infos": [],
"type_category": [
"T"
],
"upload_time": 23,
"upload_timestamp": "2025-08-01T08:20:34.605Z"
},
"filetype_info": {
"file_info": {
"description": "ASCII Text",
"encrypted": false,
"extensions": "txt,dat,prn,css",
"groupID": "T",
"groupIDs": [
"T"
],
"type": "text/plain",
"typeID": "TXT",
"type_ids": [
"TXT",
"LOG"
]
},
"is_file_type_mismatch": false,
"result_template_hash": "126b24af8d08e8199d478b03bfaf629bc0756d87c20fb46ff5c6b49b9a843303"
},
"insightsti_info": {},
"opswatfilescan_info": {},
"post_action": {
"details": [
{
"duration": 824,
"name": "PA-webhook",
"return_value": 200,
"verdict": 35
}
],
"total_blocked": 0,
"total_executed": 1,
"total_failed": 0,
"total_post_action": 1,
"total_success": 1
},
"process_info": {
"archive_handling_details": {},
"blocked_reason": "Not Scanned",
"blocked_reasons": [
"Not Scanned"
],
"file_type_skipped_scan": false,
"hash_time": 5,
"post_processing": {
"actions_failed": "",
"actions_ran": "PA-webhook",
"converted_destination": "",
"converted_to": "",
"copy_move_destination": ""
},
"processing_time": 893,
"processing_time_details": {
"filetype_time": 54,
"others_time": 13,
"post_action_time": 826
},
"profile": "File process",
"progress_percentage": 100,
"queue_time": 33,
"result": "Blocked",
"user_agent": "webscan",
"username": "LOCAL/admin",
"verdicts": [
"Not Scanned"
]
},
"reputation_info": {},
"sbom_info": {},
"scan_results": {
"current_av_result_a": "Not Scanned",
"current_av_result_i": 10,
"data_id": "414c854742bf40aab6e597a655fadd3f",
"progress_percentage": 100,
"scan_all_result_a": "Not Scanned",
"scan_all_result_i": 10,
"scan_details": {},
"start_time": "2025-08-01T08:20:34.643Z",
"total_avs": 0,
"total_time": 893
},
"vulnerability_info": {
"verdict": 3
},
"yara_info": {}
}
