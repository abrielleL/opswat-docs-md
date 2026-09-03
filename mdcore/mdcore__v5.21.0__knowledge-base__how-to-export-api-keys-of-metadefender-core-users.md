<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-export-api-keys-of-metadefender-core-users -->

# How to export API Keys of MetaDefender Core users

MetaDefender Core provides remote integration and management capabilities through its REST API interface. To perform API operations, each user must have a configured API key with the appropriate privileges for the intended actions.

However, when multiple users access MetaDefender Core simultaneously—each with their own API key—it can become challenging to maintain an accurate record of all existing keys.

To address this, the [**GET /admin/user**](https://www.opswat.com/docs/mdcore/metadefender-core#userlist) API endpoint can be used to retrieve a complete list of users within MetaDefender Core, along with their associated details. This allows administrators to programmatically process the response and identify all users who possess an API key.

Furthermore, by leveraging the [**GET /admin/userdirectory**](https://www.opswat.com/docs/mdcore/metadefender-core#userdirectorylist) API endpoint, it is possible to list all available user directories. This enables correlation between users and their respective directories, providing a clearer and more organized overview of user management within MetaDefender Core.

Below is a PowerShell script that retrieves and displays all existing users configured with an API key in MetaDefender Core. The output is presented in the following structured format:

| **USER** | **API KEY** |
| --- | --- |
| DIRECTORY\user | <api key> |

**Notes:**

- Replace `$apiKey` and `$coreUrl` with your actual MetaDefender Core credentials and instance URL.
- To export the results to a CSV file, **uncomment the last line** and provide a valid file path and name (for example: `C:\Reports\MetaDefender_Users_APIKeys.csv`).

# ---- TLS + SKIP CERT CHECK ----
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
Add-Type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
public bool CheckValidationResult(
ServicePoint srvPoint, X509Certificate certificate,
WebRequest request, int certificateProblem) { return true; }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
# ---- CONFIG ----
$apiKey = "Admin API KEY"
$coreUrl = "MD CORE URL"
# ---- FETCH DATA ----
$users = Invoke-RestMethod -Uri "$coreUrl/admin/user" -Headers @{ apikey = $apiKey } -Method GET
$directories = Invoke-RestMethod -Uri "$coreUrl/admin/userdirectory" -Headers @{ apikey = $apiKey } -Method GET
# Build directory lookup
$dirLookup = @{}
foreach ($dir in $directories) {
$dirLookup[$dir.id] = $dir.name
}
# ---- BUILD OUTPUT (only users with API keys) ----
$result = foreach ($u in $users | Where-Object { $_.api_key }) {
$directoryName = $dirLookup[$u.directory_id]
[PSCustomObject]@{
User = "$directoryName\$($u.name)"
ApiKey = $u.api_key
}
}
# ---- DISPLAY ----
$result | Format-Table -AutoSize
# ---- OPTIONAL EXPORT TO CSV ----
# $result | Export-Csv "User_ApiKey_List.csv" -NoTypeInformationSupport:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
