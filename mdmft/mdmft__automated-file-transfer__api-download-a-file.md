<!-- source: https://www.opswat.com/docs/mdmft/automated-file-transfer/api-download-a-file -->

# API - Download a file

Summarize Page    Connect to Cursor Connect to VS Code

So far, you've learned how to authenticate and list files within a specific folder. Now, let's take it a step further and explore broader file management capabilities. In this section, you'll learn how to:

- **Check the status of a file**
- **Download a file**
- **List all accessible files**

List files

First let list files. We already discussed listing files in single folder. Now we'll list files in general. for that we can use **GET** `/vault_rest/files/{type}/{start}/{count}` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getenumerate-files).

- `type`: Accepts either "my" or "all".

  - `my` returns only your own files.
  - all includes all file you can access that can include your files as well as any files shared with you...
- `start` and `count`: These parameters allow you to paginate results by specifying where to begin and how many files to retrieve.

Lets see an example

PowershellResponseCopy# Get your files
try {
$response = Invoke-RestMethod -Uri "$baseUrl/files/my/0/20" -Headers $headers -Method Get
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Output $response.items | Select-Object file_id, name, size, creation_date | Format-Table -AutoSize
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"filter_count": 4,
"items": [
{
"administrator_approval_state": "ApprovalDisabled",
"availability_state": "Available",
"availability_state_key": "FILE_STATE_SANITIZED",
"can_access_scan_results": true,
"can_be_archived": true,
"can_be_deleted": true,
"can_be_downloaded": true,
"can_be_moved": true,
"can_be_permanently_deleted": true,
"can_be_previewed": true,
"can_be_rescanned": true,
"can_update_file_password": true,
"cdr_result_key": "Sanitized",
"current_approval_count": 0,
"dlp_result_key": "DLP_SENSITIVE_DATA_NOT_DETECTED",
"duration": 920,
"engines_verdict": {
"infected_engines": 0,
"total_engines": 17
},
"file_id": "7963c14842274e519d0fae185bf4aee7",
"file_type": "OpenDocument Sheet",
"is_blocked_by_core": false,
"is_converted": true,
"is_dlp_processed": false,
"is_filescanned": false,
"is_locked": false,
"is_sanitized": true,
"md5": "fd32786eb1865218da9b726c703c0841",
"name": "Metadefender_MFT_a9d1a45fe6e0454da52207de71e6ab7a.ods",
"processing_state": "Available",
"processing_state_key": "PROCESSING_STATE_Available",
"required_approval_count": 2,
"sandbox_result_key": "FILE_INFO_SANDBOX_NOT_CONFIGURED",
"scan_result": {
"actions_failed": "",
"blocked_reason": "",
"workflow_result": "Allowed"
},
"scan_result_key": "METASCAN_RESULT_CORE_THREAT_NOT_FOUND",
"sha1": "ddc07013e8bf3790312f5313674943912396a47e",
"sha256": "ccde3c2e62245f9c6e998bb19a57c520b4b7d7572119219fd8f0979399ee6765",
"supervisor_approval_state": "ApprovalDisabled",
"supervisor_approval_state_key": "SUPERVISOR_APPROVAL_STATE_DISABLED",
"supervisor_reason": "",
"workflow": "MetaDefender Vault",
"can_retry_processing": false,
"creation_date": "2024-01-10T11:41:57.0000000",
"expires": "2025-01-09T11:41:57.0000000",
"is_false_positive": false,
"last_download_date": "0001-01-01T00:00:00.0000000",
"owner": "admin admin",
"owner_id": 1,
"size": 3956,
"can_add_supervisor_comment": false,
"can_be_approved": false,
"can_be_denied_access": false,
"can_be_overridden": false,
"can_be_released": false,
"different_approval_step": true,
"supervisor_step_for_file": 0
},
{
"administrator_approval_state": "ApprovalDisabled",
"availability_state": "Available",
"availability_state_key": "FILE_STATE_SANITIZED",
"can_access_scan_results": true,
"can_be_archived": true,
"can_be_deleted": true,
"can_be_downloaded": true,
"can_be_moved": true,
"can_be_permanently_deleted": true,
"can_be_previewed": true,
"can_be_rescanned": true,
"can_update_file_password": true,
"cdr_result_key": "Sanitized",
"current_approval_count": 0,
"dlp_result_key": "DLP_SENSITIVE_DATA_NOT_DETECTED",
"duration": 909,
"engines_verdict": {
"infected_engines": 0,
"total_engines": 17
},
"file_id": "4027075bdfde40a3a8d550383f3ec0cf",
"file_type": "Microsoft Excel Workbook",
"is_blocked_by_core": false,
"is_converted": true,
"is_dlp_processed": false,
"is_filescanned": false,
"is_locked": false,
"is_sanitized": true,
"md5": "23bc22adc528272834f8fedc6350ce70",
"name": "Metadefender_MFT_341bfb589031405595ff28bfd5bca6f8.xlsx",
"processing_state": "Available",
"processing_state_key": "PROCESSING_STATE_Available",
"required_approval_count": 2,
"sandbox_result_key": "FILE_INFO_SANDBOX_NOT_CONFIGURED",
"scan_result": {
"actions_failed": "",
"blocked_reason": "",
"workflow_result": "Allowed"
},
"scan_result_key": "METASCAN_RESULT_CORE_THREAT_NOT_FOUND",
"sha1": "0ec16b19984b27d2917105adb3a1849365b11e87",
"sha256": "87ffe258e6a4fef32ad3d40378397dac16d6ff84e0f689cf9fe971fb52b2cd84",
"supervisor_approval_state": "ApprovalDisabled",
"supervisor_approval_state_key": "SUPERVISOR_APPROVAL_STATE_DISABLED",
"supervisor_reason": "",
"workflow": "MetaDefender Vault",
"can_retry_processing": false,
"creation_date": "2024-01-10T11:39:04.0000000",
"expires": "2025-01-09T11:39:05.0000000",
"is_false_positive": false,
"last_download_date": "0001-01-01T00:00:00.0000000",
"owner": "admin admin",
"owner_id": 1,
"size": 11007,
"can_add_supervisor_comment": false,
"can_be_approved": false,
"can_be_denied_access": false,
"can_be_overridden": false,
"can_be_released": false,
"different_approval_step": true,
"supervisor_step_for_file": 0
},
{
"administrator_approval_state": "ApprovalDisabled",
"availability_state": "Available",
"availability_state_key": "FILE_STATE_SANITIZED",
"can_access_scan_results": true,
"can_be_archived": true,
"can_be_deleted": true,
"can_be_downloaded": true,
"can_be_moved": true,
"can_be_permanently_deleted": true,
"can_be_previewed": true,
"can_be_rescanned": true,
"can_update_file_password": true,
"cdr_result_key": "Sanitized",
"current_approval_count": 0,
"dlp_result_key": "DLP_SENSITIVE_DATA_NOT_DETECTED",
"duration": 1848,
"engines_verdict": {
"infected_engines": 0,
"total_engines": 17
},
"file_id": "b7b95cc3ccfb4e25932fb322498b98d8",
"file_type": "Microsoft Excel 97-2003 Workbook",
"is_blocked_by_core": false,
"is_converted": true,
"is_dlp_processed": false,
"is_filescanned": false,
"is_locked": false,
"is_sanitized": true,
"md5": "ed33a9ce2ff0929aa0a3473e12be9560",
"name": "Metadefender_MFT_bcc44a32f2af4f829372cf61e40a693d.xls",
"processing_state": "Available",
"processing_state_key": "PROCESSING_STATE_Available",
"required_approval_count": 2,
"sandbox_result_key": "FILE_INFO_SANDBOX_NOT_CONFIGURED",
"scan_result": {
"actions_failed": "",
"blocked_reason": "",
"workflow_result": "Allowed"
},
"scan_result_key": "METASCAN_RESULT_CORE_THREAT_NOT_FOUND",
"sha1": "60e60c0f7f10f85dc2eb94762be8915e03cf812c",
"sha256": "e4e27d27f8e905d0a39acc2fc142950906cfc60a02b29ad29433f089617dce89",
"supervisor_approval_state": "ApprovalDisabled",
"supervisor_approval_state_key": "SUPERVISOR_APPROVAL_STATE_DISABLED",
"supervisor_reason": "",
"workflow": "MetaDefender Vault",
"can_retry_processing": false,
"creation_date": "2024-01-10T11:39:04.0000000",
"expires": "2025-01-09T11:39:05.0000000",
"is_false_positive": false,
"last_download_date": "0001-01-01T00:00:00.0000000",
"owner": "admin admin",
"owner_id": 1,
"size": 15872,
"can_add_supervisor_comment": false,
"can_be_approved": false,
"can_be_denied_access": false,
"can_be_overridden": false,
"can_be_released": false,
"different_approval_step": true,
"supervisor_step_for_file": 0
},
{
"administrator_approval_state": "ApprovalDisabled",
"availability_state": "Available",
"availability_state_key": "FILE_STATE_SANITIZED",
"can_access_scan_results": true,
"can_be_archived": true,
"can_be_deleted": true,
"can_be_downloaded": true,
"can_be_moved": true,
"can_be_permanently_deleted": true,
"can_be_previewed": false,
"can_be_rescanned": true,
"can_update_file_password": true,
"cdr_result_key": "Sanitized",
"current_approval_count": 0,
"dlp_result_key": "DLP_SENSITIVE_DATA_NOT_DETECTED",
"duration": 523,
"engines_verdict": {
"infected_engines": 0,
"total_engines": 17
},
"file_id": "4e17f31e667843689ca41e9095cc2d26",
"file_type": "Comma-Separated Values",
"is_blocked_by_core": false,
"is_converted": true,
"is_dlp_processed": false,
"is_filescanned": false,
"is_locked": false,
"is_sanitized": true,
"md5": "a0a01c2d1295e5325e47d51f5ab65595",
"name": "Metadefender_MFT_eb76c7b792da4ea09ea81e32a27ad8ca.csv",
"processing_state": "Available",
"processing_state_key": "PROCESSING_STATE_Available",
"required_approval_count": 2,
"sandbox_result_key": "FILE_INFO_SANDBOX_NOT_CONFIGURED",
"scan_result": {
"actions_failed": "",
"blocked_reason": "",
"workflow_result": "Allowed"
},
"scan_result_key": "METASCAN_RESULT_CORE_THREAT_NOT_FOUND",
"sha1": "eb4011791fee8f86dc7585c0b20184140c44a35b",
"sha256": "11a401aa4be41e88a81e1176ad3b28bd8af73fc2aab1499df3dbd3e2639dcbc8",
"supervisor_approval_state": "ApprovalDisabled",
"supervisor_approval_state_key": "SUPERVISOR_APPROVAL_STATE_DISABLED",
"supervisor_reason": "",
"workflow": "MetaDefender Vault",
"can_retry_processing": false,
"creation_date": "2024-01-10T11:39:04.0000000",
"expires": "2025-01-09T11:39:05.0000000",
"is_false_positive": false,
"last_download_date": "0001-01-01T00:00:00.0000000",
"owner": "admin admin",
"owner_id": 1,
"size": 905,
"can_add_supervisor_comment": false,
"can_be_approved": false,
"can_be_denied_access": false,
"can_be_overridden": false,
"can_be_released": false,
"different_approval_step": true,
"supervisor_step_for_file": 0
}
],
"total_count": 4
}
## [Now lets look at one single file](/docs/mdmft/automated-file-transfer/api-download-a-file#now-lets-look-at-one-single-file)

