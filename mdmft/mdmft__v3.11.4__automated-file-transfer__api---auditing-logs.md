<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/automated-file-transfer/api---auditing-logs -->

# API - Auditing logs

Summarize Page    Connect to Cursor Connect to VS Code
## [Display auditing logs](/docs/mdmft/v3.11.4/automated-file-transfer/api---auditing-logs#display-auditing-logs)

We can use **GET** `vault_rest/audit/{start}/{count}` [endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getenumerate-audit-events) to fetch and search audit logs.

`start`- starting record to return

`count`- number of records to return

`sort_column`= Name of column to use when sorting data

`sort_direction`= Sorting direction

`find`= Free text search string

`findB64`= Free text search string (Base64 encoded)

PowershellResponseCopytry {
$headers = @{
Authorization = "Bearer $token"
sort_column = "Name of column to use when sorting data"
sort_direction = "Sorting direction"
find = "Free text search string"
findB64 = "Free text search string (Base64 encoded)"
}
$response = Invoke-RestMethod -Uri "$baseUrl/audit/0/5" -Headers $headers -Method Get
# Prints output as JSON object
Write-Host ( $response | ConvertTo-Json | Out-String)
# Prints output as Table
Write-Output $response.items | Select-Object date, location, event, status, user, description | Format-Table -AutoSize
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}{
"filter_count": 2814,
"items": [
{
"audit_id": 14037,
"date": "2025-10-02T13:39:53.0200000",
"description": "milutin logged on.",
"event": "Logon",
"location": "127.0.0.1",
"status": "Success",
"user": "milutin"
},
{
"audit_id": 14036,
"date": "2025-10-02T13:39:37.9100000",
"description": "milutin logged on.",
"event": "Logon",
"location": "127.0.0.1",
"status": "Success",
"user": "milutin"
},
{
"audit_id": 14035,
"date": "2025-10-02T13:39:36.0030000",
"description": "File image.jpg could not be permanently deleted.",
"event": "File Purged",
"location": "172.22.201.15",
"status": "Failure",
"user": "System"
},
{
"audit_id": 14034,
"date": "2025-10-02T13:38:50.3000000",
"description": "milutin logged on.",
"event": "Logon",
"location": "127.0.0.1",
"status": "Success",
"user": "milutin"
},
{
"audit_id": 14033,
"date": "2025-10-02T13:38:35.9630000",
"description": "File image.jpg could not be permanently deleted.",
"event": "File Purged",
"location": "172.22.201.15",
"status": "Failure",
"user": "System"
}
],
"total_count": 2814
}
## [Export auditing logs](/docs/mdmft/v3.11.4/automated-file-transfer/api---auditing-logs#export-auditing-logs)

PowershellCopytry {
$headers = @{
Authorization = "Bearer $token"
}
$response = Invoke-RestMethod -Uri "$baseUrl/audit/export" -Headers $headers -Method Get -OutFile "C:\Users\user\Documents\audit.csv"
} catch {
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
