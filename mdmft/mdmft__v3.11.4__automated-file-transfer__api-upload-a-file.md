<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file -->

# API - Upload a file

Summarize Page    Connect to Cursor Connect to VS Code

In this chapter we'll learn how to upload file. Uploading file using API is multi-step process.

1. Initiate a group transfer
2. Initiate a file transfer
3. Upload a file
4. Complete a file transfer
5. Complete a group transfer

## [Initiate group transfer](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#initiate-group-transfer)

You can upload multiple files in single group upload. To initiate group transfer use **GET**`/vault_rest/transfer```[endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getinitialize-group-transfer). Here is an example:

PowershellResponseCopy# Initiate group transfer
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer" -Headers $headers -Method Get
#Write-Host ( $file | ConvertTo-Json | Out-String)
Write-Host "Group ID: $($response.group_id)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"group_id": "2b6dea8f2fed49f5a5bb61c766394f45",
"owner": {
"email": "testuser@email.com",
"first_name": "Levi",
"is_impersonated": false,
"last_name": "Kim",
"username": "Levi"
},
"shared_with": [
{
"email": "testuser@email.com",
"id": 1,
"username": "Levi"
}
]
}
## [Initiate file transfer](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#initiate-file-transfer)

Now we'll create empty file on server where we'll stream data from our local file. for that we use **GET** `/vault_rest``/transfer_file` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getinitialize-file-transfer). We need to send some essential data with headers.

- `transfer_method` – Method used for transferring the file as Binary data either Stream or Chunk.
- `group_id` – The transfer **group ID.**
- `file_size` – Size of the file in **bytes.**
- `file_name` – Name of the file to be uploaded. (Example: Testing image 2.png → Testing image 2)

Warning

For larger files, this method may cause issues due to size limitations. In such cases, you should upload the file in chunks (typically 10MB per chunk). To enable chunked upload, make sure to include the **chunk_offset** header in your request.

PowershellResponseCopy# Initiate file transfer
$upload_file = "C:\Users\user\Documents\Test\image.jpg"
# check if local file exists
if (Test-Path $upload_file) {
# Get file size
$file_size = (Get-Item $upload_file).Length
# Get file name
$file_name = Split-Path -Path $upload_file -Leaf
} else {
Write-Host "File does not exist."
}
# Prepare headers
$headers_ft = @{
Authorization = "Bearer $token"
transfer_method = "Stream"
group_id = $group_id
file_name = $file_name
file_size = $file_size
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer_file" -Headers $headers_ft -Method Get
#Write-Host ( $file | ConvertTo-Json | Out-String)
$file_id = $response.file_id
Write-Host "File ID: $($response.file_id)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": "File record created",
"file_id": "17bc10b5c0dd438aa263ad0c9042c30e"
}
## [Upload a file](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#upload-a-file)

For uploading file we'll use **PATCH** `/vault_rest/transfer_file` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#patchupload-file-chunk). For this transfer we need to sed some headers:

- `group_id` – The group transfer ID received from the **Initialize Group Transfer** step
- `file_id` – The file ID received from the **Initialize File Transfer** step

PowershellResponseCopy#Upload files
$upload_file = "C:\Users\user\Documents\Test\image.jpg"
# Prepare headers
$headers_ft = @{
Authorization = "Bearer $token"
file_id = $file_id
group_id = $group_id
}
try {
$file_bytes = [System.IO.File]::ReadAllBytes($upload_file)
$response = Invoke-RestMethod -Uri "$baseUrl/transfer_file" -Headers $headers_ft -Method Patch -Body $file_bytes -ContentType "application/octet-stream"
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Host "File uploaded: $($response.result)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"result": "Success"
}
## [Complete file transfer](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#complete-file-transfer)

For uploading file we'll use **POST** `/vault_rest/transfer_file` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#postcomplete-file-transfer). For this transfer we need to sed some headers:

- `group_id` – The group transfer ID received from the **Initialize Group Transfer** step
- `file_id` – The file ID received from the **Initialize File Transfer** step

PowershellJsonCopy# Close file transfer
$headers_ft = @{
Authorization = "Bearer $token"
file_id = $file_id
group_id = $group_id
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer_file" -Headers $headers_ft -Method Post
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Host "File transfer closed: $($response.result)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"result": "Success"
}
## [Complete group transfer](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#complete-group-transfer)