### [File status](/docs/mdmft/automated-file-transfer/api-download-a-file#file-status)

We can get status of single file with **GET** `/vault_rest/file/status/{file_id}` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getquery-file-status). File status will have data on access rights, file type and security scanning.

PowershellResponseCopy# Get file status
try {
$response = Invoke-RestMethod -Uri "$baseUrl/file/status/e3de1b4640cb40af8d386f81ad3f2d79" -Headers $headers -Method Get
Write-Host ( $response | ConvertTo-Json | Out-String)
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null,
"administrator_approval_state": "ApprovalDisabled",
"availability_state": "Available",
"availability_state_key": "FILE_STATE_AVAILABLE",
"can_access_file_approval_history": false,
"can_access_scan_results": true,
"can_be_archived": true,
"can_be_deleted": true,
"can_be_downloaded": true,
"can_be_moved": true,
"can_be_permanently_deleted": true,
"can_be_previewed": false,
"can_be_renamed": true,
"can_be_rescanned": false,
"can_be_synced_to_mft": false,
"can_edit_file_tags": true,
"can_update_file_password": true,
"can_update_sharing": true,
"cdr_result_key": "Sanitization not configured",
"current_approval_count": 0,
"dlp_result_key": "FILE_INFO_PROACTIVE_DLP_NOT_CONFIGURED",
"duration": null,
"engines_verdict": {
"infected_engines": 0,
"total_engines": 0
},
"file_id": "e3de1b4640cb40af8d386f81ad3f2d79",
"file_type": null,
"is_blocked_by_core": false,
"is_converted": false,
"is_dlp_processed": false,
"is_filescanned": false,
"is_locked": false,
"is_sanitized": false,
"is_shared": false,
"md5": null,
"name": "image.jpg",
"processing_state": "Available",
"processing_state_key": "PROCESSING_STATE_Available",
"required_approval_count": 0,
"sandbox_result_key": "FILE_INFO_SANDBOX_VERDICT_UNKNOWN",
"sandboxscan_info": {
"blocked": false,
"confidence": 0,
"threat_level": 0,
"verdict": null
},
"scan_result": {
"actions_failed": null,
"blocked_reason": null,
"workflow_result": null
},
"scan_result_key": "METASCAN_RESULT_CORE_DISABLED",
"sha1": null,
"sha256": null,
"share_role": "",
"supervisor_approval_state": "ApprovalDisabled",
"supervisor_approval_state_key": "SUPERVISOR_APPROVAL_FEATURE_DISABLED",
"supervisor_reason": "",
"unlock_eta": null,
"workflow": null,
"first_upload_time": "2025-07-29T13:36:18.0000000",
"folder_id": "67cd5a48613a4fbc9423e7ead182a5db",
"is_file_owned": true,
"path": "some files",
"size": 203970
}
### [Download file](/docs/mdmft/automated-file-transfer/api-download-a-file#download-file)

Now that we listed files, checked file status, lets downloaded it. For that well use **GET** `/vault_rest/file/{file_id}` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getdownload-a-file). In our example we had file_id and from that we got file name. You can get file name and id by listing your files.

PowershellCopy# Download file
# First we need file_name and name
$file_id = "e3de1b4640cb40af8d386f81ad3f2d79"
# Step 1: Get file name
try {
$file = Invoke-RestMethod -Uri "$baseUrl/file/status/$file_id" -Headers $headers -Method Get
Write-Host ( $file | ConvertTo-Json | Out-String)
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
# Selecting detination where to save our file.
$outputFile = "C:\Users\user\Documents\Test\$($file.name)"
# Step 2: Get ID of root folder
try {
# Downloading file
Invoke-RestMethod -Uri "$baseUrl/file/$($file.file_id)" -Headers $headers -Method Get -OutFile $outputFile
# Testing success
if (Test-Path $outputFile) {
Write-Host "File $outputFile downloaded successfully."
} else {
Write-Host "File $outputFile download failed."
}
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
