<!-- source: https://www.opswat.com/docs/mdcloud/integrations/rate-limiting -->

# Rate Limiting

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

While communicating with MetaDefender Cloud APIs, you will need to use the authentication mechanism for the given API endpoint and provide your apikey. Each apikey has daily limits, and you can check yours by logging in to [MetaDefender Cloud](https://metadefender.opswat.com/) with your OPSWAT account credentials. Additionally, the MetaDefender Cloud server returns custom headers in each response that will help you track your current API usage.

If you don't have an apikey, see our guide: [Onboarding Process for MetaDefender Cloud API Users](/docs/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users)

Each MetaDefender Cloud apikey has limits for each family of APIs (Prevention, Reputation, etc.), and every response from MetaDefender Cloud contains custom headers that inform clients about the current limits.

## [Description of Custom Headers](/docs/mdcloud/integrations/rate-limiting#description-of-custom-headers)

- X-RateLimit-Limit - Your current limit for a given family of APIs.
- X-RateLimit-Remaining - The number of requests remaining in the current time window, usually set to 24 hours.
- X-RateLimit-Reset-In - The number of seconds remaining in the current time window.
- X-RateLimit-Used - The number of requests used in the current time window.

## [Custom Header Example](/docs/mdcloud/integrations/rate-limiting#custom-header-example)

> curl -vvvv "https://api.metadefender.com/v4/hash/64638C3FF08EEC********708CF5B5F111C05E3D" -H 'apikey: YOUR_API_KEY'
> GET /v4/hash/64638C3FF08E********24708CF5B5F111C05E3D HTTP/1.1
> Host: api.metadefender.com
> User-Agent: curl/7.52.1
> Accept: */*
> apikey: YOUR_API_KEY
>
* Connection state changed (MAX_CONCURRENT_STREAMS updated)!
< HTTP/2 200
< date: Mon, 11 May 2020 09:41:18 GMT
< content-type: application/json; charset=utf-8
< content-length: 5280
< vary: Accept-Encoding, Origin
< x-authenticated: by apikey
< x-account-type: other
< x-ratelimit-for: reputation_api
< x-ratelimit-limit: 4000
< x-ratelimit-used: 1
< x-ratelimit-remaining: 3999
< x-ratelimit-reset-in: 86400s
< x-ratelimit-interval: 86400
< x-redis-partial-cache: true
< x-content-type-options: nosniff
< etag: "14a0-xGmnaISdKYosJha3G+h2JjEfaQg"
< x-response-time: 330ms
## [Exceeding Allowed Rate Limit](/docs/mdcloud/integrations/rate-limiting#exceeding-allowed-rate-limit)

When the rate limit is exceeded (user performing more requests per day than their license limits) an HTTP 429 code is returned with the following body:

{
"error": {
"code": 429000,
"messages": [
"Rate limit exceeded, retry after the limit is reset. Limit: 100 requests / day"
]
}

The limit is reset after 24 hours from the first request. For example, if an apikey starts calling the API at 11:00 AM and finishes up the rate limit by 22:00 PM, the rate limit will be reset the next day at 11:00 AM.

## [Rate Limiting](/docs/mdcloud/integrations/rate-limiting#rate-limiting)

**Limit families.** Each API key has a separate limit for each family of APIs: Prevention (file analysis), Reputation (hash, IP, URL and domain lookups), Sandbox (dynamic analysis), Download (file downloads), Feed (threat intelligence feeds) and Threat Intelligence Search. `GET /v4/apikey/limits/status` returns what remains of each. The `X-RateLimit-For` response header tells you which family a request was counted against.

**Daily and monthly intervals.** Limits are counted per day or per month depending on your plan. `X-RateLimit-Reset-In` tells you how many seconds remain in the current interval.

##### [**Prevention limit**](/docs/mdcloud/integrations/rate-limiting#prevention-limit)

**One file, one call.** Submitting a file consumes one unit of your Prevention limit, whatever combination of Multiscanning, Deep CDR, Proactive DLP and Country of Origin the workflow runs. Deep CDR does not consume a second unit.

**Archives.** When you ask for archive extraction (`rule: unarchive` or a workflow with extraction enabled), every file extracted from the archive consumes one unit, and the archive itself consumes one. Nested archives are extracted and counted the same way. If the file is not an archive, only one unit is consumed.

Examples:

- An archive submitted without extraction: 1 unit.
- An archive with 40 files, with extraction: 41 units.
- An archive with 10 files, one of which is an archive holding 5 files, with extraction: 16 units.

If any file inside an archive is infected, the archive is reported as infected even when no engine detects anything in the archive file itself.

**Sanitized files.** The sanitized version of a file is not rescanned and does not consume a unit. If you want the sanitized version analysed again, submit it as a new file.

**Rejected requests.** A request refused with a 4xx error, for example a malformed request or a file over your size limit, does not consume a unit. A request that fails with a 5xx error does.

##### [**Sandbox limit**](/docs/mdcloud/integrations/rate-limiting#sandbox-limit)

- Each file analysed by Adaptive Sandbox consumes one unit of your Sandbox limit.
- When an archive is extracted, each extracted file that is sent to the sandbox consumes one unit as its analysis completes. If your remaining Sandbox allowance covers only some of the extracted files, only those files are analysed; when it is exhausted, the scan reports that limits were exceeded and the extracted-file details are omitted.
- Each file scanned with the Aether workflow consumes one Sandbox unit, charged when the request is accepted. A scan that reaches a definitive verdict early is charged the same as a full run.
- A sandbox request refused with a 4xx error consumes nothing; `X-RateLimit-Used` reads 0 on such a response.

##### [**Download limit**](/docs/mdcloud/integrations/rate-limiting#download-limit)

Downloading a file with `GET /v4/file/{hash}/download` consumes one unit of your Download limit.
