<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/automated-file-transfer/api-authentication -->

# API - Hello world! - Authentication

Summarize Page    Connect to Cursor Connect to VS Code
## [Hello World: Getting Started with MetaDefender MFT API in PowerShell](/docs/mdmft/v3.11.4/automated-file-transfer/api-authentication#hello-world-getting-started-with-metadefender-mft-api-in-powershell)

Welcome to the first step in integrating with the **OPSWAT MetaDefender Manage File Transfer (MFT) API**. This simple "Hello World!" example demonstrates how to authenticate with the API and retrieve the current version of your MFT instance using PowerShell.

Whether you're evaluating the API or preparing for deeper integration, this example provides a quick and practical starting point. You'll learn how to:

- [Set up basic authentication using an API key](https://www.opswat.com/docs/mdmft/metadefender-mft#getrequest-an-api-key)
- [Send a request to the /version endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getversion)
- Parse and display the response

This is a great way to verify connectivity and ensure your credentials are working correctly before diving into more advanced operations like file scanning, policy enforcement, or audit logging.

Let’s get started!

## [Set Up Your API Endpoint and Credentials](/docs/mdmft/v3.11.4/automated-file-transfer/api-authentication#set-up-your-api-endpoint-and-credentials)

Before making any requests, you’ll need to configure your script with the correct API endpoint. Replace the placeholder URL with the actual address of your MetaDefender MFT instance.

In our example we used: <http://localhost:8010/vault_rest>

Update the **username** and **password** with your own credentials.

The next PowerShell snippet demonstrates how to obtain an authentication token from [/authenticate endpoint](https://www.opswat.com/docs/mdmft/metadefender-mft#getrequest-an-api-key). This token is required for all subsequent API requests and ensures secure access to the MFT services.

PowershellCopy# Configuration
$baseUrl = "http://localhost:8010/vault_rest"
$username = "YourUsername"
$password = "YourPassword"
# Encode credentials using CRLF separator and Base64
$rawCreds = "$username`r`n$password"
$encodedCreds = [Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes($rawCreds))
# Step 1: Authenticate and get token
$authHeaders = @{
Authorization = "Basic $encodedCreds"
}
try {
$authResponse = Invoke-RestMethod -Uri "$baseUrl/authenticate" -Headers $authHeaders -Method Get
} catch { # In case of authentication error
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
$token = $authResponse.token
Write-Host "Authenticated. Token: $token"
## [Using the Authentication Token](/docs/mdmft/v3.11.4/automated-file-transfer/api-authentication#using-the-authentication-token)

Once you've successfully authenticated, you'll receive an **auth token**. This token must be included in the `Authorization` header of all subsequent API requests, using the following format:

`Authorization = "Bearer $token"`

To retrieve the current version of MetaDefender MFT, send a **GET** request to the `/version` endpoint.

Each server response includes two components:

- **HTTP status code** – indicating the result of the request (e.g., 200 for success). [More on Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
- **Response body** – returned in JSON format, containing the requested data. More on [API Documentation](https://www.opswat.com/docs/mdmft/metadefender-mft#getversion)

You can refer to the API documentation for a complete list of response codes and expected content for each endpoint.

PowershellCopy# Step 2: Get version number
try {
$listResponse = Invoke-RestMethod -Uri "$baseUrl/version" -Headers $headers -Method Get
# Display MFT Version
Write-Host "MetaDefender MFT ver:$($listResponse.version)"
} catch { # error response
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
# Display MFT Version
Write-Host "MetaDefender MFT ver:$($listResponse.version)"
## [Whole Script](/docs/mdmft/v3.11.4/automated-file-transfer/api-authentication#whole-script)

PowershellCopy# Configuration
$baseUrl = "http://localhost:8010/vault_rest"
$username = "YourUsername"
$password = "YourPassword"
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
} catch { # In case of authentication error
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
$token = $authResponse.token
Write-Host "Authenticated. Token: $token"
# Step 2: Get version number
$headers = @{
Authorization = "Bearer $token"
}
try {
$response = Invoke-RestMethod -Uri "$baseUrl/version" -Headers $headers -Method Get
# Display MFT Version
Write-Host "MetaDefender MFT ver:$($response.version)"
} catch { # error response
Write-Host "Error Status Code: $($_.Exception.Response.StatusCode.Value__)"
Write-Host "Error Message: $($_.Exception.Message)"
return
}
