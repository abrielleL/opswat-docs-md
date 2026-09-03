<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share -->

# API - Rename, move, delete, share

Summarize Page    Connect to Cursor Connect to VS Code

In this segment we are going to give you some examples of basic operations on files and folders

## [Create folder](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#create-folder)

To rename file we use **POST** `/vault_rest/folder` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#postcreate-a-folder).

In request body we need to send to parameters.

`name` - name of the folder you would like to create

`path` - path to place where you would like to create folder

PowershellResponseCopytry {
$body = @{
name = "new folder"
path = "folder1\folder2"
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/folder" -Headers $headers -Body $body -Method Post
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null,
"folder_guid": "149b1fb04c3c456bba805dbbd2008c94",
"folder_name": "new folder"
}
## [Rename file](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#rename-file)

To rename file we use **PUT** `/vault_rest/rename_file` [endoint](https://www.opswat.com/docs/mdmft/metadefender-mft#putrename-a-file).

In request body we need to send to parameters.

`file_id` - ID of file we plan to rename

`new_file_name` - String with new file name

PowershellResponseCopytry {
$body = @{
file_id = "ac7eac70bbd64a1ca646ac288e9978af"
new_file_name = "image_new.jpg"
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/rename_file" -Headers $headers -Body $body -Method Put
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null
}
## [Rename folder](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#rename-folder)

To rename folder we'll use **PUT** `/vault_rest/rename_folder` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#putrename-a-folder).

`folder_id` - ID of file we plan to rename

`new_folder_name` - String with new file name

PowershellResponseCopytry {
$body = @{
folder_id = "ac7eac70bbd64a1ca646ac288e9978af"
new_folder_name = "folder_new"
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/rename_folder" -Headers $headers -Body $body -Method Put
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null
}
## [Delete file](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#delete-file)

To delete file we'll use **DELETE** `/vault_rest/file/{file_id}` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#deletedelete-a-file).

PowershellResponseCopytry {
$response = Invoke-RestMethod -Uri "$baseUrl/file/ac7eac70bbd64a1ca646ac288e9978af" -Headers $headers -Method Delete
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null
}
## [Delete folder](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#delete-folder)

To delete file we'll use **DELETE** `/vault_rest/folder/{folder_id}`[endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#deletedelete-a-folder).

PowershellResponseCopytry {
$response = Invoke-RestMethod -Uri "$baseUrl/folder/ac7eac70bbd64a1ca646ac288e9978af" -Headers $headers -Method Delete
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null
}
## [Move a file](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#move-a-file)

To move files use **PUT** `/vault_rest/v2/move_files`[endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#putmove-a--file).

files- List of files to move

`file_id`- ID of file we plan to move

`name` - String with new file name

`new_path` - Destination to move files to

PowershellResponseCopytry {
$body = @{
files = @(
@{
folder_id = "c5133a2deb5a4f4798b45731cc1bcda9"
name = "image001.jpg"
},
@{
folder_id = "433beb56d2c94effb24bccdce6823a7b"
name = "image002.jpg"
},
@{
folder_id = "4db39640b3ef4f068b66ead001f5bbd2"
name = "image003.jpg"
}
)
new_path = "test\folder2"
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/v2/move_file" -Headers $headers -Body $body -Method Put
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"successful_results": {
"entities": [
{}
],
"success_counter": 1
},
"failed_results": {
"entities": [],
"failed_counter": 0
},
"total_counter": 1
}
## [Move a folder](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#move-a-folder)

To move files use **PUT** `/vault_rest/v2/move_folders`[endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#putmove-folders).

`folders` - List of folders to move

`folder_id`- IDs of folders we plan to move

`name` - String with new folder name

`new_path` - Destination to move files to

PowershellResponseCopytry {
$body = @{
folders = @(
@{
folder_id = "c5133a2deb5a4f4798b45731cc1bcda9"
name = "folder3"
path = "test\folder3"
},
@{
folder_id = "433beb56d2c94effb24bccdce6823a7b"
name = "folder2"
path = "test\folder2"
},
@{
folder_id = "4db39640b3ef4f068b66ead001f5bbd2"
name = "folder1"
path = "test\folder1"
}
)
new_path = ""
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/v2/move_folder" -Headers $headers -Body $body -Method Put
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"successful_results": {
"entities": [
{}
],
"success_counter": 1
},
"failed_results": {
"entities": [
{
"message": "The destination folder already contains a folder with the same name",
"ui_message_key": "API_FOLDER_MOVE_DESTINATION_HAS_FOLDER_WITH_SAME_NAME"
}
],
"failed_counter": 1
},
"total_count": 2
}
## [Share a file](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#share-a-file)

To move files use **PUT** `/vault_rest/upload_file_share`[endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#postshare-a-file).

`fileId` - ID of file you would like to share

`groupIds` - List of user group IDs

`userIds` - List of user group IDs

PowershellResponseCopytry {
$body = @{
fileId = "849137c80bd443cca3c49328f4a32fe9"
groupIds = @(19, 23, 65)
userIds = @(24, 66, 59)
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/update_file_share" -Headers $headers -Body $body -Method Post
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null
}
## [Share a folder](/docs/mdmft/v3.11.4/automated-file-transfer/api-rename-move-delete-share#share-a-folder)

To move files use **PUT** `/vault_rest/upload_folder_share`[endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#postshare-a-folder).

`folderId` - ID of file you would like to share

`groupIds` - List of user group IDs

`userIds` - List of user group IDs

PowershellResponseCopytry {
$body = @{
folderId = "849137c80bd443cca3c49328f4a32fe9"
groupIds = @(19, 23, 65)
userIds = @(24, 66, 59)
} | ConvertTo-Json
$response = Invoke-RestMethod -Uri "$baseUrl/update_folder_share" -Headers $headers -Body $body -Method Post
Write-Output $response | ConvertTo-Json
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"message": null,
"ui_message_key": null
}