For uploading file we'll use **POST** `/vault_rest/transfer` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#postcomplete-group-transfer). For this transfer we need to sed some headers:

- `group_id` – The group transfer ID received from the **Initialize Group Transfer** step

PowershellJsonCopy# Close group transfer
$headers_ft = @{
Authorization = "Bearer $token"
group_id = $group_id
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer" -Headers $headers_ft -Method Post
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Host "Group transfer closed: Success"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null,
"files": [
{
"file_id": "39826350e66d48f995e4e4febc4a809c",
"file_url": "http://localhost:8010/file/39826350e66d48f995e4e4febc4a809c",
"folder_url": "http://localhost:8010/files/personal/folder/2b41878d1643438984269dc43c1a9bd0",
"group_id": "712a41af19c542ef8fc1eaa3d6ac3fbf",
"status_url": "http://localhost:8010/file/status/39826350e66d48f995e4e4febc4a809c",
"web_url": "http://localhost:8010/file/39826350e66d48f995e4e4febc4a809c"
}
]
}
## [Conclusion](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#conclusion)

Process described in this document will upload one smaller file. To upload more files, repeat steps 2, 3, 4 for each file. In case of bigger files upload file in more chunks of around 10MB by repeating step 3.

## [Whole example](/docs/mdmft/v3.11.4/automated-file-transfer/api-upload-a-file#whole-example)

Here is whole ting on one place. Make sure to change configuration variable at the beginning of the code.

PowershellCopy### OPSWAT MetaDefender MFT - File upload example ###
# file to upload
$upload_file = "C:\Users\vagrant\Documents\Test\image.jpg"
# Configuration
$baseUrl = "http://localhost:8010/vault_rest"
$username = "username"
$password = "password"
# ========================================================= #
# Encode credentials using CRLF separator and Base64
$rawCreds = "$username`r`n$password"
$encodedCreds = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($rawCreds))
# grapgical header
Write-Host "#=============================================#"
Write-Host "| OPSWAT - MetaDefender Managed File Transfer |"
Write-Host "+---------------------------------------------+"
Write-Host "| https://www.opswat.com/ |"
Write-Host "#=============================================#"
# Step 1: Authenticate and get token
$authHeaders = @{
Authorization = "Basic $encodedCreds"
}
try {
$authResponse = Invoke-RestMethod -Uri "$baseUrl/authenticate" -Headers $authHeaders -Method Get
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
$token = $authResponse.token
Write-Host "Authenticated. Token: $token"
$headers = @{
Authorization = "Bearer $token"
}
# Initiate group transfer
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer" -Headers $headers -Method Get
#Write-Host ( $file | ConvertTo-Json | Out-String)
$group_id = $response.group_id
Write-Host "Group ID: $($response.group_id)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
# Initiate file transfer
# check if local file exists
if (Test-Path $upload_file) {
# Get file size
$file_size = (Get-Item $upload_file).Length
# Get file name
$file_name = Split-Path -Path $upload_file -Leaf
} else {
Write-Host "File does not exist."
exit
}
# Prepare headers
$headers_ft = @{
Authorization = "Bearer $token"
transfer_method = "Stream"
group_id = $group_id
file_name = $file_name
file_size = $file_size
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer_file" -Headers $headers_ft -Method Get
#Write-Host ( $file | ConvertTo-Json | Out-String)
$file_id = $response.file_id
Write-Host "File ID: $($response.file_id)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
#Upload files
# Prepare headers
$headers_ft = @{
Authorization = "Bearer $token"
file_id = $file_id
group_id = $group_id
}
try {
$file_bytes = [System.IO.File]::ReadAllBytes($upload_file)
$response = Invoke-RestMethod -Uri "$baseUrl/transfer_file" -Headers $headers_ft -Method Patch -Body $file_bytes -ContentType "application/octet-stream"
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Host "File uploaded: $($response.result)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
# Close file transfer
$headers_ft = @{
Authorization = "Bearer $token"
file_id = $file_id
group_id = $group_id
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer_file" -Headers $headers_ft -Method Post
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Host "File transfer closed: $($response.result)"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
# Close group transfer
$headers_ft = @{
Authorization = "Bearer $token"
group_id = $group_id
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/transfer" -Headers $headers_ft -Method Post
# Write-Host ( $response | ConvertTo-Json | Out-String)
Write-Host "Group transfer closed: Success"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
