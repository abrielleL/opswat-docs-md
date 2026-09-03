<!-- source: https://www.opswat.com/docs/mdmft/automated-file-transfer/api-list-my-files-and-folders -->

# API - List my files and folders

Summarize Page    Connect to Cursor Connect to VS Code

After authenticating with the OPSWAT Managed File Transfer API, you can interact with your files and folders. This section covers:

- List root folder contents
- List subfolder contents

## [Listing files and folders](/docs/mdmft/automated-file-transfer/api-list-my-files-and-folders#listing-files-and-folders)

We'll assume that you have some files and folders already upload from UI. If you don't do this step first so you'll be able to test your code. To list folder you need to to use `/vault_rest/folder_content/{id}/{start}/{count}` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getenumerate-folder-content). You'll notice `{id}` that refers to `folder_id`, therefore first step is to get `folder_id`of your root folder.

In our next example we'll get our root folder ID using `/vault_rest/root_folder` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getget-root-folder). We assume you already successfully authenticate using instructions from our **Hello World** example.

Example of expected response:

JsonCopy{
"availability_state": "Available",
"can_update_sharing": true,
"folder_id": "755d264f42d146d29641594c689ccb16",
"name": "",
"owner": "John Doe",
"owner_id": 1,
"path": "",
"folder_path_list": [
{
"availability_state": "Available",
"can_update_sharing": true,
"folder_id": "755d264f42d146d29641594c689ccb16",
"name": "",
"owner": "John Doe",
"owner_id": 1,
"path": ""
}
]
}

We will find root folder ID in value of `$response.folder_id` of our response object. We'll use this value to in our next call to list folder.

PowershellCopy# Step 2: Get ID of root folder
try {
$response = Invoke-RestMethod -Uri "$baseUrl/root_folder" -Headers $headers -Method Get
# Display Root folder ID
$root_folder_id = $response.folder_id
Write-Host "Root folder ID: $root_folder_id"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}

Now that we’ve successfully retrieved our root folder ID, we can use it to list all files and folders it contains. Each listed item will include its own ID, which can be used to further list contents or perform actions on those specific files and folders.

To list our root folder we'll use

- **{id}** - folder ID, in this case root folder ID `/vault_rest/folder_content/{id}/{start}/{count}` [endpoint](/docs/mdmft/vault_rest/folder_content/%7Bid%7D/%7Bstart%7D/%7Bcount%7D).
- **{start}** - integer number of starting file in list. 0 is for starting form fist file
- **{count}** - number of files listed. We'll use 15 in this example.

PowershellCopy# Step 3: List files and folders of root folder
try {
$response = Invoke-RestMethod -Uri "$baseUrl/folder_content/$root_folder_id/0/15" -Headers $headers -Method Get
# Display Root folder
# Write-Output $response
$response.folders | ForEach-Object {
Write-Output "ID: $($_.folder_id) | Folder: $($_.name)"
}
$response.files | ForEach-Object {
Write-Output "ID: $($_.file_id) | File: $($_.name.padRight(15)) | Size: $($_.size.toString().padLeft(10)) | Created: $($_.creation_date)"
}
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}

Now you can list any subfolder content by replacing root folder ID with one of folder IDs you just listed.
