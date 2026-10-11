<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex -->

# How can I export complete archive scan results from MetaDefender Core using the REST API (session_id + extraction APIs)?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V5 releases deployed on Windows systems.

### [Why this is needed](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#why-this-is-needed)

When scanning archives, the Core UI export may not include all archive-child details or the full set of extraction issues customers want to review. In those cases, you can authenticate via the REST API, then retrieve either (a) the top 100 extraction errors or (b) the full archive report including all extracted child files.

The examples below use PowerShell, Postman, and Linux curl, but none of these tools is mandatory. You can use any REST client that can send JSON requests and custom HTTP headers.

## [Prerequisites](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#prerequisites)

- MetaDefender Core base URL (for example `http(s)://<core-host>:<core-port>`)
- A local/LDAP/AD user that can log in via API (username + password)
- The **data_id** of the **parent archive** scan you want to report on (from scan history / prior submission).

## [Login to in and obtain the session_id](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#login-to-in-and-obtain-the-session_id)

### [What you get from Login](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#what-you-get-from-login)

`POST /login` returns a JSON response containing `session_id` (and `oms-csrf-token`). The `session_id` can be used as the `apikey` header for protected API calls.

---

## [PowerShell](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#powershell)

1. Set your Core URL and credentials:

$CoreUrl = "http://<core-host>:<core-port>"
$Username = "admin"
$Password = "admin"

2. Call **POST /login** and capture `session_id`:

$loginBody = @{ user = $Username; password = $Password } | ConvertTo-Json
$loginResp = Invoke-RestMethod -Method Post -Uri "$CoreUrl/login" -ContentType "application/json" -Body $loginBody
$sessionId = $loginResp.session_id
$sessionId
## [Postman](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#postman)

1. Create (or choose) an environment and add variables:

- `baseUrl` = `http://<core-host>:<core-port>`
- `user` = your username
- `password` = your password

2. Create a request:

- **Method:** `POST`
- **URL:** `{{baseUrl}}/login`
- **Headers:** `Content-Type: application/json`
- **Body (raw / JSON):**

{
"user": "{{user}}",
"password": "{{password}}"
}

3. In **Tests**, store the returned session:

pm.environment.set("session_id", pm.response.json().session_id);
## [Linux curl tool](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#linux-curl-tool)

1. Set your Core URL and credentials:

CORE_URL="https://<core-host>:<core-port>"
USERNAME="admin"
PASSWORD="admin"

2. Call `POST /login`:

curl -sS -X POST "$CORE_URL/login" \
-H "Content-Type: application/json" \
-d "{\"user\":\"$USERNAME\",\"password\":\"$PASSWORD\"}"

3. Copy the returned `session_id` value and store it in a shell variable:

SESSION_ID="<SESSION_ID>"

---

## [Fetch top 100 extraction errors inside an archive](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#fetch-top-100-extraction-errors-inside-an-archive)

This uses: **GET** `/file/{data_id}/extraction-errors` (described as “Fetch top 100 of extraction errors inside an archive”).

## [PowerShell](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#powershell)

1. Set the target archive `data_id`:

$dataId = "<PARENT_ARCHIVE_DATA_ID>"

2. Call the endpoint with the `apikey` header:

Invoke-RestMethod -Method Get `
-Uri "$CoreUrl/file/$dataId/extraction-errors" `
-Headers @{ apikey = $sessionId }
## [Postman](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#postman)

1. Add an environment variable:

- `data_id` = `<PARENT_ARCHIVE_DATA_ID>`

2. Create a request:

- **Method:** `GET`
- **URL:** `{{baseUrl}}/file/{{data_id}}/extraction-errors`
- **Headers:** `apikey: {{session_id}}`

3. Send → the response returns the extraction error list (top 100 per the endpoint description).

## [Linux curl tool](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#linux-curl-tool)

1. Set the target archive `data_id`:

DATA_ID="<PARENT_ARCHIVE_DATA_ID>"

2. Call the endpoint:

curl -sS -X GET "$CORE_URL/file/$DATA_ID/extraction-errors" \
-H "apikey: $SESSION_ID"
## [Fetch the full archive report including all extracted child files](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#fetch-the-full-archive-report-including-all-extracted-child-files)

This uses: **GET** `/archive/{data_id}` (described as “Fetch analysis reports containing all files in archive”).

## [PowerShell](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#powershell)

1. Set the target archive `data_id`:

$dataId = "<PARENT_ARCHIVE_DATA_ID>"

2. Call the endpoint with the `apikey` header:

Invoke-RestMethod -Method Get `
-Uri "$CoreUrl/archive/$dataId" `
-Headers @{ apikey = $sessionId }
## [Postman](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#postman)

- **Method:** `GET`
- **URL:** `{{baseUrl}}/archive/{{data_id}}`
- **Headers:** `apikey: {{session_id}}`

Send → the response returns the archive-level report including all files extracted/analyzed under that archive scan.

## [Linux curl tool](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#linux-curl-tool)

1. Set the target archive `data_id`:

DATA_ID="<PARENT_ARCHIVE_DATA_ID>"

2. Call the endpoint with the `apikey` header:

curl -sS -X GET "$CORE_URL/archive/$DATA_ID" \
-H "apikey: $SESSION_ID"
## [Notes and common pitfalls](/docs/mdcore/v5.22.1/knowledge-base/how-to-retrieve-a-complete-scan-report-for-archives-and-their-ex#notes-and-common-pitfalls)

- If you get an HTTP error code **403 (Forbidden) / 401 (Unauthorized)**, re-check that you are passing `apikey: <session_id>` (the `session_id` from `/login` is used as `apikey`).
- If you get an HTTP error code **404 (Not found)**, confirm the `data_id` is correct and still retained by your Core retention policy (older scan artifacts may have been purged).

####

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
