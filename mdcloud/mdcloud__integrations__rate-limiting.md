<!-- source: https://www.opswat.com/docs/mdcloud/integrations/rate-limiting -->

# Rate Limiting

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

## [Prevention API Rate Limiting](/docs/mdcloud/integrations/rate-limiting#prevention-api-rate-limiting)

### [Multiscanning Rate Limit](/docs/mdcloud/integrations/rate-limiting#multiscanning-rate-limit)

- When a file is uploaded for multiscanning, the limit is subtracted by 1.
- When an archive is uploaded for multiscanning, and the user requests an unarchiving, every file inside the archive will be extracted and scanned up to the license limit (see the [licensing](https://metadefender.opswat.com/licensing) page for details).
- If the uploaded archive contains embedded archives and unarchiving was requested by the user, the embedded archive is also extracted and the files inside are scanned.
- Every file extracted and scanned from archives is counted as a separate file and the daily limit will be deducted with the total number of files inside the archive plus one because the archive itself is scanned and counted as an individual file. This rule also applies for embedded archives.
- If the uploaded file is not an archive but the `unarchiving` header is sent (rule: `unarchive` ) the file will not be unarchived and the limit will be subtracted by 1.

**For Example:**

- When uploading an archive without `unarchiving` header, only the archive itself will be scanned as an individual file and the rate limit will be subtracted by one
- When uploading an archive with 40 files inside with the `unarchiving` header, the rate limit will be subtracted by 41 (40 files inside + the archive itself)
- When uploading an archive with 10 files inside with the `unarchiving` header, and one of the 10 files is also an archive with 5 files, the rate limit will be subtracted by 16 (10 files + 5 files in the embedded archive + the archive itself)

Info

**If there is at least one infected file inside the archive, the scan results of the archive will be marked as infected, even if the archive itself is not detected as infected by any engine.**

### [Deep CDR Rate Limit](/docs/mdcloud/integrations/rate-limiting#deep-cdr-rate-limit)

- When a file is uploaded and the Deep CDR header is sent (rule: `sanitize` ), if the file format is supported by Deep CDR, the limit is subtracted by two: one for Multiscanning and one for the Deep CDR analysis
- When an archive is uploaded with the header rule `multiscan_sanitize_unarchive`, every sanitizable file inside the archive will be sanitized. In addition to the scanned files, the limit will be subtracted by one for every file sanitized inside the archive
- If the original file is infected, the sanitized version of the file will be scanned using multiscanning free of charge to prove no infection is detected

## [Reputation API rate limiting](/docs/mdcloud/integrations/rate-limiting#reputation-api-rate-limiting)

### [Not Found Results](/docs/mdcloud/integrations/rate-limiting#not-found-results)

- When a hash lookup returns not found it is subtracted from the limit at a ratio of 5:1 (for every 5 hashes not found, 1 is subtracted from your rate limit).

**For Example**:

- If doing 20 hash lookups, and only 10 of them return results (known hashes), the limit will be subtracted by 12 (10 found hashes + 2 times 5 not found hashes)

### [Bulk Lookups](/docs/mdcloud/integrations/rate-limiting#bulk-lookups)

- When doing a bulk hash lookup request, the limit is subtracted for every successful response
- Before doing the lookup on our backend, we eliminate duplicate hashes to avoid subtracting the limit for the same hash multiple times
- The not found hashes are subtracted at a ratio of 5:1

**For Example:**

- Doing a bulk hash lookup for 20 hashes, where only 10 are found in our database, the limit will be subtracted by 12 (10 found hashes + 2 times 5 not found hashes)
